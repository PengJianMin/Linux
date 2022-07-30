# Linux

# 计算机概论
+ 文件大小使用**二进制**，速度单位使用**十进制**
1. 文件大小：1 KB = 1024 B = 2^10 B
2. 速度单位：1 Mbit/s = 1*1000*1000 bit/s
+ CPU 外频和倍频
1. **外频**：cpu与外部组件进行数据传输/运算时的速度。
2. **倍频**：CPU内部用来加速工作性能的一个**倍数**。
3. CPU频率 = 外频 * 内频
+ 32位和64位
1. 术语叫**字组大小**
2. 代表一次可以在内存寻址的范围：32位 ➡️  2^32 ➡️  2^2 * 2^10 * 2^10 * 2^10 ➡️  4G, 32位的CPU最多只能支持4G的内存，多了没用。
+ CMOS和BIOS
1. CMOS类似内存，是**存储器**，需要有电源支持，主要纪录主板上面的重要参数（系统时间、CPU电压与频率、各项设备的I/O地址与IRQ等）
2. BIOS是**程序**，加载CMOS中的参数，调用存储设备中的开机程序，进入操作系统中。
+ 系统调用
1. 应用程序和操作系统内核之间的接口，使得应用内程序可以在内核上运行。
2. 根据某一系统调用开发的应用程序无法在其他操作系统上运行。（Linux和Windows软件区别）
+ 驱动程序
1. 操作系统提供接口给硬件开发商，开发商要去实现这些接口开发驱动程序。
2. 什么意思呢？就是说操作系统告诉硬件开放商要实现哪些接口，之后直接以接口变量的形式调用这些功能，驱动程序相当于实现了那些接口的具体类，操作系统无需关心具体类是什么，只关心有什么接口，直接调用即可。
# Linux思想
1. Linux一切皆文件。
# 磁盘分区
+ IDE接口
1. IDE接口有两个：IDE1(Primary),IDE2(Secondary)，每个接口可以连接2个IDE设备，一共可以连接4个IDE设备。
2. 设备文件名与接口**物理位置**绑定：
    + IDE1-Primary(Master):/dev/hda
    + IDE1-Secondary(Slave) /dev/hdb
    + IDE2-Primary(Master):/dev/hdc
    + IDE2-Secondary(Slave) /dev/hdd
+ SATA接口
1. 设备文件名**以Linux内核检测到的顺序**决定，**与插槽的物理位置无关**。 如：/dev/sda;/dev/sdb...
+ 磁盘组成
1. 磁盘扇区大小固定（512Bytes）
2. 整块磁盘第一块扇区纪录了两个重要信息
    + 主引导分区（Master Boot Record,MBR）,可以存储**引导加载程序**，有446bytes。**系统开机的时候会主动去读取这个区块的内容**
    + 分区表，纪录整块硬盘分区的状态，有64bytes。
+ 磁盘分区表
1. 设备文件名后会再接一个数字，这个数字表示了分区位置（/dev/hda1）
2. “分区”是对64bytes的分区表进行设置
3. 分区表仅能写入**4组**分区信息(主分区Primary与扩展分区Extended一共最多有4个，扩展分区最多占其中1个)
4. 逻辑分区是由扩展分区持续切割出来的分区。**逻辑分区只能从5号开始标识（/dev/hda5）**，哪怕2、3、4号都没有被占用。
5. 分区的最小单位是柱面（cylinder），一个或多个柱面组成一个分区。
6. IDE硬盘最多有59个逻辑分区（5号到63号），SATA硬盘最多有11个逻辑分区（5号到15号）
+ 开机流程与主引导分区(MBR)
1. BIOS：开机主动执行的韧体，会认识**第一个可开机的设备**
2. MBR：第一个可开机设备的第一个扇区的主引导分区块，内含**引导加载程序（Boot loader）**
3. **引导加载程序（Boot loader）**：一支可读取内核文件来执行的**软件**。
4. 内核文件：开始操作系统的功能。
+ 多重引导（Linux/Windows双系统）
1. 引导加载程序可以将引导功能转交给其他loader负责（boot sector）
2. MBR中的引导加载程序可以提供两个菜单：一个直接加载Windows内核文件，一个是将引导加载工作交给**另一个分区的启动扇区（boot sector）**。
3. 选择第二个菜单时，引导加载工作就交个另一个分区的引导加载程序。
4. 总结
    + 每个分区都拥有自己的启动扇区（boot sector）
    + 实际可开机的内核文件是存放在各分区的
    + loader只会认识自己的系统分区内的可开机内核文件和其他loader
    + loader可直接指向或者是间接将管理权转交给另一个管理程序
5. 如果要安装多重引导，最好先安装Windows再安装Linux：Windows在安装的时候，安装程序会主动覆盖掉MBR以及自己所在分区的启动扇区。Linux则允许在Linux的boot loader里面加入Windows选项。
+ 文件系统与目录树的关系（**挂载**）
1. 挂载是利用一个目录设置一个**进入点**：通过这个进入点进入这个磁盘分区，磁盘分区的数据放置在该目录下。
2. **partition1**挂载在根目录/，**partition2**挂载在/home。所以/home内各**次目录**的数据都是放在partition2的，如果不是放在/home下面的目录，则数据放在partition1。
3. **挂载只对应目录**，不对应文件。
# 基础操作
+ 显示日期的命令：date
1. date +%Y/%m/%d 
2. date +%H:%M
+ 重要的热键
1. [Tab]  命令补全，文件补齐
2. [Ctrl]-c 终端目前程序的按键
3. [Ctrl]-d 键盘输入结束（End Of File 或 End Of Input）
+ 在线求助 man命令
1. man 7 ${command} 获得详细的说明
2. 向下翻页：空格键、[Page Down]
3. 向上翻页：[Page Up]
4.  去到第一页：[Home]
5.  去到最后一页：[End]
6.  向下查询string字符串：/string；用n键继续字符串的下一个查询
7.  向上查询string字符串：?string；用N键继续字符串的上一个查询
8.  退出：q
+ 正确关机
1. 数据同步写入磁盘：sync；将内存尚未被更新的数据写入硬盘，系统关机或重启之前最好多执行几次
2. 重启、关机命令
    + 以下命令在执行前都会进行sync命令的调用
    + `sync;sync;sync;reboot`
    + `shutdown -h now`
    + `poweroff -f`
3. 切换执行等级init
    + Linux**系统运作的模式**共有7种
        + run level 0:关机
        + run level 3：纯命令行模式
        + run level 5：含有图形界面模式
        + run level 6：重启
    + 关机命令 `init 0`
# Linux的文件权限与目录配置
1. /etc/passwd：系统上的所有账号、一般身份用户和root用户的相关信息
2. /etc/shadow：个人的密码
3. /etc/group：Linux所有的组名
4. list查看文件信息
    + 第一列代表文件的类型与权限
        + [d]目录、[-]文件、[l]连接文件、[b]块存储设备、[c]串行端口设备，如键盘鼠标
        + [r]可读、[w]可写、[x]可执行
        + 3个一组，第一组为**文件所有者的权限**，第二组为**同属一个用户组的权限**，第三组为**其他非本用户组的权限**
    + 第二列表示有多少文件名连接到此节点（i-node）
        + i-node纪录文件的权限和属性，一个i-node可以纪录多个不同文件名。
        + 这个数字表明有多少不同的文件名连接到相同的一个i-node号码
    + 第三列表示这个文件（或目录）的“所有者”账号名
    + 第四列表示这个文件的所属用户组名
    + 第五列表示这个文件的**容量**大小（**能容纳的数据量**），默认单位为B。
    + 第六列表示文件的创建日期或最新一次的修改日期。（`ls -l --full-time`）
    + 第七列为该文件名
5. 改变文件属性与权限
    + chgrp：改变文件所属用户组， -R 进行递归更改，连同子目录下所有文件、目录
    + chown：改变文件所有者，-R 同上
    + chmod：改变权限
        + r:4
        + w:2
        + x:1
        + u（user）、g（group）、o（others）、a（all）
        + +（加入）、-（除去）、=（设置）
6. 文件权限与目录权限的关系
    + 拥有对**文件**的写权限(w)并**不具备删除**该文件的权限。rwx都是针对**文件内容**而言。
    + 拥有对**目录**的写权限(w)表明可以**更改目录结构**
        + **可以删除**该目录下的文件或目录（不论该文件的权限为何）
        + 新建新的文件与目录
        + 将已存在的文件或目录重命名
        + 转移该目录内的文件、目录位置
    + 拥有对**目录**的执行权限(x)表明**用户可以进入该目录成为工作目录**，即可以**使用`cd`命令进入**。

7. Linux亩配置**标准**：FHS
    + /usr 软件放置处
    + /etc 配置文件
    + /lib 执行文件所需的函数库与内核所需的模块
    + /boot 开机与内核文件
    + /dev 设备文件
    + /proc 虚拟文件系统，表示内存数据
    + /sys 虚拟文件系统，记录与内核相关的信息
    + /sbin /bin 重要执行文件
8. 网络上的文件系统也可以挂载本地目录，例如：NFS服务
9. 绝对路径与相对路径
    + 绝对路径：由根目录(/)开头的路径
    + 相对路径：以当前所在路径的相对位置来表示
        + `.` :表示当前目录，同 `./`
        + `..` :表示上一层目录，同 `../`
# Linux文件与目录管理
1. 特殊目录
    + .  代表当前目录 
    + .. 代表上一层目录
    + \-  代表前一个**工作目录**（**执行`cd`命令前的目录**）
    + ~  代表**目前用户身份**所在的**主文件夹**
    + ~account 代表**account**这个用户所的**主文件夹**
2. 常见目录处理命令
    + cd：切换目录
    + pwd：显示当前目录
    + mkdir：新建一个新的目录
        + -p : 自动创建不存在的目录 mkdir -p /home/user1/test1 
    + rmdir：删除一个**空**的目录（即目录下有文件就执行不了）
3. 执行文件路径的变量：**$PATH**
    + 执行命令时，系统会依照PATH的设置去**每个PATH定义的目录**下查询文件名为该命令的可执行文件，如果在PATH定义的目录中含有多个相同名字的可执行文件，那么**先查询到的同名命令先被执行**。
    + PATH（**一定是大写**），变量内容是一堆目录，每个目录用冒号（:）隔开，每个目录是有**顺序**之分的。
    + 安全起见，不建议将 . 加入PATH的查询目录中。
4. 文件与目录管理
    + ls：查看文件与目录 `ls -al` `ll` `ls --full-time` `ls --time=atime` `ls --time=ctime`
        + \-a: 显示全部文件，连同隐藏文件（开头为 . 的文件）。
        + \-d：仅列出目录
        + \-l：列出文件属性与权限等数据
        + \-r：排序结果反向输出
        + \-R：子目录递归输出
        + \-S：以文件**容量**大小排序
        + \-t：以时间排序
    + cp：复制文件 `cp -a source destination`
        + 复制文件需要有**read权限**
        + 默认条件中，cp的源文件与目的文件的**权限是不同的**，目的文件的**所有者**通常会是命令操作者本身。
        + \-a：等于 \-pdr
        + \-d：若源文件为连接文件，则复制连接文件属性而非文件本身
        + \-p：连同文件的属性一起复制过去
        + \-r：递归持续复制         
    + 软连接与硬链接（更详细信息见后续相关章节）
        + 软连接（symbolic link）相当与快捷方式，直接删除不影响源文件。
        + 硬链接（hard link）相当与直接关联源文件的存储区块，本质上关联与源文件相同的i-node（所以权限参数中会有i-node关联数），直接删除会影响源文件。
    + rm：移除文件或目录 `rm -f` `rm -rf` 
        + \-f：强制删除force
        + \-r：递归删除
    + mv：移动文件与目录，或**更名** `mv old new`
        + rename同样可以更名
    + basename：取得路径的文件名与目录名称 `basename path` `dirname path`
        + basename 取得路径的最后一项 basename /etc/sysconfig/network  ➡️  network
        + dirname 除去路径的最后一项剩下的 dirname /etc/sysconfig/network ➡️  /etc/sysconfig
        + 一般在写程序的时候使用
5. 文件**内容**查阅
    + cat：由第一行开始显示内容 `cat -n` `cat -b` `cat -E` `cat -A` 
        + \-n：显示行号，空白行也标行号
        + \-b：显示行号，空白行不标行号
        + \-E：将结尾的断行字符$显示出来
        + \-A：等于 \-vET
        + \-v：列出一些看不出来的特殊字符
        + \-T：将[Tab]键以 ^I 显示出来
    + more：翻页查看（**只能向后**）
        + 空格键（Space）：向下翻**一页**
        + Enter：向下滚动**一行**
        + /string：查询字符串关键字，n键向下继续查询
        + \:f：显示文件名和行数
        + q：退出
        + b或[Ctrl]-b：往回翻页
    + less：翻页查看（**支持向前向后**）
        + 空格键（Space）/[PageDown]：向下翻**一页**
        + [PageUp]：向上翻一页
        + /string：**向下**查询字符串关键字
        + ?string：**向上**查询字符串关键字
        + n：重复前一个查询（与/或?定下的方向相关）
        + N：**反向**前一个查询（与/或?定下的方向相关）
        + q：退出
6. 数据选取
    + head：取出前面几行 `head -n 100` `head -n -100`
        + **负数**指**扣掉**文件*末尾*的100行，只取剩下的前面的所有数据行。  
    + tail：取出后面几行 `tail -n 100` `tail -n +100` `tail -f log.txt`
        + **正数**指第100行**以后**的所有数据
        + \-f：监测日志文件，**常用于查看是否有请求打进来**。
    + od：非纯文本文件（如二进制文件binary） `od -t c /usr/bin/passwd`
7. 文件时间
    + mtime：内容数据更改时间
    + ctime：文件状态（权限、属性等等）更改时间
    + atime：文件内容被取用时间，读取时间。（cat命令会更新这个时间） 
    + touch：修改文件时间或**创建新文件** `touch newfile.txt` `touch -a` `touch -c` `touch -m` 
8. 文件与目录的**默认权限**与**隐藏属性**
    + chattr设置，lsattr查看，只在**Ext2/Ext3**的文件系统上生效
    + umask：设置文件默认权限 `umask 022`
        + 文件默认权限 rw-rw-rw- 666
        + 目录默认权限 rwxrwxrwx 777
        + umask指的是默认值需要**减掉**的权限
        + 新建文件：rw-rw-rw-(666) **-** ----w--w-(022) ➡️ rw-r--r--(644)
        + 新建目录：rwxrwxrwx(777) **-** ----w--w-(022) ➡️ rwxr-xr-x(755)
    + chattr：设置文件的隐藏属性（**很多只能是root才能设置**）`chattr +a` ` chattr -a` `chattr +i` `chattr -i`
        + a 文件只能增加数据，不能删除和修改数据
        + i 文件不能删除、改名、设置连接、修改数据等等，直接锁死
9. 文件特殊权限
    + Set UID 4
        + 仅对**二进制程序**有效
        + **s**标志出现在文件**所有者**的**x权限**上
        + **非文件所有者**对该文件拥有**x权限**
        + 非文件所有者执行该文件时（run-time）将拥有文件所有者的权限。**s有share权限的意味**
    + Set GID 2
        + 仅对**二进制程序**有效
        + **s**标志出现在文件**文件所属用户组**的**x权限**上
        + **非文件所有者**对该文件拥有**x权限**
        + 非文件所有者执行该文件时（run-time）将获得**文件所属用户组的支持**。**s有share权限的意味**
