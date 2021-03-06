"Upgrade"头字段试图提供一个简单的机制来从HTTP/1.1过渡到同连接上的其他协议。客户端**可能**在请求的Upgrade头字段中发送一个协议列表来邀请服务器在发送最终响应前切换到一个或多个其他的协议，按下降的优先顺序。如果服务器希望在那个连接上继续使用当前协议，它**可能**忽略接收到的Upgrade头字段。Upgrade不能被用于坚持协议切换。

> ```
>      Upgrade          = 1#protocol
>
>      protocol         = protocol-name ["/" protocol-version]
>      protocol-name    = token
>      protocol-version = token
> ```

发送101（协议切换）响应的服务器**必须**发送Upgrade头字段来指示连接将被切换到的新协议；如果多个协议层被切换，发送者**必须**按层上升的顺序列出协议。服务器**不得**切换没有被客户端在对应的请求的Upgrade头字段中指明的协议。服务器**可能**选择忽略客户端指定的优先权的顺序并基于其它因素选择新的协议，例如请求的性质或者当前的服务器负载。

发送了426（需要Upgrade）响应的服务器**必须**发送一个Upgrade头字段以表明可接受的协议，以下降的优先级顺序。

服务器**可能**在其他任何响应中发送一个Upgrade头字段，以便在适合未来请求时，以下降的优先级排列来告知实现支持切换到列出的协议。

下列是一个由客户端发送的假想例子：

> ```
>      GET /hello.txt HTTP/1.1
>      Host: www.example.com
>      Connection: upgrade
>      Upgrade: HTTP/2.0, SHTTP/1.3, IRC/6.9, RTA/x11
> ```

协议切换后的应用层通讯的功能和性质完全依赖于新协议的选择。但是，在发送101（交换协议）响应之后，服务器应该立即继续响应原来的请求，就好像它已经在新的协议（即，在协议被改变之后，服务器仍然有一个突出的请求来满足，并且期望在不需要重复请求的情况下这样做）。

例如，如果Upgrade头字段被在一个GET请求中接收并且服务器决定切换协议，他首先以HTTP/1.1的101（交换协议）消息响应然后紧接着新的协议等同于对目标资源的GET响应。这允许将连接升级到与HTTP具有相同语义的协议，而无需额外往返的延迟成本。服务器**不得**切换协议除非接收消息语义可以被芯协议认可；OPTIONS请求可以被任何协议认可。

下面是上面的假想请求的一个响应的例子：

> ```
>      HTTP/1.1 101 Switching Protocols
>      Connection: upgrade
>      Upgrade: HTTP/2.0
>
>      [... data stream switches to HTTP/2.0 with an appropriate response
>      (as defined by new protocol) to the "GET /hello.txt" request ...]
> ```

当Upgrade被发送，发送者**必须**也发送一个Connection头字段（6.1节），其包含一个“upgrade”连接选项以防止Upgrade被没有实现列出的协议的中介意外的转发。服务器**必须**忽略在HTTP/1.0中接收到的Upgrade头字段。

客户端不得在一个连接上开始使用升级后的协议，知道它已经完整的发送了请求消息（即，客户端不能在发送消息的中间切换协议）。如果一个服务器同时收到一个带有“100-continue”期望的Upgrade和Expect头字段（RFC7231的第5.1.1节），则服务器必须在发送101（交换协议）响应之前发送100（继续）响应。

Upgrade头字段仅用于切换已存在连接的最上层协议；它不能被用于切换底层连接（传输层）协议，或者在不同的连接中切换已存在的会话。出于那些目的，使用一个3xx（重定向）响应（RFC7231的6.4节）更为合适。

本规范仅定义了由超文本转移协议族使用的协议名称“HTTP”，由第2.6节的HTTP版本规则和本规范的未来更新定义。 额外的令牌应该使用8.6节定义的注册程序向IANA注册。