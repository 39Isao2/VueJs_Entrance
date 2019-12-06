# Vue.Js超入門!
猫本使ってVue.js超入門します！  （参考著書:基礎から学ぶ Vue.js）

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
