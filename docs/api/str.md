---
sidebar_position: 77
sidebar_label: str
slug: /api/str
tags: []
title: str
description: 描述信息
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# 函数定义

## CalcSSDeep
- 描述: CalcSSDeep 计算并返回一段文本的模糊哈希值。
- 使用注意实现: 如果要计算的文本过短, 就无法计算会产生报错信息。


<Tabs>
  <TabItem value="CalcSSDeep-1" label="函数介绍" default>
    ```go
    hash = CalcSSDeep(raw []byte)
    ```
  </TabItem>
  <TabItem value="CalcSSDeep-2" label="示例">
    ```go
    // 查询所有的yakit历史流量
    flows := yakit.QueryHTTPFlowsAll()

    for flow in flows{
        // 计算响应信息的模糊哈希值
        println(str.CalcSimHash(flow.Response))
    }

    // 输出信息如下: 
    // -6096821334166095955
    // -6096821334166095955
    ```
  </TabItem>
</Tabs>



## CalcSSDeepStability
- 描述: 使用模糊哈希算法计算多段文本之间的相似度，返回相似度与错误。
- 使用注意事项: 传入的文本应该为大文本，即长度大于 30 kb

<Tabs>
  <TabItem value="CalcSSDeepStability-1" label="函数介绍" default>
    ```go
    p, err = str.CalcSSDeepStability(str.RandStr(100000), str.RandStr(100000))
    ```
  </TabItem>
  <TabItem value="CalcSSDeepStability-2" label="示例">
    ```go
    // 随机生成 100000 个字符, 进行比较
    p, _ = str.CalcSSDeepStability(str.RandStr(100000), str.RandStr(100000))
    println(p)

    // 输出信息如下: 
    // 0.11 
    ```
  </TabItem>
</Tabs>

## CalcSimHash
- 描述信息: 计算并返回一段文本的 SimHash 值

<Tabs>
  <TabItem value="CalcSimHash-1" label="函数介绍" default>
    ```go
    p = str.CalcSimHash("hello")
    ```
  </TabItem>
  <TabItem value="CalcSimHash-2" label="示例">
    ```go
    p = str.CalcSimHash("hellcdvfbgnho")
    println(p)

    // 输出信息如下: 
    // -10224759973408639
    ```
  </TabItem>
</Tabs>

## CalcSimHashStability
- 描述信息：使用 SimHash 算法计算多段文本之间的相似度，返回相似度与错误。

<Tabs>
  <TabItem value="CalcSimHash-1" label="函数介绍" default>
    ```go
    p, err = str.CalcSimHashStability("hello", "hello world") // p = 0.96484375
    ```
  </TabItem>
</Tabs>


## CalcSimilarity
- 描述信息: 计算多段文本之间的相似度，根据最长的文本长度选择不同的算法。
  - 如果最长的文本长度小于等于 2000，使用文本子串匹配算法
  - 如果最短的文本长度大于等于 30000，使用模糊哈希算法
  - 如果上述算法出现错误，则使用 SimHash 算法

<Tabs>
  <TabItem value="CalcSimilarity-1" label="函数介绍" default>
    ```go
    str.CalcSimilarity("hello", "hello world") // 0.625
    ```
  </TabItem>
</Tabs>

## CalcTextMaxSubStrStability
- 描述信息: 使用文本子串匹配算法计算多段文本之间的相似度，返回相似度与错误

<Tabs>
  <TabItem value="CalcTextMaxSubStrStability-1" label="函数介绍" default>
    ```go
    p, err = str.CalcTextMaxSubStrStability("hello", "hello world") // p = 0.625
    ```
  </TabItem>
</Tabs>

## Compare
- 描述信息: 按照ascii码表顺序逐个比较字符串a和b中的每个字符，如果 `a==b`，则返回 `0`，如果 `a<b`，则返回 `-1`，如果 `a>b` ，则返回`1`

<Tabs>
  <TabItem value="Compare-1" label="函数介绍" default>
    ```go
    str.Compare("hello yak", "hello yak") // 0
    str.Compare("hello yak", "hello") // 1
    str.Compare("hello", "hello yak") // -1
    ```
  </TabItem>
</Tabs>

## Contains
- 描述信息: 判断字符串s是否包含substr

<Tabs>
  <TabItem value="Contains-1" label="函数介绍" default>
    ```go
    str.Contains("hello yakit", "yak") // true
    ```
  </TabItem>
</Tabs>

## ContainsAny
- 描述信息: 判断字符串s是否包含chars中的任意字符

<Tabs>
  <TabItem value="ContainsAny-1" label="函数介绍" default>
    ```go
    str.ContainsAny("hello yak", "ly") // true
    str.ContainsAny("hello yak", "m") // false
    ```
  </TabItem>
</Tabs>

## Count
- 描述信息: 返回字符串s中substr出现的次数

<Tabs>
  <TabItem value="ContainsAny-1" label="函数介绍" default>
    ```go
    str.Count("hello yak", "l") // 2
    ```
  </TabItem>
</Tabs>

## Cut
- 描述信息: 判断 字符串s 是否在 subster 中, 并返回 字符串s 前后的文本。

<Tabs>
  <TabItem value="CalcSimHash-1" label="函数介绍" default>
    ```go
    before string, after string, found bool = Cut(s string, sep string)
    ```
  </TabItem>
  <TabItem value="CalcSimHash-2" label="示例">
    ```go
    before, after, found = str.Cut("hello yakit", "yak")
    before1, after1, found1 = str.Cut("hello yakit", "ds")
    before2, after2, found2 = str.Cut("hello yakit", "he")
    printf("yak 前面的字符串: %s; yak 后面的字符串: %s; 是否包含 yak 字符串: %t\n", before, after, found)
    printf("ds 前面的字符串: %s; ds 后面的字符串: %s; 是否包含 ds 字符串: %t\n", before1, after1, found1)
    printf("he 前面的字符串: %s; he 后面的字符串: %s; 是否包含 he 字符串: %t\n", before2, after2, found2)

    // 输出信息如下: 
    // yak 前面的字符串: hello ; yak 后面的字符串: it; 是否包含 yak 字符串: true
    // ds 前面的字符串: hello yakit; ds 后面的字符串: ; 是否包含 ds 字符串: false
    // he 前面的字符串: ; he 后面的字符串: llo yakit; 是否包含 he 字符串: true
    ```
  </TabItem>
</Tabs>

