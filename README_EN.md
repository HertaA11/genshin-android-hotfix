# Currently Available Genshin Impact CN Android Hotfix Configurations

[中文](README.md) | English

This repository stores the `RegionInfo` configurations from the `query_cur_region` responses for the Genshin Impact CN Android client.
Each available version branch has a corresponding JSON file.

## Version List

| Version | File |
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

Versions 3.2.0 and 3.4.0 are not listed because the official CDN manifests are no longer available and the corresponding configuration files have been removed

## File Contents

Each file contains a complete `query_cur_region` response:

```json
{
  "RegionInfo": {
    "ClientDataMd5": "...",
    "ResourceUrl": "https://autopatchcn.yuanshen.com/client_game_res/<branch>",
    "NextResourceUrl": "...",
    "ResourceUrlBak": "<branch>",
    "DataUrl": "https://autopatchcn.yuanshen.com/client_design_data/<branch>",
    "NextResVersionConfig": {
      "Md5": "0",
      "ReleaseTotalSize": "0",
      "Branch": "<branch>"
    },
    "ResVersionConfig": {
      "Version": "<resource version>",
      "Md5": "{...res_versions_external / medium / streaming / base_revision / patch_node_versions...}",
      "ReleaseTotalSize": "0",
      "VersionSuffix": "...",
      "Branch": "<branch>"
    },
    "GameBiz": "hk4e_cn",
    "AreaType": "CN",
    "ClientDataVersion": "<data version>",
    "ClientSilenceDataVersion": "<silence data version>",
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

## Field Reference

- `ClientVersionSuffix` / `ClientSilenceVersionSuffix`: client version suffixes.
- `ResVersionConfig.Version` / `VersionSuffix`: resource revision and suffix.
- `ClientDataMd5` / `ResVersionConfig.Md5`: data and resource manifest verification information.
- `ResourceUrl` / `DataUrl`: official CDN addresses for the corresponding version branch.
