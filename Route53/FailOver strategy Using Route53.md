# How to implement the perfect failover strategy using Amazon Route53

## The setup

Every application should run in at least two regions for high-availability and fault-tolerance. This should also be an active-active architecture, rather than active-passive. In an active-active system, all regions are used at the same time, whereas in active-passive a back-up region is only used in a failure scenario.
So, let’s draw an architecture diagram to show what we intend to achieve.

![image](https://user-images.githubusercontent.com/33947539/154247465-1be26ebc-667a-43c7-87a5-ce78cdcb0698.png)

We have our application running in any number of AWS regions, with a load balancer as the entry-point. We want Route53 to work as a kind of “pre-load balancer” to distribute requests and point users to the correct region.

## Route53 Routing Policies

- **Simple routing policy**: Point a domain to a single, simple resource. It does not support Route53 Health checks.
- **Failover routing policy**: Designed for active-passive failover. Uses a simple policy unless it’s unhealthy, where it’ll use the backup.
- **Geolocation routing policy**: Route traffic based on the country or continent of your users.
- **Geoproximity routing policy**: Route traffic based on the physical distance between the region and your users.
- **Latency routing policy**: Route traffic to the AWS region that provides the best latency.
- **Multivalue answer routing policy**: Respond to DNS queries with up to eight healthy records selected at random.
- **Weighted routing policy**: Route traffic to resources in proportions that you specify.

### Latency-based routing

The application we’re building has no geographic requirements, so we can use latency routing. So how do we set it up?
To use latency-based routing, a record set needs to be created for each region the application is hosted in. Here’s how to set up basic latency routing using Terraform:

```terraform
resource "aws_route53_record" "latency-use1" {
  zone_id         = "${data.aws_route53_zone.my_zone.zone_id}"
  name            = "my-application"
  type            = "A"
  set_identifier  = "service-us-east-1"

  alias {
    zone_id                = "${aws_lb.main_us_east_1.zone_id}"
    name                   = "${aws_lb.main_us_east_1.dns_name}"
    evaluate_target_health = true
  }

  latency_routing_policy {
    region = "us-east-1"
  }
}

resource "aws_route53_record" "latency-euc1" {
  zone_id         = "${data.aws_route53_zone.my_zone.zone_id}"
  name            = "my-application"
  type            = "A"
  set_identifier  = "service-eu-central-1"

  alias {
    zone_id                = "${aws_lb.main_eu_central_1.zone_id}"
    name                   = "${aws_lb.main_eu_central_1.dns_name}"
    evaluate_target_health = true
  }

  latency_routing_policy {
    region = "eu-central-1"
  }
}

```
***Latency-based routing is the approximate latency between the user and the AWS region — NOT the user and your service!***

👉 For failover to occur, the whole region must be considered unhealthy, by which time users will have experienced degraded performance.
Why does this happen? Route53 will continue to route requests until the region is detected as unhealthy, regardless of service latency. In our case, that only happened when all hosts in our load balancer were unhealthy because evaluate_target_health was set to true. The results would have been even worse without evaluating the target health, eu-central-1 would never have been detected as unhealthy by Route53, causing a major outage.


#### The solution
Route53 provides a fantastic solution to this problem. Health checks allow DNS failover to be triggered by CloudWatch alarms. This means that we have full control over when Route53 fails over to another region — we can fine-tune it to our needs.

👉 *Health checks can also be configured to monitor an endpoint by polling it, but your service could be performing badly and still respond to the health check requests.*

```teraform
resource "aws_route53_health_check" "latency" {
  type                            = "CLOUDWATCH_METRIC"
  cloudwatch_alarm_name           = "${aws_cloudwatch_metric_alarm.latency.alarm_name}"
  cloudwatch_alarm_region         = "${var.region}"
  insufficient_data_health_status = "Healthy"

  tags = {
    Name = "high-latency"
  }
}
```
#### Limitations
we found two major limitations:

1. **No support for percentiles**:
   Route53 cannot use CloudWatch alarms with extended statistics so we can only trigger a failover based on minimum, average, or maximum latency.
   
2. **No support for expressions**:
   Expressions allow us to perform calculations on metrics, which means we can have CloudWatch alarms that trigger when the error rate exceeds a certain percentage, rather than simply monitoring the total number of errors.
   
```teraform
resource "aws_cloudwatch_metric_alarm" "alb_error_rate" {
  alarm_name          = "${aws_lb.main.name}-alb-error-rate"
  comparison_operator = "GreaterThanOrEqualToThreshold"
  evaluation_periods  = 2
  threshold           = 5
  alarm_description   = "Load balancer error rate has exceeded 5%"
  treat_missing_data  = "notBreaching"

  metric_query {
    id          = "error_rate"
    expression  = "5xx_count / request_count *100"
    label       = "Error Rate"
    return_data = true
  }

  # metric queries for 5xx_count and request_count...
}
```

When attempting to create a Route53 Health Check which is triggered by a CloudWatch alarm using expressions, the AWS API returns an internal server error.

Hopefully, AWS will add support for percentile and expression CloudWatch alarms soon. Once that’s completed, we can change our health checks to suit our requirements perfectly:
                
                CPU is critically high
                High % of 5xx errors
                High % of target connection errors
                High P99 latency
















