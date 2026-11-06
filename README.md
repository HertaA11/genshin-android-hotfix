# 原神 安卓端热更新配置（CN）

国服 Android 客户端（`hk4e_cn` / `CNRELAndroid`）的热更新配置快照，结构对应 dispatch 服务 `query_security_file` 返回的 `RegionInfo`。

客户端拿到这份配置后，才知道去哪个 CDN 分支、按哪个版本号和后缀下载资源。做私服 / 抓包分析 / 资源版本对照时会用到。

## 文件

命名规则：`CNRELAndroid<版本号>.json`

- `CNREL` = CN Release
- `Android` = 平台

| 文件 | 资源分支 | 资源版本 | 资源后缀 | 客户端数据版本 | 客户端后缀 |
|---|---|---|---|---|---|
| `CNRELAndroid7.0.0.json` | `7.0_live` | 47482070 | `e637da0f75` | 47579390 | `b92051e672` |
| `CNRELAndroid7.1.0.json` | `7.1_live` | 48379043 | `cc8f4bb04d` | 48533839 | `0f4d11ebee` |
| `CNRELAndroid7.2.0.json` | `7.2_live` | 49086080 | `1c55d912bf` | 49291486 | `c25ba650a6` |

## 字段说明

| 字段 | 含义 |
|---|---|
| `ClientDataMd5` | 客户端数据清单列表，每行一个 JSON：`data_versions`、`data_versions_medium` |
| `ResVersionConfig.Md5` | 资源清单列表，每行一个 JSON：`res_versions_external` / `_medium` / `_streaming`、`base_revision`、`patch_node_versions`，部分版本还有 `audio_diff_versions_<新>-<旧>` |
| `ResourceUrl` | 资源 CDN 根：`https://autopatchcn.yuanshen.com/client_game_res/<分支>` |
| `DataUrl` | 设计数据 CDN 根：`https://autopatchcn.yuanshen.com/client_design_data/<分支>` |
| `ResVersionConfig.Version` / `VersionSuffix` | 资源版本号与后缀，实际下载路径是 `output_<Version>_<VersionSuffix>` |
| `ClientDataVersion` / `ClientVersionSuffix` | 客户端数据版本号与后缀，路径同上 |
| `ClientSilenceDataVersion` / `ClientSilenceVersionSuffix` | 静默（预下载）数据版本；与客户端版本相同时复用同一个 `output_` 目录 |
| `GateserverIp` / `GateserverPort` | 官方网关地址，随版本变化，私服一般用不到 |
| `Retcode` | 0 = 正常 |

清单行里的三个值：

- `md5` —— 文件的标准 MD5
- `hash` —— **xxHash64（seed = 0）**，16 位小写十六进制
- `fileSize` —— 字节数

下载地址拼法：

```
{ResourceUrl}/output_{Version}_{VersionSuffix}/client/Android/{remoteName}
{DataUrl}/output_{ClientDataVersion}_{ClientVersionSuffix}/client/General/AssetBundles/{remoteName}
```

## 数据来源

1. 客户端启动时请求 `https://dispatchcnglobal.yuanshen.com/query_region_list?version=CNRELAndroid<版本>&lang=2&platform=2&binary=1&channel_id=1&sub_channel_id=1`
2. 响应是 protobuf，含 `client_secret_key`（Ec2b 格式）与 `client_custom_config`
3. 用 EC2B 解出 custom config，其中 `regionConfig` 指向 `query_security_file?file_key=CNRELAndroid<版本>`
4. 该接口返回 RSA 加密内容，客户端私钥不可得，因此改为按客户端实际请求的 CDN 路径重建，并对每个清单文件重新计算 `md5` / `hash` / `fileSize`

`hash` 的算法用 7.1 的 `data_versions` 反向验证过：md5 `fe1421dbbc78bf6092705f8e2f1ef5e3`、hash `67d3fef07e68ada9` 均能对上。

## 注意

- 不同版本的结构略有差异，例如 7.0.0 的 `ResVersionConfig` 多一个 `Relogin` 字段，`ClientDataMd5` 用 `\n` 分隔；7.1 / 7.2 用 `\r\n`
- 7.2 的 CDN 上不存在 `audio_diff_versions_*`，故未写入
- `GateserverIp` 是抓取时的值，官方会轮换；不影响资源下载

## 声明

配置数据来自官方公开 CDN 与客户端自身请求，资源与游戏内容的版权归米哈游所有。本仓库仅用于版本对照与技术研究。
