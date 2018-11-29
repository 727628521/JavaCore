<h3 style="padding-bottom:6px; padding-left:20px; color:#ffffff; background-color:#E74C3C;">TCC事务补偿机制（柔性事务方案）</h3>

**TCC** 是 *Try Confirm-Cancel* 的缩写，其本质上还是2PC（两阶段提交协议）。它不像具有[ACID特性](https://github.com/about-cloud/JavaCore)的数据库事务那样刚性 ，TCC又没有XA事务那样直接依赖于资源管理器（RM），它是基于业务层面的事务操作，所以（占有资源的）粒子度是可控的，所以又称为**柔性事务方案**。TCC分为两阶段：**Try阶段** 和 **Confirm/Cancel阶段**。

![TCC]()

#### 第一阶段：Try阶段：





#### 第二阶段：Confirm/Cancel阶段：