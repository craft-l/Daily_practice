[TOC]



#### 1976.到达目的地的方案数（Dijkstra算法

你在一个城市里，城市由 n 个路口组成，路口编号为 0 到 n - 1 ，某些路口之间有 双向 道路。输入保证你可以从任意路口出发到达其他任意路口，且任意两个路口之间最多有一条路。

给你一个整数 n 和二维整数数组 roads ，其中 roads[i] = [ui, vi, timei] 表示在路口 ui 和 vi 之间有一条需要花费 timei 时间才能通过的道路。你想知道花费 最少时间 从路口 0 出发到达路口 n - 1 的方案数。

请返回花费 最少时间 到达目的地的路径数目 。由于答案可能很大，将结果对 109 + 7 取余 后返回。

示例 1：

![img](https://assets.leetcode.com/uploads/2021/07/17/graph2.png)

输入：n = 7, roads = [[0,6,7],[0,1,2],[1,2,3],[1,3,3],[6,3,3],[3,5,1],[6,5,1],[2,5,1],[0,4,5],[4,6,2]]
输出：4
解释：从路口 0 出发到路口 6 花费的最少时间是 7 分钟。
四条花费 7 分钟的路径分别为：

- 0 ➝ 6
- 0 ➝ 4 ➝ 6
- 0 ➝ 1 ➝ 2 ➝ 5 ➝ 6
- 0 ➝ 1 ➝ 3 ➝ 5 ➝ 6
  示例 2：

输入：n = 2, roads = [[1,0,10]]
输出：1
解释：只有一条从路口 0 到路口 1 的路，花费 10 分钟。


提示：

1 <= n <= 200
n - 1 <= roads.length <= n * (n - 1) / 2
roads[i].length == 3
0 <= ui, vi <= n - 1
1 <= timei <= 109
ui != vi
任意两个路口之间至多有一条路。
从任意路口出发，你能够到达其他任意路口。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/number-of-ways-to-arrive-at-destination



解法：这道题就是最短路径算法了

以下









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

**思路分析：**

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



```c++
class Solution {
public:
    vector<string> findRepeatedDnaSequences(string s) {
 //对应二进制00, 01, 10, 11.那么10个组合只要20位就够了。
        unordered_map<char, int> m{{'A', 0}, {'C', 1}, {'G', 2}, {'T', 3}};
        vector<string> res;
        bitset<1 << 20> s1, s2; //那么所有组合的值将在0到(1 << 20 - 1)之间
        int val = 0, mask = (1 << 20) - 1; //mask等于二进制的20个1
        //类似与滑动窗口先把前10个字母组合
        for (int i = 0; i < 10; ++i) val = (val << 2) | m[s[i]];
        s1.set(val); //置位
        for (int i = 10; i < s.size(); ++i) {
            val = ((val << 2) & mask) | m[s[i]]; //去掉左移的一个字符再加上一个新字符
            if (s2.test(val)) continue; //出现过两次跳过
            if (s1.test(val)) {
                res.push_back(s.substr(i - 9, 10));
                s2.set(val);
            }
            else s1.set(val);
        }
        return res;
    }
};

```





#### [352. 将数据流变为多个不相交区间](https://leetcode-cn.com/problems/data-stream-as-disjoint-intervals/)

 给你一个由非负整数 `a1, a2, ..., an` 组成的数据流输入，请你将到目前为止看到的数字总结为不相交的区间列表。

实现 `SummaryRanges` 类：

- `SummaryRanges()` 使用一个空数据流初始化对象。
- `void addNum(int val)` 向数据流中加入整数 `val` 。
- `int[][] getIntervals()` 以不相交区间 `[starti, endi]` 的列表形式返回对数据流中整数的总结。

 

**示例：**

```
输入：
["SummaryRanges", "addNum", "getIntervals", "addNum", "getIntervals", "addNum", "getIntervals", "addNum", "getIntervals", "addNum", "getIntervals"]
[[], [1], [], [3], [], [7], [], [2], [], [6], []]
输出：
[null, null, [[1, 1]], null, [[1, 1], [3, 3]], null, [[1, 1], [3, 3], [7, 7]], null, [[1, 3], [7, 7]], null, [[1, 3], [6, 7]]]

解释：
SummaryRanges summaryRanges = new SummaryRanges();
summaryRanges.addNum(1);      // arr = [1]
summaryRanges.getIntervals(); // 返回 [[1, 1]]
summaryRanges.addNum(3);      // arr = [1, 3]
summaryRanges.getIntervals(); // 返回 [[1, 1], [3, 3]]
summaryRanges.addNum(7);      // arr = [1, 3, 7]
summaryRanges.getIntervals(); // 返回 [[1, 1], [3, 3], [7, 7]]
summaryRanges.addNum(2);      // arr = [1, 2, 3, 7]
summaryRanges.getIntervals(); // 返回 [[1, 3], [7, 7]]
summaryRanges.addNum(6);      // arr = [1, 2, 3, 6, 7]
summaryRanges.getIntervals(); // 返回 [[1, 3], [6, 7]]
```

 

**提示：**

- `0 <= val <= 104`
- 最多调用 `addNum` 和 `getIntervals` 方法 `3 * 104` 次

 

**进阶：**如果存在大量合并，并且与数据流的大小相比，不相交区间的数量很小，该怎么办?



```c++
class SummaryRanges {
private:
    map<int, int> intervals;

public:
    SummaryRanges() {}
    
    void addNum(int val) {
        // 找到 l1 最小的且满足 l1 > val 的区间 interval1 = [l1, r1]
        // 如果不存在这样的区间，interval1 为尾迭代器
        auto interval1 = intervals.upper_bound(val);
        // 找到 l0 最大的且满足 l0 <= val 的区间 interval0 = [l0, r0]
        // 在有序集合中，interval0 就是 interval1 的前一个区间
        // 如果不存在这样的区间，interval0 为尾迭代器
        auto interval0 = (interval1 == intervals.begin() ? intervals.end() : prev(interval1));

        if (interval0 != intervals.end() && interval0->first <= val && val <= interval0->second) {
            // 情况一
            return;
        }
        else {
            bool left_aside = (interval0 != intervals.end() && interval0->second + 1 == val);
            bool right_aside = (interval1 != intervals.end() && interval1->first - 1 == val);
            if (left_aside && right_aside) {
                // 情况四
                int left = interval0->first, right = interval1->second;
                intervals.erase(interval0);
                intervals.erase(interval1);
                intervals.emplace(left, right);
            }
            else if (left_aside) {
                // 情况二
                ++interval0->second;
            }
            else if (right_aside) {
                // 情况三
                int right = interval1->second;
                intervals.erase(interval1);
                intervals.emplace(val, right);
            }
            else {
                // 情况五
                intervals.emplace(val, val);
            }
        }
    }
    
    vector<vector<int>> getIntervals() {
        vector<vector<int>> ans;
        for (const auto& [left, right]: intervals) {
            ans.push_back({left, right});
        }
        return ans;
    }
};

/**
 * Your SummaryRanges object will be instantiated and called as such:
 * SummaryRanges* obj = new SummaryRanges();
 * obj->addNum(val);
 * vector<vector<int>> param_2 = obj->getIntervals();
 */
```





#### [441. 排列硬币](https://leetcode-cn.com/problems/arranging-coins/)

你总共有 `n` 枚硬币，并计划将它们按阶梯状排列。对于一个由 `k` 行组成的阶梯，其第 `i` 行必须正好有 `i` 枚硬币。阶梯的最后一行 **可能** 是不完整的。

给你一个数字 `n` ，计算并返回可形成 **完整阶梯行** 的总行数

**思路**

看到的时候直接想到累加

```c++
    int arrangeCoins(int n) {
        long int i = 0;
        long int sum = 0;
        if(n == 0) return 0;
        while(sum <= n)
        {
            sum += ++i;
        }
        return --i;
    }
```

但是上面的方法效率太低了，接下来用数学方法以及二分查找

```c++
/*数学
等差数列，第k行放满一共需要k*(k+1)/2
令其等于n，得k^2 + k - 2n = 0，可求出 k
因为需要得到完整行数，所以我们向下取整
*/
int arrangeCoins(int n) {
        return (int) ((sqrt((long long) 8 * n + 1) - 1) / 2);
    }


/*二分查找
第 i 行必须有 i 个硬币（最后一行除外），所以，到第 i 行时总共使用的硬币数量为 total=i(i+1)/2，现在我们的目标是寻找这么一个 i 使用得 total 小于或等于 n，而且这个 i 的范围我们知道它在 1 到 n 之间。
所以，我们可以使用二分查找来解决本题。
*/
 public int arrangeCoins(int n) {
        // 1,2,3,4,5
        // 到第 k 行时的总硬币数等于 k(k+1)/2
        // 只要找到最接近 n 的那个 k 就可以了
        // 所以，我们可以使用二分查找
        long left = 1, right = n;
        while (left <= right) {
            long mid = left + (right - left) / 2;
            long total = mid * (mid + 1) / 2;
            if (total == n) {
                return (int) mid;
            }
            if (total > n) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return (int) right;
    }
```

#### [273. 整数转换英文表示](https://leetcode-cn.com/problems/integer-to-english-words/)

将非负整数 `num` 转换为其对应的英文表示。

**示例 1：**

```
输入：num = 123
输出："One Hundred Twenty Three"
```

**示例 2：**

```
输入：num = 12345
输出："Twelve Thousand Three Hundred Forty Five"
```

**示例 3：**

```
输入：num = 1234567
输出："One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"
```

**示例 4：**

```
输入：num = 1234567891
输出："One Billion Two Hundred Thirty Four Million Five Hundred Sixty Seven Thousand Eight Hundred Ninety One"
```

 

**提示：**

- `0 <= num <= 231 - 1`



**补充**：注意string 和stringbuilder的区别，这里可以用stringbuilder

```c++
class Solution {
public:
vector<string> singles = {"", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine"};
    vector<string> teens = {"Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"};
    vector<string> tens = {"", "Ten", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"};
    vector<string> thousands = {"", "Thousand", "Million", "Billion"};

    string numberToWords(int num) {
        if (num == 0) {
            return "Zero";
        }
        string sb;
        for (int i = 3, unit = 1000000000; i >= 0; i--, unit /= 1000) {
            int curNum = num / unit;
            if (curNum != 0) {
                num -= curNum * unit;
                string curr;
                recursion(curr, curNum);
                curr = curr + thousands[i] + " ";
                sb = sb + curr;
            }
        }
        while (sb.back() == ' ') {
            sb.pop_back();
        }
        return sb;
    }
    void recursion(string & curr, int num) {
        if (num == 0) {
            return;
        } else if (num < 10) {
            curr = curr + singles[num] + " ";
        } else if (num < 20) {
            curr = curr + teens[num - 10] + " ";
        } else if (num < 100) {
            curr = curr + tens[num / 10] + " ";
            recursion(curr, num % 10);
        } else {
            curr = curr + singles[num / 100] + " Hundred ";
            recursion(curr, num % 100);
        }
    }

    
};
```

#### [38. 外观数列](https://leetcode-cn.com/problems/count-and-say/)

给定一个正整数 `n` ，输出外观数列的第 `n` 项。

「外观数列」是一个整数序列，从数字 1 开始，序列中的每一项都是对前一项的描述。

你可以将其视作是由递归公式定义的数字字符串序列：

- `countAndSay(1) = "1"`
- `countAndSay(n)` 是对 `countAndSay(n-1)` 的描述，然后转换成另一个数字字符串。

前五项如下：

```
1.     1
2.     11
3.     21
4.     1211
5.     111221
第一项是数字 1 
描述前一项，这个数是 1 即 “ 一 个 1 ”，记作 "11"
描述前一项，这个数是 11 即 “ 二 个 1 ” ，记作 "21"
描述前一项，这个数是 21 即 “ 一 个 2 + 一 个 1 ” ，记作 "1211"
描述前一项，这个数是 1211 即 “ 一 个 1 + 一 个 2 + 二 个 1 ” ，记作 "111221"
```

要 **描述** 一个数字字符串，首先要将字符串分割为 **最小** 数量的组，每个组都由连续的最多 **相同字符** 组成。然后对于每个组，先描述字符的数量，然后描述字符，形成一个描述组。要将描述转换为数字字符串，先将每组中的字符数量用数字替换，再将所有描述组连接起来。

例如，数字字符串 `"3322251"` 的描述如下图：

![img](https://pic.leetcode-cn.com/1629874763-TGmKUh-image.png)



 

**示例 1：**

```
输入：n = 1
输出："1"
解释：这是一个基本样例。
```

**示例 2：**

```
输入：n = 4
输出："1211"
解释：
countAndSay(1) = "1"
countAndSay(2) = 读 "1" = 一 个 1 = "11"
countAndSay(3) = 读 "11" = 二 个 1 = "21"
countAndSay(4) = 读 "21" = 一 个 2 + 一 个 1 = "12" + "11" = "1211"
```

 

**提示：**

- `1 <= n <= 30`

```c++
//1<=n<=30,可直接列出全部情况

//递归

//迭代计算
 string countAndSay(int n) {
// 迭代计算结果 初始化为1
        string ans = "1";

        // 只需要计算n-1次；如果n为1，可以直接返回ans
        for (int t = 1; t < n; t++) {
            char tmp = ans[0];
            int cnt = 0;
            // 新的字符串用来记录新的外观数列
            string new_ans = "";
            for (int i = 0; i < ans.size(); i++) {
                // 和前面的数字相同 计数器+1
                if (ans[i] == tmp) cnt++;
                else {
                    // 不同的时候，我们就应该把之前的计数和对应的数字拼接起来了
                    // count + number_string
                    new_ans += to_string(cnt) + tmp;
                    // 将新的数字和出现次数1记录 继续进行相同的迭代操作
                    tmp = ans[i];
                    cnt = 1;
                }
            }
            // 迭代完成时；tmp里还存有最后一组不同的数字；不要遗漏
            new_ans += to_string(cnt) + tmp;
            
            ans = new_ans;
        }

        return ans;
    }
```



#### [282. 给表达式添加运算符](https://leetcode-cn.com/problems/expression-add-operators/)

给定一个仅包含数字 `0-9` 的字符串 `num` 和一个目标值整数 `target` ，在 `num` 的数字之间添加 **二元** 运算符（不是一元）`+`、`-` 或 `*` ，返回所有能够得到目标值的表达式。

 

**示例 1:**

```
输入: num = "123", target = 6
输出: ["1+2+3", "1*2*3"] 
```

**示例 2:**

```
输入: num = "232", target = 8
输出: ["2*3+2", "2+3*2"]
```

**示例 3:**

```
输入: num = "105", target = 5
输出: ["1*0+5","10-5"]
```

**示例 4:**

```
输入: num = "00", target = 0
输出: ["0+0", "0-0", "0*0"]
```

**示例 5:**

```
输入: num = "3456237490", target = 9191
输出: []
```

 

**提示：**

- `1 <= num.length <= 10`
- `num` 仅含数字
- `-231 <= target <= 231 - 1`

#### [29. 两数相除](https://leetcode-cn.com/problems/divide-two-integers/)

给定两个整数，被除数 `dividend` 和除数 `divisor`。将两数相除，要求不使用乘法、除法和 mod 运算符。

返回被除数 `dividend` 除以除数 `divisor` 得到的商。

整数除法的结果应当截去（`truncate`）其小数部分，例如：`truncate(8.345) = 8` 以及 `truncate(-2.7335) = -2`

 

**示例 1:**

```
输入: dividend = 10, divisor = 3
输出: 3
解释: 10/3 = truncate(3.33333..) = truncate(3) = 3
```

**示例 2:**

```
输入: dividend = 7, divisor = -3
输出: -2
解释: 7/-3 = truncate(-2.33333..) = -2
```

 

**提示：**

- 被除数和除数均为 32 位有符号整数。
- 除数不为 0。
- 假设我们的环境只能存储 32 位有符号整数，其数值范围是 [−231, 231 − 1]。本题中，如果除法结果溢出，则返回 231 − 1。

```c++
 int divide(int dividend, int divisor) {
        if(dividend == 0) return 0;
        if(divisor == 1) return dividend;
        if(divisor == -1){
            if(dividend>INT_MIN) return -dividend;// 只要不是最小的那个整数，都是直接返回相反数就好啦
            return INT_MAX;// 是最小的那个，那就返回最大的整数啦
        }
        long a = dividend;
        long b = divisor;
        int sign = 1; 
        if((a>0&&b<0) || (a<0&&b>0)){
            sign = -1;
        }
        a = a>0?a:-a;
        b = b>0?b:-b;
        long res = div(a,b);
        if(sign>0)return res>INT_MAX?INT_MAX:res;
        return -res;
    }
    int div(long a, long b){  // 似乎精髓和难点就在于下面这几句
        if(a<b) return 0;
        long count = 1;
        long tb = b; // 在后面的代码中不更新b
        while((tb+tb)<=a){
            count = count + count; // 最小解翻倍
            tb = tb+tb; // 当前测试的值也翻倍
        }
        return count + div(a-tb,b);
    }

//最近正在学分治，可以考虑一下二分法


```





#### [412. Fizz Buzz](https://leetcode-cn.com/problems/fizz-buzz/)

难度简单150

给你一个整数 `n` ，找出从 `1` 到 `n` 各个整数的 Fizz Buzz 表示，并用字符串数组 `answer`（**下标从 1 开始**）返回结果，其中：

- `answer[i] == "FizzBuzz"` 如果 `i` 同时是 `3` 和 `5` 的倍数。
- `answer[i] == "Fizz"` 如果 `i` 是 `3` 的倍数。
- `answer[i] == "Buzz"` 如果 `i` 是 `5` 的倍数。
- `answer[i] == i` 如果上述条件全不满足。

 

**示例 1：**

```
输入：n = 3
输出：["1","2","Fizz"]
```

**示例 2：**

```
输入：n = 5
输出：["1","2","Fizz","4","Buzz"]
```

**示例 3：**

```
输入：n = 15
输出：["1","2","Fizz","4","Buzz","Fizz","7","8","Fizz","Buzz","11","Fizz","13","14","FizzBuzz"]
```

 

**提示：**

- `1 <= n <= 104`

```c++
class Solution {
public:
    vector<string> fizzBuzz(int n) {
vector<string> answer;
        for (int i = 1; i <= n; i++) {
            string curr;
            if (i % 3 == 0) {
                curr　+= "Fizz";
            }
            if (i % 5 == 0) {
                curr += "Buzz";
            }
            if (curr.size() == 0) {
                curr += to_string(i);
            }            
            answer.emplace_back(curr);
        }
        return answer;
    }
};
```

#### [剑指 Offer II 069. 山峰数组的顶部](https://leetcode-cn.com/problems/B1IidL/)

符合下列属性的数组 `arr` 称为 **山峰数组**（**山脉数组）** ：

- `arr.length >= 3`

- 存在

   

  ```
  i
  ```

  （

  ```
  0 < i < arr.length - 1
  ```

  ）使得：

  - `arr[0] < arr[1] < ... arr[i-1] < arr[i]`
  - `arr[i] > arr[i+1] > ... > arr[arr.length - 1]`

给定由整数组成的山峰数组 `arr` ，返回任何满足 `arr[0] < arr[1] < ... arr[i - 1] < arr[i] > arr[i + 1] > ... > arr[arr.length - 1]` 的下标 `i` ，即山峰顶部。

 

**示例 1：**

```
输入：arr = [0,1,0]
输出：1
```

**示例 2：**

```
输入：arr = [1,3,5,4,2]
输出：2
```

**示例 3：**

```
输入：arr = [0,10,5,2]
输出：1
```

**示例 4：**

```
输入：arr = [3,4,5,1]
输出：2
```

**示例 5：**

```
输入：arr = [24,69,100,99,79,78,67,36,26,19]
输出：2
```

 

**提示：**

- `3 <= arr.length <= 104`
- `0 <= arr[i] <= 106`
- 题目数据保证 `arr` 是一个山脉数组

 

**进阶：**很容易想到时间复杂度 `O(n)` 的解决方案，你可以设计一个 `O(log(n))` 的解决方案吗？

```c++
 int peakIndexInMountainArray(vector<int>& arr) {
        int r = arr.size()-1, l = 0;
        while(r > l){
            int mid = (r+l)/2;
            if(arr[mid] > arr[mid-1] && arr[mid] > arr[mid+1]) return mid;
            else if(arr[mid] > arr[mid-1]) l = mid;
            else r = mid;
        }
        return -1;

    }

```





#### [282. 给表达式添加运算符](https://leetcode-cn.com/problems/expression-add-operators/)

给定一个仅包含数字 `0-9` 的字符串 `num` 和一个目标值整数 `target` ，在 `num` 的数字之间添加 **二元** 运算符（不是一元）`+`、`-` 或 `*` ，返回所有能够得到目标值的表达式。

 

**示例 1:**

```
输入: num = "123", target = 6
输出: ["1+2+3", "1*2*3"] 
```

**示例 2:**

```
输入: num = "232", target = 8
输出: ["2*3+2", "2+3*2"]
```

**示例 3:**

```
输入: num = "105", target = 5
输出: ["1*0+5","10-5"]
```

**示例 4:**

```
输入: num = "00", target = 0
输出: ["0+0", "0-0", "0*0"]
```

**示例 5:**

```
输入: num = "3456237490", target = 9191
输出: []
```

 

**提示：**

- `1 <= num.length <= 10`
- `num` 仅含数字
- `-231 <= target <= 231 - 1`

#### [230. 二叉搜索树中第K小的元素](https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/)

难度中等505

给定一个二叉搜索树的根节点 `root` ，和一个整数 `k` ，请你设计一个算法查找其中第 `k` 个最小元素（从 1 开始计数）。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/28/kthtree1.jpg)

```
输入：root = [3,1,4,null,2], k = 1
输出：1
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/01/28/kthtree2.jpg)

```
输入：root = [5,3,6,2,4,null,null,1], k = 3
输出：3
```

 

 

**提示：**

- 树中的节点数为 `n` 。
- `1 <= k <= n <= 104`
- `0 <= Node.val <= 104`

 

**进阶：**如果二叉搜索树经常被修改（插入/删除操作）并且你需要频繁地查找第 `k` 小的值，你将如何优化算法？



```c++
    int kthSmallest(TreeNode* root, int k) {
stack<TreeNode *> stack;
        while (root != nullptr || stack.size() > 0) {
            while (root != nullptr) {
                stack.push(root);
                root = root->left;
            }
            root = stack.top();
            stack.pop();
            --k;
            if (k == 0) {
                break;
            }
            root = root->right;
        }
        return root->val;

    }
```

#### [476. 数字的补数](https://leetcode-cn.com/problems/number-complement/)

对整数的二进制表示取反（`0` 变 `1` ，`1` 变 `0`）后，再转换为十进制表示，可以得到这个整数的补数。

- 例如，整数 `5` 的二进制表示是 `"101"` ，取反后得到 `"010"` ，再转回十进制表示得到补数 `2` 。

给你一个整数 `num` ，输出它的补数。

 



**示例 1：**

```
输入：num = 5
输出：2
解释：5 的二进制表示为 101（没有前导零位），其补数为 010。所以你需要输出 2 。
```

**示例 2：**

```
输入：num = 1
输出：0
解释：1 的二进制表示为 1（没有前导零位），其补数为 0。所以你需要输出 0 。
```

 

**提示：**

- `1 <= num < 231`

```c++
    int findComplement(int num) {
 int temp = num, c = 0;
        while(temp > 0){
            temp >>= 1;
            c =  (c << 1) + 1;
        }
        return num ^ c;
    }
```

#### [211. 添加与搜索单词 - 数据结构设计](https://leetcode-cn.com/problems/design-add-and-search-words-data-structure/)

请你设计一个数据结构，支持 添加新单词 和 查找字符串是否与任何先前添加的字符串匹配 。

实现词典类 `WordDictionary` ：

- `WordDictionary()` 初始化词典对象
- `void addWord(word)` 将 `word` 添加到数据结构中，之后可以对它进行匹配
- `bool search(word)` 如果数据结构中存在字符串与 `word` 匹配，则返回 `true` ；否则，返回 `false` 。`word` 中可能包含一些 `'.'` ，每个 `.` 都可以表示任何一个字母。

 

**示例：**

```
输入：
["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
[[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
输出：
[null,null,null,null,false,true,true,true]

解释：
WordDictionary wordDictionary = new WordDictionary();
wordDictionary.addWord("bad");
wordDictionary.addWord("dad");
wordDictionary.addWord("mad");
wordDictionary.search("pad"); // return False
wordDictionary.search("bad"); // return True
wordDictionary.search(".ad"); // return True
wordDictionary.search("b.."); // return True
```

 

**提示：**

- `1 <= word.length <= 500`
- `addWord` 中的 `word` 由小写英文字母组成
- `search` 中的 `word` 由 '.' 或小写英文字母组成
- 最多调用 `50000` 次 `addWord` 和 `search`

```c++
struct TrieNode{
    vector<TrieNode *> child;
    bool isEnd;
    TrieNode() {
        this->child = vector<TrieNode *>(26,nullptr);
        this->isEnd = false;
    }
};

void insert(TrieNode * root, const string & word) {
    TrieNode * node = root;
    for (auto c : word) {
        if (node->child[c - 'a'] == nullptr) {
            node->child[c - 'a'] = new TrieNode();
        }
        node = node->child[c - 'a'];
    }
    node->isEnd = true;
}

class WordDictionary {
public:
    WordDictionary() {
        trie = new TrieNode();
    }
    
    void addWord(string word) {
        insert(trie,word);
    }
    
    bool search(string word) {
        return dfs(word, 0, trie);
    }

    bool dfs(const string & word,int index,TrieNode * node) {
　　　　if (index == word.size()) {
            return node->isEnd;    
        }
        char ch = word[index];
        if (ch >= 'a' && ch <= 'z') {
            TrieNode * child = node->child[ch - 'a'];
            if (child != nullptr && dfs(word, index + 1, child)) {
                return true;
            }
        } else if (ch == '.') {
            for (int i = 0; i < 26; i++) {
                TrieNode * child = node->child[i];
                if (child != nullptr && dfs(word, index + 1, child)) {
                    return true;
                }
            }
        }
        return false;
    }
private:
    TrieNode * trie;
};


/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary* obj = new WordDictionary();
 * obj->addWord(word);
 * bool param_2 = obj->search(word);
 */
```

#### [453. 最小操作次数使数组元素相等](https://leetcode-cn.com/problems/minimum-moves-to-equal-array-elements/)

给你一个长度为 `n` 的整数数组，每次操作将会使 `n - 1` 个元素增加 `1` 。返回让数组所有元素相等的最小操作次数。

**示例 1：**

```
输入：nums = [1,2,3]
输出：3
解释：
只需要3次操作（注意每次操作会增加两个元素的值）：
[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]
```

**示例 2：**

```
输入：nums = [1,1,1]
输出：0
```

 

**提示：**

- `n == nums.length`
- `1 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`
- 答案保证符合 **32-bit** 整数

```c++
 int minMoves(vector<int>& nums) {
        int minNum = *min_element(nums.begin(),nums.end());
        int res = 0;
        for (int num : nums) {
            res += num - minNum;
        }
        return res;
    }

```

#### [66. 加一](https://leetcode-cn.com/problems/plus-one/)

给定一个由 **整数** 组成的 **非空** 数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储**单个**数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

 

**示例 1：**

```
输入：digits = [1,2,3]
输出：[1,2,4]
解释：输入数组表示数字 123。
```

**示例 2：**

```
输入：digits = [4,3,2,1]
输出：[4,3,2,2]
解释：输入数组表示数字 4321。
```

**示例 3：**

```
输入：digits = [0]
输出：[1]
```

 

**提示：**

- `1 <= digits.length <= 100`
- `0 <= digits[i] <= 9`

```c++
//直接
    vector<int> plusOne(vector<int>& digits) {
        int n = digits.size()-1;
        digits[n]+=1;
        if(digits[n] <= 9)return digits;
        while(n > 0)
        {
            digits[n] = 0;
            digits[--n] += 1;
            if(digits[n]<=9){break;}
        }
        if(digits[0]==10)
        {
            digits[0]=0;
            digits.insert(digits.begin(),1);
        }
        return digits;
    }
//判断尾部的9
    vector<int> plusOne(vector<int>& digits) {
       int n = digits.size();
        for (int i = n - 1; i >= 0; --i) {
            if (digits[i] != 9) {
                ++digits[i];
                for (int j = i + 1; j < n; ++j) {
                    digits[j] = 0;
                }
                return digits;
            }
        }

        // digits 中所有的元素均为 9
        vector<int> ans(n + 1);
        ans[0] = 1;
        return ans;
    }
```

#### [229. 求众数 II](https://leetcode-cn.com/problems/majority-element-ii/)

给定一个大小为 *n* 的整数数组，找出其中所有出现超过 `⌊ n/3 ⌋` 次的元素。

**示例 1：**

```
输入：[3,2,3]
输出：[3]
```

**示例 2：**

```
输入：nums = [1]
输出：[1]
```

**示例 3：**

```
输入：[1,1,1,3,3,2,2,2]
输出：[1,2]
```

 

**提示：**

- `1 <= nums.length <= 5 * 104`
- `-109 <= nums[i] <= 109`

 

**进阶：**尝试设计时间复杂度为 O(n)、空间复杂度为 O(1)的算法解决此问题。

```c++
    vector<int> majorityElement(vector<int>& nums) {
  int n = nums.size();
        vector<int> ans;
        unordered_map<int, int> cnt;

        for (auto & v : nums) {
            cnt[v]++;
        }
        for (auto & v : cnt) {
            if (v.second > n / 3) {
                ans.push_back(v.first);
            }
        }
        return ans;
    }
```

#### [492. 构造矩形](https://leetcode-cn.com/problems/construct-the-rectangle/)

作为一位web开发者， 懂得怎样去规划一个页面的尺寸是很重要的。 现给定一个具体的矩形页面面积，你的任务是设计一个长度为 L 和宽度为 W 且满足以下要求的矩形的页面。要求：

```
1. 你设计的矩形页面必须等于给定的目标面积。

2. 宽度 W 不应大于长度 L，换言之，要求 L >= W 。

3. 长度 L 和宽度 W 之间的差距应当尽可能小。
```

你需要按顺序输出你设计的页面的长度 L 和宽度 W。

**示例：**

```
输入: 4
输出: [2, 2]
解释: 目标面积是 4， 所有可能的构造方案有 [1,4], [2,2], [4,1]。
但是根据要求2，[1,4] 不符合要求; 根据要求3，[2,2] 比 [4,1] 更能符合要求. 所以输出长度 L 为 2， 宽度 W 为 2。
```

**说明:**

1. 给定的面积不大于 10,000,000 且为正整数。
2. 你设计的页面的长度和宽度必须都是正整数。

```c++
 vector<int> constructRectangle(int area) {
	int w, l;
	w = sqrt(area);
	l = area / w;
	while (w*l != area)
	{
		if (w == 1)break;
		w ++;
		l = area / w;
	}
    return {w,l};
    }
```

#### [638. 大礼包](https://leetcode-cn.com/problems/shopping-offers/)

难度中等278

在 LeetCode 商店中， 有 `n` 件在售的物品。每件物品都有对应的价格。然而，也有一些大礼包，每个大礼包以优惠的价格捆绑销售一组物品。

给你一个整数数组 `price` 表示物品价格，其中 `price[i]` 是第 `i` 件物品的价格。另有一个整数数组 `needs` 表示购物清单，其中 `needs[i]` 是需要购买第 `i` 件物品的数量。

还有一个数组 `special` 表示大礼包，`special[i]` 的长度为 `n + 1` ，其中 `special[i][j]` 表示第 `i` 个大礼包中内含第 `j` 件物品的数量，且 `special[i][n]` （也就是数组中的最后一个整数）为第 `i` 个大礼包的价格。

返回 **确切** 满足购物清单所需花费的最低价格，你可以充分利用大礼包的优惠活动。你不能购买超出购物清单指定数量的物品，即使那样会降低整体价格。任意大礼包可无限次购买。

 

**示例 1：**

```
输入：price = [2,5], special = [[3,0,5],[1,2,10]], needs = [3,2]
输出：14
解释：有 A 和 B 两种物品，价格分别为 ¥2 和 ¥5 。 
大礼包 1 ，你可以以 ¥5 的价格购买 3A 和 0B 。 
大礼包 2 ，你可以以 ¥10 的价格购买 1A 和 2B 。 
需要购买 3 个 A 和 2 个 B ， 所以付 ¥10 购买 1A 和 2B（大礼包 2），以及 ¥4 购买 2A 。
```

**示例 2：**

```
输入：price = [2,3,4], special = [[1,1,0,4],[2,2,1,9]], needs = [1,2,1]
输出：11
解释：A ，B ，C 的价格分别为 ¥2 ，¥3 ，¥4 。
可以用 ¥4 购买 1A 和 1B ，也可以用 ¥9 购买 2A ，2B 和 1C 。 
需要买 1A ，2B 和 1C ，所以付 ¥4 买 1A 和 1B（大礼包 1），以及 ¥3 购买 1B ， ¥4 购买 1C 。 
不可以购买超出待购清单的物品，尽管购买大礼包 2 更加便宜。
```

 

**提示：**

- `n == price.length`
- `n == needs.length`
- `1 <= n <= 6`
- `0 <= price[i] <= 10`
- `0 <= needs[i] <= 10`
- `1 <= special.length <= 100`
- `special[i].length == n + 1`
- `0 <= special[i][j] <= 50`

#### [240. 搜索二维矩阵 II](https://leetcode-cn.com/problems/search-a-2d-matrix-ii/)

难度中等836

编写一个高效的算法来搜索 `*m* x *n*` 矩阵 `matrix` 中的一个目标值 `target` 。该矩阵具有以下特性：

- 每行的元素从左到右升序排列。
- 每列的元素从上到下升序排列。

 

**示例 1：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/11/25/searchgrid2.jpg)

```
输入：matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5
输出：true
```

**示例 2：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/11/25/searchgrid.jpg)

```
输入：matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 20
输出：false
```

 

**提示：**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= n, m <= 300`
- `-109 <= matrix[i][j] <= 109`
- 每行的所有元素从左到右升序排列
- 每列的所有元素从上到下升序排列
- `-109 <= target <= 109`

```c++
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
          for (const auto& row: matrix) {
            for (int element: row) {
                if (element == target) {
                    return true;
                }
            }
        }
        return false;
    }
```

#### [496. 下一个更大元素 I](https://leetcode-cn.com/problems/next-greater-element-i/)

难度简单583

给你两个 **没有重复元素** 的数组 `nums1` 和 `nums2` ，其中`nums1` 是 `nums2` 的子集。

请你找出 `nums1` 中每个元素在 `nums2` 中的下一个比其大的值。

`nums1` 中数字 `x` 的下一个更大元素是指 `x` 在 `nums2` 中对应位置的右边的第一个比 `x` 大的元素。如果不存在，对应位置输出 `-1` 。

 

**示例 1:**

```
输入: nums1 = [4,1,2], nums2 = [1,3,4,2].
输出: [-1,3,-1]
解释:
    对于 num1 中的数字 4 ，你无法在第二个数组中找到下一个更大的数字，因此输出 -1 。
    对于 num1 中的数字 1 ，第二个数组中数字1右边的下一个较大数字是 3 。
    对于 num1 中的数字 2 ，第二个数组中没有下一个更大的数字，因此输出 -1 。
```

**示例 2:**

```
输入: nums1 = [2,4], nums2 = [1,2,3,4].
输出: [3,-1]
解释:
    对于 num1 中的数字 2 ，第二个数组中的下一个较大数字是 3 。
    对于 num1 中的数字 4 ，第二个数组中没有下一个更大的数字，因此输出 -1 。
```

 

**提示：**

- `1 <= nums1.length <= nums2.length <= 1000`
- `0 <= nums1[i], nums2[i] <= 104`
- `nums1`和`nums2`中所有整数 **互不相同**
- `nums1` 中的所有整数同样出现在 `nums2` 中

 

**进阶：**你可以设计一个时间复杂度为 `O(nums1.length + nums2.length)` 的解决方案吗？

```c++
  vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
        vector<int> res;
        bool flag;
        for(int k = 0; k<nums1.size();k++)
        {
            for(int i = 0; i<nums2.size();i++)
            {
                if(nums1[k] == nums2[i] && !flag)
                {
                    flag = true;
                }
                if(flag)
                {
                    if(nums1[k] < nums2[i])
                    {
                        res.push_back(nums2[i]);
                        flag = false;
                        break;
                    }
                }
            }
            if(res.size() < k+1)
            {
                res.push_back(-1);
            }
            flag = false;
        }
        return res;
    }
```

#### [301. 删除无效的括号](https://leetcode-cn.com/problems/remove-invalid-parentheses/)

给你一个由若干括号和字母组成的字符串 `s` ，删除最小数量的无效括号，使得输入的字符串有效。

返回所有可能的结果。答案可以按 **任意顺序** 返回。

 

**示例 1：**

```
输入：s = "()())()"
输出：["(())()","()()()"]
```

**示例 2：**

```
输入：s = "(a)())()"
输出：["(a())()","(a)()()"]
```

**示例 3：**

```
输入：s = ")("
输出：[""]
```

 

**提示：**

- `1 <= s.length <= 25`
- `s` 由小写英文字母以及括号 `'('` 和 `')'` 组成
- `s` 中至多含 `20` 个括号

```c++
  vector<string> removeInvalidParentheses(string s) {
        vector<string> res;
        remove(move(s), {'(', ')'}, 0, 0, res);
        return res;
    }
    
    void remove(std::string s, const vector<char>& par, int m, int n, vector<string>& res) {
        int stack = 0, i = m;
        for (int i = m; i < s.length(); ++i) {
            if (s[i] == par[0]) stack++;
            if (s[i] == par[1]) stack--;
            if (stack >= 0) continue;
            // "右"括号多出来了，删除一个右括号
            for (int j = n; j <= i; ++j) {
                if (s[j] == par[1] && (j == n || s[j-1] != par[1])) {
                    auto ss = s.substr(0, j) + s.substr(j + 1);
                    remove(move(ss), par, i, j, res);
                }
            }

            return;
        }
        
        reverse(s.begin(), s.end());
        if (par[0] == '(') {
            remove(move(s), {par[1], par[0]}, 0, 0, res);
        } else {
            res.push_back(move(s));
        }
    }
```

#### [869. 重新排序得到 2 的幂](https://leetcode-cn.com/problems/reordered-power-of-2/)

给定正整数 `N` ，我们按任何顺序（包括原始顺序）将数字重新排序，注意其前导数字不能为零。

如果我们可以通过上述方式得到 2 的幂，返回 `true`；否则，返回 `false`。

 



**示例 1：**

```
输入：1
输出：true
```

**示例 2：**

```
输入：10
输出：false
```

**示例 3：**

```
输入：16
输出：true
```

**示例 4：**

```
输入：24
输出：false
```

**示例 5：**

```
输入：46
输出：true
```

 

**提示：**

1. `1 <= N <= 10^9`

```c++
vector<int> vis;

    bool isPowerOfTwo(int n) {
        return (n & (n - 1)) == 0;
    }

    bool backtrack(string &nums, int idx, int num) {
        if (idx == nums.length()) {
            return isPowerOfTwo(num);
        }
        for (int i = 0; i < nums.length(); ++i) {
            // 不能有前导零
            if ((num == 0 && nums[i] == '0') || vis[i] || (i > 0 && !vis[i - 1] && nums[i] == nums[i - 1])) {
                continue;
            }
            vis[i] = 1;
            if (backtrack(nums, idx + 1, num * 10 + nums[i] - '0')) {
                return true;
            }
            vis[i] = 0;
        }
        return false;
    }

public:
    bool reorderedPowerOf2(int n) {
        string nums = to_string(n);
        sort(nums.begin(), nums.end());
        vis.resize(nums.length());
        return backtrack(nums, 0, 0);
    }

```

#### [237. 删除链表中的节点](https://leetcode-cn.com/problems/delete-node-in-a-linked-list/)

难度简单1045

请编写一个函数，用于 **删除单链表中某个特定节点** 。在设计函数时需要注意，你无法访问链表的头节点 `head` ，只能直接访问 **要被删除的节点** 。

题目数据保证需要删除的节点 **不是末尾节点** 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/09/01/node1.jpg)

```
输入：head = [4,5,1,9], node = 5
输出：[4,1,9]
解释：指定链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/09/01/node2.jpg)

```
输入：head = [4,5,1,9], node = 1
输出：[4,5,9]
解释：指定链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9
```

**示例 3：**

```
输入：head = [1,2,3,4], node = 3
输出：[1,2,4]
```

**示例 4：**

```
输入：head = [0,1], node = 0
输出：[1]
```

**示例 5：**

```
输入：head = [-3,5,-99], node = -3
输出：[5,-99]
```

 

**提示：**

- 链表中节点的数目范围是 `[2, 1000]`
- `-1000 <= Node.val <= 1000`
- 链表中每个节点的值都是唯一的
- 需要删除的节点 `node` 是 **链表中的一个有效节点** ，且 **不是末尾节点**

```c++
    void deleteNode(ListNode* node) {
         node->val = node->next->val;
        node->next = node->next->next;
    }
```



