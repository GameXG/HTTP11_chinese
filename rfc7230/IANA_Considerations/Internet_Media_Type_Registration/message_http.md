message/http类型可以用于封装单个HTTP请求或者响应消息，只要它包含有关线路长度和编码的所有“消息”类型的MIME限制。

- 类型名：  message
- 亚类型名：  http
- 要求语法：  N/A
- 可选参数：  version, msgtype
  - version:  封装消息的HTTP版本号（例如，“1.1”）。如果不存在，版本可以从body的第一行来确定
  - msgtype:  消息类型——“请求”或“响应”。如果不存在，可以从body的第一行确定。
- 编码考虑：  只允许“7比特”，“8比特”，或者“二进制”。
- 安全考虑： 参阅第9节
- 互操作性考虑： N/A
- 发布的规范： 本规范（参阅8.3.1节）。
- 使用该媒体类型的应用： N/A
- 片段标识符考虑： N/A
- 额外信息：
  - 魔数： N/A
  - 该类型不赞成使用的别名：N/A
  - 文件扩展：N/A
  - Macintosh文件类型代码：N/A  
- 联系人和电子邮件地址以获取更多信息：查阅作者地址章节
- 预期用法： 通用
- 使用限制： N/A
- 作者： 查阅作者地址章节
- 修改控制器： IESG