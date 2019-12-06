# Vue.Js超超入門! 
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

## 繰り返しの描画（foreach的な）
 
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
 

## イベントの利用（onclick等）
 
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
 
 
 ## フォーム入力と同期（リアルタイムで描画）
 
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


 ## 条件分岐
 
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

## これだけ覚えておくと迷わない

要素が追加される時は .v-enter から .v-enter-to
要素が削除される時は .v-leave から .v-leave-to
