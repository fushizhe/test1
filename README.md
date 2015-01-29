
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

#### [Java模板文件配置](#jtp)
1.  [\<packageName\>](#jtp1)
2.  [\<componentName\>](#jtp2)
3.  [\<basePath\>](#jtp3)
4.  [\<uentity\>](#jtp4)
5.  [\<lentity\>](#jtp5)
6.  [\<refVariables\>](#jtp6)
7.  [\<refParameters\>](#jtp7)
8.  [数据库相关](#jtp8)

#### [页面模板文件](#ptp)
1.  [\<colNames\>](#ptp1)
2.  [\<colModel\>](#ptp2)
3.  [\<sortname\>](#ptp3)
4.  [\<searchParameterLines\>](#ptp4)
5.  [\<searchParameters\>](#ptp5)

#### [示例](#ex)


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
##### \<javaModelGenerator\>
该元素可以用于指定生成模型的包名和位置：
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
`<listView>`可以配置对应的数据库的一个表，通过子元素`<listElement>` 可以进一步排列表中每项的展示顺序、中英文名称。`<listElement>`用来配置列表中的每一项的属性，`attrName`表示对应数据库的字段名,`zhLabelName`代表该字段展示的中文名，`enLabelName`代表该字段展示的英文名，`order`代表该字段显示的顺序，`key`代表该字段是否为主键。
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
该元素用来配置编辑列表中的每一项的属性，`attrName`表示对应数据库的字段名,`order`代表该字段显示的顺序，`editType`代表编辑框类型，`placeholder`代表编辑框提示信息。
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
该元素用来配置编辑列表中的每一项的属性，`attrName`表示对应数据库的字段名,`order`代表该字段显示的顺序，`editType`代表编辑框类型，`placeholder`代表编辑框提示信息。
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
该元素用来配置详细信息表中的每一项的属性，`attrName`表示对应数据库的字段名,`rder`代表该字段显示的顺序，`tableName`代表对应的数据库表名，`isForeignKey`代表该字段是否有外键约束。
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

<a name="jtp"/>
<a name="jtp1"/>
#### Java模板文件配置
##### \<packageName\>
该标签用于表示项目基本的信息
```java
package ${packageName}.${componentName}.controller;

import ${packageName}.${componentName}.model.${uentity};
import ${packageName}.${componentName}.service.${uentity}Service;
import ${packageName}.common.util.DataEditResponse;
import ${packageName}.common.util.DataRequest;
import ${packageName}.common.util.DataSearchResponse;
import ${packageName}.common.util.UtilMethod;
```

<a name="jtp2"/>
##### \<componentName\>
该标签用于表示模块名
```java
package ${packageName}.${componentName}.controller;

import ${packageName}.${componentName}.model.${uentity};
import ${packageName}.${componentName}.service.${uentity}Service;
import ${packageName}.common.util.DataEditResponse;
import ${packageName}.common.util.DataRequest;
import ${packageName}.common.util.DataSearchResponse;
import ${packageName}.common.util.UtilMethod;
```

<a name="jtp3"/>
##### \<basePath\>
该标签用于表示项目的根路径：
```xml
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
  <property name="dataSource" ref="mySqlDataSource" />
  <property name="typeAliasesPackage" value="${packageName}.*.model" />
  <!-- <property name="configLocation" value="classpath:mybatis-config.xml" /> -->
  <!-- 显式指定Mapper文件位置 -->
  <property name="mapperLocations" value="classpath:${basePath}/*/mapper/*.xml" />
</bean>
```
<a name="jtp4"/>
##### \<uentity\>
该标签用于表示开头大写的实体名，如User。

<a name="jtp5"/>
##### \<lentity\>
该标签用于表示开头大写的实体名，如User。

<a name="jtp6"/>
##### \<refVariables\>
该标签用于生成所关联的表的Mapper对象的声明以及相应的getter，setter代码：
```java
@Resource(name="${uentity}Mapper")
public void set${uentity}Mapper(${uentity}Mapper ${lentity}Mapper) {
    this.${lentity}Mapper = ${lentity}Mapper;
}

${refVariables}
```

<a name="jtp7"/>
##### \<refParameters\>
该标签用于生成在方法中的参数中用到的关联表的对象，比如User user, ClassList classList这种会放在方法参数中的代码：
```java
public interface ${uentity}Service {

    /*
   * 添加一条记录
   * @param stockInInfoList
   * @return int
   */
    public int add(${uentity} ${lentity}${refParameters});

    /**
     * 删除一条关联数据
     * @param stockInInfoId
     * @return
     */
    public int delete(int id);

    /**
     * 更新一条关联数据和入库数据
     * @param stockInList
     * @param stockInInfoList
     * @param assetList
     * @return
     */
    public int update(${uentity} ${lentity}${refParameters});
}
```

<a name="jtp8"/>
##### 数据库相关
数据库相关信息，用在jdbc.properties
```java
jdbc.url=${jdbcUrl}
jdbc.driverClassName=${driverClassName}
jdbc.username=${username}
jdbc.password=${password}
```
mybatis-config.xml中有一个配置，生成类型别名映射：
使用了basicInfo这是一个列表，里面每一个Item对应一个实体，分别显示实例名和类名，就是lentity和uentity，如：
```java
<#list basicInfo as being>
  <typeAlias alias="${being.instanceName}" type="${packageName}.${componentName}.model.${being.className}" />
</#list>
```

假设用户选择了class_list这个表，对应的代码生成后是：
```xml
<typeAliases>
  <typeAlias alias="classList" type="com.canco.classification.model.ClassList" />
</typeAliases>
```


<a name="ptp"/>
##### 页面模板文件
<a name="ptp1"/>
###### \<colNames\>
该标签表示列表的表头，如'ID', '资产名','状态名','创建人','创建日期'

<a name="ptp3"/>
###### \<sortname\>
该标签表示排序的键，如id，该项为jqGrid要求。

<a name="ptp2"/>
###### \<colNames\>
该标签表示列表的内容，如`{name: 'className', index: 'className', width: 200, sortable: true, align:"left", editable:true}`，每一行代表一个列项
```Javascript
$("#tableList").jqGrid({
          //@CodeGen begin
          url: '${lentity}SelectM',
          editurl: '${lentity}Edit',
          colNames: [
      //'ID', '资产名','状态名','创建人','创建日期'
      ${colNames}
    ],
          colModel: [
              //{name: 'classId', index: 'classId', width: 100, sortable: true, key:true, hidden:true},
              //{name: 'className', index: 'className', width: 200, sortable: true, align:"left", editable:true},
              //{name: 'defaultStatName', index: 'defaultStatName', width: 200, sortable: true, align:"left", editable:true},
              //{name: 'createMan', index: 'createMan', width: 200, sortable: true, align:"left", editable:true},
              //{name: 'createDate', index: 'createDate', width: 200, sortable: true, align:"left", editable:false}
      ${colModel}
          ],
          jsonReader : {
              page: "currentpage",
              total: "totalpage",
              records: "records",
              root: "rows",     //返回数据
              userdata: "userdata" //其他参数
          },
          caption: "数据列表", //表格名称
          sortname: '${sortname}',
          sortorder: "desc",
          //@CodeGen end
          pager: '#pager',
          rowNum: 10,
          rowList: [10, 20, 30, 50],
          viewrecords: true, //总记录数
          multiselect: true, //多选
          autowidth: true,
          hidegrid: false,
          mtype: 'POST',
          datatype: "json",
          height: '300px'
      });
```

<a name="ptp4"/>
###### \<searchParameterLines\>
该标签用于获取搜索控件里面内容的代码，js中用于搜索的代码。

<a name="ptp5"/>
###### \<searchParameters\>
和searchParameterLines搭配使用，使用searchParameterLines中获取的值，拼接url。使用上述两个配置项，js模板代码如下：
```Javascript
function gridReload(){
        ${searchParameterLines}
  $("#tableList").jqGrid('setGridParam',{url:"${lentity}SelectM?${searchParameters}, page:1}).trigger("reloadGrid");
}
```

假设用户配置的搜索字段为：className和defaultStatName，那么对应的生成的代码如下：
```Javascript
function gridReload(){
  var var0 = $("#search_className").val();
  var var1 = $("#search_defaultStatName").val();

  $("#tableList").jqGrid('setGridParam',{url:"classListSelectM?className="+var0+"&defaultStatName="+var1, page:1}).trigger("reloadGrid");
}
```

<a name="ex"/>
##### 示例
以下是一个具体的配置文件示例
```Javascript
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
  PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
  "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
<!-- 数据库驱动-->
  <!--<classPathEntry location="D:/mysql-connector-java-5.1.18-bin.jar"/>-->
  <classPathEntry location="D:/ojdbc14.jar"/>
  <!--数据库链接URL，用户名、密码 -->
  <jdbcConnection driverClass="com.mysql.jdbc.Driver" connectionURL="jdbc:mysql://192.168.1.135:3306/demotest" userId="canco" password="123">
  </jdbcConnection>
    <!--<jdbcConnection driverClass="com.sybase.jdbc3.jdbc.SybDriver"
      connectionURL="jdbc:sybase:Tds:192.168.1.132:2638" userId="canco" password="123" />-->
    <!--<jdbcConnection driverClass="oracle.jdbc.driver.OracleDriver"
      connectionURL="jdbc:oracle:thin:@192.168.1.132:1521:EAM" 
      userId="canco" password="123" />-->
    <!--工程基本路径和包名-->
  <projectProfile type="Maven" packageName="com.canco" projectName="D:/Projects/JavaEE/SSM" welcomeFile="/WEB-INF/pages/registration/login.jsp">
  </projectProfile>
  <context id="registration"  targetRuntime="MyBatis3" componentName="registration" innerComponent="registration">
    <commentGenerator>
      <property name="suppressDate" value="true"/>
      <!-- 是否去除自动生成的注释 true：是 ： false:否 -->
      <property name="suppressAllComments" value="true"/>
    </commentGenerator>
    <javaTypeResolver>
      <property name="forceBigDecimals" value="false"/>
    </javaTypeResolver>
    <!-- 生成模型的包名和位置-->
    <javaModelGenerator>
      <property name="trimStrings" value="true"/>
    </javaModelGenerator>
    <!-- 生成映射文件的包名和位置-->
    <sqlMapGenerator>
    </sqlMapGenerator>
    <!-- 生成DAO的包名和位置-->
    <javaClientGenerator type="XMLMAPPER">
    </javaClientGenerator>

    <table tableName="users" domainObjectName="User" enableCountByExample="true" enableUpdateByExample="true" enableDeleteByExample="true" enableSelectByExample="true" selectByExampleQueryId="true">
    </table>
  </context>
  <context id="DB2Tables" targetRuntime="MyBatis3" componentName="classification">
    <commentGenerator>
      <property name="suppressDate" value="true"/>
      <!-- 是否去除自动生成的注释 true：是 ： false:否 -->
      <property name="suppressAllComments" value="true"/>
    </commentGenerator>
    <javaTypeResolver>
      <property name="forceBigDecimals" value="false"/>
    </javaTypeResolver>
    <!-- 生成模型的包名和位置-->
    <javaModelGenerator>
      <property name="trimStrings" value="true"/>
    </javaModelGenerator>
    <!-- 生成映射文件的包名和位置-->
    <sqlMapGenerator>
    </sqlMapGenerator>
    <!-- 生成DAO的包名和位置-->
    <javaClientGenerator type="XMLMAPPER">
    </javaClientGenerator>

    <table tableName="class_list" domainObjectName="ClassList" enableCountByExample="true" enableUpdateByExample="true" enableDeleteByExample="true" enableSelectByExample="true" selectByExampleQueryId="true">
      <listView>
        <listElement>
          <property name="attrName" value="class_id"/>
          <property name="labelName" value="classList.id"/>
          <property name="zhLabelName" value="编号"/>
          <property name="enLabelName" value="ID"/>
          <property name="order" value="1"/>
          <property name="key" value="true"/>
        </listElement>
        <listElement>
          <property name="attrName" value="class_name"/>
          <property name="zhLabelName" value="名称"/>
          <property name="enLabelName" value="Class Name"/>
          <property name="labelName" value="classList.name"/>
          <property name="order" value="2"/>
        </listElement>
        <listElement>
          <property name="attrName" value="default_stat_name"/>
          <property name="zhLabelName" value="默认状态"/>
          <property name="enLabelName" value="Default State Name"/>
          <property name="labelName" value="classList.stateName"/>
          <property name="order" value="3"/>
        </listElement>
      </listView>
      <searchView>
        <searchElement>
          <property name="attrName" value="class_name"/>
          <property name="zhLabelName" value="名称"/>
          <property name="enLabelName" value="Class Name"/>
          <property name="labelName" value="classList.name"/>
          <property name="placeholder" value="classList.name.placeholder"/>
          <property name="zhPlaceholder" value="请输入名称"/>
          <property name="enPlaceholder" value="Input Class Name"/>
          <property name="order" value="2"/>
        </searchElement>
        <searchElement>
          <property name="attrName" value="default_stat_name"/>
          <property name="zhLabelName" value="默认状态"/>
          <property name="enLabelName" value="Default State Name"/>
          <property name="labelName" value="classList.stateName"/>
          <property name="placeholder" value="classList.stateName.placeholder"/>
          <property name="zhPlaceholder" value="请输入默认状态"/>
          <property name="enPlaceholder" value="Input Default State Name"/>
          <property name="order" value="3"/>
        </searchElement>
      </searchView>
      </table>
  </context>
</generatorConfiguration>
```
这个配置文件分成两个部分，一个是基本的信息，包括驱动包的位置，jdbc连接，工程基本信息。第二个部分可以有多个context，就是多个模块，context里面的两个属性，模块名是必须的，innerComponent可有可无。innerComponent指要是用内部的功能组件，比如登录注册这样一个，制定了之后，就会直接用，不会去做其他的事情。只需指明用哪个table作为用户表即可。例如上例中的context，是用的是class_list这样一个表，需要做增删改查所以需要有那些view。

使用方法就是给定配置路径，模板路径，新建一个空的j2ee工程，并以其配置到配置文件中，执行`Java -jar CodeGen.jar`即可。
