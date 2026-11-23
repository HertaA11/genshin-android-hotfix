

# 原神国服安卓目前有效的热更新配置

本仓库保存原神国服安卓客户端的 `query_cur_region` 响应中的 `RegionInfo` 配置，
每个可用版本分支对应一个 JSON 文件。

## 版本清单

| 版本 | 文件 |
| --- | --- |
| 1.0.0 | `CNRELAndroid1.0.0.json` |
| 1.1.0 | `CNRELAndroid1.1.0.json` |
| 1.2.0 | `CNRELAndroid1.2.0.json` |
| 1.3.0 | `CNRELAndroid1.3.0.json` |
| 1.4.0 | `CNRELAndroid1.4.0.json` |
| 1.5.0 | `CNRELAndroid1.5.0.json` |
| 1.6.0 | `CNRELAndroid1.6.0.json` |
| 2.0.0 | `CNRELAndroid2.0.0.json` |
| 2.1.0 | `CNRELAndroid2.1.0.json` |
| 2.2.0 | `CNRELAndroid2.2.0.json` |
| 2.3.0 | `CNRELAndroid2.3.0.json` |
| 2.4.0 | `CNRELAndroid2.4.0.json` |
| 2.5.0 | `CNRELAndroid2.5.0.json` |
| 2.6.0 | `CNRELAndroid2.6.0.json` |
| 2.7.0 | `CNRELAndroid2.7.0.json` |
| 2.8.0 | `CNRELAndroid2.8.0.json` |
| 3.0.0 | `CNRELAndroid3.0.0.json` |
| 3.1.0 | `CNRELAndroid3.1.0.json` |
| 3.3.0 | `CNRELAndroid3.3.0.json` |
| 3.5.0 | `CNRELAndroid3.5.0.json` |
| 3.6.0 | `CNRELAndroid3.6.0.json` |
| 3.7.0 | `CNRELAndroid3.7.0.json` |
| 3.8.0 | `CNRELAndroid3.8.0.json` |
| 4.0.0 | `CNRELAndroid4.0.0.json` |
| 4.1.0 | `CNRELAndroid4.1.0.json` |
| 4.2.0 | `CNRELAndroid4.2.0.json` |
| 4.3.0 | `CNRELAndroid4.3.0.json` |
| 4.4.0 | `CNRELAndroid4.4.0.json` |
| 4.5.0 | `CNRELAndroid4.5.0.json` |
| 4.6.0 | `CNRELAndroid4.6.0.json` |
| 4.7.0 | `CNRELAndroid4.7.0.json` |
| 4.8.0 | `CNRELAndroid4.8.0.json` |
| 5.0.0 | `CNRELAndroid5.0.0.json` |
| 5.1.0 | `CNRELAndroid5.1.0.json` |
| 5.2.0 | `CNRELAndroid5.2.0.json` |
| 5.3.0 | `CNRELAndroid5.3.0.json` |
| 5.4.0 | `CNRELAndroid5.4.0.json` |
| 5.5.0 | `CNRELAndroid5.5.0.json` |
| 5.6.0 | `CNRELAndroid5.6.0.json` |
| 5.7.0 | `CNRELAndroid5.7.0.json` |
| 5.8.0 | `CNRELAndroid5.8.0.json` |
| 6.0.0 | `CNRELAndroid6.0.0.json` |
| 6.1.0 | `CNRELAndroid6.1.0.json` |
| 6.2.0 | `CNRELAndroid6.2.0.json` |
| 6.3.0 | `CNRELAndroid6.3.0.json` |
| 6.4.0 | `CNRELAndroid6.4.0.json` |
| 6.5.0 | `CNRELAndroid6.5.0.json` |
| 6.6.0 | `CNRELAndroid6.6.0.json` |
| 6.7.0 | `CNRELAndroid6.7.0.json` |
| 7.0.0 | `CNRELAndroid7.0.0.json` |
| 7.1.0 | `CNRELAndroid7.1.0.json` |
| 7.2.0 | `CNRELAndroid7.2.0.json` |

未列出 3.2.0 和 3.4.0，因为官方 CDN 清单已不可用，对应配置文件已删除

## 文件包含的内容

每个文件都是完整的 `query_cur_region` 响应：

```json
{
  "RegionInfo": {
    "ClientDataMd5": "...",
    "ResourceUrl": "https://autopatchcn.yuanshen.com/client_game_res/<分支>",
    "NextResourceUrl": "...",
    "ResourceUrlBak": "<分支>",
    "DataUrl": "https://autopatchcn.yuanshen.com/client_design_data/<分支>",
    "NextResVersionConfig": {
      "Md5": "0",
      "ReleaseTotalSize": "0",
      "Branch": "<分支>"
    },
    "ResVersionConfig": {
      "Version": "<资源版本>",
      "Md5": "{...res_versions_external / medium / streaming / base_revision / patch_node_versions...}",
      "ReleaseTotalSize": "0",
      "VersionSuffix": "...",
      "Branch": "<分支>"
    },
    "GameBiz": "hk4e_cn",
    "AreaType": "CN",
    "ClientDataVersion": "<数据版本>",
    "ClientSilenceDataVersion": "<静默数据版本>",
    "ClientVersionSuffix": "...",
    "ClientSilenceVersionSuffix": "...",
    "UseGateserverDomainName": false,
    "GateserverIp": "...",
    "GateserverPort": 22101,
    "PrivacyPolicyUrl": "...",
    "CdkeyUrl": "..."
  },
  "Retcode": 0
}
```

## 字段说明

- `ClientVersionSuffix` / `ClientSilenceVersionSuffix`：客户端版本后缀。
- `ResVersionConfig.Version` / `VersionSuffix`：资源 revision 和后缀。
- `ClientDataMd5` / `ResVersionConfig.Md5`：数据与资源清单校验信息。
- `ResourceUrl` / `DataUrl`：对应版本分支的官方 CDN 地址。
