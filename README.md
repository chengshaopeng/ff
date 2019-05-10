#lnmp 和 laravel 一键安装包配置
##一、修改/user/local/php/etc/php.ini中的配置
	display_errors = Off 修改为On  错误信息
    
    disable_functions 中删除  proc_open,proc_get_status
##二、修改/user/local/nginx/conf/nginx.conf
	
	server中：

	root /home/wwwroot/default   改为：
	
	root /home/wwwroot/default/项目目录/public

	加入：
	 location / {
            try_files $uri $uri/ /index.php?$query_string;
     }

##三、修改/user/local/nginx/confi/fastcgi.conf
	
	最后一行

	fastcgi_param PHP_ADMIN_VALUE "open_basedir=$document_root/:/tmp/:/proc/";	
	
	修改为：
	
	fastcgi_param PHP_ADMIN_VALUE "open_basedir=/home/wwwroot/default/项目目录/:/tmp/:/proc/";

##四、进入/home/wwwroot/default
	1、git clone 项目路径   #克隆下项目
	
	2、cd 进入项目

	3、chmod R 777 storage

	4、chmod -R 777 bootstrap/cache  #修改权限

	5、cp .env.example .env

	6、vim .env

	修改配置信息

	7、php artisan key:generate

	8、composer update

##五、特别说明

   nginx 的 访问信息log 在 /home/wwwroot/access.log中查看