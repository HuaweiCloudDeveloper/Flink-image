# Flink 使用指南

# 商品链接

[Flink-流数据分析工具](https://marketplace.huaweicloud.com/contents/992480da-64a3-4ba8-90cb-686d1832e96a#productid=OFFI1111485128289529856)

# 商品说明

Apache Flink 是一个开源的分布式流处理框架，专为大规模数据处理设计，支持流处理和批处理一体化。它能够在无界和有界数据流上进行有状态计算，具有高吞吐量、低延迟的特性，广泛应用于实时数据处理场景。

本商品通过 鲲鹏服务器 + Huawei Cloud EulerOS 2.0 64bit 进行安装部署。

# 商品购买

您可以在云商店搜索 **Flink-流数据分析工具**。

其中，地域、规格、推荐配置使用默认，购买方式根据您的需求选择按需/按月/按年，短期使用推荐按需，长期使用推荐按月/按年，确认配置后点击“立即购买”。

## 商品支持自定义 ECS 购买，具体见 [ECS 控制台配置](#ECS控制台配置)

## 使用 RFS 模板直接部署

1. 选择 **模板配置开通**，点击 **下一步**。

![](images/img13.png)

![](images/img.png)

2. 必填项填写后，点击 **下一步**。

![](images/img2.png)

![](images/img3.png)

3. 创建直接计划后，点击 **确定**。

![](images/img4.png)

4. 点击 **部署**。

![](images/img5.png)

5. 如下图出现 `Apply required resource success` 即为资源创建完成。

![](images/img6.png)

# 商品资源配置

商品支持 **ECS 控制台配置**，下面对资源配置的方式进行介绍。

## <a id="ECS控制台配置"></a>ECS 控制台配置

### 准备工作

在使用ECS控制台配置前，需要您提前配置好 **安全组规则**。

> **安全组规则的配置如下：**
> - 入方向规则放通端口 `8081`，**源地址内必须包含您的客户端 ip**，否则无法访问
> - 入方向规则放通 CloudShell 连接实例使用的端口 `22`，以便在控制台登录调试
> - 出方向规则一键放通

### 创建ECS

前提工作准备好后，选择 ECS 控制台配置跳转到购买 ECS 页面，ECS 资源的配置如下图所示：

![](images/img7.png)

![](images/img8.png)

![](images/img9.png)

> **值得注意的是：**
> - VPC 您可以自行创建
> - 安全组选择 [**准备工作**](#准备工作) 中配置的安全组；
> - 弹性公网IP选择现在购买，推荐选择“按流量计费”，带宽大小可设置为5Mbit/s；
> - 高级配置需要在高级选项支持注入自定义数据，所以登录凭证不能选择“密码”，选择创建后设置；
> - 其余默认或按规则填写即可。

# 商品使用

## Flink 使用

### 批处理模式（处理静态文件）

1. 准备输入文件 `input.txt` 放入 `tmp` 目录下，内容示例： 
```shell
hello world
hello flink
flink is powerful
```

2. 提交作业 
```shell
cd /opt/flink-1.13.0
./bin/flink run examples/batch/CwordCount.jar \
  --input /tmp/input.txt \
  --output /tmp/output_batch.txt
```

3. 查看结果

![](images/img10.png)

### 流处理模式（实时Socket数据源）

1. 启动 `Netcat` 数据源，执行：
```shell
nc -lk 9999
```

2. 新开一个终端，运行流处理 `WordCount` 作业。
```shell
cd /opt/flink-1.13.0
./bin/flink run examples/streaming/SocketWindowWordCount.jar \
  --port 9999
```

3. 发送测试数据。

在 `Netcat` 终端输入数据（每行一个句子）：

![](images/img11.png)

4. 观察结果。

在 `log` 目录下找到输出文件，查看结果：

![](images/img12.png)
