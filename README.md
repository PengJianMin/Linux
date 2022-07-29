# Linux
+ [计算机概论](https://github.com/PengJianMin/Linux/edit/main/README.md#%E8%AE%A1%E7%AE%97%E6%9C%BA%E6%A6%82%E8%AE%BA)
+ [Linux思想](https://github.com/PengJianMin/Linux/edit/main/README.md#linux%E6%80%9D%E6%83%B3)
+ [磁盘分区](https://github.com/PengJianMin/Linux/edit/main/README.md#%E7%A3%81%E7%9B%98%E5%88%86%E5%8C%BA)
+ [基础操作](https://github.com/PengJianMin/Linux/edit/main/README.md#%E5%9F%BA%E7%A1%80%E6%93%8D%E4%BD%9C)
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
2. 代表一次可以在内存寻址的范围：32位 ==> 2^32 ==> 2^2 * 2^10 * 2^10 * 2^10 ==> 4G, 32位的CPU最多只能支持4G的内存，多了没用。
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
