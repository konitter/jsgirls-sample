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
- スライドアニメーションはIE10以上で動作、一部ブラウザでは``transition``プロパティ（[参照：Can I use](http://caniuse.com/#feat=css-transitions)）および``transform``プロパティ（[参照：Can I use](http://caniuse.com/#feat=transforms2d)）に``-webkit-``プレフィックスが必要

### パターン4

[demo](http://re-dzine.net/jsgirls-sample/drawer4/)

- パターン3のプラスアルファ版
- ドロワーの開閉にタッチイベントを使うことでスマホなどタッチデバイスにおける操作をより快適に
- メニューボタンだけでなくコンテンツ部分のクリック/タップでドロワーを閉じるようにすることでより使いやすく

### パターン5

[demo](http://re-dzine.net/jsgirls-sample/drawer5/)

- パターン4をjQueryを使わずに書いたもの
