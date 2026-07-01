# Netease Music 插件

从自建 [NeteaseCloudMusicApi](https://github.com/Binaryify/NeteaseCloudMusicApi)(或 enhanced 分支)获取元数据与歌词的 Navidrome 插件。

## 能力

| 能力 | 说明 | NCM 端点 |
|---|---|---|
| 歌手头像 | `picUrl` / `img1v1Url` | `/search?type=100` |
| 歌手简介 | 简介文本 | `/artist/desc` |
| 歌手热门歌曲 | 代表作 | `/artist/top/song` |
| 相似歌手 | 关联推荐 | `/simi/artist` |
| 专辑信息 | 描述 + 外链 | `/search?type=10` → `/album` |
| 专辑封面 | 封面图 | 同上 |
| 歌词 | LRC + 中文翻译 | `/search?type=1` → `/lyric/new` |

> 评论:Navidrome 当前无承载位,暂不实现(`client.go` 留有扩展点说明)。

## 配置(UI 插件页填写)

| 键 | 说明 | 默认 |
|---|---|---|
| `api_url` | NCM 地址,**填容器内可达地址**,如 `http://172.18.0.1:3000` | (必填) |
| `search_limit` | 搜索候选数 | 5 |
| `strict_name_match` | 严格名称匹配 | true |
| `enable_translated_lyrics` | 返回翻译歌词 | true |

## 构建与部署

```bash
# 需 TinyGo >= 0.34
make package                # 生成 netease.ndp
scp netease.ndp root@<host>:/data/plugins/
```

服务端需开启插件:`ND_PLUGINS_ENABLED=true`。
部署后在 UI 插件页"重新扫描" → 启用 → 填 `api_url`。
要参与元数据抓取,把插件 ID 加进 `ND_AGENTS`。
