# docker_lnmp

## 部署项目的正确姿势
1. 先docker-compose.yml 配置正确的版本和端口MySQL root账户密码应用数据库名
2. conf/nginx/conf.d/ 下部署站点
3. sudo docker-compose up -d
---
### Use
````
git clone https://github.com/1cool/docker_lnmp.git
````
````
cd docker_lnmp
````
````
在保证启动docker服务的前提下
sudo docker-compose up 
ok 如果你的端口没有占用的话服务应该就在在运行了
可以通过命令 sudo docker-compose ps 查看运行情况
````
---
### 说明
1. 如果需要修改php,mysql,nginx版本。以MySQL为例（修改其余的同MySQL一样）过程如下：
- 打开 docker-compose.yml
- 找到MySQL模块，修改  image: mysql:5.7 后边的数字就行
````
mysql:
    container_name: mysql
    image: mysql:5.6  //修改为5.6
    ports:
      - "3366:3306" 
    environment:
         MYSQL_ROOT_PASSWORD: "MySQL root用户密码"
         MYSQL_DATABASE: "你的应用的MySQL库名"
         其余配置请自行查看docker文档
````
- 其中 ports 第一个参数表示你本地的映射端口，第二个表示docker容器里服务运行的端口。以nginx为例，以下参数说明。
你访问 http://localhost:8000 的时候会访问docker容器里80端口部署的应用
````
 ports:
      - "8000:80" 
````

### nginx部署应用
- 打开1cool-dnmp/conf/nginx/conf.d/ 文件夹
- 如果你有多个站点，就配置多个conf，如：
site1.conf,site2.conf,site3.conf，site4.conf ……
- 和正常的nginx 部署项目一样配置一样，自行配置即可
---
### 常用命令
1. 启动docker容器
````
sudo docker-compose up
````
2. 查看docker容器运行情况
````
sudo docker-compose ps
````
3. 关闭docker某个服务/所有服务
````
sudo docker-compose stop nginx
sudo docker-compose stop 
sudo docker-compose restart 
````
4. 进入某个容器内
````
sudo docker exec -it php bash //进入php容器 

说明 php 是你的docker-compose.yml 配置里 php模块 container_name 定义的容器名称
````