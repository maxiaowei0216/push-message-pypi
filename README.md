# Push message

整合多种方式向用户推送消息。

# 支持的方式

- [x] QYWX(企业微信)
- [ ] webhook

逐步增加中...

# 使用方法

## QYWX

使用企业微信推送消息，需要获取corpid和secret，获取方式请参考：[https://developer.work.weixin.qq.com/document/path/90665](https://developer.work.weixin.qq.com/document/path/90665)

corpid和secret可以通过以下两种方式指定：

- 环境变量`QYWX_CORP_ID`和`QYWX_CORP_SECRET`
- 实例化时传入参数`id`和`secret`

```python
from push_message.qywx import QYWX, MsgType

# 通过参数传递id和secret
qy = QYWX(id='your_id', secret='your_secret')
# 通过环境变量的方式
qy_env = QYWX()
```

### 发送消息

`push(msg,msg_type,**kwargs)`

- `msg`：消息内容
- `msg_type`：消息类型

当前支持的消息类型有：

- `MsgType.TEXT`：文本消息

各类消息需要的参数可参考：[https://developer.work.weixin.qq.com/document/path/90236](https://developer.work.weixin.qq.com/document/path/90236)

#### 文本消息

`push(content,MsgType.TEXT,to_user='',to_party='',to_tag='',agent_id=1)`

| 参数       | 类型  | 是否必须 | 说明                                                       |
|----------|:---:|:----:|----------------------------------------------------------|
| to_user  | str |  否   | 接收消息的成员，成员ID列表（多个接收者用`&#124;`分隔）。指定为`@all`则向该企业应用的全部成员发送 |
| to_party | str |  否   | 接收消息的部门，部门ID列表。当`to_user`为`@all`时忽略本参数                   |
| to_tag   | str |  否   | 接收消息的标签，标签ID列表。当`to_user`为`@all`时忽略本参数                   |
| agent_id | int |  是   | 企业应用的id                                                  |

