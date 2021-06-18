# oTreeとは

* 経済ゲーム実験プログラムであり，webブラウザを使って実験できる．
* ベースはPythonで自由にプログラムを組むことができる．
* 詳細は別途資料へ


# oTreeのざっくりとした仕組み
### Djangoの考え方：MTVアーキテクチャ

MTVアーキテクチャ：Djangoの考え方として，それぞれのプログラムには大きく以下の3つの役割がある（らしい）．

​	この辺は独学中なので曖昧です．ごめんなさい．

| 名称     | 内容                                                         |
| -------- | ------------------------------------------------------------ |
| Model    | データアクセス関係の処理を担当する．webアプリとデータベースとの間のやり取りを実行する．oTreeでは主に`models.py`がその役割を担う．イメージとしては「必要なデータの定義」と「計算（ロジック）」を取り扱っている |
| Template | 画面表示関係を担当する．画面に表示されるwebページを作るための部分．oTreeでは主に`template`フォルダ内の各htmlファイルがその役割を担う．イメージとしては「どのようにデータを表示するか(How)」を示している． |
| View     | 画面表示関係を担当する．画面表示の順番と表示すべきデータ（入力項目）を定義している．oTreeでは主に`pages.py`(`views.py`)がその役割を担う．イメージとしては「何のデータを表示するのか(What)」を示している． |

* 本によってはMVCモデル（Model・View・Controller）によって説明されているが，Djangoに限って言えば違う角度から目を向けているだけ．
  * 基本的には同じ扱いをして良さそう．



### Djangoの考え方：プロジェクトとアプリケーション 

* 土台として「**プロジェクト**」を用意する．
  * 基本的にはここに直接プログラムを組み込むのではない．
* この中に新しい「**アプリケーション**」を作成・組み込んでいく．
  * 公共財ゲームや社会的ジレンマ，最終提案ゲームや独裁者ゲームなど．

# oTreeの下準備

## oTreeをインストールする

* 最初にインストールしましょう．

```
pip install -U "otree<5"
```
* Powershellかコマンドプロンプト(Win)，ターミナル(Mac)で上記コードを入力します．
  - インストール作業は以上です．
  - 必要に応じて追加のプログラムもインストールされます．
* 2021.3.3追記：`pip install -U otree`とした場合にはoTree Lite（新しいバージョン）がインストールされます．
  - こちらの資料はoTreeにしか対応していません．

## インストールがうまくいかない場合

1. Pythonのシステムパスは通っていますか？
   * [コチラ](https://www.javadrive.jp/python/install/index3.html)などを参考に確認してみてください．
2. Anacondaをインストールされている場合
   * インストール時に非推奨とされている「**Add Anaconda to the systemPATH environment variable**」にチェックを入れるとPowershellやコマンドプロンプト(Win)，ターミナル(Mac)でそのまま作業できます．
   * パスを通したくない場合**はAnaconda Navigator**を起動して，**Environment**へ，**base(root)**もしくは自身で用意しているならばそのEnvironmentの中にある**▶**をクリックします．そこで**Open Terminal**をクリックすると作業を進めていくことができます．

## プロジェクトを作る

* 今回はわかりやすいようにデスクトップでの作業を例とします．

* Windowsの場合
```
cd C:¥Users¥[ユーザ名]¥Desktop
```

* Macの場合
```
cd /Users/[ユーザ名]/Desktop
```

* 上記にてデスクトップに移動した後に，"otreetest"という名前のプロジェクトフォルダを作成します．
```
otree startproject otreetest
```
  - ここで様々な作業を行う感じです．


* Include sample games? (y or n)→ n
  - いきなり入れちゃうと面白くないから入れません．



# 一つのアプリの構成要素

## models：
* 実験内の変数を決める
  - 何期繰り返しか？
  - 何人プレイヤーか？
  - プレイヤー全員に影響する変数は何か？
  - プレイヤー個人が決定できる変数はなにか？
  - どういう計算を行わせるのか？
    - 関数を作成する．

## template：
* html形式で画面を作成する
  - どこに文字を出力するのか．
  - どこにを入力欄を作成するのか．  
  - どこに計算結果を出力するのか．

## pages：
* 各ページを表示した際に行う処理を決定する．
  - どこで関数を実行するのか？
  - どのページである変数を入力するのか？

* どういう順番でページ遷移を行うのか？



## settingにおけるsession config：

* oTree で実験を実装するには，`settings.py`の中の`SESSION_CONFIGS`に作成したアプリを登録する必要があります．
* ここでは複数のアプリをまとめて登録することもできます．


## サーバとして起動

* 自身の端末をサーバとして起動します．

```Python
otree devserver
```

  - これで自身の端末で実験を実施することができます．
  - [http://localhost:8000/](http://localhost:8000/)にアクセスしてみてください．



## oTree的な発想：こんなことを考えながらプログラムを考えると理解しやすい
* 何人プレイヤーか
* 全員に影響する変数は何か
* プレイヤー個人で決める変数は何か
* 何ページ作成するか
* どういうページ遷移を行うのか