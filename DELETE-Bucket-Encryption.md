# DELETE Bucket encryption
 删除OSS存储空间的默认加密配置。此接口兼容S3,仅支持OSS的兼容S3服务域名。
参见 [服务器域](https://docs.jdcloud.com/cn/object-storage-service/regions-and-endpoints)。
 
## 请求语法
 
```
DELETE  /eric-jdcloud/?encryption  HTTP/1.1
Host: <bucket>.s3.<region>.jcloudcs.com
Date: Wed, 06 Sep 2018 12:00:00 GMT
Authorization: authorization string  (使用签名版本4)

```
###  请求参数

不需要请求参数。

###  请求头

不需要特殊请求头。

###  请求体

不需要请求体。

## 响应

### 响应头

 无特殊Header。
 
### 示例：

  请求示例：
  
```
DELETE  /eric-jdcloud/?encryption  HTTP/1.1
Host: examplebucket.s3.cn-north-1.jcloudcs.com
Date: Wed, 06 Sep 2018 12:00:00 GMT
Authorization: signatureValue   (使用签名版本4)

```

响应示例：
  
```
HTTP/1.1 204 No Content
x-amz-request-id: 0CF038E9BCF63097
Date: Wed, 06 Sep 2017 12:00:00 GMT

```

  
  
  
  


