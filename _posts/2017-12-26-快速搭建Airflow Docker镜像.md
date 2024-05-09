---
layout:     post
title:      快速搭建 Airflow docker 镜像
subtitle:   Airflow映射本地路径
date:       2024-05-09
author:     Mickey
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - Airflow
    - Docker
---


## 前言

在本机使用Docker快速搭建Airflow并启动，并映射本地路径至Docker


## 正文
1. 拉取镜像  
`docker pull  apache/airflow:2.8.2`

2. 拉取配置文件  
`curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.8.2/docker-compose.yaml'`

3. 修改刚刚拉取的yaml文件  
- 关闭示例dag
```
AIRFLOW__CORE__LOAD_EXAMPLES: 'false'
```
- 映射本地路径
```
volumes:
    - 本地路径/dags:/opt/airflow/dags
    - 本地路径/logs:/opt/airflow/logs
    - 本地路径/config:/opt/airflow/config
    - 本地路径/plugins:/opt/airflow/plugins
```

4. 初始化容器  
`docker compose up airflow-init`

5. 启动  
`docker compose up`

访问 http://localhost:8080  
默认账号: airflow  
默认密码: airflow  


### 参考：

- [airflow官方文档](https://airflow.apache.org/docs/apache-airflow/stable/howto/docker-compose/index.html "官方文档")
