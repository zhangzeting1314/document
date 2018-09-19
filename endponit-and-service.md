# 服务器域名

您可以通过AWS S3协议访问下表中列出的服务域名。

兼容S3的服务域名：

|支持s3的服务器域名|区域|协议|
|-|-|-|
|s3.cn-north-1.jcloudcs.com|华北-北京|http/https|
|s3.cn-east-1.jcloudcs.com|华东-宿迁|http/https|
|s3.cn-east-2.jcloudcs.com|华东-上海|http/https|
|s3.cn-south-1.jcloudcs.com|华南-广州|http/https|

通过AWS S3协议访问OSS和直接访问OSS类似，也支持path-style和 bucket virtual hosting两种方式，以GetObject举例，两种风格请求语法如下：

|风格|请求语法|
|-|-|
|bucket virtual hosting|GET /small.zip HTTP/1.1 <br>Host: bucket.s3.cn-north-1.jcloudcs.com|
|Path-style|GET /bucket/small.zip HTTP/1.1 <br>  Host: s3.cn-north-1.jcloudcs.com |

注：sdk中默认使用第一种方式，可通过更改配置修改请求方式。
