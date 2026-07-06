# かながわ終活ナビ（ポータル）

`kanagawa-shukatsu.com` のルートで配信するポータルサイト。ビルド不要の静的ファイルのみ。

## 構成

```
public/
├── index.html   # ポータルトップ（3サービス案内・運営者情報）
├── robots.txt   # ★ドメイン全体のrobots。3サイトのサイトマップを列挙
└── sitemap.xml  # ポータル自身のサイトマップ
```

## デプロイ（Cloudflare Workers 静的アセット）

- ビルドコマンド: なし
- アセットディレクトリ: `public`
- ルート: `kanagawa-shukatsu.com/*`（各サブサイトのルートより優先度低）

## ドメイン全体のルーティング

| パス | Worker（リポジトリ） |
|------|---------------------|
| `/sougi/*` | sougi-kanagawa |
| `/ihin-seiri/*` | ihin-seiri-kanagawa |
| `/akiya/*` | akiya-kanagawa |
| `/*`（上記以外） | 本リポジトリ |

各サブサイトは Astro の `base` 設定＋ `outDir: dist/<base>` でパスを一致させている。
