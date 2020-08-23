MyBatis框架学习笔记

是一款优秀的ORM（Object/Relation Mapping）对象关系映射 半自动轻量级持久层框架。

大量使用设计模式

​    1  Builder模式   SqlSessionFactoryBuilder

 含义 ：使用多个简单的对象构建成一个复杂的对象。

```java
InputStream resourceAsStream = Resources.getResourceAsStream("sqlMapConfig.xml");
SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(resourceAsStream);
```

 2   工厂模式  SqlSessionFactory

​    含义：根据参数的不同 返回不同类的实例。

```java
SqlSession sqlSession = sqlSessionFactory.openSession();
// 设置自动提交
SqlSession sqlSession = sqlSessionFactory.openSession(boolean autoCommit);
```

3  代理模式

动态代理模式  

  一般采用接口的形式定义Mapper  其底层使用的就是Jdk的动态代理技术



```java
IUserDao mapper = sqlSession.getMapper(IUserDao.class);

// 会调用 MapperProxy 类中的方法
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        try {
            // 如果是 Object 定义的方法，直接调用
            if (Object.class.equals(method.getDeclaringClass())) {
                return method.invoke(this, args);

            } else if (isDefaultMethod(method)) {
                return invokeDefaultMethod(proxy, method, args);
            }
        } catch (Throwable t) {
            throw ExceptionUtil.unwrapThrowable(t);
        }
        // 获得 MapperMethod 对象
        final MapperMethod mapperMethod = cachedMapperMethod(method);
        // 重点在这：MapperMethod最终调用了执行的方法
        return mapperMethod.execute(sqlSession, args);
    }
```









