1. **FRP简介**

   - frp 是一款高性能的反向代理应用，专注于内网穿透。它支持多种协议，包括 TCP、UDP、HTTP、HTTPS 等，并且具备 P2P 通信功能。使用 frp，您可以安全、便捷地将内网服务暴露到公网，通过拥有公网 IP 的节点进行中转。

2. **基本工作原理**

   - FRP由客户端（frpc）和服务器端（frps）组成。客户端运行在内网机器上，它负责和运行在具有公网IP服务器上的服务器端进行通信。客户端将内网服务的请求发送给服务器端，服务器端再将请求转发到公网上，从而实现外部网络访问内网服务。

3. **安装与配置**

   - **服务器端（frps）配置**

     - 首先从FRP官方网站（https://github.com/fatedier/frp/releases）下载适合服务器操作系统的frps程序。

     - 解压frp压缩包

       ```
       tar -zxvf frp_0.61.0_linux_amd64.tar.gz
       ```

     - 编辑服务器端配置文件（frps.toml），以下是一个简单的配置示例：

       ```ini
       bindPort = 7000
       vhostHTTPPort = 8080
       auth.token = "abcd"
       ```

       `bind_port`:服务端监听端口，默认值为 7000。

       `vhost_http_port`:HTTP 类型代理监听的端口，启用后才能支持 HTTP 类型的代理。

       `auth.method ` : 鉴权方式，可选值为 token 或 oidc，默认为 token。

       `auth.token`:在 method 为 token 时生效，客户端需要设置一样的值才能鉴权通过。

     - 运行服务器端程序`./frps -c frps.ini`启动服务器。

   - **客户端A（frpc）配置**

     - 同样从官方网站下载适合内网操作系统的frpc程序。

     - 编辑客户端配置文件（frpc.toml），例如要穿透内网的一个Web服务，配置可能如下：

       ```ini
       serverAddr = "x.x.x.x"
       serverPort = 7000
       
       auth.token = "abcd" 	# 与frps配置的令牌相同
       
       [[proxies]]
       name = "web"
       type = "http"	
       localIP = "127.0.0.1"
       localPort = 80						
       customDomains = ["x.x.x.x"]
       ```

       `serverAddr`:连接服务端的地址。

       `serverPort`:连接服务端的端口，默认为 7000。

       `name`:代理名称。

       `type`代理类型，可选值为 tcp, udp, http, https, tcpmux, stcp, sudp, xtcp。

       `localIP`:被代理的本地服务 IP，默认为 127.0.0.1。

       `localPort`:被代理的本地服务端口。

       `customDomains`:自定义域名列表（也可以使用服务端的ip）。

     - 运行客户端程序`./frpc -c frpc.ini`启动客户端。

   - **客户端B（frpc）配置**

     - 同样从官方网站下载适合内网操作系统的frpc程序。

     - 编辑客户端配置文件（frpc.toml），例如要穿透内网的一个Web服务，配置可能如下：

       ```ini
       serverAddr = "x.x.x.x"
       serverPort = 7000
       
       auth.token = "abcd" 	# 与frps配置的令牌相同
       
       [[proxies]]
       name = "web2"
       type = "tcp"	
       localIP = "127.0.0.1"
       localPort = 80						
       remotePort = 8081
       ```

       `remotePort`:服务端绑定的端口，用户访问服务端此端口的流量会被转发到对应的本地服务。

     - 运行客户端程序`./frpc -c frpc.ini`启动客户端。

4. **linux 后台运行**

   - 运行frp服务端

     ```
     nohup ./frps -c ./frps.toml >/dev/null 2>&1 &
     ```

   - 关闭

     ```perl
     ps -aux|grep frp
     
     kill -9 进程号
     ```

5. **注意事项**

   - 安全问题：由于FRP可以将内网服务暴露出来，所以要注意安全防护。例如，合理配置访问权限，避免将敏感服务随意暴露，设置好防火墙规则等。
   - 网络稳定性：FRP的穿透效果可能会受到网络环境的影响。如果服务器端或客户端网络不稳定，可能会导致服务中断或访问延迟等问题。
   - 域名解析：如果使用域名来访问穿透后的服务，要确保域名正确解析到服务器端的公网IP地址，并且配置好相关的域名绑定规则。