一、环境准备

1、apt换源
https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/
sudo gedit /etc/apt/sources.list
sudo apt update

2、安装docker、docker-compose
sudo apt install docker docker-compose
sudo systemctl enable docker
sudo usermod -a -G docker <username>

3、安装golang
https://go.dev/doc/install
sudo su
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.18.2.linux-amd64.tar.gz
gedit /etc/profile
	export PATH=$PATH:/usr/local/go/bin
gedit ~/.bashrc
	source /etc/profile

4、docker加速器
https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors

二、安装fabric-sample

1、手动创建脚本，安装samples、docker
https://github.com/hyperledger/fabric/blob/main/scripts/bootstrap.sh
修改binaries=false
sudo chmod u+x bootstrap.sh
./bootstrap.sh

2、安装binaries
https://github.com/hyperledger/fabric/releases/download/v2.4.3/hyperledger-fabric-linux-amd64-2.4.3.tar.gz
https://github.com/hyperledger/fabric-ca/releases/download/v1.5.3/hyperledger-fabric-ca-linux-amd64-1.5.3.tar.gz
tar -xzvf 压缩包名 -C 目的地

3、配置go代理
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn,direct