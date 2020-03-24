# IDEA+EasyCode实现代码生成
## Easy Code介绍
 EasyCode是基于IntelliJ IDEA开发的代码生成插件，==支持自定义任意模板==（Java，html，js，xml）。只要是与数据库相关的代码都可以通过自定义模板来生成。支持数据库类型与java类型映射关系配置。支持同时生成生成多张表的代码。每张表有独立的配置信息。完全的个性化定义，规则由你设置。
 ## 搭建步骤
 ### 第一步：打开IntelliJ IDEA 新建一个maven工程，不勾选骨架
 ![新建maven工程](https://img-blog.csdnimg.cn/20200324103557399.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pva2VyZGoyMzM=,size_16,color_FFFFFF,t_70)
 ### 配置项目的groupid、artifactid、version（自定义）
 点击下一步Next![配置项目的groupid、artifactid、version](https://img-blog.csdnimg.cn/20200324103802482.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pva2VyZGoyMzM=,size_16,color_FFFFFF,t_70)
 ### 选择工程存放目录
 ![选择工程存放目录](https://img-blog.csdnimg.cn/20200324103939561.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pva2VyZGoyMzM=,size_16,color_FFFFFF,t_70)
 ### 第二步：下载安装EasyCode插件
 file->settings->plugins 搜索Easy Code
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200324104320389.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pva2VyZGoyMzM=,size_16,color_FFFFFF,t_70)
 搜索到后点击Install 我这里安装过了 安装完成会让你重启IDEA。
 如何判断是否安装成功 file->settings->Other settings 看是否有Easy Code这个选项
 ![判断是否安装成功](https://img-blog.csdnimg.cn/20200324104621741.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pva2VyZGoyMzM=,size_16,color_FFFFFF,t_70)
 ### 第三步：引入Easy Code模板 （可以根据个人情况定制 也可以使用默认的）
 file->settings->Other settings->Template Setting![在这里插入图片描述](https://img-blog.csdnimg.cn/20200324104929328.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pva2VyZGoyMzM=,size_16,color_FFFFFF,t_70)
 ### 第四步：创建数据库，数据表
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200324105918742.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pva2VyZGoyMzM=,size_16,color_FFFFFF,t_70)
 ### 第五步：配置数据源（需要指定数据库名称，要生成数据表）
 点击IDEA右侧的Datbase->点击上方的加号->选择Data Source.->Mysql![在这里插入图片描述](https://img-blog.csdnimg.cn/20200324105230858.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pva2VyZGoyMzM=,size_16,color_FFFFFF,t_70)
 ### 配置数据源
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200324110207237.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pva2VyZGoyMzM=,size_16,color_FFFFFF,t_70)
 注意：连接方式需要采用mysql8的连接方式，不然可能连接失败
`jdbc:mysql://localhost:3306/table?useUnicode=true&characterEncoding=utf-8&serverTimezone=UTC&useSSL=false`
### 连接成功如图所示
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200324110500652.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pva2VyZGoyMzM=,size_16,color_FFFFFF,t_70)
### 创建要相关的包，存放生成后的数据（以springboot项目为例）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200324110901826.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pva2VyZGoyMzM=,size_16,color_FFFFFF,t_70)
### 引入springboot的相关pom.xml依赖

```javascript
<dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>1.3.2</version>
        </dependency>
         <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.38</version>
        </dependency>
    </dependencies>

```
需要用到mybatis的启动器，所以也一起引用

### 打开Easy Code插件 选要生成的pojo,mapper,service
右击表名->Easy Code->Generate Code
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200324111400718.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pva2VyZGoyMzM=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200324111534108.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pva2VyZGoyMzM=,size_16,color_FFFFFF,t_70)
Module：当前项目模块
package:生成代码存放包的位置
Template:生成的模板
#### 勾选All表示生成所有，勾选禁止提示，防止弹出很多个提示信息，点击OK
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020032411184833.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pva2VyZGoyMzM=,size_16,color_FFFFFF,t_70)

pojo*（entity）：Brand.java代码：

```java
package com.dj.entity;

import java.io.Serializable;

/**
 * (Brand)实体类
 *
 * @author joker_dj
 * @since 2020-03-24 11:18:22
 */
public class Brand implements Serializable {
    private static final long serialVersionUID = 689051521458334271L;
    /**
    * ID
    */
    private Integer bid;
    /**
    * 品牌名称
    */
    private String bname;
    /**
    * 日期
    */
    private String ctime;

    
    public Integer getBid() {
        return bid;
    }

    public void setBid(Integer bid) {
        this.bid = bid;
    }
    
    public String getBname() {
        return bname;
    }

    public void setBname(String bname) {
        this.bname = bname;
    }
    
    public String getCtime() {
        return ctime;
    }

    public void setCtime(String ctime) {
        this.ctime = ctime;
    }

    @Override
    public String toString() {
        return "Brand{" +
                "bid=" + bid +
                "bname=" + bname +
                "ctime=" + ctime +
                 '}';      
    }
}
```
service接口:BrandService.java 代码如下：

```java
package com.dj.service;

import com.dj.entity.Brand;
import java.util.List;

/**
 * @InterfaceName BrandService
 * @Description (Brand)表服务接口
 * @author joker_dj
 * @date 2020-03-24 11:18:22
 * @Version 1.0
 **/
public interface BrandService {

    /**
     * @Description 添加Brand
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * @param brand 实例对象
     * @return 是否成功
     */
    boolean insert(Brand brand);

    /**
     * @Description 删除Brand
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * @param bid 主键
     * @return 是否成功
     */
    boolean deleteById(Integer bid);

    /**
     * @Description 查询单条数据
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * @param bid 主键
     * @return 实例对象
     */
    Brand queryById(Integer bid);

    /**
     * @Description 查询全部数据
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * 分页使用MyBatis的插件实现
     * @return 对象列表
     */
    List<Brand> queryAll();

    /**
     * @Description 实体作为筛选条件查询数据
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * @param brand 实例对象
     * @return 对象列表
     */
    List<Brand> queryAll(Brand brand);

    /**
     * @Description 修改数据，哪个属性不为空就修改哪个属性
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * @param brand 实例对象
     * @return 是否成功
     */
    boolean update(Brand brand);

}
```
serviceImpl 实现类:BrandServiceImpl.java代码如下：

```java
package com.dj.service.impl;

import com.dj.entity.Brand;
import com.dj.dao.BrandDao;
import com.dj.service.BrandService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import javax.annotation.Resource;
import java.util.List;

 /**
 * @ClassName BrandServiceImpl
 * @Description (Brand)表服务实现类
 * @author joker_dj
 * @date 2020-03-24 11:18:22
 * @Version 1.0
 **/
@Service("brandService")
public class BrandServiceImpl  implements BrandService {

    @Autowired
    protected BrandDao brandDao;

    /**
     * @Description 添加Brand
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * @param brand 实例对象
     * @return 是否成功
     */
    @Override
    public boolean insert(Brand brand) {
        if(brandDao.insert(brand) == 1){
            return true;
        }
        return false;
    }

    /**
     * @Description 删除Brand
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * @param bid 主键
     * @return 是否成功
     */
    @Override
    public boolean deleteById(Integer bid) {
        if(brandDao.deleteById(bid) == 1){
            return true;
        }
        return false;
    }

    /**
     * @Description 查询单条数据
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * @param bid 主键
     * @return 实例对象
     */
    @Override
    public Brand queryById(Integer bid) {
        return brandDao.queryById(bid);
    }

    /**
     * @Description 查询全部数据
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * 分页使用MyBatis的插件实现
     * @return 对象列表
     */
    @Override
    public List<Brand> queryAll() {
        return brandDao.queryAll();
    }

    /**
     * @Description 实体作为筛选条件查询数据
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * @param brand 实例对象
     * @return 对象列表
     */
    @Override
    public List<Brand> queryAll(Brand brand) {
        return brandDao.queryAll(brand);
    }

    /**
     * @Description 修改数据，哪个属性不为空就修改哪个属性
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * @param brand 实例对象
     * @return 是否成功
     */
    @Override
    public boolean update(Brand brand) {
        if(brandDao.update(brand) == 1){
            return true;
        }
        return false;
    }

}
```
dao层：BrandDao.java代码如下

```java
package com.dj.dao;

import com.dj.entity.Brand;
import org.apache.ibatis.annotations.Mapper;
import org.apache.ibatis.annotations.Param;
import java.util.List;

 /**
 * @InterfaceName BrandDao
 * @Description (Brand)表数据库访问层
 * @author joker_dj
 * @date 2020-03-24 11:18:22
 * @Version 1.0
 **/
@Mapper
public interface BrandDao {

    /**
     * @Description 添加Brand
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * @param brand 实例对象
     * @return 影响行数
     */
    int insert(Brand brand);
    
    /**
     * @Description 删除Brand
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * @param bid 主键
     * @return 影响行数
     */
    int deleteById(Integer bid);

    /**
     * @Description 查询单条数据
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * @param bid 主键
     * @return 实例对象
     */
    Brand queryById(Integer bid);

    /**
     * @Description 查询全部数据
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * 分页使用MyBatis的插件实现
     * @return 对象列表
     */
    List<Brand> queryAll();

    /**
     * @Description 实体作为筛选条件查询数据
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * @param brand 实例对象
     * @return 对象列表
     */
    List<Brand> queryAll(Brand brand);

    /**
     * @Description 修改Brand
     * @author joker_dj
     * @date 2020-03-24 11:18:22
     * @param 根据brand的主键修改数据
     * @return 影响行数
     */
    int update(Brand brand);

}
```
mapper.xml代码如下：

```javascript
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.dj.dao.BrandDao">

    <!--brand的映射结果集-->
    <resultMap type="com.dj.entity.Brand" id="BrandMap">
        <result property="bid" column="bid" jdbcType="INTEGER"/>
        <result property="bname" column="bname" jdbcType="VARCHAR"/>
        <result property="ctime" column="ctime" jdbcType="VARCHAR"/>
    </resultMap>
    
    <!--全部字段-->
    <sql id="allColumn"> bid, bname, ctime </sql>
    
    <!--添加语句的字段列表-->
    <sql id="insertColumn">
        <if test="bname != null and bname != ''">
                bname,
        </if>
        <if test="ctime != null and ctime != ''">
                ctime,
        </if>
    </sql>
    
    <!--添加语句的值列表-->
        <sql id="insertValue">
        <if test="bname != null and bname != ''">
                #{bname},
        </if>
        <if test="ctime != null and ctime != ''">
                #{ctime},
        </if>
    </sql>
    
    <!--通用对Brand各个属性的值的非空判断-->
    <sql id="commonsValue">
        <if test="bname != null and bname != ''">
                bname = #{bname},
        </if>
        <if test="ctime != null and ctime != ''">
                ctime = #{ctime},
        </if>
    </sql>
    
    <!--新增brand:哪个字段不为空就添加哪列数据,返回自增主键-->
    <insert id="insert" keyProperty="bid" useGeneratedKeys="true">
        insert into brand
        <trim prefix="(" suffix=")" suffixOverrides=",">
            <include refid="insertColumn"/>
        </trim>
        <trim prefix="values (" suffix=")" suffixOverrides=",">
            <include refid="insertValue"/>
        </trim>
    </insert>
   
    <!--删除brand:通过主键-->
    <delete id="deleteById">
        delete from brand
        <where>
            bid = #{bid}
        </where>
    </delete>
    
    <!--查询单个brand-->
    <select id="queryById" resultMap="BrandMap">
        select
        <include refid="allColumn"></include>
        from brand
        <where>
            bid = #{bid}
        </where>
    </select>

    <!--查询所有brand-->
    <select id="queryAllByLimit" resultMap="BrandMap">
        select
        <include refid="allColumn"></include>
        from brand
    </select>

    <!--通过实体作为筛选条件查询-->
    <select id="queryAll" resultMap="BrandMap">
        select
          <include refid="allColumn"></include>
        from brand
        <trim prefix="where" prefixOverrides="and" suffixOverrides=",">
            <include refid="commonsValue"></include>
        </trim>
    </select>

    <!--通过主键修改数据-->
    <update id="update">
        update brand
        <set>
            <include refid="commonsValue"></include>
        </set>
        <where>
            bid = #{bid}
        </where>
    </update>

</mapper>
```

### 第六步：运行并调用
##### 注意：我的mapper.xml文件存放的位置是在resources目录下，不会被扫描到，所以在pom.xml文件中配置一下，使mapper.xml能够被扫描

```java
<!--静态资源放行-->
  <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>

        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.xml</include>
                </includes>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*</include>
                </includes>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.xml</include>
                </includes>
            </resource>
        </resources>
    </build>
```

完整的pom.xml文件如下：

```java
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.2.4.RELEASE</version>
    </parent>
    <groupId>com.easycode</groupId>
    <artifactId>easycode</artifactId>
    <version>1.0-SNAPSHOT</version>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>1.3.2</version>
        </dependency>

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.38</version>
        </dependency>
    </dependencies>


    <!--静态资源放行-->
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>

        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.xml</include>
                </includes>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*</include>
                </includes>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.xml</include>
                </includes>
            </resource>
        </resources>
    </build>
</project>
```

#### 在resources目录下创建springboot全局配置文件Application.properties
配置文件如下：

```javascript
##配置数据驱动信息  （key固定）
spring.datasource.driverClassName = com.mysql.jdbc.Driver
spring.datasource.url = jdbc:mysql:///brand
spring.datasource.username = root
spring.datasource.password =

#tomcat端口号
server.port=8081

##给mybatis的实体类取别名  typeAliasesPackage
mybatis.type-aliases-package=com.dj.entity
## mybatis ：mapper存放位置
mybatis.mapper-locations:classpath*:mybatis/mapper/*.xml
```

### 创建controller调用方法实现业务
controller:

```java
package com.dj.controller;

import com.dj.entity.Brand;
import com.dj.service.BrandService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@RestController
public class webController {
    @Autowired
    BrandService service;

    @RequestMapping("/showAll")
    public List<Brand> show(){
        List<Brand> brands = service.queryAll();
        System.out.println(brands);
        return brands;
    }
}

```
### 运行查看结果
浏览器输入 localhost:8081/showAll
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200324113746690.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pva2VyZGoyMzM=,size_16,color_FFFFFF,t_70)

### 教程结束，此教程根据上面一步一步来应该是没有问题的，如果有疑难解决不了，欢迎评论区留言
