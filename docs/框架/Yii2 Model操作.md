# Yii2手册
## Model 操作数据库 新增
```php

        $customer = new User();
		$customer->name = 'Qiang';
		$customer->save();

		// 块赋值
		$values = [
    		'name' => 'James',
    		'email' => 'james@example.com',
		];

		$customer = new Customer();
		$customer->attributes = $values;
		$customer->save();
```
## Model 操作数据库 查询
    <?php
        //SELECT * FROM `User` WHERE `id` = 123 查询单条数据
		$customer = User::find()->where(['id' => 123])->one();

		// SELECT * FROM `User` WHERE `status` = 1 ORDER BY `id` 查询多条和排序
		$customers = User::find()->where(['status' => 1])->orderBy('id')->all();

		// SELECT COUNT(*) FROM `User` WHERE `status` = 1 //查询数量
		$count = User::find()->where(['status' => 1])->count();
		
		// SELECT * FROM `User` WHERE `id` = 123 主键查询一行
		$customer = User::findOne(123);

		// SELECT * FROM `User` WHERE `id` IN (100, 101, 123, 124) 主键查询多行
		$customers = User::findAll([100, 101, 123, 124]);

		// SELECT * FROM `User` WHERE `id` = 123 AND `status` = 1 主键和其他条件一起查询
		$customer = User::findOne(['id' => 123,'status' => 1]);
		
		//in查询
		$count = User::find()->where(['id' => [1,2,3]])->all();

		//not in查询
		$count = User::find()->where(['status' => 1])->andWhere(['not in','id',[88,98]])->all();

		//left join 连表查询
		// SELECT `customer`.* FROM `customer` LEFT JOIN `order` ON `order`.`customer_id` = `customer`.`id` WHERE `order`.`status` = 1
		$customers = Customer::find()
    		->select('customer.*')
    		->leftJoin('order', '`order`.`customer_id` = `customer`.`id`')
   			->where(['order.status' => Order::STATUS_ACTIVE])
    		->with('orders')
    		->all();
    ?>
## Model 操作数据库 原生SQL查询
```php

       $sql = 'SELECT * FROM User WHERE status=:status';
	   $customers = User::findBySql($sql, [':status' => 1])->all();
	   $customers = User::findBySql($sql, [':status' => 1])->one();

		$db  = Yii::$app->db;
		$sql = "select * from user";
		$command = $db->createCommand($sql)->queryAll();//查询全部
		$command = $db->createCommand($sql)->queryOne();//查询一条数据

		$updateSql = "update user set username='wangsongqing'";
		$db->createCommand($updateSql)->execute();//执行修改的添加的使用
```
## Model 操作数据库 更新
```php

        $customer = User::findOne(123);
		$customer->name = 'Qiang';
		$customer->save();
		
		// UPDATE `customer` SET `status` = 1 WHERE `email` LIKE `%@example.com%`
		User::updateAll(['status' => 1], ['like', 'email', '@example.com']);		

		$post = User::findOne(100); // +1 -1
		// UPDATE `User` SET `view_count` = `view_count` + 1 WHERE `id` = 100
		$post->updateCounters(['view_count' => 1]);
```
## Model 操作数据库 删除
	<?php
        $customer = User::findOne(123);
		$customer->delete();

		User::deleteAll(['status' => 1]);
    ?>
## Model 操作数据库 事务方式1
	<?php
        $transaction = User::getDb()->beginTransaction();//开启事务
		try {
		    $customer->id = 200;
		    $customer->save();
		    // ...other DB operations...
		    $transaction->commit();//提交事务
		} (\Throwable $e) {
		    $transaction->rollBack();////回滚事务
		    throw $e;
		}
    ?>
## Model 操作数据库 事务方式2
	<?php
		$connection = new User();
       // $connection其实是数据库连接
		$transaction = $connection->beginTransaction();
		try {
			
		    $connection->createCommand($sql1)->execute();
		    $connection->createCommand($sql2)->execute();
		    // ... executing other SQL statements ...
		    $transaction->commit();
		} catch (Exception $e) {
		    $transaction->rollBack();
		}
    ?>
## Model 操作数据库 事务方式3
	<?php
		$transaction = Yii::$app->db->beginTransaction();
		try {
		    // ... executing other SQL statements ...
		    $transaction->commit();
		} catch (\Exception $e) {
		    $transaction->rollBack();
		}
    ?>
## Model 其他

User::find()->average();    此方法返回指定列的平均值；

User::find()->min();    此方法返回指定列的最小值 ；

User::find()->max();    此方法返回指定列的最大值 ；

User::find()->scalar();    此方法返回值的第一行第一列的查询结果；

User::find()->column();    此方法返回查询结果中的第一列的值；

User::find()->exists();    此方法返回一个值指示是否包含查询结果的数据行；

User::find()->batch(10);  每次取 10 条数据 

User::find()->each(10);  每次取 10 条数据， 迭代查询

###执行原生DML语句
$sql = "update user set name='zhangsan' where id='1'";

Yii::$app->db->createCommand($sql)->execute();

###获取当前程序执行的sql语句
$query = User::find() ->where(['id'=>[1,2,3,4]) ->select(['username'])

// 输出SQL语句
$commandQuery = clone $query;
echo $commandQuery->createCommand()->getRawSql();

$users = $query->all();
