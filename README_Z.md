# docker 容器环境搭建

1. gcc和g++ (9.0)
2. cmake (3.18版本以上)
3. 端口放开 22端口(VScode编码远程连接) 9221端口(pika服务端口, 可在.conf/pika.conf配置)

## 创建docker容器
```shell
docker run -itd -p 9221:9221 -p 8030:22 --name pika -v /home/zjq/share/pika:/root/pick -d ubuntu:18.04 /bin/bash
passwd
输入密码
apt update && apt upgrade
apt install vim ssh screen -y
vi /etc/sshd_config # 插入下面四行
Port 22
PubkeyAuthentication yes
PasswordAuthentication yes
PermitRootLogin yes

service ssh restart

```

## cmake升级
```
tar -vxf cmake-3.18.0-Linux-x86_64.tar.gz
mv cmake-3.18.0-Linux-x86_64 /usr/share/cmake-3.18.0
ln -s /usr/share/cmake-3.25.0-linux-x86_64/bin/* /usr/bin/
root@aeece3c36265:~/mycode/llvm-project# cmake --version
cmake version 3.18.0
```

## gcc和g++升级
```shell
apt-get update && \
apt-get install build-essential software-properties-common autoconf -y && \
add-apt-repository ppa:ubuntu-toolchain-r/test -y && \
apt-get update && \
apt-get install gcc-snapshot -y && \
apt-get update && \
apt-get install gcc-9 g++-9 -y && \
update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 60 --slave /usr/bin/g++ g++ /usr/bin/g++-9
gcc -v
g++ -v
```

## 