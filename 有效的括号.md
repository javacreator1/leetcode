# 有效的括号

题目描述：

给定一个只包括 `'('`，`')'`，`'{'`，`'}'`，`'['`，`']'` 的字符串，判断字符串是否有效。

有效字符串需满足：

1. 左括号必须用相同类型的右括号闭合。
2. 左括号必须以正确的顺序闭合。

注意空字符串可被认为是有效字符串。

**示例 1:**

```
输入: "()"
输出: true
```

**示例 2:**

```
输入: "()[]{}"
输出: true
```

**示例 3:**

```
输入: "(]"
输出: false
```

**示例 4:**

```
输入: "([)]"
输出: false
```

**示例 5:**

```
输入: "{[]}"
输出: true
```

# 解析

解题的经典思路：

## 有效括号

a.使用栈去存储左括号，然后遇到右括号时检查是否与栈顶元素匹配,如果匹配，则继续执行程序，然后遍历完所有字符串后再检查一下栈，如果栈为空，说明所有括号都匹配完毕，为有效括号。



## 无效括号

a.使用栈去存储左括号，然后遇到右括号时检查是否与栈顶元素匹配，如果不匹配那就说明这个字符串不是有效的括号。

b.另外如果栈为空时遇到了右括号，那说明也不是有效字符串。

c.如果栈不为空就是无效括号。

（程序中增加了奇偶检测，增加效率）

```java
public static boolean isValid(String s) {
        Map<Character, Character> map = new HashMap<>();
        map.put(')', '(');
        map.put('}', '{');
        map.put(']', '[');
        Stack<Character> stack=new Stack<>();
        //将s变成char[]
        char[]arrays=s.toCharArray();
        for (int i = 0; i < arrays.length; i++) {
            //如果char[i]是左括号，则入栈。
            char c = arrays[i];
            switch (c){
                //如果arrays[i]是左括号，则入栈。
                case '(' :
                case '[' :
                case '{' :
                    stack.push(c);
                    break;
                //如果arrays[i]是右括号,则判断出栈元素和arrays[i]是否匹配，匹配返回true，不匹配返回false，栈空返回false。
                case ')':
                case ']':
                case '}':
                    if (stack.isEmpty() || stack.pop() != map.get(c)) {
                        return false;
                    }
                    break;
            }
        }
        if (stack.isEmpty()) {
            return true;
        } else {
            return false;
        }
    }
```

