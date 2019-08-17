redis源码解析（一）

GitHub地址:https://github.com/QH-LEO

#第一次用github写博客，由于时间原因，未能有效构建博客网站，敬请谅解

！！

#笔者为在校大二学生，博文来之不易，转载请说明出处

！！

What is Redis?

Redis is often referred as a data structures server. What this means is that Redis provides access to mutable data structures via a set of commands, which are sent using a server-client model with TCP sockets and a simple protocol. So different processes can query and modify the same data structures in a shared way.

<>提供两种行之有效的办法：

目前网上大多为第一种：分治法

参考博客：https://blog.csdn.net/nawenqiang/article/details/78461031 （redis源码阅读步骤，其中按块划分）

        https://blog.csdn.net/kkwant/article/details/81668871 （简介每一个文件作用）
        
提供redis源码下载：

        分享网上大神写的redis3.0注释版 百度谷歌直搜
        
        redis4.0 5.0推荐官网下载https://redis.io/download
        
！！        

强烈安利第二种：中断法

！！

方法简述：1.编译源码，clion启动

        2.读者应了解redis通信协议http://redisdoc.com/topic/protocol.html
        
        ！！！！！！！！！！！！！
        
        全文关键：server端应打断点到network.c中的processMultibulkBuffer(redisClient *c)函数
        
        ！！！！！！！！！！！！！
        
        3.选择Telnet连接6379端口发送协议
        
        eg:
        *3 $3 SET $5 mykey $7 myvalue
        
        或者redis客户端启动发送set a 1 命令
        
        4.server端自动断入断点处，执行断点函数，可以观察到命令已经按照协议解析
        
        5.笔者几乎尝试了所有命令，发现这种方式能够完美无缺的，无一遗漏的展现redis工作过程以及设计思路
        
        6.补充还需深入研究aof和rdb方式配合与选用，才能对缓存级数据库的应用以及全景有所认识。
