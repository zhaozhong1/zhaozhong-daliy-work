# MyBatis 扫盲

## MyBatis 的优缺点

## MyBatis执行一个sql的流程？*

1. 创建SqlSessionFactory会话工厂
2. 通过SqlSessionFactory创建SqlSession
3. 通过SqlSession执行数据库操作
4. 调用session.commit()提交事务
5. 调用session.close()关闭会话

## MyBatis的二级缓存



## MyBatis中 #{}和${}的区别？

#{}是采用占位符的方式对参数进行填入。

${}是采用拼接的方式对参数进行填入。因此有sql注入的风险。

## MyBatis是什么框架？

MyBatis是半ORM框架。

### 什么叫ORM框架：

