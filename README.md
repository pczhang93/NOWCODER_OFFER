# NOWCODER_OFFER
剑指Offer牛客网刷题的代码本。
都是牛客网OJ验证通过的代码。

### 20180626  

#### 二维数组中的查找  

题目描述：  

在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。
~~~
# -*- coding:utf-8 -*-
class Solution:
    # array 二维列表
    def Find(self, target, array):
        # write code here
        i = 0
        j = len(array[0]) - 1  # numbers of columns
        while i < len(array) and j >= 0:
            if array[i][j] == target:
                return True
            elif array[i][j] < target:
                i += 1
            else:  #array[i][j] > target
                j -= 1
        return False
~~~
### 20180627 
#### 替换空格 

题目描述：

请实现一个函数，将一个字符串中的空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

~~~
# -*- coding:utf-8 -*-
class Solution:
    # s 源字符串
    def replaceSpace(self, s):
        # write code here
        # s.replace(' ', '%20')
        s = s.replace(' ', '%20')
        return s
~~~
感觉用Python这么写有点心虚。
参考书上的C++思路：
~~~
class Solution {
public:
    void replaceSpace(char *str,int length) {
        int numberOfSpace = 0;
        int originalLength = 0;
        int i = 0;
        while(str[i] != '\0')
        {
            ++originalLength;
            if (str[i] == ' ')
            {
                ++numberOfSpace;
            }
             
            ++i; 
        }
        int newLength = originalLength + numberOfSpace * 2;
        int indexOfOriginal = originalLength;
        int indexOfNew = newLength;
        while(indexOfOriginal >= 0 && indexOfNew > indexOfOriginal)
        {
            if (str[indexOfOriginal] == ' ')
            {
                str[indexOfNew--] = '0';
                str[indexOfNew--] = '2';
                str[indexOfNew--] = '%';
            }
            else
            {
                str[indexOfNew--] = str[indexOfOriginal];
            }
            --indexOfOriginal;
        }
         
 
    }
};
~~~
#### 从尾到头打印链表 

题目描述：输入一个链表，从尾到头打印链表每个节点的值。
还是用C++刷题爽。
~~~
/**
*  struct ListNode {
*        int val;
*        struct ListNode *next;
*        ListNode(int x) :
*              val(x), next(NULL) {
*        }
*  };
*/
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        std::stack<ListNode*>nodes;
         
        ListNode* pNode = head;
        while(pNode != NULL)
        {
            nodes.push(pNode);
            pNode = pNode -> next;
        }
        std::vector<int>reverseVector;
        while(!nodes.empty())
        {
            pNode = nodes.top();
            cout << pNode -> val << endl;
            reverseVector.push_back(pNode -> val);
            nodes.pop();
        }
        return reverseVector;
         
    }
};
~~~
### 20180628 
#### 用两个栈实现队列 

题目描述：
用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。
~~~
class Solution
{
public:
    void push(int node) {
        stack1.push(node);     
    }

    int pop() {
        int i, e;
        while(!stack1.empty()){
            i = stack1.top();
            stack2.push(i);
            stack1.pop();
        }
        e = stack2.top();
        stack2.pop();
        while(!stack2.empty()){
            i = stack2.top();
            stack1.push(i);
        }
        return e;
        
    }

private:
    stack<int> stack1;
    stack<int> stack2;
};
~~~
不通过。
内存超限:您的程序使用了超过限制的内存。

看书上思路，修改代码。主要是每次出栈后可以先不将stack2的元素逐个送回stack1，每次出队可以直接从stack2.pop()，直到stack2为空再从stack1逐个送元素入stack2.
~~~
class Solution
{
public:
    void push(int node) {
        stack1.push(node); 
    }
 
    int pop() {
        int e;  
        if(stack2.empty()){
            if (!stack1.empty()){
            while(!stack1.empty()){
                stack2.push(stack1.top());
                stack1.pop();
            }
            e = stack2.top();
            stack2.pop();
            return e;
            }
             
            else
                return -1;
            }
        else{  // !stack2.empty()
            e = stack2.top();
            stack2.pop();
            return e;
        }
 
    }
 
private:
    stack<int> stack1;
    stack<int> stack2;
};
~~~

### 20180704 
#### 重建二叉树 

题目描述：
输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。
~~~
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* reConstructBinaryTree(vector<int> pre,vector<int> vin) {
        int length = vin.size();
        if(length==0){
            return NULL;
        }
        vector<int> leftPreorder, rightPreorder, leftInorder, rightInorder;
        TreeNode* root = new TreeNode(pre[0]);
        int rootPosition = 0;
        while(rootPosition < length-1 && vin[rootPosition]!= pre[0]){
            rootPosition ++;
        }
        while(rootPosition == length-1 && vin[rootPosition]!= pre[0]){
            throw std::exception();//?
        }
        for(int i = 0; i < rootPosition; i++){
            leftPreorder.push_back(pre[i+1]);
            leftInorder.push_back(vin[i]);
        }
        for(int j = rootPosition+1; j <= length-1; j++ ){
            rightPreorder.push_back(pre[j]);
            rightInorder.push_back(vin[j]);
        }
        root -> left = reConstructBinaryTree(leftPreorder,leftInorder);
        root -> right = reConstructBinaryTree(rightPreorder,rightInorder);
        return root;
         
 
    }
};
~~~