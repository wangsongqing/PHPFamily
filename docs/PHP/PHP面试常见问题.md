# PHP面试常见问题
###### PHP 基础相关
* PHP 编译的过程
* PHP 变量底层是如何实现的？
	> 利用zval结构体实现的
* Nginx 与 php-fpm 的通信过程？
	> php-fpm 它是 FastCGI 的实现，并提供了进程管理的功能，在 Linux 上，nginx 与 php-fpm 的通信有 tcp socket 和 unix socket 两种方式；tcp socket 的优点是可以跨服务器，当 nginx 和 php-fpm 不在同一台机器上时，只能使用这种方式
* Nginx 监听端口和 socket 方式，有何区别？
* php-fpm 是怎么调用 PHP 代码的？
* PHP 是如何连接 MySQL 的？连接池是如何实现的？
* 谈下 PHP 和 Golang 的区别
* Swoole 和 Go 中的协程有何区别？
* Go 中 goruntine 的底层实现？go 中的协程是怎么通信的？
###### PHP 函数相关
* array_key_exists () 和 in_array () 哪个性能较好？
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