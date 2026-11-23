Contributors

Special thanks to fdjgscgfj for providing the Hotfix configurations.

特别感谢 fdjgscgfj 提供热更新（Hotfix）配置。

￼ 

原神国际服安卓目前有效的热更新配置

本仓库保存原神国服安卓客户端的 query_cur_region 响应中的 RegionInfo 配置， 每个可用版本分支对应一个 JSON 文件。

版本清单

版本文件网关服务器1.0.0CNRELAndroid1.0.0.json47.116.110.112:221011.1.0CNRELAndroid1.1.0.json47.116.110.112:221011.2.0CNRELAndroid1.2.0.json47.116.110.112:221011.3.0CNRELAndroid1.3.0.json47.116.110.112:221011.4.0CNRELAndroid1.4.0.json47.116.110.112:221011.5.0CNRELAndroid1.5.0.json47.116.110.112:221011.6.0CNRELAndroid1.6.0.json47.116.110.112:221012.0.0CNRELAndroid2.0.0.json47.116.110.112:221012.1.0CNRELAndroid2.1.0.json47.116.110.112:221012.2.0CNRELAndroid2.2.0.json47.116.110.112:221012.3.0CNRELAndroid2.3.0.json47.116.110.112:221012.4.0CNRELAndroid2.4.0.json47.116.110.112:221012.5.0CNRELAndroid2.5.0.json47.116.110.112:221012.6.0CNRELAndroid2.6.0.json47.116.110.112:221012.7.0CNRELAndroid2.7.0.json47.116.110.112:221012.8.0CNRELAndroid2.8.0.json47.116.110.112:221013.0.0CNRELAndroid3.0.0.json47.116.110.112:221013.1.0CNRELAndroid3.1.0.json47.116.110.112:221013.3.0CNRELAndroid3.3.0.json47.116.110.112:221013.5.0CNRELAndroid3.5.0.json47.116.110.112:221013.6.0CNRELAndroid3.6.0.json47.116.110.112:221013.7.0CNRELAndroid3.7.0.json47.116.110.112:221013.8.0CNRELAndroid3.8.0.json47.116.110.112:221014.0.0CNRELAndroid4.0.0.json47.116.110.112:221014.1.0CNRELAndroid4.1.0.json47.116.110.112:221014.2.0CNRELAndroid4.2.0.json47.101.203.7:221014.3.0CNRELAndroid4.3.0.json47.103.29.152:221014.4.0CNRELAndroid4.4.0.json47.103.23.92:221024.5.0CNRELAndroid4.5.0.json47.116.110.112:221014.6.0CNRELAndroid4.6.0.json47.116.110.112:221014.7.0CNRELAndroid4.7.0.json47.116.110.112:221014.8.0CNRELAndroid4.8.0.json47.116.110.112:221015.0.0CNRELAndroid5.0.0.json47.116.110.112:221015.1.0CNRELAndroid5.1.0.json47.116.110.112:221015.2.0CNRELAndroid5.2.0.json47.116.110.112:221015.3.0CNRELAndroid5.3.0.json47.116.110.112:221015.4.0CNRELAndroid5.4.0.json47.116.110.112:221015.5.0CNRELAndroid5.5.0.json47.116.110.112:221015.6.0CNRELAndroid5.6.0.json47.116.110.112:221015.7.0CNRELAndroid5.7.0.json47.116.110.112:221015.8.0CNRELAndroid5.8.0.json47.116.110.112:221016.0.0CNRELAndroid6.0.0.json47.116.110.112:221016.1.0CNRELAndroid6.1.0.json47.116.110.112:221016.2.0CNRELAndroid6.2.0.json47.116.110.112:221016.3.0CNRELAndroid6.3.0.json47.116.110.112:221016.4.0CNRELAndroid6.4.0.json47.116.110.112:221016.5.0CNRELAndroid6.5.0.json47.116.110.112:221016.6.0CNRELAndroid6.6.0.json47.100.117.206:221026.7.0CNRELAndroid6.7.0.json47.116.110.112:221017.0.0CNRELAndroid7.0.0.json47.103.30.226:221017.1.0CNRELAndroid7.1.0.json47.116.110.112:221017.2.0CNRELAndroid7.2.0.json47.116.110.112:22101 

未列出 3.2.0 和 3.4.0，因为官方 CDN 清单已不可用，对应配置文件已删除。

文件包含的内容

每个文件都是完整的 query_cur_region 响应：

{ "RegionInfo": { "ClientDataMd5": "...", "ResourceUrl": "https://autopatchcn.yuanshen.com/client_game_res/<分支>", "NextResourceUrl": "...", "ResourceUrlBak": "<分支>", "DataUrl": "https://autopatchcn.yuanshen.com/client_design_data/<分支>", "NextResVersionConfig": { "Md5": "0", "ReleaseTotalSize": "0", "Branch": "<分支>" }, "ResVersionConfig": { "Version": "<资源版本>", "Md5": "{...res_versions_external / medium / streaming / base_revision / patch_node_versions...}", "ReleaseTotalSize": "0", "VersionSuffix": "...", "Branch": "<分支>" }, "GameBiz": "hk4e_cn", "AreaType": "CN", "ClientDataVersion": "<数据版本>", "ClientSilenceDataVersion": "<静默数据版本>", "ClientVersionSuffix": "...", "ClientSilenceVersionSuffix": "...", "UseGateserverDomainName": false, "GateserverIp": "...", "GateserverPort": 22101, "PrivacyPolicyUrl": "...", "CdkeyUrl": "..." }, "Retcode": 0 } 

字段说明

ClientVersionSuffix / ClientSilenceVersionSuffix：客户端版本后缀。

ResVersionConfig.Version / VersionSuffix：资源 revision 和后缀。

ClientDataMd5 / ResVersionConfig.Md5：数据与资源清单校验信息。

ResourceUrl / DataUrl：对应版本分支的官方 CDN 地址。

GateserverIp / GateserverPort：版本对应的网关服务器。

