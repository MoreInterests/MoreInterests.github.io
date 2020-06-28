---
title: Java-day26
img: 'https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05231.jpg'
top: false
cover: false
toc: true
mathjax: false
author: xing xiao
tags: Java
categories: 编程
abbrlink: 18524
date: 2020-06-27 21:28:01
coverImg:
password:
summary:
---
## 1:网络编程(理解)
###	(1)网络编程：用Java语言实现计算机间数据的信息传递和资源共享
###	(2)网络编程模型
###	(3)网络编程的三要素
####		A:IP地址
			a:点分十进制
			b:IP地址的组成
			c:IP地址的分类
			d:dos命令
			e:InetAddress
####		B:端口
			是应用程序的标识。范围：0-65535。其中0-1024不建议使用。
####		C:协议
			UDP:数据打包,有限制,不连接,效率高,不可靠
			TCP:建立数据通道,无限制,效率低,可靠
###	(3)Socket机制
####		A:通信两端都应该有Socket对象
####		B:所有的通信都是通过Socket间的IO进行操作的
###	(4)UDP协议发送和接收数据(掌握 自己补齐代码)
####		发送：
/*
 * UDP协议发送数据：
 * A:创建发送端Socket对象
 * B:创建数据，并把数据打包
 * C:调用Socket对象的发送方法发送数据包
 * D:释放资源
 */  
 
		// 创建发送端Socket对象
		// DatagramSocket()
		DatagramSocket ds = new DatagramSocket();

		// 创建数据，并把数据打包
		// DatagramPacket(byte[] buf, int length, InetAddress address, int port)
		// 创建数据
		byte[] bys = "hello,udp,我来了".getBytes();
		// 长度
		int length = bys.length;
		// IP地址对象
		InetAddress address = InetAddress.getByName("192.168.12.92");
		// 端口
		int port = 10086;
		DatagramPacket dp = new DatagramPacket(bys, length, address, port);

		// 调用Socket对象的发送方法发送数据包
		// public void send(DatagramPacket p)
		ds.send(dp);

		// 释放资源
		ds.close();
			
####		接收：
/*
 * UDP协议接收数据：
 * A:创建接收端Socket对象
 * B:创建一个数据包(接收容器)
 * C:调用Socket对象的接收方法接收数据
 * D:解析数据包，并显示在控制台
 * E:释放资源
 */  

		// 创建接收端Socket对象
		// DatagramSocket(int port)
		DatagramSocket ds = new DatagramSocket(10086);

		// 创建一个数据包(接收容器)
		// DatagramPacket(byte[] buf, int length)
		byte[] bys = new byte[1024];
		int length = bys.length;
		DatagramPacket dp = new DatagramPacket(bys, length);

		// 调用Socket对象的接收方法接收数据
		// public void receive(DatagramPacket p)
		ds.receive(dp); // 阻塞式

		// 解析数据包，并显示在控制台
		// 获取对方的ip
		// public InetAddress getAddress()
		InetAddress address = dp.getAddress();
		String ip = address.getHostAddress();
		// public byte[] getData():获取数据缓冲区
		// public int getLength():获取数据的实际长度
		byte[] bys2 = dp.getData();
		int len = dp.getLength();
		String s = new String(bys2, 0, len);
		System.out.println(ip + "传递的数据是:" + s);

		// 释放资源
		ds.close();
###	(5)TCP协议发送和接收数据(掌握 自己补齐代码)
####		发送：
/*
 * TCP协议发送数据：
 * A:创建发送端的Socket对象
 * 		这一步如果成功，就说明连接已经建立成功了。
 * B:获取输出流，写数据
 * C:释放资源
 * 
 * 连接被拒绝。TCP协议一定要先看服务器。
 * java.net.ConnectException: Connection refused: connect
 */  

		// 创建发送端的Socket对象
		// Socket(InetAddress address, int port)
		// Socket(String host, int port)
		// Socket s = new Socket(InetAddress.getByName("192.168.12.92"), 8888);
		Socket s = new Socket("192.168.12.92", 8888);

		// 获取输出流，写数据
		// public OutputStream getOutputStream()
		OutputStream os = s.getOutputStream();
		os.write("hello,tcp,我来了".getBytes());

		// 释放资源
		s.close();
			
####		接收：
/*
 * TCP协议接收数据：
 * A:创建接收端的Socket对象
 * B:监听客户端连接。返回一个对应的Socket对象
 * C:获取输入流，读取数据显示在控制台
 * D:释放资源
 */  

		// 创建接收端的Socket对象
		// ServerSocket(int port)
		ServerSocket ss = new ServerSocket(8888);

		// 监听客户端连接。返回一个对应的Socket对象
		// public Socket accept()
		Socket s = ss.accept(); // 侦听并接受到此套接字的连接。此方法在连接传入之前一直阻塞。

		// 获取输入流，读取数据显示在控制台
		InputStream is = s.getInputStream();

		byte[] bys = new byte[1024];
		int len = is.read(bys); // 阻塞式方法
		String str = new String(bys, 0, len);

		String ip = s.getInetAddress().getHostAddress();

		System.out.println(ip + "---" + str);

		// 释放资源
		s.close();
		// ss.close(); //这个不应该关闭 
###	(6)案例：
####		A:UDP
			a:最基本的UDP协议发送和接收数据
			b:把发送数据改进为键盘录入
			c:一个简易聊天小程序并用多线程改进
####		B:TCP
			a:最基本的TCP协议发送和接收数据
			b:服务器给出反馈
			c:客户端键盘录入服务器控制台输出
			d:客户端键盘录入服务器写到文本文件
			e:客户端读取文本文件服务器控制台输出
			f:客户端读取文本文件服务器写到文本文件
			g:上传图片
			h:多线程改进上传文件
![UDP协议发送和接收数据图解](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/PUDP协议发送和接收数据图解.bmp)

![TCP协议发送和接收数据图解](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/PTCP协议发送和接收数据图解.bmp)