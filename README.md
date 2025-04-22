# Linux基础操作[^教程]

## **目录**

- **Linux基础操作**
  - [文件与目录操作](#文件与目录操作)
    - [ls命令](#ls命令)
    - [pwd命令](#pwd命令)
    - [cd命令](#cd命令)
    - [mkdir命令](#mkdir命令)
    - [touch命令](#touch命令)
    - [cat命令](#cat命令)
    - [more命令](#more命令)
    - [cp命令](#cp命令)
    - [mv命令](#mv命令)
    - [rm命令](#rm命令)
    - [which命令](#which命令)
    - [find命令](#find命令)
  - [内容处理与管道](#内容处理与管道)
    - [grep命令](#grep命令)
    - [wc命令](#wc命令)
    - [管道符|](#管道符)
    - [echo命令](#echo命令)
    - [反引号\`](#反引号)
    - [tail命令](#tail命令)
    - [head命令](#head命令)
    - [重定向符](#重定向符)
  - [系统与文件管理](#系统与文件管理)
    - [软链接](#软链接)
    - [日期](#日期)
    - [时区](#时区)
  - [网络与主机配置](#网络与主机配置)
    - [ip地址](#ip地址)
    - [主机名](#主机名)
  - [进程与端口管理](#进程与端口管理)
    - [ps命令](#ps命令)
    - [kill命令](#kill命令)
    - [nmap命令](#nmap命令)
    - [netstat命令](#netstat命令)
    - [ping命令](#ping命令)
  - [网络工具与监控](#网络工具与监控)
    - [wget命令](#wget命令)
    - [curl命令](#curl命令)
    - [top命令](#top命令)
    - [df命令](#df命令)
    - [iostat命令](#iostat命令)

---

## 文件与目录操作

### ls命令

功能：列出文件夹信息

语法：`ls [-l -h -a] [参数]`

- 参数：被查看的文件夹，不提供参数，表示查看当前工作目录
- -l，以列表形式查看
- -h，配合-l，以更加人性化的方式显示文件大小
- -a，显示隐藏文件

### pwd命令

功能：展示当前工作目录

语法：`pwd`

### cd命令

功能：切换工作目录

语法：`cd [目标目录]`

参数：目标目录，要切换去的地方，不提供默认切换到`当前登录用户HOME目录`

### mkdir命令

功能：创建文件夹

语法：`mkdir [-p] 参数`

- 参数：被创建文件夹的路径
- 选项：-p，可选，表示创建前置路径

### touch命令

功能：创建文件

语法：`touch 参数`

- 参数：被创建的文件路径

### cat命令

功能：查看文件内容

语法：`cat 参数`

- 参数：被查看的文件路径

### more命令

功能：查看文件，可以支持翻页查看

语法：`more 参数`

- 参数：被查看的文件路径
- 在查看过程中：
  - `空格`键翻页
  - `q`退出查看

### cp命令

功能：复制文件、文件夹

语法：`cp [-r] 参数1 参数2`

- 参数1，被复制的
- 参数2，要复制去的地方
- 选项：-r，可选，复制文件夹使用

示例：

- cp a.txt b.txt，复制当前目录下a.txt为b.txt
- cp a.txt test/，复制当前目录a.txt到test文件夹内
- cp -r test test2，复制文件夹test到当前文件夹内为test2存在

### mv命令

功能：移动文件、文件夹

语法：`mv 参数1 参数2`

- 参数1：被移动的
- 参数2：要移动去的地方，参数2如果不存在，则会进行改名

### rm命令

功能：删除文件、文件夹

语法：`rm [-r -f] 参数...参数`

- 参数：支持多个，每一个表示被删除的，空格进行分隔
- 选项：-r，删除文件夹使用
- 选项：-f，强制删除，不会给出确认提示，一般root用户会用到

> rm命令很危险，一定要注意，特别是切换到root用户的时候。

### which命令

功能：查看命令的程序本体文件路径

语法：`which 参数`

- 参数：被查看的命令

### find命令

功能：搜索文件

语法1按文件名搜索：`find 路径 -name 参数`

- 路径，搜索的起始路径
- 参数，搜索的关键字，支持通配符*， 比如：`*`test表示搜索任意以test结尾的文件

---

## 内容处理与管道

### grep命令

功能：过滤关键字

语法：`grep [-n] 关键字 文件路径`

- 选项-n，可选，表示在结果中显示匹配的行的行号。
- 参数，关键字，必填，表示过滤的关键字，带有空格或其它特殊符号，建议使用””将关键字包围起来
- 参数，文件路径，必填，表示要过滤内容的文件路径，可作为内容输入端口

> 参数文件路径，可以作为管道符的输入

### wc命令

功能：统计

语法：`wc [-c -m -l -w] 文件路径`

- 选项，-c，统计bytes数量
- 选项，-m，统计字符数量
- 选项，-l，统计行数
- 选项，-w，统计单词数量
- 参数，文件路径，被统计的文件，可作为内容输入端口

> 参数文件路径，可作为管道符的输入

### 管道符|

写法：`|`

功能：将符号左边的结果，作为符号右边的输入

示例：

`cat a.txt | grep itheima`，将cat a.txt的结果，作为grep命令的输入，用来过滤`itheima`关键字

可以支持嵌套：

`cat a.txt | grep itheima | grep itcast`

### echo命令

功能：输出内容

语法：`echo 参数`

- 参数：被输出的内容

### 反引号`

功能：被两个反引号包围的内容，会作为命令执行

示例：

- echo \`pwd\`，会输出当前工作目录

### tail命令

功能：查看文件尾部内容

语法：`tail [-f] 参数`

- 参数：被查看的文件
- 选项：-f，持续跟踪文件修改

### head命令

功能：查看文件头部内容

语法：`head [-n] 参数`

- 参数：被查看的文件
- 选项：-n，查看的行数

### 重定向符

功能：将符号左边的结果，输出到右边指定的文件中去

- `>`，表示覆盖输出
- `>>`，表示追加输出

---

## 系统与文件管理

### 软链接

功能：创建文件、文件夹软链接（快捷方式）

语法：`ln -s 参数1 参数2`

- 参数1：被链接的
- 参数2：要链接去的地方（快捷方式的名称和存放位置）

### 日期

语法：`date [-d] [+格式化字符串]`

### 时区

修改时区为中国时区

![image-20221027220554654](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027220554.png)

## 网络与主机配置

### ip地址

格式：a.b.c.d

- abcd为0~255的数字

特殊IP：

- 127.0.0.1，表示本机
- 0.0.0.0
  - 可以表示本机
  - 也可以表示任意IP（看使用场景）

查看ip：`ifconfig`

### 主机名

功能：Linux系统的名称

查看：`hostname`

设置：`hostnamectl set-hostname 主机名`

---

## 进程与端口管理

### ps命令

功能：查看进程信息

语法：`ps -ef`，查看全部进程信息，可以搭配grep做过滤：`ps -ef | grep xxx`

### kill命令

![image-20221027221303037](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221303.png)

### nmap命令

![image-20221027221241123](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221241.png)

### netstat命令

功能：查看端口占用

用法：`netstat -anp | grep xxx`

### ping命令

测试网络是否联通

语法：`ping [-c num] 参数`

![image-20221027221129782](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221129.png)

---

## 网络工具与监控

### wget命令

![image-20221027221148964](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221149.png)

### curl命令

![image-20221027221201079](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221201.png)

![image-20221027221210518](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221210.png)

### top命令

功能：查看主机运行状态

语法：`top`，查看基础信息

可用选项：

![image-20221027221340729](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221340.png)

交互式模式中，可用快捷键：

![image-20221027221354137](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221354.png)

### df命令

查看磁盘占用

![image-20221027221413787](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221413.png)

### iostat命令

查看CPU、磁盘的相关信息

![image-20221027221439990](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221440.png)

![image-20221027221514237](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221514.png)

[^教程]:自学教程来自：<https://www.bilibili.com/video/BV1n84y1i7td>
