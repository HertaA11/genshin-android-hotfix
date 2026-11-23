# Genshin Impact CN Android Hotfix

Region configs (`query_cur_region` responses, `RegionInfo` block) for the CN Android client
(`hk4e_cn`), one file per version branch. Currently covers 4.0.0 through 7.2.0 — 29 versions.

## Versions

| Version | File | Gate server |
| --- | --- | --- |
| 4.0.0 | `CNRELAndroid4.0.0.json` | 47.116.110.112:22101 |
| 4.1.0 | `CNRELAndroid4.1.0.json` | 47.116.110.112:22101 |
| 4.2.0 | `CNRELAndroid4.2.0.json` | 47.101.203.7:22101 |
| 4.3.0 | `CNRELAndroid4.3.0.json` | 47.103.29.152:22101 |
| 4.4.0 | `CNRELAndroid4.4.0.json` | 47.103.23.92:22102 |
| 4.5.0 | `CNRELAndroid4.5.0.json` | 47.116.110.112:22101 |
| 4.6.0 | `CNRELAndroid4.6.0.json` | 47.116.110.112:22101 |
| 4.7.0 | `CNRELAndroid4.7.0.json` | 47.116.110.112:22101 |
| 4.8.0 | `CNRELAndroid4.8.0.json` | 47.116.110.112:22101 |
| 5.0.0 | `CNRELAndroid5.0.0.json` | 47.116.110.112:22101 |
| 5.1.0 | `CNRELAndroid5.1.0.json` | 47.116.110.112:22101 |
| 5.2.0 | `CNRELAndroid5.2.0.json` | 47.116.110.112:22101 |
| 5.3.0 | `CNRELAndroid5.3.0.json` | 47.116.110.112:22101 |
| 5.4.0 | `CNRELAndroid5.4.0.json` | 47.116.110.112:22101 |
| 5.5.0 | `CNRELAndroid5.5.0.json` | 47.116.110.112:22101 |
| 5.6.0 | `CNRELAndroid5.6.0.json` | 47.116.110.112:22101 |
| 5.7.0 | `CNRELAndroid5.7.0.json` | 47.116.110.112:22101 |
| 5.8.0 | `CNRELAndroid5.8.0.json` | 47.116.110.112:22101 |
| 6.0.0 | `CNRELAndroid6.0.0.json` | 47.116.110.112:22101 |
| 6.1.0 | `CNRELAndroid6.1.0.json` | 47.116.110.112:22101 |
| 6.2.0 | `CNRELAndroid6.2.0.json` | 47.116.110.112:22101 |
| 6.3.0 | `CNRELAndroid6.3.0.json` | 47.116.110.112:22101 |
| 6.4.0 | `CNRELAndroid6.4.0.json` | 47.116.110.112:22101 |
| 6.5.0 | `CNRELAndroid6.5.0.json` | 47.116.110.112:22101 |
| 6.6.0 | `CNRELAndroid6.6.0.json` | 47.100.117.206:22102 |
| 6.7.0 | `CNRELAndroid6.7.0.json` | 47.116.110.112:22101 |
| 7.0.0 | `CNRELAndroid7.0.0.json` | 47.103.30.226:22101 |
| 7.1.0 | `CNRELAndroid7.1.0.json` | 47.116.110.112:22101 |
| 7.2.0 | `CNRELAndroid7.2.0.json` | 47.116.110.112:22101 |

4.2.0, 4.3.0, 4.4.0, 6.6.0 and 7.0.0 were served from a different gate host than the rest; the
address in each file is the one that version actually returned.

## Updates

- 2026-11-23 — added the 4.x series: 4.0.0 through 4.8.0.
- 2026-11-23 — added the 5.x series: 5.0.0, 5.1.0, 5.2.0, 5.3.0, 5.4.0, 5.5.0, 5.6.0, 5.7.0,
  5.8.0.

## What is in a file

Each file is a full `query_cur_region` response:

```json
{
  "RegionInfo": {
    "ClientDataMd5": "...",
    "ResourceUrl": "https://autopatchcn.yuanshen.com/client_game_res/<branch>",
    "NextResourceUrl": "...",
    "ResourceUrlBak": "<branch>",
    "DataUrl": "https://autopatchcn.yuanshen.com/client_design_data/<branch>",
    "NextResVersionConfig": { "Md5": "0", "ReleaseTotalSize": "0", "Branch": "<branch>" },
    "ResVersionConfig": {
      "Version": <resource version>,
      "Md5": "{...res_versions_external / medium / streaming / base_revision / patch_node_versions...}",
      "VersionSuffix": "...",
      "Branch": "<branch>"
    },
    "GameBiz": "hk4e_cn",
    "AreaType": "CN",
    "ClientDataVersion": <int>,
    "ClientSilenceDataVersion": <int>,
    "ClientVersionSuffix": "...",
    "ClientSilenceVersionSuffix": "...",
    "UseGateserverDomainName": false,
    "GateserverIp": "47.116.110.112",
    "GateserverPort": 22101,
    "PrivacyPolicyUrl": "...",
    "CdkeyUrl": "..."
  },
  "Retcode": 0
}
```

Field notes:

- `ClientVersionSuffix` / `ClientSilenceVersionSuffix` — client build hashes. A client whose
  `client_versions` entry does not match will be told to update.
- `ResVersionConfig.Version` + `VersionSuffix` — resource version. Must match the client's
  `res_versions` manifest, otherwise the launcher re-downloads resources.
- `ClientDataMd5` / `ResVersionConfig.Md5` — manifests of the version lists themselves
  (`data_versions`, `res_versions_*`, `base_revision`, `patch_node_versions`).
- `ResourceUrl` / `DataUrl` — official CDN, kept per branch so each config points at its own
  version's assets.
- `GateserverIp` / `GateserverPort` — gate the client connects to after dispatch.

## Usage

These files are reference captures, useful when pointing a modified client at your own server:
replace `GateserverIp` / `GateserverPort` with your server and keep the rest of the branch's
values so the client does not try to update.

Values were captured from the live CN service; the resource and design-data URLs stay on
`autopatchcn.yuanshen.com`.
