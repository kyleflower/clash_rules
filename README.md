# subweb前端和后端搭建教程-docker版

- - -
## 1.搭建后端Subconverter
代码如下
```
docker run -d --name subcon --restart=always -p 25500:25500 tindy2013/subconverter:latest
```
- - -
## 2.搭建并配置前端
如果用docker搭建，需要配置前端之后，重新build镜像
### 2.1 Clone项目到本地
```
git clone https://github.com/CareyWang/sub-web.git
cd sub-web
```
### 2.2 编辑.env配置文件
```
vi .env
```
```
# 修改后端地址、短链接地址
# API 后端
VUE_APP_SUBCONVERTER_DEFAULT_BACKEND = "需要修改|http://***.**.***.***:25500/sub?"
# 短链接后端
VUE_APP_MYURLS_DEFAULT_BACKEND = "https://i.2z.pw"
# 文本托管后端
VUE_APP_CONFIG_UPLOAD_BACKEND = "https://convert.imgki.com"
```
### 2.3 编辑.vue配置文件
```
cd src/views
vi Subconverter.vue
```
```
#39行
placeholder="http://***.**.***.***:25500/sub?"
#300行
backendOptions: [{ value: "http://***.**.***.***:25500/sub?" }],
```
### 2.4 部署前端
```
sudo docker build -t subweb-local:latest .
```
```
sudo docker run -d -p 58080:80 --restart always --name subweb subweb-local:latest
```
