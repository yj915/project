# ftp

        Linux C++实现的FTP服务器/客户端，采用io多路复用(epoll) + 线程池的方式提高并发性
        支持的命令有
        1. USER :  客户端登录命令
        2. PASS :  客户端输入密码指令，默认不需要密码，上述两条指令无实际用处
        3. PASV :  切换被动模式
        4. PORT :  切换主动模式
        5. LIST :  列出服务器当前路径下的所有文件/目录
        6. PWD  :  打印当前工作目录
        7. CWD  :  改变当前工作目录
        8. SIZE :  获取目标文件字节数
        9. RETR :  从服务器下载指定文件
        10. STOR:  上传制定文件到服务器当前目录
        11. REST:  断点续传
        12. QUIT:  退出客户端


        注：同一台机器只能运行一个客户端
#功能：实现一个简易的FTP服务器，支持文件的上传、下载，以及断点续传 #采用多线程模型完成 #有port和pasv两种工作模式

#下面是个函数功能简单介绍 1, 基本模块： main.c sysutil.c strutil.c session.c ftp_nobody.c ftp_proto.c common.h 其中，session模块是核心， ftp_nobody模块实现nobody功能，主要实现控制功能， ftp_proto模块负责一些具体的实现，实现数据传输功能 sysutil模块是系统函数模块、strutil模块是字符串处理模块，common.h用来存放公共头文件； 2，configure.c parse_conf.c ftp_codes.h 分别是配置文件模块，配置文件解析模块、FTP应答的宏模块； 3， 具体实现模块 command_map.c priv_sock.c trans_data.c trans_ctrl.c 分别对应的是命令映射控制模块、命令请求和应答模块、数据传输模块、控制连接和数据连接模块(上传和下载限速等) 4， 其他 hash.c ftp_assist.c 哈希模块（用来控制客户端和ip连接数）、main函数实现模块

用户加密认证
服务端采用 SocketServer实现，支持多客户端连接
每个用户有自己的家目录且只能访问自己的家目录
对用户进行磁盘配额、不同用户配额可不同
用户可以登陆server后，可切换目录
能查看当前目录下文件
上传下载文件，保证文件一致性
传输过程中实现进度条展示
用户可在自己家目录进行创建目录、文件、删除目录及文件
服务端可实现增加用户、删除用户
支持上传时断点续传


