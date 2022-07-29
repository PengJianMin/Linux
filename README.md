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
3. 分区表仅能写入**4组**分区信息(主分区与扩展分区最多有4个，扩展分区最多有1个)
4. 4组分区信息分为主（Primary）和扩展（Extended）分区
5. 逻辑分区是由扩展分区持续切割出来的分区。**逻辑分区只能从5号开始标识（/dev/hda5）**，哪怕2、3、4号都没有被占用。
6. 分区的最小单位是柱面（cylinder）
7. IDE硬盘最多有59个逻辑分区（5号到63号），SATA硬盘最多有11个逻辑分区（5号到15号）
