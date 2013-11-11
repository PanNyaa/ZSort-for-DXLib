ZSort-for-DXLib
===============

DXライブラリ用のZソート風画像表示の実装＆ちょっとしたサンプルプログラムです。
.

.

.

.

.


          SetDrawBlendMode(DX_BLENDMODE_ALPHA,128);
          DrawGraph(0,0,GrHandle,TRUE);
          SetDrawBlendMode(DX_BLENDMODE_NOBLEND,0);

--使い方

・まずは、DxZSortLib.h（お好みで名前変更したほうがいいです）をインクルードする

・ゲームループ前の初期化部分( DxLib_Init(); とかしてるところ)で、SetZSortInit();をする

・ゲームループ内で、DrawGraph(x,y,handle,TRUE,DX_BLENDMODE_ALPHA,128,Z_SORT_LOWER);みたいなことをする
          (Z_SORT_LOWERのデフォルト定義値は99、Z_SORT_UPPERの定義値(1)との間で調整する
          (99→一番奥に描画　1→最前面に描画
          
・ゲームループ末端( ScreenFlip(); の直前くらい )で、DrawZCollectedGraph();をする

・DrawGraphのZ_SORT_LOWER～Z_SORT_UPPERの間で調整した優先順位順で、画像が描画される
.

.

.

.

.

--対応してないこと↓

・マスク機能
          (CreateMaskScreen();をしてからの、
          (SetUseMaskScreenFlag(1);～SetUseMaskScreenFlag(0);の間でDrawMask→DrawGraphをしてもマスク処理が適用されない
          (理由は、DrawGraphをしたときに画像関連データを次々と保持するだけで表示自体はせず、
          (メインループ終端でまとめて表示しているため、
          (SetUseMaskScreenFlag(1);～SetUseMaskScreenFlag(0);の適用圏内に入らない
          
          
・DrawGraphを挟む使い方での、SetDrawBlendMode↓
          (例えば、
          
          SetDrawBlendMode(DX_BLENDMODE_ALPHA,128);
          DrawGraph(0,0,GrHandle,TRUE);
          SetDrawBlendMode(DX_BLENDMODE_NOBLEND,0);
          
          (という画像表示をすると半透明のGrHandleが描画されますが、マスクが適用されないのと同じ理由で適用されません。
          (しかし、DrawGraphの引数が6つある、
          
          int DrawGraph(int x,int y,int GrHandle,int TransFlag ,int BlendMode,int alpha);
          
          (でブレンドモードの指定ができます。
          
          DrawGraph(0,0,GrHandle,TRUE,DX_BLENDMODE_ALPHA,128);
          
          (↑のような使い方ができます。
          
          
・他にもあるかもしれません(しろめ
.

.

.

.

.



