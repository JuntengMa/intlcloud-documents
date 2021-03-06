## API 密钥

API 密钥是用户访问腾讯云 API 进行身份验证时需要用到的安全凭证，由 SecretId 和 SecretKey 组成。一个用户帐号可以创建多个云 API 密钥，若用户还没有云 API 密钥，则需要在 [云 API 密钥控制台](https://intl.console.cloud.tencent.com/capi) 新建，否则无法调用云 API 接口。

- SecretId 用于标识 API 调用者身份。
- SecretKey 用于加密签名字符串和服务器端验证签名字符串的密钥。

## 地域

地域（Region），指日志服务 CLS 的数据中心所在地域。用户可以根据延时、费用等综合因素选择日志服务的地域。建议根据您的业务场景选择就近地域的日志服务。

## 机器组

机器组是一组需要采集日志的机器列表，一个日志主题可以绑定多个机器组，一个机器组也可以被多个日志主题绑定。

## 键值索引

键值索引（Key-Value Index）是检索分析的另一种索引类型，键值索引将原始日志拆分成多个 Key-Value 对，每组 Key-Value 对需要定义唯一的 Key 名称，键值索引的查询语法是 Key：Value。

## LogListener

日志服务 CLS 提供自研的采集 Agent（LogListener），成功安装的 LogListener 将与日志服务保持长久的心跳连接。

## 全文索引

全文索引（Full-Text Index）是查询检索的一种索引类型，全文索引将原始日志拆分成多个分词，检索日志时基于分词进行查询，输入关键词即可查询。


## 日志集

日志集（Logset）是日志服务 CLS 提供的项目管理逻辑概念，可以将一个日志集对应一个项目。

## 日志主题

日志主题（Topic）是日志服务 CLS 提供的基本管理单元，一个日志主题对应一个应用或者服务。日志主题 Topic 是 CLS 的最小管理单元，采集、索引、投递等配置围绕 Topic 进行。一个日志集可以包含多个日志主题。


