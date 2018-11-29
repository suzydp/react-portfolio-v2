
# React portfolio v2

## 1-1. Run ```Create react app```

[Official document for Create React App](https://reactjs.org/docs/introducing-jsx.html)

## 1-2. Install ```node-sass``` to activate Sass files

```$ npm install node-sass```  
or  
```$ yarn install node-sass```

That's it for installing sass! It's super easy🌟

### Useful snippets on Editor to build react

- React-Native/React/Redux snippets for es6/es7
- Bracket Pair Colorizer
- Material Icon Theme
- ESLint

## 2. Make details of App.js

[See this link to checkout the code](http://codehere)

## 3. Componentization from App.js to Header, Footer and Toppage

App.jsから要素を下記のように分割してコンポーネント化する。  
**ファイルは「components」というディレクトリを作りそこへ格納する**

- ファイル構成

- App.js
- components -- Header.jsx, Header.scss  
　　　        |_ Toppage.jsx, Toppage.scss  
　　　        |_ Footer.jsx, Footer.scss  

- App.jsは全体をオーガナイズする役目
- .scssファイルは各コンポーネントのディレクトリ内に作成する
- What is JSX? See the link : [Introducing JSX](https://reactjs.org/docs/introducing-jsx.html)  
  - JSXはHTMLでも文字列でもない。 - [See link](https://reactjs.org/docs/introducing-jsx.html#why-jsx)
  - JSXはオブジェクトの代わりを成している - [See link](https://reactjs.org/docs/introducing-jsx.html#jsx-represents-objects)
  - JSXを使わなくてもreactは機能するが、JSXを使うほうがよりセキュリティの質が向上する(DOMがJSXを描画する前に各々の値をセキュアなものに変換する) - [See link](https://reactjs.org/docs/introducing-jsx.html#jsx-prevents-injection-attacks)

### inside of each jsx file

1. `import React, { Component } from 'react'`  
このコードがいつも1行目に必要。これがReactを呼び出している印
1. 1.のコードの下にimportしたいファイル(scssやimg, svg)を記述。`<link rel="">`と同じようなことをここでやるイメージ
2. Reactで描画したい要素を下記の中に記述
   ```
   **header.jsx**
   export default class Header extends
   Component{
        render(){
            return(
                //contents which you want to appear on browser
                <header className="Header">
                    <h1 className="Title">Artworks by SZDP</h1>
                    <ul className="Menu">
                        <li>Top</li>
                        <li>Works</li>
                        <li>Bio</li>
                        <li>Contact</li>
                        <li><a href="http://suzydp.net">suzydp.net</a></li>
                    </ul>
                </header>
            )
        }
    }
   ```
   - Component化したい要素をexportしている
   - render()してreturnされるものがブラウザで表示される内容になる

### inside of App.js

- ページの親の役目
        - Javaで言うSuperclassがApp.js, Subclassが各コンポーネント
- `import Header from './components/Header/Header.jsx';` と `<Header />`のコンビがブラウザでheaderの中身を描画している
- Toppage, Footerも同様

#### Sass

- 各コンポーネントディレクトリの中に収める
- 全体に共通の要素としたいものはApp.scssに書けばOK(?*要確認)

## 4. Add ArtWorks component

- TopPage, Header, Footerと同列にArtWorksコンポーネントを作成
- 「TopPageの子要素」として、TopPageとArtWorksコンポーネントをリンクさせる
  - toppage.jsxに`import ArtWorks from '../ArtWorks/ArtWorks.jsx';`を記述し、`<ArtWorks />`を`<p></p>`にreplaceする

## 5. Add mixins

＠mixinとは？Sassで使える「複数の設定をまとめて行える」便利な機能です。メンテナンスのしやすいCSSの設計も可能です。

- `@mixin`で定義し、`@include`で呼び出す
- See this link here (Jump to another documents)
  - 参考 : https://qiita.com/nekoneko-wanwan/items/c8498a21ae0e2b2198be
  - 参考 : https://www.webcreatorbox.com/tech/sass-mixin
  - 参考 : https://dotinstall.com/lessons/basic_sass/10214

## 6. Eject for expansion and adjustment

nothing to do for now.

## 7. Make details of ArtWorks component

- 画像は `import lipstick from './../../assets/img/lipstick.png';` でインポートし、
`<img src={lipstick} alt="lipstick" />`で呼び出す

- ArtWorks.scssで呼び出している変数`$colorblack`は、config.variables.scssで作成しているものをinvokeしている

## 8. Set hover state

- stateをつけることで状態を変化させる (InitialiseしてからHoverされている状態、されていない状態をそれぞれ定義)
- Stateで定義した状態をSetstateで更新することで、Virtual DOMに再描画する。
- このとき、Stateが変化した特定のコンポーネントのみが再描画されるため、同期処理で上から順に読み込まれるのに比べて読み込みが高速化する
- hoverinした時のstate, hoveroutした時のstateをそれぞれ[onMouseOver, onMouseLeaveというReactのイベント処理にあてはめている](https://reactjs.org/docs/events.html#mouse-events)
  

## 9. Send props from artworks.jsx to Toppage.jsx

### Toppage.jsx(親コンポーネント) 
- Containerの中でArtworksをPropsとして定義している

```
<ArtWorks
    // key, imageUrl, title, categoriesはすべてprops
    // *ここでpropsを定義している → そのためにArtworkでPropsの定義が可能になる*
    key={artworks.title}
    imageUrl={artworks.imageUrl}
    title={artworks.title}
    categories={artworks.categories}
/>
```

### Artworks.jsx(子コンポーネント)

- レンダリングされたタイミングでthis.propsの中身を見ると、ObjectとしてToppage.jsxで定義したArtworksの中身が渡ってきているのがわかる

```
console.log(this.props);
// 中身
categories: (2) ["Vector", "Artwork"]
imageUrl: "/static/media/lipstick.76eb63fd.png"
title: "Lip Stick"
key: (...)
```

- 親(Toppage.jsx)から渡ってきたものをpropsとして定義

```{imageUrl: "/static/media/lipstick.76eb63fd.png", title: "Lip Stick", categories: Array(2)}
const { imageUrl, title, categories } = this.props;
```

- propsから渡ってきたimageUrl, title, categoriesをそれぞれ、`<img src={imageUrl} />`,`<h3>{title}</h3>`, `<p>{categories}</p>`に置き換える

## 10. Mapping Array from constants

- App.scssの内容はindex.scssへ移植
- ```constants```というディレクトリの中に```artworks.js```を作成して、そこへ作品一覧となる配列を格納
- artworks.jsで```artworks```を定義して配列をToppage.jsxへエクスポート
- Toppage.jsxでは```lipStick```を```{ artworks }```に置換して、mapで配列の一覧を呼び出すようにする
- categoryもmapから呼び出す

From Saayaman-san below:

- UrlをConstantsを読める様にするには、ModuleScopePluginを外す [See link (stack overflow)](https://stackoverflow.com/questions/44114436/the-create-react-app-imports-restriction-outside-of-src-directory)
- 配列をMAPする(key attributeを忘れずに!)


## 11. Pass children by making Container component

What is children? - [See link](https://reactjs.org/docs/react-api.html)
Childrenを使うことで、子要素をwrapするような子要素を記述することができる

## 12. Add another package (by either NPM or Yarn)


|Package name|how to use|resource|
|----|----|----|
|react-media|`<media>`コンポーネントがCSSメディアクエリと一致するかどうかを判別し、それに基づいてレンダリングする|https://www.npmjs.com/package/react-media|
|prop-types|Propsの型情報をJavaScriptのコードとして定義し、コンポーネントに付加情報として加えることで、Propsに渡されたデータをチェックできるようになる|https://www.npmjs.com/package/prop-types|
|classnames|要素のクラスを動的につけたり外したりする|https://www.npmjs.com/package/classnames|
|react-router|reactでルーティングするためのデファクトのライブラリ|https://www.npmjs.com/package/react-router|
|react-router-dom|ルーティングとヒストリーAPIを操作する用途を兼ねる|https://www.npmjs.com/package/react-router-dom|

How to install in NPM and Yarn
in NPM
```
$ npm i react-media 
$ npm i prop-types
$ npm i classnames
$ npm i react-router
$ npm i react-router-dom
```
in Yarn
```
$ yarn add react-media 
$ yarn add prop-types
$ yarn add classnames
$ yarn add react-router
$ yarn add react-router-dom
```

## 13. Show hamburger icon by using React-media

1. import **React-media** above in Header.jsx

```
import Media from 'react-media';
```

- React-media is for identify media query. if condition inside of `<Media>` was matched, media query will active.

2. Importしたreact-mediaを、三項演算子を使ってマッチした場所に適応させる

```
<Media query="(min-width:540px)">
    {/* 540px以上なら以下を表示 (三項演算子を使用して条件分岐している)*/}
    {(matches) => (matches 
    ? 
    <ul className="Header-menu">
        <li>Top</li>
        <li>Works</li>
        <li>Bio</li>
        <li>Contact</li>
        <li><a href="http://suzydp.net">suzydp.net</a></li>
    </ul>
    :
    <img 
        width={30}
        alt="Menu Icon"
        src={require("./../../assets/icons/menuIcons.svg")}
    />
    )}
</Media>
```

## 14. Add active class by using Classname

- **Classname**は、使用することで特定のstateがsetされているときにそのクラスを追加してくれる

1. import **Classname** above in Artworks.jsx

2. `isHovered`が適用されているときに`Artworks-title--active`が追加されるよう、下記のように記述

```
<h3 className={cx({ "Artworks-title--active": isHovered })}>{title}</h3>
```

3. Hoverした状態の時に、`Artworks-title--active`クラスのスタイルが適用される

## 15. Classname can use for adding default className

デフォルトのクラス名、isHoveredした時のクラス名をそれぞれ記載しておいて、SCSSでまとめて書く、という方法もある

- Artworks.jsx

```
<h3 className={cx("Artworks-title",{ "Artworks-title--active": isHovered })}>{title}</h3>
```

- Artworks.scss

```
.Artworks-title{
    /* h3の内容を移植　*/
    font-size:2rem;
    width:max-content;
    margin:1rem auto;

    &--active{
    color: $colorpink;
    transition: .4s color;
    }
}
```

## 16. Add Proptypes to check data-type in props

### What's PropTypes?

- PropTypesとは、Propsに渡されたデータをチェックできるようにするデバッグツールのこと(FBが提供しているNPM)
- 仕様書通りにデータ型が渡っているかPropsをチェックする手間はこれで省くことができる
- この中に定義したこと以外のことを書いている場合はDebug consoleに警告が表示される

## 17. Make Root of links by using React-router

### What's Router?

- そもそもルーティングとは： - パケットの配送経路(Route)を決定する動作のこと。
- 宛先が同じネットワークには直接通信でパケットを送ることができるが、異なるネットワークある端末にパケットを送るにはあらかじめデフォルトゲートウェイに指定されたルーターに中継を依頼する必要がある

## 18. Apply NavLink on header from React-router-dom

- 先のコミットで出てきたRouterを使ってHeaderにLinkをApplyする