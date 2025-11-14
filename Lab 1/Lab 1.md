# ラボ 1 - Microsoft 365 Agents Toolkitを使用して、TypeSpec 定義を含む RepairService 宣言型エージェントを構築する

**客観的**

このラボでは、Microsoft 365 Agents Toolkit を使用して、TypeSpec
定義を備えた宣言型エージェントを構築します。既存の API
サービスを介して修理データとやり取りし、ユーザーが自動車修理記録を管理できるようにする「RepairServiceAgent」というエージェントを作成します。

**宣言的エージェント**

**宣言型エージェントは**、Microsoft 365
のエージェントの一種です。Microsoft 365 Copilot
を拡張することで構築できます。カスタムナレッジとカスタムアクションを定義することで、特定のシナリオに合わせたエージェントを作成できます。

宣言型エージェントは、Microsoft 365 Copilot
と同じインフラストラクチャ、オーケストレーター、基盤モデル、セキュリティ
コントロールを使用するため、一貫性のある使い慣れたユーザー
エクスペリエンスが保証されます。

![Declarative agent architecture diagram. At the very basis there is the
foundational model of Microsoft 365 Copilot, as well as the same
orchestrator. The agent provides also custom knowledge and grounding
data, and custom skills as actions, triggers, and workflows.. The user
experience is available in Microsoft 365 Copilot.](./media/image1.png)

**宣言型エージェントにおけるTypeSpecの重要性**

**TypeSpecとは**

TypeSpecは、APIコントラクトを構造化かつ型安全に設計・記述するためにMicrosoftが開発した言語です。APIがどのように見えるか、どのようなデータを受け取り、返すか、そしてAPIの様々な部分とそのアクションがどのように連携するかなど、APIがどのように動作するべきかを示す青写真のようなものだと考えてください。

**エージェントに TypeSpec を使用する理由**

TypeScript
がフロントエンド/バックエンドコードに構造を強制する方法に魅力を感じるなら、TypeSpec
がエージェントやアクションなどの API
サービスに構造を強制する方法にもきっと満足するでしょう。Visual Studio
Code
などのツールと連携する、デザインファーストの開発ワークフローに最適です。

明確なコミュニケーション -
エージェントの動作方法を定義する単一の真実のソースを提供し、宣言型エージェントの場合のように複数のマニフェスト
ファイルを処理する際の混乱を回避します。

一貫性 -
エージェントのすべての部分とそのアクション、機能などが一貫して同じパターンに従って設計されていることを確認します。

自動化に最適 - OpenAPI
仕様やその他のマニフェストを自動的に生成し、時間を節約して人的エラーを削減します。

早期検証 -
実際のコードを書く前に、不一致なデータ型や不明瞭な定義などの設計上の問題を早期に検出します。

設計優先アプローチ - 実装に進む前にエージェントと API
の構造と契約について考えることを推奨し、長期的な保守性を向上させます。

## 演習1: ラボ環境の設定

この演習では、Microsoft 365 Copilot を使用してカスタマイズされた AI
アシスタンスを実現するために役立つ Copilot
エージェントを構築、テスト、展開するための開発環境をセットアップします。

### タスク 1: Agents Toolkitをインストールする

**Visual Studio Code 用エージェントツールキットを**使用するには、Visual
Studio Code が必要です。この演習では、Visual Studio Code
にツールキットをインストールします。

1.  VMから**Visual Studio
    Code**を開きます。左側のメニューから**「Extensions」を選択します。**

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image2.png)

2.  +++Microsoft 365 Agents Toolkit+++ を検索して選択し、
    **\[Install\]をクリックします**。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image3.png)

3.  ツールキットがインストールされていることを確認してください。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

4.  デスクトップに +++ServiceAgent+++
    という名前の新しいフォルダーを作成します。

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image5.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image6.png)

## 演習 2: Microsoft 365 Agents Toolkit を使用して TypeSpec でベースエージェントを構築する

この演習では、**宣言型エージェントを**構築し、定義し、アクションを更新し、エージェントをテストします。

### タスク 1: Microsoft 365 Agents Toolkitを使用してベース エージェント プロジェクトをスキャフォールディングする

このタスクでは、 **Microsoft 365 Agents Toolkit を使用して、
TypeSpec**定義を備えた**宣言型エージェントを構築します。**既存の API
サービスを介して修理データとやり取りし、ユーザーが自動車修理記録を管理できるようにする、
**RepairServiceAgent**というエージェントを作成します。

1.  **Microsoft 365 Agents
    Toolkitのアイコン**を見つけます ![m365atk-icon](./media/image7.png)左側のVS
    Codeメニューから「新しいエージェント/アプリを作成」を選択します。アクティビティバーが開きます。アクティビティバーの**「Create
    a New Agent/App」**ボタンを選択すると、Microsoft 365 Agents
    Toolkitで利用可能なアプリテンプレートの一覧を含むパレットが開きます。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image8.png)

2.  テンプレートのリストから**Declarative Agentを**選択します。

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image9.png)

3.  次に、「**Start with TypeSpec for Microsoft 365
    Copilot**」を選択して、TypeSpec を使用してエージェントを定義します。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

4.  **ServiceAgent**フォルダを選択します。これは、エージェントツールキットがエージェントプロジェクトのスキャフォールディングを行う場所です。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image11.png)

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image12.png)

5.  次に、アプリケーション名を「+++RepairServiceAgent+++」と入力し、
    **Enter**キーを押してプロセスを完了します。エージェントプロジェクトがプリロードされた新しいVS
    Codeウィンドウが表示されます。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image13.png)

6.  **Microsoft 365 Agents
    Toolkit**にサインインする必要があります そこからエージェントをアップロードしてテストします。

7.  プロジェクトウィンドウ内で、 **Microsoft 365 Agents
    Toolkit**アイコンを選択します。 ![m365atk-icon](./media/image7.png)左側のメニューからもう一度クリックします。これにより、アカウント、環境、開発などのセクションを含むエージェントツールキットのアクティビティバーが開きます。

8.  **\[Accounts\]**セクションで、 **\[Sign in to Microsoft
    365\]**を選択します。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image14.png)

9.  エディターからサインイン、Microsoft 365
    開発者サンドボックスの作成、またはキャンセルを行うためのダイアログが開きます。
    **「Sign in」**を選択し、資格情報でログインしてください。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image15.png)

10. サインインしたら、ブラウザを**閉じて**プロジェクト
    ウィンドウに戻ります。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image16.png)

### タスク2: エージェントを定義する

Agents Toolkit によってスキャフォールディングされた Declarative Agent
プロジェクトには、エージェントを GitHub API
に接続してリポジトリの問題を表示するためのコードを含むテンプレートが用意されています。このラボでは、自動車修理サービスと統合し、修理データを管理するための複数の操作をサポートする独自のエージェントを構築します。

プロジェクトフォルダには、 **main.tsp**と**actions.tsp
という2つのTypeSpec**ファイルがあります。エージェントは、
**main.tspファイル**で**メタデータ**、**指示**、および**機能を使用して定義されます**。actions.tsp
ファイルを使用して、**エージェントのアクション**を定義します。エージェント**に**APIサービスへの接続などのアクションが含まれる場合は、このファイルに定義する必要があります。

**main.tsp**を開き、デフォルトのテンプレートの内容を調べます。このテンプレートは、エージェントの修理サービス
シナリオに合わせて変更します。

**エージェントのメタデータと手順を更新する**

**main.tspファイル**には、エージェントの基本構造が記載されています。エージェントツールキットテンプレートに含まれる以下の内容を確認してください。

- エージェント**名**と**説明**1️⃣

- 基本的な**手順**2️⃣

- **アクション**と**機能**のプレースホルダコード（コメントアウト） 3️⃣

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image17.png)

1.  **@agentブロック**と**@instructions**ブロック (10 行目から 17
    行目)を特定します。

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image18.png)

2.  まず、修復シナリオ用のエージェントを定義します。
    **@agent**と**@instruction
    の**定義を以下のコードスニペットに置き換えます。

	```
	@agent(
	"RepairServiceAgent",
	"An agent for managing repair information"
	)

	@instructions("""
	## Purpose
	You will assist the user in finding car repair records based on the information provided by the user. 
	""")

	```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image19.png)

3.  次に、エージェントの会話開始機能を追加します。説明のすぐ下に、会話開始機能のコメントアウトされたコードがあります。@conversationStarter
    ブロック（22行目から25行目）を以下のコードに置き換えてください。

	```
	@conversationStarter(#{
	title: "List repairs",
	text: "List all repairs"
	})	

	```

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image20.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image21.png)

### タスク3: エージェントのアクションを更新する

**actions.tspファイルを**開いてエージェントのアクションを定義します。後で
main.tsp
ファイルに戻り、アクション参照を使用してエージェントのメタデータを完成させますが、まずはアクション自体を定義する必要があります。

actions.tsp 内のプレースホルダコードは、GitHub
リポジトリ内の未解決の問題を検索するために設計されています。これは、エージェントのアクションを定義する方法（アクションのメタデータ、API
ホスト
URL、操作または関数とその定義など）を初心者が理解するための出発点となります。これらはすべて、repair
service に置き換えます。

1.  ファイル**actions.tsp**を開きます。 **@serviceからconst
    SERVER_URL**まで（行番号は7～25）のコードを以下のコードブロックに置き換えます。

このアップデートでは、アクションメタデータが導入され、サーバーURLが設定されます。また、名前空間がGitHubAPIからRepairsAPIに変更されたことにもご注意ください。

	```
	@service
	@server(RepairsAPI.SERVER_URL)
	@actions(RepairsAPI.ACTIONS_METADATA)
	namespace RepairsAPI{
	/**
	* Metadata for the API actions.
	*/
	const ACTIONS_METADATA = #{
		nameForHuman: "Repair Service Agent",
		descriptionForHuman: "Manage your repairs and maintenance tasks.",
		descriptionForModel: "Plugin to add, update, remove, and view repair objects.",
		legalInfoUrl: "https://docs.github.com/en/site-policy/github-terms/github-terms-of-service",
		privacyPolicyUrl: "https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement"
	};

	/**
	* The base URL for the  API.
	*/
	const SERVER_URL = "https://repairshub.azurewebsites.net";

	```

2.  次に、テンプレートコード内の操作を searchIssues
    から**listRepairs**に置き換えます。これは、修復リストを取得する修復操作です。SERVER_URL定義の直後から最後の閉じ括弧*の前まで*のコードブロック全体を、以下のスニペットに置き換えます。閉じ括弧はそのままにしておいてください。（行番号は27～37です）

	```
	/**
	* List repairs from the API 
	* @param assignedTo The user assigned to a repair item.
	*/

	@route("/repairs")
	@get  op listRepairs(@query assignedTo?: string): string;

	```

	![A screenshot of a computer program AI-generated content may be incorrect.](./media/image22.png)

3.  **main.tspファイル**に戻り、先ほど定義したアクションをエージェントに追加します。会話開始部分の後のコードブロック全体を以下のスニペットに置き換えます。

	```
	namespace RepairServiceAgent{  
	// Uncomment this part to add actions to the agent.
	@service
	@server(global.RepairsAPI.SERVER_URL)
	@actions(global.RepairsAPI.ACTIONS_METADATA)
	namespace RepairServiceActions {
		op listRepairs is global.RepairsAPI.listRepairs;   
	}
	}

	```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image23.png)

### タスク4: (読み取り専用) デコレータを理解する

これは、TypeSpecファイルで定義されている内容を理解するためのタスクです。このタスクをざっと読んでみてください。TypeSpecファイル（main.tspとactions.tsp）には、エージェントのデコレータ（@で始まる）、名前空間、モデル、その他の定義が含まれています。

これらのファイルで使用されているデコレータの一部を理解するには、以下の詳細を確認してください。

- **@agent** - エージェントの名前空間（名前）と説明を定義します

- **@instructions** -
  エージェントの動作を規定する指示を定義します。8000文字以下

- **@conversationStarter** - エージェントの会話のきっかけを定義します

- op -任意の操作を定義します。op GraphicArt、op
  CodeInterpreterなどのエージェントの機能を定義する操作、またはop
  listRepairsなどのAPI操作を定義する操作のいずれかになります。

- **@server** - APIのサーバーエンドポイントとその名前を定義します

- **@capabilities**
  -関数内で使用する場合、操作の確認カードのような小さな定義を持つシンプルなアダプティブカードを定義します。

### タスク5: エージェントをテストする

このタスクでは、作成した修復サービス エージェントをテストします。

1.  プロジェクト内からアクティビティ バーを開くには、 **Agents Toolkit
    拡張機能のアイコン**を選択します。

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image24.png)

2.  エージェントツールキットのアクティビティバーで、
    **「LifeCycle」の「Provision」**を選択します。これにより、生成されたマニフェストファイルとアイコンを含むアプリパッケージがビルドされ、テスト用にアプリがカタログにサイドロードされます。

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image25.png)

3.  Web ブラウザーを開き、+++
    [https://m365.cloud.microsoft/chat+++に移動して](https://m365.cloud.microsoft/chat+++)Copilot
    アプリを開きます。

4.  **エージェント**のリストから、
    **RepairServiceAgent**を選択します。これには少し時間がかかりますが、プロビジョニングタスクの進行状況を示すトースターメッセージが表示されます。

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image26.png)

5.  会話のきっかけとなる**「List
    repairs」**を選択し、プロンプトを送信します。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

6.  エージェントとの会話が開始され、修理リストとともにエージェントからの応答を確認できます。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

## 演習3: エージェントの機能強化

この演習では、操作の追加、アダプティブカードによるレスポンスの有効化、コードインタープリター機能の組み込みなど、エージェントの機能強化を行います。これらの機能強化を一つずつ見ていきましょう。VS
Codeのプロジェクトに戻ってください。

### タスク1: エージェントを変更して操作を追加する

このタスクでは、エージェントを変更し、 **createRepair** 、
**updateRepair** 、 **deleteRepair などの操作を追加します。**

1.  **actions.tsp**に移動し、以下のスニペットを**listRepairs操作の**直後にコピー＆ペーストして、新しい操作**createRepair**
    、 **updateRepair** 、 **deleteRepairを追加します**。ここで、Repair
    アイテムのデータモデルも定義します。

	```
	/**
	* Create a new repair. 
	* When creating a repair, the `id` field is optional and will be generated by the server.
	* The `date` field should be in ISO 8601 format (e.g., "2023-10-01T12:00:00Z").
	* The `image` field should be a valid URL pointing to the image associated with the repair.
	* @param repair The repair to create.
	*/
	@route("/repairs")  
	@post  op createRepair(@body repair: Repair): Repair;

	/**
	* Update an existing repair.
	* The `id` field is required to identify the repair to update.
	* The `date` field should be in ISO 8601 format (e.g., "2023-10-01T12:00:00Z").
	* The `image` field should be a valid URL pointing to the image associated with the repair.
	* @param repair The repair to update.
	*/
	@route("/repairs")  
	@patch  op updateRepair(@body repair: Repair): Repair;

	/**
	* Delete a repair.
	* The `id` field is required to identify the repair to delete.
	* @param repair The repair to delete.
	*/
	@route("/repairs") 
	@delete  op deleteRepair(@body repair: Repair): Repair;

	/**
	* A model representing a repair.
	*/
	model Repair {
		/**
		* The unique identifier for the repair.
		*/
		id?: string;

		/**
		* The short summary or title of the repair.
		*/
		title: string;

		/**
		* The detailed description of the repair.
		*/
		description?: string;

		/**
		* The user who is assigned to the repair.
		*/
		assignedTo?: string;

		/**
		* The optional date and time when the repair is scheduled or completed.
		*/
		@format("date-time")
		date?: string;

		/**
		* The URL of the image associated with the repair.
		*/
		@format("uri")
		image?: string;
	}

	```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image29.png)

2.  次に、
    **main.tsp**ファイルを開き、これらの新しい操作をエージェントのアクションに追加します。以下のスニペットを、
    **RepairServiceActions名前**空間内の**op listRepairs is
    global.RepairsAPI.listRepairs**;の行の後に貼り付けます。

	```
	op createRepair is global.RepairsAPI.createRepair;
	op updateRepair is global.RepairsAPI.updateRepair;
	op deleteRepair is global.RepairsAPI.deleteRepair;

	```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image30.png)

3.  また、最初の会話開始定義の直後に、新しい修復項目を作成するための新しい会話スターターを追加します。

	```
	@conversationStarter(#{
	title: "Create repair",
	text: "Create a new repair titled \"[TO_REPLACE]\" and assign it to me"
	})

	```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image31.png)

### タスク 2: 関数参照にアダプティブ カードを追加する

このタスクでは、アダプティブカードを使用して参照カードまたはレスポンスカードを拡張します。**listRepairs**
操作を使用して、修復項目にアダプティブカードを追加してみましょ**う**。

1.  プロジェクト フォルダーで、 **appPackage**フォルダーの下に
    +++cards+++ という新しいフォルダーを作成します。

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image32.png)

2.  **cards**フォルダに +++repair.json+++ ファイルを作成し、以下のコード
    スニペットをそのままファイルに貼り付けます。

	```
	{
		"$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
		"type": "AdaptiveCard",
		"version": "1.5",
		"body": [
	{
		"type": "Container",
		"$data": "${$root}",
		"items": [
		{
			"type": "TextBlock",
			"text": "Title: ${if(title, title, 'N/A')}",
			"weight": "Bolder",
			"wrap": true
		},
		{
			"type": "TextBlock",
			"text": "Description: ${if(description, description, 'N/A')}",
			"wrap": true
		},
		{
			"type": "TextBlock",
			"text": "Assigned To: ${if(assignedTo, assignedTo, 'N/A')}",
			"wrap": true
		},
		{
			"type": "TextBlock",
			"text": "Date: ${if(date, date, 'N/A')}",
			"wrap": true
		},
		{
			"type": "Image",
			"url": "${image}",
			"$when": "${image != null}"
		}
		]
	}
	],  
		"actions": [
		{
			"type": "Action.OpenUrl",
			"title": "View Image",
			"url": "https://www.howmuchisit.org/wp-content/uploads/2011/01/oil-change.jpg"
		}
		]
	}

	```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image33.png)

3.  **actions.tsp**ファイルに戻り、
    **listRepairs**オペレーションを見つけます。オペレーション定義の**@get
    op listRepairs(@query assignmentTo?: string):
    string;**行を以下の2行のコードに置き換えます。

	```
	@card(#{ dataPath: "$", title: "$.title",   url: "$.image", file: "cards/repair.json"})
	@get op listRepairs(@query assignedTo?: string): Repair[];

	```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image34.png)

4.  上記のカード応答は、修理項目についてお問い合わせいただいた場合、またはエージェントが参考として項目のリストを持参した場合にエージェントから送信されます。

5.  エージェントが追加機能をサポートするようになったため、この機能強化を反映するように手順を更新してください。

6.  同じ**main.tsp**ファイルで、エージェント用の追加の指示を追加するように
    instruction
    定義を更新します。既存の**@instructions**コードブロックを以下のコードブロックに置き換えます。

	```
	@instructions("""
	## Purpose
	You will assist the user in finding car repair records based on the information provided by the user. When asked to display a report, you will use the code interpreter to generate a report based on the data you have.

	## Guidelines
	- You are a repair service agent.
	- You can use the actions to create, update, and delete repairs.
	- When creating a repair item, if the user did not provide a description or date , use title as description and put todays date in format YYYY-MM-DD
	- Do not show any code or technical details to the user. 
	- Do not use any technical jargon or complex terms.

	""")

	```

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image35.png)

### タスク3: エージェントのプロビジョニングとテスト

このタスクでは、更新され、修理アナリストにもなったエージェントをテストします。

1.  Agents
    Toolkitの拡張アイコンを選択して、プロジェクト内からアクティビティ
    バーを開きます。

2.  ツールキットのアクティビティ
    バーの**\[LifeCycle\]**で**\[Provision\]**を選択し、新しく更新されたエージェントをテスト用にパッケージ化してアップロードします。

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image36.png)

3.  プロビジョニングが成功したことを確認します。

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image37.png)

4.  **ブラウザ**セッションに戻り、**更新**を行ってください。

5.  **RepairServiceAgent**で、会話のスターター「 **Create
    repair」**を使って開始します。プロンプトの一部を置き換えてタイトルを追加し、チャットに送信してやり取りを開始します。例：

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image38.png)

6.  **「\[TO REPLACE\]」を+++** rear camera issue **+++**
    に置き換えて、私に割り当ててください。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

7.  新しい手順のおかげで、確認ダイアログには送信した内容よりも多くのメタデータが含まれていることに気付いたかもしれません。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png)

8.  ダイアログを**確認**してアイテムの追加に進みます。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

9.  エージェントは、**作成されたアイテム**をリッチ**アダプティブ
    カード**に表示して応答します。

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image42.png)

10. 次に、参照カードの動作を再確認します。以下のプロンプトを会話で送信してください。 
	
	+++ List all my repairs +++。

	確認ダイアログで**「Always allow」**を選択します。

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image43.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image44.png)

11. 担当者が、担当修理リストを返信いたします。各項目はアダプティブカードで参照されます。今回の場合は、先ほど追加したリアカメラの問題のみのはずです。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

12. 次に、エージェントの新しい分析機能をテストします。エージェントの右上にある**「New
    chat」**ボタンを選択して、新しいチャットを開いてください。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

13. 次に、以下のプロンプトをコピーしてメッセージ
    ボックスに貼り付け、Enter キーを押して送信します。

14. 修理項目をタイトルに基づいて 3 つの異なるカテゴリに分類します。

15. 定期メンテナンス、重要、低優先度。次にチャートを生成します。

16. 各カテゴリーの割合を表示します。

	![A screenshot of a phone AI-generated content may be
incorrect.](./media/image47.png)

17. のようなレスポンスが表示されるはずです。レスポンスは状況によって異なる場合があります。

	![A screenshot of a data box AI-generated content may be
incorrect.](./media/image48.png)

**まとめ：**

このラボでは、次のことを行います。

- **TypeSpec を**使用してAPI を記述し、それらを Copilot
  アクションにバインドしました。

- 豊富なビジュアルレイアウトで修理記録を表示するように**アダプティブ
  カード**を構成します。

- ユーザーが Copilot
  と自然に対話して修復データを管理できる完全なシナリオを構築します。

このラボでは、宣言型エージェントが**Copilot
プラットフォームのオーケストレーション、基盤モデル、セキュリティ制御を活用して**、カスタム
ビジネス データやワークフローと統合しながら、使い慣れた一貫したユーザー
エクスペリエンスを提供する方法を説明しました。
