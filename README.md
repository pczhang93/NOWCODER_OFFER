# NOWCODER_OFFER

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
书上C++版：
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