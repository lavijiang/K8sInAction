# 阿里云的镜像仓库
https://cr.console.aliyun.com/repository/cn-hangzhou/lavijiang/lavijiang/details

# 登录阿里云Docker Registry
```
$ docker login --username=tb_5916533 registry.cn-hangzhou.aliyuncs.com
```

# 从Registry中拉取镜像
```
$ docker pull registry.cn-hangzhou.aliyuncs.com/lavijiang/lavijiang:[镜像版本号]
```

# 推送镜像
```
$ docker login --username=tb_5916533 registry.cn-hangzhou.aliyuncs.com
$ docker tag [ImageId] registry.cn-hangzhou.aliyuncs.com/lavijiang/lavijiang:[镜像版本号]
$ docker push registry.cn-hangzhou.aliyuncs.com/lavijiang/lavijiang:[镜像版本号]
```

# 示例
![推送的阿里云镜像](../pics/first%20packed%20image.jpg)  
