# API

MyBatis的API的使用就是MyBatis使用的一些类，在JAVA项目代码中，程序员可以使用这些API实现自定义功能

## SqlSession

SqlSession由SqlSessionFactory创建， SqlSessionFactory由SqlSessionFactoryBuilde创建。创建SqlSessionFactory有五种方法

```java
SqlSessionFactory build(InputStream inputStream)
SqlSessionFactory build(InputStream inputStream, String environment)
SqlSessionFactory build(InputStream inputStream, Properties properties)
SqlSessionFactory build(InputStream inputStream, String env, Properties props)
SqlSessionFactory build(Configuration config)
```

## SqlSessionFactory

获取一个session的方法有更多，获取一个session通常要考虑，事务处理，数据库连接，语句执行等

```
SqlSession openSession()
SqlSession openSession(boolean autoCommit)
SqlSession openSession(Connection connection)
SqlSession openSession(TransactionIsolationLevel level)
SqlSession openSession(ExecutorType execType, TransactionIsolationLevel level)
SqlSession openSession(ExecutorType execType)
SqlSession openSession(ExecutorType execType, boolean autoCommit)
SqlSession openSession(ExecutorType execType, Connection connection)
Configuration getConfiguration();
```

无参数的session的默认值如下

- 事务作用域将会开启（也就是不自动提交）。

- 将由当前环境配置的 DataSource 实例中获取 Connection 对象。

- 事务隔离级别将会使用驱动或数据源的默认设置。

- 预处理语句不会被复用，也不会批量处理更新。

ExecutorType的类型，描述的是session的预处理语句的生成方式
- `ExecutorType.SIMPLE`：该类型的执行器没有特别的行为。它为每个语句的执行创建一个新的预处理语句。
- `ExecutorType.REUSE`：该类型的执行器会复用预处理语句。
- `ExecutorType.BATCH`：该类型的执行器会批量执行所有更新语句，如果 SELECT 在多个更新中间执行，将在必要时将多条更新语句分隔开来，以方便理解。



生成Java代码
不生成XML-MyBatis3注释仅用于
生成的模型对象是“平面的”-没有单独的主键对象
生成的代码依赖于MyBatis动态SQL库
生成的代码量相对较小
生成的代码在查询构造方面具有极大的灵活性