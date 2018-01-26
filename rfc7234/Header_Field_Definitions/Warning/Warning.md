### Warning: 110

响应过期

每当发送的响应过期，缓存就**应该**生成这个。

### Warning: 111

重校验失败

当缓存因尝试验证响应失败（由于无法叨叨服务器）而发送一个过期响应时，它就**应该**生成这个。

### Warning: 112

连接断开操作

如果缓存故意的从网络的其余部分断开一段时间，它**应该**生成这个。

### Warning: 113

启发式过期

如果缓存启发式的选择一个新鲜度生命期大于24小时，并且响应的年纪比24小时大，它**应该**生成这个。

### Warning: 119

杂项警告

这个告警文本可以包含任何信息用于呈现给人类用户或用于日志。一个接收到这个告警的系统**不得**作出任何自动的行动，除了将这个告警呈现给用户。

### Warning: 214

转型被应用

这个告警码**必须**由代理添加，如果它对表示应用了任何的转型，例如改变了内容编码，媒体类型或修改了表示数据，除非这个告警码已经出现在响应中。

### Warning: 299

杂项持续告警

告警文本可以包含任何信息用于呈现给人类用户或用于日志。一个接收到这个告警的系统**不得**做出任何自动的行为。