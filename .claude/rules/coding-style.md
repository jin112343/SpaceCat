---
description: Space Catのコーディングスタイルルール
---

- UIテキスト・コメントは日本語
- 状態変数は日本語名を使用（`被写体`, `選択中BG`, `背景一覧`）
- 関数名は英語（`drawStars`, `scheduleRender`, `shrink`）
- カラーテーマ: 宇宙ダーク `#030014`、パープル `#a78bfa`、ピンク `#f472b6`、ゴールド `#fbbf24`
- フォント: Orbitron（見出し）+ Noto Sans JP（本文）
- フレームワークやビルドツールを導入しない（単一HTML維持）
- Canvas描画は必ず `scheduleRender()` 経由
- シェアテキストには `#SpaceCat` を含める
