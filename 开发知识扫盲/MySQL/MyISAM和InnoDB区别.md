### MyISAM 和 InnoDB 区别

#### 事务支持

myISAM 不支持事务，InnoDB有一整套完整的事务体系。

#### 索引

MyISAM和InnoDB都是使用B+树作为索引的。

不同的点在于：

- MyISAM的索引和数据文件分离。
- InnoDB 索引就是数据。

#### 锁

MyISAM只有表级别的锁，InnoDB支持行级锁。

我的思考：

因为MyISAM没有事务，所以没有对行进行上锁的必要。