<img width="583" alt="image" src="https://user-images.githubusercontent.com/35073431/211437995-f96fb880-ecbc-4d66-bfcf-c5b494315f12.png">

<img width="557" alt="image" src="https://user-images.githubusercontent.com/35073431/211438010-aff3807e-6ab1-40d4-9be6-32958fdf12ad.png">

<img width="557" alt="image" src="https://user-images.githubusercontent.com/35073431/211438039-e12162de-084d-4239-bf22-17af515af65c.png">

<img width="638" alt="image" src="https://user-images.githubusercontent.com/35073431/211444557-43f5d870-6520-4b0b-a945-011babc98f05.png">


https://docker.easydoc.net/doc/81170005/cCewZWoN/lTKfePfP

## 安装软件
'''
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
'''
https://docs.docker.com/engine/reference/commandline/run/


## 制作镜像
编写dockerfile
'''
FROM node:11
MAINTAINER easydoc.net

- 复制代码
ADD . /app

- 设置容器启动后的默认运行目录
WORKDIR /app

- 运行命令，安装依赖
- RUN 命令可以有多个，但是可以用 && 连接多个命令来减少层级。
- 例如 RUN npm install && cd /app && mkdir logs
RUN npm install --registry=https://registry.npm.taobao.org

- CMD 指令只能一个，是容器启动后执行的命令，算是程序的入口。
- 如果还需要运行其他命令可以用 && 连接，也可以写成一个shell脚本去执行。
- 例如 CMD cd /app && ./start.sh
CMD node app.js
'''

'''
docker build -t test:v1 .
'''
-t name:tag 用于指定名字
.表示当前目录

运行
'''
docker run -p 8080:8080 --name test-hello test:v1
'''

## 目录挂载
现存问题
- 使用 Docker 运行后，我们改了项目代码不会立刻生效，需要重新build和run，很是麻烦。
- 容器里面产生的数据，例如 log 文件，数据库备份文件，容器删除后就丢失了。

bind mount 方式用绝对路径 -v D:/code:/app
volume 方式，只需要一个名字 -v db-data:/app
docker run -p 8080:8080 --name test-hello -v D:/code:/app -d test:v1

## 多容器通信
创建一个名为test-net的网络：
'''
docker network create test-net
'''
运行 Redis 在 test-net 网络中，别名redis
'''
docker run -d --name redis --network test-net --network-alias redis redis:latest
'''
修改代码中访问redis的地址为网络别名
![image](https://user-images.githubusercontent.com/35073431/211436778-70905949-dd72-4489-bf27-cba0d1eea0f9.png)

## Docker-Compose
如果项目依赖更多的第三方软件，我们需要管理的容器就更加多，每个都要单独配置运行，指定网络。
使用 docker-compose 把项目的多个服务集合到一起，一键运行。

在docker-compose.yml 文件所在目录，执行：docker-compose up就可以跑起来了。

## 发布部署
镜像仓库：镜像仓库用来存储我们 build 出来的“安装包”，Docker 官方提供了一个 镜像库，里面包含了大量镜像，基本各种软件所需依赖都有，要什么直接上去搜索。
- 首先你要先 注册一个账号
- 创建一个镜像库
- 命令行登录账号：
'''
docker login -u username
'''
- 新建一个tag，名字必须跟你注册账号一样
'''
docker tag test:v1 username/test:v1
'''
- 推上去
'''
docker push username/test:v1
'''
- 部署试下
'''
docker run -dp 8080:8080 username/test:v1
'''


