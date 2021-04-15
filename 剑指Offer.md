# 剑指Offer 个人习题总结

## 1.数组中重复的数字
在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。
* 方法一:  遍历数组 HashSet  无重复数组
  ```
  class Solution {
    public int findRepeatNumber(int[] nums) {
        Set<Integer> set = new HashSet<Integer>();
        int repeat = -1;
        for (int num : nums) {
            if (!set.add(num)) {
                repeat = num;
                break;
            }
        }
        return repeat;
    }
  }
  ```

  

* 方法二 原地交换法 时间复杂度 O(n), 如果没有重复的数字，那么通过交换，可以让数组的下标与值一一对应
  ```
  class Solution {
    public int findRepeatNumber(int[] nums) {
    	for(int i = 0; i <= nums.length - 1; i++){
    		if(nums[nums[i]] == nums[i] && nums[i] != i){
    		return nums[i];
    		}
    		if(nums[i] != i){
    		int k = nums[nums[i]];
    		nums[nums[i]] = nums[i];
    		nums[i] = k;
    		}
    	}
    	return -1;
    }
  }
  ```

  

## 2.单例模式
创建一个类，该类只能存在一个实例
* 1. 将构造方法定义为私有方法(private 修饰)
* 2. 在该类中定义一个静态方法，在静态方法中创建对象
> 注意： 静态方法本身即同步方法，不需要考虑同步性
> ```
> public class Singleton(){
> privtae static final Singleton INSTANCE = new Singleton(); //私有的成员变量
> private Singleton(){}    //私有的构造方法
> public static Singleton getInstance(){
> return INSTANCE;
> }
> }
> ```
>
> 注意：这种方法，在第一次使用类Singleton的时候就会创建对象，过早的创建对象会导致内存利用率低。
> privtae static final Singleton 修饰确保该变量属于类，而不属于实例， 可以直接在类中调用变量， 但仅仅可以调用一次。
> JAVA 中， 内部类不可以使用static 修饰 变量与方法，所以以上已经式最优解。  

## 3. 二维数组中的查找
在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。
```
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        if(matrix == null || matrix.length == 0 || matrix[0].length == 0)
        return false;
        int i = 0;
        int j = matrix[0].length - 1;
        while(i <= matrix.length - 1 && j >= 0){
            if(matrix[i][j] == target)
            return true;
            if(matrix[i][j] > target){
                j--;
            }else{
                i++;
            }
        }
        return false;
    }
}
```



>  注意：二维数组的行列数，JAVA中二维数组本质是一维数组，且该一维数组的每个数都是一维数组的引用。  行数 a.length，列数 a[0].length
>  从右上角开始查找，如果元素比目标值大，那么列减少，如果比目标值小，那么行减少，如果超过了标记值还没有找到，那么就是没有

## 4. 请实现一个函数，把字符串 s 中的每个空格替换成"%20"。
```
    public static String replaceSpace(String s) {
        StringBuilder str = new StringBuilder();
        for (char c: s.toCharArray()) {
            if(c == ' '){
                str.append("%20");
            }else{
                str.append(c);
            }
        }
      return str.toString();
}
```

> 注意： 不可以直接使用split分割字符串，如果输入为"   "，使用分割字符串，分割出来的字符串数组为null
>        JAVA 中，数组被定义为不可改变的，底层为char[]， 但是被final修饰，但是字符串缓冲区， StringBuilder 底层没有被final修饰

## 5. 从尾到头打印链表
输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回).
链表的结构是单向的指向下一个节点，从尾到头的输出方式与栈相同，因而想到可以定义一个栈来进行输出

```
/*

 * Definition for singly-linked list.

 * public class ListNode {

 * int val;

 * ListNode next;

 * ListNode(int x) { val = x; }

 * }

   */

 * class Solution {
    public int[] reversePrint(ListNode head) {
        Stack<ListNode> stack = new Stack<ListNode>();
        ListNode l = head;
        while(l != null){
            stack.push(l);
            l = l.next;
        }
        int size = stack.size();
        int[] print = new int[size];
        for(int i =0; i < size ; i++){
            print[i] = stack.pop().val;
        }
        return print;
    }

}
```

>  注意： 递归的本质实际上是一个栈的结构，因而如果不需要以数组的形式输出的话，可以用递归的方式进行输出，
>  输出一个节点前，先输出其下一个结点的值，直到链表的末尾

## 6. 重建二叉树(二叉树的遍历)
前序遍历：先访问根结点，再访问左结点，最后访问右结点
中序遍历：先访问左结点，再访问跟结点，最后访问右结点
后序遍历：先访问左结点，再访问右结点，最后访问根结点
宽度优先遍历： 先访问第一层，再访问第二层，每一层中自左向右访问

定义二叉搜索树： 树的左子结点总小于等于跟结点，右子结点总是大于等于根结点 

题目：
输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

    class Solution {
           public TreeNode buildTree(int[] preorder, int[] inorder) {
               //类似C++的 指针式 迭代方法
           /* if(preorder == null || inorder == null || preorder.length == 0){
                return null;
            }
        return Solution.ConstructCore(preorder, 0, preorder.length -1, inorder, 0, inorder.length -1);
    }
    
    public static TreeNode ConstructCore(int[] preorder, int startPreorder, int endPreorder, int[] inorder, int startInorder, int endInorder){
        //前序遍历的第一个值为根结点
        int rootValue = preorder[startPreorder];
        TreeNode root = new TreeNode(rootValue);
    
        //只有一个结点时候直接返回
        if(startPreorder == endPreorder){
            if(startInorder == endInorder && preorder[startPreorder] == inorder[startInorder]){
                return root;
            }
        }
    
        //在中序遍历中找到根结点，并且划分左右子树
        int rootInorder = startInorder;
        while( rootInorder <= endInorder && inorder[rootInorder] != rootValue)
            rootInorder++;
    
        int leftLength = rootInorder - startInorder;
        int leftPreorderEnd = startPreorder + leftLength;
        if(leftLength > 0){
            //构建左子树.左子树开始的坐标加1，跳过根结点
            root.left = Solution.ConstructCore(preorder, startPreorder + 1, leftPreorderEnd, inorder, startInorder, rootInorder - 1);
        }
    
        //构建右子树
        if(leftLength < endPreorder - startPreorder){
            root.right = Solution.ConstructCore(preorder, leftPreorderEnd + 1, endPreorder, inorder, rootInorder + 1, endInorder);
        }
    
        return root;
        */
    
        if(preorder == null || inorder == null || prorder.length == 0){
            return null;
        }
    
        TreeNode root = new TreeNode(preorder[0]);
        Deque<TreeNode> stack = new LinkedList<TreeNode>();
        stack.push(root);
        int inorderIndex = 0;
    
        for(int i =1; i < preorder.length; i++){
            int preorderVal = preorder[i];
            TreeNode node = stack.peek();
            if( node.val!= inorder[inorderIndex]){
                node.left = new TreeNode(preorderVal);
                stack.push(node.left);
            }else{
                //找到栈顶元素不等于 中序遍历中的index，或者找到栈顶
                while( !stack.isEmpty() && stack.peek().val == inorder[inorderIndex]){
                    node = stack.pop();
                    inorderIndex++;
                }
    
                node.right = new TreeNode(preorderVal);
                stack.push(node.right);
            }
        }
    
        return root;
    }
    //递归法的另一种简便写法
    class Solution {
        private Map<Integer, Integer> indexMap;
    	public TreeNode myBuildTree(int[] preorder, int[] inorder, int preorder_left, int preorder_right, int inorder_left, int 	inorder_right) {
        if (preorder_left > preorder_right) {
            return null;
        }
    
        // 前序遍历中的第一个节点就是根节点
        int preorder_root = preorder_left;
        // 在中序遍历中定位根节点
        int inorder_root = indexMap.get(preorder[preorder_root]);
        
        // 先把根节点建立出来
        TreeNode root = new TreeNode(preorder[preorder_root]);
        // 得到左子树中的节点数目
        int size_left_subtree = inorder_root - inorder_left;
        // 递归地构造左子树，并连接到根节点
        // 先序遍历中「从 左边界+1 开始的 size_left_subtree」个元素就对应了中序遍历中「从 左边界 开始到 根节点定位-1」的元素
        root.left = myBuildTree(preorder, inorder, preorder_left + 1, preorder_left + size_left_subtree, inorder_left, inorder_root - 1);
        // 递归地构造右子树，并连接到根节点
        // 先序遍历中「从 左边界+1+左子树节点数目 开始到 右边界」的元素就对应了中序遍历中「从 根节点定位+1 到 右边界」的元素
        root.right = myBuildTree(preorder, inorder, preorder_left + size_left_subtree + 1, preorder_right, inorder_root + 1, inorder_right);
        return root;
    }
    
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        int n = preorder.length;
        // 构造哈希映射，帮助我们快速定位根节点
        indexMap = new HashMap<Integer, Integer>();
        for (int i = 0; i < n; i++) {
            indexMap.put(inorder[i], i);
        }
        return myBuildTree(preorder, inorder, 0, n - 1, 0, n - 1);
    }
>  注意：1. 数组int[] a = {} (数组长度为0) 与 int[] a = null (数组为空)不同； 数组为空，引用不指向任何内存，数组长度为0，引用指向一个长度为0的数组，
>         一般为了避免出错，先判断是否为空，再判断长度是否为0，if(preorder == null || inorder == null || preorder.length == 0)
>        ，数组为空读取长度会报错
>        前序遍历的第一个值一定为根结点，在中序遍历中找到根结点，便可将树划分为左子树，右子树，继而进一步迭代划分。
>        2. 利用栈进行构造，前序遍历，一定会一直按照左子树进行排列，直到遇到第一个没有左子树的结点，这个结点对应着中序排列的第一个值，且如果每一个结点都
>           不存在右结点的情况下，中序排列的顺序与前序排列相反。 用栈存储没有分配右儿子的结点，直到找到第一个右儿子。

## 7. 用两个栈实现队列
用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )
'''
class CQueue {
    Deque<Integer> stackIn; 
    Deque<Integer> stackOut;
    public CQueue() {
        stackIn = new LinkedList<Integer>();
        stackOut = new LinkedList<Integer>();
    }
    
    public void appendTail(int value) {
        /*if(!stackOut.isEmpty()){
            while(!stackOut.isEmpty()){
            stackIn.push(stackOut.pop());
            }
            stackIn.push(value);
        }else{
            stackIn.push(value);
        }
        */
        stackIn.push(value);
    }
    
    public int deleteHead() {
        int val = -1;
        if(!stackOut.isEmpty()){
            val = stackOut.pop();
        }else{
        while(!stackIn.isEmpty() ){
            stackOut.push(stackIn.pop());
        }
        if(!stackOut.isEmpty())
         val = stackOut.pop();
        }
        return val;
    }
}
'''

>  注意： stackIn与 stackOut并不一定要规定存在谁里面，压栈的时候总是向stackIn中压，弹栈的时候，如果stackOut不是空，直接弹stackOut，如果为空，
>         则，将stackIn中的全部压入stackOut，再弹，  需要考虑两个栈全为空的情况。

## 8. 旋转最小数字
把一个数组最开始的若干个数字搬到数组的末尾。  输入一个递增排序的一个数组的旋转，输出数组的最小元素。
分析： 部分有序的数组, 根绝旋转数组的规则，一般第一个元素大于等于最后一个元素，选择两个指针，一个指向开始，一个指向数组末尾，找到数组的中间值，如果大于lo，则表示该值属于前部递增的数组，如果小于，则表明属于后部递增数组，可以相应的改变lo和hi的值，直到lo与hi相邻，作为循环的结束条件。
'''
    public static int MinArray(int[] array){
        int lo = 0;
        int hi = array.length -1;
        int min = lo;
        //指向相邻的元素作为结束标志
        while(array[lo] >= array[hi]){

            if(lo == hi -1) {
                min = hi;
                break;
            }
    
            min = (lo + hi)/2;
            //如果三个数字相等，只能顺序查找
            if(array[lo] == array[hi] && array[lo] == array[min]){
                int numberMin = array[lo];
                for(int i = lo + 1; i <= hi; i++){
                    if(numberMin > array[i])
                        numberMin = array[i];
                }
                return numberMin;
            }
    
            if(array[lo] <= array[min]) lo = min;
            else if(array[min] <= array[hi]) hi = min;
    
        }
        return array[min];
    }
    }
'''

>  注意： 考虑到相同元素的时候，只能使用顺序查找
>         防止溢出，可以使用 lo + （hi - lo）/2  代替（lo + hi）/2；

## 9.斐波那契数列(递归与循环)(动态规划)
递归： 递归的代码往往更简洁，但是递归调用函数存在时间和空间的开销，严重的时候会导致调用栈的溢出
>  注意： 大数越界问题：在程序运算的过程中，变量可能超出 int32 甚至 int64 的取值范围。
>  解决方式： 1. 循环取余， 2. 快速幂取余  3. 二分取余
'''
    public int fib(int n) {
        int[] result = {0,1};
        if(n <= 1)
        return result[n];

        int  fibOne = 0;
        int  fibTwo = 1;
        int  fibN = 0;
    
        for(int i = 2; i <= n; i++){
            fibN = (fibOne + fibTwo) % 1000000007;
            fibOne = fibTwo;
            fibTwo = fibN;
        }
    
        return fibN;
    }
'''
>   注意： 大数越界问题的取余方式： %1000000007， 对int32来说 100000007足够大， 对int64来说， 10000007的平方也不会在其中溢出
>         如果使用递归来做，虽然看起来简洁，但是实际运算重复计算了很多项， 实际复杂度增加，动态规划式最简单的方式

## 10. 青蛙跳台阶问题(斐波那契数列变形)
一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法
>   分析： 跳第一级，只有一种方法，跳第二级，可以分两次，也可一次跳两级，从第三级开始，可以选择第一次跳一级还是两级，如果一级，那么为f(n-1)中剩下楼梯的跳法
>         如果跳2级，有f(n-2)种剩下楼梯的跳法。
'''
    public int numWays(int n) {
        int fibOne = 1;
        int fibTwo = 1;
        int fibN = 0;
        for(int i = 0; i < n; i++){
            fibN = (fibOne + fibTwo) %1000000007;
            fibOne = fibTwo;
            fibTwo = fibN;
        }

        return fibOne;
    
    }
'''

## 11. 二进制中1的个数
>  注意： 右移运算中，有符号的数，补位补的是符号位的值
>         JAVA 中 >>> 为无符号右移的操作
>         JAVA 中 int与boolean 不能等价，在条件判断时候，位与操作后的值不能作为判断条件
>         n&(n-1) 会让最右边一个1变为0，其余不变。
'''
    public int hammingWeight(int n) {
        int count = 0;
        /*int flag = 1;
        while(flag != 0){
            if((n & flag) != 0){
                count++;
            }
            flag = flag << 1;
        }
        return count;
        */

        while(n != 0){
            count++;
            n=n & (n-1);
        }
    
        return count;


    }
'''

## 12 数值的整数次方(快速幂次方)
实现函数double Power(double base, int exponent)，求base的exponent次方。不得使用库函数，同时不需要考虑大数问题。
>   注意： 底数的三种情况，指数的三种情况
>       JAVA 中int32的范围为  n∈[−2147483648,2147483647]， 因此，如果指数为−2147483648，取正会溢出，将其放在long中处理
>     快速幂方法，m的16次方等于m^8 * m^8，从而减少计算量
>     次方 n 的二进制 表示了 x^4，x^2，x 的分量相乘
'''
public static double myPow(double x, int n) {
        boolean g_InvalidInput = false;
        double powerResult = 1.0;
        long b = n;
        if(Math.abs(x - 0.0) < 0.0000001 && n <= 0){
            g_InvalidInput = true;
            return 0.0;
        }

        if(n < 0){
            b = -b;
            x = 1.0/x;
        }
    
        while(b > 0){
            if((b & 1) == 1) powerResult *= x;
            x *= x;
            b >>= 1;
        }
    
        return powerResult;
    
    }
'''

##13. 打印从1到最大的n位数(大数处理方式)
输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。
>   注意： 字符串是一种有效的表示大数的方式
>        leecode 中不用静态的变量和方法，否则出错
>         利用递归的方法，遍历所有的数据
>         定义打印函数，将字符串前面的0消去
>          用字符数组(字符串)表示大数
>
'''
int count = 0;
    int[] res;

    public int[] printNumbers(int n) {
        Solution sol = new Solution();
        sol.res = new int[(int)Math.pow(10,n) -1];
        if(n <= 0)
            return null;
    
        char[] stringNUm = new char[n];
        for(int i = 0; i < 10; i++){
            stringNUm[0] = (char)('0'+ i);
            sol.PrintToMaxDigits(sol,stringNUm, n, 0);
        }
    
        return sol.res;
    }
    
    //递归遍历
    public void PrintToMaxDigits(Solution sol, char[] stringNUm, int length, int index){
        if(index == length - 1){
            sol.PrintNumber(sol, stringNUm);
            return;
        }
    
        for(int i = 0; i < 10; i++){
            stringNUm[index + 1] = (char)('0' + i);
            sol.PrintToMaxDigits(sol, stringNUm, length, index + 1);
        }
    
    }
    
    public void PrintNumber(Solution sol, char[] stringNUm){
        //转换为int打印出来
        boolean isBeginning = false;
        int length  = stringNUm.length;
        int resNum = 0;
    
        for(int i = 0; i < length; i++){
            if(!isBeginning && stringNUm[i] != '0')
                isBeginning = true;
    
            if(isBeginning){
                resNum += (stringNUm[i] - '0') * (int)Math.pow(10, length - i - 1);
            }
        }
    
        if(resNum != 0 && sol.count < sol.res.length)
        {   sol.res[sol.count] = resNum;
            sol.count++;}
    }
'''

## 14. 在O(1) 时间内删除链表的结点
给定链表的头结点和需要删除的结点信息，在O(1)时间内删除结点
'''
    public ListNode deleteNode(ListNode head, int val) {
        ListNode node = head;
        if(node == null)
        return head;
        //删除头结点
        if(node.val == val){
            return head.next;
        }

            while(node.next.val != val && node.next != null){
                node = node.next;
            }
            if(node.next != null)
            node.next = node.next.next;
    
        return head;
    }
'''
>    注意： 考虑删除为头结点情况，删除为尾结点情况可以与正常兼容。 采用的方法是，将待删除结点的上一个结点next直接指向待删除结点的下一个结点
>          如果本题给出的待删除结点信息包含了指针，那么可以将待删除结点的下一个结点复制到待删除结点上，并且将下一个结点删除。

## 15.调正数组的顺序，使奇数位于偶数前面
输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。
>   分析: 与快速排序类似，双指针从数组的两头出发，一个找奇数，一个找偶数，然后交换，直到两个指针相遇，完成全部交换。
'''
    public int[] exchange(int[] nums) {
        int lo = 0;
        int hi = nums.length -1;
        while(lo < hi){
            while(nums[lo] % 2 == 1 && lo < hi) lo++;
            while(nums[hi] % 2 == 0 && lo < hi) hi--;

            int temp = nums[hi];
            nums[hi] = nums[lo];
            nums[lo] = temp;
        }
    
        return nums;
    }
'''

## 16.链表中倒数第k个节点
输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。
例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。
>   分析： 双指针法，一个先走k-1步，另一个指针才从head开始走，这样到先走的指针到链表末尾，后走的指针就是倒数第k个数
>   注意： 边界输入， 空链表， 输入倒数第0个数， 链表长度小于k
>   发散题型： 1. 求链表的中间结点，双指针，一个一次走一步，一个一次走两步，走两步的先到末尾。走一步的为中间
>             2. 判断链表是否构成环形，双指针，一个一次走一步，一个一次走两步， 看走两步的是否能追上走一步的
'''
public ListNode getKthFromEnd(ListNode head, int k) {
        ListNode nodeFirst = head;
        ListNode nodeBehind = null;

        if(head == null || k == 0){
            return null;
        }
    
        for(int i = 0; i < k -1; i++){
            if(nodeFirst.next == null)
            return null;
    
            nodeFirst = nodeFirst.next;
        }
    
        nodeBehind = head;
    
        while(nodeFirst.next != null){
            nodeBehind = nodeBehind.next;
            nodeFirst = nodeFirst.next;
        }
    
        return nodeBehind;
    }
'''

## 17. 反转链表
定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。
>    注意： 如果链表的第i个结点前所有结点都已经反转，那么第i个结点将与前面的链表失去联系，需要提前记录下来
>           注意特殊的输入， 1. 空链表，2. 只有一个结点的链表

'''
    public ListNode reverseList(ListNode head) {
        ListNode nodeBehind = null;
        ListNode node = head;
        //反转后链表的头
        ListNode reverseHead = null;

        //如果为空链表或者只有一个结点
        if(head == null || head.next == null)
        return head;
    
        while(node != null){
            ListNode nodeNext = node.next;
            if(node.next == null)
                reverseHead = node;
            //更改当前结点的指向
            node.next = nodeBehind;
            nodeBehind = node;
            node = nodeNext;
        }
    
        return reverseHead;
    }
'''

## 18. 合并两个排序的链表
输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。
>  分析： 归并的思想
>  注意： 遍历两个链表的时候，需要先判断，是否有已经用完的链表，其中一个用完了，直接用另一个
>  可优化的两个地方：  1. 表头的判断，直接创建一个链表，把剩下的链接在其后，返回的时候返回head.next
>                    2.  有一个链表用完的时候，可以直接将另一个链表全部挂上去，不需要再重复的循环操作
'''
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode mergeHead = null;
        ListNode nodeOne = l1;
        ListNode nodeTwo = l2;
        ListNode nodeMerge = null;

        //空链表特殊输入
        if(l1 == null)
        return l2;
        else if(l2 == null)
        return l1;
    
        //确定归并链表头
        if(nodeOne.val <= nodeTwo.val){
            mergeHead = nodeOne;
            nodeOne = nodeOne.next;
        }else{
            mergeHead = nodeTwo;
            nodeTwo = nodeTwo.next;
        }
        nodeMerge = mergeHead;
    
        while(nodeOne != null || nodeTwo != null){
            if(nodeOne == null){
            nodeMerge.next = nodeTwo; 
            nodeTwo = nodeTwo.next;       
            nodeMerge = nodeMerge.next;
            }else if(nodeTwo == null){
            nodeMerge.next = nodeOne; 
            nodeOne = nodeOne.next;       
            nodeMerge = nodeMerge.next;
            }else if(nodeOne.val <= nodeTwo.val){
                nodeMerge.next = nodeOne;
                nodeOne = nodeOne.next;
                nodeMerge = nodeMerge.next;
            }else{
                nodeMerge.next = nodeTwo;
                nodeTwo = nodeTwo.next;
                nodeMerge = nodeMerge.next;
            }
        }
    
        return mergeHead;
    }
'''

'''
//优化后的代码
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dum = new ListNode(0), cur = dum;
        while(l1 != null && l2 != null) {
            if(l1.val < l2.val) {
                cur.next = l1;
                l1 = l1.next;
            }
            else {
                cur.next = l2;
                l2 = l2.next;
            }
            cur = cur.next;
        }
        cur.next = l1 != null ? l1 : l2;
        return dum.next;
    }
}
'''

## 19. 树的子结构 (树的遍历)
输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)

B是A的子结构， 即 A中有出现和B相同的结构和节点值。

例如:
给定的树 A:

     3
    / \
   4   5
  / \
 1   2
给定的树 B：

   4 
  /
 1
返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。

>  分析： 实际上是对树的遍历，先在树中找到相同的根结点，再判断根结点下的子树是否具有相同的结构。
>         二叉树的遍历，使用递归的方法显得更加清晰，分为左右子树遍历，递归的终止条件是我们到达了叶节点

'''
public boolean isSubStructure(TreeNode A, TreeNode B) {
       return hasSubtree(A,B);
    }
    //第一个递归，遍历树，找与B相同的根结点，找到之后，进入第二个递归函数判断结构；
    public boolean hasSubtree(TreeNode A, TreeNode B){
        boolean flag = false;
        if(A != null && B != null){
            if(A.val == B.val)
                flag = isTreeAhasTreeB(A,B); 
            if(!flag)
                flag = hasSubtree(A.left, B);
            if(!flag)
                flag = hasSubtree(A.right, B);
        }

        return flag;
    }
    
    //第二个递归函数，判断两个数的结构是否相同
    
    public boolean isTreeAhasTreeB(TreeNode A, TreeNode B){
        if(B == null)
            return true;
        if(A == null)
            return false;
        if(A.val != B.val)
            return false;
    
        return isTreeAhasTreeB(A.left, B.left) && isTreeAhasTreeB(A.right, B.right);
    }
'''

## 20.二叉树的镜像(树的遍历)(分为左右子树遍历)
请完成一个函数，输入一个二叉树，该函数输出它的镜像。
>   分析： 简要的画图可知，求树的镜像过程，实际上是遍历树的同时交换非叶结点的的左右子结点。
'''
    public TreeNode mirrorTree(TreeNode root) {
        return mirrorAction(root);
    }

    public TreeNode mirrorAction(TreeNode root){
        TreeNode node = root;
        if(root == null)
        return root;
    
        node = mirrorAction(root.left);
        root.left = mirrorAction(root.right);
        root.right = node;
        return root;
    }
'''
>   注意： 画图可以让很多问题更加明显，清晰

## 21. 对称的二叉树(遍历二叉树)
请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。
>   注意： 遍历二叉树的过程中，left.left 与 right.right对称，且left.right 与 right.left 对称都要进行判断；
'''
    public boolean isSymmetric(TreeNode root) {
        if(root == null)
            return true;
        return recur(root.left, root.right);
    }

    public boolean recur(TreeNode left, TreeNode right){
        if(left == null && right == null)
            return true;
        if(left == null || right == null)
            return false;
    
        if(left.val == right.val)
            return recur(left.left, right.right) && recur(left.right, right.left);
        
        return false;
    }
'''

## 22. 顺时针打印矩阵(边界判定条件)  (画图)
输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字
>    注意： 将打印分为四个部分，自左向右，自上而下，自右向左，自下向上
>           巧妙利用了++t > b 先对t进行自增操作，再判断是否越界
'''
class Solution {
    public int[] spiralOrder(int[][] matrix) {
        if(matrix.length == 0) return new int[0];
        int l = 0, r = matrix[0].length - 1, t = 0, b = matrix.length - 1, x = 0;
        int[] res = new int[(r + 1) * (b + 1)];
        while(true) {
            for(int i = l; i <= r; i++) res[x++] = matrix[t][i]; // left to right.
            if(++t > b) break;
            for(int i = t; i <= b; i++) res[x++] = matrix[i][r]; // top to bottom.
            if(l > --r) break;
            for(int i = r; i >= l; i--) res[x++] = matrix[b][i]; // right to left.
            if(t > --b) break;
            for(int i = b; i >= t; i--) res[x++] = matrix[i][l]; // bottom to top.
            if(++l > r) break;
        }
        return res;
    }
}
'''

## 23. 包含min函数的栈(举例子，找规律)
定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。
>   分析: 需要min的复杂度为O(1) 常规的思想是设置一个int值，存储最小值，但是弹栈时候，最小值可能变化，所以次最小值也要保存，因而推导出，用一个
>         辅助栈来保存最小值，通过例子可以简单看到，最小值后出现的次小值是不需要保存的，每当出现最小值的时候保存一次即可
'''
class MinStack {
    Deque<Integer> stack;
    Deque<Integer> minStack;

    /** initialize your data structure here. */
    public MinStack() {
        stack = new LinkedList<Integer>();
        minStack = new LinkedList<Integer>();
    }
    
    public void push(int x) {
        stack.push(x);
        if(minStack.isEmpty() || minStack.peek() >= x)
        minStack.push(x);
    }
    
    public void pop() {
        if(stack.pop().equals(minStack.peek()))
        minStack.pop();
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int min() {
        return minStack.peek();
    }
}
'''

>    注意： peek() 弹出的是一个Object对象，但是如果用int 接收，会自动拆箱，但是如果直接  s1.peek() == s2.peek() 会比较地址值，出错

## 24. 栈的压入、弹出序列
输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列 {4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列的弹出序列。
>      注意：  只需要借助一个栈就可以实现模拟。不需要第二个栈来存储弹出的数据
>              判断的标准是，只要栈为空，或者栈顶不等于需要弹出的数据，即继续压栈，直到所有的数据都压进去，只要栈顶的数据等于需要弹出的数据就一直弹栈
>              循环结束后判断栈内是否有数据即可
>
'''
    public boolean validateStackSequences(int[] pushed, int[] popped) {
        Deque<Integer> stack= new LinkedList<>();
        int pPop = 0;
        if(pushed == null || pushed.length ==0){
            return true;
        }

        for(int num : pushed){
            stack.push(num);
            while(!stack.isEmpty() && stack.peek() == popped[pPop]){
                stack.pop();
                pPop++;
            }
        }
    
        return stack.isEmpty();
    
    }
'''

## 25. 从上到下打印二叉树(广度优先搜索BFS) 一般使用队列来进行操作
从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。
>    分析：为了打印方便，我们打印完一个结点，需要知道其同父节点下的另一个结点，因此需要先储存下来，我们每打印一个结点，都要将该结点的左右结点储存，
>          遵循先进先出的原则，因而是队列来进行操作。
>    注意： 通过流对栈内的数据转换为int数组，会导致时间大幅度增加。  同类题目还有广度优先遍历有向图

'''
    public int[] levelOrder(TreeNode root) {
        if(root == null)
            return new int[0];
        
        Deque<TreeNode> eque = new LinkedList<>();
        Deque<Integer> out = new LinkedList<>();
        eque.add(root);
    
        while(!eque.isEmpty()){
            TreeNode node = eque.getFirst();
            out.addLast(node.val);
            eque.removeFirst();
    
            if(node.left != null)
                eque.addLast(node.left);
            if(node.right != null)
                eque.addLast(node.right);
        }
    
        int[] result = new int[out.size()];
        int i =0;
        while(!out.isEmpty()){
            result[i++] = out.removeFirst();  
        }
    
        return result;
        //return out.stream().mapToInt(Integer::intValue).toArray();
    }
'''

## 26. 从上到下打印二叉树
从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行
例如:
给定二叉树: [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [9,20],
  [15,7]
]

>   分析： 这道题与上一道题目类似，但是又有不同之处，这道题的打印，可以不是按照广度顺序输出，只要对应的数在对应的队列中即可，因而可以使用
>          递归调用，并传递当前的层。
>          注意:  也可以用上一题 的广序遍历方法， 此时可用循环的方式，在打印一个结点的时候，栈内此时所有的结点都是同一层的，打印完压栈的结点都是下一层的
'''
class Solution {
    List<List<Integer>> result = new LinkedList<>();
    public List<List<Integer>> levelOrder(TreeNode root) {
        rec(root, 0);
        return result;
    }

    public void rec(TreeNode root, int i ){
        if(root == null)
            return;
        if(result.size() <= i) result.add(new ArrayList());
        result.get(i).add(root.val);
        rec(root.left, i+1);
        rec(root.right, i+1);
    
    }
}
'''

'''
//使用BFS的遍历方式 ，其中int i = queue.size() 仅仅执行一次，后面压栈不影响i的初始值设定
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        List<List<Integer>> res = new ArrayList<>();
        if(root != null) queue.add(root);
        while(!queue.isEmpty()) {
            List<Integer> tmp = new ArrayList<>();
            for(int i = queue.size(); i > 0; i--) {
                TreeNode node = queue.poll();
                tmp.add(node.val);
                if(node.left != null) queue.add(node.left);
                if(node.right != null) queue.add(node.right);
            }
            res.add(tmp);
        }
        return res;
    }
}
'''

## 27. 从上到下打印二叉树
请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。
例如:
给定二叉树: [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [20,9],
  [15,7]
]

>   分析：此题的变型与26题类似，可以采用BFS循环的方式，并且记录当前的层数，记录每一层的队列定义为双端队列，奇数层添加到尾，偶数层添加到头

'''
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        if(root == null)
            return new LinkedList<>();
        List<List<Integer>> result = new LinkedList<>();
        Deque<TreeNode> eque = new LinkedList<>();
        int count = 1;  //记录层数
        eque.add(root);
        while(!eque.isEmpty()){
            LinkedList<Integer> tmp = new LinkedList<>();
            for(int i = eque.size(); i > 0 ; i--){
                TreeNode node = eque.poll();
                if(count % 2 == 1) tmp.addLast(node.val);
                else tmp.addFirst(node.val);
                if(node.left != null) eque.add(node.left);
                if(node.right != null) eque.add(node.right);
            }
            count++;
            result.add(tmp);
        }
        return result;
    }
}
'''


## 28. 二叉搜索树的后序遍历序列(二叉搜索树)
输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 true，否则返回 false。假设输入的数组的任意两个数字都互不相同。
后序遍历： 先左儿子，后右儿子，最后根结点。  
二叉搜索树： 所有的左子树结点值小于根节点， 所有右子树的结点值大于根结点
>    分析： 先找到最后的根结点，再从前往后找到第一个大于根节点的值，分为左右子树，左子树可以没有，再递归的判断左右子树是否为二叉搜索树
>           跳出递归的条件是已经到了叶结点，或者右子树存在小于根结点值的情况
'''
class Solution {
    public boolean verifyPostorder(int[] postorder) {
        return myVerifyPostorder(postorder, 0, postorder.length -1);
    }

    public boolean myVerifyPostorder(int[] postorder, int lo, int hi){
        if(postorder == null || hi - lo < 0)
            return true;
    
        int rootVal = postorder[hi];
        //找到左右子树分界点
        int rootId = lo;
        for(; rootId <= hi - 1; rootId++){
            if(postorder[rootId] > rootVal) break;
        }
    
        //判断右子树的结点是否都大于根结点
        for(int j = rootId; j <= hi - 1; j++){
            if(postorder[j] < rootVal) return false;
        }
    
        boolean leftFlag = true;
        boolean ringhtFlag = true;
    
        if(rootId - lo - 1 > 0){
            leftFlag = myVerifyPostorder(postorder, lo, rootId - 1);
        }
        if(hi - rootId - 1 > 0){
            ringhtFlag = myVerifyPostorder(postorder, rootId, hi - 1);
        }
    
        return leftFlag && ringhtFlag;
        
    }
}
'''

## 29. 二叉树中和为某一值的路径
输入一棵二叉树和一个整数，打印出二叉树中节点值的和为输入整数的所有路径。从树的根节点开始往下一直到叶节点所经过的节点形成一条路径。
>      分析： 回溯法 （先序遍历 + 路径记录）
>             用一个队列来记录路径，当值等于目标和sum的时候。 把整个队列加入到result中。  记得在递归函数的末尾，出列刚刚加入的数，这样返回上一层
>             的时候，队列已经自动删去了已经走过的结点
>>            *注意： 将队列加入到result的时候，如果直接add(stack) 那么只是加入了地址。stack的改变会影响result， 正确的方法是
>>                    add(new LinkedList(stack))，相当于把stack内容拷贝到result中。
```
/*

 * Definition for a binary tree node.
 * public class TreeNode {
 * int val;
 * TreeNode left;
 * TreeNode right;
 * TreeNode(int x) { val = x; }
 * }
   */
   class Solution {
   public List<List<Integer>> pathSum(TreeNode root, int sum) {
       List<List<Integer>> result = new LinkedList<>();
       LinkedList<Integer> stack = new LinkedList<>();
       if(root == null)
           return result;
       rec(result, stack, root, sum, 0);
       return result;
   }
   public void rec(List result,  LinkedList stack, TreeNode root, int sum, int nowSum){
       nowSum += root.val;
       stack.add(root.val);      
       if(root.left != null) rec(result, stack, root.left, sum, nowSum);
       if(root.right != null) rec(result, stack, root.right, sum, nowSum);
       if(root.left == null && root.right == null && nowSum == sum) 
           result.add(new LinkedList(stack));
       stack.pollLast();
   }
  }
```

## 30. 复杂链表的复制(分解复杂的问题，使其简单化)
请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 random 指针指向链表中的任意节点或者 null。
>    分析： 将复杂链表的复制分为三个部分进行， 第一阶段，我们对结点N 进行复制 N’，并将N' 插入到原链表的N与下一个结点之间
>           第二个阶段，我们对复制完成的链表进行random指针的赋值，可以看出来，N'的random指向 N的random指向结点的下一个结点
>           第三个阶段， 将链表拆成两个链表
>    注意： 拆完链表的时候，需要把链表的末尾赋值为null
'''
class Solution {
    public Node copyRandomList(Node head) {
        if(head == null) return null;
        Clone(head);
        CloneRandom(head);
        return ReconnectNode(head);
    }


    //按照格式进行链表结点复制
    public void Clone(Node head){
        Node node = head;
        while(node != null){
            Node nodeClone = new Node(node.val);
            nodeClone.next = node.next;
            nodeClone.random = null;
    
            node.next = nodeClone;
            node = nodeClone.next;
        }
    }
    
    //对结点的random指针进行复制
    public void CloneRandom(Node head){
        Node node = head;
        while(node != null){
            if(node.random != null)
            node.next.random = node.random.next;
            node = node.next.next;
        }
    }
    
    //将链表拆分成两个链表
    public Node ReconnectNode(Node head){
        Node node = head;
        Node cloneHead = head.next;
        Node cloneNode = head.next;
    
        while(cloneNode.next != null){
            node.next = node.next.next;
            cloneNode.next = cloneNode.next.next;
            node = node.next;
            cloneNode = cloneNode.next;
        }
    
        node.next = null;
    
        return cloneHead;
    }
}
'''

## 31. 二叉搜索树与双向链表  (中序遍历)
输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的循环双向链表。要求不能创建任何新的节点，只能调整树中节点指针的指向。
>      分析： 中序遍历 + 双向链表
>             父结点链接 左指针 一定指向左子树的最大值，右指针 一定指向右子树的最小值

```
      class Solution {
        Node pre, head;
        public Node treeToDoublyList(Node root) {
            if(root == null) return null;
            dfs(root);
            head.left = pre;
            pre.right = head;
            return head;
        }
        void dfs(Node cur) {
            if(cur == null) return;
            dfs(cur.left);
            if(pre != null) pre.right = cur;
            else head = cur;
            cur.left = pre;
            pre = cur;
            dfs(cur.right);
        }
      }

```



## 32. 序列化二叉树(广度优先遍历 BFS)

请实现两个函数，分别用来序列化和反序列化二叉树。
你可以将以下二叉树：

    1
   / \
  2   3
     / \
    4   5

序列化为 "[1,2,3,null,null,4,5]"

>     注意： 压入栈的node = null，当栈内还有其他数的时候，栈不为空，如果栈内只有指向null的node
>            栈是空的，借此防止树无限循环打印null层
>            逆序列化的过程中，可以借助string的拆分，与双向队列，将每一个结点与其左右结点链接

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
            if(root == null) return "[]";
            StringBuilder strResult = new StringBuilder("[");
            Deque<TreeNode> eque = new LinkedList<>();
            eque.addFirst(root);
            while(!eque.isEmpty()){
                TreeNode node = eque.poll();
                if(node != null){
                    strResult.append(node.val + ",");
                    eque.add(node.left);
                    eque.add(node.right);
                }else
                    strResult.append("null,");
            }
            //删除最后一个多余的","
            strResult.deleteCharAt(strResult.length()-1);
            strResult.append("]");
        return strResult.toString();
    }
    
    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if(data.equals("[]")) return null;
        //去除首尾的[]，并用"," 分割成数组
        String[] str = data.substring(1, data.length() - 1).split(",");
        TreeNode head = new TreeNode(Integer.parseInt(str[0]));
        Deque<TreeNode> eque = new LinkedList<>();
        eque.add(head);
    
        int count = 1;
        while(!eque.isEmpty()){
            TreeNode node = eque.poll();
            if(!str[count].equals("null")){
                node.left = new TreeNode(Integer.parseInt(str[count]));
                eque.add(node.left);
            }
            count++;
            if(!str[count].equals("null")){
                node.right = new TreeNode(Integer.parseInt(str[count]));
                eque.add(node.right);
            }
            count++;
        }
        return head;
    }

## 33. 字符串的排列
输入一个字符串，打印出该字符串中字符的所有排列。
>    分析: 回溯法  深度优先搜索BFS  所有的排列方案 
>          考虑存在重复的字符， 剪枝操作，即遇到重复的字符时候不交换，保证每个位置的每种字符只出现一次
>          当返回当前函数之后，还需要回溯，即将当前函数的交换数据交换回去
>          注意toArray的用法，含有参数的调用，会返回与参数同类型，同size()的数组，并自动将list的内容填充

    class Solution {
      //StringBuilder result = new StringBuilder();
      List<String> result = new LinkedList<>();
      char[] charArray;
      public String[] permutation(String s) {
          charArray = s.toCharArray();
          if(charArray.length <= 1)
              return new String[]{s};
          rec(0);
        return result.toArray(new String[result.size()]);
    }
    
    public void rec(int headId){
        if(headId == charArray.length -1){
            result.add(String.valueOf(charArray));
            return;
        }
        HashSet<Character> set = new HashSet<>();
        for(int i = headId; i < charArray.length; i++){
            if(set.contains(charArray[i])) continue;
            set.add(charArray[i]);
            exch(headId, i);
            rec(headId + 1);
            exch(headId, i);   //回溯，换回来
        }
    }
    
    public void exch(int i, int j){
        if(i > charArray.length - 1 || j > charArray.length - 1 || i == j)
        return;
    
        char tmp = charArray[j];
        charArray[j] = charArray[i];
        charArray[i] = tmp;
    }
## 34.数组中出现次数超过一半的数字
数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。
假设 给定的数组非空，并且一定存在多数元素。

>    分析： 一个超过数组一半的数字， 如果数组按照从小到大的顺序排列，那么这个数一定是数组的中位数。
>    现有 O(n)的成熟算法，找到数组中第k大小的数字
>    如果partition返回的index 在middle 的左边，那么需要对右侧的子数组进行partition，反之亦然。

>    另一种代码上更简洁的方式： 摩尔投票: 只搜索数组中大于一半的数，引入记录数据 和 票数的 变量， 当某一个值的票数为0的时候，替换其为当前读入的值，并记录一票， 当读入的值与当前值不相等，那么票数减一，最后剩下的数，一定为出现次数超过一半的数

    public int majorityElement(int[] nums) {
    	int count = 0, rem = 0;
        for(int num: nums){
            if(count == 0) rem = num;
            count += num == rem ? 1 : -1;
        }
    
        return rem;
    }
    //通过partition 找到第 k 大的数据方式 找到第middle 大小的数据
    //没有对原数组打乱，因此迭代时间长， 而且 重复的数剧多，很多递归是无用
    public int majorityElement(int[] nums) {
            if(nums.length == 1)
                return nums[0];
            //StdRandom.shuffle(nums);
            int middle = nums.length >> 1;
            int lo = 0, hi = nums.length -1;
            int index = partition(nums, lo, hi);
            while( nums.length % 2 == 0 && (index != middle - 1 && index != middle) || nums.length % 2 == 1 && index != middle){
                if(index > middle){
                    hi = index -1;
                    index = partition(nums, lo, hi);
                }else{
                    lo = index + 1;
                    index = partition(nums, lo, hi);
                }
            }
        return nums[middle];
    }
    
    //递归的方式调用
    public int partition(int[] nums, int lo, int hi){
        int i = lo, j = hi +1;
        int v = nums[lo];
        while(true){
            while(nums[++i] <= v) if(i >= hi) break;   //找到第一个大于v的
            while(nums[--j] >= v) if(j <= lo) break;   //找到第一个小于v的
            if(i >= j) break;
            exch(nums, i ,j);
        }
    
        exch(nums, lo, j);  //将v放到合适的位置
        return j;
    }
    
    public void exch(int[] a, int i, int j) {
        int t = a[i];
        a[i] = a[j];
        a[j] = t;
    }

## 35. 最小的k个数
输入整数数组 arr ，找出其中最小的 k 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。
> 分析： 最小的k个数可以使用partition函数 对数组进行划分，当返回值 == k 时候， 左便k个数即为所求的数据
>       方法一： 快排思想，利用partition函数，只要 index = k - 1； 左边的k个数即为最小的k个数
>               可以用Arrays.copyOf(arr, k); 快速截取数组的前k个值      缺点： 修改了原数组
>       方法二： 适用于大规模数据， 建立一个堆，动态更新的存放最小的k个数据
>               在容量为k的堆满了以后，需要考虑 删除，添加，以及找最大数

>               PriorityQueue 底层是借由二叉树实现的 小顶堆，使得每次取出的数据都是堆中最小的数
>               可以通过修改创建对象时候 Compare函数 来把小堆转化为大堆
>               频繁的查找及替换最大值时，二叉树，堆，红黑树是优先选择


    class Solution {
      public int[] getLeastNumbers(int[] arr, int k) {
          if(k == 0 || arr.length == 0)
              return new int[0];
          if(arr.length == k)
              return arr;
        int lo = 0, hi = arr.length - 1;
        int index = partition(arr, lo, hi);
        while(index != k - 1){
            if(index > k - 1){
                hi = index -1;
                index = partition(arr, lo ,hi);
            }else{
                lo = index +1;
                index = partition(arr, lo, hi);
            }
        }
    
        return Arrays.copyOf(arr, k);
    }
    
    public int partition(int[] nums, int lo ,int hi){
        int i = lo, j = hi + 1;
        int v = nums[lo];
        while(true){
            while(nums[++i] <= v) if(i >= hi) break;
            while(nums[--j] >= v) if(j <= lo) break;
            if(i >= j) break;
            exch(nums, i, j);
        }
    
        exch(nums, lo, j);
        return j;
    }
    
    public void exch(int[] nums, int i, int j){
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }


```
class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        int[] vec = new int[k];
        if (k == 0) { // 排除 0 的情况
            return vec;
        }
        //重写Compare函数，定义为最大堆，(默认最小堆)
        PriorityQueue<Integer> queue = new PriorityQueue<Integer>(new Comparator<Integer>() {
            public int compare(Integer num1, Integer num2) {
                return num2 - num1;
            }
        });
        for (int i = 0; i < k; ++i) {
            queue.offer(arr[i]);
        }
        for (int i = k; i < arr.length; ++i) {
            if (queue.peek() > arr[i]) {
                queue.poll();
                queue.offer(arr[i]);
            }
        }
        for (int i = 0; i < k; ++i) {
            vec[i] = queue.poll();
        }
        return vec;
    }
}
```



## 36. 数据流中的中位数
如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。

>           分析： 如果使用数组来存储数据，对于无序的数组，插入需要O(1)，但是找中位数需要O(n), 对于排序的数组，插入需要O(n), 但是找中位数是
>                  O(1)， 链表存储与排序数组类似
>                  使用二叉搜索树 是最好的选择，为了防止二叉树不平衡，导致像链表一样的结构， 最好选用AVL ， 平衡二叉树，但是， 平衡二叉树的代码
>                  并不在库内，短时间写不出来。
>                  考虑使用两个堆，保证两个堆中的数字数保持一致，在排序的情况下，，左边堆的最大值，与右边堆的最小值的平均值即为中位数，显然可以使用一个
>                  一个最大堆，一个最小堆来实现

```
class MedianFinder {
    PriorityQueue<Integer> minHeap;
    PriorityQueue<Integer> maxHeap;
    int count = 0;    //堆中的总数
    /** initialize your data structure here. */
    public MedianFinder() {
        //最大最小堆初始化
        maxHeap = new PriorityQueue<>(new Comparator<Integer>(){
            public int compare(Integer num1, Integer num2){
                return  num2 - num1;
            }
        });
        minHeap = new PriorityQueue<>();
    }
    
```

    public void addNum(int num) {
        //当堆内的数为偶数个的时候，新数据加入最小堆
        if(count %2 == 0){
            if(!maxHeap.isEmpty() && num < maxHeap.peek()){
                minHeap.offer(maxHeap.poll());
                maxHeap.offer(num);
            }else{
                minHeap.offer(num);
            }
        }else{
            if(!minHeap.isEmpty() && num > minHeap.peek()){
                maxHeap.offer(minHeap.poll());
                minHeap.offer(num);
            }else{
                maxHeap.offer(num);
            }
        }
            count++;
    }
    
    public double findMedian() {
        //double result = 0;
        if(count % 2 == 1)
            return minHeap.peek();
        else
            return (minHeap.peek() + maxHeap.peek())/2.0;
    }
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();


>     注意：public void addNum(int num)  代码可进一步优化，不需要考虑num 与 另一个堆顶的大小关系
```
        if(minHeap.size() != maxHeap.size()) {
            minHeadp.offer(num);
            maxHeap.offer(minHeap.poll());
        } else {
            maxHeadp.offer(num);
            minHeap.offer(maxHeap.poll());
        }
```

## 37. 连续子数组的最大和（动态规划法）
输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。

>    分析： 动态规划，以nums[i] 为结尾的子数组和最大公式为  若前 i - 1 项和最大值为负， 那么 前i 项最大和为nums[i]，如果前i 项最大和为正，则以nums[i]
>           为结尾的前i项 和最大为 f(i - 1) + nums[i];

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int sum = nums[0];
        int sumMax = nums[0];
        for(int i = 0; i <= nums.length - 1; i++){
            if(i == 0 || sum < 0){
                sum = nums[i];
            }else{
                sum += nums[i];
            }
            if(sum > sumMax)
            	sumMax = sum;
    }

    return sumMax;
}
```

## 38. 1～n 整数中 1 出现的次数(困难)
输入一个整数 n ，求1～n这n个整数的十进制表示中1出现的次数。

例如，输入12，1～12这些整数中包含1 的数字有1、10、11和12，1一共出现了5次。

>           分析：将 1 ~ n 的个位、十位、百位、...的 11 出现次数相加，即为 11 出现的总次数。
>                 设当前位的数字为 cur，那么数字n中，cur左边的数称为高位 high， cur右边的数称为 低位 low，n = high cur low；
>                 如果cur < 1 (cur == 0)  不妨设 n = 1201， 此时 设 cur 为十位， 则十位为1的数 在 0010  - 1119 之间 ，只看高低位就是
>                 000 - 119 共有 119 - 000 + 1   即为 high * digit 个
>                 如果cur == 1 不妨设 n = 1215，cur为十位,  则十位为1的数 在 0010 - 1215 之间，只看高低位为 000 - 125 + 1，
>                 即为 high * digit + low + 1，
>                 如果cur > 1 不妨设 n = 1251， cur为十位，则十位为1的数在 0010 - 1219 之间，只看高低位 为 129 - 000 + 1, 即为 （high+1）*digit

    class Solution {
      public int countDigitOne(int n) {
          int high = n /10;
          int cur = n % 10;
          int low = 0;
          int digit = 1, res = 0;
          while(high != 0 || cur != 0){
              if(cur == 0)  res += high * digit;
              else if(cur == 1) res += high * digit + low + 1;
              else res += (high + 1) * digit;
            //循环移位
            low += cur * digit;
            cur = high % 10;
            high /= 10;
            digit *= 10;
        }
        return res;
    }
## 39. 数字序列中某一位的数字
数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

请写一个函数，求任意第n位对应的数字

>          分析： 简单的写几个数据便能看到规律，一位数有10个，2位数有 90 个， 有90 * 2 个数， 3位数900个 有900 * 3 个数
>                 因此分析，先找到第n个数字，属于几位数， 再找到属于哪一个数，最后找到属于第几位数，
>                 减法更加适合求解，让指针下标变得更加简单


    class Solution {
      public int findNthDigit(int n) {
          int count = 1;  //n为几位数
          int resultMax = 9;  //找到n所在的范围
          int resultMin = 0;
          int result = 0;
        //先判断是几位数
        while(n > resultMax){
            count++;
            resultMin = resultMax;
            resultMax += 9 * Math.pow(10, count - 1) * count;
        }
    
        //找到第n位所在的多位数
        result = (int) Math.pow(10, count - 1) + 
            (int)Math.ceil((n - resultMin) / (double)count)- 1;
        for(int i = 1; i < count - (n - resultMin) % count + 1; i++ ){
            if((n - resultMin) % count == 0) break;
            result /= 10;
        }
        return (result % 10);
    }


```java
//以减法求解的简便代码
class Solution {
    public int findNthDigit(int n) {
        int digit = 1;
        long start = 1;
        long count = 9;
        while (n > count) { // 1.
            n -= count;
            digit += 1;
            start *= 10;
            count = digit * start * 9;
        }
        long num = start + (n - 1) / digit; // 2.
        return Long.toString(num).charAt((n - 1) % digit) - '0'; // 3.
    }
}
```



## 40. 把数组排成最小的数
输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。
>           分析： 拼接的方式决定，两个数最高位小的一定小，最高位大的一定大，因而定义一种新的排序方式
>                  对两个数 n，m ，如果nm > mn 那么认为 n > m， 按照这种规则对数组中的数据进行重新排序，再按照
>                  自小向大的顺序组成的数一定是最小的，涉及隐含大数问题 和函数式调用方法
>
>           复习: Lambda 表达式，函数式调用， 找一个能解决问题的对象，作为匿名内部类的语法糖，但是不创建类对象，节约
>                 仅适用于仅含一个抽象方法的接口 
>                 格式; (参数列表)->{一些重写的方法代码}  一些参数，一个箭头，一段代码
>                 可省略的内容，1.参数列表中的参数类型 2. 若参数只有一个() 也可以省略 3. 如果方法体的代码只有一行，可同时省略
>                 （必须同时省略） 方法体的大括号 {} ，return 语句 和 分号。
>                  JAVA 中自带的strig 比大小compareTo方法，返回一个int 值，如果大于0，则str1 > str2, 小于0， 则 str1 < str2



```java
class Solution {
    public String minNumber(int[] nums) {
        String[] strs = new String[nums.length];
            for(int i = 0; i <= nums.length - 1; i++)
                strs[i] = String.valueOf(nums[i]);
        Arrays.sort(strs, (x,y)->(x + y).compareTo(y + x));
        StringBuilder res = new StringBuilder();
        for(String s: strs){
            res.append(s);
        }
        return res.toString();
    }
}
```



## 41.把数字翻译成字符串
给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。
>           注意： 一个值可以选择翻译位字母，或者与下一个数字一起翻译，因而是递归
>                01 02 也是非法的翻译字段 10-25才是合法翻译

### 1. 递归
>       注意到递归存在重复的子问题，并不是最优解（可以从右往左，避免出现重复子问题）
```java
  class Solution {
    int count = 0;
    public int translateNum(int num) {
        char[] charArray = Integer.toString(num).toCharArray();
        rec(charArray, 0);
        return count;
    }

    public void rec(char[] charArray, int lo){
        if(lo == charArray.length - 1){  //最后一个
            count++;
            return;
        }
        if(lo == charArray.length - 2){ //最后两个
            String str = charArray[lo] + "" + charArray[lo+1];
            if(str.compareTo("25") <= 0 && charArray[lo] != '0') count += 2;
            else count++;
            return;
        }
    
        String str = charArray[lo] + "" + charArray[lo+1];
        if(str.compareTo("25") <= 0 && charArray[lo] != '0'){
            rec(charArray, lo + 1);
            rec(charArray, lo + 2);
        }else{
            rec(charArray, lo + 1);
        }
    
    }
}
```
### 2. 动态规划(与自右向左的递归类似)
>   分析： 我们定义以i位数字位结尾的翻译方式数为d[i], d[i] = d[i-1] 或者 d[i] = d[i-1] + d[i-2]  使用对10整除，减少字符串所占空间
>          当 num 第 1,2 位的组成的数字∈[10,25] 时，显然应有 2 种翻译方法，即 dp[2] = dp[1] + dp[0] = 
>           2dp[2]=2 ，而显然 dp[1] = 1 ，因此推出 dp[0] =1 
>    此题的动态规划计算是 对称的 ，即 从左向右 遍历（从第 dp[2] 计算至 dp[n] ）和 从右向左 遍历（从第 dp[n-2]计算至 dp[0]）所得方案数一致。

```java
class Solution {
    public int translateNum(int num) {
        int dp1 = 1, dp0 = 1, dPre, dCurrent = num % 10;
        //dPre 记录十位， dCurrent记录个位
        while(num != 0) {
            num /= 10;
            dPre = num % 10;
            int tmp = 10 * dPre + dCurrent;
            int c = (tmp >= 10 && tmp <= 25) ? dp1 + dp0 : dp1;
            dp0 = dp1;
            dp1 = c;
            dCurrent = dPre;
        }
        return dp1;
    }
}
```

## 42. 礼物的最大价值（动态规划与递归）

在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

> 分析：很容易分析出这是一道可以用递归求解的问题，到达位置[i,j] 所能拿到礼物的最大值d([i,j]) = max(gift[i-1,j], gift([i, j-1])) + gift(i,j),  但是，如果直接采用递归的方式求解，就像斐波那契数列一样，会出现大量的重复调用，比如对于矩阵中的一点[m, n] ，会出现不同的路径到[m, n]，而从[m, n] 到最终终点的求解过程是一样的，出现了大量重复调用。此时， 应考虑动态规划的求解方法，使用循环。
>
> 
>
> * 在不改变原始数据的情况下,   我们可以设置一个与列长 一样的一个矩阵，记录最大值，当当前的点位为[i,j]时， maxRoad中前[j - 1]个数据存储的是f(i,0),f(i,1),f(i,2),f(i,3),f(i,4)........f(i,j-1) 个值，max[i, j] 存储的是 f(i-1,j)的值（如果存在的话），并且将在本次循环被替换
>
> * 一种优化的思路是，当输入的二维数组特别大的时候，每次循环都判断i, j 是否大于零，是一个冗余的操作，可先对第一行和第一列进行操作，但是这种操作只能在允许改变原始数据的情况下。

```java
class Solution {
    public int maxValue(int[][] grid) {
        int[] maxRoad  = new int[grid[0].length];
            for(int i = 0; i <= grid.length - 1; i++){
                for(int j = 0; j <= grid[0].length - 1; j++){
                    int left = 0;
                    int up = 0;
                    if(i > 0)
                        up = maxRoad[j];
                    if(j > 0)
                        left = maxRoad[j-1];
                    maxRoad[j] = Math.max(up, left) + grid[i][j];
                }
            }

        return maxRoad[grid[0].length - 1];
    }
}
```

##  43.  最长不含重复字符的子字符串

请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

### 方法一： 自己写的最繁琐的方法(滑动窗口)

> ​	分析：创建一个StringBuilder 容器，存储以当前字母为结尾的最长字符串，如果StringBuilder 中存在当前位置的字母，就以该字母将StringBuilder 内的字符串分为两半，截取后一段，与当前字母链接，即为以当前结点为结尾的最长无重复字符串。
>
> ​	注意: 不能使用split 函数来切个字符串，因为split必须传递正则表达式，对于特殊字符 *, #,$等需要传递 //\*, //#, //$. 
>
> ​				存在大量的函数调用，字符串运算，十分浪费。另外 String本身也是一个字符数组，不需要将其转换

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if(s.length() == 1)
            return 1;
        StringBuilder str = new StringBuilder();
        char[] charArray = s.toCharArray();
        int maxLength = 0;
        for(int i =0; i <= charArray.length - 1; i++){
            if(str.toString().indexOf(charArray[i]) < 0){
                str.append(charArray[i]);
            }else{
                maxLength = str.toString().length() > maxLength ? 
                str.toString().length() : maxLength;
                    if(str.toString().lastIndexOf(charArray[i]) == str.toString().length() -1)
                        str = new StringBuilder();
                    else str = new StringBuilder(str.toString().substring(str.toString().
                               lastIndexOf(charArray[i]) + 1, str.toString().length()));
                    str.append(charArray[i]);
            }
            
        }

        return maxLength > str.toString().length() ? maxLength : str.toString().length();
    }
}
```

### 方法二： 动态规划 + 哈希表

>分析： 如果我们每次计算以当前结点为结尾的最长字符串，遍历到结尾，即可求得最长字符串的长度。
>
>​			考虑到需要存储每个字符最后一次出现时的位置，并且简化查找，因而想到用HashMap

```java
    public int lengthOfLongestSubstring(String s) {
            Map<Character, Integer> dis = new HashMap<>();
            int curLength = 0; //记录以当前结点为结尾的最大字符串长度
            int result = 0;

            for(int i = 0; i < s.length(); i++){
                int j = dis.getOrDefault(s.charAt(i), -1);   //获得哈希表中存储的当前字符的位置
                dis.put(s.charAt(i), i);   //更新哈希表中的值
                curLength = curLength < i - j ? curLength + 1 :  i - j;    
                result = Math.max(curLength, result);
            }

            return result;
        }
```

>注释:  getOrDefault(Key, default)   查询表中的Key所对应的值，如果没有，就返回default， 设置default为负数，是为了
>
>curLength = curLength < i - j ? curLength + 1 :  i - j;     该语句巧妙的利用了default值的作用， 如果之前表内没有就返回负数，那么i- j 就是一个比i还大的数，这显然说明，最长的字符串可以包含当前字符。
>
>curLength 记录以当前字符为末尾的最长字符串长度，实际上是记录上一个与当前字符相同的字符所在位置，判断该字符是否在curLength所代表的字符串之内
>
>> 固定右边界 j ，设字符 s[j]   s*[*j]   左边距离最近的相同字符为 s[i]，即 s[i] = s[j]
>>
>> 1.当 i < 0,  即s[j] 左边无相同的字符， 那么 d[j] = d[j-1] + 1;
>>
>> 2.当 d[j-1] < j - i, 说明字符s[i] 在字符串 d[j-1] 区间之外， 则d[j] = d[j-1] + 1；
>>
>> 3.当 d[j-1] > j - i, 说明字符s[i] 在字符串 d[j-1] 区间之内，则 d[j] = j - i；

## 44.丑数

我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。一般认为1是第一个丑数

>分析:  所有的丑数一定是之前的丑数 乘以 2 或 3 或 5， 我们只需要计算出之前丑数分别乘以 2，3 ，5之后的最小值，即为下一个丑数，并且按照从小到大顺序排列的丑数，一定存在一个数T2，使得T2*2大于序列中的所有丑数，并且T2左边的数乘以2都小于序列中的数，T2右边的数乘以2都大于序列中的数，同理存在T3, T5 我们只需要不断的更新这三个数即可。如果这三个数更新出来的下一个丑数相等，那么指针都需要指向下一位
>
>注意：	考虑特殊的输入0

```java
class Solution {
    public int nthUglyNumber(int n) {
        if(n == 0)
            return 0;
        int pTwo = 0, pThree = 0, pFive = 0;
        int[] uglyNUms = new int[n];
        uglyNUms[0] = 1;
        for(int i = 1; i <= n-1; i++){
           int n2 =  uglyNUms[pTwo] * 2, n3 =  uglyNUms[pThree] * 3, n5 =  uglyNUms[pFive] * 5;
           uglyNUms[i] = Math.min(Math.min(n2,n3),n5);
           if(uglyNUms[i] == n2) pTwo++;
           if(uglyNUms[i] == n3) pThree++;
           if(uglyNUms[i] == n5) pFive++; 
        }

        return uglyNUms[n-1];
    }
}
```

## 45.第一次只出现一次的字符

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

### 方法一. 无序的hashMap

>分析：字符与出现的次数，明显是存储键值对的问题，首先想到的是hashMap，但是hashMap是一个无序的集合，我们需要找到第一个只出现一次字符，因此还需要对原始字符穿进行二次遍历，在遍历的过程中每次都通过hashMap进行判断其是否只出现了一次，因此哈希表的值设置为boolean型

```java
class Solution {
    public char firstUniqChar(String s) {
        //双遍历，无序的HashMap
        HashMap<Character, Boolean> hashTable = new HashMap<>();
        //char[] charArray = s.toCharArray();   使用原始数组，减少内存开销
        for(int i = 0; i <= s.length() - 1; i++) 
            hashTable.put(s.charAt(i), !hashTable.containsKey(s.charAt(i)));
        for(int i = 0; i <= s.length() - 1; i++)
            if(hashTable.get(s.charAt(i))) return s.charAt(i);
        
        return ' ';
    }
}
```

### 方法二. 有序的LinkedHashMap

> 方法一在第二次遍历寻找第一个无重复的字符时候，以然需要对原始字符串进行遍历，如果输入的字符串很长，那么遍历的次数很大。如果哈希表是有序的，那么我们可以通过哈希表直接查找第一个不重复的字符，由于字符一共只有256个(题目中), 那么哈希表一定是小于字符串长度的，节约了二次循环的遍历次数

```java
import java.until.LinkedHashMap;
class Solution {
    public char firstUniqChar(String s) {
        //减少第二次循环的循环次数，有序的LinkedHashMap()
        LinkedHashMap<Character, Boolean> hashTable = new LinkedHashMap<>();
        for(int i = 0; i <= s.length() - 1; i++) 
            hashTable.put(s.charAt(i), !hashTable.containsKey(s.charAt(i)));
        for(Map.Entry<Character, Boolean> d : hashTable.entrySet() )
            if(d.getValue()) return d.getKey();
        
        return ' ';
    }
}
```

> 复习 HashMap中常用函数
>
> 1. put(K key,  V value) 添加键值对， 如果不重复，返回null，如果重复，返回被替换的V
> 2. remove(K) 通过key值删除V
> 3. containsKey(object value) 判断是否存在Key值
> 4. get(K) 获取Key对应的value
>
> 遍历集合的函数：
>
> 1. Set<K> keySet()  返回一个集合Set，包含Map中所有的Key值
> 2. Set<Map.Entry<K,V>> entrySet()  返回一个Set集合，存储Map集合中所有的Entry对象，键值对
> 3. Entry<K,V>对象可以调用 getKey(),  getValue();

补充： 可以通过简单的数组自己实现哈希表，数组的下标对应ASCII，数组的值对应出现次数。

ASCII 获取 char 直接强制转换即可(char), char 获取ASCII 码， Integer.valueOf('c');

## 46. 数组中的逆序对

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

> 分析： 在学习选择排序的时候，我们便接触过，选择排序的循环次数及为数组中的逆序对数。但是当输入的数组足够大。逆序队最大可以为数组长度n的平方： n<sup>2</sup>, 这明显与我们的要求不符合。
>
> 分治思想：将数组分为两个部分，分别进行处理。我们先将两个部分内的数进行排序，并记录逆序对数目，之后归并两个数组，归并过程中，左边的数字如果更大的情况下，则出现了逆序对，逆序对的对数，如果用两根指针分别指向左右两个数组正在比较的数据，那么逆序对数就是右边数组指针左边数字的个数
>
> 注意：  注意考虑大数问题 n<sup>2</sup>是否超出限制

```java
class Solution {
    int[] nums, tmp;
    public int reversePairs(int[] nums) {
        this.nums = nums;  //将数组扩展到类内可用
        tmp = new int[nums.length];
        return merge(0, nums.length - 1);
    }

    //归并操作
    public int merge(int lo, int hi){
        //递归终止条件
        if(lo >= hi) return 0;

        //递归划分
        int mid = lo + (hi - lo)/2;
        int res = merge(lo, mid) + merge(mid+1, hi);
        //将nums待归并的值复制到辅助数组tmp
        for(int k = lo; k <= hi; k++)
            tmp[k] = nums[k];
        //归并到nums[lo...hi]中
        int i = mid, j = hi;
        for(int k = hi; k >= lo; k--){
            if(i < lo) nums[k] = tmp[j--];     //左边数据用完，用右边的 
            else if(j < mid + 1) nums[k] = tmp[i--]; // 右边右边用完，用左边的
            else if(tmp[j] >= tmp[i]) nums[k] = tmp[j--];   //左边的值小于等于右边的, 没有产生逆序对
            else{
                nums[k] = tmp[i--];			//更新逆序对
                res += j - mid;
            }
        }

        return res;
    }
}
```

## 47. 两个链表的第一个公共节点

输入两个单向链表，找出它们的第一个公共节点。

###  方法一.  栈存储（以空间换时间）

> 分析：两个单向链表，如果从某一个结点开始相同，那么他们构成的一定是一个X型。如果从链表的末尾开始比较，那么出现第一个不同结点的上一个结点就是我们所求的第一个相同结点。这种FILO的方式让我们想到了栈，可以创建两个栈，分别存储两个链表的结点，然后一一弹出，直到遇到两站顶的结点不相同。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        Deque<ListNode> stack1 = new LinkedList<>();
        Deque<ListNode> stack2 = new LinkedList<>();
        ListNode node = headA;
        while(node != null){
            stack1.push(node);
            node = node.next;
        }
        node = headB;
        while(node != null){
            stack2.push(node);
            node = node.next;
        }
        while(stack1.peek() == stack2.peek() && !stack1.isEmpty() && !stack2.isEmpty()){
            stack1.pop();
            node = stack2.pop();
        }

        return node;
    }
}
```

###  方法二. 双指针法（与方法一时间复杂度相同，但空间复杂度低）

>分析：考虑两个链表的长度分别为a, b， 公共部分的结点数位c，不妨设a - b =2； 那么在第二次循环时候，只要让a先走两个结点，两个指针就会实现同步搜索，直到找到第一个公共结点。
>
>
>
>* 进一步提升的方法：让指针A 从 第一条链表的头结点开始走，直到走到第二条链表的公共结点，此时A走了 a+(b-c) 个结点，让指针B从第二条链表的头结点开始，一直走到第一条链表的公共结点，此时走了 b+(a - c) 个结点，此时，如果没有公共结点，那么A==B==null，否则A, B 所指向的便是第一个公共结点。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode A = headA, B = headB;
        while(A != B){
            A = A != null ? A.next : headB;
            B = B != null ? B.next : headA;
        }

        return A;
    }
}
```

## 48. 在排序数组中查找数字 I

统计一个数字在排序数组中出现的次数。

>在有序的数组中查找，自然而然的想到了二分法，但是找到目标target之后，要找有几个，还要找左右边界，如果此时按照遍历查找的方式，依然会使得复杂度O(n)，所以想到可以通过二分法查找左右边界，最后左右边界相减便可以得到。
>
>注意： 下面贴出的代码，所搜索的边界是外边界(指针指向的不是目标值)

```java
class Solution {
    public int search(int[] nums, int target) {
        int left, right;

        //找右边界
        int i = 0, j = nums.length -1;
        while(i <= j){
            int mid = (i + j)/2;
            if(nums[mid] <= target) i = mid + 1;
            else j = mid - 1;
        }

        right = i;

        //找左边界
        i = 0;
        j = nums.length - 1;
        while(i <= j){
            int mid = (i + j)/2;
            if(nums[mid] >= target) j = mid - 1;
            else i = mid + 1;
        }
        left = j;

        return (right -left - 1);
    }
}
```

## 49. 0～n-1中缺失的数字 II

一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

> 分析：0~n-1 只缺少一个数字，那么一定存在一个m+1，其是第m个数字(0是第0个数字),  那么我们的目标便成了搜索第一个下标小于数值的数。这是一个二分法查找的变型题。
>
> 注意: 我们查找数组中最后一个index与值相等的位置，该位置所对应的标签即为缺少的数

```java
class Solution {
    public int missingNumber(int[] nums) {
        int lo = 0, hi = nums.length-1;
        while(lo <= hi){
            int mid = (lo+hi)/2;
            if(nums[mid] == mid) lo = mid +1;
            else hi = mid - 1;
        }

        return lo;//lo > nums.length - 1 ? nums.length : nums[lo] - 1;
    }
}
```

## 50. 二叉搜索树的第k大节点

给定一棵二叉搜索树，请找出其中第k大的节点。

> 二叉搜索树，其中序遍历便是递增的序列。因此本题可以存储中序遍历的输出结果，并求得倒数第k个数据的值

中序遍历，可以由以下代码实现；

```java
// 打印中序遍历
void dfs(TreeNode root) {
    if(root == null) return;
    dfs(root.left); // 左
    System.out.println(root.val); // 根
    dfs(root.right); // 右
}
```



```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    int count = 1;
    public int kthLargest(TreeNode root, int k) {
        HashMap<Integer, Integer> nodeVal = new HashMap<>();
        rec(root, nodeVal);
        return nodeVal.get(nodeVal.size() + 1 - k);
    }

    public void rec(TreeNode node, HashMap<Integer, Integer> nodeVal){
        if(node == null)
            return;
        rec(node.left, nodeVal);
        nodeVal.put(count++, node.val);
        rec(node.right, nodeVal);
    }
}
```

* 更简单的一种改进方法：直接打印中序遍历的逆序

```java
// 打印中序遍历逆序
void dfs(TreeNode root) {
    if(root == null) return;
    dfs(root.right); // 右
    System.out.println(root.val); // 根
    dfs(root.left); // 左
}
```

只需记录打印数字的个数，然后对应记录结果，记得提前结束递归

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    int res, k;
    public int kthLargest(TreeNode root, int k) {
        this.k = k;
        rec(root);
        return res;
    }

    public void rec(TreeNode node){
        if(node == null)
            return;
        rec(node.right);
        if(k == 0) return;    //提前结束递归
        if(--k == 0) res = node.val;
        rec(node.left);
    }
}
```

## 51. 二叉树的深度

输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。

> 分析 ： 简单的二叉树遍历，并设置变量记录层数，在叶结点的时候，记录最大值。
>
> 注意： 传递基本数据类型的时候传递的形参，所以+1就是+1, 不能写成++

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    int res = 0;
    public int maxDepth(TreeNode root) {
        rec(root, 1);
        return res;
    }

    public void rec(TreeNode node, int deep){
        if(node == null){
            res = res > (deep-1) ? res : (deep -1);
            return;
        }
        rec(node.left, deep+1);
        rec(node.right, deep+1);
    }
}



//大佬更简单的写法
//树的深度是左子树深度与右子树深度的最大值 加一
class Solution {
    public int maxDepth(TreeNode root) {
        if(root == null) return 0;
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}
```

* 总结： 二叉树的常用搜索方式
* 1. DFS(深度优先搜索)  先序遍历，中序遍历，后续遍历
* 2. BFS(广度优先搜索)  层序遍历(一般借助堆栈)

##  52.平衡二叉树

输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

> 分析：先序遍历 + 剪枝 。 上一题中我们写出了求一棵树深度的代码，这题很容易想到判断每一个子结点的时候都计算其左右子树的深度，判断是否为平衡树，那么递归求解便可以得到这棵树是否为平衡树
>
> 这里我们要注意的是，如果左子树或右子树不是平衡树，那么便已经不需要判断结点数了，这便是剪枝的操作

自己写的一个复杂代码，后面发现可以优化掉数组变成一个值。剪枝的条件得写好。

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isBalanced(TreeNode root) {
        int[] depth = treeDepth(root);
        return depth[0] == 0 ? false : true;
    }

    public int[] treeDepth(TreeNode node){
        int[] res = {1, 0};
        if(node == null)
            return res;

        int[] resLeft = treeDepth(node.left);
        int[] resRight = treeDepth(node.right);
        if(resLeft[0] == 0 || resRight[0] == 0 || Math.abs(resLeft[1] - resRight[1]) > 1){
            res[0] = 0;
            return res;
        }else{
            res[1] = Math.max(resLeft[1], resRight[1]) + 1;
        }

        return res;
    } 
}
```

```java
//更加简便的一种写法，使用的内存空间更少
class Solution {
    public boolean isBalanced(TreeNode root) {
        return recur(root) != -1;
    }

    private int recur(TreeNode root) {
        if (root == null) return 0;
        int left = recur(root.left);
        if(left == -1) return -1;
        int right = recur(root.right);
        if(right == -1) return -1;
        return Math.abs(left - right) < 2 ? Math.max(left, right) + 1 : -1;
    }
}
```

* 第二种代码的写法，主要是其剪枝条件应用的合理，提前结束了循环。

## 53. 数组中数字出现的次数 I

一个整型数组 `nums`里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。

>  分析： 如果数组中只有一个出现了一次的数字，根据异或运算的规律，将数组中所有的数字异或，即可得到结果。 （凡是出现两次的数字都异或为0了），进一步思考该题，因为出现了两个不相等且只出现一次的数字，那么异或的结果一定是两个不相等的数字异或的值，一定不为0，我们只需要以其中不为0的位为标准，将数组分为两个部分，分别异或，得到的结果便是两个数字。

> * 注意：java 中没有数字的二进制常量表示形式
> * 逻辑运算符的优先级高于位运算符  == 优先级高于 & 
> * 异或的运算符为^

```java
class Solution {
    public int[] singleNumbers(int[] nums) {
        int key = 0;
        int count = 1;
        int[] res = {0,0}; 
        
        for(int i : nums){
            key ^= i;
        }

        //找到自右往左第一个不是0的位
        while((key & count) == 0){
            count <<= 1;
        }

        for(int i : nums){
            if((i & count) == 0)
                res[0] ^= i;
            else
                res[1] ^= i;
        }

        return res;
    }
}
```

## 53. 数组中数字出现的次数 II

在一个数组 `nums` 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。

>  		分析：除了一个数字外，其余数字都出现了三次，意味着，如果将数组中出现三次的数，每一个二进制位分别统计1出现的次数，那么所有二进制位统计的结果均是3的倍数。如果某一位不是三的倍数，那么一定是由于只出现一次的数造成的。  对该位设1即可得到最终所求的数。这种思路，当题目改为除一个数外其余数都出现了m次也适用。
>  							
>  			*  进阶思路：有限状态自动机，我们设置一个机器，存储每一位的1的统计个数除3后的余数，那么这样一个机器，其余数在0-1-2-0-1.....往复循环，由于0-2
>  			需要两位二进制存储，因而设置One 与 Two 分别存储有限状态自动机的高低位（Two为高位）。

```java
class Solution {
    public int singleNumber(int[] nums) {
        int one = 0, two = 0;
        for(int num : nums){
            one = one^num & ~ two;
            two = two^num & ~ one;
        }

        return one;
    }
}
```

* 分析one的变换，当two = 1的时候，无论输入的n是否为0，one都为0(进位或者保持不变)，当two=0的时候，one的更新值与输入的n有关，如果都为1，则进位为0，如果有一个为1，则为1，这是一种显然的异或XOR 关系，因此 one = one^n & ~two； 
* 我们进一步的探讨two的变化情况，注意此时的one已经变化完成 不妨设输入n=1， 变化前 00--01--10 ，那么变化后 01--00--10.如果 我们交换one与two可以看出 10--00--01依然为循环的进位方式，此时two处于one的位置，与one有相同的进位规则，因此one的公式也可以套用在two上。two = two^num % ~one;

```java
//另一种遍历计算二进制每一位1个数的方式
class Solution {
    public int singleNumber(int[] nums) {
        int[] counts = new int[32];
        for(int num : nums) {
            for(int j = 0; j < 32; j++) {
                counts[j] += num & 1;
                num >>>= 1;
            }
        }
        int res = 0, m = 3;
        for(int i = 0; i < 32; i++) {
            res <<= 1;
            res |= counts[31 - i] % m;
        }
        return res;
    }
}
```

## 54. 和为s的两个数字 I

输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。

> 		* 分析：双指针法，因为是排序数组，虽然使用HashMap可以将时间和空间复杂度都控制在O(N)但是，这种做法忽略了递增数组的条件，我们两个指针分别指向数组的头尾。如果计算的值大于目标值，那么尾指针左移，如果小于目标值，头指针右移。
> 		* 分析算法的正确性，看a[0] + a[j] > target 的情况， 此时j--，尾指针左移，相当于我们少了a[0] + a[j] 到a[j-1] + a[j]这些数 ，但是由于递增的特点，这些数一定大于target，因此是合理的舍弃

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int lo = 0, hi = nums.length - 1;
        while(nums[lo] + nums[hi] != target && lo < hi ){
            if(nums[lo] + nums[hi] > target)
                hi--;
            else lo++;
        }
        return new int[]{nums[lo], nums[hi]};
    }
}
```

## 54.  和为s的连续正数序列 II

输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。

> ​	分析：利用滑动窗口，首先将窗口的最小值设置为1，同时根据求和公式，设置最大值为(int)Math.sqrt(2 * target)。如果窗口内的和S 小于target，那么说明我们需要加入更多的数据，此时将最大值的指针右移一位，加入一个新的数据；如果这时候窗口和小于target，那么我们右移窗口的最小值，减少几个数据。
>
> * 注意：sum >= target的时候都要对lo++, 这样在存储完一个输出之后才能继续找下一个数据；

```
class Solution {
    public int[][] findContinuousSequence(int target) {
        int lo = 1, hi = (int)Math.sqrt(2 * target);
        int sum = (lo + hi)*(hi - lo + 1)/2;
        List<int[]> result = new ArrayList<>();

        while(lo < hi){
            if(sum == target){
                int[] aux = new int[hi - lo + 1];
                for(int i = 0; i <= hi - lo; i++)
                    aux[i] = lo + i;
                result.add(aux);
            }
            if(sum >= target){
                sum -= lo;
                lo++;
            }else{
                hi++;
                sum += hi;
            }
        }

        return result.toArray(new int[0][]);

    }

}
```

## 55. 翻转单词顺序

输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"。

要求：1.  输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。  例如： 输入 "      hello world!     "，输出 "world! hello"

			2.  如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。 例如： 输入 "a good        example"，输出 "example good a"

### 方法一. 库函数法

> ​	分析：最明显的一种思路便是用" "分割字符串，然后反向链接输出。
>
> ​	注意：1. 动态的字符串用StringBuilder 更快，concat存在复制过程，不建议使用
>
> 				2. split分割字符串之后，多个" "出现的地方会出现空字符串""，需要排除

```java
class Solution {
    public String reverseWords(String s) {
        String[] strs = s.split(" ");
        StringBuilder result = new StringBuilder();
        for(int i = strs.length - 1; i >= 0; i--){
            if(!strs[i].equals(""))
               result =  result.append(strs[i] + " ");
        }

        return result.toString().trim();  //删除末尾的空格
    }
}
```

### 方法二. 双指针法

* 倒序遍历字符串 ss ，记录单词左右索引边界 ii , jj ；
* 每确定一个单词的边界，则将其添加至单词列表 resres ；
* 最终，将单词列表拼接为字符串，并返回即可  

```java
class Solution {
    public String reverseWords(String s) {
        s = s.trim(); // 删除首尾空格
        int j = s.length() - 1, i = j;
        StringBuilder res = new StringBuilder();
        while(i >= 0) {
            while(i >= 0 && s.charAt(i) != ' ') i--; // 搜索首个空格
            res.append(s.substring(i + 1, j + 1) + " "); // 添加单词
            while(i >= 0 && s.charAt(i) == ' ') i--; // 跳过单词间空格
            j = i; // j 指向下个单词的尾字符
        }
        return res.toString().trim(); // 转化为字符串并返回
    }
}
```

> 注意 ： trim() 函数可以删除首尾的空格，且不会因为是空字符串报错，比substring(0, length -1)(容易越界)好用

## 55. 左旋转字符串II

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

### 方法一.  切分字符串拼接

```java
class Solution {
    public String reverseLeftWords(String s, int n) {
        return s.substring(n, s.length()) + s.substring(0, n);
    }
}
```

> 注意： substring()  所输入的首末位，末位是不包含在子串内的，如果要包含字符串最后一位，一定要设置末位为 s.length()

### 方法二. 列表遍历(StringBuilder)

```java
class Solution {
    public String reverseLeftWords(String s, int n) {
        StringBuilder res = new StringBuilder();
        for(int i = n; i < n + s.length(); i++)
            res.append(s.charAt(i % s.length()));
        return res.toString();
    }
}
```

> * 注意求余运算对代码的简化，使得不需要分为两段进行赋值，类似于循环状态机。

### 方法三. 字符相加

```java
class Solution {
    public String reverseLeftWords(String s, int n) {
        String res = "";
        for(int i = n; i < n + s.length(); i++)
            res += s.charAt(i % s.length());
        return res;
    }
}
```

> ​	注意：字符串加法每次都需要创建一个新的子串，十分浪费时间。

## 56. 滑动窗口的最大值(单调队列)I

给定一个数组 `nums` 和滑动窗口的大小 `k`，请找出所有滑动窗口里的最大值。

>​	分析：滑动窗口的数据更新规则是FIFO，这是队列的表现形式，我们需要知道队列的最大值，联想之前写过的包含最小值的栈，可以准备一个栈空间，记录滑动窗口的最大值。

创建一个单调队列，需要保证：

* 每轮窗口中有数据移除，单调队列中的数据也要移除
* 单调队列中的元素，非严格递减，每轮有新的元素加入窗口，需要将队列中小于该元素的队列元素全部删除(他们已经不可能是次最大值)
* 需要将新加入窗口的元素加入队列尾

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if(nums.length == 0 || k == 0) return new int[0];
        int[] result = new int[nums.length - k + 1];
        Deque<Integer> maxQueue = new LinkedList<>(); 

        //形成窗口前
        for(int i = 0; i < k; i++){
            while(!maxQueue.isEmpty() && maxQueue.peekLast() < nums[i])
                maxQueue.removeLast();
            maxQueue.addLast(nums[i]);
        }
        result[0] = maxQueue.peekFirst();

        //形成窗口后
        for(int i = k; i < nums.length; i++){
            //判断最大值是否移出窗口
            if(maxQueue.peekFirst() == nums[i - k])
                maxQueue.removeFirst();
            while(!maxQueue.isEmpty() && maxQueue.peekLast() < nums[i])
                maxQueue.removeLast();
            maxQueue.addLast(nums[i]);

            result[i - k + 1] = maxQueue.peekFirst();
        }

        return result;

    }
}
```

## 56.队列里的最大值II

请定义一个队列并实现函数 max_value 得到队列里的最大值，要求函数max_value、push_back 和 pop_front 的均摊时间复杂度都是O(1)。

> ​	分析：有了上一题的经验，我们可以知道，借助一个双端队列来进行最大值的获取。队列于窗口实质是一样的，窗口的移动实际上是将队列的添加队尾和删除队头放在了一起。这道题用单调队列保存最大值是可行的。
>
> * 复杂度计算的push与pop的平均复杂度，因此虽然push_back() 存在压栈的情况，但是复杂度依然是O(1)。

```java
class MaxQueue {
    Deque<Integer> queue;
    Deque<Integer> max;

    public MaxQueue() {
        queue = new LinkedList<>();
        max = new LinkedList<>();
    }
    
    public int max_value() {
        return max.isEmpty() ? -1 : max.peekFirst();
    }
    
    public void push_back(int value) {
        queue.addLast(value);
        while(!max.isEmpty() && max.peekLast() < value)
            max.removeLast();
        max.addLast(value);
    }
    
    public int pop_front() {
        int res = -1;
        if(!queue.isEmpty()){
            res = queue.pop();
            if(max.peekFirst() == res)
                max.removeFirst();
        }
        return res;
    }
}

/**
 * Your MaxQueue object will be instantiated and called as such:
 * MaxQueue obj = new MaxQueue();
 * int param_1 = obj.max_value();
 * obj.push_back(value);
 * int param_3 = obj.pop_front();
 */
```

## 57.n个骰子的点数(动态规划)

把n个骰子扔在地上，所有骰子朝上一面的点数之和为s。输入n，打印出s的所有可能的值出现的概率

> ​	分析：考虑x个骰子和为 n 的情况， 假设 x - 1个骰子各种情况的概率已知 ， 那么x个骰子 和为n 的概率 f(x,  n)  = f(x-1,  n -1) /6+ f(x-1,  n -1)/6 + f(x-1,  n -2)/6 + f(x-1,  n -3)/6 + f(x-1,  n -4)/6 + f(x-1,  n -5) /6+ f(x-1,  n -6)/6, 对应第x个骰子分别为1-6的六种情况，如果我们这样逆向的规划，则会出现bug，因为并非前六项一定存在比如f(2, 2),  并不存在f(1, -1) ,  因此想到可以正向的进行规划      **概率的贡献**  ，比如f(x-1,  n) 对于 f(x, n+1) ..........f(x, n+6) 的贡献为
>
> f(x-1,  n)/6.0，这种正向的动态规划巧妙的避免了条件判断问题
>
> * 第n个骰子，其范围在n — 6n，一共 6n - n +1 = 5 n +1 种情况
> * 第n个骰子的和最小值为n
> * 本题需要两个数组交替进行

```java
class Solution {
    public double[] dicesProbability(int n) {
        double[] dp = new double[6];
        Arrays.fill(dp, 1.0/6.0);
        //概率贡献法
        //骰子数
        for(int i = 2; i <= n; i++){
            double[] tmp = new double[5 * i + 1]; //n个骰子共6n-n+1种结果
            for(int j = 0; j < dp.length ; j++){   //上一个骰子的各种和概率
                for(int k = 0; k < 6; k++){			//当前骰子的各种情况
                    tmp[j + k] += dp[j] / 6.0;
                }
            }
            dp = tmp;
        }
        return dp;
    }
}
```

## 58. 扑克牌中的顺子

从扑克牌中随机抽5张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，**可以看成任意数字**。A 不能视为 14。

> ​	分析：首先对输入的数组排序，然后统计0的个数，由于0是可以充当任意数字，我们接下来统计后面非零的数据中，不相邻的的空缺位有多少，然后对比两个数，得到最后的结果。

### 方法一. 排序

```java
class Solution {
    public boolean isStraight(int[] nums) {
        int countZero = 0, countBlank = 0;
        int pNum = 0;
        Arrays.sort(nums);  //快速排序
        while(pNum < nums.length && nums[pNum] == 0) pNum++;
        countZero = pNum == 0 ? 0 : pNum;

        while(pNum < nums.length - 1){
            if(nums[pNum] == nums[pNum + 1])  //存在对子
                return false;

            countBlank += nums[pNum + 1] - nums[pNum] - 1;
            pNum++;
        }

        return countZero >= countBlank ? true : false;

    }
}
```

```java
// 更简便的写法
class Solution {
    public boolean isStraight(int[] nums) {
        int joker = 0;
        Arrays.sort(nums); // 数组排序
        for(int i = 0; i < 4; i++) {
            if(nums[i] == 0) joker++; // 统计大小王数量
            else if(nums[i] == nums[i + 1]) return false; // 若有重复，提前返回 false
        }
        return nums[4] - nums[joker] < 5; // 最大牌 - 最小牌 < 5 则可构成顺子
    }
}
```

> 第二种写法的主要简洁地方在于： 我们遍历扑克其实只是为了防止出现对子，遍历之后主要看最大值最小值的差是否小于5，如果大于5，那么0一定是补不齐的，如果小于5，那么一共五张排，剩下的0一定可以补齐。

### 方法二. HashSet

> 我们在HashSet中存储牌，遇到0不存，同时借助辅助变量获取最大最小值，如果出现对子，直接返回false。 最终依然是判断最大最小值的差。

```java
class Solution {
    public boolean isStraight(int[] nums) {
        Set<Integer> repeat = new HashSet<>();
        int max = 0, min = 14;
        for(int num : nums) {
            if(num == 0) continue; // 跳过大小王
            max = Math.max(max, num); // 最大牌
            min = Math.min(min, num); // 最小牌
            if(repeat.contains(num)) return false; // 若有重复，提前返回 false
            repeat.add(num); // 添加此牌至 Set
        }
        return max - min < 5; // 最大牌 - 最小牌 < 5 则可构成顺子
    }
}
```

## 59.  圆圈中最后剩下的数字(约瑟夫环问题)(动态规划)

0,1,···,n-1这n个数字排成一个圆圈，从数字0开始，每次从这个圆圈里删除第m个数字（删除后从下一个数字开始计数）。求出这个圆圈里剩下的最后一个数字。

例如，0、1、2、3、4这5个数字组成一个圆圈，从数字0开始每次删除第3个数字，则删除的前4个数字依次是2、0、4、1，因此最后剩下的数字是3。

### 补充知识点

* 1.  JAVA 取余运算

     负数对正数取余。 例子:   -2 % 3   =  -2

     正数对负数取余。 例子： 3 % -2 =  1

     负数对负数。         例子:    -3 % -2 = -1       **余数的正负号等于被除数的正负号**

> ​	分析：直观的想法是通过链表组成环来进行模拟删除过程，但是这种方法的复杂度在 O(n<sup>2</sup>)，并不适用于大规模的数学运算。
>
> * 定义函数f(n, m) 为n个数，每次删除第m个数，最后剩下的数。第一个删除的数显然是 (（m - 1） % n)，删除后，数字环将从下一个数( m % n)开始
>
> * 设(m % n) = t,  此时还剩下(n - 1)个数，但是这(n - 1)个数并不连续。我们将(n - 1, m)问题 中的 0........n-2 这n-1 个数映射到刚刚剩下的 n - 1个数上，0-> t, 1->t+1, 2-> t+2,....... n-2-> t-2.  可以看出映射公式为x->(x + t) % n。 
>
> * 通过第二步骤的映射，我们可以看出，如果已知(n - 1, m) 问题的解， 那么即可得到上面的（n, m）问题的解。即：
>
>   f(n) = (f(n - 1) + m) % n;

```java
class Solution {
    public int lastRemaining(int n, int m) {
        int dp = 0, result = 0;
        for(int i = 2; i <= n; i++){
            result = (dp + m) % i;
            dp = result; 
        }
        return result;
    }

}
```

## 60. 股票的最大利润(动态规划)

假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？

若输入为 [7,6,4,3,1] ，则输出0，没有交易完成。

> 动态规划分析：前i 日的最大利润 = 前 i - 1日的最大利润与  第 i 日卖出最大利润的 最大值
>
> 即我们需要 一个记录买入价格的变量， 一个记录最大利润的变量。买入价格以前i 日的最低值更新。

```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices.length <= 1)
            return 0;

        int pBuy = prices[0];   //记录买入价格
        int maxProfit =0; //记录最大利润
        for(int i = 1; i <= prices.length - 1; i++){
            if(prices[i] < pBuy) pBuy = prices[i];
            int profit = prices[i] - pBuy;
            maxProfit = maxProfit > (profit) ? maxProfit : profit;
        }

        return maxProfit;
    }
}
```

## 61. 求1+2+…+n

求 `1+2+...+n` ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

* 思路一.  依然从循环入手，不使用循环，递归函数因为需要if语句判断结束条件，也无法使用.  但是我们思考是否可以使用非条件语句来判断。逻辑运算符 &&， ||， ~ 有短路效果

```java
class Solution {
    public int sumNums(int n) {
        boolean x = n > 1 && (n += sumNums(n - 1)) > 0;
        return n;
    }
}
```

* 思路二.  不能使用乘法与除法，那我们可以使用的运算符便只剩下 加减，位运算，逻辑运算 **俄罗斯农民乘法**，A * B 如果 B的第 i 位 为1， 那么这一位对最后结果的贡献为A * (1 << i) ,  int 是一个16位的运算符，我们直接写16个代码, 利用前n项和公式计算。

```
class Solution {
    public int sumNums(int n) {
        int ans = 0, A = n, B = n + 1;
        boolean flag;

        flag = ((B & 1) > 0) && (ans += A) > 0;
        A <<= 1;
        B >>= 1;

        flag = ((B & 1) > 0) && (ans += A) > 0;
        A <<= 1;
        B >>= 1;

        flag = ((B & 1) > 0) && (ans += A) > 0;
        A <<= 1;
        B >>= 1;

        flag = ((B & 1) > 0) && (ans += A) > 0;
        A <<= 1;
        B >>= 1;

        flag = ((B & 1) > 0) && (ans += A) > 0;
        A <<= 1;
        B >>= 1;

        flag = ((B & 1) > 0) && (ans += A) > 0;
        A <<= 1;
        B >>= 1;

        flag = ((B & 1) > 0) && (ans += A) > 0;
        A <<= 1;
        B >>= 1;

        flag = ((B & 1) > 0) && (ans += A) > 0;
        A <<= 1;
        B >>= 1;

        flag = ((B & 1) > 0) && (ans += A) > 0;
        A <<= 1;
        B >>= 1;

        flag = ((B & 1) > 0) && (ans += A) > 0;
        A <<= 1;
        B >>= 1;

        flag = ((B & 1) > 0) && (ans += A) > 0;
        A <<= 1;
        B >>= 1;

        flag = ((B & 1) > 0) && (ans += A) > 0;
        A <<= 1;
        B >>= 1;

        flag = ((B & 1) > 0) && (ans += A) > 0;
        A <<= 1;
        B >>= 1;

        flag = ((B & 1) > 0) && (ans += A) > 0;
        A <<= 1;
        B >>= 1;

        return ans >> 1;
    }
}
```

* 思路三，利用构造函数，可以定义一个静态的成员变量，在构造方法中对其进行++操作，我们创建一个长度为n的数组，那么便可以得到前n项和。

## 62. 不用加减乘除做加法

写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。

> ​	分析：计算机中，所有的数都是以补码的形式存储的，因此即使a，b之间有负数，也不影响。模仿十进制的计算方法，我们分为三步
>
> * 1. 无进位的加法运算，相当于1 + 0 = 1， 1 + 1 = 0,  0 + 0 = 0.   与异或  ^ 运算相同。
>   2. 计算进位。 同为1，才是1，否则均为0. 与 & 运算相同.
>   3. 注意 计算完进位记得 左移一位 <<

```java
class Solution {
    public int add(int a, int b) {
        while(b != 0){
            int tmp = (a & b) << 1;  //计算进位
            a = a ^ b;              //  无进位的加法
            b = tmp;
        }

        return a;
    }
}
```

## 63. 构建乘积数组

给定一个数组 A[0,1,…,n-1]，请构建一个数组 B[0,1,…,n-1]，其中 B[i] 的值是数组 A 中除了下标 i 以外的元素的积, 即 B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]。不能使用除法。

> ​	分析：可以将乘积分为两个部分，A[0] * A[1] *.......A[i] ,    与  A[I+1], A[i+2], A[i+3]........A[n - 1], 可以知道B中的元素，列成一个矩阵就是上三角部分与下三角部分。对于前半部分的乘积是递增的顺序，而对于后半部分可以看作自下而上的递增。

```java
class Solution {
    public int[] constructArr(int[] a) {
        if(a.length == 0) return new int[0];
        int[] result = new int[a.length];
        result[0] = 1;
        for(int i = 1; i <= a.length - 1; i++){    //上三角部分
            result[i] = result[i - 1] * a[i - 1];
        }
        int tmp = 1;
        for(int i = a.length - 2; i >= 0; i--){		//下三角部分
            tmp *= a[i + 1];
            result[i] *= tmp;
        }

        return result;
    }
}
```

## 64. 把字符串转换成整数

写一个函数 StrToInt，实现把字符串转换成整数这个功能。不能使用 atoi 或者其他类似的库函数。

 

* 首先，该函数会根据需要丢弃无用的开头空格字符，直到寻找到第一个非空格的字符为止。

* 当我们寻找到的第一个非空字符为正或者负号时，则将该符号与之后面尽可能多的连续数字组合起来，作为该整数的正负号；假如第一个非空字符是数字，则直接将其与之后连续的数字字符组合起来，形成整数。

* 该字符串除了有效的整数部分之后也可能会存在多余的字符，这些字符可以被忽略，它们对于函数不应该造成影响。  

* 注意：假如该字符串中的第一个非空格字符不是一个有效整数字符、字符串为空或字符串仅包含空白字符时，则你的函数不需要进行转换。  

  在任何情况下，若函数不能进行有效的转换时，请返回 0。

* 说明： 假设我们的环境只能存储 32 位大小的有符号整数，那么其数值范围为 [-2<sup>31</sup>, 2<sup>31</sup> - 1]。如果数值超过这个范围，请返回  INT_MAX ( 2<sup>31</sup> - 1) 或 INT_MIN (-2<sup>31</sup>) 

> 分析：
>
> 1. 丢弃开头的空格，代码写的时候容易误判把中间的空格也丢弃，中间出现空格直接返回
> 2. 出现多余字符的提前终止循环
> 3. 开头的 + - 有效，中间的 + -也是无效字符
> 4. 数字越界处理过程中，由于我们使用的变量也是int型，需要保证比较过程中变量不越界，因此可在拼接前判断越界

```java
class Solution {
    public int strToInt(String str) {
        int signFlag = 1;
        int result = 0;
        boolean start = false;
        int bndry = Integer.MAX_VALUE / 10;
        int i = 0;
        while(i < str.length() && str.charAt(i) == ' ') i++;  //直接找到第一个非空字符
        for(; i < str.length(); i++){
            if(!start && str.charAt(i) == '+'){   //第一个正号，不处理
                start = true;  
            }else if(!start && str.charAt(i) == '-'){
                start = true;
                signFlag = -1;
            }else if(str.charAt(i) <= '9' && str.charAt(i)  >= '0'){
                start = true;
                if(result > bndry || result == bndry  && str.charAt(i) > '7'){
                    return signFlag == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
                }else result = result * 10 + str.charAt(i) - '0';
            }else break;
        }

        return result * signFlag;
    }
}
```

* 简化的写法

```java
class Solution {
    public int strToInt(String str) {
        int res = 0, bndry = Integer.MAX_VALUE / 10;
        int i = 0, sign = 1, length = str.length();
        if(length == 0) return 0;
        while(str.charAt(i) == ' ')
            if(++i == length) return 0;
        if(str.charAt(i) == '-') sign = -1;
        if(str.charAt(i) == '-' || str.charAt(i) == '+') i++;
        for(int j = i; j < length; j++) {
            if(str.charAt(j) < '0' || str.charAt(j) > '9') break;
            if(res > bndry || res == bndry && str.charAt(j) > '7')
                return sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
            res = res * 10 + (str.charAt(j) - '0');
        }
        return sign * res;
    }
}
```

* 注意： JAVA中的Integer.MAX_VALUE 可以直接使用
* 将读取正负号的语句放在外边可进一步优化代码。省去了start的boolean

## 65. 二叉搜索树的最近公共祖先 I（LCA）

给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。（LCA）

最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。

根据最近公共祖先的定义，可以知道结点node是p，q的最近公共祖先存在三种情况。

1. p 和 q分布在node的子树中，且分布在异侧
2. p == node ，且 q在node的左子树或右子树
3. q == node， 且p在node的左子树或右子树

* 本题题干显示树是二叉搜索树，且树上的结点都是唯一的，如果node.val 比 q，p的值都小，那么最近公共祖先在node的右子树，
* 如果node.val 比 q，p的值都大，那么最近公共祖先一定在node的左子树

注意： 按这种搜索方式，第一个node.val >= minVal && node.val <= maxVal 的结点一定是最近公共祖先

### 方法一.  递归 时间复杂度O(N), 空间复杂度O(N)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        int maxVal = Math.max(p.val, q.val);    //找到最大值
        int minVal = Math.min(p.val, q.val);
        return rec(root, maxVal, minVal);
    }

    public TreeNode rec(TreeNode node, int maxVal, int minVal){
        if(node.val >= minVal && node.val <= maxVal)
            return node;

        if(node.val > maxVal) 
            return rec(node.left, maxVal, minVal);
        else
            return rec(node.right, maxVal, minVal);
    }
}


//代码可优化为
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root.val < p.val && root.val < q.val)
            return lowestCommonAncestor(root.right, p, q);
        if(root.val > p.val && root.val > q.val)
            return lowestCommonAncestor(root.left, p, q);
        return root;
    }
}
```

### 方法二. 迭代

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        while(root != null) {
            if(root.val < p.val && root.val < q.val) // p,q 都在 root 的右子树中
                root = root.right; // 遍历至右子节点
            else if(root.val > p.val && root.val > q.val) // p,q 都在 root 的左子树中
                root = root.left; // 遍历至左子节点
            else break;
        }
        return root;
    }
}
```

> **以上两种写法的优化代码，都是将找到最近公共祖先的情况放在了else上，因为其判断条件比较繁琐。正是正难则反的表现**

## 65. 二叉树的最近公共祖先II  （LCA）

> ​	分析： 二叉树是一个无序的结构，我们可以先遍历，找到从root分别到两个结点的路径，然后存储在两个队列，接下来便是求两个链表的最后一个公共结点的题。（队列头部是root）

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        Deque<TreeNode> stack1 = new LinkedList<>();
        Deque<TreeNode> stack2 = new LinkedList<>();
        TreeNode result = root;

        findRoad(root, p, stack1);
        findRoad(root, q, stack2);

        while(!stack1.isEmpty() && !stack2.isEmpty() && stack1.peek() == stack2.peek()){
            result = stack1.pop();
            stack2.pop();
        }

        return result;
    }

    public void findRoad(TreeNode root, TreeNode node, Deque<TreeNode> stack){
        
        stack.add(root);
        if(root == node) return;

        if(root.left != null) findRoad(root.left, node, stack);
        if(stack.peekLast() == node)   return;
        if(root.right != null) findRoad(root.right, node, stack);
        if(stack.peekLast() == node)   return;

        stack.removeLast();  //回溯
    }
}
```

**代码优化**：后序遍历  从底至顶回溯

每遍历一个结点，我们就判断p，q两个结点是在该结点的左子树还是右子树，或者是该结点本身。

1. 当 left和 right 同时为空 ：说明 root 的左 / 右子树中都不包含 p,q  返回 null ；
2. 当 left 和 right 同时不为空 ：说明 p, q分列在 root 的 异侧 （分别在 左 / 右子树），因此 root 为最近公共祖先，返回 root ；
3. 当 left 为空 ，right 不为空 ：p,q都不在 root 的左子树中，直接返回 right 。具体可分为两种情况：
   (1) p,q 其中一个在 root 的 右子树 中，此时 right 指向 p（假设为 p ）；
   (2) p,q两节点都在 root 的 右子树 中，此时的 right 指向 最近公共祖先节点 ；   //不会再继续往下找了
4. 当 left 不为空 ， right 为空 ：与情况 3. 同理;

情况 1可以合并到 3与4内

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null || root == p || root == q) return root;
        TreeNode left = lowestCommonAncestor(root.left, p, q);   //返回的是该结点的左子树包含的结点(p 或者 q)
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if(left == null) return right;
        if(right == null) return left;
        return root;
    }
}
```

## 66. 矩阵中的路径(回溯法)（多步骤组成的问题）

请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一格开始，每一步可以在矩阵中向左、右、上、下移动一格。如果一条路径经过了矩阵的某一格，那么该路径不能再次进入该格子。例如，在下面的3×4的矩阵中包含一条字符串“bfce”的路径（路径中的字母用加粗标出）。

> ​	分析：题中表示可以从任意结点开始，但是我们所求的路径中间是不允许插入其他结点的。因此可以直接遍历二维数组，找到第一个目标路径的第一个结点作为开始结点，之后判断其上下左右是否右下一个结点。
>
> 剪枝操作： 当行列坐标越界，或者当前位置的字符不等于目标路径的字符，返回false。
>
> 不踏入同一个字符，将该字符设置为  ‘ \0’ ，在回溯的时候再将其回复为words[i]

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        char[] words = word.toCharArray();
        //双循环遍历数组，找到期望路径开始的结点
        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board[0].length; j++)
                if(dfs(board, words, i, j, 0)) return true;
        }

        return false;
    }

    public boolean dfs(char[][] board, char[] words, int i, int j, int k){
        if(i < 0 || i >= board.length || j < 0 || j >= board[0].length || board[i][j] != words[k])  return false;
        if(k == words.length - 1)   //剪枝
        return true;
        board[i][j] = '\0';   //标记已经走过
        boolean res = dfs(board, words, i+1, j, k+1) || dfs(board, words, i-1, j, k+1) ||
                      dfs(board, words, i, j-1, k+1) || dfs(board, words, i, j+1, k+1);
        board[i][j] = words[k];   //回溯
        return res;
    }
}
```

## 67.机器人运动范围

地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

### 方法一. 深度优先搜索DFS

> 分析： 根据数位和增量公式得知，数位和每逢 进位 突变一次。根据此特点，矩阵中 满足数位和的解 构成的几何形状形如多个 等腰直角三角形 ，每个三角形的直角顶点位于 0, 10, 20, ...0,10,20,... 等数位和突变的矩阵索引处。
>
> ```java
> (x + 1) % 10 != 0 ? s_x + 1 : s_x - 8; //数位和增量公式，仅仅在1-100内变化的坐标使用
> ```
>
> 根据可达解的分布情况，我们可以知道，只需要对下方和右方遍历，便可以找到所有的可达解。

```java
class Solution {
    int m, n, k;
    boolean[][] visited;
    public int movingCount(int m, int n, int k) {
        this.m = m; this.n = n; this.k = k;
        this.visited = new boolean[m][n];
        return dfs(0, 0);
    }

    public int dfs(int i, int j){
        if(i >= m || j >= n || !canMove(i, j) || visited[i][j]) return 0;
        visited[i][j] = true;

        return 1 + dfs(i, j + 1) + dfs(i + 1, j);
    }

    public boolean canMove(int i, int j){
        int result = 0;
        while(i > 0){
            result += i % 10;
            i /= 10;
        }
        while(j > 0){
            result += j % 10;
            j /= 10;
        }

        return result <= k ? true : false;
    }
}
```

### 方法二. 广度优先搜索BFS(按照平推的方式向前搜索)

通常使用队列实现广度优先搜索

* 初始化： 将机器人初始点 (0, 0)(0,0) 加入队列 queue ；
* 迭代终止条件： queue 为空。代表已遍历完所有可达解。
* 迭代工作：
  1. 单元格出队： 将队首单元格的 索引、数位和 弹出，作为当前搜索单元格。
  2. 判断是否跳过： 若 ① 行列索引越界 或 ② 数位和超出目标值 k 或 ③ 当前元素已访问过 时，执行 continue 。
  3. 标记当前单元格 ：将单元格索引 (i, j) 存入 Set visited 中，代表此单元格 已被访问过 。
  4. 单元格入队： 将当前元素的 下方、右方 单元格的 索引、数位和 加入 queue 。
     返回值： Set visited 的长度 len(visited) ，即可达解的数量。

```java
class Solution {
    public int movingCount(int m, int n, int k) {
        boolean[][] visited = new boolean[m][n];
        int res = 0;
        Queue<int[]> queue= new LinkedList<int[]>();
        queue.add(new int[] { 0, 0, 0, 0 });
        while(queue.size() > 0) {
            int[] x = queue.poll();
            int i = x[0], j = x[1], si = x[2], sj = x[3];
            if(i >= m || j >= n || k < si + sj || visited[i][j]) continue;
            visited[i][j] = true;
            res ++;
            queue.add(new int[] { i + 1, j, (i + 1) % 10 != 0 ? si + 1 : si - 8, sj });
            queue.add(new int[] { i, j + 1, si, (j + 1) % 10 != 0 ? sj + 1 : sj - 8 });
        }
        return res;
    }
}

```

## 68. 剪绳子I(动态规划与贪婪算法)

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

**动态规划问题的特点：**

* 求一个问题的最优解
* 整体的最优解依赖于各个子问题的最优解
* 大问题可以分解为子问题，子问题也可以继续分解为子问题
* 可以从上向下分解，但是从下向上计算

设第一个剪的位置为i，那么f(n) = max(f(i) * f(n - i)),  以此递推。我们可以从f(2) = 2, f(3) = 3, f(4) = 4, 入手， 反向递推，每次都将最优值存在数组的对应位置上，并且求一个新的长度时候，都需要遍历之前的数组，求max(f(i) * f(n - i))。时间复杂度O(n<sup>2</sup>), 空间复杂度O(n)。不符合复杂度要求

**贪婪算法：**

每一步都做出一个贪婪选择，基于这个选择，最终推导最优解。一般需要基于数学分析。

推论一、 若切分方案合理，会带来更大的乘积(切比不切好)

推论二、若切分方案合理，切的越多，乘积越大

推论三、为使乘积最大，只有长度为2和三的绳子不应该再切，且3比2更优

```java
class Solution {
    public int cuttingRope(int n) {
        if(n <= 3) return n-1;
        int pow = n / 3, rem = n % 3;
        if(rem == 1) return (int)Math.pow(3, pow - 1) * 4;
        if(rem == 2) return (int)Math.pow(3, pow) * 2;
        return (int)Math.pow(3, pow);
    }
}
```

## 68. 剪绳子II(贪婪算法与大数求余)

为防止数据越界，对大数求余。

方案：循环求余，快速幂求余。**其中后者时间复杂度更低**, 两者均根据下面的求余运算规则推导出来

```java
(xy)%p = [(x%p)(y%p)]%p
```

### 一、循环求余

根据以上性质可以推导出：x < p

x<sup>a</sup> ⊙ p = [(x<sup>a-1</sup>⊙ p)(x ⊙ p)] ⊙ p = [(x<sup>a-1</sup> ⊙ p) x ] ⊙p

利用此公式可以循环求x<sup>1</sup>, x<sup>2</sup>...... x<sup>a-1</sup>, x<sup>a</sup>对p的余数，保证每轮结果都在int32范围内

```java
public remainder(x,a,p){
	int rem = 1;
    	for(int i = 0; i <= a; i++)
            rem = rem * x % p;
    return rem;
}
```

### 二、快速幂求余

根据求余的运算性质可以推导出：

x<sup>a</sup> ⊙ p = (x<sup>2</sup>)<sup>a/2</sup>  ⊙ p = (x<sup>2</sup> ⊙ p) <sup>a/2</sup>⊙p

```java
public remainder(x,a,p){
	int rem = 1;
    	while(a > 0){
            if( a % 2 == 1) rem = (rem * x) % p;
            x = Math(x, 2) % p;
            a /= 2;  //向下取整的除法
        }
    return rem;
}
```

初始状态 rem=1rem=1, x=3x=3, a=19a=19, p=1000000007p=1000000007 ，最后会将 rem * (x<sup>a</sup>⊙p )化为 rem×(x<sup>0</sup>⊙p)=rem×1 的形式，即 rem 为余数答案。

```java
class Solution {
    public int cuttingRope(int n) {
        if(n <= 3) return n - 1;
        int  b = n % 3, p = 1000000007;
        long rem = 1, x = 3;
        for(int a = n / 3 -1; a > 0; a /= 2){
            if(a % 2 == 1) rem = (rem * x) % p;     //该为存在值
             x = (x * x) % p;
        }
		// a = n / 3 -1， 特意留了一个3 跟余数匹配
        if(b == 0) return (int)(rem * 3 % p);
        if(b == 1) return (int)(rem * 4 % p);
        return (int)(rem * 6 % p);  //余数2，加上之前剩下的3，配成6
    }
}
```

## 69. [正则表达式匹配](https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/)(动态规划)(非确定有限状态机)

请实现一个函数用来匹配包含'. '和'*'的正则表达式。模式中的字符'.'表示任意一个字符，而'*'表示它前面的字符可以出现任意次（含0次）。在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但与"aa.a"和"ab*a"均不匹配。

**解题思路：**

设 s 的长度为 n ， p 的长度为 m；将 s的第 i个字符记为 s<sub>i</sub>，p的第 j个字符记为 p<sub>j</sub>，将 s 的前 i个字符组成的子字符串记为 s[ : i ], 同理将 p的前 j个字符组成的子字符串记为 p[ :j ] 。因此，本题可转化为求 s[:n] 是否能和 p[:m] 匹配。这样做的主要原因是如果遍历到p的 字符为 “ * ”, 它既可以转向下一个字符，也可以保持原状态，无法直接在简单的循环中遍历。

```java
class Solution {
    public boolean isMatch(String s, String p) {
        int m = s.length() + 1, n = p.length() + 1;
        boolean[][] dp = new boolean[m][n];    //额外增加一行一列保存空字符串形式
        dp[0][0] = true;
        for(int j = 2; j < n; j += 2)
            dp[0][j] = dp[0][j-2] && p.charAt(j-1) == '*';
        for(int i = 1; i < m; i++){
            for(int j = 1; j < n; j++){
                dp[i][j] = p.charAt(j - 1) == '*' ? 
                dp[i][j-2] || dp[i-1][j] &&(s.charAt(i-1) == p.charAt(j-2) || p.charAt(j-2) == '.') 
                : dp[i-1][j-1] && (s.charAt(i-1) == p.charAt(j-1) || p.charAt(j-1) == '.');
            }
        }

        return dp[m-1][n-1];
    }
}
```

* 状态定义： 设动态规划矩阵 dp ， dp\[i][j] 代表字符串 s 的前 i 个字符和 p 的前 j 个字符能否匹配。

* 转移方程： 需要注意，由于 dp\[0][0] 代表的是空字符的状态， 因此 dp\[i][j]对应的添加字符是 s[i - 1] 和 p[j - 1] 。
  * 当 p[j - 1] = '*' 时， dp[i][j] 在当以下任一情况为 true 时等于 true ：

1. dp\[i][j - 2]： 即将字符组合 p[j - 2] * 看作出现 0 次时，能否匹配；
2. dp\[i - 1][j] 且 s[i - 1] = p[j - 2]: 即让字符 p[j - 2] 多出现 1 次时，能否匹配；(s没有新增字符时候是不是匹配，且s新增的字符与p*之前的字符相同)
3. dp\[i - 1][j] 且 p[j - 2] = '.': 即让字符 '.' 多出现 1 次时，能否匹配；
   * 当 p[j - 1] != '*' 时， dp[i][j] 在当以下任一情况为 truetrue 时等于 truetrue ：

1. dp\[i - 1][j - 1] 且 s[i - 1] = p[j - 1]： 即让字符 p[j - 1] 多出现一次时，能否匹配；
2. dp\[i - 1][j - 1] 且 p[j - 1] = '.'： 即将字符 . 看作字符 s[i - 1] 时，能否匹配；

## 70. 表示数值的字符串(有限状态机)

请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，字符串"+100"、"5e2"、"-123"、"3.1416"、"-1E-16"、"0123"都表示数值，但"12e"、"1a3.14"、"1.2.3"、"+-5"及"12e+5.4"都不是。

定义 0- 8 九种状态

0. 开始的空格
1. 幂符号前的正负号
2. 小数点前的数字
3. 小数点、小数点后的数字
4. 当小数点前为空格时，小数点、小数点后的数字幂符号
5. 幂符号后的正负号
6. 幂符号后的数字
7. 结尾的空格

我们遍历字符串，并设置符号代表get的字符类型

​		其中 当 c 为正负号的时候，t = 's'

​		当 c 为数字的时候， t = 'd' ;

​		当 c 为 e， E的时候， t = 'e'

​		当 c 为 . , 空格 时候， t = c

​		否则执行 t = '?'  代表不可识别的非法字符，剪枝操作直接返回false

![](C:\Users\WangTao\Desktop\6f41d7e46fd0344c013980e3f46429dd7a7311bb4292783a482466a90f15747b-Picture1.png)

```java
class Solution {
    public boolean isNumber(String s) {
        Map[] states = {
            new HashMap<>(){{put(' ', 0); put('s', 1); put('d', 2); put('.', 4);}}, //0 起始blank
            new HashMap<>(){{put('d',2); put('.',4);}}, //1  e 之前的正负号
            new HashMap<>(){{put('d',2); put('e',5); put(' ',8); put('.', 3);}}, //2  dot之前的数字
            new HashMap<>(){{put('d',3); put('e',5); put(' ',8);}}, //3  dot之后的数字
            new HashMap<>(){{put('d',3);}}, //4  dot前为空的时候，dot之后的digit
            new HashMap<>(){{put('s',6); put('d',7);}}, //5  e
            new HashMap<>(){{put('d',7);}}, //6  e之后sign
            new HashMap<>(){{put('d',7); put(' ',8);}}, //7  e之后的digit
            new HashMap<>(){{put(' ',8);}} //8  尾部的blank
        };
        char c;
        int res = 0;
        for(int i = 0; i < s.length(); i++){
            if(s.charAt(i) <= '9' && s.charAt(i) >= '0') c = 'd';
            else if(s.charAt(i) == '+' || s.charAt(i) == '-')  c = 's';
            else if(s.charAt(i) == 'e' || s.charAt(i) == 'E')  c = 'e';
            else if(s.charAt(i) == '.' || s.charAt(i) == ' ')  c = s.charAt(i);
            else c = '?';
            if(!states[res].containsKey(c))  return false;
            res = (int)states[res].get(c);
        }

        return res == 2 || res == 3 || res == 7 || res == 8 ? true : false;
    }
}
```

**注意：HashMap的双大括号创建并初始化** 

此代码识别 " 3.  " 是一个数字，真的对吗?

## 补充知识一：求两数的最大公约数（欧几里得除法）

用大除以小数，得到余数，如果余数不是0，则继续用较小的除数 除以 余数，不断的循环，直到某次的余数为0，此时除数即为最大公约数

```java
    //求最大公约数
    public static  int gCommonDivisor(int i, int j){
        int tmp = 0;
        if(i < j){
            tmp = j; j = i; i = tmp;
        }
        while(j != 0){
            tmp = i % j;
            i = j;
            j = tmp;
        }
        return i;
    }
```

* 注意： 此题目也可变形为求两个数的最小公倍数

## 补充知识二：求一个数的立方根

####  方法一：x<sup>3</sup> 单调递增，二分查找

```java

	// 使用二分查找算法
	public static double getCubeRoot(double input)
	{
		double min = 0;
		double max = input;
		double mid = 0;
        
        // 注意，这里的精度要提高一点，否则某些测试用例无法通过
		while ((max - min) > 0.001)
		{
			mid = (max + min) / 2;
			if (mid * mid * mid > input)
				max = mid;
			else if (mid * mid * mid < input)
				min = mid;
			else
				return mid;
		}
		return max;
	}
```

#### 方法二：牛顿迭代 x<sub>n+1</sub>=x<sub>n</sub> - f( x<sub>n</sub>)/f <sup>'</sup>( x<sub>n</sub>)   f( x) = x<sup>3</sup>-y

```java
    public static double cubeRoot(double num){
        double res = 1.0;
        while(Math.abs(res*res*res + num) > 0.01)
            res = (2*res-num/res/res)/3;
        return num > 0 ? Math.abs(res) : -Math.abs(res);
    }
```

### 补充三：前缀树

Trie（发音类似 "try"）或者说 前缀树 是一种树形数据结构，用于高效地存储和检索字符串数据集中的键。这一数据结构有相当多的应用情景，例如自动补完和拼写检查。

功能：既可以搜索单词，也可以搜索单词的前缀是否存在

**解析：**每个结点包含以下字段

1. 指向子节点的指针数组children，对于本题，数组长度位26，即为小写英文字母的数量。
2. boolean字段isEnd，表示该结点是否为字符串的结尾

```java
/**
 * 前缀树，保存单词
 * 既可以查找单词是否被保存，也可以查找是否有对应的前缀
 *
 * 分析：多叉树，每个节点维持一个数组，保存字典，即当前位可能出现的所有字符，，表示为数组的每一个位置
 * 数组的每一个位置上都保存下一个结点的地址，并维持一个位，记录当前结点是否为一个字符串的末尾
 */
public class Trie {
    private Trie[] children;
    private boolean isEnd;

    public Trie() {
        //26个小写单词
        children = new Trie[26];
        isEnd = false;
    }

    /** Inserts a word into the trie. */
    public void insert(String word) {
        Trie node = this;
        for (int i = 0; i < word.length(); i++) {
            int index = word.charAt(i) - 'a';
            //该位置上还没有元素
            if(node.children[index] == null){
                node.children[index] = new Trie();
            }
            node = node.children[index];
        }
        node.isEnd = true;
    }

    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        Trie node = searchPrefix(word);
        return node != null && node.isEnd;
    }

    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        return searchPrefix(prefix) != null;
    }

    private Trie searchPrefix(String prefix){
        Trie node = this;
        for(int i = 0; i < prefix.length(); i++){
            int index = prefix.charAt(i) - 'a';
            if(node.children[index] == null){
                return  null;
            }
            node = node.children[index];
        }
        return node;
    }
}
```

