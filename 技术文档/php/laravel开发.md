#laravel开发记录

>常用的一些命令
>

##artisan 集合
	>创建表
	php artisan make:migration create_users_table --create=users //创建users表
	>修改表
	php artisan make:migration add_votes_to_users_table --table=users //给users表增加votes字段
	>执行迁移 加上--force 参数执行强制迁移
	 php artisan migrate --force
	>回滚上一次的迁移
	 php artisan migrate:rollback
##数据库操作
http://www.golaravel.com/laravel/docs/5.0/migrations/	
		// Increments
		$table->increments('id');
		$table->bigIncrements('id');
		
		// Numbers
		$table->integer('votes');
		$table->tinyInteger('votes');
		$table->smallInteger('votes');
		$table->mediumInteger('votes');
		$table->bigInteger('votes');
		$table->float('amount');
		$table->double('column', 15, 8);
		$table->decimal('amount', 5, 2);
		
		//String and Text
		$table->char('name', 4);
		$table->string('email');
		$table->string('name', 100);
		$table->text('description');
		$table->mediumText('description');
		$table->longText('description');
		
		//Date and Time
		$table->date('created_at');
		$table->dateTime('created_at');
		$table->time('sunrise');
		$table->timestamp('added_on');
		$table->timestamps();
		// Adds created_at and updated_at columns
		$table->nullableTimestamps();
		
		// Others
		$table->binary('data');
		$table->boolean('confirmed');
		$table->softDeletes();
		// Adds deleted_at column for soft deletes
		$table->enum('choices', array('foo', 'bar'));
		$table->rememberToken();
		// Adds remember_token as VARCHAR(100) NULL
		$table->morphs('parent');
		// Adds INTEGER parent_id and STRING parent_type
		 ->nullable()
		->default($value)
		->unsigned()