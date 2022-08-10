# Linux 基础使用
# Vim程序编辑器
+ vim有3种模式：
1. 一般模式：vim打开文件时**默认**进入的模式，无法编辑，可以**移动光标**，主要进行删除、复制、粘贴数据。
2. 编辑模式
    + 按下“i，I，o，O，a，A，r，R”等任意字母进入
    + 界面左下方出现INSERT或REPLACE字样才可以编辑
    + 可按下[ESC]按键**退出编辑模式**，进入一般模式
3. 命令行模式
    + 输入“:”、“/”、“?”中任何一个按钮进入
    + 可以进行查找数据，读取、保存、大量替换字符，显示行号，离开vim等操作
+ **一般模式**下的常用操作
1. 移动光标
    + 向下移动1页：`[Ctrl]+[f]`或`[Page Down]`
    + 向上移动1页：`[Ctrl]+[b]`或`[Page Up]`
    + 向下移动**n行**：`nj`或`n↓`或`n[Enter]` 如`30j`或`30↓`
    + 光标**向后**移动n个**字符**距离：`n<space>` 按下数字后再按**空格键**
    + 移动到这行**最前面**字符处：`0`或`功能键[Home]`
    + 移动到这行**最后面**字符处：`$`或`功能键[END]`
    + 移动到这个**文件**的**最后一行**：`G`
    + 移动到这个**文件**的**第一行**：`gg`
    + 移动到这个**文件**的**第n行**：`nG` `20G` 配合 `:set nu`使用
2. 查找和替换字符
    + 向下查找**一次**：`/word`
    + **向上**查找**一次**：`?word`
    + 重复**前一个**查找的动作，前一个是向上就**继续**向上，前一个是向下就**继续**向下：`n`
    + 和n相反，前一个是向上就**反向为**向下，前一个是向下就**反向为**向上：`N`
    + 在**第**n1行和**第**n2行之间寻找word1字符串，并将word1字符串**替换**为word2：`:n1,n2s/word1/word2/g` `:100,200s/author/Elesev/g`
    + 在**第1行**和**最后一行**之间寻找word1字符串，并将word1字符串**替换**为word2：`:1,$s/word1/word2/g` `:1,$s/author/Elesev/g`
    + 在**第1行**和**最后一行**之间寻找word1字符串，并将word1字符串**替换**为word2，且在替换前需要**用户确认（confirm）** 是否需要替换：`:1,$s/word1/word2/gc` `:1,$s/author/Elesev/gc`
 3. 删除、复制与粘贴
    + 删除
        + 向后**→**删除一个字符：`x`
        + 向后**→连续**删除n个字符：`nx` `10x`
        + 向前**←**删除一个字符：`X`
        + 删除光标**所在行**：`dd`
        + 删除**包含**光标所在行在内的**向下n行**：`ndd` `20dd`
        + 删除光标所在行**到第一行**的所有数据：`d1G`
        + 删除光标所在行**到最后一行**的所有数据：`dG`
        + 删除光标所在位置**到最后一个字符**的所有数据：`d$`
        + 删除光标所在位置**到第一个字符**的所有数据：`d0`
    + 复制
        + 复制光标**所在行**：`yy`
        + 复制**包含**光标所在行在内的**向下n行**：`nyy` `20yy`
        + 复制光标所在行**到第一行**的所有数据：`y1G`
        + 复制光标所在行**到最后一行**的所有数据：`yG`
        + 复制光标所在位置**到最后一个字符**的所有数据：`y$`
        + 复制光标所在位置**到第一个字符**的所有数据：`y0`
    + 粘贴
        + 将已复制的数据在光标的**下一行**粘贴 `p`
        + 将已复制的数据在光标的**上一行**粘贴 `P`
 4. 重复动作和还原
    + **重复**上一个操作：`[Ctrl]+r`或`.`
    + **复原**上一个操作：`u`
+ 一般模式**切换**到编辑模式下
1. 插入模式
    + `i`：从目前光标所在处插入
    + `I`：从目前所在行的**第一个非空格符处**开始插入
    + `a`：从目前光标所在**下一个字符**处开始插入
    + `A`：从目前光标所在行**最后一个字符**处开始插入
    + `o`：目前光标所在行的**下一行处**插入新的一行
    + `O`：目前光标所在行的**上一行处**插入新的一行
2. 替换模式
    + `r`：只会替换**光标所在的那个字符**一次
    + `R`：**一直替换**光标所在的那个字符
3. 退出编辑模式，回到一般模式 `[Esc]`
+ 命令行的保存、离开等命令（别忘记**先输入**`:`）
1. 保存
    + `:w`：将编辑的数据写入硬盘文件中，**编辑生效**
    + `:w!`：强制写入（当没有w权限时）
2. 离开vim
    + `:q`：直接离开，**之前的操作**有效
    + `:q!`：直接离开，之前的操作**无效**
    + `:wq`：离开，并且让之前的操作**生效**
3. 另存文件 
    + `:w[filename]`
    + `:n1,n2 w [filename]`：将**第**n1行到**第**n2行内容保存到filename文件
5. 读入其他文件的数据 `:r[filename]`
6. 暂时**离开vim**查看命令显示的结果，之后**可以返回**：`:!command`
+ vim环境更改
1. 行号显示
    + `:set nu`：设置行号
    + `:set nonu`：取消设置行号
+ Vim相关警告信息
1. `.${filename}.swp`文件：
    + 使用vim编辑文件时，会创建对应的**swp暂存文件**
    + 对文件的操作会被记录到swp文件中
    + 系统断线时，操作如果没有保存，swp文件可以发挥**救援作用**
+ **块选择**（Visual Block）
    + `V`：选择字符或行
    + `[Ctrl]+v`：**块选择**，可以用**长方形**方式选择数据
    + `y`：将**反白**区域复制
    + `d`:将**反白**区域删除
    + `p`：粘贴数据
+ **单窗口**多文本编辑
    + **一次打开**多个文件，但是为**单窗口**操作，其中一个文件的复制的数据在**另一个文件**可以粘贴使用
    + `vim ${file1} ${file2} ...`
    + `:n`：编辑下一个文件
    + `:N`：编辑上一个文件
    + `:files`：列出**目前这个vim**打开的所有文件
+ **多窗口**功能 `:sp${filename}`
    + 如果`${file}`**省略**，则为**同一个文件**出现在**两个窗口**
    + `[Ctrl]+w+↑` ：光标移动到上方窗口
    + `[Ctrl]+w+↓` ：光标移动到下方窗口
    + `[Ctrl]+w+q` ：结束当前窗口
+ vim环境设置与记录：`~/.vimrc` `~/.viminfo`
+ 中文编码问题 `env | grep -i LANG` `LANG=zh_CN.big5`
+ DOS与Linux**断行字符**
1. DOS断行字符：`^M$`
2. Linux断行字符：`$`
3. 在**DOS上编辑**的shell script程序文件在Linux上可能无法执行
    + `dos2UNIX` `dos2UNIX -k -n man.config man.config.linux`
    + `UNIX2dos` `UNIX2dos -k man.config`
    + `-k`：保留该文件原本的mtime时间格式
    + `-n`：保留原本的旧文件，转换后的内容输出到新文件 `dos2UNIX -n ${old} ${new}`
+ 文本**语系**编码转换
1. `iconv --list` 列出指出的语系数据       
2. `iconv -f 原本编码 -t 新编码 filename [-o newfile]`
# 认识和学习Bash
+ /etc/shells
    + 系统上**合法的**shell要写入该文件
    + 系统服务在运行过程中，会去检查**用户能够使用**的shells，就需要借助/etc/shells的内容进行判断
+ /etc/passwd 每一行最后一个字段记录了该用户**登录时**的**默认**shell
```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
···
```
+ `type`：判断**命令**是否为bash shell的**内置（builtin）** 命令
1. `type cd` builtin
2. `type docker` docker is /usr/bin/docker
+ shell的**变量**功能
1. **环境**变量
    + 环境变量通常以**大写字符**来表示，以区分**自定义**变量
    + 环境变量的**功能**
        + null
2. `$PATH` 
    + 系统通过PATH变量里面的内容所记录的**路径顺序**来查找命令
        + 如果找完PATH变量内的路径还找不到命令，则会显示"command not found"
    + 决定某个命令能否在**任何目录**下执行 
3. `echo` 变量的**显示**
    + 变量名称前加上$即可：`echo $var`
    + 变量名称用${}**包围**即可：`echo ${var}`
4. `set`和`unset` 变量的**设置**与**取消**
    + 
    







# 计算机概论
+ 文件大小使用**二进制**，速度单位使用**十进制**
1. 文件大小：1 KB = 1024 B = 2^10 B
2. 速度单位：1 Mbit/s = 1 * 1000 * 1000 bit/s
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
+ Linux一切皆文件。
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
1. 设备文件名后会再接一个**数字**，这个数字表示了**分区位置**（/dev/hda1）
2. “分区”是对64bytes的分区表进行设置
3. 分区表仅能写入**4组**分区信息(主分区Primary与扩展分区Extended一共最多有4个，扩展分区最多占其中1个)
4. 逻辑分区是由扩展分区持续切割出来的分区。**逻辑分区只能从5号开始标识（/dev/hda5）**，哪怕2、3、4号都没有被占用。
5. 分区的最小单位是柱面（cylinder），一个或多个柱面组成一个分区。
6. IDE硬盘最多有59个逻辑分区（5号到63号），SATA硬盘最多有11个逻辑分区（5号到15号）
+ 开机流程与主引导分区(MBR)
1. BIOS：开机主动执行的韧体，会认识**第一个可开机的设备**
2. MBR：第一个可开机设备的第一个扇区的主引导分区块，内含**引导加载程序（Boot loader）**
3. **引导加载程序（Boot loader）**：一支可读取内核文件来执行的**软件**，主流的boot loader是**grub**。
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
+ /etc/passwd：系统上的所有账号、一般身份用户和root用户的相关信息
+ /etc/shadow：个人的密码
+ /etc/group：Linux所有的组名
+ list查看文件信息
1. 第一列代表文件的类型与权限
    + [d]目录、[-]文件、[l]连接文件、[b]块存储设备、[c]串行端口设备，如键盘鼠标
    + [r]可读、[w]可写、[x]可执行
    + 3个一组，第一组为**文件所有者的权限**，第二组为**同属一个用户组的权限**，第三组为**其他非本用户组的权限**
2. 第二列表示有多少文件名连接到此节点（i-node）
    + i-node纪录文件的权限和属性，一个i-node可以纪录多个不同文件名。
    + 这个数字表明有多少不同的文件名连接到相同的一个i-node号码
3. 第三列表示这个文件（或目录）的“所有者”账号名
4. 第四列表示这个文件的所属用户组名
5. 第五列表示这个文件的**容量**大小（**能容纳的数据量**），默认单位为B。
6. 第六列表示文件的创建日期或最新一次的修改日期。（`ls -l --full-time`）
7. 第七列为该文件名
+ 改变文件属性与权限
1. chgrp：改变文件所属用户组， -R 进行递归更改，连同子目录下所有文件、目录
2. chown：改变文件所有者，-R 同上
3. chmod：改变权限
    + r:4
    + w:2
    + x:1
    + u（user）、g（group）、o（others）、a（all）
    + +（加入）、-（除去）、=（设置）
+ 文件权限与目录权限的关系
1. 拥有对**文件**的写权限(w)并**不具备删除**该文件的权限。rwx都是针对**文件内容**而言。
2. 拥有对**目录**的写权限(w)表明可以**更改目录结构**，意味着：
    + **可以删除**该目录下的文件或目录（不论该文件的权限为何）
    + 新建新的文件与目录
    + 将已存在的文件或目录重命名
    + 转移该目录内的文件、目录位置
3. 拥有对**目录**的执行权限(x)表明**用户可以进入该目录成为工作目录**，即可以**使用`cd`命令进入**。
+ Linux亩配置**标准**：FHS
1. /usr 软件放置处
2. /etc 配置文件
3. /lib 执行文件所需的函数库与内核所需的模块
4. /boot 开机与内核文件
5. /dev 设备文件
6. /proc 虚拟文件系统，表示内存数据
7. /sys 虚拟文件系统，记录与内核相关的信息
8. /sbin /bin 重要执行文件
+ 网络上的文件系统也可以挂载本地目录，例如：NFS服务
+ 绝对路径与相对路径
1. 绝对路径：由根目录(/)开头的路径
2. 相对路径：以当前所在路径的相对位置来表示
    + `.` :表示当前目录，同 `./`
    + `..` :表示上一层目录，同 `../`
# Linux文件与目录管理
+ 特殊目录
1. `.`  代表当前目录 
2. `..` 代表上一层目录
3. `\-`  代表前一个**工作目录**（**执行`cd`命令前的目录**）
4. `~`  代表**目前用户身份**所在的**主文件夹**
5. `~account` 代表**account**这个用户所的**主文件夹**
+ 常见目录处理命令
1. cd：切换目录
2. pwd：显示当前目录
3. mkdir：新建一个新的目录
    + -p : 自动创建不存在的目录 mkdir -p /home/user1/test1 
4. rmdir：删除一个**空**的目录（即目录下有文件就执行不了）
+ 执行文件路径的变量：**$PATH**
1. 执行命令时，系统会依照PATH的设置去**每个PATH定义的目录**下查询文件名为该命令的可执行文件，如果在PATH定义的目录中含有多个相同名字的可执行文件，那么**先查询到的同名命令先被执行**。
2. PATH（**一定是大写**），变量内容是一堆目录，每个目录用冒号（:）隔开，每个目录是有**顺序**之分的。
3. 安全起见，不建议将 . 加入PATH的查询目录中。
+ 文件与目录管理
1. ls：查看文件与目录 `ls -al` `ll` `ls --full-time` `ls --time=atime` `ls --time=ctime`
    + \-a: 显示全部文件，连同隐藏文件（开头为 . 的文件）。
    + \-d：仅列出目录
    + \-l：列出文件属性与权限等数据
    + \-r：排序结果反向输出
    + \-R：子目录递归输出
    + \-S：以文件**容量**大小排序
    + \-t：以时间排序
2. cp：复制文件 `cp -a source destination`
    + 复制文件需要有**read权限**
    + 默认条件中，cp的源文件与目的文件的**权限是不同的**，目的文件的**所有者**通常会是命令操作者本身。
    + \-a：等于 \-pdr
    + \-d：若源文件为连接文件，则复制连接文件属性而非文件本身
    + \-p：连同文件的属性一起复制过去
    + \-r：递归持续复制
    + cp /dir1/file1 /dir2： dir1至少需要x权限，file1至少需要r权限，dir2至少需要w、x权限。         
3. 软连接与硬链接（更详细信息见后续相关章节）
    + 软连接（symbolic link）相当与快捷方式，删除**被链接的源文件**会导致无法访问。
    + 硬链接（hard link）相当与直接关联源文件的存储区块，本质上关联与源文件相同的i-node（所以权限参数中会有i-node关联数），**直接删除仍有源文件**。
4. rm：移除文件或目录 `rm -f` `rm -rf` 
    + \-f：强制删除force
    + \-r：递归删除
5. mv：移动文件与目录，或**更名** `mv old new`
    + rename同样可以更名
6. basename：取得路径的文件名与目录名称 `basename path` `dirname path`
    + basename 取得路径的最后一项 basename /etc/sysconfig/network  ➡️  network
    + dirname 除去路径的最后一项剩下的 dirname /etc/sysconfig/network ➡️  /etc/sysconfig
    + 一般在写程序的时候使用
+ 文件**内容**查阅
1. cat：由第一行开始显示内容 `cat -n` `cat -b` `cat -E` `cat -A` 
    + \-n：显示行号，空白行也标行号
    + \-b：显示行号，空白行不标行号
    + \-E：将结尾的断行字符$显示出来
    + \-A：等于 \-vET
    + \-v：列出一些看不出来的特殊字符
    + \-T：将[Tab]键以 ^I 显示出来
2. more：翻页查看（**只能向后**）
    + 空格键（Space）：向下翻**一页**
    + Enter：向下滚动**一行**
    + /string：查询字符串关键字，n键向下继续查询
    + \:f：显示文件名和行数
    + q：退出
    + b或[Ctrl]-b：往回翻页
3. less：翻页查看（**支持向前向后**）
    + 空格键（Space）/[PageDown]：向下翻**一页**
    + [PageUp]：向上翻一页
    + /string：**向下**查询字符串关键字
    + ?string：**向上**查询字符串关键字
    + n：重复前一个查询（与/或?定下的方向相关）
    + N：**反向**前一个查询（与/或?定下的方向相关）
    + q：退出
+ 数据选取
1. head：取出前面几行 `head -n 100` `head -n -100`
    + **负数**指**扣掉**文件*末尾*的100行，只取剩下的前面的所有数据行。  
2. tail：取出后面几行 `tail -n 100` `tail -n +100` `tail -f log.txt`
    + **正数**指第100行**以后**的所有数据
    + \-f：监测日志文件，**常用于查看是否有请求打进来**。
3. od：非纯文本文件（如二进制文件binary） `od -t c /usr/bin/passwd`
+ 文件时间
1. mtime：内容数据更改时间
2. ctime：文件状态（权限、属性等等）更改时间
3. atime：文件内容被取用时间，读取时间。（cat命令会更新这个时间） 
4. touch：修改文件时间或**创建新文件** `touch newfile.txt` `touch -a` `touch -c` `touch -m` 
+ 文件与目录的**默认权限**与**隐藏属性**
1. chattr设置，lsattr查看，只在**Ext2/Ext3**的文件系统上生效
2. umask：设置文件默认权限 `umask 022`
    + 文件默认权限 rw-rw-rw- 666
    + 目录默认权限 rwxrwxrwx 777
    + umask指的是默认值需要**减掉**的权限
    + 新建文件：rw-rw-rw-(666) **-** ----w--w-(022) ➡️ rw-r--r--(644)
    + 新建目录：rwxrwxrwx(777) **-** ----w--w-(022) ➡️ rwxr-xr-x(755)
3. chattr：设置文件的隐藏属性（**很多只能是root才能设置**）`chattr +a` ` chattr -a` `chattr +i` `chattr -i`
    + a 文件只能增加数据，不能删除和修改数据
    + i 文件不能删除、改名、设置连接、修改数据等等，直接锁死
+ 文件特殊权限
1. Set(Share) UID 4
    + 仅对**二进制程序**有效
    + **s标志**出现在文件**所有者**的**x权限**上
    + **非文件所有者**对该文件拥有**x权限**
    + 非文件所有者执行该文件时（run-time）将拥有文件所有者的权限。**s有share权限的意味**
2. Set(Share) GID 2
    + 仅对**二进制程序**有效
    + **s标志**出现在文件**文件所属用户组**的**x权限**上
    + **非文件所有者**对该文件拥有**x权限**
    + 非文件所有者执行该文件时（run-time）将获得**文件所属用户组的支持**。**s有share权限的意味**
3. Sticky Bit 1
    + 只针对**目录**有效
    + 用户对目录**拥有w，x权限**
    + **只能针对自己创建的文件或目录进行删除、重命名、移动等操作，无法删除他人文件。**
4. 通过chmod命令更改，在之前的三个数字前**再加上一个数字**，该数字代表特殊权限。 `chmod 6755 test` 
+ 查看文件类型
    1. file：`file /usr/bin/passwd`
+ 寻找“执行文件”
    1. which：默认查找PATH内所规范的目录 `which cd`
+ 文件名的查找
1. 通常先使用`whereis`或者`locate`来检查，速度更快，查不到了再用`find`
2. `whereis`和`locate`查找**数据库/var/lib/mlocate**，`find`查找硬盘
3. 更新locate数据库命令 `updatedb`
4. find：`find / -name passwd` `find /var -type f` `find / -perm 555` `find / -size +1000k` `find ./ -name "*.log" -exec rm -rf {}\;` `find / -atime +4`
    + \-exec：对查找结果进行**额外动作**，`{}`表示其中查找结果中的一条纪录，必须以`\;`结尾
# linux磁盘与文件系统管理
+ 文件系统的运行：
1. super block：纪录此文件系统的**整体信息**，包括index/block的总量、使用量、剩余量，以及文件系统的格式与相关信息等。
2. i-node：记录文件的**属性**，一个文件占用一个i-node，同时记录此文件的**数据所在的block号码**；
3. block：实际记录文件的内容，若文件太大时，会占用多个block。
4. 如果能找到文件的i-node的话，就能知道这个文件所放置的block号码，就能读出该文件的实际数据了。
5. Ext2为索引式文件系统。
6. FAT格式文件系统（U盘、闪存）**没有i-node存在**，每个block号码都记录在前一个block当中，类似链表，读取效率差，会导致**磁盘碎片**
+ Ext2文件系统
1. data block
    + 大小有：1KB 2KB 4KB
    + 文件大小大于block的大小，则一个文件会占用多个block数量
    + 文件大小小于block的大小，则该block剩余空间就不能够再被利用（**磁盘空间浪费**）
    + block的大小和数量在格式化完就不能再改变（除非重新格式化）
2. i-node table
    + 每个i-node大小均固定为 **128bytes**
    + 记录一个block号码要花费**4bytes**
3. i-node/block与**文件大小**的关系
    + 一个i-node分为**4个区域**（以1KB的block为例）
        + 12个**直接记录区**：直接记录12个block号码。12 * 1KB = 12KB
        + 1个**间接记录区**：记录1个block号码，这个block再去记录block号码。 1 * (1KB/4B) * 1KB = 256KB
        + 1个**双间接记录区**：记录1个block号码，这1个block的数据依然是block号码，再往下的block依然记录的是block号码。1 * (1KB/4B) * (1KB/4B) * 1KB = 256 * 256 KB
        + 1个**三间接记录区**: 记录1个block号码，这1个block的数据依然是block号码，再往下的block依然记录的是block号码，再再往下的block依然记录的是block号码。1 * (1KB/4B) * (1KB/4B) * (1KB/4B) * 1KB = 256 * 256 * 256 KB
        + 总额：12 + 256 + 256 * 256 + 256 * 256 * 256 = 16GB，所以如果将data block设置成1KB的话，文件系统能够容纳的**最大文件**为16GB。 
4. dumpe2fs：查看设备的文件系统信息 `dumpe2fs /dev/hdc2`
5. df：调出目前挂载的设备 `df -h` `df -h /` 
+ 文件系统的简单操作
1. df：列出文件系统的整体磁盘使用量 `df -h /etc` `df -i`
    + /proc挂载在内存当中，没有占据任何硬盘空间
    + /dev/shm 是**利用内存虚拟出来的磁盘空间**，这个目录下的任何数据文件的**访问速度非常快速**（在内存工作），**断电**后内容会消失
2. du：评估文件系统的磁盘使用量（常用于评估目录）`du -sh /etc` `du -m`
+ 连接文件：ln `目标文件连接源文件`
1. 硬链接（hard link） `ln 源文件 目标文件`
    + 新建一个文件名连接到某一个i-node上，不会增加i-node，也不会耗用block数量
    + 如果你将任何一个“文件名”删除，其实i-node与block**都还是存在的**，此时可以通过另一个“文件名”来读取到正确的文件数据
2. 软链接（Symbolic link） 符号链接，也即快捷方式 `ln -s 源文件 目标文件` 
    + symbolic link是创建一个**独立的文件**，指向**它链接的那个文件的文件名**
    + 当源文件被删除之后，symbolic link文件会**“无法打开”**
    + symbolic link所创建的文件为一个独立的新的文件，会**占用掉i-node与block**
+ 磁盘的分区、格式化、检验与挂载
1. 向系统新增硬盘的流程
    + 对磁盘进行分区，以新建可用分区
    + 对*该分区*进行格式化（format），以创建系统可用的文件系统
    + 对刚才新建好的文件系统进行检验
    + 在Linux系统上，创建挂载点（也即目录），并将它挂载上来
2. fdisk：**磁盘分区**，**只有root权限**才可以执行，设备名**不带数字**。 `fdisk /dev/hdc` `fdisk -l /dev/hdc 该命令仅查看信息，不操作磁盘` `partprobe`
    + m：命令介绍
    + d：删除一个分区
    + n：新增一个分区
    + p：显示分区表
    + q：退出，之前的所有操作**都不生效**
    + w：写入分区表，之前的所有操作**都生效**
    + **partprobe** w后要强制让**内存**更新分区表。
3. mkfs：进行**文件系统的格式化**，设备名**带数字**，表示对某一分区格式化文件系统。 `mkfs -t ext3 /dev/hdc6`
4. mke2fs：可以制定blcok大小和i-node数量,设备名**带数字**。`mke2fs -j -L "test" -b 2048 -i 8192 /dev/hdc6`
5. fsck,badblocks：**磁盘检验**，设备名**带数字** `fsck -C -f -t ext3 /dev/hdc6` `badlocks -sv /dev/hdc6`
6. mount,umount：**磁盘挂载与卸载**，设备名**带数字** `mount -a` `mount /dev/hdc6 /home/elesev` `mount -l` `umount /home/elesev` `umount /dev/hdc6` `mount -L "elesev" /home/elesev`
    + 单一文件系统不应该被重复挂载在不同的挂载点（目录）
    + 单一目录不应该重复挂载多个文件系统
    + 作为挂载点的目录理论上应该都是**空目录**
    + \-a：依照配置文件/etc/fstab的数据将所有未挂载的磁盘都挂载上来
    + \-l：显示目前挂载的信息
    + \-L：利用**卷标名称**进行挂载
7. e2label：设置**文件系统卷标**（Lable）`e2label /dev/hdc6 "elesev"`
+ 开机挂载
1. 关机后**挂载失效**，开机后系统**自动进行挂载**。
2. /etc/fstab(file system table)是mount命令执行时，所有参数会写入的文件。
3. 每次开机会根据/etc/fstab中的配置自动进行挂载，可以**直接编辑**此文件。
4. /etc/fstab输入有误导致无法开机成功，进入**单用户维护模式**。 使用命令`mount -n -o remount,rw /`，再重新编辑/etc/fstab
+ 内存交换空间（swap）的构建 `mkswap /dev/hdc7` `free -h` `free -m` `swapon /dev/hdc7` 
1. swap是**利用硬盘**来暂时存放**内存**中的信息。
2. swapon 启用内存交换空间
3. 最多创建32个swap
4. 64位最大内存寻址到64GB，swap总量最大也是仅能达64GB。
# 文件与文件系统的压缩与打包（文件系统也可以打包）
+ tar 
1. `tar -vtf` 
2. `tar -xvzf  -C ` 
3. `tar -czvf `
4.  `tar -czvf --exclude= `
+ dump：完整备份工具
1. `dump -S /dev/hdc1`
2. `dump -W`
3. `dump -0j -f /root/etc.dump.bz2 /etc`
+ restore：恢复数据
1. `restore -t -f /root/boot.dump`
+ dd：读取磁盘设备的内容，将整个设备备份成一个**文件**。
1. `dd if="input file" of="output file" bs="blocksize"`
2. `dd if=/etc/passwd of = /tmp/passwd.back`
3. `dd if=/dev/zero of=/tmp/elesev bs=1M count=128`
# Linux账号管理与ACL权限设置（未完成）
# 软件磁盘阵列（Software RAID）（未完成）
# 逻辑卷管理器（Logical Volume Manager）（未完成）
# 例行性工作（crontab）
+ 仅**执行一次**的工作调度
1. **atd**：调度单一工作的**服务**
    + `/etc/init.d/atd restart`
    + `chkconfig atd on`
2. atd的**运行方式**
    + **at命令**生成所要运行的工作，并将工作以**文本文件**的方式写入 **/var/spool/at/目录**下，该工作便能等待**atd服务**的取用和执行
    + **不是所有人**都可以进行at工作调度
        + 通过 **/etc/at.allow**和 **/etc/at.deny**文件进行限制
        + 如果 **/etc/at.allow存在**，**只有**写入该文件的用户才能使用使用，**其余人**不可使用。
        + 如果 **/etc/at.allow不存在**，就寻找 **/etc/at.deny**文件，**没在该文件中**的用户**都能**使用。
        + 如果上述两个文件都不存在，**只有root**可以使用
    + at工作可以**独立出**用户的**bash环境外**执行，直接交给**atd程序接管**，允许用户**脱机**
3. at命令使用
    + `at now + 5 minutes`
    + `atq` 查询主机上面有多少at工作调度
    + `atrm [jobnumber]` 将对应号码的工作调度删除
4. batch：系统有空时才进行后台任务（会在**CPU工作负载**小于0.8的时候才执行工作任务）
+ **循环执行**的例行性工作调度
1. cron**每分钟**会读取一次/etc/crontab（**系统**例行性任务）和/etc/spool/cron（**用户**例行性任务）里面的数据内容
2. 用户权限设置
    + 通过 **/etc/cron.allow**和 **/etc/cron.deny**文件进行限制
    + 如果 **/etc/cron..allow存在**，**只有**写入该文件的用户才能使用使用，**其余人**不可使用。
    + 如果 **/etc/cron..allow不存在**，就寻找 **/etc/cron..deny**文件，**没在该文件中**的用户**都能**使用。
    + 如果上述两个文件都不存在，**只有root**可以使用
3. `crontab`：**用户**新建工作调度 `crontab -e` `:wq`
    + `crontab -e` 会进入vim界面，新的工作记录会写入**/var/spool/cron**下对应的**用户文件**
    + 不推荐通过**直接编辑**/var/spool/cron下对应的用户文件，可能由于输入**语法错误**导致无法执行cron
    + /var/log/cron：cron每执行一项工作就会记录日志到该文件，可以查看是否被**植入木马**
4. crontab语法
    + 格式：`分 时 日 月 周 命令` `0 3,6 * * * /data/scan.sh > /dev/null`
    + 特殊字符
        + \*（星号）：任何数字表示的时间点都会执行 \*
        + ，（逗号）：所列的数字表示的时间点会执行 3,6
        + \-（减号）：表示一段时间内都在执行 8-12
        + /n（斜线）：表示每隔n段时间就会执行 /5
5. /etc/crontab：针对**系统的**例行性任务
    + `*/5 * * * * root run-parts /root/runcron` 让系统每隔5分钟去执行/root/runcron**目录**下的所有**可执行文件**
    + `run-parts`是一个脚本，内容是将后面接的**目录**内所有**文件**找出来执行。
6. anacron：不能指定何时执行某项任务，而是会检测**停机期间**应该执行但是并没有进行的crontab任务，将该任务执行一遍。
# 程序管理与SELinux初探
+ for-and-exec流程
1. 系统先以fork的方式复制一个与父进程相同的**暂存进程**，这个进程与父进程**唯一的区别**就是PID不同。
2. 这个暂存进程还会多一个**PPID参数（父进程的进程标识符）**
3. 然后暂存进程以exec的方式加载实际要执行的程序。
+ 服务（daemon）：常驻在内存当中的进程
+ **工作管理（job control）**
1. 进行工作管理的行为中，每个工作都是**目前bash的子进程**，彼此之间是有相关性的。
2. &：直接将命令丢到后台中“执行”
    + 这样不会被[Ctrl]+c中断，一定会执行
    + 后台执行的命令，如果有stdout和stderr，依然是输出到屏幕上面，由于无法用[Ctrl]+c中断，很有可能导致屏幕被搞得花花绿绿的，此时用数据流重定向，将输出数据传送至某个文件中。`tar -czvf /tmp/etc.tgz /etc > /tmp/log.txt 2>&1 &`
3. [Ctrl]+z：将目前的工作丢到后台中“暂停”
4. jobs：查看目前的后台工作状态
    + +：表示最近放到后台的工作号码，fg会先处理这个
    + -：表示最近最后第二个放置到后台的工作号码
5. fg(fore ground):将后台工作**拿到前台**来处理 `fg %1 工作号码为1的取出到前台处理`
6. bg：让工作在**后台下**的状态变成执行中 `bg %3`
+ kill：管理后台的工作 `kill -9 ${pid}` `kill -9 %2` `kill -SIGTERM %1`
1. -9：**强制删除**一个不正常的工作
2. -15：以**正常步骤**结束一项工作（15是默认值）
+ 脱机管理问题（退出bash后，任务会被中断掉）
1.nohup：脱机或注销系统后，工作继续进行。 `nohup ./tesh.sh &`
+ 进程的查看
1. ps：将某个时间点的进程运行情况选取下来
    + `ps -l`：仅查看自己的bash相关进程
        + F:4(root) 1(此子进程仅可进行复制fork而无法实际执行exec）
        + S：进程状态（STAT）
            + R(Running)：进程正在运行
            + S(Sleep)：进程处于睡眠状态，但可以被**唤醒**
            + D：不可以被唤醒，可能在等待I/O
            + T：停止状态，可能在工作控制（后台暂停）或除错（trace）状态
            + Z(Zombie)：进程已经终止，却无法被**删除至内存外**。
        + UID/PID/PPID：编号
        + C：CPU使用率，单位为百分比
        + PRI/NI：Priority/Nice缩写，CPU执行优先级，数值越小表示该进程越快被CPU执行
        + ADDR/SZ/WCHAN：都与内存有关
        + TTY：登陆者的终端机位置
        + TIME：**使用掉**的CPU时间，即此进程实际**花费CPU运行的时间**，不是系统时间
        + CMD：触发进程的命令
    + `ps aux`：查看系统所有进程，默认按照PID的顺序排序显示
        + USER：进程所属用户
        + PID：进程标识符
        + %CPU：使用掉的CPU资源百分比
        + %MEM：所占用的**物理内存**百分比
        + VSZ：使用掉的**虚拟内存量**（KB）
        + RSS：占用的**固定内存量**（KB）
        + TTY：终端机
        + STAT：进程状态（R/S/T/Z）
        + START:进程被触发启动的时间
        + TIME：进程**实际使用**CPU运行的时间
        + COMMAND：进程的实际命令
2. top：持续监测进程运行的状态（实时）
    + load average：系统在1,5,15分钟的**平均工作负载**。
    + 默认使用CPU使用率（%CPU）作为排序
    + M键 按照内存使用率排序
    + 1键 显示所有CPU核心
    + r键 修改nice指
 3. pstree：显示进程树
    + 所有的进程都是依附在**init进程**下面，这个进程的**PID是1号**，是由Linux内核主动调用的第一个进程。
 4. kill：管理进程，帮助我们将signal传送给**某个工作（%jobnumber）**或者是**某个PID（直接输入数字）** `kill -SIGKILL %1` `kill -SIGKILL 12345`
    + SIGHUP 1：让PID重新读取自己的配置文件，类似重新启动
    + SIGINT 2：相当于[Ctrl]-c，中断一个进程的进行
    + SIGKILL 9：强制中断一个进程
    + SIGTERM 15：以正常的结束进程来终止该进程
    + SIGSTOP 17：相当于[Ctrl]-z，暂停一个进程的进行
5. killall：通过**命令名称**发送信号，不需要查找PID或%jobnumber。`killall -1 httpd` `killall -9 httpd`        
+ 僵尸进程
1. 某个进程的CMD后面还街上< defunct > ，代表该进程是僵尸进程
2. 成因：进程已经执行完毕，或者因故应该要终止了，父进程却无法完整将该进程结束掉，造成进程一直存在内存当中。
3. **init进程**是所有进程的父进程，会接管僵尸进程，如果init无法将僵尸进程删除，只能通过**reboot**的方法抹去进程。
+ 进程的执行顺序（进程的**优先级**）
1. PRI值由**内核动态调整**，用户无法直接调整PRI值，但可以调整nice值
2. nice值
    + root 可调整范围 -20~19
    + 一般用户 可调整范围 0~19
    + nice：**启动命令时**同时设置nice值 `nice -n -5 vim`
    + renice：**已经启动**的进程的nice重新调整 `renice 10 ${PID}`
3. PRI(new) = PRI(old) + nice
+ 检查系统资源
1. free：查看内存使用情况 `free -h` `free -m`
    + buffers：缓冲记忆
    + cached：缓存
    + 物理内存被用光是**正常的**（为了加速访问而将最近访问的数据放在内存），swap最好不要被使用。
2. uname：查看系统与内核相关信息 `uname -a`
3. uptime：查看系统启动时间与工作负载 `uptime`
4. netstat：跟踪网络 `netstat -antupl` `netstat -tlnp`
    + LocalAddress：本地的IP端口情况
    + ForeignAddresss：远程主机的IP端口情况
    + State：连接状态，主要有建立（ESTABLISHED）及监听(LISTEN)
    + Path：连接到**此socket**的相关程序的路径，或者是相关数据输出的路径。
5. dmesg：分析内核产生的信息 `dmesg|more` `dmesg| grep -i hd`  `dmesg |grep -i eth` 
6. vmstat：监测系统资源变化 `vmstat 1 3` `vmstat 5` `vmstat -d`
    + 进程字段procs：
        + r：等待运行中的进程数量
        + b：不可被唤醒的进程数量
        + r和b越大，代表系统越忙碌
    + 内存字段memory：
        + swpd：虚拟内存被使用的大小
        + free：未被使用的内存大小
        + buff：用于缓冲存储器的内存大小
        + cache：用于高速缓存的大小
    + 内存交换空间swap：
        + si：从磁盘进入内存的量
        + so：从内存进入磁盘的量
        + si/so：越大，系统性能越差
    + 磁盘读写io
        + bi：**磁盘写入**内存的**块数量**
        + bo：内存**写入磁盘**的**块数量**
        + 两者值越高，io越忙碌
    + 系统system
        + in：每秒被中断的进程数
        + cs：每秒钟进行的事件切换数
        + 两个数值越大，代表系统与**接口设备**的通信非常频繁，包括磁盘、网卡、时钟等等。
    + CPU
        + us：非内核层的CPU使用状态
        + sy：内核层的CPU使用状态
        + id：闲置的状态
        + wa：等待I/O所耗费的CPU状态
        + st：被**虚拟机**所盗用的CPU的状态
+ /proc/* `cat /proc/${PID}/cmdline` `cat /proc/${PID}/environ`
1. 进程在内存中，内存中数据写入到/proc/* 目录下
2. **cmdline**：启动进程的**命令串**
3. environ：进程的环境变量内容
+ 查询**已打开**文件或**已执行程序打开**的文件
1. fuser：通过**文件（或文件系统）** 找出 **正在使用该文件的程序** `fuser -k /dev/pts/${user_id} 清理终端（停止用户登录）`  `fuser -v ${file}`
2. lsof：列出被进程所打开的文件名 `lsof |  grep dele | awk -F " " '{print $NF}' | xargs kill -9 ` `lsof -p $pid` `lsof -i:$port` `lsof -u root -a -U` `lsof -u root | grep bash`
3. pidof：找出某个正在执行的进程的PID `pidof init` `pidof httpd`
+ SELinux初探（未完成）
# 认识系统服务（daemons）
+ daemon是程序，service是服务。一般说法是：实现了某种service功能的daemon程序。
+ daemon分类：
1. stand_alone：此daemon可以自行单独启动服务，一直占用内存和系统资源**持续**对外提供服务。
2. super daemon：通过一个**统一的daemon**来负责唤起服务。没有客户端请求时，各项服务都是未启动。等到有客户端请求时，super daemon才**唤醒**相对应的服务，客户端请求结束后，服务也会关闭并释放系统资源。**优点**：super daemon具有安全控管的机制；**缺点**：服务加载到内存需要时间，响应时间稍慢。（**telnet**是由super daemon管理）
+ daemon命名规则：服务名称后加上“d”，如httpd。
+ /etc/services：记录服务与端口号之间对应关系的文件
1. http 80
2. ftp 21
3. ssh 22
4. mysql 3306
5. ...
+ daemon的**启动脚本**与**启动方式**
1. 启动脚本（shell script）和配置文件存放目录
    + /etc/init.d/* ：**启动脚本（可执行文件）** 放置处，是**公认**的目录
    + /etc/sysconfig/* ：各服务的**初始化**环境配置文件
        + /etc/sysconfig/syslog
        + /etc/sysconfig/network
    + /etc/xinetd.conf,/etc/xinetd/* ：super daemon配置文件
    + /etc/* ：各服务各自的配置文件
    + /var/lib/* ：各服务产生的数据库
        + /var/lib/mysql
    + /var/run/* ：各服务的程序的PID记录处
        + /var/run/syslogd.pid
2. **Stand alone**的 **/etc/init.d启动** `/etc/init.d/syslog status` `/etc/init.d/syslog restart` `/etc/init.d/crond restart`
    + **service**：启动Stand alone的另一种方式，它是一个脚本，会分析service后边的**参数**，**再去/etc/init.d去取得**正确的服务来start或stop
        + `service --status-all`
        + `service crond restart`
4. **Super daemon**的启动方式 
    + **xinetd服务** 是一个super daemon，默认配置文件是/etc/xinetd.conf
    + super daemon本身也是一个**Stand alone**的服务，自己也**常驻内存**
    + super daemon自己启动的方式与Stand alone是**相同**的，但是它所管理的其他daemon则是通过**修改配置文件**来启动。
        + `grep -i 'disable' /etc/xinetd.d/* ` 查看super daemon所管理的*未启动*的服务
        + `vim /etc/xinetd.d/rsync`
    + super daemon管理的服务可以**多一层**管理的手段来达成**类似防火墙的机制**。我们可以将某个系统服务**针对不同的客户端来源**指定不同的**权限** `vim /etc/xinetdd/rsync`
    + 任何以**xinetd管理的服务**都可以通过 **/etc/hosts.allow,/etc/hosts.deny** 来设置防火墙
    + 服务如果**支持TCP Wrappers函数**的功能，该服务业可以通过/etc/hosts.allow,/etc/hosts.deny来设置防火墙
        + ldd(library dependency discovery)：查询某个**程序**的动态函数支持状态 `ldd httpd` `ldd sshd`
        + ldconfig：更新动态库
        + 允许进入的写在/etc/hosts.allow，不允许进入的写在/etc/hosts.deny，**以allow优先**。
 5. 设置服务**在开机时**启动
    + chkconfig：管理系统服务**开机时**是否启动 `chkconfig --list` `chkconfig --level 3 httpd on 让httpd这个服务在run level为3的时候启动` `chkconfig rsync off` `chkconfig --add myTestServer 将我的服务加入chkconfig的管理中，该服务必须可以通过init.d启动`
# 认识与分析日志文件
+ 用于日志文件的服务种类：
1. syslogd：主要记录系统与网络服务的信息（所**配置的服务**）
2. klogd：主要记录内核产生的各项信息
3. logrotate：主要进行日志文件的**轮替**功能
+ syslogd：一个好的系统管理员要**经常去“巡视”日志文件**的内容。 `ps aux | grep syslog 检查是否启动syslogd` `chkconfig --list syslog 检查是否设置开机启动`
1. 日志格式
    + 时间发生的日期与时间
    + 发生此时间的主机名
    + 启动此事件的**服务名称（如samba，xinetd等）** 或 **函数名称（如libpam）**
    + 该信息的实际数据内容
2./etc/syslog.conf：syslog的配置文件
    + `mail.info /var/log/maillog_info ` mail服务产生的大于等于info等级的信息，都记录到var/log/maillog_info**文件**中
    + 服务名称：例如 mail auth cron daemon kern等
    + 信息等级： info notice warning(warn) err(error) crit alert emerg(panic)
    + 链接符号：
        + “.”代表比后面**还要高**的等级（含该等级）都被记录下来
        + “=”所需要的等级就是后面接的等级而已，**其他的不要**
        + “.!”代表不等于，除了该等级，**其他都要**
3. 日志文件的安全性设置 `chattr +a /var/log/message 文件只增不可删` `chattr -a /var/log/message`
4. **日志文件服务器**记录其他主机上的日志文件。客户端传送，服务端接收。
+ logrotate：将**旧的日志文件**移动成**旧文件**，并**新建一个空的文件作为新的日志文件**。
1. logrotate挂在**cron**下面，在**规定的时间**到了才来进行日志文件的轮替。`/etc/cront.daily/logrotate`
2. logrotate配置文件
    + /etc/logrotate.conf
        + weekly daily
        + rotate
        + create
        + compress
        + 外部命令
            + sharedscripts
            + endscript
            + prerotate
            + postrotate
        + include /etc/logrotate.d/ 读入该目录下的所有配置一起执行
    + /etc/logrotate.d/
3. 文件名**后缀数字越小**，代表记录的是**越新的**日志数据
+ **自定义**日志文件的**轮替功能**
1. 对文件新建**+a属性** `chattr +a ${logfile}`
2. 在/etc/logrotate.d/新建conf文件 `vim /etc/logrotate.d/${server}.conf`
+ logwatch：每天分析一次日志文件，并且将数据**以email的格式寄送给root**。
# 源码与Tarball
+ Linux系统真正识别的可执行文件是**二进制文件**
+ 软件程序的源代码为纯文本文档 + 利用已经存在的函数库 ➡️ 生成可执行文件为**binary file**
+ 函数库：**类似**子程序的角色们可以**被调用**来执行一段功能。
1. 函数库分为**动态函数库**和**静态函数库**
2. 程序执行**调用**外部函数库，外部函数库**回传**执行结果，
3. make与configure
    + make：make是一个**程序**，会去找**Makefile文件**
    + configure：软件开发商提供的**系统环境检测程序**，并主动**生成Makefile文件**，并**开启编译**。
        + 是否有合适的编译程序可以编译本软件的程序代码
        + 是否已经存在本软件所需要的函数库或其他需要的相关软件
        + 操作系统平台是否适合本软件，包括Linux的内核版本
        + 内核的头定义文件（header include）是否存在（驱动程序要使用）
4. Linux默认将函数库放置在 **/lib** 和 **/usr/lib**
5. **Tarbll管理**的**基础软件**
    + gcc或cc等C语言编译程序（compiler）
    + make及autoconfig等软件
    + 需要kernel提供的Library以及相关的Include文件
6. **Tarbll软件**安装的**基本步骤**
    + 取得源文件：将tarbll文件在/usr/local/src目录下解压
    + 取得步骤流程：进入目录，查阅INSTALL和README等相关文件（很**重要的步骤**）
    + 相关属性软件安装：根据INSTALL/README的内容安装好一些**相关的软件**（非必要）
    + 建立makefile：以**自动检测程序（configure或config）**检测操作环境，并**建立Makefile这个文件**。
    + 编译：以**make**这个程序并使用**当前目录下**的Makefile作为它的**参数配置文件**，来进行make（编译或其他）的操作
    + 安装：以**make**这个程序并使用**当前目录下**的Makefile作为它的**参数配置文件**，依据**install这个目标（target）** 的指定来安装到**正确的路径**
7. 基本步骤的**命令执行方式**
    + `./configure`：建立Makefile文件（**./configure 可以修改安装目录**）
    + `make clean`：读取Makefile文件中关于clean的工作，去除**目标文件（*.o）**，源码中可能存在之前编译过的**目标文件（*.o）**
    + `make`：依据Makefile当中的默认工作进行编译，默认将编译完成后的可执行文件放到**当前目录**
    + `make install`：依据Makefile文件中关于install的选项，将编译后的数据安装到**对应的目录**中去
8. Tarball软件**管理建议**
    + 安装的软件一般放置在`/usr/local`，源码放置在`/usr/local/src`
    + 只要将**安装目录**删除，即可视为**删除软件**。
    + 软件的**man page**可以加入到**man path**中
+ 函数库管理
1. **静态函数库**
    + 扩展名（**后缀为.a的文件**）
        + 形式通常为**libxxx.a**
    + **编译时**直接**整合到执行程序**中，所以利用静态函数库编译成的**文件会比较大**。
    + 编译成功的文件不再需要**向外部**要求读取函数库的内容，可以**独立执行**。
    + 函数库如果升级，程序则需要**重新编译**
2. **动态函数库**
    + 扩展名（**后缀为.so的文件**） share object
        + 形式通常为**libxxx.so**
    + **编译时**动态函数库在程序里面只有一个**指向(Pointer)** 的位置，没有被整合到可执行文件当中
    + 编译成功的文件不能独立被执行，**函数库文件**必须存在，函数库的**所在目录**也不能改变
    + 函数库升级时，程序**无需**重新编译。
3. ldconfig：将动态函数库**预加载到内存**，提高访问速度。 `ldconfig`
    + 动态函数加载到高速缓存的步骤
        + 首先必须在**/etc/ld.so.conf文件**中写下想要读入高速缓存当中的动态函数**所在的目录**
        + 执行`ldconfig`将/etc/ld.so.conf的数据读入缓存当中，同时也将数据记录一份在**/etc/ld.so.cache文件**当中
4. ldd：程序的动态函数库解析（查找**程序相关**的动态函数库）`ldd /usr/bin/passwd`
5. md5sum，sha1sum：检验软件正确性，防止篡改
# 软件安装
+ 软件开放商在他们系统上**先编译好**软件，再将编译好的可执行文件**发布给用户**，如果用户的系统环境与厂商一模一样，则可以直接使用，**省去用户编译的工作**
+ RPM与**SRPM**
1. RPM
    + 文件名 ***xxx.rpm***
    + **可以直接安装**
    + 内含程序类型：**已编译**
    + **不可**修改参数并编译
2. SRPM
    + 文件名 ***xxx.src.rpm***
    + **不可以**直接安装
    + 内含程序类型：**未编译的源代码**
    + **可以**修改参数并编译
+ **YUM**在线升级：解决RPM**属性依赖问题**
    + yum的配置文件 **/etc/yum.repos.d/* 
    + 查询功能：yum \[list|info|search|provides|whatprovides]
        + `yum search raid` 搜索磁盘阵列（raid）**相关的软件**有哪些
        + `yum info mdadm` 找出mdadm这个软件的功能为何，相关信息
        + `yum list` 找出**yum服务器**上面提供的所有软件名称
        + `yum upgrade` 列出**yum服务器**上可供本机升级的软件有哪些
        + `yum provides passwd` 列出提供**passwd这个文件**的软件有哪些
    + 安装/升级功能：yum \[install|upgrade]
        + `yum insatll pam-devel`
        + `yum remove pam-devel`
    + RPM软件属性依赖位置：`yum repolist all` `yum clean`
    + 全系统自动升级
        + `vim /etc/crontab` `crontab -e`
        + 0 3 * * * /usr/bin/yum -y update
+ rpm：RPM软件管理程序
    + RPM安装（install） `rpm -ivh` `rpm --prefix 新路径` `rpm --nosignature`
        + \-v：查看更详细的安装信息页面
        + \-h：以安装信息栏显示安装进度
        + rpm -ivh rp-pppoe-3.5-32.1.i386.rpm
        + rpm -ivh http://wevsute.name/path/pkgname.rpm
    + RPM升级（upgrade/freshen） `rpm -Uvh` `rpm -Fvh`
    + RPM查询（query）
        + \-q：仅查询后面接的软件是否安装
        + \-qa:列出所有已经安装在本机的软件名称
        + \-qi:列出**某个软件**的详细信息
        + \-qR:列出**该软件**有关的依赖软件所含的文件
        + \-qf:找出**该文件**属于哪一个已安装的软件
    + RPM验证与数字证书（Verify/Signature）
        + \-V
        + \-Vp
        + \-Vf
    + RPM卸载与重建数据库（erase/rebuilddb）`rpm -e pam` `rpm --rebuilddb`
        + RPM数据库/var/lib/rpm
# Linux备份策略
1. 备份资料的考虑
    + 硬件问题
    + 软件问题 `rm -rf /home`
2. 备份方式
    + 增量备份：系统进行完第一次完整备份后，经过一段时间的运行，比较系统与备份文件的差异，仅备份有差异的文件而已。之后每一次备份都只备份当前系统**与上一次备份时间点的系统**之间的差异。即**当前时间点**与**上一次的时间点**
    + 差异备份：每次备份都是与**原始的完整备份比较**的结果，即**当前时间点**与**最初时间点**。
3. rsync：**远程备份**  需要先有远程服务器的**免密登录**权限
    + rsync -av -e ssh $ {basedir} $ {id}@${host}:${remotedir}
    + rsync -av -e ssh /data/elesev/weekly elese@192.168.0.100:/home/elesev
