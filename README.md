# vps-shadowsocks
### 准备条件：
      需要一个Digital Ocean的账号，充值5刀后，利用Github的Student Package可以领取50刀，建议先点击分享链接，然后就可以先拿10刀，再拿50刀 <br>
      分享链接：https://m.do.co/c/145bd92bff50 
### 建立VPS
      进入官网后，创建一个Droplets,系统选择默认的Ubuntu,配置可以选择最低的5刀/月，已经足够了； <br>
      服务器配置根据自己的地区选择最快的机房，我选择的是SFO1  <br>
      测速地址：http://speedtest-sfo1.digitalocean.com/ <br>
      注意有选择添加SSH key的选项，建议预先在网站里添加自己的ssh key最方便，当然也可以后面再加，这个可以用来作为ssh的快速登陆，不用输密码 
### 服务器配置
    官网有浏览器登陆的方式，但是我认为很不好用，需要改密码，而且很卡，所以选择ssh远程登录 
##### 使用cmd登陆ssh,如果没用过ssh,需要自行安装
    ssh root@你的服务器ip 
###### 如果出现错误的话，可以选择指定ssh key
    ssh -i .ssh/你的公钥pubkey root@你的服务器IP 
   
##### 安装与配置Shadowsocks
```
    sudo apt-get update
    apt-get install python-pip
    pip install shadowsocks
    nano /etc/shadowsocks.json 
```
##### 修改配置文件shadowsocks.json
```
    { 
       "server":"my_server_ip", 
       "local_address": "127.0.0.1", 
       "local_port":1080, 
       "port_password": { 
       "8381": "123456", 
       "8382": "123456", 
       "8383": "123456", 
       "8384": "123456" 
       }, 
       "timeout":300, 
       "method":"aes-256-cfb", 
       "fast_open": false 
     } 
```
##### 注意my_server_ip要修改成自己的IP 
##### 重启shadowsocks 
    ssserver -c /etc/shadowsocks.json -d start 
#### 接下来这步很关键，在官网配置防火墙
 在Network->Firewall 创建新的规则，然后在Inbound Rule里添加Custom的Type，端口选择在配置文件里的端口，加了几个端口就加几个准入端口。 
### 大功告成
 接下来只需在服务器里配置自己的Shadowsocks客户端即可登陆GOOGLE！ 
