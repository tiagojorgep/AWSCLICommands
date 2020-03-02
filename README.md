# AWSCLICommands
Contain AWS CLI commons commands<br />
For complete AWS CLI documentation follow: [AWS CLI Command Reference](https://docs.aws.amazon.com/cli/latest/index.html)

S3 Commands
-------------

**Clear Bucket**<br />
Remove all content in a S3 Bucket
```sh
$ aws s3 rm s3://<bucket-name> --recursive
```

**Sync Bucket**<br />
Sync all content into a folder to a S3 Bucket
```sh
$ aws s3 sync <folder-path> s3://<bucket-name>
```

**Sync Bucket with public read access**<br />
Sync all content into a folder to a S3 Bucket granting public read access
```sh
$ aws s3 sync <folder-path> s3://<bucket-name> --acl public-read
```

CloudFront Commands
-------------
**List distribution**<br />
List all cloudfront distributions
```sh
$ aws cloudfront list-distributions
```

**Create invalidate**<br />
Create a invalidate request to a cloudfront distribution
```sh
$ aws cloudfront create-invalidation --distribution-id <distribution-id> --paths "/*"
```
