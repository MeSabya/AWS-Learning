## S3 object lock 

### Retention Periods:

There are two types of retention periods you can set: Legal Hold and Retention Period with Retention Mode.

#### Legal Hold: 
It allows you to place a legal hold on an object, which protects it from deletion or modification regardless of the object's retention settings. This is useful for situations where you want to preserve data for legal or compliance reasons.

#### Retention Period with Retention Mode: 
This is the more traditional Object Lock feature. You set a retention period (e.g., 30 days) and choose a retention mode, either COMPLIANCE or GOVERNANCE.

COMPLIANCE mode enforces the retention period and cannot be shortened. Once set, objects cannot be deleted or modified until the retention period expires.

GOVERNANCE mode also enforces the retention period, but you can shorten or remove the retention period if needed, provided you have the necessary permissions.

### Setting Object Lock:

Object Lock can be configured at the bucket or object level. To enable Object Lock on a bucket, you need to add a bucket-level retention configuration. To enable Object Lock on individual objects, you need to include Object Lock parameters when uploading or copying objects.
