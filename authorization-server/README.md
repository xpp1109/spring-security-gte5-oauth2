> 说明

​	spring Security5 时候，不推荐使用spring-security-oauth2。提供了新的方法（https://github.com/spring-projects/spring-authorization-server）

需要注意的是该方式支持的并不是oauth2，而是oauth2.1，什么是oauth2.1呢？推荐查看：https://oauth.net/2.1/和https://aaronparecki.com/2019/12/12/21/its-time-for-oauth-2-dot-1。

摘取oauth2.net网站上对比oauth2的说明：

主要区别（以下使用翻译软件翻译，大致意思没错）

- 使用授权代码流的所有 OAuth 客户端都需要 PKCE
- 必须使用精确的字符串匹配来比较重定向 URI
- `response_type=token`本规范中省略了隐式授权 ( )
- 本规范中省略了资源所有者密码凭证授权
- 不记名令牌用法省略了在 URI 的查询字符串中使用不记名令牌
- 公共客户端的刷新令牌必须受发送方限制或一次性使用

> 官方demo运行

​	根据https://github.com/spring-projects/spring-authorization-server上说明使用gradle命令运行即可。

> 拷贝官方代码（基本未做更改），使用postman进行测试。

​		代码位置：authorization-server

​		

```tex
authorization-server
├── README.md
├── authorization-server.iml
├── pom.xml
└── src
    ├── main
    │   ├── java
    │   │   └── com
    │   │       └── xpp
    │   │           └── ssgo
    │   │               └── as
    │   │                   ├── AuthorizationServerApplication.java
    │   │                   ├── config
    │   │                   │   ├── SecurityConfig.java
    │   │                   │   └── WebAuthorizationServerConfig.java
    │   │                   └── jose
    │   │                       ├── Jwks.java
    │   │                       └── KeyGeneratorUtils.java
    │   └── resources
    │       ├── data.sql
    │       └── application.yml
    └── test
        └── java
```



> 测试

* 启动项目

  查看自动创建的表结构：

  浏览器访问：https://localhost:8080/h2-console

  ![image-20210826135010766](https://raw.githubusercontent.com/xpp1109/images/main/uPic/image-20210826135010766.png)

  点击Connect：

  ![image-20210826135541371](https://raw.githubusercontent.com/xpp1109/images/main/uPic/image-20210826135541371.png)

  我们看到有五张表创建，打开表会发现数据也被初始化进去了。

* 授权码模式

  请求授权码模式地址：http://localhost:8080/oauth2/authorize?response_type=code&client_id=messaging-client&scope=message.read&redirect_uri=https://baidu.com

  ![image-20210825172558674](https://raw.githubusercontent.com/xpp1109/images/main/uPic/image-20210825172558674.png)

  输入用户名密码(user1, password):

  ![image-20210825172624486](https://raw.githubusercontent.com/xpp1109/images/main/uPic/image-20210825172624486.png)

  勾选授权scope，点击submit consent按钮：

  ![image-20210825172710505](https://raw.githubusercontent.com/xpp1109/images/main/uPic/image-20210825172710505.png)

  拷贝地址栏：https://www.baidu.com/?code=dPEZCnsiz2WPk5mWdnPImxbSQkbwK7-yPKmg56JuR2NHbswtbXWZFjgZr6MEXfIqi8JhRourmlSSYVVfGuCN-46ep8jbQwxHsqrUVeeY-1XRHkpqaQ2UM9-ulbTsU0mg

  授权码code=`dPEZCnsiz2WPk5mWdnPImxbSQkbwK7-yPKmg56JuR2NHbswtbXWZFjgZr6MEXfIqi8JhRourmlSSYVVfGuCN-46ep8jbQwxHsqrUVeeY-1XRHkpqaQ2UM9-ulbTsU0mg`

  打开postman 通过该code获取access_token:

  ![image-20210825172829461](https://raw.githubusercontent.com/xpp1109/images/main/uPic/image-20210825172829461.png)

  ![image-20210825172855024](https://raw.githubusercontent.com/xpp1109/images/main/uPic/image-20210825172855024.png)

  点击send，返回：

  ![image-20210825172954849](https://raw.githubusercontent.com/xpp1109/images/main/uPic/image-20210825172954849.png)

  JSON数据如下：

  ```json
  {
      "access_token": "eyJraWQiOiI3NzlmYTBkMC1kYmI5LTRkOGMtYTljNy1iMWE3N2U1MjU3ZDMiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJ1c2VyMSIsImF1ZCI6Im1lc3NhZ2luZy1jbGllbnQiLCJuYmYiOjE2Mjk4ODM3NTgsInNjb3BlIjpbIm1lc3NhZ2UucmVhZCJdLCJpc3MiOiJodHRwOlwvXC9hdXRoLXNlcnZlcjo5MDAwIiwiZXhwIjoxNjI5ODg0MDU4LCJpYXQiOjE2Mjk4ODM3NTh9.DONZ0BYwqikDpX36yifOraxr6h_AX4uUAbLqnitC1vEaRHIZVuaSXcLesXx2XxIOyfKu-gglMxho83-JnNU60sX9QQVgnzsHQIExFoBtnFIOmj6mrxOcuTLFWEjya1fqN9rRDAHDInNkTpHICdzKWAtnRR_N7Xwt87B7EwcmAaZedLEyRZo6xQWrx_nIDIsdalxDHricniK7lYxMRHBzXIiV7hIFUtjfPCTGGUhuV3Etu5WGJpo9loOGezTydttvcHttlC8A71viDBR8jD0fQ5Z6NZuq1CfK3rBoh1jXmGUp8g8fi7WTeA2zKyLYYYPSot5FiHcecpc9bAPIh8oPEA",
      "refresh_token": "m166TmZ_o8XpP_wunxsjRRHqH5qbyMMVZz6-tRPQe_73DiKKd5ujdA8TdiwPDgxw6bnYE6MjlTcLy7Cc30BDYsZhHwr7PKXqX0QyQCwkiFRIkrmQOmvCAl-GO_R4gwWZ",
      "scope": "message.read",
      "token_type": "Bearer",
      "expires_in": 299
  }
  ```

  刷新token

  ![image-20210825173244161](https://raw.githubusercontent.com/xpp1109/images/main/uPic/image-20210825173244161.png)

  ![image-20210825173308149](https://raw.githubusercontent.com/xpp1109/images/main/uPic/image-20210825173308149.png)

  请求后结果：

  ![image-20210825173228047](https://raw.githubusercontent.com/xpp1109/images/main/uPic/image-20210825173228047.png)

  JSON数据是：

  ```json
  {
      "access_token": "eyJraWQiOiI3NzlmYTBkMC1kYmI5LTRkOGMtYTljNy1iMWE3N2U1MjU3ZDMiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJ1c2VyMSIsImF1ZCI6Im1lc3NhZ2luZy1jbGllbnQiLCJuYmYiOjE2Mjk4ODM5MzgsInNjb3BlIjpbIm1lc3NhZ2UucmVhZCJdLCJpc3MiOiJodHRwOlwvXC9hdXRoLXNlcnZlcjo5MDAwIiwiZXhwIjoxNjI5ODg0MjM4LCJpYXQiOjE2Mjk4ODM5Mzh9.GoCvmcLHIWYEN7-_jJQw3cOAC1TOH_If6VuxhgzsRIw2jfeJlgdKRxC9a_meRzoZGWcDb95aM_BPEwFgXsOgiXM5u_NTTaB9j6xEOoaTP_KA8V9bbqw63C-_nYlIzRQwYZUy4YHFDA-bOrUGjZxtRbr1WxP27iwiSMnXQ8XOI8P-gN5mr3EW7gxIr7vtoP1duwmqROirUuskw74YAr2l6ZDxdn7AEG17Qqb5gWYU9j61NHuyJGT7Vy1RQJT_G__vsLVaf-1z7CnE1_9IxSRGQf4TlKDG2F2C7TEGqGnNXQa5Sc-CPjh7hNHEirqH0_rBnKFwG9irtbS7eCFLporjkg",
      "refresh_token": "m166TmZ_o8XpP_wunxsjRRHqH5qbyMMVZz6-tRPQe_73DiKKd5ujdA8TdiwPDgxw6bnYE6MjlTcLy7Cc30BDYsZhHwr7PKXqX0QyQCwkiFRIkrmQOmvCAl-GO_R4gwWZ",
      "scope": "message.read",
      "token_type": "Bearer",
      "expires_in": 300
  }
  ```

  简化模式（response_type=token）在oauth2.1被移除.

* 客户端模式：

  ![image-20210825173403173](https://raw.githubusercontent.com/xpp1109/images/main/uPic/image-20210825173403173.png)

  ![image-20210825173415004](https://raw.githubusercontent.com/xpp1109/images/main/uPic/image-20210825173415004.png)

  返回结果如图：

  ![image-20210825173435350](https://raw.githubusercontent.com/xpp1109/images/main/uPic/image-20210825173435350.png)

  JSON结果：

  ```json
  {
      "access_token": "eyJraWQiOiJjOGRhNzAwZC0zNzUyLTQyMTMtOTFmZi1hOTlmMjY5NTU4NTciLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJtZXNzYWdpbmctY2xpZW50IiwiYXVkIjoibWVzc2FnaW5nLWNsaWVudCIsIm5iZiI6MTYyOTg4MzEzNywic2NvcGUiOlsib3BlbmlkIiwibWVzc2FnZS5yZWFkIiwibWVzc2FnZS53cml0ZSJdLCJpc3MiOiJodHRwOlwvXC9hdXRoLXNlcnZlcjo5MDAwIiwiZXhwIjoxNjI5ODgzNDM3LCJpYXQiOjE2Mjk4ODMxMzd9.NvTu-y5AxLXLSSC_FvxgG3ZYCsOdQRBQgay5sZOmgPAPHcNrTeau7RtdQPoYL7rxedbbfgzBzBOQA3wYepMcuWqO7DBc3kB-I6D6c8nImMo24hSVDTXqnGEtyAUWUhiWJPY1IvVmgksZdaemXQUjFQmBM6Lxt32nBVz8Ap7NXb4oqIbr2bkYodvPRLdYY0PeMpPKAqJuKl4nnRzTCGWx9koJ4KGynkCo3KtMjpv3WuarVKpyiUIhTRlOOAI7wrGplFukaKXpNriMMwasFNtcKfSdWQ6iIDtFs1oUOfE7NJ8EY1FkUaZP1brrHzJgrSvaQPATOfNMFWAA7MN6DzUrlQ",
      "scope": "openid message.read message.write",
      "token_type": "Bearer",
      "expires_in": 300
  }
  ```

* 密码模式 在oauth2.1被移除。

  之前以为是bug，就给提了issue（https://github.com/spring-projects/spring-authorization-server/issues/419），官方回复不支持。

  但是有扩展方式。还没弄。具体可看我提出的issue的作者回复。

  

> spring-security-oauth2的实现方式，可查看我之前的笔记
>
> 知乎：https://zhuanlan.zhihu.com/p/403379055
>
> github源码：https://github.com/xpp1109/spring-security-lt5-oauth2



> 本文内容github地址是：https://github.com/xpp1109/spring-security-gte5-oauth2



> 一键三联，关注、点赞、分享。完结撒花，谢谢！



---

梦想越是美丽，就越是显得遥不可及。可奇怪的是，一旦你下定了决心，很快地，那些梦想就一一成为了现实！

---

