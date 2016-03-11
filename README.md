# kcptun
TCP流转换为KCP+UDP流(AES加密)，工作示意图:        
```原client -> kcptun client ->  kcptun server -> 原server```

# 基于二进制的安装(推荐)
在release中下载对应平台的client, server， 执行 client -h 和server -h 查看详细使用方法. 举例：            
我们要代理```ssh -D```的socks5通信，假定服务器IP为:```xxx.xxx.xxx.xxx```

服务器端执行:     
```server -t "127.0.0.1:22"  ```     // 所有数据包转发到本地22端口           

客户端执行:          
```client -r "xxx.xxx.xxx.xxx:29900"   ```    // 默认server端口是29900           

客户端和服务端启动后，使用ssh -D 连接本地kcptun客户端，即可发起socks通信， 例如:             
```ssh -D 8080 ubuntu@localhost:12948 ```     // 默认的client端口为12948    

浏览器就可以连接8080端口做socks代理了

# 基于源码的安装
## 预备条件:       
1. 安装好```golang```       
2. 设置好```GOPATH```  以及```PATH=$PATH:$GOPATH/bin``` (例如: ```export GOPATH=/home/ubuntu;  export PATH=$PATH:$GOPATH/bin```)       
## 安装命令
1. 服务端: ```go get github.com/xtaci/kcptun/server;  server```        
![server](server.gif)      

2. 客户端: ```go get github.com/xtaci/kcptun/client;  client```      
![client](client.gif)    


# 使用案例
1. openvpn client -> kcptun client -> kcptun server -> openvpn server
2. ssh client -> kcptun client -> kcptun server -> sshd
2. browser socks5 proxy(pac) -> kcptun client -> kcptun server -> socks5 server

# 贡献
欢迎短小精干的PR
