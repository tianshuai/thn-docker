## 太火鸟开发环境Docker

### 说明
* 公司：太火鸟
* 作者：田帅
#### 已配置的环境
* nginx
* mongo
* redis
* centos

#### docker配置目录结构
> -thn-docker/  
> --docker-compose.yml  
> --.env_example   
> --README.md  
> --etc/  
> ---nginx.conf   
> ---conf.d/  
> ----default.conf  
> ----thn.conf    
> ---mongod.conf  
> ---redis.conf  
> --data_volume/  
> ---Dockerfile  
> --nginx/  
> ---Dockerfile  
> --centos/  
> ---Dockerfile  
> --mongo/  
> ---Dockerfile  
> --redis/  
> ---Dockerfile  

#### docker数据及日志目录结构demo(需要自建)
> -/data/thn-docker/  
> --nginx/  
> ---log/  
> ----access.log  
> --mongo/  
> ---db/  
> ---log/  
> --redis/  
> ---db/  
> ---log/  
> --centos/  
> ---log/  
> ---pid/   

### 安装步骤
#### 首次安装
* 安装docker及docker-compose插件，根据当前系统自行安装及配置
* 复制根目录文件`docker-compose_example.yml` 到`docker-compose.yml`，根据自身需求微调
* 复制根目录文件`.env_example` 到`.env`，同时根据自身需求修改配置
* 自行创建数据目录，包括日志文件、数据库等，格式参考目录结构demo
* 执行命令 `docker-compose build` 

#### 命令介绍
* 启动容器： `docker-compose up -d 容器名`
* 停止所有容器：`docker-compose down`
* 带终端运行某个容器：`docker-compose run 容器名 bash`
* 启用|关闭某个容器：`docker-compose stop|start 容器名`
* 查看运行的容器：`docker ps`
* 查看所有容器：`docker ps -a`
* 查看所有镜像：`docker images`

