# JS Girls Osaka #1 サンプルコード

## ドロワー

### パターン1

[demo](http://re-dzine.net/jsgirls-sample/drawer1/)

- メニューボタンのクリックでの開閉
- スライドアニメーションをjQueryの``animate()``で実現
- ``position``プロパティの``left``/``right``の値を操作
- スライドアニメーションはIE8でも動作

### パターン2

[demo](http://re-dzine.net/jsgirls-sample/drawer2/)

- メニューボタンのクリックでの開閉
- スライドアニメーションをCSSの``transition``プロパティで実現
- ``position``プロパティの``left``/``right``の値を操作
- スライドアニメーションはIE10以上で動作、一部ブラウザでは``transition``プロパティに``-webkit-``プレフィックスが必要（[参照：Can I use](http://caniuse.com/#feat=css-transitions)）

### パターン3

[demo](http://re-dzine.net/jsgirls-sample/drawer3/)

- メニューボタンのクリックでの開閉
- スライドアニメーションをCSSの``transition``プロパティで実現
- ``transform``プロパティの``translateX``の値を操作
- ``transform: translateZ(0)``によりハードウェア・アクセラレーションを有効化しスムーズにアニメーションさせる
	- 【参考】 [Web制作にGPU処理を取り入れる｜Web制作 W3G](https://w3g.jp/blog/studies/web_gpu_adopt)
	- 【参考】 [Webアニメーションを高速化するために知っておくべき10のこと（前編） | HTML5Experts.jp](http://html5experts.jp/cssradar/2027/)
	- 【参考】 [スムーズなアニメーションを実装するコツと仕組みを説明するよ。CPUとGPUを理解しハードウェアアクセラレーションを駆使するのだ！（Frontrend Advent Calendar 2013 – 06日目） | Ginpen.com](http://ginpen.com/2013/12/06/hardware-acceleration/)
	- 【参考】 [Dev.Opera — CSS will-changeプロパティについて知っておくべきこと](http://dev.opera.com/articles/ja/css-will-change-property/)
- スライドアニメーションはIE10以上で動作、一部ブラウザでは``transition``プロパティ（[参照：Can I use](http://caniuse.com/#feat=css-transitions)）および``transform``プロパティ（[参照：Can I use](http://caniuse.com/#feat=transforms2d)）に``-webkit-``プレフィックスが必要

### パターン4

[demo](http://re-dzine.net/jsgirls-sample/drawer4/)

- パターン3のプラスアルファ版
- ドロワーの開閉にタッチイベントを使うことでスマホなどタッチデバイスにおける操作をより快適に
- メニューボタンだけでなくコンテンツ部分のクリック/タップでドロワーを閉じるようにすることでより使いやすく

### パターン5

[demo](http://re-dzine.net/jsgirls-sample/drawer5/)

- パターン4をjQueryを使わずに書いたもの
