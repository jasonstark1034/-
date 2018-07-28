# -
                                              关于贪心算法的初步认识
摘要
  1.渴婴问题：婴儿可以喝n种饮料，有的可口，有的不好喝，每种都具有满意值，第i瓶即为si，总量为ai，总需求量为t,问每种饮料为多少量时可满足其解渴。
  2.0/1背包问题：有n个物品和一个容量为c的背包，从n个物品中选取装包的物品。物品i的重量为wi，价值为pi。一个最佳背包装载指，物品总价值最高的可行背包装载。max(sum(pi*xi)),约束条件是sum(wi*xi)<=c,xi的01表示物品是否放入背包。
3.最小成本生成树：在n个顶点的无向网络G中，每棵生成树都有n-1条边，现在问题是如何选择n-1条边使他们形成G的最小成本生成树。列出2种不同的贪婪策略。       
解决
 1.
  渴婴问题中，即寻求一组实数xi，使sum(si*xi)最大，并满足sum(xi)=t,0<=xi<=ai。
在程序中输入： n, t, si, ai (1<=i<=n).    输出：实数xi，利用贪心算法
   使得sum(si*xi)=max, sum(xi)=t, 若sum(ai)<t,则输出反馈信息。
 2.
        从剩余的物品中选出可装入背包的价值最大的物品或装入重量最小的物品，或者选择装入pi/wi值最大的物品。以上皆是贪心启发式方法，不可保证得到最优解。首先将最多k件物品放入背包，若k件物品质量大于c，则放弃。否则，根据剩余容量，将剩余物品按pi/wi的递减顺序装入背包。考虑最多有k件物品的所有可能子集而得到的最优解即为启发式方法产生的解。
	 class Body{
   int id;// 物体的序号
   int w;// 物体的重量
   int p;// 物体的价值
List<Body> commonPackage( int[] w, int[] p, int m ){
    // 构造物体对象列表
    List<Body> bodys = new ArrayList<>();
    for ( int i=0; i<w.length; i++ ) 
    {
        bodys.add(new Body(w[i],p[i]));
    }
    // 对性价比从高到低排序
    Collections.sort(bodys, new Comaprator<Body>()
    {
        int compare(Body b1,Body b2)
       {return b2.p/b2.w-b1.p/b1.w;}
    })；
    // 将物体按照性价比从高到低依次加入背包
    int rest = m;// 剩余重量
    int i=0;
    List<Body> results=new ArrayList<>();// 存放结果集
    for(; i<bodys.size(); i++)
    {
        if ( rest<bodys.get(i).w )
            break;
        Body curBody = bodys.get(i);
        results.add(curBody);
        rest -= curBody.w;
    }
    // 计算最后一个物体能放入的部分
    Body lastBody = bodys.get(i);
    results.add(new Body(lastBody.id,rest,(lastBody.p*rest/lastBody.w));
}
 3.最小成本生成树
 （1）kruskal算法：		
	分步骤选择n-1条边，每步选择一条边。从剩下的边中选择一条成本最小且不会产生环路的边去加入已选择的边集。总共有n步，每次都从总边集中选出成本最小且不产生环路者，不重复选择即可。
  	伪代码：
           for(i=1;i++;i<=n)
   	   for(i=1;i++;i<=n)
	     	{p[a, b]=1; c[a, b]=0;}
	while ((E!=0)&&(T!=n-1))
           	{
		f=0;
            	for(i=1;i++;i<=n)
              	   for(i=1;i++;i<=n)
 			if (c[a, b]==1) k=k+p[a, b];
	     	if (k/2==1) f=1;
   		min(c);
 		 E=E-1;
   		 c[a, b]=1;
 		 W=W+L[a, b];
		 if(f==0)
  			T=T+1;
  			p[a, b]+=1;
		}
	if(T==n-1)
	printf(“%d”,W);
       else 
          printf(“no tree has been built”); 
（2）Prim 算法：
  	从剩余的边中，选择一条成本最小的，并且把它加入边集中形成一棵树。
         伪代码：
	T=0;
	TV=1;
	for(i=1;i++;i<=n)
   	   for(i=1;i++;i<=n)
	     	{p[a, b]=1; c[a, b]=0;}
         	while(E!=0)&&(T!=n-1)
	{
		min(cb[a+1,b],cb[a, b+1]);
		for(i=1;i++;i<=n)
              	   for(i=1;i++;i<=n)
 			if (c[a, b]==1) k=k+p[a, b];
	     	if (k/2==1) f=1;
		if(f==1) break;
		E=E-1;
		T=T+1;	
		c[a, b]=1;
		p[a, b]+=1;
	}
总结
  贪心算法是为解决最优化话问题而生的一种算法。也就是说，不从整体最优上加以考虑，它所做出的是在某种意义上的局部最优解。每个问题都有一组限制条件和优化函数。我们要做的是找出可行解以及近似最优解。
 选择的贪心策略必须具备无后效性，即某个状态以前的过程不会影响以后的状态，只与当前状态有关。
文献引用
  《数据结构算法与应用：c++语言描述》
   “CSDN博客摘要 ”
   《C语言教程》



Jason 
18.7.28
