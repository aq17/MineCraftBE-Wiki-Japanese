# Scripting API について

## Ver.1.12.0.2
MineCraftのベータバージョンの内容についてのドキュメントです。  
このバージョンの新機能、コンポーネント、および機能は、正式バージョンで同様に実装されるとは限らず、予告なく変更される場合があります。  
バージョンが変更されてアドオンが正しく動作しなくなった場合は、必ずこのドキュメントを確認してください。  
ベータ版向けに開発されたリソースパックおよびビヘイビアパックは、正式バージョンで正しくリリースするとは限りません。  

## Scripting システム
Scripting APIを動かしている、MineCraft Script Engineは、JavaScriptを使っています。  
JavaScriptプログラムを作成し、それをビヘイビアパックに読み込ませれば、イベントを起こしたり、エンティティが持っているデータを取得・変更したり、ゲームの様々な部分に干渉する事ができます。  

### サンプルワールド
Scripting APIで開発を始めるときに役立つサンプルワールドを２つ紹介します。zipファイルになっているので解凍してプログラムをチェックするか、拡張子を「.mcpack」に変更して、ワールドを読み込んで遊んでみてください。  

|ワールド名  |最終更新日  |ダウンロードリンク  |
|---|---|---|
|Turn-Based RPG  |2019-04-17  |[[1]](https://aka.ms/minecraftscripting_turnbased)  |
|Mob Arena  |2019-04-17  |[[2]](https://aka.ms/minecraftscripting_mobarena)  |

### 現在の問題点
現在報告されている、Scripting APIの問題点です。

|問題点  |対処方法  |
|---|---|
|スクリプトがアーカイブファイルから正しく読み込まれない |ファイルを解凍してからワールドに適用します。拡張子が「.mcpack」のファイルを読み込んでください。 |
|カスタムUIがVR/MRモードで機能しない |現在、通常モードでプレイしている時のみ、カスタムUIをサポートしています。|
|カスタムUIがゲームを中断・再開したときにデータを保存しない |現在、これに対しての対処方法はありません。 |
|スクリプトを読み込んでいないワールドを出てから、スクリプトを読み込んでいるワールドに入ると、意図しないワールドが読み込まれることがある |新しいっワールドに入る前に、MineCraftを再起動してください。 |
|死にかけているエンティティに対して、「removeEntity関数」を呼び出すと、MineCraftがクラッシュすることがある |エンティティの体力が0になったフレームで同時に「removeEntity関数」を呼び出さないでください。呼び出すと、すぐに削除されます。ただし、その代わりに死にかけているエンティティを保存し、次のフレームで処理してください。 |

### 重大な変更点
Scripting APIの仕様変更とともに、互換性が切り捨てられる場合があります。スクリプトが意図している動作をしない場合、これを確認してみてください。

|カテゴリー  |変更点  |
|---|---|
|UI |engine.onはファセット名になりました。UIを利用するには、次のコードが必要です。engine.on("facet:updated:core.scripting", ...);  初期化が完了したら、 engine.trigger("facet:request", ["core.scripting"]); と続けます。|
|コンポーネント |getComponent関数を呼び出すと、返り値で返されるオブジェクトの 'data' パラメーターの中に、コンポーネントのパラメータが返されるようになりました。 |
|イベント |イベントデータオブジェクトは、'data'パラメータ内にイベントのパラメータを保持するようになりました。 |
|イベント |カスタムイベントは、使う前にイベントを登録しなければいけなくなりました。詳しくは、registerEventDataに関しての記述を見てください。 |
|イベント |カスタムイベントは名前空間を持つ必要があるようになりました。ただし、組み込み専用であるため、名前空間'minecraft'を使うことはできません。|
|イベント |イベントデータは標準化されました。createEventData関数を呼び出して、全てのフィールドとイベントのデフォルト値をあらかじめ入力したイベントデータオブジェクトを作成します。イベントを発生させるには、このイベントデータオブジェクトが必要になります。|

### 開発環境
あなたはScripting APIを開発したいんですか！？すごいです！([訳者注]特に、日本には開発者が数えるほどしかいません。)  
あなたが開発するための開発環境を示します。  
注意！現在、Scripting APIはWindows10がインストールされているパソコンのみでサポートされています。スクリプトをサポートしていないデバイスでスクリプトを読み込んだワールドを開こうとすると、エラーメッセージが表示され、ワールドに入ることができない旨が伝えられます。

|ソフトウェア |最低限環境  |おすすめ |
|---|---|---|
|MineCraft |Windows10デバイス上のMineCraft |Windows10デバイス上のMineCraft |
|コードエディタ |Visual Studio Codeなどのコードエディタ |「JavaScript diagnostics」「JavaScript and TypeScript language support」「Just-In-Time debugger」がインストールされた Visual Studio Community 2017|
|デバッガ |なし |Visual Studio Community 2017 |
|その他 |[[1]](https://aka.ms/MinecraftBetaBehaviors) から入手できるビヘイビアパック |[[1]](https://aka.ms/MinecraftBetaBehaviors) から入手できるビヘイビアパック |
|ストレージ |1.0GBの空き容量 |3.0GBの空き容量 |