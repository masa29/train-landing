# assets/screenshots/

ランディングページ (`index.html`) で使用する実機スクリーンショット。

## 必要ファイル

| ファイル名 | 対応画面 |
| --- | --- |
| `home.png` | ホーム (Today タブ) |
| `workout.png` | ワークアウト実行 (セット入力) |
| `progress.png` | 進捗 (Progress タブ) |
| `cardio.png` | ランニング記録 (Cardio タブ) |

## 仕様

- **解像度**: 1290 × 2796 px (iPhone 6.7" 縦向き、iPhone 15 Pro Max 相当)
- **形式**: PNG 8-bit (透過不要)
- **ファイルサイズ**: 1 枚あたり 300 KB 以下を目安 (TinyPNG 等で圧縮推奨)
- **撮影方法**: Xcode シミュレータで `iPhone 15 Pro Max` (または `16 Pro Max`) を選び、`⌘S` でスクリーンショット保存
- **内容のヒント**:
  - `home.png` は「今日」のタブを開いた状態で、当日のメニューが見える状態
  - `workout.png` は `SetLoggerView` でセット入力中
  - `progress.png` は `ProgressTabView` のサマリ表示
  - `cardio.png` は `CardioView` または `CardioDetailView`

## 差し替え手順

1. 撮ったスクショをこのディレクトリに同名で保存
2. `git add assets/screenshots/*.png && git commit -m "feat: add landing screenshots"`
3. `git push` → GitHub Pages が数十秒で再ビルド、ブラウザ再読込で反映

## App Store Connect 用のスクリーンショット

Apple に申請するスクショは解像度・枚数要件が別 (6.7" と 6.1" の 2 種類必須、各 3-10 枚)。
それらは App Store Connect に直接アップロードするため、このディレクトリには含めなくて OK。
詳細は `/Users/masa/app/train/docs/app-store-submission.md` を参照。
