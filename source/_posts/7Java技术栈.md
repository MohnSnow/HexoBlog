---
title: Java技术栈
date: 2017-03-09 16:39:56
tags: Java 面试
categories: "面试"
toc: true
---
作为互联网行业的三大巨头，百度、阿里巴巴、腾讯对于互联网人才有很大的吸引力，他们的员工也是众多互联网同行觊觎的资深工程师、管理者人选。
下面我总结了进入这三家公司你所需掌握的技能：
<!--more-->
### 0 java基础：
#### 1.阿里基础：
扎实的计算机专业基础，包括算法和数据结构，操作系统，计算机网络，计算机体系结构，数据库等
具有扎实的Java编程基础，理解IO、多线程等基础框架
熟练使用Linux系统的常用命令及shell有一定了解
精通多线程编程，熟悉分布式,缓存,消息队列等机制；熟悉JVM，包括内存模型、类加载机制以及性能优化
精通spring mvc、orm框架（ibatis或hibernate）、模板引擎（velocity）、关系型数据库设计及SQL
具备良好的面向对象编程经验，深入理解OO、AOP思想，具有很强的分析设计能力，熟悉常用设计模式
有大型分布式、高并发、高负载、高可用性系统设计和稳定性经验
熟悉面向对象设计开发，熟悉各种常用设计模式，并有在具体的应用场景落地经验
熟悉Spring、iBatis，等开源框架及消息，存储等常用中间件。 有通读过开源框架源码
熟悉基于Oracle或者Mysql的设计和开发、Linux操作系统
熟悉SOA，有平台化实施经验者，有大数据量、高并发系统和大型网站构建经验
分布式系统应用架构设计与研发经验，精通Java EE、SOA、OSGI等相关技术
对各种开源的框架如Spring、Hibernate等有深入的了解，对框架本身有过开发或重构者可优先考虑
具有大型电子商务网站、O2O行业、C端产品系统架构设计经验
#### 2.腾讯基础：
熟悉常见设计模式，掌握java流行的开源框架SpringMVC/Spring Boot/Spring Cloud，熟练使用至少一种 ORM 框架
熟练掌握基本的数据结构和算法，有系统分析和设计的实践经验
熟悉Rest，HTTP，Socket、webservice、HTTP协议，具备并发、多线程的编程经验
对Mysql、Redis、MongoDB 等数据库有研究或者项目经验
具有大型互联网服务设计及开发经验
熟悉JVM，对JVM有一定理解，并能借助相关工具进行JVM性能调优
熟悉常见的开源分布式中间件、缓存、消息队列等，熟悉nginx，MySQL，Redis，mongodb 等常用的开源软件
熟悉 MySQL 数据库设计和优化，有 NoSQL 数据库使用经验
具有大数据存储或者高性能计算平台架构、设计及开发等方面经历
具有大型互联网服务设计及开发经验
#### 3.百度基础：
精通Web后台开发语言至少一种（PHP、Java、.Net、C++）,有一定的架构能力和良好代码规范
熟悉linux/unix系统与开发环境
熟悉TCP/IP协议，socket编程
熟悉mysql以及SQL语言
有高性能大容量服务系统设计开发经验
精通面向对象设计，精通J2EE开发，java web开发
全面并且扎实的软件知识结构（操作系统、软件工程、设计模式、数据结构、数据库系统、网络安全）；
具备良好的分析解决问题能力，能独立承担任务和有系统进度把控能力
精通MySQL或Mongo DB，熟悉缓存技术memcached、redis
有大型分布式、高并发、高负载、高可用系统设计、开发和调优经验
B/S结构系统分析及设计经验，有构建可伸缩、可扩展、高可用系统经验
有良好的开发习惯，熟悉Maven, Jenkins, JUnit等工具
精通MVC/REST架构、模板引擎、中间件的原理与应用
熟悉MySQL数据库，了解MySQL索引优化、查询优化和存储优化
### 1 java基础：
#### 1.1 算法
1. 排序算法：直接插入排序、希尔排序、冒泡排序、快速排序、直接选择排序、堆排序、归并排序、基数排序
2. 二叉查找树、红黑树、B树、B+树、LSM树（分别有对应的应用，数据库、HBase）
3. BitSet解决数据重复和是否存在等问题

#### 1.2 基本
1. 字符串常量池的迁移
2. 字符串KMP算法
3. equals和hashcode
4. 泛型、异常、反射
5. string的hash算法
6. hash冲突的解决办法：拉链法
7. foreach循环的原理
8. static、final、transient等关键字的作用
9. volatile关键字的底层实现原理
10. Collections.sort方法使用的是哪种排序方法
11. Future接口，常见的线程池中的FutureTask实现等
12. string的intern方法的内部细节，jdk1.6和jdk1.7的变化以及内部cpp代码StringTable的实现

#### 1.3 设计模式
1. 单例模式
2. 工厂模式
3. 装饰者模式
4. 观察者设计模式
5. ThreadLocal设计模式
6. 其他

#### 1.4 正则表达式
1. 捕获组和非捕获组
2. 贪婪，勉强，独占模式

#### 1.5 java内存模型以及垃圾回收算法
1. 类加载机制，也就是双亲委派模型
2. java内存分配模型（默认HotSpot）
3. 线程共享的：堆区、永久区 线程独享的：虚拟机栈、本地方法栈、程序计数器
4. 内存分配机制：年轻代（Eden区、两个Survivor区）、年老代、永久代以及他们的分配过程
5. 强引用、软引用、弱引用、虚引用与GC
6. happens-before规则
7. 指令重排序、内存栅栏
8. Java 8的内存分代改进
9. 垃圾回收算法：
标记-清除（不足之处：效率不高、内存碎片）
复制算法（解决了上述问题，但是内存只能使用一半，针对大部分对象存活时间短的场景，引出了一个默认的8:1:1的改进，缺点是仍然需要借助外界来解决可能承载不下的问题）
标记整理
10. 常用垃圾收集器：
新生代：Serial收集器、ParNew收集器、Parallel Scavenge 收集器
老年代：Serial Old收集器、Parallel Old收集器、CMS（Concurrent Mark Sweep）收集器、 G1 收集器（跨新生代和老年代）
11. 常用gc的参数：-Xmn、-Xms、-Xmx、-XX:MaxPermSize、-XX:SurvivorRatio、-XX:-PrintGCDetails
12. 常用工具： jps、jstat、jmap、jstack、图形工具jConsole、Visual VM、MAT

#### 1.6 锁以及并发容器的源码
1. synchronized和volatile理解
2. Unsafe类的原理，使用它来实现CAS。因此诞生了AtomicInteger系列等
3. CAS可能产生的ABA问题的解决，如加入修改次数、版本号
4. 同步器AQS的实现原理
5. 独占锁、共享锁；可重入的独占锁ReentrantLock、共享锁 实现原理
6. 公平锁和非公平锁
7. 读写锁 ReentrantReadWriteLock的实现原理
8. LockSupport工具
9. Condition接口及其实现原理
10. HashMap、HashSet、ArrayList、LinkedList、HashTable、ConcurrentHashMap、TreeMap的实现原理
11. HashMap的并发问题
12. ConcurrentLinkedQueue的实现原理
13. Fork/Join框架
14. CountDownLatch和CyclicBarrier

#### 1.7 线程池源码
1. 内部执行原理
2. 各种线程池的区别

### 2 web方面：

#### 2.1 SpringMVC的架构设计
1. servlet开发存在的问题：映射问题、参数获取问题、格式化转换问题、返回值处理问题、视图渲染问题
2. SpringMVC为解决上述问题开发的几大组件及接口：HandlerMapping、HandlerAdapter、HandlerMethodArgumentResolver、HttpMessageConverter、Converter、GenericConverter、HandlerMethodReturnValueHandler、ViewResolver、MultipartResolver
3. DispatcherServlet、容器、组件三者之间的关系
4. 叙述SpringMVC对请求的整体处理流程
5. SpringBoot

#### 2.2 SpringAOP源码
1. AOP的实现分类：编译期、字节码加载前、字节码加载后三种时机来实现AOP
2. 深刻理解其中的角色：AOP联盟、aspectj、jboss AOP、Spring自身实现的AOP、Spring嵌入aspectj。特别是能用代码区分后两者
3. 接口设计：
 AOP联盟定义的概念或接口：Pointcut（概念，没有定义对应的接口）、Joinpoint、Advice、MethodInterceptor、MethodInvocation
 SpringAOP针对上述Advice接口定义的接口及其实现类：BeforeAdvice、AfterAdvice、MethodBeforeAdvice、AfterReturningAdvice；针对aspectj对上述接口的实现AspectJMethodBeforeAdvice、AspectJAfterReturningAdvice、AspectJAfterThrowingAdvice、AspectJAfterAdvice。
 SpringAOP定义的定义的AdvisorAdapter接口：将上述Advise转化为MethodInterceptor
 SpringAOP定义的Pointcut接口：含有两个属性ClassFilter（过滤类）、MethodMatcher（过滤方法）
 SpringAOP定义的ExpressionPointcut接口：实现中会引入aspectj的pointcut表达式
 SpringAOP定义的PointcutAdvisor接口（将上述Advice接口和Pointcut接口结合起来）
4. SpringAOP的调用流程
5. SpringAOP自己的实现方式（代表人物ProxyFactoryBean）和借助aspectj实现方式区分

#### 2.3 Spring事务体系源码以及分布式事务Jotm Atomikos源码实现
1. jdbc事务存在的问题
3. Hibernate对事务的改进
3. 针对各种各样的事务，Spring如何定义事务体系的接口，以及如何融合jdbc事务和Hibernate事务的
4. 三种事务模型包含的角色以及各自的职责
5. 事务代码也业务代码分离的实现（AOP+ThreadLocal来实现）
6. Spring事务拦截器TransactionInterceptor全景
7. X/Open DTP模型，两阶段提交，JTA接口定义
8. Jotm、Atomikos的实现原理
9. 事务的传播属性
10. PROPAGATION_REQUIRES_NEW、PROPAGATION_NESTED的实现原理以及区别
11. 事物的挂起和恢复的原理

#### 2.4 数据库隔离级别
1. Read uncommitted：读未提交
2. Read committed ： 读已提交
3. Repeatable read：可重复读
4. Serializable ：串行化

#### 2.5 数据库
1. 数据库性能的优化
2. 深入理解mysql的Record Locks、Gap Locks、Next-Key Locks
例如下面的在什么情况下会出现死锁：
start transaction; DELETE FROM t WHERE id =6; INSERT INTO t VALUES(6); commit;
3. insert into select语句的加锁情况
4. 事务的ACID特性概念
5. innodb的MVCC理解
6. undo redo binlog
7. undo redo 都可以实现持久化，他们的流程是什么？为什么选用redo来做持久化？
8. undo、redo结合起来实现原子性和持久化，为什么undo log要先于redo log持久化？
9. undo为什么要依赖redo？
10. 日志内容可以是物理日志，也可以是逻辑日志？他们各自的优点和缺点是？
11. redo log最终采用的是物理日志加逻辑日志，物理到page，page内逻辑。还存在什么问题？怎么解决？Double Write
12. undo log为什么不采用物理日志而采用逻辑日志？
13. 为什么要引入Checkpoint？
14. 引入Checkpoint后为了保证一致性需要阻塞用户操作一段时间，怎么解决这个问题？（这个问题还是很有普遍性的，redis、ZooKeeper都有类似的情况以及不同的应对策略）又有了同步Checkpoint和异步Checkpoint
15. 开启binlog的情况下，事务内部2PC的一般过程（含有2次持久化，redo log和binlog的持久化）
16. 解释上述过程，为什么binlog的持久化要在redo log之后，在存储引擎commit之前？
17. 为什么要保持事务之间写入binlog和执行存储引擎commit操作的顺序性？（即先写入binlog日志的事务一定先commit）
18. 为了保证上述顺序性，之前的办法是加锁prepare_commit_mutex，但是这极大的降低了事务的效率，怎么来实现binlog的group commit？
19. 怎么将redo log的持久化也实现group commit？至此事务内部2PC的过程，2次持久化的操作都可以group commit了，极大提高了效率

#### 2.6 ORM框架: mybatis、Hibernate
1. 最原始的jdbc->Spring的JdbcTemplate->hibernate->JPA->SpringDataJPA的演进之路

#### 2.7 SpringSecurity、shiro、SSO（单点登录）
1. Session和Cookie的区别和联系以及Session的实现原理
2. SpringSecurity的认证过程以及与Session的关系
3. CAS实现SSO（详见Cas（01）——简介）输入图片说明

#### 2.8 日志
1. jdk自带的logging、log4j、log4j2、logback
2. 门面commons-logging、slf4j
3. 上述6种混战时的日志转换

#### 2.9 datasource
1. c3p0
2. druid
3. JdbcTemplate执行sql语句的过程中对Connection的使用和管理

#### 2.10 HTTPS的实现原理

### 3 分布式、java中间件、web服务器等方面：

#### 3.1 ZooKeeper源码
1. 客户端架构
2. 服务器端单机版和集群版，对应的请求处理器
3. 集群版session的建立和激活过程
4. Leader选举过程
5. 事务日志和快照文件的详细解析
6. 实现分布式锁、分布式ID分发器
7. 实现Leader选举
8. ZAB协议实现一致性原理

#### 3.2 序列化和反序列化框架
1. Avro研究
2. Thrift研究
3. Protobuf研究
4. Protostuff研究
5. Hessian

#### 3.3 RPC框架dubbo源码
1. dubbo扩展机制的实现，对比SPI机制
2. 服务的发布过程
3. 服务的订阅过程
4. RPC通信的设计

#### 3.4 NIO模块以及对应的Netty和Mina、thrift源码
1. TCP握手和断开及有限状态机
2. backlog
3. BIO NIO
4. 阻塞/非阻塞的区别、同步/异步的区别
5. 阻塞IO、非阻塞IO、多路复用IO、异步IO
6. Reactor线程模型
7. jdk的poll、epoll与底层poll、epoll的对接实现
8. Netty自己的epoll实现
9. 内核层poll、epoll的大致实现
10. epoll的边缘触发和水平触发
11. Netty的EventLoopGroup设计
12. Netty的ByteBuf设计
13. Netty的ChannelHandler
13. Netty的零拷贝
14. Netty的线程模型，特别是与业务线程以及资源释放方面的理解

#### 3.5 消息队列kafka、RocketMQ、Notify、Hermes
1. kafka的文件存储设计
2. kafka的副本复制过程
3. kafka副本的leader选举过程
4. kafka的消息丢失问题
5. kafka的消息顺序性问题
6. kafka的isr设计和过半对比
7. kafka本身做的很轻量级来保持高效，很多高级特性没有：事务、优先级的消息、消息的过滤，更重要的是服务治理不健全，一旦出问题，不能直观反应出来，不太适合对数据要求十分严苛的企业级系统，而适合日志之类并发量大但是允许少量的丢失或重复等场景
8. Notify、RocketMQ的事务设计
9. 基于文件的kafka、RocketMQ和基于数据库的Notify和Hermes
10. 设计一个消息系统要考虑哪些方面
11. 丢失消息、消息重复、高可用等话题

#### 3.6 数据库的分库分表mycat

#### 3.7 NoSql数据库mongodb

#### 3.8 KV键值系统memcached redis
1. redis对客户端的维护和管理，读写缓冲区
2. redis事务的实现
3. Jedis客户端的实现
4. JedisPool以及ShardedJedisPool的实现
5. redis epoll实现，循环中的文件事件和时间事件
6. redis的RDB持久化，save和bgsave
7. redis AOF命令追加、文件写入、文件同步到磁盘
8. redis AOF重写，为了减少阻塞时间采取的措施
9. redis的LRU内存回收算法
10. redis的master slave复制
11. redis的sentinel高可用方案
12. redis的cluster分片方案

#### 3.9 web服务器tomcat、ngnix的设计原理
1. tomcat的整体架构设计
2. tomcat对通信的并发控制
3. http请求到达tomcat的整个处理流程

#### 3.10 ELK日志实时处理查询系统
1. Elasticsearch、Logstash、Kibana

#### 3.11 服务方面
1. SOA与微服务
2. 服务的合并部署、多版本自动快速切换和回滚
详见基于Java容器的多应用部署技术实践
3. 服务的治理：限流、降级
具体见 张开涛大神的架构系列
服务限流：令牌桶、漏桶
服务降级、服务的熔断、服务的隔离：netflix的hystrix组件
4. 服务的线性扩展
无状态的服务如何做线性扩展：
如一般的web应用，直接使用硬件或者软件做负载均衡，简单的轮训机制
有状态服务如何做线性扩展：
如Redis的扩展：一致性hash，迁移工具
5. 服务链路监控和报警：CAT、Dapper、Pinpoint

#### 3.12 Spring Cloud
1. Spring Cloud Zookeeper:用于服务注册和发现
2. Spring Cloud Config:分布式配置
3. Spring Cloud Netflix Eureka：用于rest服务的注册和发现
4. Spring Cloud Netflix Hystrix：服务的隔离、熔断和降级
5. Spring Cloud Netflix Zuul:动态路由，API Gateway

#### 3.13 分布式事务
1. JTA分布式事务接口定义，对此与Spring事务体系的整合
2. TCC分布式事务概念
3. TCC分布式事务实现框架案例1：tcc-transaction
13.3.1 TccCompensableAspect切面拦截创建ROOT事务
13.3.2 TccTransactionContextAspect切面使远程RPC调用资源加入到上述事务中，作为一个参与者
13.3.3 TccCompensableAspect切面根据远程RPC传递的TransactionContext的标记创建出分支事务
13.3.4 全部RPC调用完毕，ROOT事务开始提交或者回滚，执行所有参与者的提交或回滚
13.3.5 所有参与者的提交或者回滚，还是通过远程RPC调用，provider端开始执行对应分支事务的confirm或者cancel方法
13.3.6 事务的存储，集群共享问题
13.3.7 事务的恢复，避免集群重复恢复
4. TCC分布式事务实现框架案例2：ByteTCC
13.4.1 JTA事务管理实现，类比Jotm、Atomikos等JTA实现
13.4.2 事务的存储和恢复，集群是否共享问题
调用方创建CompensableTransaction事务，并加入资源
13.4.3 CompensableMethodInterceptor拦截器向spring事务注入CompensableInvocation资源
13.4.4 Spring的分布式事务管理器创建作为协调者CompensableTransaction类型事务，和当前线程进行绑定，同时创建一个jta事务
13.4.5 在执行sql等操作的时候，所使用的jdbc等XAResource资源加入上述jta事务
13.4.6 dubbo RPC远程调用前，CompensableDubboServiceFilter创建出一个代理XAResource，加入上述CompensableTransaction类型事务，并在RPC调用过程传递TransactionContext
参与方创建分支的CompensableTransaction事务，并加入资源，然后提交jta事务
13.4.7 RPC远程调用来到provider端，CompensableDubboServiceFilter根据传递过来的TransactionContext创建出对应的CompensableTransaction类型事务
13.4.8 provider端，执行时遇见@Transactional和@Compensable，作为一个参与者开启try阶段的事务，即创建了一个jta事务
13.4.9 provider端try执行完毕开始准备try的提交，仅仅是提交上述jta事务，返回结果到RPC调用端
调用方决定回滚还是提交
13.4.10 全部执行完毕后开始事务的提交或者回滚，如果是提交则先对jta事务进行提交（包含jdbc等XAResource资源的提交），提交成功后再对CompensableTransaction类型事务进行提交，如果jta事务提交失败，则需要回滚CompensableTransaction类型事务。
13.4.11 CompensableTransaction类型事务的提交就是对CompensableInvocation资源和RPC资源的提交，分别调用每一个CompensableInvocation资源的confirm，以及每一个RPC资源的提交
CompensableInvocation资源的提交
13.4.12 此时每一个CompensableInvocation资源的confirm又会准备开启一个新的事务，当前线程的CompensableTransaction类型事务已存在，所以这里开启事务仅仅是创建了一个新的jta事务而已
13.4.13 针对此，每一个CompensableInvocation资源的confirm开启的事务，又开始重复上述过程，对于jdbc等资源都加入新创建的jta事务中，而RPC资源和CompensableInvocation资源仍然加入到当前线程绑定的CompensableTransaction类型事务
13.4.14 当前CompensableInvocation资源的confirm开启的事务执行完毕后，开始执行commit,此时仍然是执行jta事务的提交，提交完毕，一个CompensableInvocation资源的confirm完成，继续执行下一个CompensableInvocation资源的confirm，即又要重新开启一个新的jta事务
RPC资源的提交（参与方CompensableTransaction事务的提交）
13.4.15 当所有CompensableInvocation资源的confirm执行完毕，开始执行RPC资源的commit，会进行远程调用，执行远程provider分支事务的提交，远程调用过程会传递事务id
13.4.16 provider端，根据传递过来的事务id找到对应的CompensableTransaction事务，开始执行提交操作，提交操作完成后返回响应
结束
13.4.17 协调者收到响应后继续执行下一个RPC资源的提交，当所有RPC资源也完成相应的提交，则协调者算是彻底完成该事务

#### 3.14 一致性算法
1. raft（详见Raft算法赏析）
14.1.1 leader选举过程，leader选举约束，要包含所有commited entries，实现上log比过半的log都最新即可
14.1.2 log复制过程，leader给所有的follower发送AppendEntries RPC请求，过半follower回复ok，则可提交该entry，然后向客户端响应OK
14.1.3 在上述leader收到过半复制之后，挂了，则后续leader不能直接对这些之前term的过半entry进行提交（这一部分有详细的案例来证明，并能说出根本原因），目前做法是在当前term中创建空的entry，然后如果这些新创建的entry被大部分复制了，则此时就可以对之前term的过半entry进行提交了
14.1.4 leader一旦认为某个term可以提交了，则更新自己的commitIndex，同时应用entry到状态机中，然后在下一次与follower的heartbeat通信中，将leader的commitIndex带给follower，让他们进行更新，同时应用entry到他们的状态机中
14.1.5 从上述流程可以看到，作为client来说，可能会出现这样的情况：leader认为某次client的请求可以提交了（对应的entry已经被过半复制了），此时leader挂了，还没来得及给client回复，也就是说对client来说，请求虽然失败了，但是请求对应的entry却被持久化保存了，但是有的时候却是请求失败了（过半都没复制成功）没有持久化成功，也就是说请求失败了，服务器端可能成功了也可能失败了。所以这时候需要在client端下功夫，即cleint端重试的时候仍然使用之前的请求数据进行重试，而不是采用新的数据进行重试，服务器端也必须要实现幂等。
14.1.6 Cluster membership changes
2. ZooKeeper使用的ZAB协议（详见ZooKeeper的一致性算法赏析）
14.2.1 leader选举过程。要点：对于不同状态下的server的投票的收集，投票是需要选举出一个包含所有日志的server来作为leader
14.2.2 leader和follower数据同步过程，全量同步、差异同步、日志之间的纠正和截断，来保证和leader之间的一致性。以及follower加入已经完成选举的系统，此时的同步的要点：阻塞leader处理写请求，完成日志之间的差异同步，还要处理现有进行中的请求的同步，完成同步后，解除阻塞。
14.2.3 广播阶段，即正常处理客户端的请求，过半响应即可回复客户端。
14.2.4 日志的恢复和持久化。持久化：每隔一定数量的事务日志持久化一次，leader选举前持久化一次。恢复：简单的认为已写入日志的的事务请求都算作已提交的请求（不管之前是否已过半复制），全部执行commit提交。具体的恢复是：先恢复快照日志，然后再应用相应的事务日志
3. paxos（详见paxos算法证明过程）
14.3.1 paxos的运作过程：
Phase 1: (a) 一个proposer选择一个编号为n的议案，向所有的acceptor发送prepare请求
Phase 1: (b) 如果acceptor已经响应的prepare请求中议案编号都比n小，则它承诺不再响应prepare请求或者accept请求中议案编号小于n的， 并且找出已经accept的最大议案的value返回给该proposer。如果已响应的编号比n大，则直接忽略该prepare请求。
Phase 2：(a) 如果proposer收到了过半的acceptors响应，那么将提出一个议案（n，v）,v就是上述所有acceptor响应中最大accept议案的value，或者是proposer自己的value。然后将该议案发送给所有的acceptor。这个请求叫做accept请求，这一步才是所谓发送议案请求，而前面的prepare请求更多的是一个构建出最终议案(n,v)的过程。
Phase 2：(b) acceptor接收到编号为n的议案，如果acceptor还没有对大于n的议案的prepare请求响应过，则acceptor就accept该议案，否则拒绝
14.3.2 paxos的证明过程：
1 足够多的问题
2 acceptor的初始accept
3 P2-对结果要求
4 P2a-对acceptor的accept要求
5 P2b-对proposer提出议案的要求（结果上要求）
6 P2c-对proposer提出议案的要求（做法上要求）
7 引出prepare过程和P1a
8 优化prepare
14.3.3 base paxos和multi-paxos

### 4 大数据方向

#### 4.1 Hadoop
1. UserGroupInformation源码解读：JAAS认证、user和group关系的维护
2. RPC通信的实现
3. 代理用户的过程
4. kerberos认证

#### 4.2 MapReduce
1. MapReduce理论及其对应的接口定义

#### 4.3 HDFS
1. MapFile、SequenceFile
2. ACL

#### 4.4 YARN、Mesos 资源调度

#### 4.5 oozie
1. oozie XCommand设计
2. DagEngine的实现原理

#### 4.6 Hive
1. HiveServer2、metatore的thrift RPC通信设计
2. Hive的优化过程
3. HiveServer2的认证和授权
4. metastore的认证和授权
5. HiveServer2向metatore的用户传递过程

#### 4.7 Hbase
1. Hbase的整体架构图
2. Hbase的WAL和MVCC设计
3. client端的异步批量flush寻找RegionServer的过程
4. Zookeeper上HBase节点解释
5. Hbase中的mini、major合并
6. Region的高可用问题对比kafka分区的高可用实现
7. RegionServer RPC调用的隔离问题
8. 数据从内存刷写到HDFS的粒度问题
9. rowKey的设计
10. MemStore与LSM

#### 4.8 Spark
1. 不同的部署方式
2. SparkSql的实现方式
3. 。。。