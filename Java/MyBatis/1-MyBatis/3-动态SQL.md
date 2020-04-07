# 动态 SQL

动态 SQL 是 MyBatis 的强大特性之一，如果你在代码中使用过原生的SQL，那么肯定感受过处理SQL拼接中空格，逗号等痛苦。动态SQL可以帮你不需要关注这些细枝末节

由于MyBatis3精简了元素的种类，现在需要学习的很少，主要是有下面的几类

- if
- choose (when, otherwise)
- trim (where, set)
- foreach

## if

```xml
<select id="query" resultType="com.entity.Student">
    select id,name,age from student
    <where>
        <if test="name!=null">
            AND name like '%#{name}%'
        </if>
        <if test="age>0">
            AND age=#{age}
        </if>
    </where>
</select>
```

## choose (when, otherwise)

```xml
<select id="pick" resultType="com.entity.Student">
    select id,name,age from student
    <choose>
        <when test="name!=null">
            AND name like '%#{name}%'
        </when>
        <when test="age>0">
            AND age=#{age}
        </when>
        <otherwise>
            AND age>20
        </otherwise>
    </choose>
</select>
```



## trim (where, set)

### Where

```xml
<select id="findActiveBlogLike"
     resultType="Blog">
  SELECT * FROM BLOG
  <where>
    <if test="state != null">
         state = #{state}
    </if>
    <if test="title != null">
        AND title like #{title}
    </if>
    <if test="author != null and author.name != null">
        AND author_name like #{author.name}
    </if>
  </where>
</select>
```

### trim

```xml
<trim prefix="WHERE" prefixOverrides="AND |OR ">
  ...
</trim>
```

### set

```xml
 <update id="update" parameterType="com.entity.Student">
     update student
     <set>
         <if test="name!=null">name=#{name},</if>
         <if test="age>0">age=#{age}</if>
     </set>
     where id=#{id}
 </update>
```

## foreach

foreach用来方便的描述，select * from student where id in (2,3,4);

```xml
<select id="selectPostIn" resultType="domain.blog.Post">
  SELECT *
  FROM POST P
  WHERE ID in
  <foreach item="item" index="index" collection="list"
      open="(" separator="," close=")">
        #{item}
  </foreach>
</select>
```

## script

要在带注解的映射器接口类中使用动态 SQL，可以使用 *script* 元素。比如:

```xml
@Update({"<script>",
      "update Author",
      "  <set>",
      "    <if test='username != null'>username=#{username},</if>",
      "    <if test='password != null'>password=#{password},</if>",
      "    <if test='email != null'>email=#{email},</if>",
      "    <if test='bio != null'>bio=#{bio}</if>",
      "  </set>",
      "where id=#{id}",
      "</script>"})
    void updateAuthorValues(Author author);
```

但是这里使用的很不方便，建议还是在XML文件中使用比较好

## bind

`bind` 元素允许你在 OGNL（对象图导航语言） 表达式以外创建一个变量，并将其绑定到当前的上下文。比如：

```xml
<select id="selectBlogsLike" resultType="Blog">
  <bind name="pattern" value="'%' + _parameter.getTitle() + '%'" />
  SELECT * FROM BLOG
  WHERE title LIKE #{pattern}
</select>
```

## 多数据库支持

如果配置了 databaseIdProvider，你就可以在动态代码中使用名为 “_databaseId” 的变量来为不同的数据库构建特定的语句。比如下面的例子：

```xml
<!--   位于environments之后 -->
<databaseIdProvider type="DB_VENDOR">
    <property name="MySQL" value="mysql"/>
    <property name="Oracle" value="oracle" />
</databaseIdProvider>
```

```xml
<insert id="insert">
  <selectKey keyProperty="id" resultType="int" order="BEFORE">
    <if test="_databaseId == 'oracle'">
      select seq_users.nextval from dual
    </if>
    <if test="_databaseId == 'db2'">
      select nextval for seq_users from sysibm.sysdummy1"
    </if>
  </selectKey>
  insert into users values (#{id}, #{name})
</insert>
```

多数据库使用起来还是比较的混乱的，不建议使用

### 动态 SQL 中的插入脚本语言

MyBatis 从 3.2 版本开始支持插入脚本语言，这允许你插入一种语言驱动，并基于这种语言来编写动态 SQL 查询语句。详情可以查看[MyBatis](https://mybatis.org/mybatis-3/zh/dynamic-sql.html)