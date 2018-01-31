**api host为 https://api2.xlink.cn**

## 1、通过手机验证码注册新账号

**Request**

URL

```java
POST /v2/user_register
```
Header
```
Content-Type : "application/json"
```
Content
```
{
"phone":"手机号码",
"phone_zone":"手机区号，不填则默认中国:+86",
"nickname":"昵称",
"corp_id":"企业ID",
"verifycode":"验证码",
"password":"登录密码",
"source":"用户来源",
"local_lang":"本地语言代码",
"plugin_id":"应用插件ID"
}
```
Response

Header
```
HTTP/1.1 200 OK
```
Content
```
{
    "phone":"手机号码"
}
```
|字段	|是否必须	|描述|
| --------   | -----:   | :----: |
|phone	|是	|手机号|
|phone_zone	|否	|手机区号，不填则默认中国:+86|
|nickname	|是	|用户昵称，长度2-32个字符|
|corp_id	|是	|企业ID|
|verifycode	|是	|手机短信验证码|
|password	|是	|认证密码，长度6-16个字符|
|source	|是	|用户来源，见附录|
|local_lang	|否	|本地语言代码，默认：zh-ch，见附录|
|plugin_id	|否	|用户所属的应用插件ID|


## 2、登录与认证
**Request**

URL
```
POST /v2/user_auth
```
Header
```
"Content-Type":"application/json"
```
Content
```
{
    "corp_id":"企业ID",
    "phone/email" : "手机号码/邮箱",
	"phone_zone":"手机区号，使用手机号码登录时可选。",
    "password" : "登录密码",
	"resource":"登录源"
}
```

|字段	|是否必须	|描述|
| --------   | -----:   | :----: |
|corp_id	|是	|企业ID|
|phone/email	|是	|邮箱或者手机（根据用户注册的方式）|
|phone_zone	|否	|手机区号，使用手机号码登录时可选。|
|password	|是	|密码|
|resource	|否	|登录源，用户可以在登录时指定登录源，不同登录源可同时登录，长度在0~16个字符之间。|

Response

Header
```
HTTP/1.1 200 OK
```
Content
```
{
    "user_id":"用户ID",
    "access_token":"调用凭证",
    "refresh_token":"刷新凭证",
    "expire_in":"有效期（秒）",
	"authorize":"用户认证码"
}
```

|字段	|是否必须	|描述|
| --------   | -----:   | :----: |
|user_id	|是	|用户ID|
|access_token	|是	|RESTful接口调用凭证|
|refresh_token	|是	|刷新凭证，可用于刷新一个新的调用凭证|
|expire_in	|是	|调用凭证的有效时长，单位：秒|
|authorize	|是	|用户认证码|
