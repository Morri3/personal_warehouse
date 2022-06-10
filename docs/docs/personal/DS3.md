# 数据结构错题整理（二）



1、若有 n 阶对称矩阵 A，以行序为主序方式，将其下三角形的元素(包括主对角线上所有元素)依次存放于一维数组B[1..(n(n+1))/2]中，则在 B 中确定 a[i, j]（i<j）的位置 k 的关系为  ：j(j-1)/2+i 

**解：** n阶对称矩阵中的元素满足下述条件：aij=aji，(1＜=i，j＜=n)。对称矩阵中的每一对数据元素可以共用一个存储空间，因此可以将n2个元素压缩存储到n(n+1)/2个元的空间中，即可以一维数组保存。

假设用一维数组B[n(n+1)/2]作为对称矩阵A的存储结构，则B[k]和矩阵元素aij的下标i、j的对应关系为：

当i＞-j时，k=i(i-1)/2+i；

当i＜j时，k=j(j-1)/2+i；

(以上公式是针对aij和aji保存在同一个单元中的情况)

因为存储下三角元素，所以i＜j，k=j(j-1)/2+i。

2、数组 A[0..5, 0..6] 的每个元素占 5 个字节，将其按列优先次序存储在起始地址为 1000 的内存单元中，则元素 A[5, 5] 的地址是( 1175)。

**解：** a[5]的地址是1000+(5×6+5)×5=1175。

3、设矩阵A是一个对称矩阵，为了节省存储空间，将其下三角部分按照行优先存放在一维数组B[0..n(n+1)/2-1]中，对于下三角部分的任一元素a{i,j}(i>=j，i和j从0开始取值），在一维数组B中的下标k的值是i(i+1)/2+j

**解**：前i-1行共有（首项+末项）*项数/2 = i(i+1)/2，加上第i行的j个数，就是总共的。

4、若有 n 阶对称矩阵 A，以行序为主序方式，将其下三角形的元素(包括主对角线上所有元素)依次存放于一维数组B[1..(n(n+1))/2]中，则在 B 中确定 a[i, j]（i<j）的位置 k 的关系为___j*(j-1)/2+i___ 

5、The inorder traversal sequence of an AVL tree must be in sorted (non-decreasing) order.

根据二叉搜索树性质，中序遍历一定是有序的，而且是递增的。

6、If the depth of an AVL tree is 5 (the depth of an empty tree is defined to be −1), then the minimum possible number of nodes in this tree is:

**解**：由AVL树的递推公式Nh = Nh-1 +Nh-2 +1得，深度为5的AVL数最少结点是20（空树深度为-1）

7、In a disjoint set problem, given a set of m elements S = { 1, 2, 3, ..., m } and n ( 0<n<m ) distinct relations, the set S must have _m-n_ equivalence classes.

在一个不交集问题中，给定一组m元素S={1,2,3,…,m}和n（0<n<m）不同的关系，集S必须有m-n等价类。

8、Let T be a tree created by union-by-size with N nodes, then the height of T can be at most log2(N)+1.

9、critical path关键路径

10、就平均查找长度而言，折半查找>分块查找>顺序查找。

11、Given a sequentially stored list L of 16 sorted records. If binary search is used to find a record that does not exist, then the maximum number of comparisons is:

 A.4

 B.5

 C.6

 D.7

**正确答案：** B

**解析：** 循环结束条件为left>right。例如有n个数，第一次比较剩余n/2个数，第二次比较剩余n/22个数，第三次比较剩余n/23个数，……，倒数第二次比较剩余一个数，最后一次比较时最后一个数也要比较，因为可能key不存在这个序列中。故二分查找的最大比较次数（最坏情况）：log2N + 1

12、高度为 5 的 3 阶 B 树含有的关键字个数至少是 （31）

**解：** 3阶，每个结点的关键字个数是[[m/2]向上取整,m]，即[2,3]，所以每层结点都有两个关键字，同时是满二叉树，就是2^5-1=31

13、一棵有21个数字的、度为3的B+树最多有 _4_ 个度为3的结点。（画图！！）

**解：** 2x+3y=21,x为度为2的结点个数，y为度为3的结点个数. 要使y最多。当x=6，y=3时，该B树总共有9个非叶子结点，第二层总共有3个度为3的结点，第一层有一个度为3的结点，故总共有4个。

14、一棵有21个数字的、度为3的B+树最多有 _7_ 个度为2的结点（画图！！）

**解：** 2x+3y=21,x为度为2的结点个数，y为度为3的结点个数.要使x最多。当x=9，y=1时，该B树总共有10个非叶子结点，第三层总共有2个度为3的结点、2个度为2的结点，第二层有2个度为2的结点，第一层总共有1个度为2的结点故总共有7个。

15、下列关于m阶B-树的说法错误的是（C）。

A.根结点至多有m棵子树

B.所有叶子都在同一层次上

C.除根结点非叶结点至少有m/2 (m为偶数)或m/2+1（m为奇数）棵子树

D.根结点中的数据是有序的

16、Which of the following statements concerning a B+ tree of order M is FALSE?（C）

A. The root has at most M children

B. All leaves are at the same depth

C. All nonleaf nodes have between [M/2] and M children

D. Keys in any node are ordered

17、外排序中，给定 1000 个段和 8 条磁带。如果使用简单的 k 路归并，则最少要执行 5 趟（段的生成不算在内）  答案T

**解**：logk（N/M）= logk125.当k小于5，次数都太大。k取5时，归并次数=3，k取125时，归并次数=1。所以k=5

18、The first 9 numbers of 3-order Fibonacci numbers are 0,0,1,1,2,4,7,13,24.

19、For the purpose of parallel operations, we need 2k input buffers and 2 output buffers for a k-way merge. 为了实现并行操作，我们需要2k个输入缓冲区和2个输出缓冲区来进行k路合并。

20、Suppose that the internal memory can handle M records at a time, replacement selection can generate a longer run up to a maximun of 2M. 假设内存一次可以处理M条记录，那么替换选择可以产生更长的运行时间，最大可达2M。

**答案：** F

21、给定13段有序列以及4条磁带用于做外部排序。如果我们应用3路多相归并、以及Fibonacci分割，则必须执行多少轮归并（初始有序段的生成不算在内）？ __4__

22、Given that problem A is NP-complete. If problem B is in NP and can be polynomially reduced to problem A, then problem B is NP-complete.

**答案：** F

23、Let X be a problem that belongs to the class NP. Then which one of the following is TRUE?

**答案：** If X is NP-hard, then it is NP-complete.

24、A balanced binary search divides the sequence into 50%:50% equal sized subsequences. Now we define the unbalanced binary search to be always dividing the sequence into 1%:99% subsequences. That is, we always test at the position corresponding to the fraction 1/100 of the input of size N (e.g., if N=1000, we will test the position 10 of the array). So the binary search still take O(logN) time. 

平衡二进制搜索将序列分成50%：50%大小相等的子序列。现在我们定义非平衡二进制搜索总是将序列分成1%：99%的子序列。也就是说，我们总是在大小为N的输入的分数1/100对应的位置进行测试（例如，如果N=1000，我们将测试数组的位置10）。所以二进制搜索仍然需要O（logN）时间。

25、对于递推方程 T(N)=aT(N/b)+f(N)，若存在常数 K>1 使得 af(N/b)=Kf(N)，则有 T(N)=Θ(f(N))  

**答案：** F

26、For the recurrence equation T(N)=aT(N/b)+f(N), if af(N/b)=f(N), then T(N)=Θ(f(N)logbN). 

**答案：** T

27、How many of the following sorting methods use(s) Divide and Conquer algorithm?

•	Heap Sort

•	Insertion Sort

•	Merge Sort

•	Quick Sort

•	Selection Sort

•	Shell Sort

**答案：** 2

**解析：** 快排和归并

28、分法法的设计思想是将一个难以直接解决的大问题分割成规模较小的子问题，分别解决子问题，最后将子问题的解组合起来形成原问题的解，这要求原问题和子问题：问题规模不同，问题性质相同。 

29、用分治法解决一个规模为N的问题。若每步将问题分成规模均为N/5的4个子问题，且治而得到解的步骤耗时O(logN)，则整个算法的时间复杂度为多少？

**答案：** O(Nlog4/log5)

30、贪心基本解决问题的方案就是：

#1.尽可能在局部找到一个最优的解

#2然后证明这个局部的优化解是全局优化解的一部分

#3最后把这个局部解用递归或者迭代的方式推广到全局。

31、令 C 为字母集，其中每个字符 c 有对应频率 c.freq。若 C 的大小为 n，则其中任一字符 c 的最优前缀编码长度都不会超过 n−1.

**答案：** T

32、给定一段文本中的 4 个字符 (u,v,w,x) 及其出现频率 (fu,fv,fw,fx)。若对应的哈夫曼编码为 u: 00, v: 010, w: 011, x: 1，则下列哪组频率可能对应 (fu,fv,fw,fx)？

**答案：** 30, 21, 12, 33

**解析：** 画图，u>v,u>w,同时u<x

33、适于对动态查找表进行高效率查找的组织结构是(  C )。

A．有序表

B．分块有序表

C．三叉排序树

D．线性链表

34、若有向图G存在拓扑排序序列，则G一定不是强连通的。

35、在N皇后问题中，由于其对应的决策树有N!个叶子结点，所以解决此问题的空间复杂度是Ω(N!)  

**答案：** F

36、只有当局部最优跟全局最优解一致的时候，贪心法才能给出正确的解。

37、Let S be the set of activities in Activity Selection Problem. Then there must be some maximum-size subset of mutually compatible activities of S that includes the earliest finish activity am.

让S成为活动选择问题中的活动集。那么，必须有一些相互兼容的活动的最大大小子集，其中包括最早的完成活动am。

38、一个问题可用动态规划法或贪心法求解的关键特征是问题的最优子结构性质。

39、动态规划的基本要素为最优子结构性质与重叠子问题性质。