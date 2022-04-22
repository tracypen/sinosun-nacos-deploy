## B+Nacos容器化部署指南

### 一、获取镜像

#### 方法一：通过DockerHub仓库获取

> 不推荐，因为官方镜像体积很大1G+，柔和了很多不用的插件和UI库

#### 方法二： 制作镜像

> 推荐，目前经过简单的优化，镜像大小为750M

##### 1.获取JAR文件
可以通过以下两种方式获取
- release包（推荐）
- 通过源码编译
##### 2.构建
- 将JAR文件拷贝至./nacos-docker-build/nacos/target目录下

- 在./nacos-docker-build目录下执行

```shell
docker build -t xast.test.com/sinosun/nacos-server:2.0.2
```

- 推送至B+Docker私服

```shell
xast.test.com/sinosun/nacos-server:2.0.2
```

### 二、部署运行

> 默认以集群三节点部署，如需要单节点部署，参考官方文档修改 MODE参数为standalone即可

##### 1. 启动Mysql（可选）

如果已有Mysql，则跳过

- 编辑`./nacos-k8s-deploy/nacos-mysql-local.yaml`,修改相关参数

- 执行`./nacos-k8s-deploy/kubectl apply -f ./nacos-k8s-deploy/nacos-mysql-local.yaml `

##### 2. 部署Naocs

- 编辑`./nacos-k8s-deploy/nacos-deploment.yaml`

- 修改相关参数

其中namespace、镜像名、configMap需要特别注意

- 执行`kubectl apply -f ./nacos-k8s-deploy/nacos-deployment.yaml `


### 三、参考文档
- [nacos-github](https://github.com/alibaba/nacos)
- [nacos-docker](https://github.com/nacos-group/nacos-docker.git)
- [nacos-k8s](https://github.com/nacos-group/nacos-k8s)