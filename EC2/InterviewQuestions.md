## Amazon EC2 instances in a development environment run between 9 am and 5 pm Monday-Friday. Production instances run 24/7. Which pricing models should be used? (Select TWO)

        Spot instances for the development environment
        Reserved instances for the development environment
        Scheduled reserved instances for the development environment
        Reserved instances for the production environment
        On-Demand instances for the production environment
        
**Explanation:** 

Scheduled Instances are a good choice for workloads that do not run continuously but do run on a regular schedule. This is ideal for the development environment. Reserved Instances are a good choice for workloads that run continuously. This is a good option for the production environment.

INCORRECT: “Spot instances for the development environment” is incorrect. Spot instances are a cost-effective choice if you can be flexible about when your applications run and if your applications can be interrupted. Spot instances are not suitable for the development environment as important work may be interrupted.

INCORRECT: “Reserved instances for the development environment” is incorrect as they should be used for the production environment.

CORRECT: “Scheduled reserved instances for the development environment” is a correct answer.

CORRECT: “Reserved instances for the production environment” is also a correct answer.

INCORRECT: “On-Demand instances for the production environment” is incorrect. There is no long-term commitment required when you purchase On-Demand Instances. However, you do not get any discount, and therefore this is a very expensive option.    

