## 安装laravel 5.4
* step 1 : 安装[composer](https://getcomposer.org/download/)

* step 2 : composer安装laravel

    ``` shell
    composer global require "laravel/installer"
    ```

* step 3 : 创建laravel项目

    ``` shell
    //创建blog文件夹，并下载相关文件到blog文件夹下
    laravel new blog
    ```
* step 4 ： 开启php服务（无需使用wamp）

    ``` shell
    php artisan server
    ```

* step 5 : 文件夹权限

    `storage`与`bootstrap/cache`文件夹需要可写
