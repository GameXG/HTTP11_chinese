HTTP没有对每个头字段的长度或者整个头部分的长度放置预定义的限制，就像2.5节所描述的那样。在实践中发现各个头部字段长度的特定限制，通常取决于具体的字段语义。

服务器接收一个头字段或一系列字段比它期望处理的要大的请求时**必须**响应一个适当的4XX（客户端错误）状态码。忽略这些头字段将增加服务器对请求走私攻击的漏洞（9.5节）。

客户端**可以**丢弃或截断大于客户端希望处理的接收到的头部字段，如果字段语义是这样的，即在不改变消息成帧或响应语义的情况下可以安全地忽略丢弃的值。

