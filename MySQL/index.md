## @Transactional注解详解

### @Transactional注解可以作用于接口、接口方法、类以及类方法上
1. 当作用于类上时，该类的所有 public 方法将都具有该类型的事务属性
2. 当作用在方法级别时会覆盖类级别的定义
3. 当作用在接口和接口方法时则只有在使用基于接口的代理时它才会生效，也就是JDK动态代理，而不是Cglib代理
4. 当在 protected、private 或者默认可见性的方法上使用 @Transactional 注解时是不会生效的，也不会抛出任何异常
5. 默认情况下，只有来自外部的方法调用才会被AOP代理捕获，也就是，类内部方法调用本类内部的其他方法并不会引起事务行为，即使被调用方法使用@Transactional注解进行修饰

### @Transactional注解的可用参数
readOnly
该属性用于设置当前事务是否为只读事务，设置为true表示只读，false则表示可读写，默认值为false

rollbackFor
该属性用于设置需要进行回滚的异常类数组，当方法中抛出指定异常数组中的异常时，则进行事务回滚。例如：
1. 指定单一异常类：@Transactional(rollbackFor=RuntimeException.class)
2. 指定多个异常类：@Transactional(rollbackFor={RuntimeException.class, BusnessException.class})

rollbackForClassName
该属性用于设置需要进行回滚的异常类名称数组，当方法中抛出指定异常名称数组中的异常时，则进行事务回滚。例如：
1. 指定单一异常类名称：@Transactional(rollbackForClassName=“RuntimeException”)
2. 指定多个异常类名称：@Transactional(rollbackForClassName={“RuntimeException”,“BusnessException”})

noRollbackFor
该属性用于设置不需要进行回滚的异常类数组，当方法中抛出指定异常数组中的异常时，不进行事务回滚

noRollbackForClassName
参照上方的例子

timeout
该属性用于设置事务的超时秒数，默认值为-1表示永不超时

propagation
该属性用于设置事务的传播行为
例如：@Transactional(propagation=Propagation.NOT_SUPPORTED)

事物传播行为介绍:

@Transactional(propagation=Propagation.REQUIRED) 如果有事务, 那么加入事务, 没有的话新建一个(默认)
@Transactional(propagation=Propagation.NOT_SUPPORTED) 容器不为这个方法开启事务
@Transactional(propagation=Propagation.REQUIRES_NEW) 不管是否存在事务,都创建一个新的事务,原来的挂起,新的执行完毕,继续执行老的事务
@Transactional(propagation=Propagation.MANDATORY) 必须在一个已有的事务中执行,否则抛出异常
@Transactional(propagation=Propagation.NEVER) 必须在一个没有的事务中执行,否则抛出异常(与Propagation.MANDATORY相反)
@Transactional(propagation=Propagation.SUPPORTS) 如果其他bean调用这个方法,在其他bean中声明事务,那就用事务.如果其他bean没有声明事务,那就不用事务
isolation
该属性用于设置底层数据库的事务隔离级别

事务隔离级别介绍:

@Transactional(isolation = Isolation.READ_UNCOMMITTED)读取未提交数据(会出现脏读, 不可重复读) 基本不使用
@Transactional(isolation = Isolation.READ_COMMITTED)读取已提交数据(会出现不可重复读和幻读)
@Transactional(isolation = Isolation.REPEATABLE_READ)可重复读(会出现幻读)
@Transactional(isolation = Isolation.SERIALIZABLE)串行化
什么是脏读、幻读、不可重复读？

脏读 : 一个事务读取到另一事务未提交的更新数据
不可重复读 : 在同一事务中, 多次读取同一数据返回的结果有所不同, 换句话说, 后续读取可以读到另一事务已提交的更新数据. 相反, "可重复读"在同一事务中多次读取数据时, 能够保证所读数据一样, 也就是后续读取不能读到另一事务已提交的更新数据
幻读 : 一个事务读到另一个事务已提交的insert数据
其中MySQL默认使用的隔离级别为REPEATABLE_READ、Oracle的为READ_COMMITTED
