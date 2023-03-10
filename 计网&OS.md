## 计算机网络

#### 计算机网络体系结构

![img](./assets/0fa6c237-a909-4e2a-a771-2c5485cd8ce0.png)

## UDP 和 TCP 的特点

- 用户数据报协议 UDP（User Datagram Protocol）是无连接的，尽最大可能交付，没有拥塞控制，面向报文（对于应用程序传下来的报文不合并也不拆分，只是添加 UDP 首部），支持一对一、一对多、多对一和多对多的交互通信。
- 传输控制协议 TCP（Transmission Control Protocol）是面向连接的，提供可靠交付，有流量控制，拥塞控制，提供全双工通信，面向字节流（把应用层传下来的报文看成字节流，把字节流组织成大小不等的数据块），每一条 TCP 连接只能是点对点的（一对一）。













### DNS工作原理

https://www.wangan.com/wenda/10364

##### DNS组成

整个 DNS 域名系统由三部分组成： DNS 域名空间、DNS 服务器和解析器。

DNS服务器分为根**DNS服务器、顶级域DNS服务器和权威DNS服务器**

![](./assets/beb6f887b32e4004a22922ce7d43c0a7.png)

设主机cse.sicnu.edu需要查询gaia.cs.umass.edu的ip地址，会发生的流程如下：

![](./assets/f232ffc56efe43b0bbd3f160a192e8a0.png)

**递归查询**：DNS服务器收到一个域名解析请求时，如果所要检索的资源记录不在本地，DNS服务器将和自己的上一层服务器交互，获得最终的答案，并将其返回给客户。
**迭代查询**：DNS服务器收到解析请求，首先在本地的数据库中查找是否有相应的资源记录，如果没有，则向客户（本地服务器）提供另外一个DNS服务器的地址，客户（本地服务器）负责把解析请求发送给新的DNS服务器地址

##### DNS工作流程

1. 当在浏览器中输入URL时，浏览器会先检查**自己的缓存**是否有域名IP的映射关系，有则直接使用IP进行通信
2. 如浏览器没有缓存，则操作系统检查**本地hosts文件**是否有域名IP的映射关系，有则使用IP进行通信
3. 如果hosts没有这个域名的映射，则查找**本地DNS解析器缓存**是否有映射关系，有则直接返回完成域名解析
4. 如果还未找到映射关系，首先会找TCP/IP参数中设置的首选DNS服务器，也就是本地DNS服务器，如果服务器已缓存了映射关系，则使用这个IP地址映射返回完成域名解析，此时解析不具有权威性。
5. 如果本地DNS服务器缓存已经失效，进行上述的递归查询和迭代查询操作。



域名具有层次结构，从上到下依次为：根域名、顶级域名、二级域名。

![img](./assets/b54eeb16-0b0e-484c-be62-306f57c40d77.jpg)

DNS 可以使用 UDP 或者 TCP 进行传输，使用的端口号都为 53。大多数情况下 DNS 使用 UDP 进行传输，这就要求域名解析器和域名服务器都必须自己处理超时和重传从而保证可靠性。

##### DNS工作流程

- 客户机提出域名解析请求，并将该请求发送给本地的域名服务器。
- 当本地的域名服务器收到请求后，就先查询本地的缓存，如果有该纪录项，则本地的域名服务器就直接把查询的结果返回。
- 如果本地的缓存中没有该纪录，则本地域名服务器就直接把请求发给根域名服务器，然后根域名服务器再返回给本地域名服务器一个所查询域 (根的子域) 的主域名服务器的地址。
- 本地服务器再向上一步返回的域名服务器发送请求，然后接受请求的服务器查询自己的缓存，如果没有该纪录，则返回相关的下级的域名服务器的地址。
- 重复第四步，直到找到正确的纪录。
- 本地域名服务器把返回的结果保存到缓存，以备下一次使用，同时还将结果返回给客户机。





### 浏览器工作原理

https://zhuanlan.zhihu.com/p/47407398

https://blog.csdn.net/weixin_45532305/article/details/11889912

https://baijiahao.baidu.com/s?id=1704953759036216124&wfr=spider&for=pc

##### 一、进程和线程

进程是资源分配的最小单位，线程是CPU调度的最小单位

进程和线程之间的关系

- 进程中的某一个线程出错，都会导致整个进程的崩溃
- 线程之间共享进程中的公共数据
- 当一个进程关闭之后，操作系统会回收进程所占的内存
- 进程之间的内容相互隔离

浏览器多进程

- 1个浏览器主进程：主要负责显示渲染进程生成的页面图层、用户交互、子管理进程、提供存储等功能
- 1个GPU进程：负责图形处理
- 1个网络进程：负责网络资源的下载
- 多个插件进程：负责页面中的插件运行，运行在沙箱模式下
- 多个渲染进程：每个tab页一个进程，互不影响，运行在沙箱模式下
- 渲染进程包括以下线程
  1. GUP渲染线程、
  2. js引擎线程
  3. 事件触发线程
  4. 定时触发器线程
  5. 异步http请求线程
  6. 合成线程
  7. IO线程

##### 二、浏览器渲染流程

1. 主线程解析HTML
2. 生成Layout Tree（布局树）
3. 布局计算
4. 分层，生成图层树
5. 绘制
6. 光栅化，生成位图
7. 合成
8. 显示界面







### HTTP

HTTP 协议，全称超文本传输协议（Hypertext Transfer Protocol）。HTTP 协议就是用来规范超文本的传输，超文本，也就是网络上的包括文本在内的各式各样的消息。

##### HTTP协议通信过程

1. 服务器在 80 端口等待客户的请求。
2. 浏览器发起到服务器的 TCP 连接（创建套接字 Socket）。
3. 服务器接收来自浏览器的 TCP 连接。
4. 浏览器（HTTP 客户端）与 Web 服务器（HTTP 服务器）交换 HTTP 消息。
5. 关闭 TCP 连接

##### HTTP协议的特点

1. 拓展性强，速度快，跨平台支持好
2. 支持C/S模式
3. 灵活：HTTP允许传输任意类型的数据对象
4. 无连接、无状态

##### HTTP方法

1. GET ：获取资源，参数在URL中，只支持ASCII码，会对中文进行编码，GET方法是安全的，因为他不会改变服务器状态，可缓存
2. POST ：传输实体文本，参数存储在请求主体中，支持标准字符集，POST方法是不安全的，多数情况下不可缓存。
3. HAEAD  ：获取报文首部，和GET方法类似，但是不返回报文实体主体部分，可缓存
4. PUT ：传输文件
5. PATCH ：对资源进行修改
6. DELETE ：删除文件
7. OPTIONS ：查询支持的方法，查询指定的URL支持的方法
8. CONNECT ：要求在与代理服务器通信时建立隧道，并实现用隧道协议进行TCP通信。主要使用SSL和TLS协议把通信内容加密后经网络隧道传输
9. TRACE ：追踪路径，客户端可以对请求消息的传输路径进行追踪，TRACE方法是让Web服务器端将之前的请求通信还给客户端的方法

##### HTTP状态码

| 状态码 | 类别                             | 含义                       |
| ------ | -------------------------------- | -------------------------- |
| 1XX    | Informational（信息性状态码)     | 接收的请求正在处理         |
| 2XX    | Success（成功状态码）            | 请求正常处理完毕           |
| 3XX    | Redirection（重定向状态码）      | 需要进行附加操作以完成请求 |
| 4XX    | Client Error（客户端错误状态码） | 服务器无法处理请求         |
| 5XX    | Server Error（服务器错误状态码） | 服务器处理请求出错         |

###### 常见的状态码

1. 100 Continue ：表明到目前为止都正常，客户端可以继续发送请求或者忽略这个响应
2. 200 OK ：请求被成功处理。
3. 201 Created ：请求被成功处理并在服务端创建了一个新资源。
4. 202 Accepted ：服务端已经接收到请求，但还没有处理。
5. 204 No Content ：请求发送成功，但是返回的响应报文不包含实体的主体部分，也就是没有返回任何内容
6. 301 Moved Permanently ： 资源被永久重定向了
7.  302 Found ：资源被临时重定向了
8. 304 Not Modified ：请求资源成功，但是服务端不返回资源，资源从本地缓存中读取。
9. 400 Bad Request ：请求报文中存在语法错误
10. 401 Unauthorized ：请求需要有认证信息，未认证就请求需要认证之后才能访问的资源。
11. 403 Forbidden ：请求被拒绝，一般处理非法请求
12. 404 Not Found ：请求的资源未找到
13. 500 Internal Server Error ：服务端出现了bug
14. 502 Bad Gateway ：作为网关或者代理工作的服务器尝试执行请求时，从远程服务器接收到了一个无效的响应
15. 503 Service Unavailable ：服务器暂时处于超负载或正在进行停机维护，现在无法处理请求

### HTTPS

HTTPS 是基于 HTTP 的，也是用 TCP 作为底层协议，并额外使用 SSL/TLS 协议用作加密和安全认证。默认端口号是 443，优点是保密性好，安全度高。

#### SSL/TLS 的工作原理

##### 非对称加密

非对称密钥加密，又称公开密钥加密（Public-Key Encryption），加密和解密使用不同的密钥。

公开密钥所有人都可以获得，通信发送方获得接收方的公开密钥之后，就可以使用公开密钥进行加密，接收方收到通信内容后使用私有密钥解密。

##### 对称加密

加密和解密使用同一密钥

#### HTTPS采用的加密方式

- 使用非对称密钥加密方式，传输对称密钥加密方式所需要的 Secret Key，从而保证安全性;
- 获取到 Secret Key 后，再使用对称密钥加密方式进行通信，从而保证效率。



### 域名

域名（Domain Name），又称网域，用于在数据传输时对计算机的定位标识。

由于IP地址不方便记忆并且不能显示组织的名称的特点等缺陷，设计出域名，使用网域名称系统（DNS）将域名和IP地址相互映射。

域名由两组或两组以上的ASCII或各国语言文字构成，各组字符间由点分隔开，最右边的字符成为**顶级域名**或一级域名，倒数第二组成为二级域名，倒数第三组称为三级域名，以此类推。

顶级域名分为三类

- 国家或地区顶级域名，例如.cn 、.jp 、.us等
- 通用顶级域名，例如.com、.net、.org等
- 新顶级域名，如.top、.xyz等

### 路由

#### 一、什么是路由

路由是指导报文转发的路径信息，通过路由可以确认转发IP报文的路径。 路由设备是依据路由转发报文到目的网段的网络设备，最常见的路由设备：路由器。 路由设备维护着一张**路由表**，保存着路由信息。

**设置路由器的主要目的是找到数据包从源到目的地的最有效路径**

路由中包含以下信息：

1. 目的网络：标识目的网段 
2. 掩码：与目的地址共同标识一个网段 
3. 出接口：数据包被路由后离开本路由器的接口 
4. 下一跳：路由器转发到达目的网段的数据包所使用的下一跳地址     这些信息标识了目的网段、明确了转发IP报文的路径。

#### 二、路由获取信息的方式

- 动态路由：路由器运行动态路由协议学习到的路由
- 静态路由：由网络管理员手动配置路由条目
- 直连路由：由设备自动生成指向本地直连网络

### VLAN（虚拟局域网）

用于在二层交换机上**分割广播域**的技术，就是VLAN。通过利用VLAN，我们可以自由设计广播域的构成，提高网络设计的自由度。

如果仅有一个广播域，可能会影响到网络整体的传输性能。比如计算机A需要和计算机B通信，计算机A必须先广播“ARP请求信息”，来尝试获取计算机B的MAC地址，ARP请求会被转发到同一网络中的所有客户机上，对每一台计算机的CPU造成负担，造成网络带宽和CPU运算能力的大量无谓损耗。

#### 实现VLAN的机制

- VLAN通过限制广播帧转发的范围分割了广播域。交换机收到广播帧后，只转发到属于同一VLAN的其他端口。
- 可以理解成将一台交换机在逻辑上分割成数台交换机。
- 不同VLAN相当于不同的广播域，要实现 不同VLAN之间的通信，需要路由器提供中继服务，成为**VLAN间路由**

![image-20230222152829476](./assets/image-20230222152829476.png)







# Linux

### 一、Linux文件类型

- **普通文件（-）** ： 用于存储信息和数据， Linux 用户可以根据访问权限对普通文件进行查看、更改和删除。比如：图片、声音、PDF、text、视频、源代码等等。
- **目录文件（d，directory file）** ：目录也是文件的一种，用于表示和管理系统中的文件，目录文件中包含一些文件名和子目录名。打开目录事实上就是打开目录文件。
- **符号链接文件（l，symbolic link）** ：保留了指向文件的地址而不是文件本身。
- **字符设备（c，char）** ：用来访问字符设备比如键盘。
- **设备文件（b，block）** ： 用来访问块设备比如硬盘、软盘。
- **管道文件(p,pipe)** : 一种特殊类型的文件，用于进程之间的通信。
- **套接字(s,socket)** ：用于进程间的网络通信，也可以用于本机之间的非网络通信。

### 二、Linux目录树

![Linux的目录结构](./assets/Linux目录树.b82202fa.png)

##### 常见目录

- **/bin：** 存放二进制可执行文件(ls、cat、mkdir 等)，常用命令一般都在这里；

- **/etc：** 存放系统管理和配置文件；

- **/home：** 存放所有用户文件的根目录，是用户主目录的基点，比如用户 user 的主目录就是/home/user，可以用~user 表示；

- **/usr ：** 用于存放系统应用程序；

- **/opt：** 额外安装的可选应用程序包所放置的位置。一般情况下，我们可以把 tomcat 等都安装到这里；
- **/proc：** 虚拟文件系统目录，是系统内存的映射。可直接访问这个目录来获取系统信息；
- **/root：** 超级用户（系统管理员）的主目录（特权阶级^o^）；
- **/sbin:** 存放二进制可执行文件，只有 root 才能访问。这里存放的是系统管理员使用的系统级别的管理命令和程序。如 ifconfig 等；
- **/dev：** 用于存放设备文件；
- **/mnt：** 系统管理员安装临时文件系统的安装点，系统提供这个目录是让用户临时挂载其他的文件系统；
- **/boot：** 存放用于系统引导时使用的各种文件；
- **/lib ：** 存放着和系统运行相关的库文件 ；
- **/tmp：** 用于存放各种临时文件，是公用的临时文件存储点；
- **/var：** 用于存放运行时需要改变数据的文件，也是某些大文件的溢出区，比方说各种服务的日志文件（系统启动日志等。）等；
- **/lost+found：** 这个目录平时是空的，系统非正常关机而留下“无家可归”的文件（windows 下叫什么.chk）就在这里。

### 三、Linux基本命令

#### 目录切换目录

- **`cd usr`：** 切换到该目录下 usr 目录
- **`cd ..（或cd../）`：** 切换到上一层目录
- **`cd /`：** 切换到系统根目录
- **`cd ~`：** 切换到用户主目录
- **`cd -`：** 切换到上一个操作所在目录

#### 目录操作命令（增删改查）

- **`mkdir 目录名称`：** 增加目录。

- **`ls/ll`**（ll 是 ls -l 的别名，ll 命令可以看到该目录下的所有目录和文件的详细信息）：查看目录信息。
- **`find 目录 参数`：** 寻找目录（查）。示例：① 列出当前目录及子目录下所有文件和文件夹: `find .`；② 在`/home`目录下查找以.txt 结尾的文件名:`find /home -name "*.txt"` ,忽略大小写: `find /home -iname "*.txt"` ；③ 当前目录及子目录下查找所有以.txt 和.pdf 结尾的文件:`find . \( -name "*.txt" -o -name "*.pdf" \)`或`find . -name "*.txt" -o -name "*.pdf"`。
- **`mv 目录名称 新目录名称`：** 修改目录的名称（改）。注意：mv 的语法不仅可以对目录进行重命名而且也可以对各种文件，压缩包等进行 重命名的操作。mv 命令用来对文件或目录重新命名，或者将文件从一个目录移到另一个目录中。后面会介绍到 mv 命令的另一个用法。
- **`mv 目录名称 目录的新位置`：** 移动目录的位置---剪切（改）。注意：mv 语法不仅可以对目录进行剪切操作，对文件和压缩包等都可执行剪切操作。另外 mv 与 cp 的结果不同，mv 好像文件“搬家”，文件个数并未增加。而 cp 对文件进行复制，文件个数增加了。
- **`cp -r 目录名称 目录拷贝的目标位置`：** 拷贝目录（改），-r 代表递归拷贝 。注意：cp 命令不仅可以拷贝目录还可以拷贝文件，压缩包等，拷贝文件和压缩包时不 用写-r 递归。
- **`rm [-rf] 目录` :** 删除目录（删）。注意：rm 不仅可以删除目录，也可以删除其他文件或压缩包，为了增强大家的记忆， 无论删除任何目录或文件，都直接使用`rm -rf` 目录/文件/压缩包。

#### 压缩文件操作命令

**1）打包并压缩文件：**

Linux 中的打包文件一般是以.tar 结尾的，压缩的命令一般是以.gz 结尾的。而一般情况下打包和压缩是一起进行的，打包并压缩后的文件的后缀名一般.tar.gz。 命令：`tar -zcvf 打包压缩后的文件名 要打包压缩的文件` ，其中：

- z：调用 gzip 压缩命令进行压缩
- c：打包文件
- v：显示运行过程
- f：指定文件名

比如：假如 test 目录下有三个文件分别是：aaa.txt bbb.txt ccc.txt，如果我们要打包 test 目录并指定压缩后的压缩包名称为 test.tar.gz 可以使用命令：**`tar -zcvf test.tar.gz aaa.txt bbb.txt ccc.txt` 或 `tar -zcvf test.tar.gz /test/`**

**2）解压压缩包：**

命令：`tar [-xvf] 压缩文件`

其中：x：代表解压

示例：

- 将 /test 下的 test.tar.gz 解压到当前目录下可以使用命令：**`tar -xvf test.tar.gz`**
- 将 /test 下的 test.tar.gz 解压到根目录/usr 下:**`tar -xvf test.tar.gz -C /usr`**（- C 代表指定解压的位置）

#### Linux权限命令

![img](./assets/Linux权限解读.7c1098a0.png)

**文件的类型：**

- d： 代表目录
- -： 代表文件
- l： 代表软链接（可以认为是 window 中的快捷方式）

**Linux 中权限分为以下几种：**

- r：代表权限是可读，r 也可以用数字 4 表示
- w：代表权限是可写，w 也可以用数字 2 表示
- x：代表权限是可执行，x 也可以用数字 1 表示

**文件和目录权限的区别：**

对文件和目录而言，读写执行表示不同的意义。

对于文件：

| 权限名称 | 可执行操作                  |
| :------- | :-------------------------- |
| r        | 可以使用 cat 查看文件的内容 |
| w        | 可以修改文件的内容          |
| x        | 可以将其运行为二进制文件    |

对于目录：

| 权限名称 | 可执行操作               |
| :------- | :----------------------- |
| r        | 可以查看目录下列表       |
| w        | 可以创建和删除目录下文件 |
| x        | 可以使用 cd 进入目录     |

**超级用户可以无视普通用户的权限，即使文件目录权限是 000，依旧可以访问。**

**修改文件/目录的权限的命令：`chmod`**

示例：修改/test 下的 aaa.txt 的权限为文件所有者有全部权限，文件所有者所在的组有读写权限，其他用户只有读的权限。

**`chmod u=rwx,g=rw,o=r aaa.txt`** 或者 **`chmod 764 aaa.txt`**

![image-20230307110053648](./assets/image-20230307110053648.png)

#### 用户管理

**Linux 用户管理相关命令:**

- `useradd 选项 用户名`:添加用户账号
- `userdel 选项 用户名`:删除用户帐号
- `usermod 选项 用户名`:修改帐号
- `passwd 用户名`:更改或创建用户的密码
- `passwd -S 用户名` :显示用户账号密码信息
- `passwd -d 用户名`: 清除用户密码

#### 其他常用命令

- **`pwd`：** 显示当前所在位置
- `sudo + 其他命令`：以系统管理者的身份执行指令
- **`grep 要搜索的字符串 要搜索的文件 --color`：** 搜索命令，--color 代表高亮显示
- **`ps -ef`/`ps -aux`：** 都是查看当前系统正在运行进程，两者的区别是展示格式不同。如果想要查看特定的进程可以使用这样的格式：**`ps aux|grep redis`** （查看包括 redis 字符串的进程），也可使用 `pgrep redis -a`。

​		注意：如果直接用 ps（（Process Status））命令，会显示所有进程的状态，通常结合 grep 命令查看某进程的状态。

- **`kill -9 进程的pid`：** 杀死进程（-9 表示强制终止。）先用 ps 查找进程，然后用 kill 杀掉

**网络通信命令：**

1. 查看当前系统的网卡信息：ifconfig
2. 查看与某台机器的连接情况：ping
3. 查看当前系统的端口使用：netstat -an

- **`shutdown`：** `shutdown -h now`： 指定现在立即关机；`shutdown +5 "System will shutdown after 5 minutes"`：指定 5 分钟后关机，同时送出警告信息给登入用户。

- **`reboot`：** **`reboot`：** 重开机。**`reboot -w`：** 做个重开机的模拟（只有纪录并不会真的重开机）。