---
id: 243
title: 'switch和多分支if else语句到底用谁？'
date: '2020-06-18T09:06:32+08:00'
author: Aaron
layout: post
guid: 'http://185.199.109.153/?p=243'
permalink: /2020/06/18/switch%e5%92%8c%e5%a4%9a%e5%88%86%e6%94%afif-else%e8%af%ad%e5%8f%a5%e5%88%b0%e5%ba%95%e7%94%a8%e8%b0%81%ef%bc%9f/
views:
    - '143'
seo_description_value:
    - 'switch和多分支if else语句到底用谁？'
seo_keywords_value:
    - if语句;switch语句
categories:
    - Programming
tags:
    - switch还是多if语句
---

大家都知道在Java中一共有两种选择语句分别是switch与if语句，但究竟什么时候用？用哪一种好呢？这一直是大家心中的一个小疑虑。

现在简单的回顾switch与if语句的基本构造，再深入了解它们的使用区别。

## 首先回顾下switch与if的基本结构

```text
switch(choose){    
    case 1:语句1;break;    
    case 2:语句2;break;    
    case 3:语句3;break;    
    default:默认语句;
}
```
上述是一个简单的switch语句的例子，根据choose的取值不同，选择不同的case语句执行；如果没有匹配任何case值，则执行默认语句。

注意事项：  
1.choose的数据类型有一定要求：可以为byte、short、char、int、String、枚举，当然不同的JDK版本对switch影响不同。  
2.choose一般建议是变量，当然也可以是常量。而case后面的值为常量，并且choose与case的值的数据类型要一致。  
3.还记得每个case语句后的break吗？break表示退出此switch语句，如果没有break，则case语句会继续执行下去。

以上是switch比较重要的知识点，做一个简单的回顾。

## 接下来回顾下if语句,if语句的样式就比较多了。  if语句分为三种：简单if语句、双分支if语句、多分支if语句

### 简单if语句
在代码中展示为：
```
if(条件){
    语句1
}
语句2
```
大家可以直接从代码中看出来，简单if语句，也就只有if的存在，作为一个简单的判断，不管语句1执不执行，并不妨碍下方语句2的执行。

回顾了简单的if语句，接下来再说说双分支if语句

### 双分支if语句

还记得什么是双分支if语句吗？  
是在简单if语句的基础上添加对立的条件else语句  
比如下面的代码：

```text
if(条件1){
    语句1
}else{
    语句2
}
语句3
```
通过条件1来判断是否需要执行语句1，如果条件1为真，则直接执行语句1；反之为假，则执行语句2。但是不管执行语句1或者语句2，语句3都会执行

双分支if语句中需要时刻了解其else的取值范围。

### 多分支if语句

什么是多分支if语句呢？就是在if…else的基础上，再加入更多的条件进行选择。
```
if(条件1){
    语句1
}else if(条件2){
    语句2
}else{
    语句3
}
语句4
```
由于出现了一个else if，则每个判断的取值发生了变化，但在多分支if语句中，我们虽然可以像下面的代码一样添加更多的else if条件，但是选中的语句只会有一个，也就是说语句1、2、3只会有一个执行，谁先执行后面的就直接无效了，但并不影响语句4的执行。
```
if(条件1){
    语句1
}else if(条件2){
    语句2
}else if(条件3){
    语句3
}else{
    语句4
}
语句5
```
很多同学都已经掌握了上述的内容

接下来，来看一个不一样的if语句

### 双if语句

什么是双if语句呢？
```
if(条件1){//第一个if语句
    语句1
}if(条件2){//第二个if语句
    语句2
}
语句3
```
这个代码有点奇怪！一个代码中竟然连续出现多个if语句,那问题来了，到底执行哪一个if语句呢？答案是：都可能会执行，每个if语句间没有影响，不管是几个if语句，只要满足条件都会运行。

上述代码，条件1和条件2没有任何的关系，只要条件1满足就执行语句1，只要条件2满足就执行语句2，两者可能都会执行，当然，也可能都不执行；但请注意语句3一定会执行。

注意：不要把双if语句与多分支if语句傻傻分不清楚哟。

接下来进入我们的正题

## switch和if else语句到底用谁

面对switch于if else语句进行了基本结构的回顾。

从基本结构也可以看出其区别：

switch：主要是将choose中的值和某一个case值进行比较，而case值是一个确定的值。

if else：每个执行的语句前都会有一个条件，这个条件可以是类似x==0的这种匹配一个确定值的布尔表达式，也可以是x&gt;10的这种匹配一个范围的布尔表达式。

从它们的结构可以大致的分析出它们的用法区别，下面我们举几个例子来详细的表现出它们的区别。

例子1：将一个班级按照 0-59：E级 60-69：D级 70—79：C级 80—89：B级 90-100：A级的要求对输入的成绩进行等级评判

若使用if else语句
```
Scanner sc = new Scanner(System.in);
int x = sc.nextInt();//前两步骤是在获得输入值
if(x>=0&&x<60){//注意，区间范围之间需要使用&&/||或者&/|，来进行区间划分，而0<=x<60这种写法是禁止的
    System.out.println("E级")；
}else if(x>=60&&x<69){
    System.out.println("D级")；
}else if(x>=70&&x<79){
    System.out.println("C级")；
}else if(x>=80&&x<89){
    System.out.println("B级")；
}else if(x>=90&&x<=100){
    System.out.println("A级")；
}else{//当然，不能排除有些同学比较淘气，输入了小于0或者大于100的数据
    System.out.println("输入有误")；
}
```
而使用switch来完成该代码呢？
```
Scanner sc = new Scanner(System.in);
int x = sc.nextInt();//前两步骤是在获得输入值
switch(x/10){//由于0-100之间有100个数据，用case来一个一个进行划分很麻烦，
  //所以先让x/10这样的话如:70-79的区间/10，则都为7
  case 10:  //估计有同学会有疑问了，为什么10不做处理却要写出来呢？
  //原因是100/10等于10，所以有case 10选项，但是由于100和90-99的输出结果是相同的，
  //不写break，如果是100，则选择case 10，不输出，然后就直接执行case 9的语句，达到效果
  case 9:System.out.println("A级")；break;  
  case 8:System.out.println("B级")；break;  
  case 7:System.out.println("C级")；break;  
  case 6:System.out.println("D级")；break;  
  case 5:  
  case 4:  
  case 3: 
  case 2:  
  case 1:  
  //上面怎么那么多case语句没有执行的语句呢？
  //和之间的case 10是一样的，case 5/4/3/2/1/0的效果都是一样的，都需要输出E级，
  //如果选中0，1,2,3,4,5某一个值，最后都会执行case 0的效果
  case 0:System.out.println("E级")；break;  
  default:System.out.println("输入有误")；
}
```
从上面可以看出，if else语句在这道题里用起来感觉挺顺手的，而switch呢？就要复杂得多了。

我们再来看一个例子

例2：给出如下选项，并根据选项进行效果展示：  
输入1：则输出“普通攻击”；  
输入2：则输出“魔法攻击”；  
输入3：则输出“使用道具”；  
输入3：则输出“逃跑”；

当然，这道题更多出现在游戏的内容中

那如果我们使用if else语句该如何书写呢？
```
Scanner sc = new Scanner(System.in);
int x = sc.nextInt();//前两步骤是在获得输入值
if(x==1){
    System.out.println("普通攻击")；
}else if(x==2){
    System.out.println("魔法攻击")；
}else if(x==3){
    System.out.println("使用道具")；
}else if(x==4){
    System.out.println("逃跑")；
}else{//当然，依然会有同学比较淘气，不按常理出牌
    System.out.println("输入有误")；
}
```
而使用switch语句呢？
```
Scanner sc = new Scanner(System.in);
int x = sc.nextInt();//前两步骤是在获得输入值
switch(x){    
    case 1:System.out.println("普通攻击")；break;    
    case 2:System.out.println("魔法攻击")；break;    
    case 3:System.out.println("使用道具")；break;    
    case 4:System.out.println("逃跑")；break;    
    default:System.out.println("输入有误")；
}
```
从这个例子可以看出：switch写起来要比if else更为简洁，并且使用x==0这些方式写出来，难免感觉怪怪的。

综上两道题可以看出：switch更适用于有确切值的选择，而if else更适合用于进行范围判断的内容。

当然上述两道题可以互相转换，也就是说到底使用switch还是if else并没有严格要求，在恰当的地方使用恰当的方法是每个程序员需要深思熟虑的。

当然我们的讨论还没有结束，上面只是从例子说明了switch与if else的区别，接下来我们从它们的执行效率上来进行讲解。

## switch与if else的执行效率

单从JVM的执行效率上讲的话,switch的执行效率要高于if语句：

原因在于:switch语句在运行时，首先会生成一个“跳转表”来指示实际的case分支的地址，而这个“跳转表”的索引号与swtich中的case值是相等的，这样的话，switch就不用像if else那样，遍历所有的条件，直至找到正确条件，而仅仅只需要访问对应索引号的表项就可以到达定位分支的目的。

简单的说，switch会生成一个数据统计表，将case后面的值全部统计起来，匹配时先拿表中的数据进行比较，如果有则直接跳转到相应case语句；如果没有，则直接跳转到default语句。

那if else呢？其实刚刚我们已经简单的说了其工作流程，这里再次说明一下：

if else语句需要一条一条的去进行取值范围的判断，直到找到正确的选项位置，这样的话势必会浪费大量的时间。

所以，单从其运行的效率来看，switch语句要更胜一筹。

## 总结

1.switch语句由于它独特的case值判断方式，使其执行效率更高，而if else语句呢，则由于判断机制，导致效率稍慢。

2.到底使用哪一个选择语句，和当前的代码环境有关，如果是范围取值，则使用if else语句更为快捷；如果是确定取值，则使用switch更是一个不错的选择。

所有好的程序都是经过不断思考，不断琢磨，付出努力，最终得以完成的。