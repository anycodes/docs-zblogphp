# 发布应用

Z-Blog 官方搭建的[`Z-Blog 应用中心`](https://app.zblogcn.com/) 是广大 Z-Blog 使用者和开发者提供了主题和插件大本营，提供免费与收费的 Z-Blog & Z-BlogPHP 主题、模板和插件的下载。

任何希望为 Z-Blog 做贡献的开发者都可以免费加入到应用中心并发布自己的因为给所有用户使用。为了保持应用中心应用质量，我们制定了一些应用上架的基本要求，在您的应用符合相应标准后即可发布到应用中心，

## 成为开发者
当您想首次发布您的应用时，请提供您开发的应用并参照[`欢迎加入Z-Blog应用开发者中心https://bbs.zblogcn.com/thread-77001.html`](https://bbs.zblogcn.com/thread-77001.html)的要求联系我们，我们会审核您的应用并将您的帐号添加开发者权限。

## 发布标准
### A.通用
1. 开启 debug 模式后报错的
2. 含有木马等有害代码的
3. 含有任何被加密的 PHP(Z5 加密也不行，只能由应用中心服务器端加密)
4. php 文件有 UTF-8 BOM 头的
5. 有安全漏洞（包括 SQL 注入、跨站脚本攻击、跨站请求伪造等）
6. 引用了外站资源尤其是小站资源的
7. 自动审核内容里有黄色提示的（使用较老旧版本的 js 等）
8. 打着免费旗号跳过“应用中心支付系统”搞“内置收费”的(微博、微信、支付宝等支付社交系统或其它功能 API 必须要收费除外)
9. 应用有免费或低价诱导后续高消费或是明显高于市场定价等不良意图或是违反公序良俗的
10. 修改保存系统源码或是系统默认语言包

### B.主题
1. 主题里没有 zblog 版权
2. 自动审核后的截图，出现错位等不正常的
3. 标题等长度过长不会导致变形
4. 摘要的空格被移除的
5. ul,ol,li,blockquote 等 Html 元素样式错误的
6. 需要提供配置的地方没的可配置的页面
7. 评论层级不对

### C.插件
1. 数据库表和 Class 没有使用 zbp 的标准数据库创建操作规范的
2. 数据库操作没有使用链式对象等系统自带操作而使用自行拼接 sql 代码的
3. 在应该用$zbp→CheckRights 判断权限的地方用最简单的 zbp→User→Level 去实现的

### D.上传后的应用发布内容
1. 缺少前台展示截图(如有前台展示的话)
2. 缺少后台截图(如有后台配置的话)
3. 缺少基本的（或详细的）使用说明和功能介绍

### E.禁止条款
1. 严禁抄袭复制有版权保护的主题模板
2. 禁止多次提交无意义的应用去刷新排行

## 完善简介

## 提交发布

## 应用审核

## 应用加密说明
[`Z5加密`](https://z5encrypt.com/) 是由 Z-Blog 应用中心推出的 PHP 加密方案，也是 「Z-Blog 应用中心」 唯一支持的加密方案。为确保用户权益，只有 Z5 加密后的加密文件被允许上架到应用中心，非使用 Z5 加密的应用代码必须以明文形式提交到应用中心上架。

`Z5加密` 相关介绍内容详见：https://z5encrypt.com/docs/

使用说明见：https://z5encrypt.com/docs/usage/

## 应用验证
为保证开发者利益，应用中心提供应用购买验证系统用于验证用户使用应用的合法性。应用验证系统与应用中心独立，即使应用中心网站无法访问，也不影响应用验证系统的正常运行。

**开发者应用验证调用**

应用验证系统与应用中心独立，即使应用中心网站无法访问，也不影响应用验证系统的正常运行。

**新版本 V2 验证**

仅提供 PHP 版本代码，请在应用中心网站后台 → 开发者工具 → 验证代码处获得。

**添加指南**
1. 添加在 `InstallPlugin` 函数中，实现启用插件时自动验证。
2. 需要运行某些速度慢的功能时，如批量发邮件等，可在这之前进行验证。

建议配合 Z5 加密使用。

**不正确行为**
1. 验证因需要连接服务器，会严重影响页面访问速度。因此，不允许在模板的浏览页等地方插入这部分代码。
2. 即使验证不通过，也不允许对用户的数据进行任何意义上的破坏。

## 应用验证回调

### 验证服务端
验证系统会对验证结果加密后，通知到开发者设置的回调地址。HTTP 方法为 `POST`，`Content-Type` 为 `application/zblogverify`。

Body 的加密方式为：**RSA(base64(AES_KEY) + '.' + base64(AES_IV) + '.' + HS256(realData) + '.' + timestamp) + '.' + AES(realData)**

RSA 公钥和 HMAC-SHA256 密钥见示例代码。

### 明文数据格式
```json
{
	"id": "65fbe736-aa01-4d60-946a-64da5e1bccd7", /* 本次校验的唯一ID，每一次校验返回值都不同 */
	"from": "initiative", /* 校验来源 */
	"error": {
		"number": 0, /* 错误编号 */
		"message": "OK", /* 错误信息 */
		"verified": true, /* 是否验证成功 */
		"cracking": false, /* 疑似破解 */
		"user": {
			"message": "面向用户的错误信息"
		}
	},
	"appId": "应用ID",
	"host": "网站",
	"user": {
		"id": "应用中心ID",
		"username": "用户账号"
	},
  "modified": "应用最后修改日期（时间戳）",
	"license": {
		"appId": "授权文件保存的应用ID",
		"userId": "授权文件保存的用户ID",
		"timestamp": "授权文件生成时间戳"
	}
}
```

### 示例代码(PHP)
以下代码仅能运行于 PHP 5.3+。请注意，以下代码不对重放攻击做出保证，在入库前请先确认 ID 是否唯一。
```php
<?php
function getVerifyData($data) {
	$publicKey = openssl_pkey_get_public('-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAoH4uiMZYWy1sOXuq4YAA
MtyrAtUcWHOXalSAmtDs1FA2H8fTBbEF+gnvg83Byp/mIvHMIaXc7RPIniwoMgDo
Xo3H0GquBEOH4YoufIqfRFGFwnBw7V1KNv9Iw4XpmBYEboD5HT4PLuoUvSP78iWK
7kMMsYsYOVi7EPn8DbPZbvxnrDXkJmkj3l8YhGWtAjbFU7XgyEKEKBTes9fcxWSW
GCdd1jV9oXcV9EQRkRr50wMvydgIWAAWvcVZ5zzK4sZelZDaGz7yEXG/Q1F1Xp3e
GcC057CQoaEzuTQILUCypiNeQpKdzGXxwyp+Q6DAYITjyFBjQ5WbQiSaZtCPV5D9
lwIDAQAB
-----END PUBLIC KEY-----');
	$rsaDecrypted = '';
	$explodeData = explode('.', $data);
	$rsaEncrypted = $explodeData[0];
	$aesEncrypted = $explodeData[1];
	openssl_public_decrypt(base64_decode($rsaEncrypted), $rsaDecrypted, $publicKey);
	$aesInfo = explode('.', $rsaDecrypted);
	$aesKey = base64_decode($aesInfo[0]);
	$aesIv = base64_decode($aesInfo[1]);
	$hash = $aesInfo[2];
	$data = openssl_decrypt(base64_decode($aesEncrypted), 'aes-256-cbc', $aesKey, OPENSSL_RAW_DATA, $aesIv);
	if (hash_hmac('sha256', $data, 'zblogverification') === $hash) {
		return json_decode($data, false);
	} else {
		throw new Exception('Hash error!');
	}
}

$object = getVerifyData(file_get_contents('php://input'));

if ($object->error->verified) {
	echo '验证通过';
}

var_dump($object);
```

### 测试数据

```bash
PpBHLt70jUUpA1TdP38tm68bVWxRKDA69GqR04PA6on3lcGAwz2s8Dj4qMvCuMosI67b1JNFVELfMmxt1RfKQsSS2vLtIVdblDbmZCBptNd5IYNx2qFZFQQ5Hju3bhwR9VDW8fcy63bEOpWVYxAEhQXT3ztaLZn63gJhpDemA06Emxv6VJgxfe9uLTX31FCDfg6yd
```

### 服务端插件
你可以直接使用如上代码自行搭建服务端系统，也可以直接使用插件，并在应用中心后台填写回调地址即可:https://bbs.zblogcn.com/thread-94905-1-1.html
