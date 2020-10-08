# V2ray RSS
---
### 说明
通过爬取免费v2ray链接分享，自动生成订阅链接

### Linux一键安装脚本
```
curl https://raw.githubusercontent.com/sunyuting83/v2rss-go/master/install.sh |bash
```
> 一键脚本监听端口5500
### Linux一键卸载脚本
```
curl https://raw.githubusercontent.com/sunyuting83/v2rss-go/master/uninstall.sh |bash
```

### 使用
从releases下载最新版本的v2rss.zip 已经编译好版本，然后执行：
```bash
unzip v2rss.zip
cd v2rss
./v2rss -p 5500
```
参数说明：-p 监听端口号

浏览器访问 http://localhost:5500/?i=1

#### 参数说明

| 参数  | 说明 |
| ------------ | ------------ |
| w | 启用代理访问（国内跨域访问） |
| n | 内容数字 |
| i | 合并数据数量 |

### nginx配置文件
```
server {
    listen 80;
    server_name yourdomain.com;
    location / {
        proxy_pass http://127.0.0.1:5500;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
    access_log  your log path;
}
```
修改yourdomain.com成你的域名

修改your log path 成你的log文件路径

使用其他端口 请修改 proxy_pass 后面的端口号


### 修改servie文件，程序启动目录
```bash
# 修改v2rss.service文件第7、8行的v2rss程序所在目录.例：
PIDFile=/data/v2rss/v2rss.pid
ExecStart=/data/v2rss/start.sh
```
### 添加开机启动
```bash
# 例v2rss目录在/data:
# 拷贝 v2rss.service 到 systemctl目录
sudo cp /data/v2rss/v2rss.serivce /usr/lib/systemd/system/
#更新systemctl
sudo systemctl daemon-reload
#启动
systemctl start v2rss
#停止
systemctl stop v2rss
#重启
systemctl restart v2rss  
```

- Win版使用说明
> 下载v2rss_x86_64.zip 并解压。双击运行。
在v2ray客户端订阅处填入订阅地址：
http://localhost:3000/?w=1&n=1
必须加w参数，用于国内访问。
其他参数请看说明文件
订阅成功后关闭窗口即可

##### 注：如使用其他端口，修改启动文件start.sh -p参数后面的端口号