# JS Girls Osaka #1 サンプルコード

## ドロワー

### ドロワーとは



### コーディングパターン

[コーディングのベースファイル](https://github.com/jsgirls-osaka/handson01-drawer)

#### パターン1

[demo](http://re-dzine.net/jsgirls-sample/drawer1/)

- メニューボタンのクリックでの開閉
- スライドアニメーションをjQueryの``animate()``で実現
- ``position``プロパティの``left``/``right``の値を操作
- スライドアニメーションはIE8でも動作

#### パターン2

[demo](http://re-dzine.net/jsgirls-sample/drawer2/)

- メニューボタンのクリックでの開閉
- スライドアニメーションをCSSの``transition``プロパティで実現
- ``position``プロパティの``left``/``right``の値を操作
- スライドアニメーションはIE10以上で動作、一部ブラウザでは``transition``プロパティに``-webkit-``プレフィックスが必要（[参照：Can I use](http://caniuse.com/#feat=css-transitions)）

#### パターン3

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

#### パターン4

[demo](http://re-dzine.net/jsgirls-sample/drawer4/)

- パターン3のプラスアルファ版
- ドロワーの開閉にタッチイベントを使うことでスマホなどタッチデバイスにおける操作をより快適に
	- 300msディレイ問題
		- タッチイベントには、``touchstart``（画面に指が触れた）``touchmove``（画面上で指が動いている）``touchend``（画面から指が離れた）``touchcancel``（タッチイベントをキャンセル）がある（[Appleによる詳細説明](https://developer.apple.com/library/ios/documentation/AppleApplications/Reference/SafariWebContent/HandlingEvents/HandlingEvents.html)）
		- iPhoneやAndroidのwebkitでは、``touchend``してから``click``イベントが起きるまでに300ms程度の待ち時間がある
		- その待ち時間では、ダブルタップによるズーム（一度画面から指を離してから、もう一度タップされるかどうか）の判定をしている
		- つまり``click``イベントだとその待ち時間によってタッチデバイスではモッサリ（反応が鈍い）ように感じるため、タッチイベント（``touchstart``か``touchend``）を使う方がよい
	- ``touchstart``と``touchend``どちらがいいのか問題
		- コードでは``touchstart``でイベントが起きるようにしているが、それだとその要素がある場所（より画面の中央に近い位置など）によっては、ただ画面をスクロールしたいだけなのに、指を置いた場所に``touchstart``でイベントが起きる要素があると、スクロールできずにイベントが発火してしまい、ユーザーの意図した操作ができなくなってしまう
		- 一方``touchend``にした場合、要素の外から指を動かしてきて、その要素の上で指を離すと``touchend``イベントが発火してしまう
		- 逆に言うと、``touchend``だともし間違ってタップしてしまったとしても、指をそのまま画面の外に出してしまえばキャンセルできるという利点があったりする
		- その辺りを厳密に処理しようと思うと、``touchstart``を検知してから``touchmove``で指を動かしたかどうかを確認し、動かしてなければ``touchend``としてそれを「タップした」と判定する必要がある
		- その処理を自前で書くのもいいが、プラグインを使う手もある（[ftlabs/fastclick](https://github.com/ftlabs/fastclick)）
	- Win8対応めんどい問題
		- Win8は、画面のタッチもでき、マウスでの操作もできるということを前提に設計されたOS
		- Win8上で動くChromeやFirefoxにはタッチイベントが実装されているため、このパターン4のコードだとマウスで操作しても``click``イベントが使われず、何も反応しないことになる（``mousedown``/``mousemove``/``mouseup``で設定したイベントも同様）
		- 一方、Win8上のIE10は、画面のタッチを内部的にマウスイベントに置き換えて処理するため、タッチでもマウスでもパターン4のコードで動作する
		- Win8のIE10以降では、Microsoft独自仕様の[Pointer Events](http://www.w3.org/TR/pointerevents/)が使える
		- このPointer Eventsによって、マルチタッチに対応したり、スタイラスペンのタッチに反応したり、筆圧やペンの傾きを検出できたりする
			- 【参考】 [Windows8 + IE10 でCanvasお絵描きツールを - Intelligent Technology&apos;s Technical Blog](http://iti.hatenablog.jp/entry/2013/07/19/162133)
- メニューボタンだけでなくコンテンツ部分のタップ/クリックでもドロワーを閉じるようにすることでより使いやすく
	- 今回のHTMLでは、メニューボタンがコンテンツ``#content``の中に含まれているので、メニューボタンのイベントが``#content``に伝播（バブリング）して``#content``に設定したイベントが発火してしまう
	- これをイベントバブリングという
		- 【参考】 [jQueryのバブリングと、「return false;」「e.stopPropagation();」「e.preventDefault();」について](http://blog.neo.jp/dnblog/index.php?module=Blog&action=Entry&blog=pg&entry=3107&rand=66027)
	- これを防ぐために、メニューボタンのイベント設定で``event.stopPropagation()``しておき、イベントがバブリングしないようにする
	- じゃあ何でもかんでもイベントバブリングを止めておけばよいかというとそうでもなく、イベントデリゲートも止まってしまうという弊害もあるので注意が必要
		- 【参考】 [jQueryのイベントハンドラでreturn falseするとイベントのバブリングが止まる](http://webtech-walker.com/archive/2012/09/event_handler_return_false.html)
		- 【参考】 [jQuery の on() と off() を理解する - tacamy.blog](http://tacamy.hatenablog.com/entry/2013/03/03/213113)

#### パターン5

[demo](http://re-dzine.net/jsgirls-sample/drawer5/)

- jQueryを使わずに書いたもの
