# assets/screenshots/

ランディングページ (`index.html`) で使用する実機スクリーンショット。

## 現在のファイル

| ファイル名 | 対応画面 | 撮影元 |
| --- | --- | --- |
| `prompt.png` | ようこそ (オンボーディング) | WelcomeSetupView |
| `today.png` | 今日のセッション | TodayView |
| `program.png` | プログラム (12 週タイムライン) | WeekListView |
| `progress.png` | 進捗 | ProgressTabView |

## 仕様

- **解像度**: 1320 × 2868 px (iPhone 17 Pro Max / 6.9" 縦向き)
- **形式**: PNG 8-bit
- **ステータスバー**: 9:41 / 満充電 / 満アンテナ (`xcrun simctl status_bar override` で事前に整えている)

## 再撮影手順

1. Xcode シミュレータ で `iPhone 17 Pro Max` を起動
2. ステータスバーを整える:
   ```
   xcrun simctl status_bar booted override --time 9:41 --batteryState charged --batteryLevel 100 --wifiBars 3 --cellularBars 4 --cellularMode active --dataNetwork lte
   ```
3. アプリを起動 → 規約同意 → 「サンプルプログラムを試す」でサンプル投入
4. 各画面に遷移して ⌘S (Simulator.app メニュー: File → Save Screen)
5. Desktop に保存された PNG を本ディレクトリに同名で配置
6. `git add assets/screenshots/*.png && git commit && git push` で GitHub Pages に反映

## App Store Connect 用のスクリーンショット

Apple が必須とするのは **6.9" (1320 × 2868)** のみ (2026年現在)。6.3"/6.1" は自動スケール対象で不要。
上記の 4 枚はそのまま App Store Connect の「iPhone 6.9" Display」スロットに流用可能。
詳細は `/Users/masa/app/train/docs/app-store-submission.md` を参照。
