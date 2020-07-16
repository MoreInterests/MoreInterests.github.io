---
title: Linux-命令
img: 
top: false
cover: false
toc: true
mathjax: false
date: 2020-07-14 17:19:27
author: xing xiao
coverImg:
password:
summary:
tags: 命令
categories: Linux
---
## 软件包命令

- /etc/apt/sources.list——软件配置文件
- /var/lib/apt/list/*——服务器资源列表存放位置
- /var/cache/apt/archives——本地软件缓存目录



- 安装软件

```bash
sudo apt-get install xxx
```

- 中途安装失败，重新安装

```bash
sudo apt-get install xxx --reinstall
```

- 不完全卸载

```bash
sudo apt-get remove xxx
```

- 完全卸载

```bash
sudo apt-get --purge remove xxx
```

- 清理软件包缓冲区(var/cache/apt/archives)

```bash
sudo apt-get clean
```

- 保留最新版本软件包，多于版本全部清除

```bash
sudo apt-get autoclean
```

- 获取软件包详细信息

```bash
apt-cache show xxx
```

- 获取软件包的安装状态

```bash
apt-cache policy xxx
```

- 获取某个软件包依赖于哪些软件包

```bash
apt-cache depends xxx

```

- 获取某个软件包被哪些软件包所依赖

```bash
apt-cache rdepends xxx

```

## shell

### 1.shell是一个命令行解释器

- Bourne Shell（简称sh）：它是Unix的第一个shell程序，早已成为工业标准。目前几乎所有的Linux系统都支持它。不过Bourne Shell的作业控制功能薄弱，且不支持别名与历史记录等功能。
- CShell（简称csh）
- Korn Shell（简称ksh）
- Bourne Again Shell：能够提供环境变量以配置用户Shell环境，支持历史记录，内置算术功能，支持通配符表达式，将常用命令内置简化。

### 2.补齐命令与文件名

- 在使用Shell命令时，很多用户会经常遇到命令或文件名没有记全的情况。Bash Shell的命令和文件名补齐功能会帮助用户。在输入命令或文件名的前几个字符后，按TAB键或ESC键自动补齐剩余没有输入的字符串。
- 如果存在多个命令或文件有相同前缀，shell将列出所有相同前缀的命令或文件。shell给出的提示信息，帮助用户回忆和完成输入。之后等待用户输入足够的字符。
- 需要说明的是，连续按两下TAB键或ESC键，用于命令补齐；按下一次TAB键，用于文件名补齐。



### 3.查询命令历史

- 用户在Shell下的操作是有很太连续性的，曾经输入的命令可能需要多次使用。当用户在操作中发现问题，需要查看曾经执行过的操作。Bash将用户曾经键入的命令序列保存在一个命令历史表中。按“个”键和“！”键，便可查询命令历史。

- Bash Shell还提供了history命令。该命令将命令历史表按列表形式，从记录号1开始，一次性全部显示出来。

  ```bash
  history [numberine]
  
  ```

  ​		

- 显然history只能记录有限条的历史命令，默认保留500条命令。

- Bash Shell将历史命令容量保存在环境变量HISTSIZE中。

  - 使用“echo_SHISTSIZE”查看当前历史命令容量；

  - 通过直接赋值的方法，修改这个环境变量。

    ```bash
    linux@ubuntu:-S echo SHISTSIZE#显示历史命令容量500
    linux@ubuntu:-S HISTSIZE=1000#修改历史命令容量
    
    linux@ubuntu：～S echo SHISTSIZE
    1000
    
    ```

    

### 4.通配符

- 当需要用命令处理一组文件，例如filel.txt、file2.txt、file3.txt…，用户不必一一输入文件名，可以使用she11通配符。

  ![1594716534544](C:\Users\15476\AppData\Roaming\Typora\typora-user-images\1594716534544.png)

### 5.管道

- 管道可以把一系列命令连接起来，意味着第一个命令的输出将作为第二个命令的输入，通过管道传递给第二个命令，第二个命令的输出又将作为第三个命令的输入，以此类推。就像通过使用“|”符连成了一个管道。

  ```bash
  linux@ubuntu：~$ ls/usr/bin | wc -w
  
  ```

  以上操作中，借助管道“|"，将ls的输出直接作为wc命令的输入。使用管道可以巧妙的将一些命令联合使用，得到单个命令所无法实现的效果。例如使用以上的命令组合，得到的是/usr/bin目录下文件的个数。

  

### 6.输入/输出重定向

- 输入/输出重定向是改变shell命令或程序默认的标准输入/输出目标，重新定向到新的目标。
- Linux中默认的标准输入定义为键盘，标准输出定义为终端窗口。
- 用户可以为当前操作改变输入或输出，迫使某个特定命令的输入或输出来源为外部文件。

![1594717254263](C:\Users\15476\AppData\Roaming\Typora\typora-user-images\1594717254263.png)



### 7.命令置换

命令替换是将一个命令的输出作为另一个命令的参数。命令格式如下所示。

- 其中，命令command2的输出将作为命令command1的参数。需要注意，命令置换的单引号为ESC键下方的“ ` ”键

  ```bash
  command1 `command2`
  
  ```

  

- pwd命令用于显示当前目录的绝对路径。在上面的命令行中，使用命令置换符，将pwd的运行结果作为ls命令的参数。最终，命令执行结果是显示当前目录的文件内容。

  ```bash
  linux@ubuntu：~$ ls `pwd`
  Desktop Examples historycommandlist mywork
  
  ```

  

### 8.获取联机帮助

- man

  - 使用man命令可以找到特定的联机帮助页，并提供简短的命令说明。一般语法格式

    ```bash
    man commandname
    
    ```

  - 联机帮助页提供了指定命令commandname的相关信息，包括：名称、函数、语法以及可选参数描述等。无论帮助有多长，都遵循这个格式显示。在页面很多的情况下使用PageUp和PageDown键翻页。最后，使用“：q”退出帮助页面。

### 9.基本系统维护命令

- passwd

  - 出于系统安全考虑，Linux系统中的每一个帐号都必须同时具备用户名和密码。
  - 可以使用passwd命令，为已有账户重新修改用户口令。
  - 需要说明的是，超级用户root可以修改所有其他用户的口令，而普通用户只能修改自己的用户口令，如果确要修改超级用户或其他用户口令的话，需要具有超级用户的权限。
  - passwd命令的一般语法格式为：

  ```bash
  passwd username
  
  ```

  

- su

  - su命令用于临时改变用户身份，具有其他用户的权限。普通用户可以使用su命令临时具有超级用户的权限；超级用户也可以使用普通用户身份完成一些操作。当需要放弃当前用户身份，可以使用exit命令切换回来。su命令的一般语法格式为：

  ```bash
  su[-c|-m-]username
  
  ```

  - 选项“-c”表示执行一个命令后就结束；-m表示仍保留环境变量不变；-表示转换用户身份时，同时使用该用户的环境。

- echo

  - echo命令用于在标准输出一—显示器上显示一段文字，一般起到提示作用。echo命令的一般语法格式为：

  ```bash
  echo [-n] information
  
  ```

  - 选项-n表示输出文字后不换行。提示信息字符串可以加引号，也可以不加。

  ```bash
  linux@ubuntu:-Secho"Hello everyone."#输入信息字符串使用引号Hello everyone.
  linux@ubuntur-S echo Hello everyone.#输入信息字符串不使用引号，字符串之间用一个空格隔Hello everyone.
  
  ```

  

- date

  - date命令用于显示和设置系统日期和时间。date命令的一般语法格式为：

  ```bash
  date [-d|-s-u] datestr
  
  ```

  - 选项-s表示按照datestr日期显示格式设置日期；单独使用date命令，用于显示系统时钟中当前日期。时间的格式为：“hh:mm:ss”，日期格式为：“mm/dd/yy”。

  ```bash
  linux@ubuntu:-$ date#查看当前时间2007年09月16日星期日18：44：45 CST linux@ubuntu:-S sudo date-s 1：19：18#设置新时间，需要系统管理员权限Password：katag
  2007年09月16日星期日01：19：18CST
  
  ```



- clear

  - clear命令用于清除屏幕上的信息。清屏后，se11命令提示符移动到屏幕左上角。
  - clear命令的一般语法格式为：

  ```bah
  clear				ctrl+l
  
  ```

  - 由于shell命令是逐行执行，执行结果也将随即显示。因此，用户在使用命令终端窗口时，终端窗口会很快就会被字符占满。clear可以帮助清理一下窗口中杂乱的字符显示。



- df

  - df命令用于查看磁盘空间的使用情况。查看磁盘空间是用户应当经常做的事情，因为谁也不希望看到根或/var分区在不经意间填满，以便及时清理。df命令的一般格式为：

  ```bash
  df[-al-T|-h|-k]Filesystem
  
  ```

  - 其中，参数Filesystem表示物理文件系统。各选项的含义如表所示。

    ![1594728937481](C:\Users\15476\AppData\Roaming\Typora\typora-user-images\1594728937481.png)

## 用户管理

### 1./etc/passwd文件

/etc/passwd文件是系统能够识别的用户清单。用户登陆时，系统查询这个文件，确定用户的UID并验证用户口令

- 登陆名
- 经过加密的口令
- UID
- 默认的GID
- 个人信息
- 主目录
- 登陆shell

### 2./etc/group文件

- 包含了UNIX组的名称和每个组中成员列表
- 每一行代表一个组，包括4个字段：
  - 组名
  - 加密的口令
  - GID号
  - 成员列表，彼此用逗号隔开

### 3.添加用户

- adduser
  语法：adduser  <username>
  实例：

  ```bash
  #adduser newuser
  
  ```

- 添加用户名为newuser的新用户

### 4.添加新用户的过程

- 系统
  - 编辑passwd和shadow文件，定义用户帐号
  - 设置一个初始口令
  - 创建用户主目录，用chown和chmod命令改变主目录的属主和属性
- 为用户所进行的步骤
  - 将默认的启动文件复制到用户主目录中
  - 设置用户的邮件主目录并建立邮件别名

### 5.修改用户属性

- usermod

- 语法：

  ```bash
  usermod [-u uid [-o]][-g group][-G gropup,…]
  d home [-m]][-s shel1][-c comment]
  [-1 new name][-f inactive][-e expirer
  [-p passwd][-LI-U] name
  
  ```

  

- 举例用户oldname改名为newname，注意要同时更改家目录：

  ```bash
  usermod -d/home/newname-m -1 newname oldname
  
  ```

  

### 6.删除用户

- deluser
  语法：deluser<username〉
  使用方法：

  ```bash
  deluser--remove-home userl
  
  ```

- 删除用户user1的同时删除用户的工作目录



### 7.添加用户组

- addgroup
  语法：addgroup groupname.
  使用方法：

  ```bash
  addgroup groupname
  
  ```

  

## 进程

### 1.编译程序上的两个进程

​		程序的一次执行就是一个进程

​	![1594730495721](C:\Users\15476\AppData\Roaming\Typora\typora-user-images\1594730495721.png)



### 2.ps命令

- 显示进程（process）的动态
- 语法：
      ps[options]
- 常见的参数：
  - -A列出所有的进程
  - -w显示加宽可以显示较多的资讯
  - -au显示较详细的资讯
  - -aux显示所有包含其他使用者的进程

### 3.进程的状态标志

- R：正在执行中
- S：塞状态
- T：暂停我行
- Z：不存在但暂时无法消除
- D：不可中断的静止
- 〈：高优先级的进程
- N：低优先级的进程
- L：有内存分页分配并锁在内存中



### 4.top命令

- 监视进程
- 通常会全屏显示，而且会随着进程状态的变化不断更新
- 整个系统的信息也会显示，为查找问题提供了便利
- 可以显示系统总共有多少CPU和内存资源以及负载平衡等信息。



### 5.pstree命令

- 将所有行程以树状图显示，树状图将会以pid（如果有指定）或是以init这个基本进程为根，如果有指定使用者id，则树状图会只显示该使用者所拥有的进程。



### 6.终止进程

- 使用kill命令终止进程
  - kill[-signal]PID 
  - signal是信号，PID是进程号
    kill命令向指定的进程发出一个信号signal，在默认的情况下，kill命令向指定进程发出信号15，正常情况下，将杀死那些不捕捉或不忽略这个信号的进程



## Linux文件系统

### 1.概念

- 在任何一个操作系统中，文件系统无疑是其最重要的组件，用于组织和管理计算机存储设备上的大量文件，并提供用户交互接口。Linux同样具备完善的文件系统。用户既可以使用界面友好的Nautilus图形文件管理器，也可以使用功能强大的shell文件系统管理工具。

### 2.文件系统类型

- linux是一种兼容性很高的操作系统，支持的文件系统格式很多，大体可分以下几类：
  - 磁盘文件系统：指本地主机中实际可以访问到的文件系统，包括硬盘、CD-ROM、DVD、USB存储器、磁盘阵列等。常见文件系统格式有：autofs、coda、Ext（Extended File sytem，扩展文件系统）、Ext3、Ext4、VFAT、IS09660（通常是CD-ROM）、UFS（Unix File System，Unix文件系统）、FAT、FAT16、FAT32、NTFS等；
  - 网络文件系统：是可以远程访问的文件系统，这种文件系统在服务器端仍是本地的磁盘文件系统，客户机通过网络远程访问数据。常见文件系统格式有：NFS、Samba等；
  - 专有/虚拟文件系统：不驻留在磁盘上的文件系统。常见格式有：TMPFS（临时文件系统）、PROCFS（Process File System，进程文件系统）和LOOPBACKFS（Loopback File System，回送文件系统）。
- 目前Ext4是Linux系统广泛使用的一种文件格式。在Ext3基础上，对有效性保护、数据完整性、数据访问速度、向下兼容性等方面做了改进。
- 最大特点是日志文件系统：可将整个磁盘的写入动作完整地记录在磁盘的某个区域上，以便在必要时回溯追踪。。

### 3.SCSI与IDE设备命名

- sata硬盘的设备名称是“/dev/sda”
  - /dev/sdal含义？-/dev/sdb3含义？
  - IDE硬盘的设备名称是“/dev/hda”
  - /dev/hdc2含义？
- 如果很在意系统的高性能和稳定性，应该使用SCSI硬盘
  - cat/proc/partitions



### 4.Linux分区的命名方式

- 字母和数字相结合
- 前两个字母表示设备类型
  - “hd”代表IDE硬盘
  - “sd”表示SCSI或SATA硬盘
- 第三个字母说明具体的设备
  - “/dev/hda”表示第一个IDE硬盘
  - “/dev/hdb”表示第二个IDE硬盘

### 5.SCSI与IDE设备命名

- sata硬盘的设备名称是“/dev/sda”
  - /dev/sdal含义？.
  - /dev/sdb3含义？
- IDE硬盘的设备名称是“/dev/hda”
  - /dev/hdc2含义？
- 如果很在意系统的高性能和稳定性，应该使用SCSI硬盘
  - cat/proc/partitions

### 6.交换分区

- 将内存中的内容写入硬盘或从硬盘中读出，称为内存交换（swapping）
- 交换分区最小必须等于计算机的内存
- 可以创建多于一个的交换分区
- 尽量把交换分区放在硬盘驱动器的起始位置



### 7.文件系统逻辑结构

- 某所大学的学生可能在一两万人左右，通常将学生分配在以学院-系-班为单位的分层组织机构中。若需要查找一名学生时，最笨的办法是依次问询大学中的每一个学生，直到找到为止。如果按照从学院、到系、再到班的层次查询下去，必然可以找到该学生，且查询效率高。这种树形的分层结构就提供了一种自顶向下的查询方法。
- 如果把学生看作文件，院-系-班的组织结构看作是Linux文件目录结构，那么就同样可以有效地管理数量庞大的文件。
- 一直使用微软Windows操作系统的用户似乎已经习惯了将硬盘上的几个分区，并用A:、B:、C:、D：等符号标识。存取文件时一定要清楚存放在哪个磁盘的哪个目录下。
- Linux的文件组织模式犹如一颗倒置的树，这与Windows文件系统有很大差别。所有存储设备作为这颗树的一个子目录。存取文件时只需确定目录就可以了，无需考虑物理存储位置。



### 8.文件系统结构

- 分区与目录的关系：
  - 在Windows下，目录结构属于分区；在Linux下，分区属于目录结构。
- 如何知道文件存储的具体硬件位置呢？
  - 在Linux中，将所有硬件都视为文件来处理，包括硬盘分区、CD-ROM、软驱以及其他USB移动设备等。为了能够按照统一的方式和方法访问文件资源，Linux中提供了对每种硬件设备相应的设备文件。一旦Linux系统可以访问到硬件，就将其上的文件系统挂载到目录树中的一个子目录中。
  - 例如，用户插入USB移动存储器，Ubuntu Linux自动识别后，将其挂载到
    “/media/disk”目录下。而不象Windows系统将USB存储器作为新驱动器，表示为
    “F:”盘。



### 9.file命令

- 在Linux文件系统中，文件扩展名不总是被使用或被一致地使用。如果一个文件没有扩展名，或者文件与其扩展名不时怎么办呢？file命令功能用于判定一个文件的类型。
  file命令一般语法格式为：

  ```bash
  file[filename]
  
  ```

  

- 其中filename是文件名。命令的输出将显示该文件是二进制文件、文本文件、目录文件、设备文件，还是Linux中其他类型的文件。

  ```bash
  linux@ubuntu:-S file/usr/games/banner banner:ELF 32-bit LSB executable，Intel 80386，version 1（SYSV），for GNU/Linux 2.6.0，dymamically linked（uses shared libs），stripped 
  linux@ubuntu：～S file Textfile.txt Textfile.txt:UTF-8 Unicode text
  
  ```

  

### 10.mkdir命令

- 用于创建一个目录。mkdir命令一般语法格式为：

  ```bash
  mkdir[-p]directory_name
  
  ```

- 其中，directory_name为要创建的目录名，并且不能是已有的目录，通常不允许嵌套创建子目录。

- 使用选项“-p”表示可以嵌套创建子目录，即多层目录。

- 需要说明的是，创建目录的用户在工作目录应具有写入权限。假设要创建下面这样结构的目录。

  ```bash
  dir1
  dir1/dir2
  dir1/dir2/dir3
  
  ```

  

### 11.创建链接文件

- Linux中有两种类型的链接：

  - 硬链接是利用Linux中为每个文件分配的物理编号——inode建立链接。因此，硬链接不能跨越文件系统。
  - 软链接（符号链接）是利用文件的路径名建立链接。通常建立软链接使用绝对路径而不是相对路径，以最大限度增加可移植性。

- ln命令

  - 命令可以用于创建文件的链接文件。1n命令一般语法格式为：

    ```bash
    ln[-s]target link_name
    
    ```

    

  - 其中，选项“-s”表示为创建软链接。在缺省情况下，创建硬链接。参数target为目标文件，1ink name为链接文件名。如果链接文件名已经存在但不是目录，将不做链接。目标文件可以是任何一个文件名，也可以是一个目录。

    ```bash
    linux@ubuntu:-S In-s/proc/cpuinfo mycpuinfo linux@ubuntu:-S Is-1 mycpuinfo wxrwxrwx 1 wdl wdl 13 2007-09-22 00：43mycpuinfo->/proc/cpuinfo
    
    ```

    

### 12.文件压缩和归档

- 用户在进行数据备份时，需要把若干文件整合为一个文件以便保存。尽管整合为一个文件进行管理，但文件大小仍然没变。若需要网络传输文件时，就希望将其压缩成较小的文件，以节省在网络传输的时间。因此本节介绍文件的归档与压缩。

- 归档文件是将一组文件或目录保存在一个文件中。

- 压缩文件也是将一组文件或目录保存一个文件中，并按照某种存储格式保存在磁盘上，所占磁盘空间比其中所有文件总和要少。

  - 归档文件仍是没有经过压缩的，它所使用的磁盘空间仍等于其所有文件的总和。因而，用户可以将归档文件再进行压缩，使其容量更小。
  - gzip是Linux中最流行的压缩工具，具有很好的移植性，可在很多不同架构的系统中使用。bzip2在性能上优于gzip，提供了最大限度的压缩比率。如果用户需要经常在Linux和微软

- gzip与gunzip命令

  - 与zip明显区别在于只能压缩一个文件，无法将多个文件压缩为一个文件。
    gzip命令符号模式的一般语法格式为：

  - 其中，filename表示要压缩的文件名，gzip会自动在这个文件名后添加扩展名为.gz，作为压缩文件的文件名。

    ```BASH
    gzip[-l|-d|-num]filename
    
    ```

    ![1594783220660](C:\Users\15476\AppData\Roaming\Typora\typora-user-images\1594783220660.png)

  - gunzip命令符号模式的一般语法格式为：

    ```bash
    gunzip [-f]file.gz
    
    ```

    

