<p align="center">
  <h1 align="center">Flink 流数据分析工具</h1>
  <p align="center">
    <a href="README.md"><strong>English</strong></a> | <strong>简体中文</strong>
  </p>
</p>

## 目录

- [仓库简介](#项目介绍)
- [前置条件](#前置条件)
- [镜像说明](#镜像说明)
- [获取帮助](#获取帮助)
- [如何贡献](#如何贡献)

## 项目介绍
‌[Apache Flink‌](https://github.com/apache/flink) 是一个开源的分布式处理引擎，主要用于对无界和有界数据流进行有状态的计算。它能够在内存中以高速处理数据，并且能够扩展到任意规模。

**核心特性：**
1. ‌批流一体化‌：Flink 支持批处理和流处理，使得开发者可以使用同一套系统处理不同类型的计算任务。批处理适用于有界数据集的处理，而流处理适用于无界数据流的处理‌。
2. ‌状态管理‌：Flink 提供了丰富的状态管理 API，包括 ValueState、ListState、MapState 等，帮助开发者更容易地管理复杂的状态‌。
3. ‌事件时间处理‌：Flink 支持基于事件时间的数据处理，能够容忍数据的延迟和乱序，确保数据的准确性‌。
4. ‌高可用性和容错机制‌：Flink 通过 Checkpoint 机制提供数据一致性保障，确保在故障发生时能够恢复状态，保证计算的正确性‌。

**架构设计：**

![](./images/img.png)

![](./images/img2.png)

本项目提供的开源镜像商品 [**`Flink-流数据分析工具`**](https://marketplace.huaweicloud.com/contents/992480da-64a3-4ba8-90cb-686d1832e96a#productid=OFFI1111485128289529856)，已预先安装 Flink 软件及其相关运行环境，并提供部署模板。快来参照使用指南，轻松开启“开箱即用”的高效体验吧。

> **系统要求如下：**
> - CPU: 2GHz 或更高
> - RAM: 4GB 或更大
> - Disk: 至少 40GB

## 前置条件
[注册华为账号并开通华为云](https://support.huaweicloud.com/usermanual-account/account_id_001.html)

## 镜像说明

| 镜像规格                                                                                                                     | 特性说明 | 备注 |
|--------------------------------------------------------------------------------------------------------------------------| --- | --- |
| [Flink-1.13.0-kunpeng](https://github.com/HuaweiCloudDeveloper/flink-image/tree/Flink-1.13.0-kunpeng) | 基于 鲲鹏服务器 + Huawei Cloud EulerOS 2.0 64bit 安装部署 |  |
| [Flink-1.17.0-kunpeng](https://github.com/HuaweiCloudDeveloper/flink-image/tree/Flink-1.17.0-kunpeng) | 基于 鲲鹏服务器 + Huawei Cloud EulerOS 2.0 64bit 安装部署，新增对 GaussDB 实时写入与实时采集 |  |

## 获取帮助
- 更多问题可通过 [issue](https://github.com/HuaweiCloudDeveloper/flink-image/issues) 或 华为云云商店指定商品的服务支持 与我们取得联系
- 其他开源镜像可看 [open-source-image-repos](https://github.com/HuaweiCloudDeveloper/open-source-image-repos)

## 如何贡献
- Fork 此存储库并提交合并请求
- 基于您的开源镜像信息同步更新 README.md
