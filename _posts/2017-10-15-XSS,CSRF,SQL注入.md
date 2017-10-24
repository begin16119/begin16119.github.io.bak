---
layout:     post
title:      XSS,CSRF,SQL
subtitle:   网络安全
date:       2017-10-15
author:     BX
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - web安全
    - 脚本
    - SQL注入
    
    

---

## XSS

> Cross-site scripting 

由于同源策略，只能有三种标签可以请求不同的源。
>   <script>

>   <sytle>

>   <img>

XSS 通过网站的上述标签，将代码植入到网页上，攻击者窃取网页内容， cookie等重要信息。

漏洞的防御和利用

可以将使用者的内容进行过滤

    PHP的htmlentities()或是htmlspecialchars()。
    Python的cgi.escape()。
    Java的xssprotect (Open Source Library)。
    
## CSRF
> 跨站请求伪造（英语：Cross-site request forgery）

攻击者欺骗服务器，用用户的身份去访问浏览器。

#### 例子

假如一家銀行用以執行轉帳操作的URL地址如下：

    http://www.examplebank.com/withdraw?account=Acc         outName&amount=1000&for=PayeeName
那麼，一個惡意攻擊者可以在另一个網站上放置如下代碼：

    <img src="http://www.examplebank.com/withdraw?account=Alice&amount=1000&for=Badman">
如果有賬戶名為Alice的用戶訪問了惡意站點，而她之前剛訪問過銀行不久，登錄信息尚未過期，那麼她就會損失1000資金。

这个漏洞存在的是，服务器没有做用户的身份确认，一般解决思路是：

> 每一个用户给一个隐藏的表单Token
> 检查Refer字段 保证同源，但是也有篡改的可能

## SQL注入

前端和后端为对传入参数过滤，导致直接使用SQL操控数据库。

作用原理：
    1.SQL CURL 
    2. 恒等 1=1
    3.字符串闭合 
    4.注释号 mysql中的# 注释掉SQL
    
   
```
select * from users where (name =' $username') and (password = ' $ password')
```

 
 恶意填入
 
```
username =  1' or '1'='1 #

```
结果

    select * from users;
    
    
如何避免：
 
Java中 使用PrepareStatement预编译SQL语句。
    
优点：
    1：预编译到缓存中，重复使用，高效。
    2：提高可毒性
    3：防止SQL注入

 




