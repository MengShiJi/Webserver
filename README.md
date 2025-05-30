# Webserver
项目介绍
  项目由IO多路复用模块、定时器模块、线程池模块、缓冲区模块组成。实现了浏览器访问服务器，获取服务器资源的功能。
  
  项目总体的框架采用的是单Reactor多线程模型。在主线程里通过IO多路复用监听多个文件描述符上的事件。主线程负责连接的建立和断开，同时将读写和逻辑处理任务加入线程池里的任务队列，由线程池里的线程负责完成相应操作实现任务的并行处理。在应用层，通过定时器来清除不活跃的连接减少高并发场景下不必要的系统资源的占用（文件描述符的占用、维护一个TCP连接所需要的资源） 。对于到达的HTTP报文，采用了有限状态机和正则表达式进行解析，资源的响应则通过集中写和内存映射的方式进行传输。

项目职责
  在应用层采用HTTP1.1协议构建B/S模型。通过使用状态机和正则表达式完成HTTP报文的解析。
  通过构建线程池完成多个读写任务和逻辑处理任务的并行处理。
  同时采用Reactor设计模式和IO多路复用实现了高并发的服务器。
  在应用层检测不活跃连接，通过及时释放资源来确保服务器在高并发场景下也能够稳定可靠。
