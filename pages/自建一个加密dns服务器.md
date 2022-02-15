-
- ### 配置域名
	- 配置域名，指定 `dns` 。
	- 假设指定的域名为 `dns.foo.bar` 。
- ### Nginx 反代
	- 新建一个网站配置文件。
	- ```nginx
	  server {
	     listen 443;
	     server_name dns.foo.bar;
	     client_max_body_size 0;
	  
	  location /dns-query {
	     proxy_pass         https://127.0.0.1:10553; # 后续dnsproxy监听的端口号
	     }
	  }
	  ```
	- 然后 `certbot --nginx` 申请证书。
	- 再次编辑配置文件，加上 `http2` ，重载 `nginx` 。
	- ```nginx
	  listen 443 ssl http2; # managed by Certbot
	  ```
- ### 配置 ip
	- 百度 `ip` ，知晓自己 `ip` 然后把最后一段改为 `1` ，降低风险。
	- 此举是为了配置 `edns` 的 `ip` 地址，让国内网站访问速度变快。
- ### 配置 dnsproxy
	- 到 [dnsproxy](https://github.com/AdguardTeam/dnsproxy/releases) 项目下载最新安装包。
	- 解压，进入文件夹，运行 `dnsproxy` 。
	- ```shell
	  ./dnsproxy -l 127.0.0.1 --https-port=10553 --tls-crt=/etc/letsencrypt/live/dns.foo.bar/fullchain.pem --tls-key=/etc/letsencrypt/live/dns.foo.bar/privkey.pem -u https://1.1.1.1/dns-query -f 8.8.8.8:53 -f 8.8.4.4:53 --cache --edns –edns-addr=[上一步配置的地址] -p 0
	  ```
- ### 使用！
	- 配置下来，自建的 `doh` 服务器地址为，`https://dns.foo.bar/dns-query` 。
	- 主流现代浏览器(火狐、谷歌) -> 设置 -> 安全 -> 使用安全/加密 `dns` -> 选择自定义 -> 填入上述地址 -> 冲浪快乐！
- ### 参考
	- 1. [使用DNSProxy搭建一个支持EDNS的DoH服务器 - 荒岛](https://lala.im/7705.html)
	  2. [搭建无污染的DNS服务 - Foxhole](https://blog.southfox.me/2021/07/%E6%90%AD%E5%BB%BA%E6%97%A0%E6%B1%A1%E6%9F%93%E7%9A%84DNS%E6%9C%8D%E5%8A%A1/)