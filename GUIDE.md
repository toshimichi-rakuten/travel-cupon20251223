# 楽天トラベル コンポーネント再利用ガイド

このガイドでは、「まとめてクーポン」ページの書き方を他のページで活かす方法を説明します。

---

## 📋 目次

1. [このコードの構造の特徴](#このコードの構造の特徴)
2. [パーツとして再利用できる部分](#パーツとして再利用できる部分)
3. [実際の流用方法](#実際の流用方法)
4. [新しいページを作る手順](#新しいページを作る手順)

---

## このコードの構造の特徴

このページは**3つの層**に分かれています:

```
┌─────────────────────────────┐
│ 1. HTMLファイル(骨組み)      │  ← index まとめてクーポン.html
├─────────────────────────────┤
│ 2. CSSファイル(見た目)       │  ← css/contents_pc.css
│                             │     css/contents_sp.css
├─────────────────────────────┤
│ 3. SSIファイル(中身のパーツ) │  ← ssi/coupon.html
└─────────────────────────────┘
```

### なぜこの構造が便利なのか?

- **HTMLは骨組みだけ** → 一度作れば、ずっと使える
- **CSSは見た目だけ** → デザインを変えたい時だけ触る
- **SSIは中身だけ** → クーポン内容を変えたい時だけ触る

**例えるなら**: お弁当箱(HTML)、盛り付け方(CSS)、おかず(SSI)が分かれている感じです。

---

## パーツとして再利用できる部分

### ✅ そのまま流用できるパーツ

#### 1️⃣ **ヒーローセクション(目立つ見出し部分)**

```html
<section class="ss-container" id="getAllCoupon">
  <p class="txt">クーポン併用で<br class="sp">最大30%OFF<span>ここに小さい説明</span></p>
  <div class="getAllCoupon">
    <div class="cpn-all-click">
      <button id="cpn-madome" class="cpn-all-click-btns">まとめてクーポンを獲得</button>
    </div>
  </div>
</section>
```

**使える場面**:
- キャンペーンのトップ訴求
- 特集ページの見出し
- 期間限定セールの告知

**変更するところ**:
- `.txt` の中身 → あなたの訴求文言に変える
- ボタンのテキスト → 「今すぐ予約」「詳細を見る」など

---

#### 2️⃣ **クーポンカード**

```html
<div class="couponOneClick">
  <div class="coupon__container">
    <a href="リンク先" class="couponOneClick-default">
      <div class="coupon__content">
        <div class="coupon__service__category">
          <div class="coupon__service">国内宿泊</div>
          <div class="coupon__category">最高級宿</div>
        </div>
        <div class="coupon__price">
          <span>20</span>%OFF
        </div>
        <div class="coupon__get">宿クーポンを獲得する</div>
      </div>
    </a>
  </div>
</div>
```

**使える場面**:
- クーポン一覧ページ
- 特典の表示
- お得情報カード

**変更するところ**:
- `国内宿泊` → サービス名
- `最高級宿` → カテゴリー名
- `20%OFF` → 割引率や特典内容

---

#### 3️⃣ **詳細テーブル**

```html
<div class="tableholderCpn">
  <table>
    <tbody>
      <tr>
        <td>予約対象期間</td>
        <td>2025/12/12(金) 10:00～2025/12/23(火) 9:59</td>
      </tr>
      <tr>
        <td>対象サービス</td>
        <td>国内宿泊(日帰り・デイユース除く)</td>
      </tr>
      <!-- 行を増やしたい場合は<tr>...</tr>をコピー -->
    </tbody>
  </table>
</div>
```

**使える場面**:
- 条件の詳細説明
- 規約の表示
- スペック表

**変更するところ**:
- 左側 → 項目名
- 右側 → 詳細内容

---

## 実際の流用方法

### 方法1: 同じレイアウトで内容だけ変える

**手順**:

1. `index まとめてクーポン.html` をコピー
2. ファイル名を変更 (例: `index 温泉特集.html`)
3. `ssi/coupon.html` をコピー
4. ファイル名を変更 (例: `ssi/onsen.html`)
5. HTMLの中の以下の部分を変更:

```javascript
// 元のコード
const allssi = {
  coupon_01: "ssi/coupon.html",
};

// 変更後
const allssi = {
  coupon_01: "ssi/onsen.html",  // ← ここを新しいファイル名に
};
```

6. 新しい `ssi/onsen.html` の中身を編集

---

### 方法2: パーツだけを別ページに組み込む

**手順**:

#### ステップ1: 必要なCSSを読み込む

既存のHTMLの `<head>` タグ内に以下を追加:

```html
<link rel="stylesheet" href="css/contents_pc.css" media="all and (min-width: 721px)">
<link rel="stylesheet" href="css/contents_sp.css" media="all and (min-width: 0px) and (max-width: 720px)">
```

#### ステップ2: 使いたいパーツをコピー

例えば、クーポンカードだけ使いたい場合:

```html
<!-- あなたの既存ページのどこかに貼り付け -->
<div class="coupon__box">
  <div class="coupon__box__holder">
    <!-- ここにssi/coupon.htmlの内容をコピペ -->
  </div>
</div>
```

---

## 新しいページを作る手順

### 例: 「秋の紅葉特集」ページを作る

#### 手順1: HTMLファイルを作る

`index 紅葉特集.html` を作成:

```html
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<title>秋の紅葉特集 【楽天トラベル】</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

<!-- 共通CSS -->
<link rel="stylesheet" href="https://img.travel.rakuten.co.jp/share/common/css/style-pc.css" media="screen and (min-width: 721px)">
<link rel="stylesheet" href="https://img.travel.rakuten.co.jp/share/common/css/style-sp.css" media="screen and (min-width: 0px) and (max-width: 720px)">

<!-- このページ専用のCSS -->
<link rel="stylesheet" href="css/contents_pc.css" media="all and (min-width: 721px)">
<link rel="stylesheet" href="css/contents_sp.css" media="all and (min-width: 0px) and (max-width: 720px)">
</head>
<body>

<div id="widewrapper">

  <!-- ヒーローセクション -->
  <section class="ss-container" id="getAllCoupon">
    <p class="txt">紅葉シーズン限定<br class="sp">最大25%OFF<span>絶景の紅葉スポット近くの宿</span></p>
    <div class="getAllCoupon">
      <div class="cpn-all-click">
        <button id="cpn-madome" class="cpn-all-click-btns">クーポンをまとめて獲得</button>
      </div>
    </div>
  </section>

  <!-- クーポン一覧 -->
  <section class="ss-container" id="coupon">
    <h2 class="ttl">紅葉特集で使えるクーポン</h2>
    <div class="coupon__box">
      <div class="coupon__box__holder">
        <div id="coupon_01"></div>
      </div>
    </div>
  </section>

</div>

<!-- SSI読み込み -->
<script>
  const allssi = {
    coupon_01: "ssi/koyo.html",
  };
</script>
<script src="https://img.travel.rakuten.co.jp/share/assets/js/coupon/allClickMerge.min.js"></script>
</body>
</html>
```

#### 手順2: SSIファイルを作る

`ssi/koyo.html` を作成:

```html
<div class="couponOneClick">
  <div class="coupon__container">
    <a href="クーポン獲得URL" class="couponOneClick-default">
      <div class="coupon__content">
        <div class="coupon__service__category">
          <div class="coupon__service">国内宿泊</div>
          <div class="coupon__category">紅葉スポット</div>
        </div>
        <div class="coupon__price">
          <span>25</span>%OFF
        </div>
        <div class="coupon__get">宿クーポンを獲得する</div>
      </div>
    </a>
  </div>
  
  <div class="coupon__button__pattern coupon__button__pattern-button1a">
    <div class="coupon__amount__condition">
      <div class="coupon__amount">先着利用5,000枚</div>
      <div class="coupon__condition">利用条件を確認</div>
    </div>
    <div class="coupon__button">
      <a href="対象施設検索URL">対象施設を見る</a>
    </div>
  </div>
  
  <div class="tableholderCpn">
    <table>
      <tbody>
        <tr>
          <td>予約対象期間</td>
          <td>2025/10/01～2025/11/30</td>
        </tr>
        <tr>
          <td>対象施設</td>
          <td>紅葉スポット周辺の対象宿泊施設</td>
        </tr>
        <!-- 他の条件も追加 -->
      </tbody>
    </table>
  </div>
</div>
```

#### 手順3: 完成!

これで新しいページができました。

---

## 💡 よくある質問

### Q1: CSSファイルは毎回作る必要がある?

**A**: いいえ! 同じデザインなら `css/contents_pc.css` と `css/contents_sp.css` を使い回せます。

### Q2: 複数のクーポンを表示したい場合は?

**A**: SSIファイルの中で `<div class="couponOneClick">...</div>` を繰り返すだけです:

```javascript
const allssi = {
  coupon_01: "ssi/koyo.html",  // ← この1ファイルに複数のクーポンを書く
};
```

または、複数のSSIファイルを読み込むこともできます:

```javascript
const allssi = {
  coupon_01: "ssi/koyo_coupon1.html",
  coupon_02: "ssi/koyo_coupon2.html",
  coupon_03: "ssi/koyo_coupon3.html",
};
```

```html
<div id="coupon_01"></div>
<div id="coupon_02"></div>
<div id="coupon_03"></div>
```

### Q3: 色を変えたい場合は?

**A**: CSSファイルで以下の部分を変更:

```css
/* 濃紺の背景色を変える */
#getAllCoupon{ background: #213153; }  /* ← この色コードを変更 */

/* ボタンの色を変える */
.cpn-all-click-btns{ background: #bf0000; }  /* ← この色コードを変更 */
```

---

## 📦 チートシート: コピペ用パーツ集

### パーツ1: シンプルなボタン

```html
<div class="cpn-all-click">
  <button class="cpn-all-click-btns">ボタンテキスト</button>
</div>
```

### パーツ2: リンク付きボタン

```html
<div class="coupon__button">
  <a href="リンク先URL">ボタンテキスト</a>
</div>
```

### パーツ3: ガイドリンク

```html
<div class="coupon__filter__guide">
  <a href="リンク1" target="_blank">リンクテキスト1</a>
  <a href="リンク2" target="_blank">リンクテキスト2</a>
</div>
```

### パーツ4: セクションタイトル

```html
<h2 class="ttl">タイトルテキスト</h2>
```

---

## ✅ まとめ

このコードの良いところ:

1. **HTMLとCSSとコンテンツが分離**している
2. **パーツを組み合わせ**て新しいページが作れる
3. **デザインの統一**が簡単
4. **メンテナンスしやすい**

新しいページを作る時は:

1. HTMLファイルをコピー
2. SSIファイルをコピー
3. 中身のテキストだけ変更

これだけで、同じデザインの新しいページが完成します! 🎉
