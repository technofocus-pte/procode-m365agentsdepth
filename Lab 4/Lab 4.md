# Lab 4- Zava 的人工智能集成之旅 – 在 Microsoft Copilot Studio 中構建 MCP 支持的代理

## 場景:

Zava
是一家快速發展的數字健康組織，最近成立了一個**內部創新中心**，以試驗新的人工智能功能，這些功能稍後可以應用於受監管的醫療保健解決方案。在連接敏感醫療系統之前，創新團隊需要一個**安全、低風險的沙盒，以瞭解如何**使用**模型上下文協議
（MCP）** 將外部 API 和數據源與 **Microsoft Copilot Studio 集成**。

為此，該團隊從一個**簡單、無害的示例（**Jokes MCP
服務器*）*開始，該示例演示了 Copilot Studio 如何通過 MCP 調用實時
API。這個輕量級原型可幫助工程師、數據科學家和 AI 解決方案架構師瞭解：

- 如何將 MCP 服務器部署到 Azure，

- Copilot Studio 如何發現和使用 MCP 工具，以及

- 如何將實時外部數據安全地集成到代理中.

通過完成此實驗，Zava 創新團隊為將未來的 MCP
服務器連接到實際業務系統奠定了基礎——一旦應用了治理和合規措施。

## 商業價值:

- 鼓勵在將 MCP 集成應用於敏感領域之前進行實踐學習。

- 演示安全、Azure 就緒設置中的端到端部署和工具使用。

- 為下一代 AI 驅動的工作流程做好組織準備。

## 目標:

在本實驗室中，你將模擬 Zava 的創新中心如何使用模型上下文協議 （MCP）
進行試驗，以將外部 API 和知識源與 Microsoft Copilot Studio
連接起來。您將學習如何將 MCP 服務器部署到 Azure，將其註冊為 Copilot
Studio 中的工具，並將其集成到對話代理中。

完成本實驗後，您將：

- 瞭解 MCP 如何為 Copilot Studio 代理實現安全、實時的數據集成。

- 瞭解如何使用 Azure 開發人員 CLI 部署、配置和連接 MCP 服務器。

- 探索將 MCP 支持的工具添加到 Copilot Studio 代理的端到端工作流。

## 練習 1: 將 MCP 服務器部署到 Azure

在本練習中，你將 使用 Azure 開發人員 CLI （azd） 將 **Microsoft
MCP**（模型上下文協議）服務器從本地開發環境部署到
**Azure**。這將建立一個**雲託管終結點**， **Copilot Studio**
或其他應用程序可以在以後的練習中使用該終結點。

1.  從實驗室 VM 打開 **Docker Desktop**。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image1.png)

2.  打開 **Visual Studio Code** 並選擇 **OpenFolder**。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image2.png)

3.  從 **C：\LabFiles** 中選擇 **mcsmcp**
    文件夾，然後單擊**“選擇文件夾**”。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image3.png)

4.  **選擇Yes, I trust the authors** 繼續。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

5.  從 **VS Code** 中，選擇**“View** -\> **Terminal**  “以打開終端。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image5.png)

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image6.png)

6.  輸入 +++azd auth login+++ 以登錄到**Azure**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image7.png)

7.  **使用**“資源”**選項卡**中的憑據登錄。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image8.png)

8.  輸入 +++azd up+++ ，然後單擊 Enter 將項目基架到 Azure 中。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

9.  將名稱輸入為<+++mcsmcp@lab.LabInstance.Id>+++

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

10. 選擇 **Enter** 以接受列出的訂閱。

	![A screen shot of a computer AI-generated content may be
incorrect.](./media/image11.png)

11. 選擇 **@lab.CloudResourceGroup(ResourceGroup1).Location** 作為您的位置

12. 使用箭頭標記上下滾動區域列表，然後選擇 上述步驟中標識的區域，然後按
    **Enter**。屏幕截圖中的區域與實驗室 VM
    中分配給你的區域可能會有所不同。

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image12.png)

13. 這會在 Azure 門戶中部署必要的資源並輸出成功消息。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image13.png)

14. 輸出還提供**Endpoint url**.  
    **將其保存**到**記事本**中，以便在接下來的練習中使用。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image14.png)

15. 將 **/mcp** 添加到該 URL 的末尾，然後在瀏覽器中打開它。您將在 JSON
    消息中看到錯誤，這沒關係。這意味著您正在訪問 MCP 服務器。

	![](./media/image15.png)

在本練習中，你在 Visual Studio Code 中打開了 MCP 服務器項目，使用 Azure 開發人員 CLI 向 Azure 進行身份驗證，並使用 azd up 命令將解決方案部署到 Azure。部署創建了必要的 Azure 資源（例如容器應用和支持基礎結構），並為 MCP 服務器提供了公共終結點 URL。在瀏覽器中驗證端點確認部署和連接成功，為在即將進行的練習中將 MCP 服務器與下游組件集成奠定了基礎。

## 練習 2: 在 Microsoft Copilot Studio 中使用 Jokes MCP 服務器

### 任務 1: 導入連接器

**目標**

**在 Power Apps** 中導入和配置**自定義 MCP 連接器**，以便與已部署的 MCP
服務器集成。

1.  轉到 +++<https://make.preview.powerapps.com/customconnectors+++>

2.  選擇 **+ New custom connector** -\> **Import from GitHub**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image16.png)

3.  選擇以下詳細信息。

    - **Connector Type – Custom**

    - **Branch – dev**

    - **Connector - MCP-Streamable-HTTP**

	選擇 **Continue**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image17.png)

4.  將 **Connector Name更改** 為 +++**Jokes MCP**+++.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image18.png)

5.  粘貼之前保存的 URL 中的根 URL（https:// 之後的部分），在主機字段中
    選擇** Create connector。**

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image19.png)

	[!Alert] **警告**

您可能會在創建時看到警告和錯誤 - 它應該很快就會解決 -
但您現在可以忽略它。

6.  **關閉**連接器。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image20.png)

	![A screenshot of a computer AI-generated content may be incorrect.](./media/image21.png)

在此任務中，您將 **MCP-Streamable-HTTP** 連接器從 GitHub 導入 Power
Apps，將其重命名為 **Jokes MCP**，並使用 Azure 託管的 MCP 服務器 URL
對其進行配置。這在 Power Platform 和 MCP
服務器之間建立了連接，從而支持將來在後續任務中的交互。

### 任務 2: 創建代理並將 MCP 服務器添加為工具

在此任務中，您將 **在 Microsoft Copilot Studio 中**生成自定義 Jokester
**代理，並使用模型上下文協議 （MCP） 框架將其與 Jokes MCP
服務器集成，使代理能夠從連接的 MCP 終結點獲取和傳遞動態笑話。**

1.  從瀏覽器打開 **Copilot Studio**，其中 url 為

	+++https://copilotstudio.microsoft.com+++/ ，然後使用“資源”**選項卡中的憑據登錄** 。選擇**“開始”**以啟用**試用**許可證。

	![A screenshot of a web page AI-generated content may be
incorrect.](./media/image22.png)

2.  選擇 **Create** -> **+ New agent**.

	![A screenshot of a phone AI-generated content may be
incorrect.](./media/image23.png)

3.  選擇**配置**選項卡以配置代理。

	![A screenshot of a login page AI-generated content may be
incorrect.](./media/image24.png)

4.  輸入以下詳細信息，然後選擇 **Create**.

	- **名字** – +++Jokester+++

	- **描述** – A humor-focused agent that delivers concise, engaging jokes only upon user request, adapting its style to match the user's tone and preferences. It remains in character, avoids repetition, and filters out offensive content to ensure a consistently appropriate and witty experience.+++

- **指示** –

	```
	You are a joke-telling assistant. Your sole purpose is to deliver appropriate, clever, and engaging jokes upon request. Follow these rules:

	* Respond only when the user asks for a joke or something related (e.g., "Tell me something funny").
	* Match the tone and humor preference of the user based on their input—clean, dark, dry, pun-based, dad jokes, etc.
	* Never break character or provide information unrelated to humor.
	* Keep jokes concise and clearly formatted.
	* Avoid offensive, discriminatory, or NSFW content.
	* When unsure about humor preference, default to a clever and universally appropriate joke.
	* Do not repeat jokes within the same session.
	* Avoid explaining the joke unless explicitly asked.
	* Be responsive, witty, and quick.

	```

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image25.png)

5.  根據提供的說明**創建代理**。

	![A logo of a company AI-generated content may be
incorrect.](./media/image26.png)

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

6.  從代理頁面的右上角選擇**設置**。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

7.  在“**設置**”窗格中，在**“Use generative AI orchestration for your
    agent responses**.”下選擇**“否**”。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image29.png)

8.  向下滾動並禁用**Use general knowledge and Use information from the
    Web**。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

9． **Use generative AI orchestration for your agent responses** 下 向上滾動並選擇**是**

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image31.png)

10. 選擇**保存，**然後**關閉**設置窗口。

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image32.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image33.png)

11. 從代理的概述頁面中 ，選擇**工具。**

	[A screenshot of a computer AI-generated content may be
incorrect.](./media/image34.png)

12. 選擇 **+ Add a tool** 以將新工具添加到代理。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image35.png)

13. 在“添加工具”窗口中，選擇“**Model Context Protocol** **”**選項卡。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image36.png)

14. 選擇您之前創建**的 Jokes MCP** 服務器。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image37.png)

15. 選擇“**Not connected** **”旁邊**的**下拉列表**，然後選擇“**reate new
    connection**”。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image38.png)

16. 在下一個屏幕中選擇**Create**。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

17. 建立連接後，選擇“**Add to agent** ”按鈕將 MCP 服務器添加到 Jokester
    代理。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png)

18. 現在，**MCP Server** 已作為**工具**添加到代理中。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

19. 在開始測試代理行為之前，在測試窗格中選擇**Refresh**。

	![A screenshot of a phone AI-generated content may be
incorrect.](./media/image42.png)

20. 輸入 +++Can I get a Chuck Norris joke?+++ ，然後選擇**發送**。

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image43.png)

21. 選擇 **Open connection manager**.

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image44.png)

22. 選擇“**連接”**以建立連接。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

23. 選擇 Jokes MCP 連接後，選擇**Submit**.**。**

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

24. 現在，您可以看到在**“Manage your connections** **”**頁面中，Jokes
    MCP 服務器處於**connected **狀態。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image47.png)

25. 連接後，導航回“測試”窗格並選擇“ **Retry**”。

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image48.png)

26． 現在，您可以看到正在調用 MCP 服務器，並且代理嘗試從 Jokes MCP 服務器生成響應。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image49.png)

27. 代理使用 **MCP 服務器**，生成響應並將其**填充到**“**Test
    pane**”窗格**中**。

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image50.png)

這是在 **Microsoft Copilot Studio** 中工作的 **Jokes MCP 服務器**。

在此任務中，您在 Copilot Studio 中創建了一個名為 **Jokester**
的新代理，配置了其用於幽默生成的用途和行為指令，並啟用**了Generative AI
業務流程**以實現智能響應。然後，您通過模型上下文協議將 **Jokes MCP
服務器**作為工具連接，對連接進行身份驗證，並通過代理的測試面板檢索笑話成功測試了集成。這確認
MCP 服務器已正確連接並在 Copilot Studio 環境中運行。

## 總結

在此實驗室中，Zava 的創新中心成功探索了 **Model Context Protocol
(MCP)（MCP）** 如何通過實時外部數據集成擴展 Microsoft Copilot
Studio。從安全且低風險的示例（**Jokes MCP
Server**）開始，參與者學習了如何使用 Azure 開發人員 CLI **將** MCP
服務器部署到 **Azure**，將其配置為**Custom connector**，並在 **Copilot
Studio 代理中使用它**。

通過這些練習，您創建了一個安全連接到 Jokes MCP 服務器的自定義
**Jokester** 代理，演示了 Copilot Studio 如何通過 MCP 調用實時 API
調用。該實驗室提供了設置、驗證和測試基於 MCP
的工具的實踐經驗，為未來的關鍵業務 MCP
服務器與企業數據系統集成奠定了基礎。
