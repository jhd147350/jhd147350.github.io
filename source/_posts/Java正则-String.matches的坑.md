---
title: Java正则-String.matches的坑
date: 2017-01-31 18:59:27
tags: 
- java
- 正则
- 正则表达式
categories: 
- java正则
comment: true
---

#Java正则-String.matches的坑

我想用String.matches匹配一行之中是否有特定的子串，结果死活出不来，我也在好多在线正则匹配的网上测试了，我正则表达式写的正确。查询了半天才知道，用String.matches匹配的正则，会在正则表达式前后加上^ $，是匹配整个大字符串是否满足正则表达式，而不会匹配到其中满足条件的子串！

```java
//我的想法是以下2种都会成功匹配，其实是错误的
//以下2种的正则"abc"相当于"^abc$",所以结果false
boolean a = "abcd".matches("abc");
boolean b =Pattern.matches("abc", "abcd");
System.out.println(a);//false
System.out.println(b);//false

//而这种方法就能成功匹配出abcd中的abc
Pattern p=Pattern.compile("abc");  
Matcher m=p.matcher("abcd");  
while(m.find()){  
	System.out.println(m.group());//abc  
}
```

不解的是java api中[Pattern.matches](http://tool.oschina.net/apidocs/apidoc?api=jdk_7u4)是这样说明的

> public static boolean matches(String regex,
              CharSequence input)
Compiles the given regular expression and attempts to match the given input against it.
An invocation of this convenience method of the form

>>Pattern.matches(regex, input);

>**behaves in exactly the same way as the expression**
 >>Pattern.compile(regex).matcher(input).matches()
 
>If a pattern is to be used multiple times, compiling it once and reusing it will be more efficient than invoking this method each time.

>    Parameters:
regex - The expression to be compiled
input - The character sequence to be matched

官网说表现是一样的，可结果肯定是不一样的啊。

参考链接：[stackoverflow](http://stackoverflow.com/questions/8923398/regex-doesnt-work-in-string-matches)