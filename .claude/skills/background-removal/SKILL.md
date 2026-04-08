---
name: background-removal
description: '@imgly/background-removalの統合方法と注意点'
user-invocable: false
---

# 背景除去

## ライブラリ

`@imgly/background-removal` v1.5.13（CDN経由 ES Module）

```js
import { removeBackground } from 'https://cdn.jsdelivr.net/npm/@imgly/background-removal@1.5.13/+esm'
```

## 処理フロー

1. `shrink(file, 1024)` — モバイルOOM対策で1024px以下にリサイズ
2. `removeBackground(resized, { progress })` — 背景除去実行
3. 結果Blobを `Image` に変換して `被写体` に設定

## progressコールバック

- `key.includes('fetch')` → モデルダウンロード中
- `key.includes('inference')` → 推論処理中（進捗%表示）

## エラー分類

- `memory` / `alloc` → メモリ不足
- `network` / `fetch` → ネットワークエラー
- その他 → 汎用エラー（2.5秒後にUIリセット）

## ライセンス

AGPL-3.0 → プロジェクト全体もソース公開必須
