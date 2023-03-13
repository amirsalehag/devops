# Mounting minio bucket on a local directory
* First we install `s3fs-fuse` from https://github.com/s3fs-fuse/s3fs-fuse:  
```
sudo apt install s3fs
```
* Then create a bucket on the MinIO Server if you dont already have one.  
* Before you run s3fs, you will need to save your MinIO credentials in a file. Replace access_key and secret_key with your actual MinIO credentials. ( you have to make an access key from minio server and then use it here.):  
```
echo "access_key:secret_key" > /etc/s3cred
```
* Run s3fs to mount the bucket from the MinIO server using the MinIO credentials from the previous command.
```
s3fs <bucket> /<mount path> -o passwd_file=/etc/s3cred,use_path_request_style,url=http://minio-server:9000
```
( check this [link](https://github.com/nitisht/cookbook/blob/master/docs/s3fs-fuse-with-minio.md) for more info.)  
