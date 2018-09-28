# shadowsocks搭建

## 选择套餐

  + 首推 CN2 GT 直连套餐，目前性价比最高，效果不错；追求质量的选择 CN2 GIA，价格比 GT 多些，但效果更好;效果最好的是香港套餐,双程 PCCW,价格略贵;普通 KVM 套餐效果一般，适合一般需求、稳定建站跑服务等。
  
  + 优惠码：BWH26FXH3HIQ，付款时使用可优惠 6.25% 。（重要！）
  
  + 线路质量：香港 KVM > CN2 GIA > CN2 GT > 普通 KVM

## 搬瓦工搭建SS
  + 搬瓦工安装完成后默认系统为 Centos 6 x86 bbr，自带谷歌 BBR 加速优化，不用再额外安装。我们可以直接开始安装SS。
  
  + 安装 wget 命令工具：
    > yum install wget
    
  + 依次运行下面三行命令，如下图所示按提示选择选项。建议：端口选择大于 1000 。
    > wget — no-check-certificate -O shadowsocks.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh
    
    > chmod +x shadowsocks.sh
    
    > ./shadowsocks.sh 2>&1 | tee shadowsocks.log
  + 出现提示语句，依次填写密码、端口、加密方式。回车待配置完成。记录下返回信息
  
## SS多用户配置 
  
  + 切换为英文输入法
  
  + 核对正确再保存，一个逗号都不能多
  
  + 没提到的，除非自己清楚，否则保持默认，不要多改
  
  + 配置好后 重启 shadowsocks 才会生效
  
  + 首先，准备好配置信息，把下面的代码复制到记事本中（# 开头的是注释，不要复制进去）。
  
  + 按要求自行更改 "port\_password"{……} 中的端口和密码，其他默认。
  
    1.编辑好端口和对应的密码
    2.添加或删除的用户都在 "port_password"{……} 中
    3.用户信息格式，注意末尾的英文逗号："端口"："密码",  如 "8006": "123456",
4."method" 为加密方式，可修改，默认也行
  
    {
      "server":"0.0.0.0",
      "local_address":"127.0.0.1",
      "local_port":1080,
      "port_password":{
           "8989":"password0",
           "9001":"password1",
           "9002":"password2",
           "9003":"password3",
           "9004":"password4"
      },
      "timeout":300,
      "method":"aes-256-gcm",
      "fast_open": false
    }
+ 然后，在 /etc 目录下创建 shadowsocks.json 配置文件：

 > vi /etc/shadowsocks.json

 > 进入 vim 后，按 a ，删除原配置信息，然后把刚才准备好的 “配置信息” 粘贴进去，替换掉原内容，检查无误；

+ 重启 shadowsocks 生效：
 
 > /etc/init.d/shadowsocks restart
 
+ 关闭防火墙：
  + service iptables stop
  + chkconfig iptables off
 
 
 + 只要下载客户端连接就 OK 了，全平台支持，win、mac 和 Android 等。（iOS 需在商店中安装）
