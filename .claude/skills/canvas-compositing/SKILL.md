---
name: canvas-compositing
description: Space CatのCanvas合成・レンダリングシステムの技術詳細
user-invocable: false
---

# Canvas合成システム

## レンダリングパイプライン（render関数）

1. 初回のみCanvasサイズを被写体の元画像サイズに設定
2. `clearRect` で全面クリア
3. `renderBg()` でキャッシュ済み宇宙背景を描画
4. 被写体をtransform付きで描画:
   - `translate(posX * W, posY * H)` — 正規化座標→ピクセル変換
   - `rotate(rotation * π / 180)` — 度→ラジアン
   - `scale(-1, 1)` — 反転時のみ
   - `drawImage(img, -drawW/2, -drawH/2, drawW, drawH)` — 中心基準

## パフォーマンス

- `scheduleRender()` — RAF で1フレーム1描画に間引き
- `renderBg()` — 背景をオフスクリーンCanvasにキャッシュ（同じ背景・サイズなら再利用）
- `canvasSized` フラグ — リサイズは1回のみ

## 出力

- `canvas.toBlob('image/png')` → File → Web Share API / Clipboard / download
