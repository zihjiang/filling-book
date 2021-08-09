# 组件

组件是计算任务DAG的组成单位，分为Source，Transformer，Sink三类。

Source类组件负责从不同的数据源中获取数据，生成一个table。

Transformer类组件可以有一个或多个输入、输出，根据用户配置的规则对table作不同的处理。

Sink类组件负责将table中的数据写入到不同的数据库、文件仓库或消息队列中。

详细的组件功能、属性介绍参见下一章：组件
