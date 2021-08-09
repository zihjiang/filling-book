

# Filling

Filling, 如其名, 致力于填充你的各种存储,  是一个`非常易用`，`高性能`、支持`实时流式`和`离线批处理`的`海量数据`处理产品，架构于 `Apache Flink`之上。

Filling是一个基于[Flink](https://flink.apache.org/)的流式数据处理工具, Filling将每条数据以表的形式进行抽象, 后续还会支持托拉拽式编程的流处理引擎。

Filling组件分为数据源(source)、算子(transfrom) 和 输出(sink)三种

------

## 处理流程图

Filling的简单处理流程图如下图所示：

```Mermaid
graph TD
source[source] --> transfrom[transfrom]
transfrom --> sink[sink]
```

复杂一点的处理流程:

``` Mermaid
graph TD
source-kafka(日志数据-kakfa) --> transfrom01(join)
source-jdbc(cmdb数据-mysql) --> transfrom01(join)
transfrom01(join) --> transfrom02(过滤掉错误日志)
transfrom02(过滤掉错误日志) --> transfrom03(解析字段)
transfrom03 --> sink-kafka[kafka]
transfrom03 --> sink-jdbc[jdbc]
```

简述各组件的工作原理：

- Filling-web：// TODO。

- Filling-service：// TODO。

- Filling-cluster：// TODO。

  > **多种集群部署方式的支持**
  >
  > 目前Filling-cluster主要对接以standalone cluster或on yarn模式运行的flink cluster，分别需要提供虚拟机或Hadoop-Yarn计算资源。这两种模式和Filling-cluster之间的通信接口是相同的，仅在启动集群方式上有所区别。
  >
  > 将来，Filling-cluster可以扩展为对接更多种类的集群，例如支持以appliation mode部署在yarn上的flink任务提交方式等。

- Filling-core：Filling的核心流处理程序包，运行在flink集群环境下或在本地java环境以测试模式运行。Filling-core可以通过提供的url或配置文件读取处理任务内容并执行。通过Filling-web/Filling-service提交的任务将会通过url获取处理任务信息；用户也可以绕过上述服务直接提交Filling-core任务到flink集群上运行，此时可以指定url，也可以指定配置文件地址通过文件启动处理任务。

Filling，即基于Flink的流式数据处理工具，预期将拥有如下特性：

- 核心模块基于Flink实现，实现精确一次语义，同时提供高性能、断点恢复等支持
- 核心数据抽象为table，操作过程近似对table进行操作，更加贴近数据摄取和清洗场景的用户使用习惯
- 实现诸如Kafka、File、JDBC、ES等常见输入输出，支持Add、Drop, Rename, 等常用转换逻辑，还支持flink所有函数, 支持流join和窗口统计，并支持sql等脚本对数据自定义操作
- 前端实现对处理流程的可视化编辑，通过对处理单元的拖拽、连接、属性配置完成整个处理流程的设置过程，一般无需编写代码
- 支持从随版本发布更新的模板创建新的处理任务，支持处理任务文件上传/下载
- 提供对于服务自身和运行流程任务的监控
- 流式处理任务运行环境支持裸机部署或对接Hadoop平台及其部分商业版本

预期在将来，Filling可以逐步满足现场实施交付从多种来源，特别是Kafka来源实时接入数据，对其进行简单清洗、格式整理和可能的统计接入其他产品的需求。
