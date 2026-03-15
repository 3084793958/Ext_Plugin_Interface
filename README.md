# Ext_Plugin_Interface
适用于Easy_Desktop插件的接口,修改自dde-dock插件接口,增加了一些接口用于与Easy_Desktop交互.License:LGPL3.0

# 使用方法
1.将该项目的C++文件放到插件项目中,并引用

2.在<插件名>.json文件中添加 "Ext_Plugin": ""

模板如下

```json
{
    "api": "1.1.1",
    "Ext_Plugin": ""
}

```

# 自定类介绍
## 1.P_Version
用于标记Interface的版本,在Easy_Desktop判断版本后执行 在该版本已定义的函数
## 2.P_Sender
用于插件向Easy_Desktop发送信息

```c++
class P_Sender : public QObject
{
    Q_OBJECT
public:
    explicit P_Sender(QObject *parent = nullptr, bool m_allow_Send_Data = true, bool m_allow_Send_Ptr = true);
    void Send();                         //正常发送
    void Send_Data(QVariant var);        //带数据发送
    void Send_Ptr(void *ptr);            //带指针发送
    bool allow_Send_Data = true;        //允许带数据发送
    bool allow_Send_Ptr = true;         //允许带指针发送
signals:
    void sig_Send();
    void sig_Send_Data(QVariant var);
    void sig_Send_Ptr(void *ptr);
};
```

### 为什么在pluginproxyinterface.h中添加定义?
若新版本插件被旧版本Easy_Desktop载入,并且插件调用新的pluginproxyinterface.h中的功能,Easy_Desktop会崩溃
