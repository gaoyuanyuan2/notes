## 其他
### 1、内存映射文件
#### 好处：
内存映射文件的好处是提高了I/O性能，尤其是在大文件上使用时。对于小文件，内存映射文件会导致浪费空间，因为内存映射始终与页面大小对齐，大多为4 KiB。因此，5 KiB文件将分配8 KiB，因此浪费了3 KiB。

由于两个原因，访问内存映射文件比使用直接读写操作更快。

首先，系统调用比程序本地内存的简单更改慢几个数量级。其次，在大多数操作系统中，实际映射的内存区域是内核的页面缓存（文件缓存），这意味着不需要在用户空间中创建副本。

某些应用程序级内存映射文件操作也比它们的物理文件操作更好。应用程序可以直接和就地访问和更新文件中的数据，而不是从文件的开头搜索或将整个编辑的内容重写到临时位置。由于内存映射文件是在页面内部处理的，因此线性文件访问（例如，在平面文件数据存储或配置文件中看到）仅在跨越新页面边界时才需要磁盘访问，并且可以写入更大的部分。单个操作中的文件到磁盘。

内存映射文件的一个可能的好处是“延迟加载”，因此即使对于非常大的文件也使用少量RAM。

尝试加载明显大于可用内存量的文件的全部内容可能会导致严重的抖动，因为操作系统从磁盘读入内存并同时将页面从内存写回磁盘。内存映射不仅可以完全绕过页面文件，还可以在编辑数据时加载较小的页面大小的部分，类似于用于程序的请求分页。

内存映射过程由虚拟内存管理器处理，虚拟内存管理器是负责处理页面文件的相同子系统。内存映射文件一次一页地加载到内存中。该页面大小是由操作系统以获得最佳性能选择。由于页面文件管理是虚拟内存系统的最关键元素之一，因此将文件的页面大小部分加载到物理内存中通常是非常高度优化的系统功能。

### 类型

有两种类型的内存映射文件：

#### 持久性

持久文件与磁盘上的源文件相关联。最后一个过程完成后，数据将保存到磁盘上的源文件中。这些内存映射文件适合处理非常大的源文件。

####  非持久性
非持久文件与磁盘上的文件无关。当最后一个进程使用该文件时，数据将丢失。这些文件适用于为进程间通信（IPC）创建共享内存。

### 缺点
选择内存映射文件I / O的主要原因是性能。尽管如此，还是可以进行权衡。由于系统调用开销和内存复制，标准I/O方法成本很高。

内存映射方法在次要页面错误中有成本当一个数据块加载到页面缓存中时，但尚未映射到进程的虚拟内存空间。在某些情况下，内存映射文件I/O可能比标准文件I/O慢得多。

内存映射文件的另一个缺点与给定体系结构的地址空间有关：大于可寻址空间的文件一次只能映射部分，这使得读取变得复杂。

例如，诸如Intel的IA-32之类的32位架构只能直接寻址4 GiB或更小的文件部分。各个程序可以使用更小的可寻址空间 - 通常在2到3 GiB的范围内，具体取决于操作系统内核。

底层文件上的I / O错误（例如，其可移动驱动器已拔出或光学介质被弹出，写入时磁盘已满等），而访问其映射内存时，

会将其作为POSIX上的SIGSEGV/SIGBUS信号报告给应用程序，并且Windows上的EXECUTE_IN_PAGE_ERROR结构化异常。访问映射内存的所有代码都必须准备好处理这些错误，这些错误在访问内存时通常不会发生。

只有具有MMU的硬件架构才能支持内存映射文件。在没有MMU的体系结构中，操作系统可以在发出映射请求时将整个文件复制到内存中，但如果只访问文件的一小部分，则这非常浪费和缓慢，并且只能用于文件这将适合可用的内存。

### 常用
对于内存映射文件，最常见的用途可能是大多数现代操作系统（包括Microsoft Windows和类Unix系统）中的进程加载器。当进程启动时，

操作系统使用内存映射文件来带来可执行文件，以及任何可加载的模块，进入内存执行。大多数内存映射系统使用称为请求分页的技术，其中文件以子集（每个页面一页）加载到物理内存中，并且仅在实际引用该页面时。

在可执行文件的特定情况下，这允许OS选择性地仅加载实际需要执行的过程映像的那些部分。

内存映射文件的另一个常见用途是在多个进程之间共享内存。在现代保护模式操作系统中，通常不允许进程访问分配给另一进程使用的存储器空间。（程序尝试这样做会导致无效的页面错误或分段违规。）有许多技术可用于安全地共享内存，而内存映射文件I / O是最受欢迎的技术之一。两个或多个应用程序可以同时将单个物理文件映射到内存并访问此内存。例如，Microsoft Windows操作系统为应用程序提供了一种机制，用于内存映射系统页面文件本身的共享段，并通过此部分共享数据。