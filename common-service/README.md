# common-service
服务层项目，结构是soa/[api; service]。api的接口或常量变动，必须升级版本号。

本层继承parent pom，依赖基础公包、common组件包、soa的api包。前两者的版本号由父pom定义，后者的版本号自己维护。
