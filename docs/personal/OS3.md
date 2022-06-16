### 操作系统原理实验错题&知识点

一、常见信号

SIGHUP（1）：从终端挂断或退出正在运行的前台进程

kill -1

SIGINT（2）：中断（同Ctrl-C）

kill -2

SIGKILL（9）：强制杀死该进程。该信号不能被捕获或忽略，同时接收该信号的进程在收到该信号时不能执行任何清理。

kill -9

SIGALRM（14）：闹钟。

（Kill默认情况）SIGTERM（15）：终止。发送信号给进程，告诉进程，你需要被关闭，请自行停止运行并退出。

kill -15

SIGUSR1（16）：用户自定义信号1

SIGUSR1（17）：用户自定义信号2

二、进程管理重要命令

查看进程

ps [选项] 查看进程静态统计信息

top [选项] 查看进程动态信息，每3s刷新一次

pstree [选项] 查看进程树，明确进程间父子关系

启动进程

Shell命令& 手工启动——后台启动

控制进程

kill [-9] 进程号 根据进程号PID强制终止进程和子进程

三、进程

1、创建pid_t fork(void);   头文件#include<unistd.h>     #include<sys/types.h>

2、获取进程标识号pid_t getpid(void);          pid_t getppid(void);

3、等待子进程终止      头文件#include<sys/wait.h>    #include<sys/types.h>

pid_t wait(int *status);

4、正常终止void exit(int status);

四、POSIX线程    头文件#include<pthread.h>

1、创建int pthread_create(pthread_t *thread, const pthread_attr_t *attr, void *(*start_routine) (void *), void *arg);

2、终止void pthread_exit(void *retval);

3、等待int pthread_join(pthread_t thread, void **retval);

4、创建互斥锁int pthread_mutex_init(pthread_mutex_t *restrict mutex,const pthread_mutexattr_t
*restrict attr);

5、锁定互斥锁（P操作）int pthread_mutex_lock(pthread_mutex_t *mutex);

6、解除互斥锁（V操作）int pthread_mutex_unlock ( pthread_mutex_t *mutex );

五、POSIX信号量    头文件#include<semaphore.h>

1、初始化int sem_init(sem_t *sem,int pshared,unsigned int value);

2、信号量-1（P操作）int sem_wait(sem_t *sem);

3、信号量+1（V操作）int sem_post(sem_t *sem);

4、获取信号量的值int sem_getvalue(sem_t *sem);

六、System Ⅴ信号量    头文件#include<sys/sem.h>

1、创建信号量semget()

2、改变信号量值semop()

七、进程通信——信号

1、设置信号  头文件#include<signal.h>

（1）void (*signal(int signum,void(* handler) (int)))(int);

（2）int sigaction(int signum,conststruct sigaction *act,struct sigaction *oldact));

2、向任何进程/进程组发送任何信号  头文件#include<signal.h>    #include<sys/types.h>

（1）kill(pid_t pid, int sig);

（2新）int sigqueue(pid_t pid, int sig,const union sigval val)

3、定时发送SIGALRM的信号：unsigned int alarm(unsigned int seconds)

4、让进程暂停直到信号出现：int pause(void);

八、进程通信——共享内存

1、创建  头文件#include <sys/ipc.h>            #include <sys/shm.h>

int shmget(key_t key, size_t size, int shmflg)

2、映射  头文件#include <sys/types.h>           #include <sys/shm.h>

void *shmat(int shmid, const void *shmaddr, int shmflg)

映射到调用进程的地址空间，随后就可方便地对共享区域进行访问操作

3、解除映射  头文件#include <sys/types.h>       #include <sys/shm.h>

int shmdt(const void *shmaddr)

解除进程对共享内存区域地映射

4、共享内存管理  头文件#include <sys/types.h>   #include <sys/shm.h>

int shmctl(int shmid, int cmd, struct shmid_ds *buf)

九、进程通信——管道

int pipe(fildes);

int fildes[2];

建立进程间通信，返回两个描述

fildes[0]读管道

fildes[1]写管道

十、进程通信——消息队列

1、创建或访问 int msgget(key_t key,int msgflg);

2、操作——发送消息int msgsnd(int msqid,const void *msg,size_t nbytes,int msgflg); 

3、操作——接收消息ssize_t msgrcv(int msqid,void *msg,size_t nbytes,long msgtype,int msgflg);

4、控制int msgctl(int msqid,int cmd,struct msqid_ds *buf);

十一、常见设备文件

1、SCSI设备：/dev/sd[a-z]

2、虚拟终端：/dev/tty[0-63]

3、/dev/cdrom

十二、下述代码运行后，共产生（4）个进程，输出（8）个字符'a'？

```
#include <stdio.h>
#include <sys/types.h> 
#include <unistd.h> 
int main(void)
{
    int i；
    for(i=0; i<2; i++)
    {
        fork();
        printf("a");
    }
    wait(NULL); 
    wait(NULL);
    return 0;
}
```

**解析**：i=0，父进程通过fork生成一个子进程，父进程和子进程各输出一个a。
i=1，因为没有\n，缓冲区未清空，两个进程各输出一个a，两个进程各自通过fork生成一个子进程，此时共4个进程，然后4个进程各自输出一个a，故总共输出8个a。

十三、下述代码运行后，共产生（4）个进程，输出（6）个字符'a'？

```
#include <stdio.h>
#include <sys/types.h> 
#include <unistd.h> 
int main(void)
{
    int i；
    for(i=0; i<2; i++)
    {
        fork();
        printf("a\n");
    }
    wait(NULL); 
    wait(NULL);
    return 0;
}
```

**解析**：因为有\n，所以缓冲区会被清空，产生4个进程，输出6个a。

十四、收到信号的进程对各种信号有不同的处理方法。处理方法可以分为三类：第一种是类似中断的处理程序，对于需要处理的信号，进程可以指定处理函数，由该函数来处理：第二种方法是，忽略某个信号，对该信号不做任何处理，就像未发生过一样;第三种方法是，对该信号的处理保留系统的默认值。进程通过系统调用（signal、sigaction）来指定进程对某个信号的处理行为。

十五、下列哪些函数或系统调用涉及发送信号：

A、signal()           进程通信——信号 创建

B、alarm()           进程通信——信号 发送ALRM信号

C、sigqueue()        进程通信——信号 发送

D、sigaction()        进程通信——信号 创建

E、raise() 

F、pause()           进程通信——信号 挂起直至信号出现

G、kill()             进程通信——信号 发送信号

**答案：**BCEG

十六、如果在代码中没有使用IPC_RMID命令手动删除共享内存，则共享内存并不会随着进程的终止而自动清理。  √

十七、消息队列的数据结构msgid_ds中登记了消息的最后发送进程的PID,和最后接收进程的PID。

**答案**：×    包含最后发送进程的时间和最后接收进程的时间。

十八、一般在一个进程中先用pipe创建管道，再用fork创建子进程，然后通过管道，再用fork创建子进程，然后通过管道实现父子进程间的通信。

十九、在创建Linux分区时，至少要创建的两个分区是：SWAP/根分区

二十、查看Linux kernel版本信息的命令：uname

二十一、下列关于Linux内核的说法，正确的是：A

A、Linux有多种发行版本，如ubuntu、debian。但是其内核均道循GNU的GPL。

B、内核源代码通过编译，生成可执行代码文件后，必须安装在/boot目录下，才起作用。

C、内核源代码只要通过编译，生成了可执行代码文件（例如bzimage），就起作用了。

D、Linux的内核，绝大部分源代码是公开的，除了极少量与CPU类型密切相关的代码段。

二十二、Linux操作系统内核使用哪种操作系统结构：单内核（宏内核）结构

二十三、在Linux进程管理的重要数据结构task_struct中，volatile long state表示进程状态，unsigned int flags表示进程标志

二十四、Linux的目录结构中，/dev存放设备相关文件，/usr/src存放源代码，/proc是虚拟目录，是系统内存的映射，访问内存信息：cat /proc/meminfo，访问CPU信息：cat /proc/cpuinfo

二十五、Linux内核支持几平所有的CPU架构。为此，满足特定CPU特定要求的操作代码，可以在（/arch）子目录找到

二十六、Linux内核主要由 进程调度、内存管理、虚拟文件系统、网络接口、进程间通信 五个子系统组成

二十七、Linux操作系统支持的进程间通信机制：信号Signals、管道Pipe、命名管道Named Pipe、System Ⅴ的IPC机制（信号量Semaphore、消息队列机制Message Queues Mechanism、共享内存Shared Memories）…

二十八、Linux内核源代码目录：/arch体系结构，/drivers设备驱动程序，/ipc包含核心进程间的通信代码，/kernel内核管理的核心代码

二十九、在Linux内核中，进程标识符PID为0的进程是：空闲进程。进程标识符PID为1的进程是：init/systemd进程（进程1）

三十、How could you get a list of all running processes?

**答**：ps ax

三十一、Linux进程：是运行的程序，是程序的一次动态执行过程，是在自身的虚拟地址空间运行的一个单独程序。

重要数据结构：PCB进程控制块

三十二、Linux进程状态：

TASK_RUNNING运行状态

TASK_INTERRUPTIBLE可中断的睡眠状态

TASK_UNINTERRUPTIBLE不可中断的睡眠状态

TASK_STOPPED暂停状态

TASK_TRACED跟踪状态

EXIT_ZOMBIE僵尸状态

EXIT_DEAD僵尸撤销状态

三十三、ps命令返回的结果的STAT/S字段：进程当前的状态

三十四、结束进程方法：

<Ctrl+c>组合键               kill [-s 信号 | -p][ -a] 进程号

三十五、(signal)不属于Linux的文件

三十六、下述哪种IPC效率最高？

A、管道

B、共享内存    √

C、消息队列

D、信号

三十七、消息队列是采用链表数据结构实现的, writer 进程在链尾输入数据, read 进程在链首读出数据. 因此它只支持单向通信。         ×双向通信。

三十八、Linux系统中，文件描述符1表示：标准输出设备文件描述符。文件描述符0表示：标准输入设备文件描述符

三十九、（/dev/tty1）设备是字符设备，（IDE硬盘）是块设备

四十、分时系统不需要多道程序技术的支持。

×

四十一、进行程序的相对地址到物理地址的转换，就是地址重定位。

√

四十二、进程切换在内核态。

四十三、mutual exclusion互斥        critical section临界区    concurrent process 并行程序          Synchronization同步

四十四、分段存储管理每一段必须是连续的存储区

四十五、在固定分区分配中，每个分区的大小是：可以不同但预先固定

四十六、考虑页面置換算法，系统有m个物理块供调度，初始时全空，页面引用串长度为p，包含了n个不同的页号，无论用什么算法，缺页次数不会少于：n

四十七、进程在执行中发生了缺页中断，经操作系统处理后，应让其执行（被中断的那一条）指令。

四十八、共享内存允许两个或多个进程共享一定的存储区，因为不需要拷贝数据，所以这是最快的一种IPC。