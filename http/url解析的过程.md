### url的完整解析过程
- DNS域名解析 拿到ip地址
  - 浏览器自身缓存中是否存在当前域名
  - 本地host文件中是否存在当前域名
  - 本地域名服务器是否有当前域名的缓存
  - 根域名服务器会向顶级域名服务器(TLD),没有就报错，有的话返回ip
- TCP连接
  - TCP三次握手
    - 第一次握手：客户端A将标志位SYN置为1,随机产生一个值为seq=J（J的取值范围为=1234567）的数据包到服务器，客户端A进入SYN_SENT状态，等待服务端B确认；
    - 第二次握手：服务端B收到数据包后由标志位SYN=1知道客户端A请求建立连接，服务端B将标志位SYN和ACK都置为1，ack=J+1，随机产生一个值seq=K，并将该数据包发送给客户端A以确认连接请求，服务端B进入SYN_RCVD状态。
    - 第三次握手：客户端A收到确认后，检查ack是否为J+1，ACK是否为1，如果正确则将标志位ACK置为1，ack=K+1，并将该数据包发送给服务端B，服务端B检查ack是否为K+1，ACK是否为1，如果正确则连接建立成功，客户端A和服务端B进入ESTABLISHED状态，完成三次握手，随后客户端A与服务端B之间可以开始传输数据了。
- 客户端发送请求
  请求头包含了请求信息、请求头、请求正文
- 服务器处理请求，并返回响应
  响应包含了响应头、响应行、响应正文
- 浏览器渲染html
  - 构建DOM树
  - DOM树构建完毕后，与CSS一起构建渲染树
  - 布局渲染树
  - 绘制渲染树
浏览器渲染html是自上而下及逆行渲染的，但是遇到外链css，请求过程是异步的，不会影响渲染，但是对于外链的js来说，因为js加载是同步的，因此会停止DOM树的构建，会先加载js，等js加载完毕之后，在进行DOM树的绘制
- 四次挥手
  - 第一次挥手：Client发送一个FIN，用来关闭Client到Server的数据传送，Client进入FIN_WAIT_1状态。
  - 第二次挥手：Server收到FIN后，发送一个ACK给Client，确认序号为收到序号+1（与- SYN相同，一个FIN占用一个序号），Server进入CLOSE_WAIT状态。
  - 第三次挥手：Server发送一个FIN，用来关闭Server到Client的数据传送，Server进入LAST_ACK状态。
  - 第四次挥手：Client收到FIN后，Client进入TIME_WAIT状态，接着发送一个ACK给Server，确认序号为收到序号+1，Server进入CLOSED状态，完成四次挥手。

script 中增加defer 不会影响DOM树的渲染
