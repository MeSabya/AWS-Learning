# S3 MultiPart upload

Uploading files to S3 is a common task that developers often encounter. While for most use cases a simple PUT request to S3 would get the job done.

However, if you want to upload large files or want more flexibility with your uploads you might want to try out multipart uploads.

Note: With normal S3 uploads we can upload a maximum of 5GB with a single request, if you want to upload files greater than this, you must use multipart S3 upload.

A multipart upload operation to S3 consists of 3 distinct steps…

### Multipart upload initiation
The first step is to send a request to S3 to initiate the multipart upload. S3 returns an upload ID in the response which is a unique identifier for our multipart upload request. In later steps,
we can make use of this Id to upload the individual parts and finalize our upload.

### Uploading individual parts
Now that we have initiated the multipart upload request and obtained the upload ID we can start uploading individual parts to S3.

When uploading each part we must specify a Part number in addition to the upload ID.

Some points to remember:

Part numbers may not be consecutive this means you can upload parts in any order.
A part number can range between 1 to 10000. ( S3 allows a maximum of 10000 parts in a multipart upload request)
On successfully uploading a part S3 will respond back with an ETag in the response. You must save the ETags and their corresponding part numbers since this will be required later to complete the multipart upload request.

### Finalizing the upload

Once we have uploaded all the parts to S3 we need to finalize the upload so that S3 creates an object by concatenating all the parts in ascending order based on the part number.


