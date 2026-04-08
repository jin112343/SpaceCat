---
description: モバイルファースト設計の原則
---

- 主要ターゲットはモバイルブラウザ
- タッチターゲットは最小44px
- 大きい画像は処理前に1024pxにリサイズ（OOM防止）
- Web Share API → Clipboard → download の順でフォールバック
- `safe-area-inset-bottom` でノッチ対応
- `touch-action: none` + `preventDefault()` でスクロール抑制
- `100dvh` でモバイルアドレスバー対応
