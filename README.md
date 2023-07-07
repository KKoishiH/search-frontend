# 聚合搜索平台
## 项目简介
基于vue3 + Spring boot + Elastic Stack的一站式聚合搜索平台(也是简化版的企业用搜索中台)  
  
对于用户使用来说，使用该平台搜索出来自不同数据源、不同类型的内容，提升用户的检索效率和搜索体验  
对于实际应用来说，当企业内部有多个项目的数据都存在搜索需求时，无需针对每个项目单独开发搜索功能，可以直接将各项目的数据源接入此搜索中台，从而提升开发效率、降低维护成本
  
## 技术选型
**前端**
> - Vue3
> - Ant Design Vue 组件库 v4.0
> - 页面状态同步
**后端**
> - SpringBoot 2.7 + springboot-init万用模板
> - MySQL数据库(8.x)
> - Elastic Stack
>   - Elasticsearch搜索引擎
>   - Logstash数据管道
>   - Kibana数据可视化
> - 数据抓取(jsoup、HttpClient爬虫)
>   - 离线
>   - 实时
> - Jmeter压力测试