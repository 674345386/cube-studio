# 生产部署

基础环境依赖
docker >= 19.03
kubernetes >=1.18
ssd ceph > 10T  挂载到每台机器的 /data/k8s/
单机 磁盘>=1T   单机磁盘容量要求不大，仅做镜像容器的的存储
控制端机器 cpu>=32 mem>=64G * 2
任务端机器，根据需要自行配置

本平台依赖k8s/kubeflow/prometheus/efk相关组件，请优先参考install/kubenetes/readme.md 部署依赖组件。


# 本地调试

## deploy mysql

```
linux
docker run --network host --restart always --name mysql -e MYSQL_ROOT_PASSWORD=admin -d mysql:5.7
mac
docker run -p 3306:3306 --restart always --name mysql -e MYSQL_ROOT_PASSWORD=admin -d mysql:5.7

```
进入数据库创建一个db
```
CREATE DATABASE IF NOT EXISTS kubeflow DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
```
镜像构建


```
构建基础镜像（包含基础环境）
docker build -t ai.tencentmusic.com/tme-public/myapp:base -f install/docker/Dockerfile-base .

使用基础镜像构建生产镜像
docker build -t ai.tencentmusic.com/tme-public/myapp:2021.10.01.1 -f install/docker/Dockerfile .
```

镜像拉取(如果你不参与开发可以直接使用线上镜像)
```
docker pull ai.tencentmusic.com/tme-public/myapp:2021.10.01.1
```

## deploy myapp (docker-compose)

本地开发使用

docker-compose.yaml文件在install/docker目录下，这里提供了mac和linux版本的docker-compose.yaml。
可自行修改
image：刚才构建的镜像
LOGIN_URL地址：登录重定向地址
MYSQL_SERVICE：mysql的地址


1) build fore
```
STAGE: 'build'
docker-compose -f docker-compose.yml  up
```
2) debug backend
```
STAGE: 'dev'
docker-compose -f docker-compose.yml  up
```
3) Production
```
STAGE: 'prod'
docker-compose -f docker-compose.yml  up
```

部署以后，登录首页 会自动创建用户，绑定角色（Gamma和username同名角色）。

可根据自己的需求为角色授权。


## 可视化页面

页面资源镜像制作：
```sh
cd myapp/vision && docker build --no-cache ./ -t your_images_name:your_label --network host
```

项目资源打包：
```
开发环境要求：
node: 14.15.0+
npm: 6.14.8+

包管理（建议使用yarn）：
yarn: npm install yarn -g
```
```sh
cd myapp/vision && yarn && yarn build
```

输出路径：`/myapp/static/appbuilder`
