# train-landing

iOS アプリ **TrainingApp** の紹介 / サポート用静的サイト。

## 目的

- App Store Connect 提出時に必須となる **プライバシーポリシー URL** / **サポート URL** の公開場所
- アプリ自体のシンプルな紹介ページ
- GitHub Pages で無料配信、通信・分析・広告なし

## 構成

```
train-landing/
├── .gitignore
├── .nojekyll              # GitHub Pages の Jekyll 処理を無効化
├── LICENSE                # コード部は MIT、法務本文は All Rights Reserved
├── README.md
├── index.html             # トップ (アプリ紹介 + FAQ)
├── terms.html             # 利用規約 (プレースホルダ)
├── privacy.html           # プライバシーポリシー (プレースホルダ)
├── support.html           # サポート窓口
└── assets/
    ├── favicon.svg        # SVG ファビコン (ダンベル)
    ├── ogp.png            # 1200x630 OGP 画像 (未生成 — 下記参照)
    └── style.css          # Tailwind で足りない部分の最小 CSS
```

- HTML / CSS / SVG のみ。ビルドツールなし、Node.js 不要
- スタイルは Tailwind CDN + 自前 `assets/style.css`
- JS は使用しない (progressive enhancement のみ)

## ローカル確認

```bash
cd /Users/masa/app/train-landing
python3 -m http.server 8000
# → http://localhost:8000/
```

`index.html`, `terms.html`, `privacy.html`, `support.html` がそれぞれ 200 で返ることを確認してください。

```bash
for p in "" terms.html privacy.html support.html; do
  curl -s -o /dev/null -w "%{http_code}  /$p\n" "http://localhost:8000/$p"
done
```

## GitHub Pages デプロイ手順

1. GitHub で新規 **public** リポジトリを作成 (例: `train-landing`)
2. このディレクトリで remote を追加して push

   ```bash
   cd /Users/masa/app/train-landing
   git remote add origin git@github.com:<your-account>/train-landing.git
   git branch -M main
   git push -u origin main
   ```

3. リポジトリ Settings → **Pages**
   - Source: `Deploy from a branch`
   - Branch: `main` / `/` (root)
   - Save
4. 数分後、`https://<your-account>.github.io/train-landing/` で公開される
5. (任意) カスタムドメインを使う場合:
   - `assets/` と同じ階層に `CNAME` ファイルを作成、中身は `example.com` などドメイン名のみ
   - DNS で CNAME レコードを `<your-account>.github.io` に向ける
   - Pages 設定で HTTPS を強制

## プレースホルダ一覧 (公開前に必ず差し替え)

| 場所 | 目的 | キー / マーカー |
|---|---|---|
| 全ページ `data-app-name` 付き要素 | アプリ名 (リリース時変更の可能性あり) | `data-app-name` |
| 全ページフッター `data-owner` | 運営者名 (個人名 or 屋号) | `data-owner` |
| `support.html` `data-contact-email` | サポートメール (`mailto:`) | `data-contact-email` |
| `support.html` `data-github-issues` | GitHub Issues の URL | `data-github-issues` |
| `support.html` `data-google-form` | Google Form の URL (任意。不要なら当該セクション削除可) | `data-google-form` |
| `index.html` Hero の App Store リンク | 公開後の App Store URL | `TODO: App Store バッジ` コメント |
| 全ページ `<link rel="canonical">` と OGP `og:image` | 公開先 URL (`https://<account>.github.io/train-landing/`) | `example.github.io` を全置換 |
| `assets/screenshots/*.png` | 実機スクリーンショット 4 枚 (ホーム / ワークアウト / 進捗 / ランニング) | `TODO: assets/screenshots/*.png` コメント |
| `assets/ogp.png` | 1200x630 の OGP 画像 | ファイル未生成 (下記参照) |

全プレースホルダは以下で一覧できます:

```bash
grep -rn "TODO\|example\|data-owner\|data-contact-email\|data-github-issues\|data-google-form" .
```

## OGP / スクリーンショット画像について

- **`assets/ogp.png`** (1200×630) は未生成です。Figma / Keynote / Canva 等で作成してください。
  - 推奨: アプリ名 + キャッチコピー + ダークベース + アクセントカラー (#c2ff00)
  - 書き出し後 `assets/ogp.png` として配置
- **スクリーンショット**: iPhone 実機 / シミュレータで 4 枚撮影し、`assets/screenshots/home.png` などとして配置。
  - `index.html` の `TODO: assets/screenshots/*.png` コメント付近の `<div class="screenshot-placeholder">` を `<img src="assets/screenshots/home.png" alt="..." />` に置き換え

## 法的文書の同期フロー

利用規約 / プライバシーポリシーの本文は **別リポ** (`../train/legal/*.md`) を正本として管理する運用です。

1. `../train/legal/terms.md` または `../train/legal/privacy.md` を編集
2. Markdown を HTML に変換 (`pandoc -f gfm -t html terms.md` などを想定)
3. `terms.html` / `privacy.html` の `<article data-sync-source="...">` の中身を置換
4. 同ページの `最終更新日` (`<time datetime="YYYY-MM-DD">`) を更新
5. 両リポで commit

同期ポイントは以下のコメントで示してあります:

```html
<!-- SYNC FROM: /Users/masa/app/train/legal/terms.md -->
<article data-sync-source="legal/terms.md">
  ...
</article>
```

## ライセンス

- ソースコード (HTML/CSS/SVG 構造部): MIT (`LICENSE` 参照)
- 法務文書本文・アプリ固有のコピー・スクリーンショット・ロゴ・OGP 画像: All Rights Reserved
