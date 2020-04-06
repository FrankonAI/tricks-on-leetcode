# tricks-on-leetcode
## 1. 动态规划(Dynamic Programming)
### 72题(困难) 编辑距离
\[ 来源：力扣（LeetCode）https://leetcode-cn.com/problems/edit-distance \]  
**问题描述**  
给你两个单词 word1 和 word2，请你计算出将 word1 转换成 word2 所使用的最少操作数。  
你可以对一个单词进行如下三种操作：  
1.插入一个字符；  
2.删除一个字符；  
3.替换一个字符。  
示例1：
```
输入：word1 = "horse", word2 = "ros"
输出：3
解释：
horse -> rorse (将 'h' 替换为 'r')
rorse -> rose (删除 'r')
rose -> ros (删除 'e')
```
示例2：
```
输入：word1 = "intention", word2 = "execution"
输出：5
解释：
intention -> inention (删除 't')
inention -> enention (将 'i' 替换为 'e')
enention -> exention (将 'n' 替换为 'x')
exention -> exection (将 'n' 替换为 'c')
exection -> execution (插入 'u')
```
**分析**
1. 将字符串A和字符串B进行上述三种操作，共有6种操作，在要求获得相同字符串的条件下，以下操作是等价的：
    - 字符串A插入一个字符和字符串B删除一个字符，如A="dog"，B="doge"，A+="e"和B.replace('e','')是等价的；
    - 字符串A删除一个字符和字符串B插入一个字符（同上）；
    - 字符串A替换一个字符和字符串B替换一个字符，如A="doga"，B="doge"，A.replace('a','e')和B.replace('e','a')是等价的；  
    <p style="text-indent:2em"><b>因此，实际上本质不同的操作只有三个：(1)字符串A插入一个字符；(2)字符串B插入一个字符；(3)字符串A替换一个字符。</b></p>
2. 分析1中为我们减小问题规模提供了前提，即指示我们在“将word1转换成word2”过程中还差最后一步时可以进行哪些操作，以A='horse'和B='ros'为例，我们可以得到如下结论：
    - 如果'horse'和'ro'的距离为a，则'horse'和'ros'的距离不会超过a+1，因为经过a步后可以将A='horse'转化为'ro'，再对A进行一次插入操作则转化成功；
    - 如果'hors'和'ros'的距离为b，则'horse'和'ros'的距离不会超过b+1，因为经过b步后可以将B='ros'转化为'hors'，再对B进行一次插入操作则转化成功；
    - 如果'hors'和'ro'的距离为c，则'horse'和'ros'的距离不会超过c+1，因为经过c步后可以将A='hors'转化为'ro'，而此时将问题变为原规模后，A+'e'='roe'、B+'s'='ros'，再对A进行一次替换操作则转化成功（特别地，当问题上升为原规模时A和B增加的字符相同，则不用进行替换操作）。
    <p style="text-indent:2em"><b>以上分析包括了所有可行的操作以及所有缩小问题规模的方式（即将A缩小一个单位、将B缩小一个单位和将A、B均缩小一个单位）。并且以上分析表明，'horse'到'ros'的编辑距离应该为min(a+1, b+1, c+1)。</b></p>
3. 按照分析2的思路，我们可以将原问题拆分至最终的子问题：
    - 当字符串A=''时，到'ros'的编辑距离明显为len('ros')；
    - 当字符串B=''时，到'horse'的编辑距离明显为len('horse')。
    
**代码**
``` python
python

def minDistance(word1, word2):
    
```
