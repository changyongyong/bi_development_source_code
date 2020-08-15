# 数据挖掘

大数据挖掘系统，采用前后端分离技术:SpringBoot，Mybatis，Shiro，JWT，Vue & Element

DataX：解决数据导入导出问题
ClickHouse：解决列式存储和计算问题

 
## 技术栈

> 1. Spring Boot
> 2. Vue
> 3、DataX
> 4、ClickHouse 
> 

技术架构：
后端
    1、基础框架：Spring Boot 2.0.3.RELEASE
    2、持久层框架：Mybatis-plus_3.0.6
    3、安全框架：Apache Shiro 1.4.0-RC2，Jwt_3.4.1
    4、数据库连接池：阿里巴巴Druid 1.1.10
    5、缓存框架：redis
    6、日志打印：logback
    7、其他：fastjson，poi，Swagger-ui，quartz, lombok（简化代码）等。

前端
    1、Vue 2.5.22,Vuex,Vue Router
    2、Axios
    3、element-ui
    4、webpack
    5、vue-cropper - 头像裁剪组件
    6、@antv/g2 - Alipay AntV 数据可视化图表
    7、Viser-vue - antv/g2 封装实现
    8、eslint，@vue/cli 3.2.1
    9、vue-print-nb - 打印

开发环境

  语言：Java 8

  IDE(JAVA)： Eclipse安装lombok插件 或者 IDEA

  IDE(前端)： WebStorm 或者 IDEA

  依赖管理：Maven

   数据库：MySQL5.0 

   缓存：Redis

## 快速启动

 
2. 数据库依次导入litemall-db/sql下的数据库文件

    打包
        ```
        cd litemall
     
        cd ./admin-webin
        cnpm install
        
        cnpm run build:dep
        
        cd ..
        
        mvn clean package
        cp -f ./litemall-all/target/litemall-all-*-exec.jar ./deploy/litemall/litemall.jar
        ```
        如果是在Windows下，可以直接用命令方式启动：
        java -jar bianwu.jar --servercd.port=9090
        
        //如果在Linux下，用以下命令方式启动
        nohup java -jar --servercd.port=8089 litemall.jar & 
        
        //阿里云RDS本机端口映射
        netsh interface portproxy add v4tov4 listenport=映射端口 connectaddress=RDS服务器IP connectport=端口
        netsh interface portproxy delete v4tov4 listenport=映射端口
4. 启动管理后台前端

    打开命令行，输入以下命令
    ```bash
    npm install -g cnpm --registry=https://registry.npm.taobao.org
    cd litemall/litemall-admin
    cnpm install
    cnpm run dev
    ```
    此时，浏览器打开，输入网址`http://localhost:9527`, 此时进入管理后台登录页面。
    
   
## 开发计划

当前版本[v1.3.0](https://linlinjava.gitbook.io/litemall/changelog)

目前项目开发中，存在诸多不足，以下是目前规划的开发计划。

V 1.0.0 完成以下目标：

1. 除了部分功能（如优惠券等），小商城的优化和改进基本结束；
2. 管理后台基本实现所有表的CRUD操作；
3. 后端服务能够对参数进行检验。

V 2.0.0 完成以下目标：

1. 小商城和管理后台完成所有基本业务；
2. 管理后台实现统计功能、日志功能、权限功能；
3. 业务代码和细节代码进行调整优化；
4. 轻商城的开发；

V 3.0.0 完成以下目标：

1. 管理后台一些辅助功能
2. 后端服务加强安全功能、配置功能
3. 缓存功能以及优化一些性能


   
## 问题
 
//注册组件
mvn install:install-file -Dfile=taobao-sdk-java-auto_1455552377940-20160607.jar -DgroupId=com.taobao -DartifactId=api -Dversion=1.0 -Dpackaging=jar

如果删除了Mysql中的表字段，在视图里有恰好有这些字段，则用下面的方法查询视图语句:
SELECT VIEW_DEFINITION FROM INFORMATION_SCHEMA.VIEWS
WHERE  TABLE_NAME = '视图名称';

mysql 查询死锁并且删除死锁
SELECT * FROM INFORMATION_SCHEMA.INNODB_TRX;
kill 81431


问题描述：
Unexpected end of JSON input while parsing near '…"

解决办法：
（1）npm install --registry=https://registry.npm.taobao.org --loglevel=silly
（2） npm cache clean --force
（3） npm install

在创建getPY函数时要先执行下面的语句
set global log_bin_trust_function_creators=TRUE;
SHOW  VARIABLES LIKE 'innodb_flush_log_at_trx_commit' ;
--加快数据写入速度
SET GLOBAL innodb_flush_log_at_trx_commit =0;
--恢复安全写入速度
SET GLOBAL innodb_flush_log_at_trx_commit =1;

将mysql数据库高版本导入到低版本时要更新替换的类型如下:
datetime(0) datetime
datetime(3) datetime
datetime(6) datetime
timestamp(3) timestamp
CURRENT_TIMESTAMP(3) CURRENT_TIMESTAMP
utf8mb4_0900_ai_ci utf8mb4_unicode_ci

