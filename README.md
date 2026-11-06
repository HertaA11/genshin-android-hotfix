# Genshin Impact CN — Android Hotfix Configs

Hot-update configuration snapshots for the Chinese Android client (`hk4e_cn` / `CNRELAndroid`).

The structure matches the `RegionInfo` payload returned by the dispatch endpoint `query_security_file`. With it, the client knows which CDN branch to use and which version / suffix to download resources from.

Useful for private-server work, traffic analysis, and version comparison.

## Files

Naming: `CNRELAndroid<version>.json`

- `CNREL` — CN release
- `Android` — platform

| File | Resource branch | Res version | Res suffix | Client data version | Client suffix |
|---|---|---|---|---|---|
| `CNRELAndroid7.0.0.json` | `7.0_live` | 47482070 | `e637da0f75` | 47579390 | `b92051e672` |
| `CNRELAndroid7.1.0.json` | `7.1_live` | 48379043 | `cc8f4bb04d` | 48533839 | `0f4d11ebee` |
| `CNRELAndroid7.2.0.json` | `7.2_live` | 49086080 | `1c55d912bf` | 49291486 | `c25ba650a6` |

## Fields

| Field | Meaning |
|---|---|
| `ClientDataMd5` | Client data manifests, one JSON object per line: `data_versions`, `data_versions_medium` |
| `ResVersionConfig.Md5` | Resource manifests, one JSON object per line: `res_versions_external` / `_medium` / `_streaming`, `base_revision`, `patch_node_versions`, and on some versions `audio_diff_versions_<new>-<old>` |
| `ResourceUrl` | Resource CDN root: `https://autopatchcn.yuanshen.com/client_game_res/<branch>` |
| `DataUrl` | Design data CDN root: `https://autopatchcn.yuanshen.com/client_design_data/<branch>` |
| `ResVersionConfig.Version` / `VersionSuffix` | Resource version and suffix; the download path is `output_<Version>_<VersionSuffix>` |
| `ClientDataVersion` / `ClientVersionSuffix` | Client data version and suffix; same path scheme |
| `ClientSilenceDataVersion` / `ClientSilenceVersionSuffix` | Pre-download (silent) data version; when equal to the client version, the same `output_` directory is reused |
| `GateserverIp` / `GateserverPort` | Official gateway; rotates between versions, not needed for private servers |
| `Retcode` | 0 = OK |

Each manifest line carries three values:

- `md5` — standard MD5 of the file
- `hash` — **xxHash64 (seed = 0)**, 16 lowercase hex chars
- `fileSize` — size in bytes

URL construction:

```
{ResourceUrl}/output_{Version}_{VersionSuffix}/client/Android/{remoteName}
{DataUrl}/output_{ClientDataVersion}_{ClientVersionSuffix}/client/General/AssetBundles/{remoteName}
```

## How the data was obtained

1. The client requests `https://dispatchcnglobal.yuanshen.com/query_region_list?version=CNRELAndroid<ver>&lang=2&platform=2&binary=1&channel_id=1&sub_channel_id=1`
2. The response is protobuf, carrying `client_secret_key` (Ec2b format) and `client_custom_config`
3. Decrypting the custom config with EC2B reveals a `regionConfig` URL pointing to `query_security_file?file_key=CNRELAndroid<ver>`
4. That endpoint returns RSA-encrypted content and the client private key is not available, so the configs were rebuilt from the CDN paths the client actually requested, recomputing `md5` / `hash` / `fileSize` for every manifest

The `hash` algorithm was verified against the 7.1 `data_versions`: md5 `fe1421dbbc78bf6092705f8e2f1ef5e3` and hash `67d3fef07e68ada9` both match.

## Notes

- Structure differs slightly between versions. 7.0.0 has an extra `Relogin` field and uses `\n` line separators in `ClientDataMd5`; 7.1 and 7.2 use `\r\n`
- No `audio_diff_versions_*` file exists on the CDN for 7.2, so it is omitted
- `GateserverIp` reflects the value at capture time and is rotated by the official service; it does not affect resource downloads

## Disclaimer

The configuration data comes from the official public CDN and the client's own requests. All game content and assets are copyright miHoYo. This repository is provided for version comparison and technical research only.
