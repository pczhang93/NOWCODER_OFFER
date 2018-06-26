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