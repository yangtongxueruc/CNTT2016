WolfDelaymasterHard
===================

作者：袁宇韬

关键词：动态规划

题目简述
--------

给定一个由`wo?`三种字符组成的字符串$$s$$，问有多少种方案将`?`变为`w`或`o`，使得新字符串为若干个长度为偶数且前一半全部为`w`，后一半全部为`o`的字符串连接形成。答案对$$10^9+7$$取模。

算法一
------

将最终字符串中的每一段字符串的前一半称为`w`部分，后一半称为`o`部分。

用$$f_i$$表示前$$i$$个字符的答案。则容易通过枚举最后一段的长度得到一个$$O(n^2)$$的DP。考虑对这个DP的优化。

考虑$$f_j$$能够转移到$$f_i$$的条件。令$$l = \frac{i - j}{2}$$。分两种情况考虑。

如果`w`部分中只有`?`，则对于一个固定的$$j$$，`w`部分可行的条件为`s[j..j+l-1]`全部为`?`，`o`部分可行的条件为`s[j..j+2*l-1]`中没有`w`。满足条件的`l`为一个区间，可以用前缀和转移。

如果`w`部分中有至少一个`w`，则对于一个固定的$$i$$，`w`部分可行的条件为`s[i-2*l..i-l-1]`中没有`o`且有至少一个`w`，`o`部分可行的条件为`s[i-l..i-1]`中没有`w`。由于`o`部分中没有`w`，则`w`部分中一定包含`s[i]`之前的最近一个`w`字符，而`o`部分中则包含这个`w`字符之后的所有`o`字符。满足条件的`l`为一个区间，可以用前缀和转移。

时间复杂度$$O(n)$$。
