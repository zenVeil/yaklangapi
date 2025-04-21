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

## CutPrefix
- 描述信息: 返回不包含所提供前导前缀字符串的 s，并返回是否找到该前缀。

<Tabs>
  <TabItem value="CalcSimHash-1" label="函数介绍" default>
    ```go
    after string, found bool = str.CutPrefix(s string, prefix string) 
    ```
  </TabItem>
  <TabItem value="CalcSimHash-2" label="示例">
    ```go
    after, found = str.CutPrefix("Hello Yakiy", "He") 
    printf(" He 后面的字符串: %s; 是否包含 He 字符串: %t\n", after, found)

    // 输出信息如下: 
    // He 后面的字符串: llo Yakiy; 是否包含 He 字符串: true
    ```
  </TabItem>
</Tabs>

## CutSuffix
- 描述信息：返回不包含指定结尾后缀字符串的 s，并返回是否找到该后缀

<Tabs>
  <TabItem value="CalcSimHash-1" label="函数介绍" default>
    ```go
    before string, found bool = str.CutSuffix(s string, suffix string) 
    ```
  </TabItem>
  <TabItem value="CalcSimHash-2" label="示例">
    ```go
    before, found = str.CutSuffix("Hello Yakiy", "iy") 
    printf(" iy 前面的字符串: %s; 是否包含 iy 字符串: %t\n", before, found)

    // 输出信息如下: 
    // iy 前面的字符串: Hello Yak; 是否包含 iy 字符串: true
    ```
  </TabItem>
</Tabs>

## EndsWith / HasSuffix
- 描述信息: 判断字符串s是否以suffix结尾

```go
str.EndsWith("Hello Yak", "Yak") // true
str.EndsWith("Hello Yak", "Hello") // false
```

## EqualFold
- 描述信息：判断字符串s和t是否相等，忽略大小写

```go
str.EqualFold("hello Yak", "HELLO YAK") // true
```

## ExtractBodyFromHTTPResponseRaw
- 描述信息: 从原始 HTTP 响应报文中提取 body

<Tabs>
  <TabItem value="ExtractBodyFromHTTPResponseRaw-1" label="函数介绍" default>
    ```go
    body, _ = str.ExtractBodyFromHTTPResponseRaw(b"HTTP/1.1 200 OK\r\nContent-Length: 2\r\n\r\nok") // body = b"ok"
    println(string(body))
    ```
  </TabItem>
  <TabItem value="ExtractBodyFromHTTPResponseRaw-2" label="项目示例">
    ```go
    flows = yakit.QueryHTTPFlowsByKeyword("https://cde-gateway.cscec.com/aecmate/province/list")
    for flow in flows{
        body,_ = str.ExtractBodyFromHTTPResponseRaw(flow.GetResponse())
        println(body)
    }

    // 输出信息如下: 
    // 输出信息为：Body 信息
    ```
  </TabItem>
</Tabs>

## ExtractChineseIDCards
- 描述信息: 尝试将传入的参数转换为字符串，然后提取字符串中的身份证号

```go
str.ExtractChineseIDCards("Your ChineseID is: 110101202008027420?") // ["110101202008027420"]
```

## ExtractDomain
- 描述信息： 尝试提取字符串中的域名并返回，可以添加一个 tryDecode 参数，如果传入 true，则会尝试对输入的文本进行解码(双重URL编码，URL编码，unicode编码，quoted编码)

```go
[]string = ExtractDomain(i any, tryDecode ...bool) 

str.ExtractDomain("hello yak") // []
str.ExtractDomain("hello yaklang.com or yaklang.io") // ["yaklang.com", "yaklang.io"]
str.ExtractDomain(`{"message:"%79%61%6b%6c%61%6e%67.com"}`, true) // ["yaklang.com"]
```

## ExtractHost
- 描述信息: 尝试从字符串中解析出host和port，并返回host

```go
string = ExtractHost(raw string) 

str.ExtractHost("127.0.0.1:8888") // 127.0.0.1
str.ExtractHost("https://example.com") // example.com
```

## ExtractHostPort
- 描述信息: 尝试从字符串中解析出host和port，并返回host:port

```go
string = ExtractHostPort(raw string) 

str.ExtractHostPort("https://127.0.0.1:8888") // 127.0.0.1:8888
str.ExtractHostPort("https://baidu.com") // 127.0.0.1:443
```

## ExtractJson
- 描述信息: 尝试提取字符串中的 JSON 并进行修复返回

```go
[]string = ExtractJson(i any)

str.ExtractJson("hello yak") // []
str.ExtractJson(`{"hello": "yak"}`) // [{"hello": "yak"}]
```

## ExtractJsonWithRaw
- 描述信息: 尝试提取字符串中的 JSON 并返回，第一个返回值返回经过修复后的JSON字符串数组，第二个返回值返回原始JSON字符串数组(如果修复失败)

```go
successJson[]string, failJson[]string = ExtractJsonWithRaw(i any)

str.ExtractJsonWithRaw("hello yak") // [], []
str.ExtractJsonWithRaw(`{"hello": "yak"}`) // [{"hello": "yak"}], []
```

## ExtractRootDomain
- 描述信息: 尝试提取字符串中的根域名并返回

```go
domain []string = ExtractRootDomain(i any)

str.ExtractRootDomain("hello yak") // []
str.ExtractRootDomain("hello www.yaklang.com or www.yaklang.io") // ["yaklang.com", "yaklang.io"]
```

## ExtractStrContext
- 描述信息: 从字符串raw中提取一组关键字res上下文的内容，上下文的长度是512个字符确定

```go
[]string = ExtractStrContext(raw string, res []string) 

str.ExtractStrContext("hello yak", ["hello"]) // ["hello yak"]
```

## ExtractTitle
- 描述信息: 尝试将传入的字符串进行HTML解析并提取其中的标题(title标签)返回

```go
str.ExtractTitle("hello yak") // ""
str.ExtractTitle("<title>hello yak</title>") // "hello yak"
```

## ExtractURLFromHTTPRequest
- 描述信息: 从 HTTP 请求结构体中提取 URL，返回URL结构体与错误

```go
url, err := str.ExtractURLFromHTTPRequestRaw(b"GET / HTTP/1.1\r\nHost: www.yaklang.com\r\n\r\n", false)
```

## Fields
- 描述信息: 返回将字符串s按照空白字符（'\t', '\n', '\v', '\f', '\r', ' ', 0x85, 0xA0）分割的字符串切片

```go
str.Fields("hello world\nhello yak\tand\vyakit") // [hello", "world", "hello", "yak", "and", "yakit"]
```

## FilterPorts
- 描述信息: 接受两个字符串形式的端口列表作为参数，返回一个新的端口列表。返回 sourcePorts 独有的端口

<Tabs>
  <TabItem value="FilterPorts-1" label="函数介绍" default>
    ```go
    FilterPorts(sourcePorts string, excludePorts string) []int
    ```
  </TabItem>
  <TabItem value="FilterPorts-2" label="疑问">
    ```go
    println(str.FilterPorts("1-10", "2-11"))

    // 输出信息如下: 
    // 输出信息为：[1]
    ```
  </TabItem>
</Tabs>

## FixHTTPRequest
- 描述信息: 尝试对传入的HTTP请求报文进行修复，并返回修复后的请求

```go
str.FixHTTPRequest(b"GET / HTTP/1.1\r\nHost: example.com\r\n\r\n")
```

## FixHTTPResponse
- 描述信息: 尝试对传入的响应进行修复，并返回修复后的响应，响应体和错误

```go
fixedResponse, body, err = str.FixHTTPResponse(b"HTTP/1.1 200 OK\r\nContent-Type: text/html; charset=gbk\r\n\r\n<html>你好</html>")
```

## Grok
- 描述信息: Grok 用于将字符串 line 使用 Grok 以规则 rule 进行解析，并返回解析结果(map)，参考 [Grok 正则捕获](https://doc.yonyoucloud.com/doc/logstash-best-practice-cn/filter/grok.html) 获取更多信息。

```go
str.Grok("04/18-00:59:45.385191", "%{MONTHNUM:month}/%{MONTHDAY:day}-%{TIME:time}") // map[HOUR:[00] MINUTE:[59] SECOND:[45.385191] day:[18] month:[04] time:[00:59:45.385191]]
```

## StartsWith / HasPrefix
- 描述信息: 判断字符串s是否以prefix开头

```go
str.StartsWith("Hello Yak", "Hello") // true
str.StartsWith("Hello Yak", "Yak") // false
```

## HostPort
- 描述信息: 将 host 和 port 拼接成 host:port 的形式

```go
str.HostPort("yaklang.com", 443) // yaklang.com:443
```

## IPv4ToCClassNetwork
- 描述信息: 尝试从一个 IPv4 地址中获取 C 类网络地址，并返回错误

```go
network, err = str.IPv4ToCClassNetwork("192.168.0.1") // network = "192.168.0.0/24", err = nil
```
## Index
- 描述信息: 返回字符串s中substr第一次出现的位置的索引，如果字符串中不存在substr，则返回-1

```go
str.Index("hello yak", "yak") // 6
str.Index("hello world", "yak") // -1
```
