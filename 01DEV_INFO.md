#智慧能源云平台基本开发信息概览
[TOC]

# 1 项目技术概况
- 主站平台1.0 使用技术概览：

  jdk版本：1.7

​                后端：Spring+SpringMVC+Hibernate/SpringJDBCTemplate+velocity；

​		前端：javascript+jquery+AdminlteUI+H5+CSS3

​		web服务器：tomcat7.0

​                数据库：mysql-5.6

- 主站平台2.0使用技术概览：

  在1.0的基础上，平台新业务（购售电业务）

  构建工具：maven；

  前端：增加使用angularJS，用来进行前后端分离；

  ​

# 2 服务器信息：
## 2.1 公司环境

- SVN地址：

https://192.168.25.48:8443/svn/研发部/项目管理/P2017002(爱康智慧能源云平台)/02开发区/02代码/trunck

- 数据库地址

## 2.2 现场环境  

- svn地址

  > https://192.168.3.179:8443/svn/akcome/02开发区/02代码


- bugfree

  > http://192.168.3.179:8082/bugfree/index.php 


- 服务器信息：

  | 应用           | 地址    | 服务器用户信息 | 中间件   | 中间件用户信息 |
  | ------------ | ----- | ------- | ----- | ------- |
  | 生产数据库        | 3.179 |         | mysql |         |
  | 生产应用（TOMCAT） | 3.188 |         |       |         |
  | 生产采集         |       |         |       |         |
  | 测试应用         |       |         |       |         |
  | 测试数据库        |       |         |       |         |
  | 开发数据库        |       |         |       |         |
  ​

# 3 MAVEN 信息 @SINCE V2
## 3.1 私服信息 
- 公司私服

- 现场私服

  私服版本：nexus 2

  私服地址： http://192.168.3.179:8081/nexus/

  公开仓库： /content/groups/public/

  管理账号密码： admin/ 123

# 4 模块说明

## 4.1 基础模块（必须）

- emplatform 
> 主项目。即War

  - ~~emplatform-modules-ui~~
   > ~~基础模块** 为前台页面提供 easy-ui 框架。（项目中主要为元数据、非业务功能模块目前使用）~~

  - emplatform-modules-ui.adminlte
  > 为前台提供 基于bootstrap的adminlte的UI组件等静态资源。

  - emplatform.modules.metadata
  > **基础模块** 元数据模块，提供监测对象、指标等元数据内容的功能

  - emplatform.modules.mainindex
  > **基础模块** 提供不同角色的登陆页 ，首页，菜单框架页

  - emplatform.modules.style
  > **基础模块** 重写底层jar包（cn.com.ksplatform.ui）主要提供 include.vm等 包含。
  - akcome-modules-common-service
  > 提供各种服务接口。包含：用户、组织机构、角色、各监测对象的用电指标。

## 4.2 业务模块

### 4.2.1 需求侧

- ~~emplatform.modules.monitor~~
> ~~能效：用电监测~~
- emplatform.modules.monitor-ex 
> 能效：用电监测
>
> @SINCE V2.0.0  变更为 emplatform.modules.monitor

- akcome-modules-analysis
> 能效：用能分析
- akcome-modules-policy-server
> 政策法规（售电政策）、有序用电、需求响应的发布编辑、查看

 - 交易和结算页面使用HTML+js+css来实现
    对应模块：![](index_files/7e034afe-209b-4626-ba6d-864617d137ab.png)

### 4.2.2 购售电



#   



# 6 编码要求

## 6.1 java编码规范

## 6.2 注释规范

- eclipse 注释规范

> [点击下载 eclipse 注释规范。](http://files.git.oschina.net/group1/M00/01/38/PaAvDFkNj_yAOFLLAAAL7oEq7Oc242.xml?token=c0bf14fee0d402d6d07a395c91f58ff1&ts=1494061053&attname=codetemplates.xml "点击下载 eclipse 注释规范。")

- intellj idea 规范
> ``#`` TODO


## 6.3 前后端分离
前台视图通过JSON数据与后台进行交互。

## 6.4 ORM与数据库解耦
- DAO层增删改查，遵守Hibernate映射关系进行编写
- 复杂的查询，在数据库层编写VIEW，写好VIEW统一交由DBA进行创建。通过DAO层映射VIEW。
- 避免使用存储过程
# 7 DEMO示例
- 模块示例
 - 非mavne模块
     ![](index_files/f8239a19-bda8-4efe-9f86-4c41fb1fac8a.png)
 - maven模块 @SICNE V2

```
akcome-modules-policy-web     ## 页面jar包  
  - src/main/java             
  - src/test/java               
  - src/view/page             ## vm

akcome-modules-policy-server  ## 页面jar包
  - src/main/java             ## java
     - cn.com.gdt.akcome.dsm.policy
        - dao
        - model
        - service
        - controller
  - src/main/resource         ## 资源文件夹
  - src/test/java               
  - src/view/page             
```

# 8 部分公共接口说明

*``TODO``  swagger公布后端接口*

## 8.1 采集数据接口说明

## 8.2 树形结构使用说明

## 8.3 获取系统参数、码表字段值

- 获取系统参数
 - java
```java

    @Autowired
    PlatParamItemService paramItenService;
    
    @RequestMapping("/go")
    public String go(){
        PlatParamItem welcome = paramItenService.getParam("SYS_INDEX");
    
    }
```
 - JS
 ``` javascript
260: var param = PlatForm.System.Cache.getParam("SYS_TITLE");  
 ```
- 获取码表数据
 - java

``` javascript
根据数据字典类型获取一组数据字典值
PlatDictTypeService dictTypeService;
ArrayList list = dictTypeService.getPlatDict(ecode);

根据数据字典类型  和  key值 取出value

```
   -  js


```javascript
javascript
// 根据码表类型 获取一组码表数据
var items = PlatForm.System.Cache.getDictItems(dataType);  

// 根据码表类型 和 数据key值获取一个码表value
PlatForm.System.Cache.getDictItems(dataType,key);
```



