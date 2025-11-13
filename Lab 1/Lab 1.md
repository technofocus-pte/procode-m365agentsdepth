# 實驗室 1 - 使用 Microsoft 365 代理工具包生成具有 TypeSpec 定義的 RepairService 聲明性代理

在本實驗室中，你將使用 Microsoft 365 代理工具包生成具有 TypeSpec
定義的聲明性代理。您將創建一個名為 RepairServiceAgent
的代理，它通過現有的 API
服務與維修數據進行交互，以幫助用戶管理汽車維修記錄。

**聲明性代理**

**聲明性代理是** Microsoft 365 的一種代理。可以通過擴展 Microsoft 365
Copilot
來構建一個。您可以定義自定義知識和自定義作，以創建針對特定方案定制的代理。

聲明性代理使用與 Microsoft 365 Copilot
相同的基礎結構、業務流程協調程序、基礎模型和安全控制，從而確保一致且熟悉的用戶體驗。

![Declarative agent architecture diagram. At the very basis there is the
foundational model of Microsoft 365 Copilot, as well as the same
orchestrator. The agent provides also custom knowledge and grounding
data, and custom skills as actions, triggers, and workflows.. The user
experience is available in Microsoft 365 Copilot.](./media/image1.png)

**TypeSpec 對聲明性代理的意義**

**什麼是 TypeSpec**

TypeSpec 是 Microsoft
開發的一種語言，用於以結構化和類型安全的方式設計和描述 API
協定。可以將其視為 API 外觀和行為的藍圖，包括它接受、返回的數據以及 API
的不同部分及其作如何連接。

**為什麼選擇 TypeSpec for Agents?**

如果您喜歡 TypeScript 在前端/後端代碼中強制執行結構的方式，您一定會喜歡
TypeSpec 如何在代理及其 API 服務（如作）中強制執行結構。它非常適合與
Visual Studio Code 等工具保持一致的設計優先開發工作流程。

清晰的通信 -
提供單一事實來源，定義您的代理應如何行為，避免在處理多個清單文件時出現混淆，例如聲明式代理的情況。

一致性 - 確保代理的所有部分及其作、功能等都遵循相同的模式進行設計。

自動化友好 - 自動生成 OpenAPI 規範和其他清單，節省時間並減少人為錯誤。

早期驗證 -
在編寫實際代碼之前及早發現設計問題，例如數據類型不匹配或定義不明確。

設計優先的方法 - 鼓勵在開始實施之前考慮代理和 API
結構以及契約，從而提高長期可維護性。

## 練習 1: 設置實驗室環境

在本練習中，你將設置開發環境來生成、測試和部署 Copilot
代理，這將有助於你使用 Microsoft 365 Copilot 實現量身定制的 AI 輔助。

### 任務 1: 安裝代理工具包

**Agents Toolkit for Visual Studio Code** 需要 Visual Studio
Code。在本練習中，你將在 Visual Studio Code 中安裝該工具包。

1.  從 VM 打開 **Visual Studio Code**。從**左側菜單中選擇**擴展。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image2.png)

2.  搜索並選擇 +++Microsoft 365 Agents Toolkit+++ 並單擊**安裝**。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image3.png)

3.  確保已安裝工具包。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

4.  在桌面中創建一個folder 名為 +++ServiceAgent+++。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image5.png)

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image6.png)

## 練習 2: 使用 Microsoft 365 代理工具包使用 TypeSpec 生成基本代理

在本練習中，您將構建**聲明性代理**、定義它、更新作並測試代理。

### 任務 1: 使用 Microsoft 365 代理工具包搭建基本代理項目

在此任務中，你將 **使用** Microsoft 365 代理工具包**生成具有 TypeSpec**
定義的**聲明性代理**。您將創建一個名為 **RepairServiceAgent**
的代理，它通過現有的 API
服務與維修數據進行交互，以幫助用戶管理汽車維修記錄。

1.  從左側的 VS Code 菜單中找到**Microsoft 365 Agents Toolkit
    icon** ![m365atk-icon](./media/image7.png)  並選擇它.
    活動欄將打開。選擇活動欄中的“C**reate a New
    Agent/App**”按鈕，這將打開面板，其中包含 Microsoft 365
    代理工具包上可用的應用模板列表。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image8.png)

2.  從模板列表中選擇**聲明**式代理。

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image9.png)

3.  接下來，選擇**Start with TypeSpec for Microsoft 365 Copilot** 以使用
    TypeSpec 定義您的代理。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

4.  接下來，從桌面中選擇文件夾
    **ServiceAgent**。這是您希望代理工具包將搭建代理項目的位置。

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image11.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image12.png)

5.  接下來，將應用程序名稱輸入為 +++RepairServiceAgent+++，然後選擇
    **Enter** 以完成該過程。您將獲得一個新的 VS Code
    窗口，其中預加載了代理項目。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image13.png)

6.  需要登錄到 **Microsoft 365 Agents
    Toolkit** ，才能從其中上傳和測試代理。

7.  在項目窗口中，選擇**Microsoft 365 Agents Toolkit
    icon** ![m365atk-icon](./media/image7.png) 再次從左側菜單。這將打開代理工具包的活動欄，其中包含帳戶、環境、開發等部分。

8.  在**“帳戶”**部分下，選擇**“Sign in to Microsoft 365. ”**。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image14.png)

9.  這將從編輯器中打開一個對話框，用於登錄或創建 Microsoft 365
    開發人員沙盒或取消。選擇**Sign in** 並使用憑據登錄。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image15.png)

10. 登錄後，**close** 瀏覽器並返回項目窗口。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image16.png)

### 任務 2: 定義您的代理

由 Agents Toolkit
搭建的聲明性代理項目提供了一個模板，其中包含用於將代理連接到 GitHub API
以顯示存儲庫問題的代碼。在本實驗室中，你將構建自己的代理，該代理與汽車維修服務集成，支持多種作來管理維修數據。

在項目文件夾中，您將找到兩個 **TypeSpec** 文件 **main.tsp** 和
**actions.tsp**。代理在 **main.tsp**
文件中使用**其元數據**、**指令**和**功能**進行定義。使用 **actions.tsp**
文件定義**代理的作**。如果您的代理包含任何作，例如連接到 API
服務，則這是應定義它的文件。

打開 **main.tsp**
並檢查默認模板中的內容，您將針對代理的修復服務方案修改該模板。

**更新代理元數據和說明**

在 **main.tsp**
文件中，您將找到代理的基本結構。查看代理工具包模板提供的內容，其中包括：
-

- **代理名稱**和**描述** 1️⃣

- 基本**說明** 2️⃣

- **Actions** 和**功能**的 **占位符代碼** (注釋掉) 3️⃣

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image17.png)

1.  識別代碼的**@agent**和**@instructions**塊（從第 10 行到第 17 行）。

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image18.png)

2.  首先為修復方案定義代理。將**@agent**和**@instruction**定義替換為以下代碼片段。

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

3.  接下來，為代理添加對話啟動器。在說明下方，您將看到對話啟動器的注釋掉代碼。將@conversationStarter塊（應該是
    22 到 25 之間的行）替換為以下代碼。

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

### 任務 3: 更新代理的 Action

在此任務中，您將通過打開 **actions.tsp**
文件來定義代理的作。稍後將返回到 main.tsp
文件，以使用作引用完成代理元數據，但首先，必須定義作本身。

actions.tsp 中的占位符代碼旨在搜索 GitHub
存儲庫中的未解決問題。它作為一個起點，幫助新手瞭解如何為其代理定義作，例如作的元數據、API
主機 URL 和作或函數及其定義。您將用維修服務取代所有這些。

1.  打開文件 **actions.tsp**。將從 **@service** 開始到 **const
    SERVER_URL**（行號應為 7 到 25）的代碼替換為以下代碼塊。

此更新引入了作元數據並設置了服務器 URL。另請注意，命名空間已從 GitHubAPI
更改為 RepairsAPI。

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

2.  接下來，將模板代碼中的作從 searchIssues 替換為
    **listRepairs**，這是一個用於獲取**repairs**列表的修復操作。將從SERVER_URL定義之後開始到
    最後一個右大括號之前結束的整個代碼塊替換為下面的代碼片段。請務必保持右大括號完好無損。（行號應為
    27 至 37）

	```
	/**
	* List repairs from the API 
	* @param assignedTo The user assigned to a repair item.
	*/

	@route("/repairs")
	@get  op listRepairs(@query assignedTo?: string): string;
	```

	![A screenshot of a computer program AI-generated content may be incorrect.](./media/image22.png)

3.  現在返回到 **main.tsp**
    文件，並將剛剛定義的作添加到代理中。對話開始後，將整個代碼塊替換為以下代碼片段。

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

### 任務 4: (只讀) 瞭解裝飾器

這是一項瞭解我們在 TypeSpec
文件中定義的內容的任務。只需通讀此任務即可。在 TypeSpec 文件 main.tsp 和
actions.tsp 中，您將找到代理的裝飾器（以 @
開頭）、命名空間、模型和其他定義。

查看以下詳細信息以瞭解這些文件中使用的一些裝飾器

- **@agent** - 定義代理的命名空間（名稱）和描述

- **@instructions** - 定義規定代理行為的指令。8000 個字符或更少

- **@conversationStarter** - 為代理定義對話啟動器

op - 定義任何作。它可以是定義代理功能的作，如 op GraphicArt、op
CodeInterpreter 等，也可以是定義 API作，如 op listRepairs。

- **@server** - 定義 API 的服務器端點及其名稱

- **@capabilities** -
  在函數中使用時，它定義了具有小定義的簡單自適應卡，例如作的確認卡

### 任務 5: 測試您的代理

在此任務中，您將測試剛剛創建的修復服務代理。

1.  選擇** Agents Toolkit extension 的**圖標，以從項目中打開活動欄。

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image24.png)

2.  在“代理工具包”的“**LifeCycle**”下的活動欄中**，**選擇**“Provision”**。這將生成由生成的清單文件和圖標組成的應用包，並將應用側載到目錄中，僅供你測試。

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image25.png)

3.  打開您的 Web 瀏覽器並導航到 +++https://m365.cloud.microsoft/chat+++ to open Copilot app.

4.  從 Microsoft 365 Copilot 界面中可用的**代理**列表中選擇
    **RepairServiceAgent**。這將需要一段時間，您將能夠看到一條烤麵包機消息，其中顯示要預配的任務的進度。

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image26.png)

5.  選擇對話啟動器**列表修復**並發送提示。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

6.  這將啟動與代理的對話，您可以看到代理的響應以及維修列表。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

## 練習 3: 增強代理功能

在本練習中，你將通過添加更多作、使用自適應卡片啟用響應以及合併代碼解釋器功能來增強代理。讓我們逐步探討這些增強功能中的每一個。返回到
VS Code 中的項目。

### 任務 1: 修改代理以添加更多操作

在此任務中，您將修改代理並添加作，例如**createRepair**, **updateRepair** 和 **deleteRepair.**

1.  轉到文件 **actions.tsp 並在**
    listRepairs作**後立即複製粘貼到下面的代碼片段** 以添加這些新作
    **createRepair**、**updateRepair** 和
    **deleteRepair**。在這裡，您還定義了維修物料數據模型。

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

2.  現在，打開 **main.tsp** 文件並將這些新作添加到代理的作中。
    **將以下代碼段粘貼**到該行後面 **op listRepairs is
    global.RepairsAPI.listRepairs;** 在 **RepairServiceActions**
    命名空間中。

	```
	op createRepair is global.RepairsAPI.createRepair;
	op updateRepair is global.RepairsAPI.updateRepair;
	op deleteRepair is global.RepairsAPI.deleteRepair;
	```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image30.png)

3.  此外，還添加一個新的對話啟動器，以便在第一個對話開始定義之後創建新的修復項。

	```
	@conversationStarter(#{
	title: "Create repair",
	text: "Create a new repair titled \"[TO_REPLACE]\" and assign it to me"
	})
	```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image31.png)

### 任務 2: 將自適應卡片添加到函數引用

在此任務中，您將使用自適應卡片增強參考卡或響應卡。讓我們進行
**listRepairs**作，並為修復項添加自適應卡。

1.  在項目文件夾中，在 appPackage **文件夾**下創建一個名為 +++cards+++
    的新文件夾。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image32.png)

2.  在 **cards** 文件夾**中創建一個文件 +++repair.json+++**
    ，然後將代碼片段按原樣從下面粘貼到文件中。

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

3.  接下來，返回到 **actions.tsp** 文件並找到 **listRepairs**作。
    將作定義 **@get op listRepairs(@query assignedTo?: string):
    string;,**  行替換為以下 2 行代碼。

	```
	@card(#{ dataPath: "$", title: "$.title",   url: "$.image", file: "cards/repair.json"})
	@get op listRepairs(@query assignedTo?: string): Repair[];
	```

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image34.png)

4.  當您詢問維修項目或代理攜帶項目列表作為參考時，代理將發送上述卡片響應。

5.  由於代理現在支持其他功能，因此請相應地更新說明以反映此增強功能。

6.  在同一個 **main.tsp**
    文件中，更新指令定義以具有代理的其他指令。將現有**的@instructions**代碼塊替換為以下代碼塊。

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

### 任務 3: 配置和測試代理

在此任務中，您將對更新後的代理進行測試，該代理現在也是維修分析師。

1.  選擇代理工具包的擴展圖標，從項目中打開其活動欄。

2.  在工具包的活動欄中，在**lifeCycle** 下，選擇** Provision
    以**打包並上傳新更新的代理進行測試。

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image36.png)

3.  確保預配成功。

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image37.png)

4.  返回打開的**瀏覽器**會話並執行**刷新**。

5.  在 **RepairServiceAgent**，首先使用對話啟動器創建**Create
    repair**。替換提示的部分內容以添加標題，然後將其發送到聊天以啟動交互。例如：

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image38.png)

6.  將**“\[TO REPLACE\]”** 替換為 +++後置攝像頭問題+++ 並將其分配給我。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

7.	如果您注意到確認對話框的元數據比您發送的元數據更多，這要歸功於新的說明。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png)

8.  通過確認**confirming** 繼續添加項目。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

9.  代理使用豐富的**自適應卡片**中顯示的**已創建項進行響應**。

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image42.png)

10. 接下來，重新檢查參考卡是否有效。在對話中發送以下提示。 +++List all my repairs+++.

	在確認對話框中選擇“**Always allow** ”。

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image43.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image44.png)

11. 代理將回復分配給您的維修清單。每個項目都引用自適應卡片。在這種情況下，應該只是您剛剛添加的後置攝像頭問題。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

12. 接下來，您將測試代理的新分析能力。通過選擇
    代理右上角的**新聊天**按鈕打開新聊天。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

13. 接下來，複製下面的提示並將其粘貼到消息框中，然後按 Enter 鍵發送。

14. 根據標題將維修項目分為三個不同的類別：

15. 日常維護、關鍵和低優先級。然後，生成圖表

16. 顯示每個類別的百分比表示。

	![A screenshot of a phone AI-generated content may be
incorrect.](./media/image47.png)

17. 您應該會得到類似於以下屏幕的響應。有時可能會有所不同。

	![A screenshot of a data box AI-generated content may be
incorrect.](./media/image48.png)

**總結:**

在本實驗室中，您擁有:

- 使用 **TypeSpec** 描述 API 並將其綁定到 Copilot作。

- 配置**自適應卡片**以豐富的視覺佈局顯示維修記錄。

- 構建一個完整的場景，用戶可以與 Copilot 自然交互以管理維修數據。

本實驗室演示了聲明式代理如何利用 **Copilot
平臺的業務流程、基礎模型和安全控制**來提供熟悉且一致的用戶體驗，同時與自定義業務數據和工作流集成。
