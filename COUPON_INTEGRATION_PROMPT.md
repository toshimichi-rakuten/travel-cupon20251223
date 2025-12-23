# 楽天トラベル まとめてクーポンコンポーネント 組み込みプロンプト

以下のクーポンコンポーネントを既存のページに組み込んでください。

## 必要な依存ファイル

### 1. 外部CSS（head内に追加）
```html
<!-- 楽天トラベル共通CSS -->
<link rel="stylesheet" href="https://img.travel.rakuten.co.jp/share/common/css/style-pc.css" media="screen and (min-width: 721px)">
<link rel="stylesheet" href="https://img.travel.rakuten.co.jp/share/common/css/style-sp.css" media="screen and (min-width: 0px) and (max-width: 720px)">

<!-- クーポン専用CSS -->
<link rel="stylesheet" href="https://img.travel.rakuten.co.jp/share/assets/css/coupon/coupon_simple.css" media="all">

<!-- Google Fonts -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Nanum+Gothic&family=Noto+Sans+JP:wght@100..900&family=Noto+Serif+JP:wght@200..900&display=swap" rel="stylesheet">
```

### 2. カスタムCSS（head内に追加、またはcss/ディレクトリに配置）

**PC用CSS（css/contents_pc.css）:**
```css
.sp { display: none !important; }
#widewrapper{width: 100%; position: relative; clear: both; font-family: 'メイリオ', 'Meiryo';}
.ss-container{ margin: 40px 0 0; border-radius: 0 !important;}

a:hover { opacity: 0.8; text-decoration: none !important; }

/* coupon */
#getAllCoupon{ margin: 0; padding: 32px 0 40px; background: #213153;}
#getAllCoupon .txt{color: #FFF; font-size: 36px; font-weight: 500; text-align: center; line-height: 140%; letter-spacing: 1.44px; position: relative;}
#getAllCoupon .txt::after{ display: block; content: ""; width: 220px; height: 1px; background: #fff; position: absolute; left: 50%; top: 60px; transform: translateX(-50%);}
#getAllCoupon .txt span{ display: block; margin-top: 40px; font-size: 20px;line-height: 140%; letter-spacing: 1.6px;}
#getAllCoupon .txt2{ color: #fff; font-size: 12px; line-height: 1.6; margin-top: 12px;}
.getAllCoupon{ display: flex; justify-content: center; align-items: center; flex-direction: column;}
.cpn-all-click{display: flex;justify-content: center; margin: 20px auto 0;}
.cpn-all-click-btns{background: #bf0000; color: #fff; display: block; padding: 16px 0; font-size: 24px; border: none; border-radius: 100rem; width: 425px; line-height: 1; font-family: inherit; position: relative;}
.cpn-all-click-btns::after{ content: ""; position: absolute; right: 8%; top: 50%; width: 10px; height: 10px; border-top: 2px solid #fff; border-right: 2px solid #fff; transform: translateY(-50%) rotate(45deg);}
.cpn-all-click-btns:hover{opacity: .8; cursor: pointer;}
.cpn-all-click-btns.acquired, .cpn-all-click-btns.finished, .cpn-all-click-btns.expired{background: #666; color: #fff; cursor: not-allowed;}

.coupon__filter__guide{ margin: 24px 0 0; justify-content: flex-start;}
.coupon__filter__guide::after{ background-image: url(https://img.travel.rakuten.co.jp/special/special-offers/images/modal_svg.svg);display: none;}
.coupon__filter__guide a{ padding: 4px 32px 4px 8px; background: #D9D9D9 url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACEAAAAiCAMAAADmrkDzAAAARVBMVEUAAAAwMDAwMDAwMDAxMTEzMzMyMjIzMzMzMzMyMjIzMzM1NTUyMjIwMDAzMzMzMzMyMjIxMTEyMjIzMzMyMjI0NDQzMzP51LwrAAAAFnRSTlMAIEAwoJ+Av+9/r2BgEFDP3x9w3+9Aa03MBwAAAHlJREFUeNrdykUSQkEUA8DvriPv/kfFSRhSxQ7rdWcfkhdQylEZ1HI07VWHofXGQ4cBQ4dxwpjzq5lDhrF0djVxoLHadrVQ4LHZnl0hyMFBDw56cNCDA+PBQQ9HQY95RRCDuM29GI01fzzahE+Gsychzx7EKTVnb3YA6mQP/gr9fQ8AAAAASUVORK5CYII=) no-repeat 96% center / 16px; color: #213153;}
.couponlink{ display: flex; justify-content: center; align-items: center; margin: 20px auto 0;}
.couponlink a{ display: block; padding: 12px 50px 12px 24px; border: 1px solid #D9D9D9; border-radius: 3px; font-size: 14px; color: #fff; position: relative;}
.couponlink a::after{ content: ""; position: absolute; right: 8%; top: 25%; width: 10px; height: 10px; border-top: 2px solid #fff; border-right: 2px solid #fff; transform: rotate(135deg);}

#coupon{background: #F5F5F5; padding:64px 0; margin-top: 0;}
#coupon .ttl { font-family: 'Noto Serif JP', serif; color: #000; text-align: center; font-size: 24px; font-style: normal; font-weight: 600; line-height: 100%; }
```

**スマホ用CSS（css/contents_sp.css）:**
```css
.pc { display: none !important; }
#widewrapper{width: 100%; position: relative; clear: both; font-family: 'メイリオ', 'Meiryo',sans-serif;}
.ss-container{ margin: 32px 0 0; padding: 0; border-radius: 0 !important;}

/* coupon */
#getAllCoupon{ margin: 0; padding: 16px; background: #213153;}
#getAllCoupon .txt{color: #FFF; font-size: 24px; font-weight: 500; text-align: center; line-height: 140%; letter-spacing: 1.2px; position: relative;}
#getAllCoupon .txt::after{ display: block; content: ""; width: 200px; height: 1px; background: #fff; position: absolute; left: 50%; top: 85px; transform: translateX(-50%);}
#getAllCoupon .txt span{ display: block; text-align: center; margin-top: 36px; font-size: 16px; line-height: 140%; letter-spacing: 1.6px;}
#getAllCoupon .txt2{ color: #fff; font-size: 12px; line-height: 1.6; margin-top: 12px;}
.cpn-all-click{display: flex;justify-content: center;gap: 20px; margin: 20px auto;}
.cpn-all-click-btns{background: #bf0000; color: #fff; display: block; padding: 16px 0; font-size: 16px; border: none; border-radius: 100rem; width: 80%; max-width: 276px; line-height: 1; font-family: inherit; position: relative;}
.cpn-all-click-btns::after{ content: ""; position: absolute; right: 8%; top: 50%; width: 8px; height: 8px; border-top: 1px solid #fff; border-right: 1px solid #fff; transform: translateY(-50%) rotate(45deg); }
.cpn-all-click-btns:hover{opacity: .8; cursor: pointer;}
.cpn-all-click-btns.acquired, .cpn-all-click-btns.finished, .cpn-all-click-btns.expired{background: #666; color: #fff; cursor: not-allowed;}
.couponOneClick{ margin-top: 24px;}

.coupon__filter__guide{ margin: 24px 0 0;}
.coupon__filter__guide::after{ background-image: url(https://img.travel.rakuten.co.jp/special/special-offers/images/modal_svg.svg);display: none;}
.coupon__filter__guide a{ padding: 4px 28px 4px 8px; background: #D9D9D9 url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACEAAAAiCAMAAADmrkDzAAAARVBMVEUAAAAwMDAwMDAwMDAxMTEzMzMyMjIzMzMzMzMyMjIzMzM1NTUyMjIwMDAzMzMzMzMyMjIxMTEyMjIzMzMyMjI0NDQzMzP51LwrAAAAFnRSTlMAIEAwoJ+Av+9/r2BgEFDP3x9w3+9Aa03MBwAAAHlJREFUeNrdykUSQkEUA8DvriPv/kfFSRhSxQ7rdWcfkhdQylEZ1HI07VWHofXGQ4cBQ4dxwpjzq5lDhrF0djVxoLHadrVQ4LHZnl0hyMFBDw56cNCDA+PBQQ9HQY95RRCDuM29GI01fzzahE+Gsychzx7EKTVnb3YA6mQP/gr9fQ8AAAAASUVORK5CYII=) no-repeat 98% center / 16px; color: #213153;}
.couponlink{ display: flex; justify-content: center; align-items: center; margin: 20px auto 0;}
.couponlink a{ display: block; padding: 8px 40px 8px 16px; border: 1px solid #D9D9D9; border-radius: 3px; font-size: 14px; color: #fff; position: relative;}
.couponlink a::after{ content: ""; position: absolute; right: 8%; top: 25%; width: 10px; height: 10px; border-top: 1px solid #fff; border-right: 1px solid #fff; transform: rotate(135deg);}

#coupon{background: #F5F5F5; padding:24px 0; margin-top: 0;}
#coupon .ttl { font-family: 'Noto Serif JP', serif; color: #000; text-align: center; font-size: 20px; font-style: normal; font-weight: 600; line-height: 100%; }
.coupon__box__holder{ padding: 0 30px}
```

これらのCSSを既存ページに追加する場合：
```html
<link rel="stylesheet" href="css/contents_pc.css" media="all and (min-width: 721px)">
<link rel="stylesheet" href="css/contents_sp.css" media="all and (min-width: 0px) and (max-width: 720px)">
```

### 3. JavaScript（body閉じタグの前に追加）
```html
<!-- jQuery（すでに読み込まれている場合は不要） -->
<script type="text/javascript" src="https://img.travel.rakuten.co.jp/share/common/js/lib/jquery/jquery.js"></script>

<!-- タイル表示用 -->
<script src="https://img.travel.rakuten.co.jp/special/smap/js/jquery.tile.js" type="text/javascript"></script>

<!-- 楽天モジュール -->
<script type="text/javascript" src="https://a.ichiba.jp.rakuten-static.com/com/js/d/Rmodules/Rmodules.min.js?v=1.4.0"></script>

<!-- クーポンワンクリック獲得 -->
<script src="https://r.r10s.jp/com/js/d/coupon/one_click_acquisition/1.1/one_click_acquisition-1.1.0.min.js" type="text/javascript"></script>

<!-- クーポンカウントダウン -->
<script src="https://img.travel.rakuten.co.jp/share/assets/js/coupon/coupon_countdown.js"></script>

<!-- まとめてクーポン用設定 -->
<script>
  const allssi = {
    coupon_01: "ssi/coupon.html",  // クーポンHTMLファイルのパス（必要に応じて変更）
  };
</script>

<!-- まとめてクーポン獲得機能 -->
<script src="https://img.travel.rakuten.co.jp/share/assets/js/coupon/allClickMerge.min.js"></script>
```

## HTMLコンポーネント

### メインHTMLコード（body内に配置）
```html
<div id="widewrapper">
  
  <!-- まとめてクーポン獲得セクション -->
  <section class="ss-container" id="getAllCoupon">
    <p class="txt">クーポン併用で<br class="sp">最大30%OFF<span>最高級宿スペシャルオファー<br class="sp">限定クーポン！</span></p>
    <div class="getAllCoupon">
      <div class="cpn-all-click">
        <button id="cpn-madome" class="cpn-all-click-btns">まとめてクーポンを獲得</button>
      </div>
      <!-- 一括獲得の機能、削除しないでください -->
      <div>
        <div id="allClick"></div>
      </div>
      <!-- 一括獲得の機能、削除しないでください -->
      <div class="coupon__filter__guide">
        <a href="https://coupon.rakuten.co.jp/myCoupon?service=travel" target="_blank">獲得済みクーポン一覧</a>
        <a href="https://travel.rakuten.co.jp/coupon/guide/help.html?l-id=beginner_help" target="_blank">クーポンの使い方</a>
      </div>
      <p class="txt2">※20%OFF宿クーポンと10%OFF楽天トラベルクーポンの併用で最大30%OFFとなります。<br>
        ※クーポンの利用条件・対象施設・併用可否は各クーポンで異なります。<br>
        各クーポンの「利用条件を確認」で詳細をご確認ください。</p>
    </div>
    <p class="couponlink"><a href="#coupon">すべてのクーポンをみる</a></p>
  </section>

  <!-- クーポン一覧セクション -->
  <section class="ss-container" id="coupon">
    <h2 class="ttl">最高級宿スペシャルオファーで<br class="sp">使えるクーポン</h2>
    <div class="coupon__box">
      <div class="coupon__box__holder">
        <div id="coupon_01"></div>
      </div>
    </div>
  </section>

</div>
```

## 個別クーポンHTMLファイル（ssi/coupon.html）

ssiディレクトリを作成し、以下のファイルを配置してください：

**ssi/coupon.html の内容：**
個別のクーポンカードHTMLコード（.couponOneClick要素）を配置します。
各クーポンは以下の構造を持ちます：

```html
<div class="couponOneClick" data-coupon-authkey="認証キー" data-filterItem="dh" data-start="開始日時" data-end="終了日時">
  <div class="coupon__container">
    <a href="クーポン取得URL" class="couponOneClick-default">
      <div class="coupon__content">
        <div class="coupon__service__category">
          <div class="coupon__service">国内宿泊</div>
          <div class="coupon__category">カテゴリー名</div>
        </div>
        <div class="coupon__price">
          <span>割引率数値</span>%OFF
        </div>
        <div class="coupon__get">クーポンを獲得する</div>
      </div>
    </a>
    <span class="couponOneClick-acquired coupon__cover"><span>獲得しました</span></span>
    <span class="couponOneClick-having coupon__cover"><span>獲得済みです</span></span>
    <span class="couponOneClick-expired coupon__cover"><span>終了しました</span></span>
    <span class="couponOneClick-finished coupon__cover"><span>先着利用上限に達しました</span></span>
  </div>
  <div class="coupon__time" start_time="開始日時" end_time="終了日時">
    <p class="coupon__time__start"><span>開始日時表示</span>から利用開始</p>
  </div>
  <div class="coupon__button__pattern coupon__button__pattern-button1a">
    <div class="coupon__amount__condition">
      <div class="coupon__amount">先着利用枚数</div>
      <div class="coupon__condition">利用条件を確認</div>
    </div>
    <div class="coupon__button">
      <a href="対象施設検索URL">対象施設を見る</a>
    </div>
  </div>
  <div class="tableholderCpn">
    <table>
      <tbody>
        <!-- クーポン詳細情報 -->
      </tbody>
    </table>
  </div>
</div>
```

## 重要な注意事項

### ✅ 必須要素
1. **`#widewrapper`** - すべてのコンテンツを囲む親要素
2. **`#getAllCoupon`** - まとめて獲得セクション（削除しないでください）
3. **`#allClick`** - 一括獲得機能用のdiv（削除しないでください）
4. **`#coupon_01`** - 個別クーポンを読み込むためのdiv（allssiオブジェクトのキーと一致させる）
5. **allssi設定** - JavaScriptでクーポンHTMLファイルのパスを指定

### 🔧 カスタマイズ可能な箇所
- タイトルテキスト（`.txt`内の文言）
- 注釈テキスト（`.txt2`内の文言）
- クーポン詳細（ssi/coupon.html内のクーポン情報）
- リンク先URL（各ボタンやリンクのhref属性）
- 背景色やフォントサイズ（CSSで調整可能）

### 📂 ファイル構成
```
your-project/
├── index.html（または既存ページ）
├── css/
│   ├── contents_pc.css
│   └── contents_sp.css
└── ssi/
    └── coupon.html
```

### 🎨 スタイルのカスタマイズ
- PC/SPで異なるスタイルが適用されます（メディアクエリ: 721px）
- `.sp`クラス：スマホのみ表示
- `.pc`クラス：PCのみ表示
- 背景色、ボタン色、フォントサイズなどは対応するCSSファイルで変更可能

### 🔗 依存関係の順序
1. jQuery
2. Rmodules
3. one_click_acquisition
4. coupon_countdown
5. allssi設定（const allssi）
6. allClickMerge

この順序を守って読み込んでください。

---

## 実装手順

1. **head内に外部CSSとGoogle Fontsを追加**
2. **カスタムCSS（contents_pc.css、contents_sp.css）を作成・配置し、head内でリンク**
3. **body内の任意の位置にHTMLコンポーネントを配置**
4. **ssiディレクトリを作成し、coupon.htmlを配置**
5. **body閉じタグの前にJavaScriptを追加（依存関係の順序を守る）**
6. **allssiオブジェクトでクーポンHTMLファイルのパスを正しく指定**
7. **プレビューで動作確認**

以上で、クーポンコンポーネントの組み込みは完了です。
