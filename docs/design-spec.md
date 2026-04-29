# GURUMA SNSコンサル LP — デザインリニューアル仕様書

**日付:** 2026-04-29
**対象ファイル:** `OtaSanpot/sns_consul/index.html`

---

## 1. デザイン方向性

**Vivid Gradient × Modern Dark**

現在のLuxury Dark（黒×ゴールド）から、モダンなインディゴ×ピンクグラデーションスタイルに全面刷新する。動きのあるUI（アニメーション・ホバーエフェクト・スクロールフェードイン）を用いて、スタートアップ・SaaSのような洗練された印象を実現する。

---

## 2. カラーパレット

| 用途 | カラー | HEX |
|------|--------|-----|
| プライマリ | Indigo | `#6366f1` |
| セカンダリ | Purple | `#7c3aed` |
| アクセント | Pink | `#ec4899` |
| グラデーション | Indigo → Purple → Pink | `135deg` |
| ダーク背景 | Near Black | `#09090b` |
| ライト背景 | Off White | `#fafafa` |
| テキスト主 | — | `#0f0f0f` |
| テキスト副 | — | `#777777` |

### グラデーション定義
```css
--grad-main: linear-gradient(135deg, #6366f1, #7c3aed, #ec4899);
--grad-text: linear-gradient(135deg, #a5b4fc, #f9a8d4); /* ダーク背景上のグラデーションテキスト */
```

---

## 3. タイポグラフィ

- フォント：**Noto Sans JP**（Google Fonts）`wght@300;400;700;900`
- 見出し：`font-weight: 900`、`letter-spacing: -1px`〜`-2px`
- 本文：`font-weight: 300`〜`400`、`line-height: 1.8`〜`1.9`
- ラベル：`font-weight: 700`、`letter-spacing: 3px〜4px`、大文字
- グラデーションテキスト：`-webkit-background-clip: text; -webkit-text-fill-color: transparent`

---

## 4. ボタン仕様（視認性重視）

### プライマリボタン
```css
background: linear-gradient(135deg, #6366f1, #ec4899);
color: #ffffff;
font-weight: 700;
font-size: 13px;
padding: 15px 34px;
border-radius: 100px;
box-shadow: 0 8px 40px rgba(99,102,241,0.5);
/* ホバー時 */
transform: translateY(-2px);
box-shadow: 0 16px 48px rgba(99,102,241,0.6);
```

### ゴーストボタン（ダーク背景上）
```css
color: rgba(255,255,255,0.85); /* 視認性確保のため高めの不透明度 */
border-bottom: 1px solid rgba(255,255,255,0.5);
font-size: 13px;
/* ホバー時 */
color: #ffffff;
```

### アウトラインボタン（ライト背景上）
```css
border: 1.5px solid #e5e7eb;
color: #0f0f0f; /* 十分なコントラスト */
font-size: 12px;
font-weight: 700;
border-radius: 100px;
/* ホバー時 */
background: #0f0f0f; color: #fff;
```

---

## 5. アニメーション仕様

### Blob アニメーション（ヒーロー背景）
```css
@keyframes blobFloat {
  0%, 100% { transform: translate(0,0) scale(1); }
  33%       { transform: translate(30px,-40px) scale(1.05); }
  66%       { transform: translate(-20px,20px) scale(.95); }
}
/* blob-1: 8s ease-in-out infinite */
/* blob-2: 8s ease-in-out infinite, delay -3s */
/* blob-3: 8s ease-in-out infinite, delay -5s */
```

### スクロールフェードイン
```javascript
// IntersectionObserver で .reveal クラスを監視
// threshold: 0.1, rootMargin: '0px 0px -40px 0px'
// 可視になったら .visible を付与 → opacity:1, translateY(0)
transition: opacity .7s cubic-bezier(.16,1,.3,1), transform .7s cubic-bezier(.16,1,.3,1);
```

### カードホバー
```css
/* 浮き上がり */
transform: translateY(-6px);
box-shadow: 0 20px 60px rgba(99,102,241,0.1);
/* サービスカード上部ライン */
::before { height:3px; background: grad-main; transform: scaleX(0→1); }
```

### マーキー（サービス名流れるテキスト帯）
```css
@keyframes marquee { from{transform:translateX(0)} to{transform:translateX(-50%)} }
/* 18s linear infinite */
```

---

## 6. セクション構成

| セクション | 背景 | 主な要素 |
|-----------|------|---------|
| Nav | 白・半透明（`backdrop-filter: blur(20px)`） | ロゴ（グラデーション）・リンク・CTAボタン |
| Hero | ダーク（`#09090b`）＋3 blob アニメーション＋ドットグリッド | バッジ・H1・サブコピー・ボタン2つ・KPI数値3つ |
| Marquee | グラデーション帯 | サービス名が流れる |
|悩み | `#fafafa` | 3カードグリッド（ホバーで浮き上がり） |
| サービス | `#ffffff` | 2×2カードグリッド（ホバーでトップライン展開） |
| 料金 | `#fafafa` | 3カード（中央のみグラデーション・scale拡大） |
| CTA | ダーク＋blob | 大見出し・CTAボタン |
| Footer | `#040407` | ロゴ・コピーライト |

---

## 7. テキスト配置の原則

- セクション見出しは左揃え（中央揃えはCTA・料金のみ）
- `max-width` を設定してテキストが長くなりすぎないよう制限（本文は最大 `480px`〜`520px`）
- ヒーローのサブコピーは `font-weight: 300` でライトに
- ラベル（PAIN POINTS 等）は `::before` の短いラインと組み合わせて視覚的なアクセントを付ける
- 行間は最小 `1.7`、本文は `1.8`〜`1.9`

---

## 8. 既存コンテンツの継承

以下は現行 `index.html` から内容をそのまま引き継ぐ：
- ナビゲーションリンク・セクション構成
- 問題提起（3項目）
- サービス内容（4項目）
- 導入の流れ（5ステップ）
- 実績・事例（2件）
- 料金プラン（3プラン・金額）
- FAQ（5問）
- CTAリンク（Googleフォーム URL）
- フッターSNSリンク・Instagram/TikTok/YouTube/LINE/Web

---

## 9. 実装上の注意

- Tailwind CDN は引き続き使用可（または純粋なCSSで書き直しも可）
- Lucide アイコンは継続使用
- Font Awesome は継続使用（フッターSNSアイコン）
- `backdrop-filter` は Safari 対応のため `-webkit-backdrop-filter` も付与
- グラデーションテキストは `-webkit-background-clip` と `-webkit-text-fill-color` を使用
- スクロールアニメーションは `IntersectionObserver` で実装（既存と同方式）
