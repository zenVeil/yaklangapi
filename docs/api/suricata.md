---
sidebar_position: 79
sidebar_label: suricata
slug: /api/suricata
tags: []
title: suricata
description: 描述信息
---
# 函数定义
## LoadSuricataToDatabase
- 描述: 将原始 Suricata 规则字符串加载到数据库中，便于后续规则管理和匹配操作。

```go
rawRules := `alert http any any -> any any (msg:"Test Rule"; content:"example"; sid:1;)`
suricata.LoadSuricataToDatabase(rawRules)
```

## NewSuricataMatcher
- 描述: 基于指定的 Suricata 规则对象创建一个匹配器，用于对网络数据包进行规则匹配

```go
rules, _ := suricata.ParseSuricata(`alert tcp any any -> any any (msg:"match test"; content:"abc"; sid:2;)`)
matcher := suricata.NewSuricataMatcher(rules[0])
```

## NewSuricataMatcherGroup
- 描述: 创建一个规则匹配器组，支持通过可选参数配置匹配行为，例如添加回调函数等。

```go
group := suricata.NewSuricataMatcherGroup(
    suricata.groupCallback(func(pkt, rule) {
        println("Matched:", rule.SID)
    })
)
```

## ParseSuricata
- 描述: 解析 Suricata 规则字符串，返回规则对象列表。可选的环境变量参数用于处理规则中的变量替换。

```go
rules, err := suricata.ParseSuricata(`
    alert tcp any any -> any any (msg:"Test1"; content:"aaa"; sid:1001;)
    alert udp any any -> any any (msg:"Test2"; content:"bbb"; sid:1002;)
`)
```

## TrafficGenerator
- 描述: 创建一个流量生成器对象，用于模拟网络流量，测试规则的匹配效果。

```go
gen := suricata.TrafficGenerator()
gen.TCP("192.168.0.1", "80").Payload("abc").Send()
```

## YieldRules
- 描述: 返回一个通道，逐个输出已加载的规则存储对象，适用于规则遍历和处理。

```go
for r := range suricata.YieldRules() {
    println("Rule:", r.Rule.SID)
}
```

## YieldRulesByKeyword
- 描述: 根据指定的关键字和协议过滤规则，返回匹配的规则存储对象通道。

```go
for r := range suricata.YieldRulesByKeyword("example", "http") {
    println("Matched rule SID:", r.Rule.SID)
}
```

## YieldSuricataRulesByKeywords
- 描述: 功能类似于 YieldRulesByKeyword，用于根据关键字和协议筛选 Suricata 规则。

```go
for r := range suricata.YieldSuricataRulesByKeywords("test", "tcp") {
    println("Filtered SID:", r.Rule.SID)
}
```

## groupCallback
- 描述: 定义一个回调函数选项，用于在规则匹配时执行特定操作，如日志记录或自定义处理。

```go
cb := suricata.groupCallback(func(pkt, rule) {
    println("Detected:", rule.Msg)
})
group := suricata.NewSuricataMatcherGroup(cb)
```