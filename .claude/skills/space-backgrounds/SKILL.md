---
name: space-backgrounds
description: プロシージャル宇宙背景の生成アルゴリズム
user-invocable: false
---

# 宇宙背景生成

## 構成要素

3つの描画関数を組み合わせて宇宙空間を表現:

### drawStars(ctx, w, h, count, maxRadius)
- ランダムな位置・サイズ・明るさで星を配置
- 大きめの星（maxRadius × 0.55超）にはRadialGradientでグロー効果
- 色相は5色をローテーション: 220, 40, 200, 350, 180

### drawBrightStar(ctx, x, y, size, hue)
- 十字の光条（LinearGradient × 2方向）
- RadialGradientのハロ
- 中心の白い点

### drawNebula(ctx, w, h, clouds, passes)
- cloud定義: `{ x, y, r/rx/ry, h, s, l, a }`
- 複数passで重ね描き（ランダムオフセットで自然な揺らぎ）
- 楕円形の星雲は `scale(1, ry/rx)` で変形

## 背景テーマ一覧

| テーマ | ベース色 | 星雲の色相 | 星の数 |
|--------|---------|-----------|--------|
| ディープ | #010810 | 青緑〜紫系 | 700 |
| パープル | #08000f | 紫〜マゼンタ | 550 |
| ウォーム | #060208 | オレンジ×青 | 550 |
| オーロラ | #020810 | 緑（sin波カーテン）| 500 |

## カスタム背景

ユーザー画像は `imgEl` として保持し、cover表示でクロップ:
```
アスペクト比の差に応じて sx/sy/sw/sh を計算 → drawImage
```

## 新しい背景を追加する場合

`背景一覧` 配列に `{ name, draw(ctx, w, h) }` を追加するだけ。
