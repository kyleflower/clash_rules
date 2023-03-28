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
### 2.4 更换远程规则
VPS找到 `/root/sub-web/src/views/Subconverter.vue` 文件，找到 258行 `remoteConfig: [`，敲下回车，插入下面内容
```
{
    label: "ACL4SSR",
    options: [
        {
            label: "ACL4SSR_Online 默认版 分组比较全 (与Github同步)",
            value: "https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online.ini"
        },

        {
            label: "ACL4SSR_Online_AdblockPlus 更多去广告 (与Github同步)",
            value: "https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online_AdblockPlus.ini"
        },

        {
            label: "ACL4SSR_Online_NoAuto 无自动测速 (与Github同步)",
            value:"https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online_NoAuto.ini"
        },

        {
            label: "ACL4SSR_Online_NoReject 无广告拦截规则 (与Github同步)",
            value:"https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online_NoReject.ini"
        },

        {
            label: "ACL4SSR_Online_Mini 精简版 (与Github同步)",
            value:"https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online_Mini.ini"
      },

      {
            label: "ACL4SSR_Online_Mini_AdblockPlus.ini 精简版 更多去广告 (与Github同步)",
            value:"https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online_Mini_AdblockPlus.ini"
      },

      {
            label: "ACL4SSR_Online_Mini_NoAuto.ini 精简版 不带自动测速 (与Github同步)",
            value:"https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online_Mini_NoAuto.ini"
      },

      {
            label: "ACL4SSR_Online_Mini_Fallback.ini 精简版 带故障转移 (与Github同步)",
            value:"https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online_Mini_Fallback.ini"
      },

      {
            label: "ACL4SSR_Online_Mini_MultiMode.ini 精简版 自动测速、故障转移、负载均衡 (与Github同步)",
            value:"https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online_Mini_MultiMode.ini"
      },

      {
          label: "ACL4SSR_Online_Full 全分组 重度用户使用 (与Github同步)",
          value:"https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online_Full.ini"
      },

      {
          label: "ACL4SSR_Online_Full_NoAuto.ini 全分组 无自动测速 重度用户使用 (与Github同步)",
          value:"https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online_Full_NoAuto.ini"
      },

      {
          label: "ACL4SSR_Online_Full_AdblockPlus 全分组 重度用户使用 更多去广告 (与Github同步)",
          value:"https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online_Full_AdblockPlus.ini"
      },

      {
          label: "ACL4SSR_Online_Full_Netflix 全分组 重度用户使用 奈飞全量 (与Github同步)",
          value:"https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online_Full_Netflix.ini"
      },

      {
          label: "ACL4SSR 本地 默认版 分组比较全",
          value: "config/ACL4SSR.ini"
      },

      {
          label: "ACL4SSR_Mini 本地 精简版",
          value: "config/ACL4SSR_Mini.ini"
      },

      {
          label: "ACL4SSR_Mini_NoAuto.ini 本地 精简版+无自动测速",
          value: "config/ACL4SSR_Mini_NoAuto.ini"
      },

      {
          label: "ACL4SSR_Mini_Fallback.ini 本地 精简版+fallback",
          value: "config/ACL4SSR_Mini_Fallback.ini"
      },

      {
          label: "ACL4SSR_BackCN 本地 回国",
          value: "config/ACL4SSR_BackCN.ini"
      },

      {
          label: "ACL4SSR_NoApple 本地 无苹果分流",
          value: "config/ACL4SSR_NoApple.ini"
      },

      {
            label: "ACL4SSR_NoAuto 本地 无自动测速 ",
            value: "config/ACL4SSR_NoAuto.ini"
      },

      {
            label: "ACL4SSR_NoAuto_NoApple 本地 无自动测速&无苹果分流",
            value: "config/ACL4SSR_NoAuto_NoApple.ini"
      },

      {
            label: "ACL4SSR_NoMicrosoft 本地 无微软分流",
            value: "config/ACL4SSR_NoMicrosoft.ini"
      },

      {
            label: "ACL4SSR_WithGFW 本地 GFW列表",
            value: "config/ACL4SSR_WithGFW.ini"
      }
    ]
  },
```

### 2.5 部署前端
```
sudo docker build -t subweb-local:latest .
```
```
sudo docker run -d -p 58080:80 --restart always --name subweb subweb-local:latest
```
