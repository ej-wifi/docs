## 模块划分
根据功能，分以下几个功能模块。

* uart 收发模块，该部分主要负责从 uart 口读取数据。定义为 uart_recv
* uart 数据处理模块。定义为 uart_mgr
* 消息中心处理模块。主要负责消息分发给不同的模块。 cm
* mqtt 模块。该模块主要负责 mqtt 通讯。 定义为 mqtt_proc
* udp server 模块。主要处理局域网的数据查询。 udp_server
* tcp server 模块。用于 ap 配网使用。 tcp_server
* smart config 模块。主要用于配网使用。 smart_config
* OTA 升级。包括 wifi 自身升级以及，设备端升级。ota_proc
* 网络状态模块。network_mgr
* 主模块。主要是启动其他模块。main_proc


## 模块之间通讯方式

使用 message queue 方式。thread 同步使用 semaphore 方式实现。 在定义消息类型的时候，通过消息头，以及消息体。

## 模块启动顺序

在 WiFi 模块上电后，进行系统初始化后，进入用户自定义 thread 中， 同时启动 uart_recv , uart_mgr， 以及 network_mgr 三个 thread 。
在 network_mgr 中，根据网络状况，确定是否启动 mqtt_proc，tcp_server，udp_server 。
