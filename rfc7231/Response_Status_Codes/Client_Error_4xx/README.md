4xx（客户端错误）类状态码表明客户端似乎有错误。除了当响应HEAD请求时，服务器**应该**发送一个包含错误情况说明的表示，以及它是一个临时还是永久的情况。这些状态码对任何请求方法都适用。用户代理**应该**给用户展示任何被包含的表示。