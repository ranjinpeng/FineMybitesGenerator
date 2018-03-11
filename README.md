# MybitesGenerator定制化开发

本源码已经配置好，可直接下载用maven打出jar包后替换mybatis-generator-core-1.3.2文件

如果需要更多定制化开发可以读源码增加自己的定制化开发。本项目添加了对swagger-ui的支持

添加了mybites3Simple方式的生成的Selective方法.并可通过修改配置开关注释，swagger等功能。

使用的 generator.xml 文件如下

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
  PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
  "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">

<generatorConfiguration>


  <context id="DB2Tables" targetRuntime="MyBatis3Simple">

      <commentGenerator type="org.mybatis.generator.internal.DG2CommentGenerator">
          <property name="suppressAllComments" value="true"/>
          <property name="suppressDate" value="true"/>
          <property name="generalsettings" value="noget,nomethod,noset"/>//自定义的参数，可
        //  通过配置开关注释和swagger注解  使用方式用“，”号隔开 
        //  noget 取消get方法注释
       	//  noset 取消set方法注释
       	//  nofile 取消swagger注解及字段注释
       	//  nomethod 取消mapper方法注释
       	  
      
      </commentGenerator>

    <jdbcConnection driverClass="com.mysql.jdbc.Driver"
			connectionURL="jdbc:mysql://127.0.0.1:3306/db?useUnicode=true&amp;characterEncoding=utf-8"
			userId="root" password="pwd" />

<!--
    <javaTypeResolver >
      <property name="forceBigDecimals" value="false" />
    </javaTypeResolver>
	-->


    <javaModelGenerator targetPackage="cn.entity" targetProject="src">
    </javaModelGenerator>

    <sqlMapGenerator targetPackage="cn.dao"  targetProject="src">
    </sqlMapGenerator>

    <javaClientGenerator type="XMLMAPPER" targetPackage="cn.dao"  targetProject="src">
    </javaClientGenerator>
	
      <table tableName="admin" domainObjectName="Admin">
     	<generatedKey column="adminid" sqlStatement="SELECT MD5(UUID())"  />
      </table>


  </context>
</generatorConfiguration>
```

使用MyBatis3Simple 可以不生成那些用不到的****Example文件，且本项目会生成常用的Selective方法