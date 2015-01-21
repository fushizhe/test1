
CodeGen代码自动生成工具
================================


### 简介
  CodeGen是一款基于FreeMarker和MyBatis Generator的代码自动生成工具。它主要的功能是针对单个
或者多个数据库表自动生成增加，删除，修改，查询的框架代码。
### 目录
#### [使用方法](#usage)
1.	[概述](#usage1)
2.	[整体架构](#usage2)

#### [项目相关元素详解](#ele)
1.	[\<generatorConfiguration\>](#ele1)
2.	[\<classPathEntry/\>](#ele2)
3.  [\<context\>](#ele3)
4.	[\<commentGenerator\>](#ele4)
5.	[\<jdbcConnection\>](#ele5)
6.	[\<javaTypeResolver\>](#ele6)
7.	[\<javaModelGenerator\>](#ele7)
8.	[\<sqlMapGenerator\>](#ele8)
9.	[\<javaClientGenerator\>](#ele9)
10. [\<projectProfile\>](#ele10)

#### [表相关元素详解](#tle)
1.	[\<table\>](#tle1)
2.	[\<listView\>, \<listElement\>](#tle2)
3.	[\<editView\>, \<editElement\>](#tle3)
4.  [\<searchView\>, \<searchElement\>](#tle4)
5.  [\<detailView\>, \<detailElement\>](#tle5)
6.  [\<ref-list\>](#tle6)



<a name="usage"/>
<a name="usage1"/>
#### 使用方法
##### 概述
  开发人员只需要配置一个单独的XML文件，指明所需生成的框架的相关参数，执行程序，框架代码即可生成。

<a name="usage2"/>
##### 整体架构
  CodeGen代码自动生成工具的整体架构图：

![alt text](http://image16-c.poco.cn/mypoco/myphoto/20150121/14/6445810220150121145234015.png?778x398_130 "架构")

<a name="ele"/>
<a name="ele1"/>
#### 项目相关元素详解
#####  <generatorConfiguration>
所有的关于自动生成的配置项都应该在该元素下。

<a name="ele2"/>
##### \<classPathEntry/\>
该元素指明数据库驱动地址：
```xml
<classPathEntry location="E:/Code/java5/mysql-connector-java-5.1.33.jar"/>
```

<a name="ele3"/>
##### \<context\>
该元素指明数据库上下文：
```xml
<context id="DB2Tables" targetRuntime="MyBatis3" componentName="classification">
```

<a name="ele4"/>
##### \<commentGenerator\>
该元素可以设置自动生成的注释的形式：
```xml
<commentGenerator>
    <property name="suppressDate" value="true"/>
    <!-- 是否去除自动生成的注释 true：是 ： false:否 -->
    <property name="suppressAllComments" value="true"/>
</commentGenerator>
```

<a name="ele5"/>
##### \<jdbcConnection\>
该元素可以设置数据库的链接类，地址，用户名，密码：
```xml
<jdbcConnection driverClass="com.mysql.jdbc.Driver" connectionURL="jdbc:mysql://192.168.1.135:3306/demotest" userId="root" password="mysqlpwd">
</jdbcConnection>
```

<a name="ele6"/>
##### \<javaTypeResolver\>
该元素可以用于指定一个用户提供的Java类型解析器：
```xml
<javaTypeResolver>
  <property name="forceBigDecimals" value="false"/>
</javaTypeResolver>
```

<a name="ele7"/>
##### \<javaTypeResolver\>
该元素可以用于指定一个用户提供的Java类型解析器：
```xml
<javaModelGenerator targetPackage="com.canco.classification.model" targetProject="E:/Code/java5/TestProject">
  <property name="enableSubPackages" value="true"/>
  <property name="trimStrings" value="true"/>
</javaModelGenerator>
```

<a name="ele8"/>
##### \<sqlMapGenerator\>
该元素可以用于指定生成映射文件的包名和位置：
```xml
<sqlMapGenerator targetPackage="com.canco.classification.mapping" targetProject="E:/Code/java5/TestProject">
  <property name="enableSubPackages" value="true"/>
</sqlMapGenerator>
```

<a name="ele9"/>
##### \<javaClientGenerator\>
该元素可以用于指定生成DAO的包名和位置：
```xml
<javaClientGenerator type="XMLMAPPER" targetPackage="com.canco.classification.dao" targetProject="E:/Code/java5/TestProject">
  <property name="enableSubPackages" value="true"/>
</javaClientGenerator>
```

<a name="ele10"/>
##### \<projectProfile\>
该元素可以用于指定生成的项目包名和位置：
```xml
<projectProfile packageName="com.canco" projectName="E:/Code/java5/TestProject">
</projectProfile>
```

<a name="tle"/>
<a name="tle1"/>
#### 表相关元素详解
##### \<table\>
该元素用于配置要自动生成代码的表，针对每个表可以在其子元素内配置展示层的展示方式：
```xml
<table tableName="asset_list" domainObjectName="AssetList" enableCountByExample="true" enableUpdateByExample="true" enableDeleteByExample="true" enableSelectByExample="true" selectByExampleQueryId="true">
  <listView>
    <listElement>
      <property name="attrName" value="asset_id"/>
      <property name="labelName" value="asset.id"/>
      <property name="zhLabelName" value="资产ID"/>
      <property name="enLabelName" value="ID"/>
      <property name="order" value="1"/>
      <property name="key" value="true"/>
    </listElement>
    <listElement>
      <property name="attrName" value="asset_name"/>
      <property name="zhLabelName" value="资产名"/>
      <property name="enLabelName" value="Asset Name"/>
      <property name="labelName" value="asset.name"/>
      <property name="order" value="2"/>
    </listElement>
  </listView>
</table>
```
<a name="tle2"/>
##### \<listView\>, \<listElement\>
`<listView>`可以配置对应的数据库的一个表，通过子元素'<listElement>' 可以进一步排列表中每项的展示顺序、中英文名称。'<listElement>'用来配置列表中的每一项的属性，'attrName'表示对应数据库的字段名,'zhLabelName'代表该字段展示的中文名，'enLabelName'代表该字段展示的英文名，'order'代表该字段显示的顺序，'key'代表该字段是否为主键。
```xml
<listElement>
  <property name="attrName" value="asset_id"/>
  <property name="labelName" value="asset.id"/>
  <property name="zhLabelName" value="资产ID"/>
  <property name="enLabelName" value="ID"/>
  <property name="order" value="1"/>
  <property name="key" value="true"/>
</listElement>
```

<a name="tle3"/>
##### \<editView\>, \<editElement\>
该元素用来配置编辑列表中的每一项的属性，'attrName'表示对应数据库的字段名,'order'代表该字段显示的顺序，'editType'代表编辑框类型，'placeholder'代表编辑框提示信息。
```xml
<editView>
  <editElement>
    <property name="attrName" value="username"/>
    <property name="labelName" value="用户名"/>
    <property name="order" value="1"/>
    <property name="editType" value="input"/>
    <property name="placeholder" value="类别名"/>
  </editElement>
  <editElement>
    <property name="attrName" value="password"/>
    <property name="labelName" value="密码"/>
    <property name="order" value="2"/>
    <property name="editType" value="input"/>
    <property name="placeholder" value="密码"/>
  </editElement>
</editView>
```

<a name="tle4"/>
##### \<searchView\>, \<searchElement\>
该元素用来配置编辑列表中的每一项的属性，'attrName'表示对应数据库的字段名,'order'代表该字段显示的顺序，'editType'代表编辑框类型，'placeholder'代表编辑框提示信息。
```xml
<searchView>
  <searchElement>
    <property name="attrName" value="username"/>
    <property name="labelName" value="用户名"/>
    <property name="order" value="1"/>
    <property name="placeholder" value="用户名"/>
  </searchElement>
  <searchElement>
    <property name="attrName" value="password"/>
    <property name="labelName" value="密码"/>
    <property name="order" value="2"/>
    <property name="placeholder" value="密码"/>
  </searchElement>
</searchView>
```

<a name="tle5"/>
##### \<detailView\>, \<detailElement\>
该元素用来配置详细信息表中的每一项的属性，'attrName'表示对应数据库的字段名,'order'代表该字段显示的顺序，'tableName'代表对应的数据库表名，'isForeignKey'代表该字段是否有外键约束。
```xml
<detailView>
  <detailElement>
    <property name="attrName" value="username"/>
    <property name="labelName" value="姓名"/>
    <property name="order" value="1"/>
    <property name="tableName" value="user"/>
    <property name="isForeignKey" value="false"/>
  </detailElement>
  <detailElement>
    <property name="attrName" value="age"/>
    <property name="labelName" value="年龄"/>
    <property name="order" value="2"/>
    <property name="tableName" value="user"/>
    <property name="isForeignKey" value="false"/>
  </detailElement>
  <detailElement>
    <property name="attrName" value="sex"/>
    <property name="labelName" value="性别"/>
    <property name="order" value="2"/>
    <property name="tableName" value="sex"/>
    <property name="isForeignKey" value="true"/>
  </detailElement>
</detailView>
```

<a name="tle6"/>
##### \<ref-list\>
该元素用在关联表当中，每个子元素代表关联表的信息。
```xml
<table tableName="stock_in_info_list" domainObjectName="StockInInfoList" enableCountByExample="true" enableUpdateByExample="true" enableDeleteByExample="true" enableSelectByExample="true" selectByExampleQueryId="true">
  <ref-list>
    <ref name="StockInList">
      <property name="foreignKey" value="stock_in_info_stock_in_id"/>
    </ref>
    <ref name="AssetList">
      <property name="foreignKey" value="stock_in_info_asset_id"/>
    </ref>
  </ref-list>
</table>
```