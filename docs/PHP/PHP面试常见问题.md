# PHP面试常见问题
###### PHP 基础相关
* PHP 编译的过程
* PHP 变量底层是如何实现的？
	> 利用zval结构体实现的。
* Nginx与PHP-FPM 的通信过程？
	> php-fpm 它是 FastCGI 的实现，并提供了进程管理的功能，在 Linux 上，nginx 与 php-fpm 的通信有 tcp socket 和 unix socket 两种方式；tcp socket 的优点是可以跨服务器，当 nginx 和 php-fpm 不在同一台机器上时，只能使用这种方式。[相关博客](https://www.cnblogs.com/a609251438/p/11867154.html "相关博客")。
* Nginx 监听端口和 socket 方式，有何区别？
* PHP-FPM 是怎么调用 PHP 代码的？
	>PHP-FPM是FastCGI的实现，并提供了进程管理的功能。进程包含master进程和worker进程两种进程。master 进程只有一个，负责监听端口，接收来自 Web Server 的请求，而worker进程则一般有多个(具体数量根据实际需要配置)，每个进程内部都嵌入了一个 PHP 解释器是 PHP代码真正执行的地方。
* PHP 是如何连接 MySQL 的？连接池是如何实现的？
	>mysql_connent、mysqli、PDO;连接池对于PHP来说，只有在常驻内存开发中才能实现，如：在swoole中开发，easyswoole和swoft都实现了连接池；
	>
	>连接池简单来说，就是创建一个容器，并且把资源提前准备好放在里面，比如我们常用的redis连接、mysql连接
	>
	>如果在短时间内进行一万次mysql的连接，就需要在这个往返过程循环，在路上浪费了很多时间、性能消耗，说白了也就是要进行三万次的握手，造成资源浪费。
	>
	>如果我们先把连接连接好，并且放在连接池中，程序中需要使用就从池中获取，执行操作。
	就省去了反复创建连接、断开连接的操作。
	可以减少I/O操作，提高资源利用率。
* 谈下 PHP 和 Golang 的区别
	* 1、PHP是弱类型语言，Golang是强类型语言
	* 2、PHP是解释型语言，Golang编译型语言
	* 3、编译型语言一般运行速度要优于解释型语言
* Swoole 和 Go 中的协程有何区别？
* Go 中 goruntine 的底层实现？go 中的协程是怎么通信的？
###### PHP 函数相关
* array_key_exists () 和 in_array () 哪个性能较好？
	>array_key_exists()性能相对较好，因为KEY是进行HASH组织的，查询很快
###### PHP 编码相关
* 说一下你写的项目中的代码架构？（mvc、transformer、中间件等）
* laravel 中常用设计模式（除了依赖注入和控制反转，还问到了策略模式和装饰者模式）
* composer 自动加载机制（psr-4）
###### 数据库（MySQL）
* 老生常谈的有：常见的优化手段、为什么使用 B+ 树存储、索引类型、隔离级别等。
* 现在有联合索引 a,b,c, 使用 select * from table where c=1 and a=2 其中 a 和 c 分别都可以走索引吗？为什么
* 只使用 MySQL 在高并发下的问题
* MySQL 执行慢怎么处理？explain 中 extra 字段中一般都会出现什么信息？如果在 explain 中看到 sql 已经走了索引，但是执行还是慢，会是什么原因？
* MySQL 中排它锁的加锁时机？能否手动加排它锁？
* myisam 引擎和 innodb 存储数据方式有何不同？myisam 这种存储方式又有何优点？
* MySQL 主从出现延迟要如何解决？
###### Redis 和 NoSQL
* Redis 和 MongoDB 的区别
* Redis 缓存雪崩、击穿、穿透的概念和解决方法
* Redis 哨兵之间如何通信？
* Redis 的连接数用完了怎么办？
* 一致性哈希和哈希槽的区别？
* 延时队列（这个是通过一个解决方案来问的，问题是延时发送短信或邮件如何实现）
* 如何保证一个接口一个用户请求在一秒内只能请求一次？
###### 操作系统
* 线程和协程的区别
* session 共享