博弈算法
---
巴什博弈

问题描述

有一堆石子，共计n颗，规定二人每次拿1~m颗石头，先拿完者胜，求解先手是否能赢。

算法思路

因为最多是拿m颗石子，只要先手面对的n是m+1的整倍数颗石子，那么先手必败。
若先手面对的不是m+1的整倍数颗石子，那先手只需将剩余石子变成m+1的整数倍即可，先手必胜。

应用

[http://acm.hdu.edu.cn/showproblem.php?pid=2149](http://acm.hdu.edu.cn/showproblem.php?pid=2149)

	问题描述：
	虽然不想，但是现实总归是现实，Lele始终没有逃过退学的命运，因为他没有拿到奖学金。
	现在等待他的，就是像FarmJohn一样的农田生涯。
	要种田得有田才行，Lele听说街上正在举行一场别开生面的拍卖会，拍卖的物品正好就是一块20亩的田地。于是，Lele带上他的全部积蓄，
	冲往拍卖会。
	后来发现，整个拍卖会只有Lele和他的死对头Yueyue。
	通过打听，Lele知道这场拍卖的规则是这样的：刚开始底价为0，两个人轮流开始加价，不过每次加价的幅度要在1～N之间，当价格大于或等于田地
	的成本价 M 时，主办方就把这块田地卖给这次叫价的人。
	Lele和Yueyue虽然考试不行，但是对拍卖却十分精通，而且他们两个人都十分想得到这块田地。所以他们每次都是选对自己最有利的方式进行加价。
	由于Lele字典序比Yueyue靠前，所以每次都是由Lele先开始加价，请问，第一次加价的时候，
	Lele要出多少才能保证自己买得到这块地呢？
	input：
	本题目包含多组测试，请处理到文件结束(EOF)。每组测试占一行。
	每组测试包含两个整数M和N(含义见题目描述，0<N，M<1100)
	output：
	对于每组数据，在一行里按递增的顺序输出Lele第一次可以加的价。两个数据之间用空格隔开。
	如果Lele在第一次无论如何出价都无法买到这块土地，就输出"none"。
	
代码

    public class BashGame {
	    public static void main(String[] args) {
	        int M;
	        int N;
	        Scanner in = new Scanner(System.in);
	        while (true){
	            M = in.nextInt();
	            N = in.nextInt();
	            if (N >= M) {
	                for (int i = M; i <= N; i++)
	                    System.out.print(i + " ");
	                System.out.println();
	            }
	            else if (M % (N + 1) == 0)
	                System.out.println("none");
	            else
	                System.out.println((M % (N + 1)));
	        }
	    }
	}

---
威佐夫博弈

问题描述

有两堆石子，两个玩家可以（1）从两堆石子中分别取相同数目的石子（2）从一堆石子中取任意数目的石子，求解先手是否能赢。

算法思路

奇异局势：先手必败局势，（0，0）一定是奇异局势，以此类推（1，2），（3，5），（4，7），（6，10），（10，13），（9，15）......
可以发现，奇异局势（a[k]，b[k]）:b[k] = a[k] + k，a[k]是前面没有出现过的最小自然数。

奇异局势有以下三条性质：

1.任何自然数都包含在唯一一个奇异局势之中。

2.任意操作都可将奇异局势变为非奇异局势。

3.方法适当，非奇异局势可以变为奇异局势。


那么任给一个局势（a，b），怎样判断它是不是奇异局势呢？我们有如下公式：

    ak =[k（1+√5）/2]，bk=ak + k  （k=0，1，2，…,n 方括号表示取整函数)

奇妙的是其中出现了黄金分割数（1+√5）/2 = 1。618…,因此,由ak，bk组成的矩形近似为黄金矩形，

由于2/（1+√5）=（√5-1）/2，

先求出 k =a（√5-1）/2，

若a=(int) (k（+√5）/2 ),

那么a = ak，bk= ak + k，若不等于，那么a = ak+1，bk+1 = ak+1+ k + 1，

若都不是，那么就不是奇异局势。然后再按照上述法则进行，一定会遇到奇异局势。

（此处复制粘贴）

应用

[http://acm.hdu.edu.cn/showproblem.php?pid=1527](http://acm.hdu.edu.cn/showproblem.php?pid=1527)

	有两堆石子，数量任意，可以不同。游戏开始由两个人轮流取石子。游戏规定，每次有两种不同的取
	法，一是可以在任意的一堆中取走任意多的石子；二是可以在两堆中同时取走相同数量的石子。最后
	把石子全部取完者为胜者。现在给出初始的两堆石子的数目，如果轮到你先取，假设双方都采取最好
	的策略，问最后你是胜者还是败者。

	input：输入包含若干行，表示若干种石子的初始情况，其中每一行包含两个非负整数a和b，表示两堆
	石子的数目，a和b都不大于1,000,000,000。

	output：输出对应也有若干行，每行包含一个数字1或0，如果最后你是胜者，则为1，反之，则为0。

代码

    public class WythoffGame {
	    public static void main(String[] args) {
	        double q = (Math.sqrt(5) + 1) / 2;
	        int a;
	        int b;
	        Scanner in = new Scanner(System.in);
	        while (true){
	            a = in.nextInt();
	            b = in.nextInt();
	            if (a > b){
	                int t = a;
	                a = b;
	                b = t;
	            }
	            int k = b - a;
	            if (a == (int)(q * k))
	                System.out.println("0");
	            else
	                System.out.println("1");
	        }
    	}
	}


