# HowToMakeSave_json_Unity
## Unityバージョン
2020.3.29f1

## はじめに
サルでもわかるUnityの会話システムの作り方のチュートリアルです！サルである著者が書いたので本当です！🐵  
三人称視点の3Dゲームを作りながら、「NPCに近づき、会話ボタンを押すと会話が始まる」というのが基礎編となります。よりクオリティを高めたい方はスクロールして応用編もご覧ください。  
とにかくわかりやすいように、Unityエディターのスクショは一部分でなく全体を映し、スクリプトに追記するときも全文記載しながらゲームを一緒に作っていきます。  
さっそくこのReadMeに沿って実践してみましょう。なお、リポジトリのファイルはゲームの完成品なので、このReadMeさえ見ればセーブシステムは作れます。万が一作り方がわからなければダウンロードして確認してみましょう。  
（このプロジェクトはこちらを参考に作りました：  [ユニティちゃんのRPGを作ってみよう5ー村人との会話ー|Unityを使った３Dゲームの作り方（かめくめ）](https://gametukurikata.com/letstrymakeit/unitychanrpg/unitychanrpg5)）  

## 目次
**サルでもわかる制作の流れ（基礎編）**
- **①3Dシーンの作成**  
    - 公式アセットからインポートしたシーンに会話相手を配置  
    - 会話相手を追加  
    - 会話を表示するUIを追加  
    - 会話可能アイコンのUIを追加  
- **②スクリプトを作成**
    - 必要なスクリプト4つ
    - 会話範囲に入った時に実行するスクリプト
    - プレイヤーのコントローラースクリプトを改修
    - 会話処理用スクリプト
    - 村人の会話内容ファイルを作成するスクリプト  
    
**サルでもわかる制作の流れ（応用編）**
- **①会話内容をテキストファイルに変更する** 
- **②UIを画面比率に合わせる** 
- **③話しかけた時にNPCをこちらに向かせる** 


## サルでもわかる制作の流れ（基礎編）
###  ①3Dシーンの制作
#### 公式アセットからインポートしたシーンに会話相手を配置  
このチュートリアルではUnityストアからインポートしたアセット内のシーンを元に作っていきます。  
それではまず3Dテンプレートから新規プロジェクトを作成して下さい。次にパッケージマネージャーからこちらの公式アセットをダウンロードおよびインポートしてください。[Starter Assets - Third Person Character Controller](https://assetstore.unity.com/packages/essentials/starter-assets-third-person-character-controller-196526)  
すると「このアセットはNew Input Systemを使っている。プロジェクトの設定を変更して再起動してもええか？」という内容のダイアログが出てくることがあると思いますが、「はい」を選択して再起動されるのをお待ちください。


無事インポートが完了いたしましたら、StarterAssets/ThirdPersonController/Scenes内のPlaygroundというシーンをダブルクリックして開きます。ではこの素晴らしいUnityの公式アセットの実力を見るために再生してみましょう。マウスでカメラ移動、WASD(+Shift)でキャラクターを動かせます。  
![スクリーンショット (84)](https://user-images.githubusercontent.com/82185511/184536261-dc98a5c1-1847-438f-9062-7e68280689f6.png)


#### 会話相手を追加  
大変素晴らしいアセットですが、プレイヤー1人では可哀想ですね。会話相手を追加しましょう。StarterAssets/ThirdPersonController/Character/ModelsからArmatureというモデルを、目の前の壁前に適当に配置しておきましょう。  
それからややこしいので、名前を「Armature」から「NPC1」に変更しましょう。![スクリーンショット (87)](https://user-images.githubusercontent.com/82185511/184537799-278527fc-2ec8-4c41-a606-6fdd87151b3b.png)

続いてNPC1にコライダーを追加します。プレイヤーが接近したら会話が出来ることを検知するための範囲になります。NPC1の子として「SearchArea」という空のオブジェクトを配置し、スフィアコライダーコンポーネントを追加します。トリガーにチェック、中心のyを1、半径を2にしてください。![スクリーンショット (89)](https://user-images.githubusercontent.com/82185511/184541204-4a7fea4a-0364-4679-baa6-f50a4ff42e41.png)




#### 会話を表示するUIを追加  
キャンバスに会話を表示させます。  
ヒエラルキー上で右クリックからUI>パネルを選択し、作成されたキャンバスの名前をTalkUIに変更します。続けて今パネルを選択した状態で右クリックからUI>画像、UI>テキストを作成します。  
まずパネルをいい感じにします。私はAlt+Shiftでアンカーを設定し、位置や幅/高さをこんな感じにしました。![スクリーンショット (90)](https://user-images.githubusercontent.com/82185511/184541465-36b711cc-0fbd-423a-87c6-e47d15d061b1.png)  
画像のパラメータはこんな感じ。アンカーをbottom rightにし、パネルの右下に表示されるようにします。幅と高さは30にして、画像のソース画像にはDropdownArrowを設定します。![スクリーンショット (93)](https://user-images.githubusercontent.com/82185511/184541440-ec63c166-b276-4b02-9214-80cdd28577ca.png)  
テキストのパラメーターはこんな感じに変更。アンカーはstretch stretchにし、パネルのサイズに合わせて伸縮するようにします。
またFont Sizeを25、Colorを白色にします。![スクリーンショット (94)](https://user-images.githubusercontent.com/82185511/184541637-4b668b9f-d390-4626-92e3-17571f454cf7.png)













## さいごに
「サルでもわかる」の謳い文句につられたあなたは不覚にもfor文を覚えてしまった訳ですが、今回のセーブ方式には良いところがあります。Saveで作成したjsonファイルを開いてみましょう。  
`{"flagStrToSave":"111"}`  
このように、我々はゲームの制作者ですからこの数字が意味するところは分かりますが、勘の悪いプレイヤーが見れば「111？なんのこっちゃ？」と思うことでしょう。つまり、セーブの変数をもっと複雑にすれば、jsonファイルをいじられてセーブデータを改造される恐れがなくなる、いわゆる**暗号化**処理が行えます。  

いかがでしたでしょうか。もしわからないところがあればコメントして頂ければ答えらえる範囲でお答えいたします。ではまた。🐒  
