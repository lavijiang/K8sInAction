# 1. 创建、运行和共享容器镜像

## 创建应用
```
const http = require('http');
const os = require('os');

console.log("Kubia server starting......");

var handler = function(request, response){
    console.log("Received request from "+request.connection.remoteAddress);
    response.writeHead(200);
    response.end("You've hit "+os.hostname()+"\n");
};

var www = http.createServer(handler);
www.listen(8080);
```
## 创建Dockerfile
```
FROM node:7
ADD app.js /app.js
ENTRYPOINT ["node", "app.js"]
```

## 构建镜像
```
docker build -t kubia .
```

## 运行镜像
```
docker run --name kubia-container -p 8081:8080 -d kubia
```

## 测试访问应用
```
curl localhost:8081
```

## 在已有的容器内部运行shell
```
sudo docker exec -it kubia-container bash
```
我们会发现容器内nodejs的进程运行在主机操作系统上，但是PID不同

## 停止容器
```
docker stop kubia-container
```

## 删除容器
```
docker rm kubia-container
```

## 向镜像仓库推送镜像

### 使用标签标注镜像
```
docker tag kubia lavijiang/kubia
```
### 向docker hub推送镜像(其他仓库也行)
```
docker login
docker push lavijiang/kubia
```

### 在其他机器运行镜像
```
docker run -p 8080:8080 -d lavijiang/kubia
```

# 2. 配置kubernetes集群 

## 安装minikube
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube version
```

## 使用minikube启动一个kubernetes集群
```
minikube start
```

## 安装kubernetes客户端(kubectl)
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
kubectl version
```

## 使用kubectl查看集群是否正常工作
```
kubectl cluster-info
```