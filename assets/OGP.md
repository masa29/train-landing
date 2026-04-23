# OGP 画像 (`assets/ogp.png`)

SNS シェア時のプレビュー画像。X (Twitter), Facebook, LINE, Slack 等で表示される。

## 仕様

- **ファイルパス**: `assets/ogp.png`
- **解像度**: **1200 × 630 px** (OGP/Twitter Card 両対応の推奨サイズ)
- **形式**: PNG (JPEG も可)
- **ファイルサイズ**: 500 KB 以下推奨 (あまり大きいとシェア時にクロールが失敗する)
- **余白**: 周囲 60 px 以上の余白を取ると、Twitter Card で切り取られても中身が収まる (セーフエリア: 中央 1080 × 540 px)

## 反映先 (既に設定済)

各 HTML の `<meta property="og:image" content="https://masa29.github.io/train-landing/assets/ogp.png">` で参照済み。
画像を配置して push すれば反映される。

## デザインの考え所

- **視認性**: SNS タイムラインでは小さく表示されるので、文字は太め・大きめ
- **ブランド統一**: 本体アプリと同じアクセントカラー (`#c2ff00` 系ライム) を使うと視認性が高い
- **要素例** (参考):
  - アプリ名 "TrainingApp"
  - キャッチコピー "AI で作る12週間の筋力トレーニング" 程度
  - iPhone に表示されたアプリのモックアップ (右寄せ等)
  - 背景はダーク (`#0a0a0a` 系)

## 反映確認

push 後、以下で OGP のプレビューを確認できる:

- Twitter/X: https://cards-dev.twitter.com/validator (現在は `https://x.com/home` にログイン後、ツイート編集画面で URL を貼ると自動プレビュー)
- Facebook: https://developers.facebook.com/tools/debug/
- LINE: https://poker.line.naver.jp/ (LINE Developers)

SNS キャッシュがある場合は上記ツールの "Scrape Again" / "Re-fetch" で最新化できる。
