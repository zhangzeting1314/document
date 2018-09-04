# 错误响应 

当用户访问OSS出错时，以及一个application/xml格式的消息体；OSS会返回给用户一个合适的3xx，4xx或者5xx的HTTP状态码。


下面是错误响应的消息体例子：
```angular2html
<Error>
    <statusCode>404</statusCode>
    <Code>NoSuchBucket</Code>
    <Message>The specified bucket does not exist.</Message>
    <Resource>/henry-dev-test-bucket123123123123</Resource>
    <RequestId>956F69119AE3958B</RequestId>
</Error>

```
例子中错误消息体包含的几个元素解释，请见下表：

| 名称 | 描述 | 类型|
| ------ | ------ |  ------ | 
| statusCode | 状态码|  数值   |
| code | 错误码是唯一标识错误的，用来确定错误场景 | 字符串|
| Message | OSS给出的详细错误信息 |字符串|
| Resource | 资源地址：Bucket地址或者Object地址。 |字符串|
| RequestId | 当请求发送时，服务端将会自动为请求生成一个唯一的 ID。使用遇到问题时，request-id能更快地协助 OSS 定位问题。 |字符串|


## 错误码列表

3XX类型错误
<table>
<thead>
<tr>
<th>错误码</th>
<th>描述</th>
<th>HTTP状态码</th>
</tr>
</thead>
<tbody>
<tr>
<td>PermanentRedirect</td>
<td>该资源已经被永久改变了位置，请利用HTTP Location来重定向到正确的新位置</td>
<td>301</td>
</tr>
<tr>
<td>TemporaryRedirect</td>
<td>该资源已经被临时改变了位置，请利用HTTP Location来重定向到正确的新位置</td>
<td>302 </td>
</tr>
<tr>
<td>Redirect</td>
<td>临时重定向</td>
<td>307</td>
</tr>
<tr>
<td>TemporaryRedirect</td>
<td>在DNS更新期间，您将被临时重定向</td>
<td>307</td>
</tr>
</tbody>
</table>

4XX类型错误

<table>
<thead>
<tr>
<th>错误码</th>
<th>描述</th>
<th>HTTP状态码</th>
</tr>
</thead>
<tbody>
<tr>
<td>POLICYError</td>
<td>bucket policy 为 null</td>
<td>400</td>
</tr>
<tr>
<td>RequestTimeOut</td>
<td>读取数据超时，检查网络是否过慢或上传并发数过大</td>
<td>400 </td>
</tr>
<tr>
<td>SlowDown</td>
<td>请降低访问频率</td>
<td>400</td>
</tr>
</tbody>
<tr>
<td>RequestTimeTooSkewed</td>
<td>请求时间超过权限有效时间</td>
<td>400</td>
</tr>
<tr>
<td>InvalidCompressError</td>
<td>Compress need bucket acl public-read-write.</td>
<td>400</td>
</tr>
<tr>
<td>TooManyBuckets</td>
<td>您创建的bucket超过限制</td>
<td>400</td>
</tr>
<tr>
<td>CompressOjectsNumError</td>
<td>打包文件数量有误，您打包的范围应该1-100</td>
<td>400</td>
</tr>
<tr>
<td>TooManyMultipartUploads</td>
<td>初始化分片上传数量超过限制</td>
<td>400</td>
</tr>
<td>InvalidParamError</td>
<td>请求参数错误</td>
<td>400</td>
</tr>
<tr>
<td>EFFECT</td>
<td>referer can not apply effect</td>
<td>400</td>
</tr>
<tr>
<td>UserAlreadyHasKeys</td>
<td>the user already has keys</td>
<td>400</td>
</tr>
<tr>
<td>ConnectionLost</td>
<td>连接丢失</td>
<td>400</td>
</tr>
<tr>
<td>InvalidParamError</td>
<td>请求参数错误</td>
<td>400</td>
</tr>
<tr>
<td>SignatureDoesNotMatch</td>
<td>提供的签名不符合规则</td>
<td>403</td>
</tr>
<tr>
<td>SignatureDoesNotMatchV2</td>
<td>签名版本错误，您提供的签名不支持，我们支持签名版本4The request signature we calculated does not match the signature you provided.</td>
<td>403</td>
</tr>
<tr>
<td>MethodNotAllowed</td>
<td>此资源不允许您指定的方法。The specified method is not allowed against this resource</td>
<td>405 </td>
</tr>
<tr>
<td>InvalidPayer</td>
<td>对象禁止访问</td>
<td>403</td>
</tr>
<tr>
<td>InvalidAccessKeyId</td>
<td>AccessKey不存在</td>
<td>403 </td>
</tr>
<tr>
<td>SignatureDoesNotMatch</td>
<td>提供的签名不符合规则</td>
<td>403 </td>
</tr>
<tr>
<td>AccessForbidden</td>
<td>签名或者权限不正确，拒绝访问</td>
<td>403 </td>
</tr>
<tr>
<td>InvalidBucketName</td>
<td>bucket名称不合法</td>
<td>400</td>
</tr>
<tr>
<td>InvalidMaxAge</td>
<td>指定的MaxAge不合法</td>
<td>400</td>
</tr>
<tr>
<td>InvalidLocationConstraint</td>
<td>指定的位置约束不合法</td>
<td>400</td>
</tr>
<tr>
<td>InvalidObjectKey</td>
<td>文件名称不合法</td>
<td>400</td>
</tr>
<tr>
<td>InvalidThumbnailContent</td>
<td>The specified thumbnail source bucket is empty.</td>
<td>400</td>
</tr>
<tr>
<td>InvalidThumbnailBucket</td>
<td>The specified thumbnail source bucket is empty</td>
<td>400</td>
</tr>
<tr>
<td>InvalidThumbnailKey</td>
<td>The specified thumbnail source key is empty</td>
<td>400</td>
</tr>
<tr>
<td>InvalidThumbnailKeyPrefix</td>
<td>The specified thumbnail key prefix is not valid</td>
<td>400</td>
</tr>
<tr>
<td>InvalidThumbnailMode</td>
<td>The specified thumbnail mode is not valid.</td>
<td>400</td>
</tr>
<tr>
<td>InvalidThumbnailFormat</td>
<td>The specified thumbnail format is not valid.</td>
<td>400</td>
</tr>
<tr>
<td>InvalidThumbnailCount</td>
<td>The specified thumbnail count is not valid.</td>
<td>400</td>
</tr>
<tr>
<td>InvalidCompressType</td>
<td>打包类型不合法，仅支持zip</td>
<td>400</td>
</tr>
<tr>
<td>InvalidContentLengthError</td>
<td>http header content-length 错误</td>
<td>400</td>
</tr>
<tr>
<td>InvalidContentMD5Error</td>
<td>http header content-md5 错误</td>
<td>400</td>
</tr>
<tr>
<td>EntityTooLarge</td>
<td>上传文件的大小超过要求的最大值</td>
<td>413</td>
</tr>
<tr>
<td>CORSConfigurationTooLarge</td>
<td>CORS的配置文件超过允许的最大值</td>
<td>400</td>
</tr>
<tr>
<td>InvalidCORSConfiguration</td>
<td>CORS设置不合法</td>
<td>400</td>
</tr>
<tr>
<td>InvalidWebsiteConfiguration</td>
<td>静态网站托管设置不合法</td>
<td>400</td>
</tr>
<tr>
<td>WebsiteConfigurationTooLarge</td>
<td>静态网站托管设置超过允许的最大值</td>
<td>400</td>
</tr>
<tr>
<td>ImgProtectedConditionTooLarge</td>
<td>原图保护设置超过允许的最大值</td>
<td>400</td>
</tr>
<tr>
<td>MissingContentLength</td>
<td>Header Content-Length缺失</td>
<td>400</td>
</tr>
<tr>
<td>MissingContentMD5</td>
<td>请求头中缺少Content-MD5</td>
<td>400</td>
</tr>
<tr>
<td>ContentDispositionTooLong</td>
<td>Content Disposition过长</td>
<td>400</td>
</tr>
<tr>
<td>BadDigest</td>
<td>指定的Content-MD5与我们接收到的不匹配</td>
<td>400</td>
</tr>
<tr>
<td>BadContentLength</td>
<td>指定的文件ContentLength与我们接收到的不匹配</td>
<td>400</td>
</tr>
<tr>
<td>InvalidRange</td>
<td>请求的文件范围不合法</td>
<td>416</td>
</tr>
<tr>
<td>NotSupportMultiRange</td>
<td>不支持多Range</td>
<td>416</td>
</tr>
<tr>
<td>KeyTooLong</td>
<td>文件名过长</td>
<td>400</td>
</tr>
<tr>
<td>InvalidPartOrder</td>
<td>分块上传编号不连续</td>
<td>400</td>
</tr>
<tr>
<td>MalformedPolicy</td>
<td>policy 格式错误</td>
<td>400</td>
</tr>
<tr>
<td>IncorrectNumberOfFilesInPostRequest</td>
<td>Post请求每次只允许上传一个文件</td>
<td>400</td>
</tr>
<tr>
<td>InvalidToken</td>
<td>非法Token</td>
<td>400</td>
</tr>
<tr>
<td>BadRequest</td>
<td>错误请求</td>
<td>400</td>
</tr>
<tr>
<td>InvalidURI</td>
<td>URI不合法</td>
<td>400</td>
</tr>
<tr>
<td>InvalidArgument</td>
<td>请求参数不合法</td>
<td>400</td>
</tr>
<tr>
<td>NoSuchDomain</td>
<td>指定域名不存在</td>
<td>404</td>
</tr>
<tr>
<td>InvalidPolicyDocument</td>
<td>策略配置文件不合法</td>
<td>400</td>
</tr>
<tr>
<td>InvalidImgProtectedCondition</td>
<td>原图保护配置文件不合法</td>
<td>400</td>
</tr>
<tr>
<td>MalformedJson</td>
<td>JSON格式有误</td>
<td>400</td>
</tr>
<tr>
<td>MissingSecurityHeader</td>
<td>必要Header缺失</td>
<td>400</td>
</tr>
<tr>
<td>IncompleteBody</td>
<td>Content-Length 请求头未指定的数值</td>
<td>400</td>
</tr>
<tr>
<td>AccessDenied</td>
<td>签名或者权限不正确，拒绝访问</td>
<td>403 </td>
</tr>
<tr>
<td>AccountProblem</td>
<td>您的账号拒绝了此次操作</td>
<td>403 </td>
</tr>
<tr>
<td>AccessKeyLimited</td>
<td>您的签名或权限被policy阻止</td>
<td>403 </td>
</tr>
<tr>
<td>AccountArrear</td>
<td>账户欠费</td>
<td>403 </td>
</tr>
<tr>
<td>BucketAlreadyExists</td>
<td>bucket名称已存在，名称全局唯一</td>
<td>409</td>
</tr>
<tr>
<td>BucketAlreadyOwnedByYou</td>
<td>您已创建该Bucket</td>
<td>409</td>
</tr>
<tr>
<td>BucketNotEmpty</td>
<td>bucket不为空不能删除</td>
<td>409</td>
</tr>
<tr>
<td>BucketHasMutiUploads</td>
<td>有分片上传任务，bucket不能删除</td>
<td>409</td>
</tr>
<tr>
<td>BucketHasReplicationConfiguration</td>
<td>bucket存在跨区域复制规则，不能删除</td>
<td>400</td>
</tr>
<tr>
<td>BucketHasPictureStyle</td>
<td>bucket存在图片样式不能删除</td>
<td>400</td>
</tr>
<tr>
<td>InvalidPart</td>
<td>分片缺失</td>
<td>400</td>
</tr>
<tr>
<td>TooManyParts</td>
<td>分片过多</td>
<td>400</td>
</tr>
<tr>
<td>NoSuchCORSConfiguration</td>
<td>不存在CORS配置</td>
<td>404</td>
</tr>
<tr>
<td>NoSuchWebsiteConfiguration</td>
<td>不存在静态网站托管配置</td>
<td>404</td>
</tr>
<tr>
<td>NoSuchBucket</td>
<td>不存在该bucket</td>
<td>404</td>
</tr>
<tr>
<td>NoSuchReplicationConfiguration</td>
<td>不存在跨区域复制配置</td>
<td>404</td>
</tr>
<tr>
<td>NoSuchImgProtectedCondition</td>
<td>不存在原图保护配置</td>
<td>404</td>
</tr>
<tr>
<td>NoSuchKey</td>
<td>指定的文件名不存在</td>
<td>404</td>
</tr>
<tr>
<td>NoSuchUpload</td>
<td>指定的分片上传不存在</td>
<td>404</td>
</tr>


</table>
5XX类型错误

<table>
<thead>
<tr>
<th>错误码</th>
<th>描述</th>
<th>HTTP状态码</th>
</tr>
</thead>
<tbody>
<tr>
<td>InternalErrror</td>
<td>服务端内部错误</td>
<td>500</td>
</tr>
<tr>
<td>DecryptError</td>
<td>解密错误，文件加密使用了一种错误的方式</td>
<td>500</td>
</tr>
<tr>
<td>NotImplemented</td>
<td>Header中存在无法处理的方法</td>
<td>501</td>
</tr>
<tr>
<td>ServiceUnavailable</td>
<td>服务器繁忙，请重试</td>
<td>503</td>
</tr>

</tbody>
</table>
