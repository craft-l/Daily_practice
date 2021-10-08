#### [1436. 旅行终点站](https://leetcode-cn.com/problems/destination-city/)

给你一份旅游线路图，该线路图中的旅行线路用数组 `paths` 表示，其中 `paths[i] = [cityAi, cityBi]` 表示该线路将会从 `cityAi` 直接前往 `cityBi` 。请你找出这次旅行的终点站，即没有任何可以通往其他城市的线路的城市*。*

题目数据保证线路图会形成一条不存在循环的线路，因此恰有一个旅行终点站。

 

**示例 1：**

```
输入：paths = [["London","New York"],["New York","Lima"],["Lima","Sao Paulo"]]
输出："Sao Paulo" 
解释：从 "London" 出发，最后抵达终点站 "Sao Paulo" 。本次旅行的路线是 "London" -> "New York" -> "Lima" -> "Sao Paulo" 。
```

**示例 2：**

```
输入：paths = [["B","C"],["D","B"],["C","A"]]
输出："A"
解释：所有可能的线路是：
"D" -> "B" -> "C" -> "A". 
"B" -> "C" -> "A". 
"C" -> "A". 
"A". 
显然，旅行终点站是 "A" 。
```

**示例 3：**

```
输入：paths = [["A","Z"]]
输出："Z"
```

 

**提示：**

- `1 <= paths.length <= 100`
- `paths[i].length == 2`
- `1 <= cityAi.length, cityBi.length <= 10`
- `cityAi != cityBi`
- 所有字符串均由大小写英文字母和空格字符组成。



### 思路分析：

题目说了只有一个旅行终点站，所以终点站只会出现在cityB中，那么只要找到只在cityB中出现的城市就好了。

```c++
class Solution {
public:
    string destCity(vector<vector<string>>& paths) {//相当于二维的动态数组
        unordered_map<string> road;
		for(auto &path : paths)//auto为自动识别变量，简化代码；因为要修改值，所以&
        {
            road.insert(path[0]);
		}
        for(auto &path : paths)
        {
            if(!road.count(path[1]))
            {
                return path[1];
            }
        }
    }
};
```





#### [405. 数字转换为十六进制数](https://leetcode-cn.com/problems/convert-a-number-to-hexadecimal/)

给定一个整数，编写一个算法将这个数转换为十六进制数。对于负整数，我们通常使用 [补码运算](https://baike.baidu.com/item/补码/6854613?fr=aladdin) 方法。

**注意:**

1. 十六进制中所有字母(`a-f`)都必须是小写。
2. 十六进制字符串中不能包含多余的前导零。如果要转化的数为0，那么以单个字符`'0'`来表示；对于其他情况，十六进制字符串中的第一个字符将不会是0字符。 
3. 给定的数确保在32位有符号整数范围内。
4. **不能使用任何由库提供的将数字直接转换或格式化为十六进制的方法。**

**示例 1：**

```
输入:
26

输出:
"1a"
```

**示例 2：**

```
输入:
-1

输出:
"ffffffff"
```



如果输入的数是正数：
直接通过迭代%16, /16的方法解决。

如果输入的数是负数：
当输入数是负数时, 其补码的数字范围就是0到UINT_MAX(2^31-1)。
我们需要找一种方法将其转为正数, 且不影响补码间的计算。
这样也可以直接复用正数的迭代方法进行计算。

一种可行的方法是:


N = N + 2^32 (2^32的16进制表示为 0x100000000)。
用代码表示是:

if (N < 0) N = N + 0x100000000;



```c++
class Solution {
public:
    string toHex(int num) {
        string res;
        long N = num;     // 预处理: 将精度提升到int64, 防止大整数溢出
        if (N == 0) return "0";
        unordered_map<int, char> dict;
        dict = {
                {0, '0'},
                {1, '1'},
                {2, '2'},
                {3, '3'},
                {4, '4'},
                {5, '5'},
                {6, '6'},
                {7, '7'},
                {8, '8'},
                {9, '9'},
                {10, 'a'},
                {11, 'b'},
                {12, 'c'},
                {13, 'd'},
                {14, 'e'},
                {15, 'f'}
            };
        if (N < 0) N = N + 0x100000000; /* 负数的补码: 其数字范围就是0到UINT_MAX(2^31-1), 即为16^8-1。这里+ 0x100000000是为了将任意一个负数转换到正数范围内(且不影响计算结果), 理论上±2^32均可, 但我们后面的迭代需要是正数, 于是选择+0x100000000。 */
        while (N > 0)
        {
            long lastDigit = N % 16;
            N /= 16;
            res = dict[lastDigit] + res;
        }
        return res;
    }
};

//用1个字符串模拟一个"哈希表"\
class Solution {
public:
    string toHex(int num) {
        string res;
        long N = num; 
        if (N == 0) return "0";
        string dict = "0123456789abcdef";
        if (N < 0) N = N + 0x100000000; 
        while (N > 0)
        {
            long lastDigit = N % 16;
            N /= 16;
            res = dict[lastDigit] + res;
        }
        return res;
    }
};



/*其他优秀解法：
【笔记】核心思想，使用位运算，每4位，对应1位16进制数字。
使用0xf(00...01111b)获取num的低4位。
>>算数位移，其中正数右移左边补0，负数右移左边补1。
位移运算并不能保证num==0，需要使用32位int保证（对应16进制小于等于8位）。
使用string直接进行字符串拼接....
*/
string toHex(int num) {
    if (num == 0) return "0";
    string hex = "0123456789abcdef", ans = "";
    while(num && ans.size() < 8){
        ans = hex[num & 0xf] + ans;
        num >>=  4; 
    }
    return ans;
}
```



#### [166. 分数到小数](https://leetcode-cn.com/problems/fraction-to-recurring-decimal/)

给定两个整数，分别表示分数的分子 `numerator` 和分母 `denominator`，以 **字符串形式返回小数** 。

如果小数部分为循环小数，则将循环的部分括在括号内。

如果存在多个答案，只需返回 **任意一个** 。

对于所有给定的输入，**保证** 答案字符串的长度小于 `104` 。

 

**示例 1：**

```
输入：numerator = 1, denominator = 2
输出："0.5"
```

**示例 2：**

```
输入：numerator = 2, denominator = 1
输出："2"
```

**示例 3：**

```
输入：numerator = 2, denominator = 3
输出："0.(6)"
```

**示例 4：**

```
输入：numerator = 4, denominator = 333
输出："0.(012)"
```

**示例 5：**

```
输入：numerator = 1, denominator = 5
输出："0.2"
```

 

**提示：**

- `-231 <= numerator, denominator <= 231 - 1`
- `denominator != 0`

```c++
 string fractionToDecimal(int numerator, int denominator) {
        // 转 long 计算，防止溢出
        long a = numerator, b = denominator;

        // 如果本身能够整除，直接返回计算结果
        if (a % b == 0) return to_string(a / b);

        string ans;
        // 如果其一为负数，先追加负号
        if (a * b < 0) ans.push_back('-');
        a = abs(a); b = abs(b);

        // 计算小数点前的部分，并将余数赋值给 a
        ans += to_string(a / b) + ".";
        a %= b;

        unordered_map<long, int> map;
        while (a != 0) {
            // 记录当前余数所在答案的位置，并继续模拟除法运算
            map[a] =  ans.size();
            a *= 10;
            ans += to_string(a / b);
            a %= b;
            // 如果当前余数之前出现过，则将 [出现位置 到 当前位置] 的部分抠出来（循环小数部分）
            if (map.find(a) != map.end()) {
                int u = map[a];
                string ret = ans.substr(0,u) + "(" + ans.substr(u, ans.size()-u+1) + ")";
                return ret;
            }
        }
        return ans;
    }


//特判整除的情况，哈希表记录每次除后分子对应的下标，用于寻找循环节

//本质就是竖式除法，每次后补0继续除，直到循环或者除到0
 string fractionToDecimal(int numerator, int denominator) {
        if((int64_t)numerator % denominator == 0) return to_string((int64_t)numerator / denominator);

        int64_t up = abs((int64_t)numerator), down = abs((int64_t)denominator);
        string ans(((numerator < 0) ^ (denominator < 0) ? "-" : "") + to_string(up / down) + '.');
        unordered_map<int64_t, int> index;

        for(int i = ans.size(); up = up % down * 10; ++i){
            if(index.count(up)) {
                ans.insert(begin(ans) + index[up], '(');
                ans.push_back(')');
                break;
            }
            index[up] = i;
            ans.push_back('0' + up / down);
        }
        return ans;
    }
```



#### [187. 重复的DNA序列](https://leetcode-cn.com/problems/repeated-dna-sequences/)

所有 DNA 都由一系列缩写为 `'A'`，`'C'`，`'G'` 和 `'T'` 的核苷酸组成，例如：`"ACGAATTCCG"`。在研究 DNA 时，识别 DNA 中的重复序列有时会对研究非常有帮助。

编写一个函数来找出所有目标子串，目标子串的长度为 10，且在 DNA 字符串 `s` 中出现次数超过一次。

 

**示例 1：**

```
输入：s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"
输出：["AAAAACCCCC","CCCCCAAAAA"]
```

**示例 2：**

```
输入：s = "AAAAAAAAAAAAA"
输出：["AAAAAAAAAA"]
```

 

**提示：**

- `0 <= s.length <= 105`
- `s[i]` 为 `'A'`、`'C'`、`'G'` 或 `'T'`



