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
	- 300msディレイ問題
		- タッチイベントには、``touchstart``（画面に指が触れた）``touchmove``（画面上で指が動いている）``touchend``（画面から指が離れた）``touchcancel``（タッチイベントをキャンセル）がある
		- iPhoneやAndroidのwebkitでは、``touchend``してから``click``イベントが起きるまでに300ms程度の待ち時間がある
		- その待ち時間では、ダブルタップによるズーム（一度画面から指を離してから、もう一度タップされるかどうか）の判定をしている
		- つまり``click``イベントだとその待ち時間によってタッチデバイスではモッサリ（反応が鈍い）ように感じるため、タッチイベント（``touchstart``か``touchend``）を使う方がよい
	- ``touchstart``でいいのか問題
		- コードでは``touchstart``でイベントが起きるようにしているが、それだとその要素がある場所によっては、ただ画面をスクロールしたいだけなのに、指を置いた場所に``touchstart``でイベントが起きる要素があると、スクロールできずにイベントが発火してしまい、ユーザーの意図した操作ができなくなってしまう
		- 一方``touchend``にした場合、要素の外から指を動かしてきて、その要素の上で指を離すと``touchend``イベントが発火してしまう
		- 厳密に処理しようと思うと、``touchstart``を検知してから``touchmove``で指を動かしたかどうかを確認し、動かしてなければ``touchend``としてそれを「タップした」と判定する必要がある
		- その処理を自前で書くのもいいが、プラグインを使う手もある（[ftlabs/fastclick](https://github.com/ftlabs/fastclick)）
- メニューボタンだけでなくコンテンツ部分のタップ/クリックでもドロワーを閉じるようにすることでより使いやすく

### パターン5

[demo](http://re-dzine.net/jsgirls-sample/drawer5/)

- パターン4をjQueryを使わずに書いたもの
