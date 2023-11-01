# AWS CLI integration for MINIO
* [link](https://min.io/docs/minio/linux/integrations/aws-cli-with-minio.html) to its document.
* We can use aws cli to use it like minio client (mc) as a client for our minio server.
* Here's how we can give minio credentials to aws:
```bash
AWS_ENDPOINT_URL=http://<minio url>
AWS_ACCESS_KEY_ID=<minio access-key>
AWS_SECRET_ACCESS_KEY=<minio secret-key>
aws --endpoint-url $AWS_ENDPOINT_URL s3 ls <bucket name>/
```
## How to list the latest modified object, bucket or a prefix
```bash
x=$(aws s3 ls <bucket name>/ | sort | tail -n 1) ; y=($x) ; echo "${y[-1]}"
```
