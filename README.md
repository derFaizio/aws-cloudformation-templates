# aws-cloudformation-templates
AWS CloudFormation templates

# How to use the templates
1. In the AWS region select `US East (N. Virginia)` as the region. (The buckets are created in the same region as the cloudformation template)
1. Specify template
    1. Click Create Stack
    1. Select template is ready
    1. Select upload a template file
    1. Choose file
    1. Click `Next`
1. Specify stack details
    1. Give the stack a meaningful name
    1. Add parameters if necessary
    1. Click `Next`
1. Configure stack options
    1. Add meaningful tags
    1. Use the default permissions
    1. Leave the default
    1. Click `Next`
1. Review
    1. Click `Create Stack`

# Template description
Templates with increasing level of difficulty

1. [createS3Bucket.yaml](./createS3Bucket.yaml): Create a simple S3 Bucket with bucket name hardcoded
1. [createS3BucketasWebsite.yaml](./createS3BucketWebsite.yaml): **createS3Bucket** + bucket policy for hosting a static website
1. [createS3BucketWebsiteWithParams.yaml](./createS3BucketWebsiteWithParams.yaml): **createS3BucketWebsite** + name of the bucket is taken as an parameter
1. [createS3BucketWebsiteWithParamsBareDomain.yaml](./createS3BucketWebsiteWithParamsBareDomain.yaml): **createS3BucketWebsiteWithParams** + a bare domain bucket with redirection
1. [createS3BucketWebsiteWithParamsSubdomainCDN.yaml](./createS3BucketWebsiteWithParamsSubdomainCDN.yaml): **createS3BucketWebsiteWithParams** but for subdomain bucket instead of website bucket + CloudFront distribution for the subdomain
1. [createS3BucketWebsiteWithParamsBareDomainSubdomain.yaml](./createS3BucketWebsiteWithParamsBareDomainSubdomain.yaml): **createS3BucketWebsiteWithParamsBareDomain** but for subdomain buckets instead of website buckets
1. [createS3BucketWebsiteWithParamsBareDomainSubdomainACM.yaml](./createS3BucketWebsiteWithParamsBareDomainSubdomainACM.yaml): **createS3BucketWebsiteWithParamsBareDomainSubdomain** + signed certificate via ACM
1. [createS3BucketWebsiteWithParamsBareDomainSubdomainACMCDN.yaml](./createS3BucketWebsiteWithParamsBareDomainSubdomainACMCDN.yaml): **createS3BucketWebsiteWithParamsBareDomainSubdomainACM** + CloudFront distributions for www and bare domain
1. [createSubdomain.yaml](./createSubdomain.yaml): **createS3BucketWebsiteWithParamsBareDomainSubdomainACMCDN** + route53 for www and bare domain. The complete subdomain deployment.


### ADDITIONAL HINTS
> During the Certificate validation via ACM `Create Records in Route53` might be needed to speed up the process.

> Use [SampleIndex.html](./SampleIndex.html) as index.html in the www.subdomain.website.com

> After making changes to the source code `index.html` Invalidate the CloudFront Distribution using the AWS Management Console (UI)
1. Open the CloudFront Console.
Click on the ID of the distribution associated with your subdomain (subdomain.website.com).
1. Select the Invalidations tab from the horizontal menu.
1. Click the Create invalidation button.
1. In the Object paths box, type:
/* (to clear everything)
OR /index.html (to clear just that file).
1. Click Create invalidation.
The status will show as In Progress. Once it switches to Completed (usually within 60 seconds), refresh your browser.

> To add the A and AAAA records, go to the CloudFront Distribution and in the `General` tab, click `Route Domains to CloudFront`.