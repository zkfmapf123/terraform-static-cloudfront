# Terraform-Static-Cloudfront

- Terraform module which creates Cloudfront + S3 use Deploy Static-Site

## Usage

```
module "static-site" {
  source = "../../"

  ## Commomn
  common_name = "dk-example"
  env         = "common"

  ## S3
  s3_is_versioning = true
  s3_acl           = "private" // 변경은 자제...
  s3_cors_rule = {
    allowed_headers = ["*"]
    allowed_methods = ["PUT", "GET", "POST"]
    allowed_origins = ["*"]
    expose_headers  = ["ETag"]
    max_age_seconds = 3000
  }
  s3_source = "./common/index.html"
  s3_website = {
    index = "index.html"
    error = "error.html"
  }

  ## Cloudfront
  cf_acm            = null
  cf_enabled        = true
  cf_is_ipv6        = false
  cf_comment        = "example cloudfront static-site"
  cf_default_object = "index.html"
  cf_alias          = []
  cf_waf_id         = null

  ## Cloudfront-origin
  cf_origin_attempts = 3
  cf_origin_timeout  = 10

  ## Cloudfront-cache
  cf_caching_policy_name   = "Managed-CachingOptimized"
  cf_caching_allow_methods = ["GET", "HEAD", "OPTIONS"]
  cf_caching_cache_methods = ["GET", "HEAD"]
  cf_caching_viewer_policy = "allow-all"

  cf_caching_ttl = {
    default_ttl = 0
    min_ttl     = 0
    max_ttl     = 0
  }

  ## geo
  cf_geo_restriction_type      = "none"
  cf_geo_restriction_locations = null

  ## viwer
  cf_viewer_acm_arn           = null
  cf_minimum_protocol_version = null
  cf_ssl_support_method       = null
}
```

## Desc

- Cloudfront + S3 Deploy use Static Site

## Example

- <a href="https://github.com/zkfmapf123/terraform-static-cloudfront/blob/master/examples/default-static-site/main.tf"> Default-Static-Site</a>

## Reference

- vars.tf 참고
- <a href="https://registry.terraform.io/modules/zkfmapf123/cloudfront/static/latest/examples/default-static-site"> Terraform Module Site </a>
