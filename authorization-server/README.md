> 测试

* 授权码模式

  启动项目，请求授权码模式地址：http://localhost:8080/oauth2/authorize?response_type=code&client_id=messaging-client&scope=message.read&redirect_uri=https://baidu.com

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

* 