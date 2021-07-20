# AWSCLICommands
Contain AWS CLI commons commands<br />
For complete AWS CLI documentation follow: [AWS CLI Command Reference](https://docs.aws.amazon.com/cli/latest/index.html)

Profiles Commands
-------------

**List Profiles**<br />
List all profiles registered in your computer.
```sh
$ aws configure list-profiles
```

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
> :warning: This command will make your data public readable, be careful and if you don't sure, don't use it.
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

**Get specific distribution by domain name**<br />
Get a specific distibution info by domain name<br />
<br />
First enable cloudfront preview stage.
```sh
$ aws configure set preview.cloudfront true
```
After preview is enabled, just run command bellow.
```sh
$ aws cloudfront list-distributions --query "DistributionList.Items[].{DomainName: DomainName, OriginDomainName: Origins.Items[0].DomainName, Id: Id, ARN: ARN, DNS: Aliases.Items[0]}[?contains(OriginDomainName, 'your.domain.com')] | [0]"
```
This command will return a data like bellow:
```
{
    "ARN": "arn:aws:cloudfront::XPTOID:distribution/DISTRIBUITIONID",
    "DNS": "your.domain.com",
    "DomainName": "xptoid.cloudfront.net",
    "Id": "DISTRIBUITIONID",
    "OriginDomainName": "your.domain.com.s3-website-sa-east-1.amazonaws.com"
}
```

**Create invalidate**<br />
Create a invalidate request to a cloudfront distribution
```sh
$ aws cloudfront create-invalidation --distribution-id <distribution-id> --paths "/*"
```

Cognito Commands
-------------
**Set UserPool UI Customization**<br />
Customize the CSS of an app client in a User Pool.<br />
```
$ aws cognito-idp set-ui-customization --user-pool-id <user-pool-id> --client-id <client-id> --css "< your CSS plain text here, without line breaks >" --image-file fileb://< your logo path here >>
