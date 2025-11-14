#  Microsoft 365 Agents Toolkitを使用して、指示ベースのジオロケーター ゲーム エージェントを構築する

**所要時間: 30分**

## 客観的

このラボの目的は、参加者がMicrosoft 365 Agents Toolkitを用いてMicrosoft
365
Copilot用の宣言型エージェントを構築できるようにすることです。ラボを完了することで、参加者は仕事の合間に楽しく学べる位置情報ゲームを作成できるようになります。ラボでは、宣言型エージェントの構造を理解し、指示に従って設定し、Microsoft
365エコシステムに統合してCopilotのインタラクションをカスタマイズすることに重点を置きます。

## 解決

参加者はVisual Studio CodeにMicrosoft 365 Agents
Toolkitをインストールし、開発環境をセットアップします。テンプレートを使用して、「Geo
Locator
Game」という宣言型エージェントのスキャフォールディングを行います。エージェントの指示をカスタマイズし、instruction.txtやmanifest.jsonなどの構成ファイルを更新します。また、このラボでは、参加者がエージェントに固有の識別子、カスタムアイコン、テスト機能を追加する方法についても指導します。その結果、Microsoft
365とシームレスに統合しながら、都市に関するヒントを提供するようにカスタマイズされた、完全に機能する魅力的なCopilotアプリケーションが完成します。

## 演習 1: Microsoft 365 Copilot の開発環境をセットアップする

### タスク 1: Microsoft 365 Agents Toolkitをインストールする

1.  Visual Studio Code を開き、**Extensions**ツールバー
    ボタンをクリックします。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image1.png)

2.  +++ **Microsoft 365 agents**+++ を検索し、 **Microsoft 365 Agents
    Toolkitを見つけます**。

	![image](./media/image2.png)

3.  **Installを**選択します。

	![image](./media/image3.png)

4.  インストールが完了すると、 **Microsoft 365 Agents
    Toolkitの**アイコンが左側のナビゲーション バーに表示されます。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

[!Note]**注:** Microsoft 365 Agents Toolkit は Teams Toolkit
の進化版です。現在移行段階にあり、一部では Teams
ツールキットとして、一部では Microsoft 365 Agents Toolkit
として表示されます。

## 練習問題2: 最初の宣言的行為主体

このラボでは、Visual Studio Code 用の Microsoft 365 Agents Toolkit
を使用して、シンプルな宣言型エージェントを構築します。このエージェントは、世界中の都市を探索することで、仕事の合間に楽しく学びのひとときを過ごせるよう設計されています。抽象的なヒントを提示して都市を推測しますが、ヒントを多く使うほど得点が低くなります。最後に、最終スコアが発表されます。

この演習では以下のことを学習します。

- Microsoft 365 Copilot の宣言型エージェントとは

- Microsoft 365 Agents Toolkit
  テンプレートを使用して宣言型エージェントを作成する

- 指示に従ってエージェントをカスタマイズし、ジオロケーターゲームを作成します

- アプリの実行とテストの方法を学ぶ

- ボーナス演習では、SharePointチームサイトが必要になります

**導入**

宣言型エージェントは、Microsoft 365 Copilot
と同じスケーラブルなインフラストラクチャとプラットフォームを活用し、お客様のニーズの特定の領域に特化して対応します。特定の分野やビジネスニーズにおける専門家として機能し、標準的な
Microsoft 365 Copilot
チャットと同じインターフェイスを使用しながら、エージェントが特定のタスクに集中できるようにします。

宣言型エージェントの構築へようこそ！さあ、Copilot
を魔法のように動かしてみましょう！

このラボでは、Microsoft 365 Agents Toolkit
のデフォルトテンプレートを使用して、宣言型エージェントの構築から始めます。これは、何かを始める際の手助けとなります。次に、エージェントを地理位置情報ゲームに特化したものに修正します。

AIの目的は、世界中の様々な都市について学びながら、仕事の合間に楽しいひとときを過ごすことです。AIは抽象的な手がかりを提示し、都市を特定します。手がかりが多ければ多いほど、獲得できるポイントは少なくなります。ゲーム終了時に、最終スコアが表示されます。

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image5.png)

また、エージェントに秘密の日記🕵🏽や地図🗺️を参照するためのファイルをいくつか提供し、プレイヤーにさらなる課題を与えます。

それでは始めましょう

**宣言的エージェントの解剖**

していくと、最終的に構築するのはいくつかのファイルを zip
ファイルにまとめたコレクションになります。これをアプリ
パッケージと呼びます。アプリ
パッケージをインストールして使用します。そのため、アプリ
パッケージの構成について基本的な理解が重要です。宣言型エージェントのアプリ
パッケージは、以前に Teams アプリを追加したことがある方なら、そのアプリ
パッケージに似ています。すべてのコア要素については、表をご覧ください。また、アプリの展開プロセスも
Teams アプリの展開と非常によく似ていることがわかります。

|	要素|説明	|	|
|:------|:-----|:----------|
|アプリマニフェスト	|アプリの構成、機能、必要なリソース、重要な属性について説明します。	|	manifest.json|
|アプリアイコン	|宣言エージェントには、カラー(192x192) とアウトライン (32x32) のアイコンが必要です。	|icon.png, color.png	|
|宣言型エージェントマニフェスト	|エージェントの構成、手順、必須フィールド、機能、会話の開始、およびアクションについて説明します。	|	declarativeAgent.json|

**注:** SharePoint、OneDrive、Web
検索などから参照データを追加したり、プラグインやコネクタなどの拡張機能を宣言型エージェントに追加したりできます。プラグインの追加方法については、このパスの今後のラボで学習します。

**宣言型エージェントの機能**

指示を追加するだけでなく、アクセスすべき知識ベースを指定することで、エージェントのコンテキストとデータへの集中度を高めることができます。これらは「機能」と呼ばれ、3種類の機能がサポートされています。

- **Microsoft Graph コネクタ**- Graph
  コネクタの接続をエージェントに渡し、エージェントがコネクタの知識にアクセスして利用できるようにします。

- **OneDrive および SharePoint** -
  エージェントがコンテンツにアクセスできるように、ファイルとサイトの URL
  をエージェントに提供します。

- **Web サーチ**- エージェントのナレッジ ベースの一部として Web
  コンテンツを有効または無効にします。

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image6.png)

**One DriveとSharePoint**

URLはSharePointアイテム（サイト、ドキュメントライブラリ、フォルダー、またはファイル）へのフルパスで指定する必要があります。SharePointの「直接リンクをコピー」オプションを使用すると、ファイルやフォルダーのフルパスを取得できます。これを行うには、ファイルまたはフォルダーを右クリックし、「詳細」を選択します。「パス」に移動し、コピーアイコンをクリックします。URLを指定しない場合、エージェントはログインユーザーが利用できるOneDriveおよびSharePointコンテンツの全コーパスを使用します。

**Microsoft Graph コネクタ**

接続を指定しないと、ログインしたユーザーが利用できるグラフ コネクタ
コンテンツのコーパス全体がエージェントによって使用されます。

**Webサーチ**

現時点では、特定の Web サイトまたはドメインを渡すことはできず、これは
Web の使用のオン/オフを切り替えるものとしてのみ機能します。

## 演習3: テンプレートから宣言型エージェントを構築する

前述のアプリパッケージ内のファイル構造を理解していれば、任意のエディタを使用して宣言型エージェントを作成できます。しかし、Microsoft
365 Agents
Toolkitのようなツールを使用すると、これらのファイルの作成だけでなく、アプリの展開と公開もサポートされるため、作業がより簡単になります。そのため、作業を可能な限りシンプルにするために、Microsoft
365 Agents Toolkitを使用します。

### タスク 1: Microsoft 365 Agents Toolkitを使用して宣言型エージェント アプリを作成する

1.  Visual Studio コード エディターで Microsoft 365 Agents
    Toolkit拡張機能に移動し、\[**Create a new app\]** を選択します。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image7.png)

2.  プロジェクト
    タイプのリストから**Agentを**選択する必要があるパネルが開きます。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image8.png)

3.  次に、Copilot Agent
    のアプリ機能を選択するよう求められます。**Declarative
    agent**を選択してください。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

4.  基本的な宣言型エージェントを作成するか、APIプラグイン付きのエージェントを作成するかを選択するよう求められます。「**No
    Plugin**」オプションを選択して**ください**。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

5.  次に、プロジェクト フォルダーを作成する場所を指定するための
    \[Default folder\] オプションを**選択します**。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image11.png)

6.  次に、アプリケーション名に「**+++Geo Locator
    Game+++**」と入力し、\[Enter\] を選択します。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image12.png)

	数秒以内に指定したフォルダにプロジェクトが作成され、Visual Studio Code
の新しいプロジェクトウィンドウで開きます。これが作業フォルダです。

7.  ソースの信頼性に関するプロンプトが表示された場合は、 **「Yes, I
    trust the authors」**をクリックします。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image13.png)

	![A screenshot of a computer AI-generated content may be incorrect.](./media/image14.png)

よくできました！ベースとなる宣言型エージェントの設定に成功しました！次は、その中のファイルを調べてカスタマイズし、ジオロケーターゲームアプリを作成しましょう。

### タスク 2: Microsoft 365 Agents Toolkitでアカウントを設定する

1.  次に、左側の \[**Accounts\]にある Microsoft 365 Agents Toolkit
    アイコンを選択し、 \[Sign in to Microsoft 365\]**をクリックして、
    **\[Resources\]タブの\[Azure
    Portal\]**セクションでUser1**の資格情報**を使用してログインします。

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image15.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image16.png)

2.  ブラウザ ウィンドウがポップアップ表示され、Microsoft 365
    へのログインが求められます。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image17.png)

3.  「Security Alert」ダイアログで**「Allow access」**を選択します。

	![A screenshot of a computer security alert AI-generated content may be
incorrect.](./media/image18.png)

4.  ブラウザウィンドウに「You are signed in now and close this
    page」と表示されたら、サインインしてください。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image19.png)

5.  **Custom App Upload
    Enabled** チェッカーに緑色のチェックマークが付いていることを確認します。

	![image](./media/image20.png)

### タスク3: アプリ内のファイルを理解する

基本プロジェクトの外観は次のとおりです。

|フォルダ/ファイル	|コンテンツ	|
|:----|:----|
|	. vscode|VSCodeファイル	|
|appPackage	|Teams アプリケーション マニフェスト、GPT マニフェスト、API 仕様のテンプレート	|
|env	|デフォルトの.env.devファイルを持つ環境ファイル	|
|appPackage/color.png	|アプリケーションロゴ画像	|
|appPackage/outline.png	|	アプリケーションロゴのアウトライン画像|
|	appPackage/declarativeAgent.json|宣言型エージェントの設定と構成を定義します。	|
|	appPackage/instruction.txt|動作を定義します。	|
|appPackage/manifest.json	|宣言型エージェントのメタデータを定義するTeamsアプリケーション マニフェスト。	|
|teamsapp.yml	|Microsoft 365 Agents Toolkit のメインプロジェクトファイル。このプロジェクトファイルでは、プロパティと構成ステージ定義という2つの主要な要素を定義します。	|

1.  このラボで特に注目すべきファイルは、エージェントに必要なコアディレクティブが記述された**appPackage/instruction.txt**ファイルです。これはプレーンテキストファイルで、自然言語による指示を記述できます。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image21.png)

2.  もう一つの重要なファイルは**appPackage/declarativeAgent.json**です。このファイルには、Microsoft
    365 Copilot
    を新しい宣言型エージェントで拡張するためのスキーマが含まれています。このファイルのスキーマがどのようなプロパティを持っているか見てみましょう。

    - $schemaはスキーマ参照です

    - バージョンはスキーマバージョンです

    - 名前キーは宣言エージェントの名前を表します。

    - 説明には説明が提供されます。

    - 操作動作を決定する指示を含む**instructions.txt**ファイルへのパスです。指示をプレーンテキストで値として入力することもできますが、このラボでは**instructions.txt**ファイルを使用します。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image22.png)

3.  もう一つの重要なファイルは**appPackage/manifest.json**ファイルです。このファイルには、パッケージ名、開発者名、アプリケーションで使用されるコパイロットエージェントへの参照など、重要なメタデータが含まれています。manifest.json
    ファイルの次のセクションは、これらの詳細を示しています。

	```
	"copilotAgents": {
			"declarativeAgents": [            
				{
					"id": "declarativeAgent",
					"file": "declarativeAgent.json"
				}
			]
		},

	```

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image23.png)

4.  アプリケーションのブランドに合わせて、ロゴファイル（color.pngとoutline.png）を更新することもできます。本日のラボでは、エージェントのアイコンを目立たせるために、
    **color.png**アイコンを変更します**。**

## 演習4: 指示とアイコンを更新する

### タスク1: アイコンとマニフェストを更新する

1.  まず、ロゴを置き換えます。プロジェクト内の画像**color.png
    を新しい画像に置き換えます。C
    :\LabFiles**にある画像**color.pngをコピーし、ルートプロジェクトのappPackage**フォルダ（パスは**C:\Users\Student\TeamsApps\Geo
    Locator Game\appPackage）**にある同名の画像を置き換えます。

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image24.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image25.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image26.png)

2.  **appPackage/manifest.json**ファイルに移動し、
    **copilotAgents**ノードを見つけます。
    declarativeAgents配列の最初のエントリの id
    値をdeclarativeAgentから+++ dcGeolocator +++
    に更新して、このIDを一意にします。

	```
	"copilotAgents": {
			"declarativeAgents": [            
				{
					"id": "dcGeolocator",
					"file": "declarativeAgent.json"
				}
			]
		},

	```

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image27.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image28.png)

3.  次に、ファイル**appPackage /instruction
    txt**に移動し、以下の命令をコピーして貼り付け、ファイルの既存の内容を上書きします。

	```
	System Role: You are the game host for a geo-location guessing game. Your goal is to provide the player with clues about a specific city and guide them through the game until they guess the correct answer. You will progressively offer more detailed clues if the player guesses incorrectly. You will also reference PDF files in special rounds to create a clever and immersive game experience.

	Game play Instructions:

	Game Introduction Prompt

	Use the following prompt to welcome the player and explain the rules:

	Welcome to the Geo Location Game! I’ll give you clues about a city, and your task is to guess the name of the city. After each wrong guess, I’ll give you a more detailed clue. The fewer clues you use, the more points you score! Let’s get started. Here’s your first clue:

	Clue Progression Prompts

	Start with vague clues and become progressively specific if the player guesses incorrectly. Use the following structure:

	Clue 1: Provide a general geographical clue about the city (e.g., continent, climate, latitude/longitude).

	Clue 2: Offer a hint about the city’s landmarks or natural features (e.g., a famous monument, a river).

	Clue 3: Give a historical or cultural clue about the city (e.g., famous events, cultural significance).

	Clue 4: Offer a specific clue related to the city’s cuisine, local people, or industry.

	Response Handling

	After the player’s guess, respond accordingly:
	If the player guesses correctly, say:

	That’s correct! You’ve guessed the city in [number of clues] clues and earned [score] points. Would you like to play another round?

	If the guess is wrong, say:

	Nice try! [followed by more clues]

	PDF-Based Scenario

	For special rounds, use a PDF file to provide clues from a historical document, traveler's diary, or ancient map:

	This round is different! I’ve got a secret document to help us. I’ll read clues from this [historical map/traveler’s diary] and guide you to guess the city. Here’s the first clue:

	Reference the specific PDF to extract details:
	Traveler's Diary PDF,Historical Map PDF.
	Use emojis where necessary to have friendly tone. 
	Scorekeeping System

	Track how many clues the player uses and calculate points:

	1 clue: 10 points

	2 clues: 8 points

	3 clues: 5 points

	4 clues: 3 points

	End of Game Prompt

	After the player guesses the city or exhausts all clues, prompt:

	Would you like to play another round, try a special challenge?

	```

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image29.png)

4.  **appPackage/declarativeAgent.json**の次の行に注目してください:

	"instructions": "$\[file('instruction.txt')\]",

	**instruction.txt**ファイルから指示が読み込まれます。パッケージファイルをモジュール化したい場合は、**appPackage**フォルダ内の任意の
JSON ファイルでこの手法を使用できます。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

### タスク2: 会話のきっかけを追加する

会話のきっかけを追加することで、宣言型エージェントに対するユーザー
エンゲージメントを強化できます。

会話のきっかけを持つことの利点は次のとおりです。

- **エンゲージメント**:
  インタラクションを開始し、ユーザーの安心感を高め、参加を促します。

- **コンテキスト設定**:
  スターターは会話のトーンとトピックを設定し、ユーザーにどのように進めるかをガイドします。

- **効率性**:
  明確な焦点を先導することで、スターターは曖昧さを減らし、会話をスムーズに進めることができます。

- **ユーザー維持**:
  適切に設計されたスターターはユーザーの興味を維持し、AI
  との繰り返しのやり取りを促します。

1.  ファイル**declarativeAgent.jsonを**開き**、**instructionsノードの直後にコンマを追加してEnter
    キーを押し、以下のコードを貼り付けます。

	```
	"conversation_starters": [
		{ 
				"title": "Getting Started",
				"text":"I am ready to play the Geo Location Game! Give me a city to guess, and start with the first clue." 
			},
			{
				"title": "Ready for a Challenge",
				"text": "Let us try something different. Can we play a round using the travelers diary?"
			},
			{ 
				"title": "Feeling More Adventurous",
				"text": "I am in the mood for a challenge! Can we play the game using the historical map? I want to see if I can figure out the city from those ancient clues."
			}
		]

	```

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image31.png)

これでエージェントへの変更がすべて完了したので、テストする準備が整いました。

2.  上部のバーから**「Files」**に移動し、「**Save
    All」**をクリックします。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image32.png)

### タスク3: アプリをテストする

1.  アプリをテストするには、Visual Studio Code で Microsoft 365 Agents
    Toolkit
    拡張機能にアクセスしてください。すると左側のペインが開きます。
    **「LIFECYCLE」で「Provision」**を選択してください。Microsoft 365
    Agents Toolkit
    の真価は、ここでお分かりいただけるでしょう。公開が非常に簡単になります。

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image33.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image34.png)

2.  プロンプトが表示されたら、資格情報を使用してサインインします。

	![A screen shot of a computer AI-generated content may be
incorrect.](./media/image35.png)

3.  appPackageフォルダー内のすべてのファイルがzip
    ファイルとしてパッケージ化され、宣言型エージェントが独自のアプリカタログにインストールされます。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image36.png)

4.  4\. ブラウザを開き、開発者テナントにログインした状態で
    +++*https://m365.cloud.microsoft/chat/*+++
    にアクセスします。左側のペインから「Geo Locator Game」を開きます。

	![image](./media/image37.png)

5.  起動すると、エージェントとのチャットウィンドウが開きます。会話のきっかけとなる項目が以下のように表示されます。

	![image](./media/image38.png)

6.  会話のきっかけとなるもののいずれかを選択すると、メッセージ作成ボックスにきっかけとなるプロンプトが表示され、「Enter」キーを押すのを待ちます。これはあくまでもあなたのアシスタントであり、あなたがアクションを起こすまで待機します。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

7.  質問に答えて、開発したゲームを探索してみましょう。

## まとめ：

このラボでは、Microsoft 365 Agents
Toolkitを使用して宣言型エージェントを構築し、エージェントの機能をテストする方法を学習しました。
