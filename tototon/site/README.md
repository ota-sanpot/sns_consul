# 魚魚呑（とととん）公式ブランディング・ウェブ

大田区サンポット「Simple Branding Web for Food」初の実店舗実装。

- 店舗: 和酒だいにんぐ 魚魚呑（蒲田駅東口 徒歩2分・海鮮居酒屋）
- 公開URL（予定）: https://ota-sanpot.github.io/tototon/
- 設計書: `../../../docs/superpowers/specs/2026-05-29-tototon-site-design.md`
- スタイルベース: https://ota-sanpot.github.io/simple-hp/

## ローカルプレビュー

```bash
cd OtaSanpot/sns_consul/tototon/site
python3 -m http.server 8765
# → http://localhost:8765
```

## デザイン制約

- フォント: Noto Sans JP のみ（serif 不可、日本語 italic 不可）
- カラー: paper / kinari / sumi / gold / goldlt / sub / line + 藍 `#1F3A5F`
- ホスト: GitHub Pages（`main` ブランチ root）

## オーナー確認待ち

- ebica 予約URL
- 公式 SNS アカウント（IG / X / FB）
- 看板品の最終リスト・価格表記
- 写真素材（朝〆刺身盛・店内・外観・店主・日本酒棚）
- 受賞情報の掲載許諾

## 公開手順（CEO 用）

````bash
# 1. このディレクトリを別の場所にコピー（CEO リポ管理外に置く）
cp -r OtaSanpot/sns_consul/tototon/site ~/Desktop/tototon-deploy

# 2. github-ota-sanpot ホスト経由で新規リポを作る
cd ~/Desktop/tototon-deploy
git init
git checkout -b main
git add .
git commit -m "init: 魚魚呑 公式ブランディング・ウェブ v0"

# 3. GitHub 側で空リポ ota-sanpot/tototon を作成（gh CLI / Web どちらでも）
#    Public・README 無し・.gitignore 無し
gh repo create ota-sanpot/tototon --public --source=. --remote=origin --push

# 4. GitHub Pages を有効化（main ブランチ root）
gh api -X PUT repos/ota-sanpot/tototon/pages -f source.branch=main -f source.path=/

# 5. 公開URL
#    https://ota-sanpot.github.io/tototon/
````

## 公開後の差し替え運用

- ebica 予約URL 受領 → `data-reserve-link="ebica-pending"` のボタンを差し替え
- 受賞許諾 取得 → `award-badge` の `data-empty="true"` を `"false"` に変更
- 写真受領 → `assets/` に配置し、SIGNATURE のプレースホルダ `<div>` を `<img>` に差し替え
- 公式 SNS → footer の運営表記近くにリンクを追加
