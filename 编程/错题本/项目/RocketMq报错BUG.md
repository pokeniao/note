---
日期: 2024-03-23
tags:
  - bug
---
表示心态炸裂。这几个问题弄了至少7个小时，才找到原因，包括寻找是否异步同步可以在同一个线程运行等等怀疑。最后得出结果都不是，就是Mqbug。我哭了😭
# 使用MQ遇到重启或debug循环出现同一条消息
可能原因：代码发生错误，Mq遇到错误会，一直请求重试。
后来发现，重启mq又正常了，并没有重复循环
解决：1. 重启mq 2. 把错误的全部消费，通过代码return null.全部通过正确后重启mq


# 明明发送了10条，但是只处理了4-5条
可能原因：虽然同一个组，但不同主题。但是他发送的时候，还是把消息发到了同一个组的不同主题下
解决：一个组一个主题。只需要主题和发送者对应即可 ^1821fd

# 明明代码正确，却没有消费
解决：更换主题和分组名，重启mq
可能原因：主题堵塞或者其他某些不知名原因。

# 不要写嵌套的消息