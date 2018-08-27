# Put Bucket Policy

## 描述
该操作可设置指定Bucket的policy，仅Bukcet的Owner可操作。更多Bucket Policy相关信息，请访问https://www.jdcloud.com/help/detail/1858/isCatalog/1

## 请求
### 语法
```
PUT /?policy HTTP/1.1
Host: <bucket>.s3.<region>.jcloudcs.com 
Date: <date>
Authorization: <authorization string> (see Authenticating Requests (AWS Signature Version4))

Policy written in JSON
```
### 请求参数
无请求参数
### 请求Header
无特殊请求Header
### 请求元素
Body为JSON字符串，包含Policy语句。每个Policy可以有多个规则(Statement),每条规则有以下元素组成：

元素|含义|必须
---|---|---
Action|该条规则生效的操作，支持操作：s3:DeleteBucket、s3:ListBucket、s3:GetObject、s3:PutObject、s3:DeleteObject|是
Effect|如果匹配该规则的时候产生的效果，为Deny或者Allow|是
Resource|该规则生效的资源，格式为arn:aws:s3:${bucket}/${dir}，默认为当前Bucket|是
Principal|该规则生效的requester，JSON对象，支持通配符"*"，允许所有。例如{"AWS":["1000022","2322324"]}|是
Condition|该规则生成的条件，是JSON对象，目前只支持Referer和SourceIP|否

## 响应
### 响应Header
无特殊响应Header
### 响应元素
无响应元素

## 示例
### 请求示例
```
PUT /?policy HTTP/1.1
Host: oss-example.s3.<region>.jcloudcs.com  
Date: Tue, 04 Apr 2010 20:34:56 GMT  
Authorization: <authorization string>

{
"Version":"2008-10-17",
"Id":"aaaa-bbbb-cccc-dddd",
"Statement" : [
    {
        "Effect":"Allow",
        "Sid":"1", 
        "Principal" : {
            "AWS":["111122223333","444455556666"]
        },
        "Action":["s3:*"],
        "Resource":"arn:aws:s3:::bucket/*"
    }
 ] 
}

```

### 响应示例
```
HTTP/1.1 204 No Content  
x-amz-request-id: 656c76696e6727732SAMPLE7374  
Date: Tue, 04 Apr 2010 20:34:56 GMT  
Connection: keep-alive  
Server: JDCloudOSS  
```