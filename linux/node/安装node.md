## linux安装node

* **step 1 ：下载或上传文件**
文件名:node-v6.10.2.tar.gz
存放路径: /usr/local/src

* **step 2 : 解压源码**
`tar zxvf node-v6.10.24.tar.gz`

* **step 3 :安装编译**
    ``` shell
    cd node-v6.10.2
    ./configure --prefix=/usr/local/node/6.10.2
    make
    make install
    ```

    **注意：** 如果是centOS7.0 可以直接编译安装.如果是centOS 6.5 32位 的需要以下处理

    * 升级CXX=g++库
    **提示:**
    `WARNING: C++ compiler too old, need g++ 4.8 or clang++ 3.4 (CXX=g++)`

    **解决:**
        ``` shell
    	wget http://gcc.skazkaforyou.com/releases/gcc-4.9.1/gcc-4.9.1.tar.gz
    	tar -xf gcc-4.9.1.tar.gz
    	cd gcc-4.9.1
    	./contrib/download_prerequisites
    	mkdir gcc_temp
    	cd gcc_temp
    	../configure --enable-checking=release --enable-languages=c,c++ --disable-multilib
    	make & make install
        ```
    * 升级安装GCC库
    **提示：**
    `make[1]: *** [/usr/local/src/node-v6.10.2/out/Release/obj.target/v8_snapshot/geni/snapshot.cc] Error 1`

    **解决：**
    ``` shell
	find / -name "libstdc++.so.6"
	cp /home/node/gcc-4.9.1/gcc_temp/stage1-i686-pc-linux-gnu/libstdc++-v3/src/.libs/libstdc++.so.6 /usr/lib
    ```
    _完成以上操作，重新编译 make&make install_


* **step 4 : 设置nodejs home 目录**
``` shell
vim /etc/profile
export NODE_HOME=/usr/local/node/6.10.2
export PATH=$NODE_HOME/bin:$PATH
```

* **step 5 : 编译/etc/profile 使配置生效**
`source /etc/profile`
