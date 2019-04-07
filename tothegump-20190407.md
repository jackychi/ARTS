# 2019-03-24
**# 1.Algorithm**
> 每周至少做一个 leetcode 的算法题  

虽然标记难度为中，实际上。。。比前面的都简单

https://leetcode.com/problems/binary-string-with-substrings-representing-1-to-n/
```
class Solution:
    def queryString(self, s: str, n: int) -> bool:
        s_list = [bin(i)[2:] for i in range(1, n+1)]
        return all(_ in s for _ in s_list)
```


**# 2.Review**
> 阅读并点评至少一篇英文技术文章 
Kombu 的文档比较简单，读完了
[Kombu 的文档](http://kombu.readthedocs.io)

另外还有一篇 PEP-205 ，正在阅读中。

**# 3.Tip**
> 学习至少一个技术技巧  
* 使用了 ansible 非常好用
* Linux 系统优化（上下文切换）

**# 4.Share**
> 分享一篇有观点和思考的技术文章  
本周输出 （没有整理，我还是直接贴在这里吧）：

# Python 连接 AMQP MQ 的客户端
## 可选项
在 RabbitMQ 的官网中，推荐了 pika 作为 Python 的客户端。毕竟是官网推荐的，当然可以使用，正常使用场景，分为三种：
1. 只是想写一个 `hello world` 的简单 demo 
2. 要快速、安全、稳定地用起来，过滤掉很多不必要的细节
3. 财大气粗，先把这个 pika 封装好，设计好 api, 供上层调用
4. 超级富豪，自己从零写一个客户端

对于 1，用什么都无所谓，反正都是玩玩。
对于 2，用 pika 显然是不行的，过于底层了，缺少必要的封装和工具。
对于 3，有钱任性。
对于 4，献上膝盖。
那么我们先看看 3，有哪些底层框架可供选择吧。
## 比较底层的 AMQP 客户端
RabbitMQ 网站上列出了几个，其实看了一圈，也就 pika 和 Celery 比较靠谱了。不过这里 Celery 并不是一个专门的客户端，他所依赖的 Kombu 和 librabbitmq 才是。其中，librabbitmq 是跟 pika 对等的关系。
其实 librabbitmq 是 C 写的 RabbitMQ 客户端，用 Python 包装了一下。
所以，如果要选择底层的客户端，那么这两个都可以考虑。其他的，可以看看他们的 Github 主页，看看能否满足自己的要求。
## 封装一下
Kombu 就是基于 librabbitmq 所做的封装。除了很多工具外，主要封装出了这么几个类：
- Connection (Channel, Transport)
- Producer, Consumer
- Serialization
基本上满足了快速使用的基本需求。而且 Kombu 作为上层封装，amqp 只是其中的一个 transport, 可以被替换成 redis, in-memory 等，具体可以看看 [Transport Comparison]
## Kombu 快速开始
最快的开始，当然是什么都不依赖啦，一下子体验 producer 和 consumer 。当然由于过于简陋，可能什么都感受不到(⊙﹏⊙)b
from kombu import Connection
# 往队列里面塞消息
with Connection('memory:///') as conn:
    with conn.SimpleQueue('nothing') as queue:
        queue.put({'hello': 'world'})

# 从队列里面取消息，打印一下
with Connection('memory:///') as conn:
    with conn.SimpleQueue('nothing') as queue:
        message = queue.get(block=True, timeout=10)
        message.ack()
        print(message.payload)
直接用内存作为 transport, 上面往队列里面生产一点消息，下面从队列里面消费消息。
## 生产者，消费者
上面的示例，有点过于简单了，让人感到一脸懵逼，作为严肃的程序员，我们还是想要一套完整的演示的：
首先，有一个生产者，产生消息
其次，有一个消费者，消费消息
另外，每次使用完都要记得关闭，所以直接使用 `with` 上下文即可。在 kombu 中提供了示例代码，可以快速的依次看完:
1. `hello_publisher.py` and `hello_consumer.py`
2. `simple_send.py` and `simple_receive.py`
3. `complete_send.py` and `complete_receive.py`
就可以开始写代码了，当然，前面的 1, 2 都是供理解用的，可以直接按照 3 中的来。
