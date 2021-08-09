# Vue.Js超入門! 
猫本使ってVue.js超入門します！  （参考著書:基礎から学ぶ Vue.js の一部）

<img src="https://images-na.ssl-images-amazon.com/images/I/51UVfJB%2B8sL._SX351_BO1,204,203,200_.jpg" width="150px">

# イントロダクション

## これからのJavaScript
はるか昔、JavaScriptはカーソルにキラキラ星を追尾させるのが主な仕事でした。　
しかし、ここ数年のwebフロントエンド技術の進歩により、jsは単なる飾り装飾だけではなく、
複雑なUIやWeb&スマホアプリや、なんとデスクトップアプリの実装にも使われるようになりました。

そんな中、「Vue.jsが楽しい！」フロントエンド界隈でこのワードを耳にすることが多くなりました。
「フレームワークって難しそう...」「Node.js? webpack? なんか必要知識が多そう」そんな風に感じる方も多いのではないでしょうか。
しかし！なんとVueはたったこの一行を読み込めば使えます！   


    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

（あらまぁjQueryみたい！）


## Vue,jsについて&コンセプト
「フレームワークは沢山の機能を持ったプロダクトで使われる」というイメージを持っている方が多いかもしれませんが、
Vue.jsは手軽に小さくはじめられることも大切なコンセプトとして作られています。

Vue.jsは、Evan You氏の個人プロジェクトとして始まり、2014年にリリースされました。
2015年にはphpフレームワーク「Laravel」んpフロントエンジンとして使用され、一気に知名度がアップ。
Adobeや任天堂、LineやGitLabなどでも採用されています。


Vueの２代要素
・リアクティブデータバインディング（今回はこっちの簡単なUI周りに触れます）
・コンポーネント

https://v1-jp.vuejs.org/guide/overview.html（公式サイト）


# さぁ、まずは書いてみる！

雛形↓

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>初めてのvue.js</title>
    </head>
    <body>
        <div id="app">
        
        </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script>

        </script>
    </body>
    </html>

１、アプリケーションの作成をはじめるには、コンストラクタ関数Vue()を使ってVueインスタンスを作成します。

    var app = new Vue({
        // ここにこの後、色々記述
    });


２、テンプレートに次のようにプロパティ名を記述するとその場所に値を描画します。

    // HTML
    <p>{{ message }}</p>
    
    
    // JavaScript
    var app = new Vue({
  
        el:'#app',
        
        data:{
            message: "ここに好きなテキスト〜"
        }
    });
    
# いろんな基本機能 （チャプター1より）

## 繰り返しの描画（foreach的な） v-for
 
    // HTML
    <ul>
        <li v-for="item in list">{{ item }} </li>
    </ul>
    
    
    // JavaScript
    var app = new Vue({
  
        el:'#app',
        
        data:{
            list: ['秋葉原','六本木', '配列で追加可能']
        }
    });
 

## イベントの利用（onclick等） v-on:click
 
    // HTML
    <button v-on:click="handleClick">ボタンを押す</button>
    
    // JavaScript
    var app = new Vue({
  
        el:'#app',
        
        // 関数はここに登録
        methods: {
            handleClick: function(event){
                alert(event.target + "オンクリックイベント");
            }
        }
    });
 
 
 参考（jQueryなしでさくっと色々作れそう...）
 
 【脱jQuery】Vue.jsで簡単に「トップへ戻るボタン」を作る方法
 https://masatoshihanai.com/vue-scrollto/
 
 Vue.jsでスクロールを検知する
 https://qiita.com/SatoTakumi/items/d88df8afae82c53d2d2a
 
 
 ## フォーム入力と同期（リアルタイムで描画） v-model
 
    // HTML
    <p>{{ message }}</p>
    <input v-model="message">
    
    // JavaScript
    var app = new Vue({
  
        el:'#app',
        
        data:{
            message: "初期メッセージ"
        }
    });


 ## 条件分岐 v-if
 
    // HTML
    
    <!-- showプロパティがtrueの時だけ表示 -->
    <p v-if="show">ここが出たり消えたり</p>
   
    <button v-on:click="show=!show">トグルボタン</button>
    
    // JavaScript
    var app = new Vue({
  
        el:'#app',
        
        data:{
            // showプロパティがボタンを押すたびにtrue/falseに変化
            show: true
        }
    });
    
    
## コンポーネント基本

```
<div id="app">
    <hello/>
</div>

<script>
    // JavaScript
  Vue.component('hello', {
      data:function(){
          return {
          message: "これはメッセージです"
          };
      },
      template: '<p class="hello">{{message}}</p>'
      
  });


    var app = new Vue({
        el:'#app',
    });
</script>

```

## props(親から子にデータを渡す)

```

Product.vue

<template>
  <h3>{{ name }}</h3>
</template>

<script>
export default {
  name: "Product",
  props: ["name"],
};
</script>

<style>
</style>


App.vue

<template>
  <div id="app">
    <Product name="トートバッグ" />
  </div>
</template>

<script>
import Product from "./components/Product.vue";

export default {
  name: "App",
  components: {
    Product,
  },
};
</script>

```

## class名の追加と削除 v-bind


```

    <div id="app">
        <div class="btn">
            <button v-on:click='is_active=!is_active' v-bind:class='{active:is_active}'>押して！</button>
        </div>
      </div>

<script>


// JavaScript
    // JavaScript
    var app = new Vue({
        el: '#app',
        data: {
            is_active: false
        }
    });

</script>
  ```
'''
 
## Vue.jsでtopへ戻る
```

<style>
.top-btn{
    position: fixed;
    bottom: 10px;
    right: 10px;
}
</style>
</head>
<body>
    <div id="app">
          クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーークリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーーーーっ！！！<br><br>クリリンのことかーーー

            <a class="top-btn" v-on:click="scrollTop">
                トップへ戻る
            </a>
        </div>
<script>
new Vue({
  el: '#app',

  methods: {
    // スクロールトップメソッド
    scrollTop: function(){
      window.scrollTo({
        top: 0,
        behavior: "smooth"
      });
    }
  }
})

```
 
 
# トランジションとアニメーション
Vue.jsの「トランジション」はCSSトランジション/アニメーションをより簡単に使いやすくサポートする機能。

    <button v-on:click="show=!show">トグルボタン</button>
    <transition>
        <div v-show="show">トランジションさせたい要素</div>
    </transition>

transition要素で囲むと中身がDOM要素に追加される時に「enter」、
DOM要素から削除される時には「leave」という文字を含んだクラスが付与される。

    // css <style>タグの中に
    
    /*1秒かけてfadeIn*/
    .v-enter-active, .v-leave-active{
        transition:opacity 1s;
    }
    
    .v-enter, .v-leave-to{
        opacity:0;
    }
     
トランジションの使い分け
    
    <transition name="demo">
        <div v-show="show">トランジションさせたい要素</div>
    </transition>
    
    /*5秒かけてfadeIn*/
    .demo-enter-active, .demo-leave-active{
        transition:opacity 5s;
    }
    
    .demo-enter, .demo-leave-to{
        opacity:0;
    }
    
    /*
        初期描画時にもトランジション実行
        <transition appear>
            <div v-show="show">トランジションさせたい要素</div>
        </transition>
    *?

ーーーーーーーーーーーーーーーーーーーーーーーーーーーーー<br>
要素追加<br>
.v-enter トランジション開始前<br>
.v-enter-to トランジション中<br>
.v-enter-active トランジション終了（要素存在）<br>

要素削除<br>
.v-leave トランジション開始前<br>
.v-leave-to トランジション中<br>
.v-leave-active トランジション終了<br>
ーーーーーーーーーーーーーーーーーーーーーーーーーーーーー

## これだけ覚えておくと迷わない らしい

要素が追加される時は .v-enter から .v-enter-to<br>
要素が削除される時は .v-leave から .v-leave-to


    <style type="text/css">

    div{
        width: 800px;
        height: 800px;
    }
        .v-enter-active,
        .v-leave-active{
        transition:all 1s;
    }

    /* 表示する時は左から */
    .v-enter{
        opacity: 0;
        transform: translateX(-10px);
    }
    /* 消える時は下へ */
    .v-leave-to{
        opacity: 0;
        transform: translateY(10px);
    }
    </style>
    
    <button v-on:click="show=!show">トグルボタン</button>
    <transition>
        <div v-show="show">トランジションさせたい要素</div>
    </transition>



参考！<br>
Vue.jsでスライドショー！<br>
https://qiita.com/ryo511/items/4c65caffb01ba13fb89b<br>
https://qiita.com/yske/items/7bc0df9bf0a82d222422<br>
<br>
(スタンダードなUIからVueに慣れる②)　タブ切り替えがjs6行<br>
https://qiita.com/yske/items/7f1305ed904963d93729
