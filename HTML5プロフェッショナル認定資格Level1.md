



 





HTML5プロフェッショナル認定資格Level1合格記

### 1.1 Webの基礎知識

##### lang

```
<!DOCTYPE html>
<html lang="[       ja 　]">
```



##### XHTML

HTML5はXHTML書式を利用できます。
その際、html要素にはデフォルト名前空間としてxmlns属性で「http://www.w3.org/1999/xhtml」を指定する必要があります。
要素名や属性名は全て小文字で記述する必要があります。
属性の値は「"」や「'」で囲む必要があります。
xhtml要素という要素はいずれのXHTML仕様にも存在しません



##### meta要素

グローバル属性を除けば、meta要素に指定可能な属性は次の4つのみです。
・http-equiv
・name
・content
・charset
scheme属性は、HTML 4.01 や XHTML 1.0 では指定可能でしたが、HTML5以降では指定できなくなっています。

<meta http-equiv="Content-Type" content="text/html; charset=utf-8">

文字エンコーディングを設定するために有効な書式

- <meta charset="UTF-8">

- <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">

##### cookie

- HTTP cookieによりステートフルなサービスを可能にする。
- HTTP cookieは通信時はHTTPヘッダに含まれる。
- HTTP cookieはクライアントに保存される。
- HTTP cookieのサイズは4KBである。

HTTP cookieに有効期限がないと削除しない限り残り続ける。

您可以为 cookie 设置一个过期日期，过期日期后，存储的 cookie 将失效。如果指定了失效日期，即使在失效日期内关闭浏览器也会保存，但如果未指定，则在浏览器关闭时将被删除。 

##### クロスサイトスクリプティング（XSS）

跨站脚本（XSS）是利用目标网站的漏洞，设置脚本引导攻击者进入恶意站点，窃取访问该站点的用户个人信息的一种攻击。 之所以使用此名称，是因为它将访问受困网站的用户定向到易受攻击的网站（跨站点）并进行信息利用等攻击。

简而言之，它是一种“在用户访问网页时执行恶意脚本的漏洞或攻击技术”。

攻击者未经授权的登录（欺骗）

クロスサイト・スクリプティング(XSS: Cross Site Scripting)は掲示板など、ユーザーからの入力値を元に動的にWebページを表示するサイトに悪意のあるスクリプトを埋め込み、ユーザーの環境で実行させます。こうすることで、個人情報を搾取するフィッシングや、そのユーザーのふりをする「なりすまし」などを行います。
クロスサイト・スクリプティングへの対策は、悪意のあるスクリプトが表示、実行されないように出力値を適切にエスケープ処理(特別な意味を持つ文字列を一定のルールに従って別の文字列に置き換える)することです。

サニタイジング（エスケープ）処理をする

サニタイジング（エスケープ）処理とは、「<」や「“」といった区切りやタグなどの意味を持つ文字を、意味を持たない文字列に置き換え無害化する行為を指します。サニタイジング（エスケープ）処理をすることで、スクリプトが意図せずに挙動してしまうことを防ぐことができます。

解决方法：出力値を適切にエスケープ処理する

##### クロスサイトリクエストフォージェリ（CSRF）

跨站请求伪造 (CSRF) 是存在于 Web 应用程序中的漏洞或利用该漏洞的攻击方法。处理公告板和查询表单的 Web 应用程序接收并处理来自其他站点的应拒绝的请求。 攻击方式/特点 攻击者准备一个攻击网页并诱使用户访问它。 当用户访问攻击网页时，攻击网页中预先准备好的恶意请求被发送到攻击目标服务器。 攻击目标服务器上的Web应用程序处理恶意请求，并进行用户不希望的处理。

简而言之，“允许 Web 应用程序用户执行非预期处理的漏洞或攻击方法”

クロスサイト・リクエスト・フォージェリ(CSRF)
攻撃用サイトにアクセスしたユーザーの環境から攻撃者が用意したHTTPリクエストを送信させることによって、不正な操作を実行します。

解决方法：サーバ側で外部サイトからのリクエストを受け付けないようにする

SQLインジェクション解决方法：ユーザーの入力値を適切にエスケープ処理するか、プリペアードステートメントを使用する

HTTPヘッダ・インジェクション解决方法：改行として認識される特殊文字をエスケープ処理したり、改行が含まれていたら入力エラーとする

##### XSSとCSRFの違い

| 観点             | XSS                   | CSRF                       |
| :--------------- | :-------------------- | :------------------------- |
| 脆弱性の存在箇所 | Webアプリ             |                            |
| 実行契機         | 不正なURLへのアクセス |                            |
| 実行される場所   | Webブラウザ (Client)  | Webアプリサーバ (Server)   |
| 実行可能な処理   | 基本的に自由*1        | Webアプリで 定義された処理 |
| 実行の前提       | 特になし              | Webアプリに ログイン済み*2 |

##### link 要素の rel 属性

- <link rel="stylesheet" href="/default.css" type="text/css">
- <link rel="canonical" href="https://example.com/">
- <link rel="stylesheet" href="style.css">
- <link rel="stylesheet" href="style.css" type="text/css">

##### 画像

- BMP（位图图像）是在 Windows 中创建的图像格式，不能在 Web 上使用。 

- JPEG（联合图像专家组）的特点是可以表现全色和精美表现层次。
-  -PNG（便携式网络图形）可以像 JPEG 一样表达全彩，但文件大小可能比 JPEG 大。与 JPEG 不同，背景可以是透明的。 -GIF（Graphics Interchange Format）可以使背景透明，可以做动画，但最多只能表达256种颜色。过去，透明 GIF 存在许可问题，因此开发了 PNG。 除了上述之外，还有一种格式叫做TIFF（Tagged Image File Format）。适用于高分辨率图像，但尺寸较大

画像ファイルの形式(フォーマット)には、主に次のようなものがあります。

![【図を表示】](https://ping-t-data-tokyo.s3.ap-northeast-1.amazonaws.com/uploads/question_image/file/7702/k31338.jpg?X-Amz-Expires=600&X-Amz-Date=20210924T145107Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZCJ2QHLF73X4YH6P%2F20210924%2Fap-northeast-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=0e70a6b012102902b7e8fd7ceaf9dd3a9d09928fc62b80cd723a7ef63f8f91d9)

##### セクショニング

![要素カテゴリーの関係図](http://html5.cyberlab.info/content-models/sectioning-content.png)

- セクショニング・ルートの要素は下記の6つです。

  body, blockquote, details, fieldset, figure, td

  HTML5での要素ごとのカテゴリーの1つである「セクショニング・コンテンツ」には、文書のセクションを表す要素が属します。
  セクショニング・コンテンツの要素は下記の4つです。

  article, aside, nav, section

##### fieldset

**HTML の `<fieldset>` 要素**は、ウェブフォーム内のラベル ([``](https://developer.mozilla.org/ja/docs/Web/HTML/Element/label)) などのようにいくつかのコントロールをグループ化するために使用します。

```
<form>
  <fieldset>
    <legend>Choose your favorite monster</legend>

    <input type="radio" id="kraken" name="monster">
    <label for="kraken">Kraken</label><br/>

    <input type="radio" id="sasquatch" name="monster">
    <label for="sasquatch">Sasquatch</label><br/>

    <input type="radio" id="mothman" name="monster">
    <label for="mothman">Mothman</label>
  </fieldset>
</form>
```



##### Other

HTML5の文書型宣言の基本形は、「<!DOCTYPE」＋1個以上のスペース＋「HTML」＋0個以上のスペース＋「>」です。アルファベットは大文字でも小文字でもかまいません。

!doctype html>  <!DOCTYPE HTML > <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01//EN"

Data URIは、通常外部ファイルへのURIを記述する、imgタグのsrc属性やCSSのurl()に直接画像データなどを埋め込むための技術です。
Data URIはデータの場所を指すものではありませんので、B.の説明は間違っています。

SSL/TLSの規格として古い順：SSL 1.0,SSL 2.0,SSL 3.0,TLS 1.0,TLS 1.1,TLS 1.2



### 1.2 CSS

##### link要素 

外部スタイルシートを読み込む際は次のように記述します。

<link rel="stylesheet" href="style.css" type="text/css">

rel属性の値が「stylesheet」の場合は、type属性はデフォルト値「text/css」が適用されるため省略できます。
rel="値は下記の表を参照": HTML文書とリンク先の関係
href="URL": リンク先のURL
type="MIMEタイプ": リンク先のMIMEタイプ(ファイル形式を示す識別子)
media="メディアタイプ": 適用するメディアの種類
hreflang="言語コード": リンク先の言語

![img](https://ping-t-data-tokyo.s3.ap-northeast-1.amazonaws.com/uploads/question_image/file/7600/k30969.jpg?X-Amz-Expires=600&X-Amz-Date=20210915T150531Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZCJ2QHLF73X4YH6P%2F20210915%2Fap-northeast-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=42b5c1a70fce041d336408a192be15804d546ab8791978400cc5c200a84e0730)

また、rel属性は半角スペースで区切って複数の値を指定できます。

例) alternateとstylesheetを組み合わせて、代替スタイルシート(ユーザがページのスタイルを選択できる)を提供する
<link rel="stylesheet" href="default.css" title="Default Style">

##### CSSのcolor

プロパティは文字の色を指定します。
これまでの分野で紹介してきた、色をキーワード(redやblueなどの英語名)で指定する方法の他にも、以下の指定方法があります。

・16進数
RGBを16進数で表します。RGBとは、赤(Red)、緑(Green)、青(Blue)の3つの原色を組合わせて多くの色を表現する方法です。
「#」の後にRGBの各値を2桁ずつの16進数に置き換え、6桁の16進数で表します。
例) 赤 -> #FF0000

RGBの各値の2桁がそれぞれ同じ値である場合は、3桁で表すこともできます。

例) 赤 -> #FF0000 -> #F00

下表は主な色の対応です。
![<img src="/mondai3/img/jpg/k31163.jpg">](https://ping-t-data-tokyo.s3.ap-northeast-1.amazonaws.com/uploads/question_image/file/7645/k31163.jpg?X-Amz-Expires=600&X-Amz-Date=20210924T144940Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZCJ2QHLF73X4YH6P%2F20210924%2Fap-northeast-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=1525a7bcfd6919f6d3c0fc629037849131a57b17476efb6352814cbefcad2d9f)



##### セレクタ

CSS(Cascading Style Sheets: Webページの装飾やレイアウトを記述するための言語)の基本的な書式は以下のとおりです。

セレクタ{プロパティ名: プロパティ値;}

セレクタ(要素など、スタイルを適用する対象)を「,」(カンマ)で区切って複数指定すると、複数の異なるセレクタに同じスタイルを適用することができます。これを「グループ化」といいます。
その他にも「結合子」を使用してセレクタを組合せることで、より複雑にセレクタを指定できます。

CSSの結合子には、次の種類があります。

|    cssセレクタの書き方    | 左記例の意味 |                                  |
| :-----------------------: | :----------: | -------------------------------- |
| p **,** a { color: red; } |  「または」  | p要素とa要素を赤文字する         |
|   p  a { color: red; }    |    「子」    | p要素内のa要素を赤文字する       |
| p **>** a { color: red; } | 「直下の子」 | p要素内の直下のa要素を赤文字する |
| p **+** a { color: red; } |   「隣接」   | p要素と隣り合うa要素を赤文字する |
| p **~** a { color: red; } |   「以降」   | p要素以降のa要素を赤文字する     |

・属性セレクタ
CSS3(2011年から策定が進んでいるCSSのバージョン)では次の書式が使用できます。

■[属性名] ---この属性名が指定されている要素(属性値は考慮しない)
例) class属性を持つ全てのp要素の文字を赤色にする
p[class]{color:red;}

■[属性名="属性値"] ---この属性名と属性値が指定されている要素(属性値が完全一致)
例) class属性の値が「foo」であるp要素の文字を赤色にする
p[class="foo"]{color:red;}

■[属性名~="属性値"] ---この属性名と属性値が指定されている要素(複数の属性値のうちの一つが一致すればよい)
例) class属性の値の1つが「foo」であるp要素の文字を赤色にする
p[class~="foo"]{color:red;}

■[属性名|="属性値"] ---この属性名と属性値が指定されている要素(属性値の1つ、または「-」(ハイフン)区切りの属性値の前半が一致、言語コード「ja-JP」など)
例) lang属性の値が「en」(英語)であるblockquote要素の文字を赤色にする
blockquote[lang|="en"]{color:red;}

■[属性名^="属性値の始め"] ---この属性名の属性値が「属性値の始め」で始まる要素
例) class属性の値が「foo」で始まるp要素の文字を赤色にする
p[class^="foo"]{color:red;}

■[属性名"属性値の終わり"] ---この属性名の属性値が「属性値の終わり」で終わる要素
例) id属性の値が「2」で終わるp要素の文字を赤色にする
p[id$="2"]{color:red;}

■[属性名*="属性値の一部"] ---この属性名の属性値が「属性値の一部」の文字列を含む要素
例) id属性の値が「aa」を含むp要素の文字を赤色にする
p[id*="aa"]{color:red;}



##### 優先順位

1、内嵌样式 > 内部样式表 > 外联样式表
 2、important > 内嵌样式 > ID > 类 > 标签 | 伪类 | 属性选择 > 伪对象 > 继承 > 通配符。
 important的权重为1,0,0,0
 ID的权重为0,1,0,0
 类的权重为0,0,1,0
 标签的权重为0,0,0,1
 伪类的权重为0,0,1,0
 属性的权重为0,0,1,0
 伪对象的权重为0,0,0,1
 通配符的权重为0,0,0,0

|   指定方法   |        例        |  点数   |
| :----------: | :--------------: | :-----: |
|  style属性   |     style=""     | 1.0.0.0 |
|      ID      |      #main       | 0.1.0.0 |
|    クラス    |      .entry      | 0.0.1.0 |
| 属性セレクタ | [href*="google"] | 0.0.1.0 |
|  疑似クラス  |      :hover      | 0.0.1.0 |
|    要素名    |        h1        | 0.0.0.1 |
|   擬似要素   |   :first-line    | 0.0.0.1 |

- 主要な擬似要素

  - [１．A:: first-letter（要素の一文字目を指定）](https://www.asobou.co.jp/blog/web/css2#A_first-letter)
  - [２．A:: first-line（要素の一行目を指定）](https://www.asobou.co.jp/blog/web/css2#A_first-line)
  - [３．A::before（要素の直前にコンテンツを追加）](https://www.asobou.co.jp/blog/web/css2#Abefore)
  - [４．A::after（要素の直後にコンテンツを追加）](https://www.asobou.co.jp/blog/web/css2#Aafter)

  指定目标元素的一部分并应用装饰，或向目标元素添加伪元素并应用装饰的选择器称为伪元素。

- 主要な擬似クラス

  - [１．A:link（未訪問のリンク要素の指定）](https://www.asobou.co.jp/blog/web/css2#Alink)

  - [２．A:visited（訪問済のリンク要素の指定）](https://www.asobou.co.jp/blog/web/css2#Avisited)

  - [３．A:hover（要素にマウスがホバーした際の指定）](https://www.asobou.co.jp/blog/web/css2#Ahover)

  - [４．A:active（要素がアクティブ状態になった際の指定）](https://www.asobou.co.jp/blog/web/css2#Aactive)

  - [５．A:nth-child(n)（親要素内のn番目の要素の指定）](https://www.asobou.co.jp/blog/web/css2#Anth-childnn)

  - [６．A:nth-of-type(n)（親要素内の同じ種類の要素の中のn番目の要素）](https://www.asobou.co.jp/blog/web/css2#Anth-of-typenn)

  - [７．A:not(B)（B以外の要素の指定）](https://www.asobou.co.jp/blog/web/css2#AnotBB)

    CSS **伪类** 是添加到选择器的关键字，指定要选择的元素的特殊状态。例如，[`:hover`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:hover) 可被用于在用户将鼠标悬停在按钮上时改变按钮的颜色。

    https://www.asobou.co.jp/blog/web/css2

##### border-collapse

```
collapse
```

隣接するセルで境界線を共有します (collapsed-border 表レンダリングモデル)。

```
separate
```

隣接するセルが個別に境界線を持ちます (separated-border 表レンダリングモデル)。

- border-collapseの値が「collapse」だとborder-radiusは無効になる

##### CSSの @import 

- @import "style.css";
- @import 'style.css';
- @import url("style.css");
- @import url('style.css');
- @import url(style.css);





##### transform

| No   | 関数      | 読み方         | 変形効果 | 2D（XY方向） | 3D（XYZ方向） |
| :--- | :-------- | :------------- | :------- | :----------- | :------------ |
| 01   | translate | トランスレイト | 移動     | ○            | ○             |
| 02   | rotate    | ローテート     | 回転     | ○            | ○             |
| 03   | scale     | スケール       | 伸縮     | ○            | ○             |
| 04   | skew      | スキュー       | 傾斜     | ○            | －            |

https://creive.me/archives/16145/

##### アニメーション

```html
			/* 背景にトランジションの効果を適用する */
			transition-property:background-color;
			/* 変化するのに5秒かかるように指定する */変化するのにかかる時間
			transition-duration:5s;
			/* 一定速度で変化するように指定する */transition-timing-functionは、加速したり減速したりして変化のタイミングを調整します。
			transition-timing-function:linear;
			/* 2秒後に変化を開始する */
			transition-delay:2s
```

animationプロパティは、以下の8つのanimation関連のプロパティをまとめて指定できます。

animation-nameは、実行するアニメーションとして、@keyframesで定義したキーフレームの名前を指定します。
animation-durationは、アニメーションの再生時間を指定します。
animation-timing-functionは、アニメーションの再生速度を加速したり減速したりしてタイミングを調整します。
animation-delayは、アニメーションの再生を開始する時間を遅らせます。
animation-iteration-countは、アニメーションの再生を繰り返す回数を指定します。
animation-directionは、アニメーションを逆再生するかどうかを指定します。
animation-play-stateは、アニメーションの再生・一時停止を指定します。
animation-fill-modeは、animation-delayでアニメーションの再生が遅延されている間(再生の開始前)や、再生の終了後にどのような状態で表示するのかを指定します。

【animation】
animationは、上述した8つのアニメーション関連のプロパティをまとめて指定できます。
各値は半角スペースで区切って順不同で指定しますが、時間を示す値については1つ目が「animation-duration」、2つ目が「animation-delay」と認識されます。





##### white-space

|                                                              | 改行 | まとめ | 折り返し   |              |
| ------------------------------------------------------------ | ---- | ------ | ---------- | ------------ |
| -------------------------------------------------------------- |      |        |            |              |
| normal                                                       | ｜   | しない | まとめる   | 折り返す     |
| pre                                                          | ｜   | する   | まとめない | 折り返さない |
| nowrap                                                       | ｜   | しない | まとめる   | 折り返さない |
| pre-wrap                                                     | ｜   | する   | まとめない | 折り返す     |
| pre-line                                                     | ｜   | する   | まとめる   | 折り返す     |
|                                                              |      |        |            |              |

##### 相対的な単位

em: フォントサイズを1とする
rem: ルート要素(html要素)のフォントサイズを1とする
ex: 小文字のxの高さを1とする

|   値   |                             メモ                             |
| :----: | :----------------------------------------------------------: |
|  pre   |       改行、半角スペース、タブ文字をそのまま表示する。       |
| nowrap | 改行、半角スペース、タブ文字を半角スペースに置き換えて表示する。 囲われているボックスからはみ出す場合でも自動改行はされない。 |
| normal | 改行、半角スペース、タブ文字を半角スペースに置き換えて表示する。 囲われているボックスからはみ出す場合は自動改行される。 |

![image-20210924225735651](/Users/gaoyunhu/Library/Application Support/typora-user-images/image-20210924225735651.png)



##### type child

https://kansai.weblab.co.jp/blog/tech/css-pseudo-num/

セレクタ(スタイルを適用する対象)には、特定の要素名と疑似クラスを連結して指定できます。
疑似クラスは、指定した要素が特定の状態である場合に適用対象とします。

[xxx-of-type 和 xxx-child 的区别] 两者之间有以下区别。 -Xxx-of-type 只按顺序统计选择器中指定的元素 ・ Xxx-child 按顺序对选择器中指定的元素以外的元素进行计数。

first-child，首先参考所有子元素（无论是tag还是p tag）来查看子元素的个数。
然后检查相应的子元素是否符合条件。
这一次，“父元素（.food）中的第一个子元素”是“p标签”吗？
如果正确，则应用样式，如果不正确，则不应用样式。
在示例中，没有应用样式，因为“父元素 (.food) 中的第一个子元素”是“a 标签”。

```html
<div class="food">
	<a href="#">リンゴ</a>
	<p>キャベツ</p>
	<p>お米</p>
	<p>ラーメン</p>
</div>
.food p:first-child {
	color: red;
}
```



![img](https://ping-t-data-tokyo.s3.ap-northeast-1.amazonaws.com/uploads/question_image/file/7637/kk31121.jpg?X-Amz-Expires=600&X-Amz-Date=20210914T143119Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZCJ2QHLF73X4YH6P%2F20210914%2Fap-northeast-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=1a327d510b646ca1ec2ca6b7172598e1494a4b4a74340a486a0eebcd5d1baf6d)

##### font-size

![img](https://ping-t-data-tokyo.s3.ap-northeast-1.amazonaws.com/uploads/question_image/file/7651/kk31179.jpg?X-Amz-Expires=600&X-Amz-Date=20210915T135019Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZCJ2QHLF73X4YH6P%2F20210915%2Fap-northeast-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=03a93e02390d95eefa324212c27253f2c01e8cd1a06b651b6c1c3d6edcd262bc)

```html
	<p class="f1">xx-small</p>
	<p class="f2">x-small</p>
	<p class="f3">small</p>
	<p class="f4">medium</p>
	<p class="f5">large</p>
	<p class="f6">x-large</p>
	<p class="f7">xx-large</p>
```

##### メディアクエリ

CSS3からのメディアクエリは、デバイスの画面サイズや向きなどの条件によって、適用するCSSを切り替える技術です。

メディアクエリで条件を記述するには以下の方法があります。

・link要素のmedia属性に記述する
<link rel="stylesheet" media="screen and (max-width: 800px)" href="style.css">

・書式「@media」でCSSに記述する
@media screen and (min-width: 360px){
　body{background-color:aqua;}
}

また、CSSの中の書式「@import」で外部スタイルシートを読み込む際に、デバイスの条件を記述することもできます。

@import "style.css" screen, projection;



したがって正解は
・link要素のmedia属性に記述する
・書式「@media」を使用する
・書式「@import」を使用する
です。

##### 継承inherit

親要素のCSSプロパティの設定を子要素に強制的に継承する際に指定する値

**親要素に指定したスタイルが子要素にも引き継がれることである**

**強制的に継承するには、プロパティの値に「inherit」を指定する**

CSSのプロパティには、親要素に指定したスタイルが子要素に継承されるものがあります。
例えばcolorプロパティですが、body要素に「color:red;」を指定すると、body要素の中の子要素の文字も赤色になります。
しかし、borderやbackground、margin、paddingなど多くのプロパティは、デフォルトではスタイルは継承されません。このようなプロパティのスタイルを強制的に継承させるには、値に「inherit」(親要素のスタイルを継承する)を指定します。inheritはどのプロパティにも指定できます。

したがって正解は
・親要素に指定したスタイルが子要素にも引き継がれることである
・強制的に継承するには、プロパティの値に「inherit」を指定する
です。

例) borderプロパティの値を、body要素の中のh1とp要素にも継承させる
body{border:1px solid pink;}
h1, p{border:inherit;}

##### Webフォント

ブラウザでWebページを表示する際、通常、その端末にインストールされているフォントを呼び出して表示します。CSSで特定のフォントを指定していても、それがユーザの環境にインストールされていない場合は、そのフォントでは表示できません。
CSS3の「Webフォント」という仕様では、サーバ上などに保存しておいたフォントファイルを読み込むことで、環境に依存しないフォントの表示を可能にします。

Webフォントを使用するには、書式「@font-face{}」の中でフォントの名前とフォントファイルのURLを指定します。そしてフォントを使用したい部分にCSSを適用します。

\1. CSSで、「myfont」という名前を付けたフォントファイル「testfont.woff」を指定する。
@font-face{
　font-family:myfont;
　src:url("fonts/testfont.woff");
}

\2. font-family(フォントの種類を指定)の値としてWebフォントを要素に適用する。
p{font-family:"myfont";}

したがって正解は
・@font-faceで読み込む
・ユーザの環境に依存しないフォントの表示が可能である
です。

その他の選択肢については以下のとおりです。

・@importで読み込む
@importで読み込むのは外部スタイルシートです。

・ユーザがWeb上のフォントを選べる
ユーザがWeb上のフォントを選べる機能ではありません。

・font-styleプロパティでWebフォントを指定する
font-familyプロパティでWebフォントを指定します。

##### CSSを設定できる指定元

CSSを設定できる指定元には、基本的には「制作者」「ユーザー」「ユーザーエージェント(User Agent)」の3つがあります。
「制作者」はWebページの制作者で、HTML文書でCSSを指定します。
「ユーザー」はWebページを閲覧するユーザーで、ブラウザで自分のスタイルシートを指定し、希望のスタイルでWebページを表示することができます。
「ユーザーエージェント」は、様々な種類のブラウザや音声読み上げソフトなど、Webコンテンツのデータをユーザが利用できるようにするソフトウェアのことです。ブラウザはデフォルトのスタイルシートを持っています。

これらの指定元から同じセレクタに対してそれぞれCSSを指定した場合(設定が競合した場合)、制作者の指定したCSSの優先順位が一番高くなります。優先順位の高い順に並べると、次のようになります。

制作者 > ユーザー > ユーザーエージェント

但し、CSSの「プロパティ:値」の後ろに「!important」を追加することで、その設定を最も高い優先順位にすることができます。

例) p{color:red !important;}

「!important」を追加した場合とそうでない場合の指定元の優先順位は、次のようになります。
![<img src="/mondai3/img/jpg/k31238.jpg">](https://ping-t-data-tokyo.s3.ap-northeast-1.amazonaws.com/uploads/question_image/file/7678/k31238.jpg?X-Amz-Expires=600&X-Amz-Date=20210923T153829Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZCJ2QHLF73X4YH6P%2F20210923%2Fap-northeast-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=fe904086ad4e2b4ae624d1712c6ad2af886cbdcc67cd360bbb991099aaafd1af)

したがって正解は
・!important付きユーザーエージェント > !important付きユーザー > !important付き制作者 > 制作者 > ユーザー > ユーザーエージェント
です。

### 1.3 要素

##### formaction属性

```html
<p><input type="submit" value="送信" formaction="sample.php"></p>
```

- formaction 属性是指定表单数据目的地的 URL 的属性。在 input 元素的 form action 属性中指定的表单数据目标 URL 优先于在 input 元素所属的表单元素的 action 属性中指定的表单数据目标 URL。 formaction 属性是 HTML5 新引入的一个属性。
- type属性の値が「image」のinput要素に指定できる

##### meter要素

<label for="fuel">Fuel level:</label>

<meter id="fuel"
       min="0" max="100"
       low="33" high="66" optimum="80"
       value="50">
    at 50/100
</meter>

value属性の値によってメーターの色が緑・黄色・赤と変化した 

- low属性、high属性、optimum属性

##### 要素と属性

b要素は、その部分が重要であるなどの特別な意味を持たせることなく、実用的な目的で目立たせたい部分に対して使用する要素です。文中のキーワードや製品名といった部分に対して使用します。

<p>囲った部分が<b>太字</b>で表示されます。</p>

i要素は、文書内のテキストのうち、そこだけが異質であることを示すための要素です。たとえば、英語の文書中でドイツ語になっている部分などのほか、専門用語、学名といった部分をマークアップする際にも使用されます。

<p>囲った部分が<i>Italic</i>で表示されます。 </p>

s要素は、正しい内容ではなくなってしまった部分や関連性が失われてしまった部分に対して使用されます。

```html
<s>打ち消し線が引かれます</s>
```

u要素は、中国語のテキストにおいてその部分が固有名詞であることを示す場合や、単語の綴りが間違っていることを示す場合などに使用されます。

<p>囲った部分が<u>下線付き</u>で表示されます。</p>

em要素は、アクセントを付ける(強勢する)部分を示します。strong要素のように「重要さ」は表しません。以前は意味を強めるものでした。

したがって正解は
・アクセントを付ける部分を示す
です。

例) <p>文章に<em>アクセント</em>を付けます。</P>
![<img src="/mondai3/img/jpg/kk31069.jpg">](https://ping-t-data-tokyo.s3.ap-northeast-1.amazonaws.com/uploads/question_image/file/7621/kk31069.jpg?X-Amz-Expires=600&X-Amz-Date=20210924T144238Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZCJ2QHLF73X4YH6P%2F20210924%2Fap-northeast-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=288f777e4db7717524d55f0c6d20342f51bf530a098539f73a068a88a6de8f04)



##### video要素

値を指定せずに属性名だけで指定するタイプの属性を「論理属性（boolean attribute）」と言います。

autoplay属性は、ページのロード後に自動的に再生を開始させるための属性です。
loop属性を指定すると、動画が繰り返し再生されるようになります。
muted属性を指定すると、デフォルトで音を出さない（ミュートされた）状態にします。
controls属性を指定すると、コントローラー（再生・停止・ボリューム調整などを行うためのUI）を表示させます。

videoタグを使って動画圧縮規格がh.264の映像を表示する場合：video/mp4

##### source要素

source 元素用于指定媒体文件类型和 URL 作为视频元素和音频元素的子元素。



##### fieldset 要素

组合表单中的相关元素

fieldset 元素可将表单内的相关元素分组。

<fieldset> 标签将表单内容的一部分打包，生成一组相关表单的字段。

当一组表单元素放到 <fieldset> 标签内时，浏览器会以特殊方式来显示它们，它们可能有特殊的边界、3D 效果，或者甚至可创建一个子表单来处理这些元素。

<fieldset> 标签没有必需的或唯一的属性。

[ 标签](https://www.w3school.com.cn/tags/tag_legend.asp)<legend>为 fieldset 元素定义标题。

　ウェブのフォーム内のラベル(`<label>`)のようにいくつかのコントロールをグループ化するために用いる。なので、複数のinputタグなどを項目としてグループ化するための要素である。

<td>
<fieldset>
<legend>連絡先</legend>

<table width=100%>
<tr>
<td><label for=name>名前:</label></td>
<td><input type=text id=name placeholder="例）資格月斗" required></td>
</tr>
<tr>
<td><label for=tel>電話:</label></td>
<td><input type=tel id=tel pattern="^[0-9]+$" placeholder="例）
08099999999" required></td>



##### object要素

object要素は、data属性でファイルを指定し、type属性でMIMEタイプを指定することで文書内に外部リソースを埋め込んで表示することができます

object data="sample.mpg" …>



##### time要素

如果指定了 datetime 属性，则 time 元素的值必须为规范中指定的机器可读格式。如果未指定 datetime 属性，则 time 元素的元素内容的文本必须为机器可读格式。

```
<time>02:50</time>
<time datetime="02:50">真夜中</time>
<time datetime="2015-12-24T02:50">2時50分</time>
<time datetime="2015-12-24 02:50:00">ニ時五十分</time>
wrong:
<time>2時50分</time>
```

![img](https://ping-t-data-tokyo.s3.ap-northeast-1.amazonaws.com/uploads/question_image/file/7608/k31039.jpg?X-Amz-Expires=600&X-Amz-Date=20210923T124435Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZCJ2QHLF73X4YH6P%2F20210923%2Fap-northeast-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=00f4246e512a2c2048ea160529d6620aec8572776c14d7b02e6a1e6c88101b48)

##### ruby

ruby要素の最初の子要素には、ルビを振る対象となるテキスト（phrasing content）またはrb要素を配置する必要があります。したがって、最初の子要素としてrtc要素を配置しているEは文法的に正しくありません。ルビを振る対象となるテキストは、rb要素のタグを付けても付けなくても問題はありませんが、rb要素のタグを付けることでそこにCSSが指定しやすくなるなどの利点もあります。
ruby要素自体はタグを省略することはできませんが、その内容となるruby関連の各要素は終了タグを省略することが可能です。
ルビ関連の要素は、要素名が何の略なのかをおぼえておくと記憶しやすくなります。たとえばrtは「ruby text」の略で、それがルビのテキスト（振仮名となるテキスト）であることを示しています。rtcは「ruby text container」の略なので、そこにrt要素を入れるということがわかります。rb要素のbは「base text」を意味し、rp要素のpは「parentheses（パーレン=丸括弧）」を意味しています。

- <ruby><rtc><rb>長万部</rb><rt>おしゃまんべ</rt></rtc></ruby>

##### グローバル属性

グローバル属性とは、全てのHTML要素で使用できる属性のこと。

| 属性                                                         | 概要                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [accesskey](http://html5.cyberlab.info/global-attributes/accesskey.html) | 要素にアクセスキーを割り当てる属性。                         |
| [class](http://html5.cyberlab.info/global-attributes/class.html) | 要素にクラスを割り当てる属性。                               |
| [contenteditable](http://html5.cyberlab.info/global-attributes/contenteditable.html) | 要素の内容を編集可能かどうかを指定する属性。                 |
| contextmenu                                                  | 要素のコンテキストメニューを指定する属性。                   |
| [data-*](http://html5.cyberlab.info/global-attributes/data.html) | 要素にカスタム（独自、オリジナル）・データを格納する属性。   |
| [dir](http://html5.cyberlab.info/global-attributes/dir.html) | 要素内のテキストの方向を指定する属性。                       |
| [draggable](http://html5.cyberlab.info/global-attributes/draggable.html) | 要素をドラッグ可能かどうかを指定する属性。                   |
| [dropzone](http://html5.cyberlab.info/global-attributes/dropzone.html) | ドラッグデータを、要素にドロップした時の処理（コピー、移動、リンク）を指定する属性。 |
| [hidden](http://html5.cyberlab.info/global-attributes/hidden.html) | 関連性がある要素かどうかを指定する属性。                     |
| [id](http://html5.cyberlab.info/global-attributes/id.html)   | 要素に、固有のidを指定する属性。                             |
| [lang](http://html5.cyberlab.info/global-attributes/lang.html) | 要素内の言語コードを指定する属性。                           |
| [spellcheck](http://html5.cyberlab.info/global-attributes/spellcheck.html) | 要素内のテキストのスペルチェックをするかしないかを指定する属性。 |
| [style](http://html5.cyberlab.info/global-attributes/style.html) | スタイルシートを要素に直接指定するための属性。               |
| [tabindex](http://html5.cyberlab.info/global-attributes/tabindex.html) | 要素のタブインデックスを指定する属性。                       |
| [title](http://html5.cyberlab.info/global-attributes/title.html) | 要素に関する補足情報を指定する属性。                         |
| translate                                                    | ページ翻訳時、要素の内容を翻訳するかどうかを指定する属性     |

##### input要素のtype属性に指定できる値

https://webliker.info/39533/】

[type="hidden"](http://www.htmq.com/html5/input_type_hidden.shtml)

画面上は表示されない隠しデータを指定する

[type="text"](http://www.htmq.com/html5/input_type_text.shtml)

一行テキストボックスを作成する（初期値）

[type="search"](http://www.htmq.com/html5/input_type_search.shtml)

検索テキストの入力欄を作成する![HTML5から追加](http://www.htmq.com/images/html5add.gif)

[type="tel"](http://www.htmq.com/html5/input_type_tel.shtml)

電話番号の入力欄を作成する![HTML5から追加](http://www.htmq.com/images/html5add.gif)

[type="url"](http://www.htmq.com/html5/input_type_url.shtml)

URLの入力欄を作成する![HTML5から追加](http://www.htmq.com/images/html5add.gif)

[type="email"](http://www.htmq.com/html5/input_type_email.shtml)

メールアドレスの入力欄を作成する![HTML5から追加](http://www.htmq.com/images/html5add.gif)

[type="password"](http://www.htmq.com/html5/input_type_password.shtml)

パスワード入力欄を作成する

[type="datetime"](http://www.htmq.com/html5/input_type_datetime.shtml)

UTC（協定世界時）による日時の入力欄を作成する![HTML5から追加](http://www.htmq.com/images/html5add.gif)

[type="date"](http://www.htmq.com/html5/input_type_date.shtml)

日付の入力欄を作成する![HTML5から追加](http://www.htmq.com/images/html5add.gif)

[type="month"](http://www.htmq.com/html5/input_type_month.shtml)

月の入力欄を作成する![HTML5から追加](http://www.htmq.com/images/html5add.gif)

[type="week"](http://www.htmq.com/html5/input_type_week.shtml)

週の入力欄を作成する![HTML5から追加](http://www.htmq.com/images/html5add.gif)

[type="time"](http://www.htmq.com/html5/input_type_time.shtml)

時間の入力欄を作成する![HTML5から追加](http://www.htmq.com/images/html5add.gif)

[type="datetime-local"](http://www.htmq.com/html5/input_type_datetime-local.shtml)

UTC（協定世界時）によらないローカル日時の入力欄を作成する![HTML5から追加](http://www.htmq.com/images/html5add.gif)

[type="number"](http://www.htmq.com/html5/input_type_number.shtml)

数値の入力欄を作成する![HTML5から追加](http://www.htmq.com/images/html5add.gif)

[type="range"](http://www.htmq.com/html5/input_type_range.shtml)

レンジの入力欄を作成する![HTML5から追加](http://www.htmq.com/images/html5add.gif)

[type="color"](http://www.htmq.com/html5/input_type_color.shtml)

色の入力欄を作成する![HTML5から追加](http://www.htmq.com/images/html5add.gif)

[type="checkbox"](http://www.htmq.com/html5/input_type_checkbox.shtml)

チェックボックスを作成する

[type="radio"](http://www.htmq.com/html5/input_type_radio.shtml)

ラジオボタンを作成する

[type="file"](http://www.htmq.com/html5/input_type_file.shtml)

サーバーへファイルを送信する

[type="submit"](http://www.htmq.com/html5/input_type_submit.shtml)

送信ボタンを作成する

[type="image"](http://www.htmq.com/html5/input_type_image.shtml)

画像ボタンを作成する

type="reset"

リセットボタンを作成する

[type="button"](http://www.htmq.com/html5/input_type_button.shtml)

汎用ボタンを作成する



##### HTML5から追加された下記の要素について記載します。

 details要素、summary要素、datalist要素、keygen要素、output要素  【details要素、summary要素】

 details要素は、ユーザーが表示/非表示を切り替えられる詳細情報のウィジェット(画面上で小型化されたアプリケーションソフト)を表します。 details要素の子要素であるsummary要素を記述すると、キャプション(詳細情報の要約)を示せます。  例) ヒントを表示する <details> <summary>ヒントを表示</summary> <p>ヒントは動物の名前です。</p> </details>   

【datalist要素】 datalist要素は、入力欄でユーザーに入力候補として提案するデータのリストを定義します。 入力候補のリストはoption要素で作成します。 ※option要素は、select要素(ドロップダウンのセレクトボックス)やdatalist要素の選択肢を作成します。  例) <datalist> <option value="A">選択肢A</option> <option value="B">選択肢B</option> </datalist>  

【keygen要素】 公開鍵暗号方式では、一般に公開される公開鍵と、公開されない秘密鍵のペアを使用してデータを暗号化/復号化します。 keygen要素は、暗号化の公開鍵と秘密鍵をペアで発行します。フォームを送信すると、公開鍵はサーバに送信され、秘密鍵はローカルに格納されます。  keygen要素に指定できる属性は以下のとおりです。  form="form要素のid属性の値": 所属するform要素 challenge="文字列": 公開鍵と共にサーバに送信する文字列 keytype="文字列": 鍵の暗号化の種類(rsaなど、指定できる種類はブラウザに依存する) name="文字列": フォーム部品の名前  例) CGIプログラム「generatekey.cgi」にフォームを送信する <form action="generatekey.cgi" method="post"> <p><keygen name="pubkeycrypto" keytype="rsa"></p> <p><input type=submit value="公開鍵を送信"></p> </form>  

【output要素】 output要素は、計算やユーザーの操作などの結果を出力します。  例) 足し算の結果を表示する(一部にJavaScriptが使用されていますが、試験範囲外のため説明を割愛します。) <form onsubmit="return false" oninput="add.value=a.valueAsNumber + b.valueAsNumber"> <input type="number" name="a"> + <input type="number" name="b"> = <output name="add"></output>



### 1.4 レスポンシブWebデザイン

##### メディアクエリ

link要素として指定する場合

<link rel="stylesheet" href="style.css" media="screen and (max-width:480px)">

スタイルシートに指定する場合

/*

@media以外の所は全てのサイズで読み込まれます。

*/

p {

 color:red;

}

@media screen and (min-width:480px) { 

  /*　画面サイズが480pxからはここを読み込む　*/

p { color:#ededed;}

}

@media screen and (min-width:768px) and ( max-width:1024px) {

  /*　画面サイズが768pxから1024pxまではここを読み込む　*/

p {}

}

@media screen and (min-width:1024px) {

  /*　画面サイズが1024pxからはここを読み込む　*/

“读取style.css最多480px的屏幕尺寸”，style.css中描述的CSS应用于最多480px的屏幕尺寸。 如果值超过设置值（在这种情况下为宽度大小），则不会应用 CSS。

https://sole-color-blog.com/blog/71/

- @media { ... }
- @media all { ... }
- @media (min-width: 500px) { ... }
- @media all and (min-width: 500px) { ... }
- @media (min-width: 500px) and (max-width: 800px) { ... }

##### 端末の向きを判定する

```
//縦向きの場合
@media screen and (orientation:portrait){
  p {font-size: 1em; }  
}
//横向きの場合
@media screen and (orientation:landscape){
  p {font-size: 1.2em; }  
}
```

##### srcset属性

该元素可以根据浏览器的屏幕要求（宽度、高度、像素密度）加载不同的图像

```
<img src="img/example-img.jpg"
     srcset="img/example-img.jpg 1x,
             img/example-img@2x.jpg 2x"
     alt="Example image">
```

1x で解像度1倍のとき
2x で解像度2倍のとき ※Retinaのとき

imgタグを使った例



```
<img src="img/example-img.jpg"
     srcset="img/example-img-320.jpg 320w,
             img/example-img-640.jpg 640w"
     sizes="50vw"
>
```

320w, 640w ... w とは？

その画像を表示したい時のブラウザ幅px と捉えておけばOKです
(昔はViewportのサイズだったらしいです)

sizes="50vw” の　vw とは

`viewport width`の略称です
ビューポートの幅に対する割合(%)　を指します

```
srcset="画像URL その画像を表示したい時の想定ブラウザ幅(px), ..."
```

と書いてしまえば良いです。

##### format-detection

スマートフォンでは例題のように数字列を電話番号と判断して関連するアプリにリンクする拡張があります。

```
<meta name="format-detection" content="telephone=no, email=no address=no" />
<a href="tel:030-0000-0000">030-0000-0000</a>
<a href="mailto:info@lpi.or.jp">info@lpi.or.jp</a><br>
<a href="http://maps.google.com/maps?q=東京都港区麻布台1-11-9">東京都港区麻布台1-11-9</a>
```

##### CSSスプライト

图标等小图片是通过HTTP为每个文件下载的，所以大量会影响页面的显示速度。 因此，将小图像排列在一张图像上，一次性下载它们，并通过指定 CSS 显示它们的技术称为 CSS 精灵。

在一张图像上放置多个图像，例如图标 通过 CSS 指定图像的坐标和大小来显示要使用的图像部分 由于图像加载一次完成，因此页面显示速度更快。

##### viewport

<meta name="viewport" content="width=device-width"> (E.) と記述することで、スマートフォンのデバイスの横幅で描画が行なわれるようになります。

移动设备上的viewport就是设备的屏幕上能用来显示我们的网页的那一块区域，viewport不局限于浏览器可视区域的大小，它可能比浏览器的可视区域要大，也可能比浏览器的可视区域要小。
 一般来讲，移动设备上的viewport都是要大于浏览器可视区域的，这是因为考虑到移动设备的分辨率相对于桌面电脑来说都比较小，所以为了能在移动设备上正常显示那些传统的为桌面浏览器设计的网站，移动设备上的浏览器都会把自己默认的viewport设为980px或1024px（也可能是其它值，这个是由设备自己决定的），但带来的后果就是浏览器会出现横向滚动条，因为浏览器可视区域的宽度是比这个默认的viewport的宽度要小的。

https://qiita.com/ryounagaoka/items/045b2808a5ed43f96607

https://www.jianshu.com/p/cc81197b0886

###### 利用meta标签对viewport进行控制

移动设备默认的viewport是layout viewport，也就是那个比屏幕要宽的viewport，但在进行移动设备网站的开发时，我们需要的是ideal viewport。那么怎么才能得到ideal viewport呢？这就该轮到meta标签出场了。

我们在开发移动设备的网站时，最常见的的一个动作就是把下面这个东西复制到我们的head标签中：

```
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
```

该meta标签的作用是让当前viewport的宽度等于设备的宽度，同时不允许用户手动缩放。也许允不允许用户缩放不同的网站有不同的要求，但让viewport的宽度等于设备的宽度，这个应该是大家都想要的效果，如果你不这样的设定的话，那就会使用那个比屏幕宽的默认viewport，也就是说会出现横向滚动条。

这个name为viewport的meta标签到底有哪些东西呢，又都有什么作用呢？

meta viewport 标签首先是由苹果公司在其safari浏览器中引入的，目的就是解决移动设备的viewport问题。后来安卓以及各大浏览器厂商也都纷纷效仿，引入对meta viewport的支持，事实也证明这个东西还是非常有用的。

在苹果的规范中，meta viewport 有6个属性(暂且把content中的那些东西称为一个个属性和值)，如下：

| width         | 设置***layout viewport*** 的宽度，为一个正整数，或字符串"width-device" |
| ------------- | ------------------------------------------------------------ |
| initial-scale | 设置页面的初始缩放值，为一个数字，可以带小数                 |
| minimum-scale | 允许用户的最小缩放值，为一个数字，可以带小数                 |
| maximum-scale | 允许用户的最大缩放值，为一个数字，可以带小数                 |
| height        | 设置***layout viewport*** 的高度，这个属性对我们并不重要，很少使用 |
| user-scalable | 是否允许用户进行缩放，值为"no"或"yes", no 代表不允许，yes代表允许 |

每个移动设备浏览器中都有一个理想的宽度，这个理想的宽度是指css中的宽度，跟设备的物理宽度没有关系，在css中，这个宽度就相当于100%的所代表的那个宽度。我们可以用meta标签把viewport的宽度设为那个理想的宽度，如果不知道这个设备的理想宽度是多少，那么用device-width这个特殊值就行了，同时initial-scale=1也有把viewport的宽度设为理想宽度的作用。所以，我们可以使用

```
<meta name="viewport" content="width=device-width, initial-scale=1">
```

来得到一个理想的viewport（也就是前面说的ideal viewport）。

实际上，这就是响应式布局的基础。



##### フルードグリッド

レスポンシブWebデザインは、1つのHTMLファイルで様々な表示デバイスに応じてWebページのレイアウトやデザインを最適化して表示する手法です。

レスポンシブWebデザインを実現するための技術の1つであるフルードグリッド(Fluid Grid)は、ブラウザの幅に応じてグリッド(格子、方眼)の大きさを伸縮させます。ページ全体をグリッドで区切りコンテンツを配置していくデザイン手法である「グリッドデザイン」と、画面の幅に応じてコンテンツの横幅が可変となる「フルードデザイン」を組み合わせたものです。

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>フルードグリッドのサンプル</title>
	<style>
		body{
			width:100%;
			}
		#box1{
			width:50%;
			height:100px;
			background-color:#00ffff;
		}
		#box2{
			width:25.5%;
			height:100px;
			margin-top:20px;
			border-radius:50%;
			background-color:#ffc0cb;
		}
	</style>
</head>
<body>
		<div id="box1">ブラウザの幅に応じて伸縮します。</div>
		<div id="box2"></div>
</body>
</html>
```

### 1.5 APIの基礎知識

##### 著作権を保護する目的の技術・仕様

- Digital Rights Management - DRM
- Encrypted Media Extensions - EME

##### リアルタイム通信API

- Socket.io
- WebSocket

】

##### Geolocation API

Geolocation API 使用 JavaScript 来获取位置信息。可以获取的信息有纬度/经度/海拔/位置精度/海拔精度/移动方向/速度/获取时间，这个信息除了只能使用一次之外，还可以用它来保持自动获取信息

关于 Geolocation API 的一个常见误解是您无法获得地址。由于API获取的经纬度只是坐标，单靠这些信息是无法识别地址的。换句话说，仅 Geolocation API 无法获取地址。 要将 Geolocation API 获取的纬度/经度转换为地址，必须使用一种称为 Geocoding 的技术。首先，需要通过 Geolocation API 获取用户的位置信息作为“纬度/经度”，并通过 Geocoding 将该信息转换为地址这两个步骤。这将允许您识别您的地址，例如您的当前位置。当然，很多与地理编码相关的 API 都注册在 Rakuten Rapid API 中。

关于位置信息的另一个常见误解是，除非您的设备配备 GPS，否则您无法使用位置信息。由于 GPS 被广泛用作获取位置信息的技术，因此可能会出现“获取位置信息 = GPS 必不可少”的图像。然而，在现实中，没有 GPS 也可以获得位置信息。在这种情况下，纬度和经度是使用 IP 地址等信息获得的。

| 属性名           | 値の内容          | 値の単位 |
| ---------------- | ----------------- | -------- |
| latitude         | 緯度（-180～180） | 度       |
| longitude        | 経度（-90～90）   | 度       |
| altitude         | 高度              | m        |
| accuracy         | 緯度・経度の誤差  | m        |
| altitudeAccuracy | 高度の誤差        | m        |
| heading          | 方角（0～360）    | 度       |
| speed            | 速度              | m/秒     |

http://www.htmq.com/geolocation/

##### SVG 

SVG（Scalable Vector Graphics）是一种用 XML 表示矢量图形的规范。

和CSS一样，可以单独用SVG创建、装饰和变换字符和图形，也可以用CSS装饰。作为使用示例，一个 SVG 可以覆盖徽标和图标，这对于响应式设计也很有效。它还用于各种格式的图表表示，例如饼图和条形图。

##### バックグラウンドで実行

Service Workers 和 Web Workers 是允许您使用 Javascript 在后台执行操作的 API。

Web Workers可以以Worker为单位并行处理多个进程，因此可以在后台进行计算处理、大文件访问等耗时处理，提高应用的可用性。

Service Workers 是替代Application Cache 的离线处理API，但它使用Push API 和fetch 一起实现类似的处理，与后台处理同步。

##### CACHE MANIFEST 

キャッシュマニフェスト作为一个Web开发相关的人员，都不会少听到、看到Cache这个词。是的，上面也已经说了，它是一种缓存的机制。它可以通过一个.manifest文件来配置需要缓存的或者一定要保持联网缓存的文件。而重点就是这个.manifest文件，这里进行了简单的整理：
　　◆MIME TYPE：text/cache-manifest
　　◆需要由你创建的：NAME.manifest
　　◆作用：主要是配置需要缓存的文件

应用缓存的优势：
（1） 离线浏览：用户可以在应用离线时使用它们
（2） 速度更快：已缓存资源，加载得更快
（3） 减少服务器负载：浏览器只需从服务器删下载更改过或更新过的资源就可以了。

```xml
<!DOCTYPE html>
<html manifest="test.manifest">
    <head>
        <meta charset="UTF-8">
        <title></title>
        <link rel="stylesheet" type="text/css" href="css/test.css"/>
        <link rel="stylesheet" type="text/css" href="css/network.css"/>
        <script type="text/javascript" src="js/test.js" ></script>
    </head>
    <body>
        <div id="box"></div>
    </body>
</html>
```

**test.manifest代码**

```objectivec
CACHE MANIFEST
## v 1.3

CACHE:
./css/test.css
./js/test.js
NETWORK: 
./css/network.css
FALLBACK:
```

必ずネットワーク経由でアクセスするリソースを記述するセクション:NETWORK

CACHE  FALLBACK ONLINE NOCACHE

A.キャッシュするリソースを指定するセクションです。
C.リソースにアクセスできない場合の代替リソースを指定するセクションです。
D.ONLINEというセクションはありません。
E.NOCACHEというセクションはありません。

オフラインウェブアプリケーションにおけるマニフェストファイルをウェブページに関連づけるには、どの要素の何属性を使用するか？:html要素のmanifest属性

- 一行目には、「CACHE MANIFEST」と記述する必要がある。
- \#から始まる行はコメントとなる。
- CACHE、FALLBACK、NETWORKの３つのセクションが存在する。
- マニフェストファイルは、通常Webサーバ上に配置する。

指定できるファイルは.htmlファイルや.cssのファイル以外にも、Javascriptのコードファイルや、PNGなどの画像ファイルを指定する事ができます。

离线应用程序需要同时具有要处理的内容和清单文件。 manifest文件描述了运行应用程序所需的Javascript文件和样式表，并将运行所需的所有文件下载到客户端，以便离线运行。

・ブラウザのキャッシュ領域にファイルがキャッシュされる
・ファイルのダウンロードに失敗するとエラーが発生し、キャッシュは更新されない

![img](https://ping-t-data-tokyo.s3.ap-northeast-1.amazonaws.com/uploads/question_image/file/7692/k31297.jpg?X-Amz-Expires=600&X-Amz-Date=20210920T124715Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZCJ2QHLF73X4YH6P%2F20210920%2Fap-northeast-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=bcf1a2edfc87cabd1c88f1a34e7fe2508d290a909706db5c3ccea225394ddd74)

##### 認証

・Basic認証
ユーザー名とパスワードを「:」(コロン)でつないで、Base64というエンコード方式で符号化して送信します。暗号化されていない平文なので、認証情報の改ざん(第三者がデータを無断で書き換えたり消去する行為)や覗き見が容易にできてしまいます。

・Digest認証
ユーザー名とパスワードをMD5(ハッシュ関数の1つ)でハッシュ化して送信します。ハッシュ化とは、ハッシュ関数から得られたハッシュ値を使用して、データを不可逆(元の状態に戻せない)のフォーマットに変換することです。認証情報の改ざんや覗き見をすることが困難になります。

##### HTTPメッセージの中のメッセージヘッダ

HTTPメッセージの中のメッセージヘッダには、メッセージでやり取りされる様々な情報を扱う「ヘッダフィールド」が含まれます。
主なヘッダフィールドには次のものがあります。
![<img src="/mondai3/img/jpg/kkkkk31309.jpg">](https://ping-t-data-tokyo.s3.ap-northeast-1.amazonaws.com/uploads/question_image/file/7701/kkkkk31309.jpg?X-Amz-Expires=600&X-Amz-Date=20210922T161107Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZCJ2QHLF73X4YH6P%2F20210922%2Fap-northeast-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=f05bedba58397855641fc7a1a99389a6cf5598fadfa8dd82407a21e1623f783c)



##### **参考**

【HTTP】
HTTP(HyperText Transfer Protocol)は、ブラウザなどのWebクライアントとWebサーバの間でデータを送受信する際の通信プロトコル(通信手順)です。ブラウザはHTMLや画像などのファイルをWebサーバからHTTPで取得してWebサイトを表示します。

HTTPでの通信は2つのメッセージをやり取りします。
ブラウザはWebサーバに対して「HTTPリクエスト」として取得したいファイルを要求し、Webサーバは「HTTPレスポンス」としてファイルやステータスをブラウザに返します。
![【図を表示】](https://ping-t-data-tokyo.s3.ap-northeast-1.amazonaws.com/uploads/question_image/file/7696/k31309.jpg?X-Amz-Expires=600&X-Amz-Date=20210922T161107Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZCJ2QHLF73X4YH6P%2F20210922%2Fap-northeast-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=c64b8692decc7c68df4fc2ab422fa5c536c0e131afc7c7c2918c53a71dcb38a9)

HTTPの各メッセージの構造は次のとおりです。

![【図を表示2】](https://ping-t-data-tokyo.s3.ap-northeast-1.amazonaws.com/uploads/question_image/file/7697/kk31309.jpg?X-Amz-Expires=600&X-Amz-Date=20210922T161107Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZCJ2QHLF73X4YH6P%2F20210922%2Fap-northeast-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=913775050a9a62d3e9a6a70cce0c40ef359fcd82dc2fffdd377781c545c6f2ed)

・URL(Uniform Resource Locator)、URI(Uniform Resource Identifier)
URLはインターネット上のリソース(ファイルなど)の位置を示す文字列です。
URIはインターネットに限らないより大きな概念でのリソースの位置を示す文字列です。URLはURIの1つの形式です。

URLの書式は次のとおりです。
![【図を表示6】](https://ping-t-data-tokyo.s3.ap-northeast-1.amazonaws.com/uploads/question_image/file/7698/kkkkkk31309.jpg?X-Amz-Expires=600&X-Amz-Date=20210922T161107Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZCJ2QHLF73X4YH6P%2F20210922%2Fap-northeast-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=6f17f8f61b2ef1d9190f9c55be9238c5012bb14ec0000c617072846f7d5bcb44)

スキーム名にはリソースにアクセスするために使用するプロトコルなどを指定します。httpやftp(File Transfer Protocol: ファイル転送プロトコル)などを指定でき、スキーム名の後の書式はスキームによって変わります。
ドメイン名はインターネット上で個々のコンピュータを識別するための名前です。

・リクエストメソッド
HTTPリクエストの中の「メソッド」は、指定したURIに対して、クライアントからサーバに要求するアクションです。
主なメソッドには次のものがあります。
![【図を表示3】](https://ping-t-data-tokyo.s3.ap-northeast-1.amazonaws.com/uploads/question_image/file/7699/kkk31309.jpg?X-Amz-Expires=600&X-Amz-Date=20210922T161107Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZCJ2QHLF73X4YH6P%2F20210922%2Fap-northeast-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=a16091dde25e9374433f168aca8b7bac8723bb916cf28ab4d78de1136dbc3522)

よく利用されるメソッドはGETとPOSTです。
GETで送信時にIDやパスワードなどのパラメータを指定した場合、それらはURLに追加され表示されてしまいます。そのため情報が漏えいするリスクが高まります。

例) HTTPリクエストの開始行にパラメータ(「?name=yamada&password=pass」の部分)が表示される
GET /index.html?name=yamada&password=pass HTTP/1.1

POSTで送信時は、パラメータはメッセージボディに書かれるためURLには追加されません。重要なデータはPOSTで送信します。

・ステータスコード
HTTPレスポンスの中の「ステータスコード」は、リクエストに対する結果を表す3桁の数字です。
主なステータスコードには次のものがあります。
![【図を表示4】](https://ping-t-data-tokyo.s3.ap-northeast-1.amazonaws.com/uploads/question_image/file/7700/kkkk31309.jpg?X-Amz-Expires=600&X-Amz-Date=20210922T161107Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZCJ2QHLF73X4YH6P%2F20210922%2Fap-northeast-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=51e332d10812df8e067ccd564be374bd76ce54ba9b18baca84a5022f06f5933a)

ステータスコードの301や307では、指定したWebページから自動的に他のページに転送される「リダイレクト」を、Webサーバで設定できます。

・ヘッダフィールド
HTTPメッセージの中のメッセージヘッダには、メッセージでやり取りされる様々な情報を扱う「ヘッダフィールド」が含まれます。
主なヘッダフィールドには次のものがあります。
![【図を表示5】](https://ping-t-data-tokyo.s3.ap-northeast-1.amazonaws.com/uploads/question_image/file/7701/kkkkk31309.jpg?X-Amz-Expires=600&X-Amz-Date=20210922T161107Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZCJ2QHLF73X4YH6P%2F20210922%2Fap-northeast-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=f05bedba58397855641fc7a1a99389a6cf5598fadfa8dd82407a21e1623f783c)

ヘッダの種類であるRequest-headerはリクエストに追加できるヘッダで、Response-headerはレスポンスに追加できるヘッダです。General-headerはリクエスト/レスポンスの両方に追加できるヘッダで、Entity-headerはメッセージボディについての情報を記載するヘッダです。

Content-Typeヘッダは、コンテンツのMIMEタイプに加えてエンコーディングを示すこともできます。これによりメッセージを受け取る側は、コンテンツの種類とエンコーディングを理解できます。
例) HTTPヘッダフィールド
Content-Type: text/html; charset=UTF-8

【認証】
HTTPではWeb上のファイルへのアクセスを制限する認証を行えます。主な認証方法として、Basic認証とDigest認証があります。

・Basic認証
ユーザー名とパスワードを「:」(コロン)でつないで、Base64というエンコード方式で符号化して送信します。暗号化されていない平文なので、認証情報の改ざん(第三者がデータを無断で書き換えたり消去する行為)や覗き見が容易にできてしまいます。

・Digest認証
ユーザー名とパスワードをMD5(ハッシュ関数の1つ)でハッシュ化して送信します。ハッシュ化とは、ハッシュ関数から得られたハッシュ値を使用して、データを不可逆(元の状態に戻せない)のフォーマットに変換することです。認証情報の改ざんや覗き見をすることが困難になります。

【HTTP Cookie】
Cookie(クッキー)とは、HTTPにおいてWebブラウザとWebサーバ間で状態を管理するためのプロトコル、または保存された情報のことです。HTTPでの通信は各メッセージが独立しており、現在の状態を保持しないため、ブラウザにCookieを保存することで状態を管理します。Cookieとして保存されるのは、例えばショッピングサイトでのログイン状態やカートの情報、アクセス履歴などです。Cookieは覗き見される恐れがあるので、WEBサービスの開発者は、自動ログインのためにIDやパスワードなどの認証情報を直接Cookieへ保存する実装にすべきではありません。
Webサーバからブラウザに返すレスポンスのヘッダ「Set-Cookie」でCookieを設定します。Cookieには4096バイトのASCII文字列を保存できます(ブラウザによってはより大きな容量を保存できます)。ブラウザは再度Webサイトへアクセスする際、保存していた状態をリクエストのヘッダ「Cookie」としてWebサーバに送信します。
Webクライアント側では、ブラウザからCookieの送受信の設定(無効にするなど)や削除を行えます。また、JavaScriptなどのスクリプトによってCookieを操作することが可能です。
Cookieが保存されるディレクトリやファイルは、OSやブラウザのバージョンによって異なります。

【HTTPS】
HTTPS(HyperText Transfer Protocol Secure)は、SSL/TLSプロトコルによってセキュリティを確保した通信路上で、より安全にHTTP通信を行うことです。SSL(Secure Socket Layer)/TLS(Transport Layer Security)は、データを暗号化して送受信するプロトコルです。
HTTPSのデフォルトのポート番号は443です。

例) HTTPSでのWebアクセス(デフォルトのポート443番であれば、ポート番号は省略可能)
