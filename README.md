## 太火鸟开发环境-docker

### 说明
* 公司：太火鸟
* 作者：田帅
#### 已配置的环境
* nginx
* php56
* php72
* mongodb
* redis
* mysql

#### docker配置目录结构demo
> -thn-docker  
> --docker-compose.yml  
> --.env_example  
> --README.md  
> --nginx  
> ---conf  
> ----conf.d  
> ----nginx.conf  
> ---Dockerfile  
> --mysql  
> ---Dockerfile  
> ---conf  
> ----my.cnf  

#### docker数据及日志目录结构demo(需要自建)
> -/data/docker/  
> --nginx/  
> ---log/  
> ----access.log  
> --mongo/  
> ---db/  
> ---log/  

### 安装步骤
#### 首次安装
* 安装docker及docker-compose插件，根据当前系统自行安装及配置
* 复制根目录文件`.env_example` 到`.env`，同时根据自身需求修改配置
* 自行创建数据目录，包括日志文件、数据库等，格式参考目录结构demo
* 执行命令 `docker-compose build` 

#### 命令介绍
* 启动所有容器： `docker-compose up -d`
* 停止所有容器：`docker-compose down`
* 启用|关闭某个容器：`docker-compose stop|start 容器名`
* 查看运行的容器：`docker ps`
* 查看所有镜像：`docker images`

