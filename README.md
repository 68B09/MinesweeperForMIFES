# Minesweeper for MIFES
【必ず読むこと】
------
・マクロのバグによってMIFESがハングアップしてしまうかも知れません。  
・マクロのバグによってMIFESで開いているファイルが壊れるかも知れません。  
・ゲームを終了するときはMIFESも終了させてください。  
・上記をご理解頂いた上、本マクロの利用は自己責任でお願いします。  

![3](https://user-images.githubusercontent.com/11640544/222715182-59c507f7-b22f-4eae-9c8c-d40a497a05b2.png)  

【これってなに？】
------
最近のMIFESのマクロはどれくらいのことが出来るんだろうと思って試しに作ってみた「マ○ンスイーパーもどき」です。  

【どうやって動かすの？】
-----
MIFES11が必要です。  
未確認ですがもしかするとMIFES10でも動くかも知れません。  

1. mine.macを取得してMIFES11で開く。  
2. ファイル全体をコンパイル。500行弱あるのでコンパイルに数秒かかります。  
3. マクロが暴走しても被害が出ないように全てのファイルを閉じる。閉じないと実行出来ないようにしています。  
![202302261032_002](https://user-images.githubusercontent.com/11640544/222411398-5c28a9cc-34ff-4fdb-a8f7-4032a372ec20.png)

4. カレントマクロの実行。

で動き出すと思います。  

【操作方法】
-----
操作方法はウィンドに表示してますが、  
[A] 現在地を開く(本家の左ボタンクリック)  
[S] マークに従って開く(本家の左右ボタン同時クリック)  
[D] マーク切換(本家の右ボタンクリック)  
[←↑↓→] カーソル移動  
[ESC] ゲーム終了  
です。   
なお操作はキーボードオンリーです。マウスでの操作はできません。  

それと表示されている文字の意味は、  
■=未開封マス  
☒=機雷チェック  
数字=周囲の機雷数  
＊=機雷  
です。  

【マクロの内容について】
-----
・環境によってはうまく動作しないかもしれません。  
例えばプロポーショナルフォントを使っている場合は綺麗に表示されませんし、冒頭の画像のようにアンダーラインが表示されます。  

・マクロ内で挿入・上書きモードなどを変更しています。  

・~~本家マインスイーパーの「数字の上で左右ボタン同時押し」の機能はありません。~~  
Ver1.1にて実装。  

・「連鎖開け」の処理に時間がかかります。  
再帰呼び出しを使用していない(引数付きで再帰呼び出しが出来ない)ため文字列用の配列を色々と操作しているためです。  
また文字列用配列の上限が2048個なので悪い条件の時に配列数が足りなくて落ちるかも知れません。  
さしあたり20x20マスに70個の機雷を配置している状態では問題無さそうですが・・・  

・乱数はマクロで作っています。  
現在のミリ秒を使用してシードを設定してはいますが、周期性があるので同じ盤面が出てくるかもしれません。  

・盤面のサイズは  
@@15 = `20`  
@@16 = `20`  
で変更出来ますが、先ほどの連鎖開け処理の仕様があるのであまり広くは出来ません。  

機雷の数は  
@@18 = (@@17 * `175`) / 1000  
のように総マス数の17.5%にしています。`175`を弄れば良いですが、総マス数を超えるような値にするとハングアップするんじゃないかな。  

・処理冒頭の  
@@31 = `0`  
の`0`を`1`にするとデバッグモードになり、現在位置に機雷があるかどうかがわかります。  
※表示されているMARKが3000なら安全地帯  

【ライセンス】
---
MIT License  

【更新履歴】
-----
2023.2.25 Ver1.0 zzo  

2023.3.1 Ver1.1 zzo  
周囲開け(Sキー)対応

2023.3.3 Ver1.2 zzo  
・現日時取得方法の変更  
・乱数シード値の設定に時と分も追加  
