# sub-web-modify
[最美订阅转换](https://sub.v1.mk)基于项目[CareyWang/sub-web](https://github.com/CareyWang/sub-web)，重制CSS样式，增加“暗黑模式”，监听系统默认主题，自动切换亮/暗模式，点击切换主题按钮的同时会将切换结果写入浏览器localStorage【点击“太阳/月亮”图标即可切换】，增加“高级功能”点击显示/隐藏，新增fakeloader过渡动画、bootstrap框架【解决当手机浏览器切换电脑UA时，远程配置添加过多后，布局乱的问题】和layui【网站弹窗】，解决重新载入网页依然保留上次订阅的问题，添加短链接选择/自定义功能，增加近百条远程配置！<br/>**PS:默认把layui弹窗给删了，如果需要加，请在public/index.html中按顺序引入layui.css、layui.all.js、laybox.js即可，路径自己找找！**
## 效果预览：
![avatar](https://cdn.jsdelivr.net/gh/limr95/webcdn@3.2/7.gif)
### 食用方法【以Linux为例】：
1.安装 [node](https://blog.csdn.net/achabuhecha/article/details/111400068) 和 [yarn](https://classic.yarnpkg.com/en/docs/install#debian-stable) 和 [git](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)

2.终端执行 `cd /home && git clone https://github.com/limr95/sub-web-modify.git && chmod -R 755 sub-web-modify && cd sub-web-modify && yarn install && yarn build`

3.build成功后，需要安装nginx并正确配置，以下为nginx server部分配置，可以参考一下【这块建议新手使用宝塔面板等自动化运维工具，直接将网站目录更改为/home/sub-web-modify/dist即可】！

```shell
server {
    listen 80;
    server_name 你的域名或IP;
    root /home/sub-web-modify/dist;
    index index.html index.htm;
    error_page 404 /index.html;
    gzip on; #开启gzip压缩
    gzip_min_length 1k; #设置对数据启用压缩的最少字节数
    gzip_buffers 4 16k;
    gzip_http_version 1.0;
    gzip_comp_level 6; #设置数据的压缩等级,等级为1-9，压缩比从小到大
    gzip_types text/plain text/css text/javascript application/json application/javascript application/x-javascript application/xml; #设置需要压缩的数据格式
    gzip_vary on;
    location ~* \.(css|js|png|jpg|jpeg|gif|gz|svg|mp4|ogg|ogv|webm|htc|xml|woff)$ {
        access_log off;
        add_header Cache-Control "public,max-age=30*24*3600";
    }
}
```

4.如需进一步修改前端，请在/home/sub-web-modify下执行 `yarn serve` 进行调试即可
