# 实验室 1 - 使用 Microsoft 365 代理工具包生成具有 TypeSpec 定义的 RepairService 声明性代理

在本实验室中，你将使用 Microsoft 365 代理工具包生成具有 TypeSpec
定义的声明性代理。您将创建一个名为 RepairServiceAgent
的代理，它通过现有的 API
服务与维修数据进行交互，以帮助用户管理汽车维修记录。

**声明性代理**

**声明性代理是** Microsoft 365 的一种代理。可以通过扩展 Microsoft 365
Copilot
来构建一个。您可以定义自定义知识和自定义作，以创建针对特定方案定制的代理。

声明性代理使用与 Microsoft 365 Copilot
相同的基础结构、业务流程协调程序、基础模型和安全控制，从而确保一致且熟悉的用户体验。

![Declarative agent architecture diagram. At the very basis there is the
foundational model of Microsoft 365 Copilot, as well as the same
orchestrator. The agent provides also custom knowledge and grounding
data, and custom skills as actions, triggers, and workflows.. The user
experience is available in Microsoft 365 Copilot.](./media/image1.png)

**TypeSpec 对声明性代理的意义**

**什么是 TypeSpec**

TypeSpec 是 Microsoft
开发的一种语言，用于以结构化和类型安全的方式设计和描述 API
协定。可以将其视为 API 外观和行为的蓝图，包括它接受、返回的数据以及 API
的不同部分及其作如何连接。

**为什么选择 TypeSpec for Agents?**

如果您喜欢 TypeScript 在前端/后端代码中强制执行结构的方式，您一定会喜欢
TypeSpec 如何在代理及其 API 服务（如作）中强制执行结构。它非常适合与
Visual Studio Code 等工具保持一致的设计优先开发工作流程。

清晰的通信 -
提供单一事实来源，定义您的代理应如何行为，避免在处理多个清单文件时出现混淆，例如声明式代理的情况。

一致性 - 确保代理的所有部分及其作、功能等都遵循相同的模式进行设计。

自动化友好 - 自动生成 OpenAPI 规范和其他清单，节省时间并减少人为错误。

早期验证 -
在编写实际代码之前及早发现设计问题，例如数据类型不匹配或定义不明确。

设计优先的方法 - 鼓励在开始实施之前考虑代理和 API
结构以及契约，从而提高长期可维护性。

## 练习 1: 设置实验室环境

在本练习中，你将设置开发环境来生成、测试和部署 Copilot
代理，这将有助于你使用 Microsoft 365 Copilot 实现量身定制的 AI 辅助。

### 任务 1: 安装代理工具包

**Agents Toolkit for Visual Studio Code** 需要 Visual Studio
Code。在本练习中，你将在 Visual Studio Code 中安装该工具包。

1.  从 VM 打开 **Visual Studio Code**。从**左侧菜单中选择**扩展。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image2.png)

2.  搜索并选择 +++Microsoft 365 Agents Toolkit+++ 并单击**安装**。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image3.png)

3.  确保已安装工具包。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

4.  在桌面中创建一个folder 名为 +++ServiceAgent+++。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image5.png)

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image6.png)

## 练习 2: 使用 Microsoft 365 代理工具包使用 TypeSpec 生成基本代理

在本练习中，您将构建**声明性代理**、定义它、更新作并测试代理。

### 任务 1: 使用 Microsoft 365 代理工具包搭建基本代理项目

在此任务中，你将 **使用** Microsoft 365 代理工具包**生成具有 TypeSpec**
定义的**声明性代理**。您将创建一个名为 **RepairServiceAgent**
的代理，它通过现有的 API
服务与维修数据进行交互，以帮助用户管理汽车维修记录。

1.  从左侧的 VS Code 菜单中找到**Microsoft 365 Agents Toolkit
    icon** ![m365atk-icon](./media/image7.png)  并选择它.
    活动栏将打开。选择活动栏中的“C**reate a New
    Agent/App**”按钮，这将打开面板，其中包含 Microsoft 365
    代理工具包上可用的应用模板列表。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image8.png)

2.  从模板列表中选择**声明**式代理。

    ![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image9.png)

3.  接下来，选择**Start with TypeSpec for Microsoft 365 Copilot** 以使用
    TypeSpec 定义您的代理。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

4.  接下来，从桌面中选择文件夹
    **ServiceAgent**。这是您希望代理工具包将搭建代理项目的位置。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image11.png)

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image12.png)

5.  接下来，将应用程序名称输入为 +++RepairServiceAgent+++，然后选择
    **Enter** 以完成该过程。您将获得一个新的 VS Code
    窗口，其中预加载了代理项目。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image13.png)

6.  需要登录到 **Microsoft 365 Agents
    Toolkit** ，才能从其中上传和测试代理。

7.  在项目窗口中，选择**Microsoft 365 Agents Toolkit
    icon** ![m365atk-icon](./media/image7.png) 再次从左侧菜单。这将打开代理工具包的活动栏，其中包含帐户、环境、开发等部分。

8.  在**“帐户”**部分下，选择**“Sign in to Microsoft 365. ”**。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image14.png)

9.  这将从编辑器中打开一个对话框，用于登录或创建 Microsoft 365
    开发人员沙盒或取消。选择**Sign in** 并使用凭据登录。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image15.png)

10. 登录后，**close** 浏览器并返回项目窗口。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image16.png)

### 任务 2: 定义您的代理

由 Agents Toolkit
搭建的声明性代理项目提供了一个模板，其中包含用于将代理连接到 GitHub API
以显示存储库问题的代码。在本实验室中，你将构建自己的代理，该代理与汽车维修服务集成，支持多种作来管理维修数据。

在项目文件夹中，您将找到两个 **TypeSpec** 文件 **main.tsp** 和
**actions.tsp**。代理在 **main.tsp**
文件中使用**其元数据**、**指令**和**功能**进行定义。使用 **actions.tsp**
文件定义**代理的作**。如果您的代理包含任何作，例如连接到 API
服务，则这是应定义它的文件。

打开 **main.tsp**
并检查默认模板中的内容，您将针对代理的修复服务方案修改该模板。

**更新代理元数据和说明**

在 **main.tsp**
文件中，您将找到代理的基本结构。查看代理工具包模板提供的内容，其中包括：
-

- **代理名称**和**描述** 1️⃣

- 基本**说明** 2️⃣

- **Actions** 和**功能**的 **占位符代码** (注释掉) 3️⃣

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image17.png)

1.  识别代码的**@agent**和**@instructions**块（从第 10 行到第 17 行）。

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image18.png)

2.  首先为修复方案定义代理。将**@agent**和**@instruction**定义替换为以下代码片段。

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

    [A screenshot of a computer program AI-generated content may be
incorrect.](./media/image19.png)

3.  接下来，为代理添加对话启动器。在说明下方，您将看到对话启动器的注释掉代码。将@conversationStarter块（应该是
    22 到 25 之间的行）替换为以下代码。

    ```
    @conversationStarter(#{
      title: "List repairs",
      text: "List all repairs"
    })

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image20.png)

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image21.png)

### 任务 3: 更新代理的 Action

在此任务中，您将通过打开 **actions.tsp**
文件来定义代理的作。稍后将返回到 main.tsp
文件，以使用作引用完成代理元数据，但首先，必须定义作本身。

actions.tsp 中的占位符代码旨在搜索 GitHub
存储库中的未解决问题。它作为一个起点，帮助新手了解如何为其代理定义作，例如作的元数据、API
主机 URL 和作或函数及其定义。您将用维修服务取代所有这些。

1.  打开文件 **actions.tsp**。将从 **@service** 开始到 **const
    SERVER_URL**（行号应为 7 到 25）的代码替换为以下代码块。

    此更新引入了作元数据并设置了服务器 URL。另请注意，命名空间已从 GitHubAPI
更改为 RepairsAPI。

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

2.  接下来，将模板代码中的作从 searchIssues 替换为
    **listRepairs**，这是一个用于获取**repairs**列表的修复操作。将从SERVER_URL定义之后开始到
    最后一个右大括号之前结束的整个代码块替换为下面的代码片段。请务必保持右大括号完好无损。（行号应为
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

3.  现在返回到 **main.tsp**
    文件，并将刚刚定义的作添加到代理中。对话开始后，将整个代码块替换为以下代码片段。

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

### 任务 4: (只读) 了解装饰器

这是一项了解我们在 TypeSpec
文件中定义的内容的任务。只需通读此任务即可。在 TypeSpec 文件 main.tsp 和
actions.tsp 中，您将找到代理的装饰器（以 @
开头）、命名空间、模型和其他定义。

查看以下详细信息以了解这些文件中使用的一些装饰器

- **@agent** - 定义代理的命名空间（名称）和描述

- **@instructions** - 定义规定代理行为的指令。8000 个字符或更少

- **@conversationStarter** - 为代理定义对话启动器

op - 定义任何作。它可以是定义代理功能的作，如 op GraphicArt、op
CodeInterpreter 等，也可以是定义 API作，如 op listRepairs。

- **@server** - 定义 API 的服务器端点及其名称

- **@capabilities** -
  在函数中使用时，它定义了具有小定义的简单自适应卡，例如作的确认卡

### 任务 5: 测试您的代理

在此任务中，您将测试刚刚创建的修复服务代理。

1.  选择** Agents Toolkit extension 的**图标，以从项目中打开活动栏。

    ![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image24.png)

2.  在“代理工具包”的“**LifeCycle**”下的活动栏中**，**选择**“Provision”**。这将生成由生成的清单文件和图标组成的应用包，并将应用侧载到目录中，仅供你测试。

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image25.png)

3.  打开您的 Web 浏览器并导航到 +++https://m365.cloud.microsoft/chat+++ to open Copilot app.

4.  从 Microsoft 365 Copilot 界面中可用的**代理**列表中选择
    **RepairServiceAgent**。这将需要一段时间，您将能够看到一条烤面包机消息，其中显示要预配的任务的进度。

    ![A screenshot of a chat AI-generated content may be
incorrect.](./media/image26.png)

5.  选择对话启动器**列表修复**并发送提示。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

6.  这将启动与代理的对话，您可以看到代理的响应以及维修列表。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

## 练习 3: 增强代理功能

在本练习中，你将通过添加更多作、使用自适应卡片启用响应以及合并代码解释器功能来增强代理。让我们逐步探讨这些增强功能中的每一个。返回到
VS Code 中的项目。

### 任务 1: 修改代理以添加更多操作

在此任务中，您将修改代理并添加作，例如**createRepair**, **updateRepair** 和 **deleteRepair.**

1.  转到文件 **actions.tsp 并在**
    listRepairs作**后立即复制粘贴到下面的代码片段** 以添加这些新作
    **createRepair**、**updateRepair** 和
    **deleteRepair**。在这里，您还定义了维修物料数据模型。

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

2.  现在，打开 **main.tsp** 文件并将这些新作添加到代理的作中。
    **将以下代码段粘贴**到该行后面 **op listRepairs is
    global.RepairsAPI.listRepairs;** 在 **RepairServiceActions**
    命名空间中。

	```
	op createRepair is global.RepairsAPI.createRepair;
	op updateRepair is global.RepairsAPI.updateRepair;
	op deleteRepair is global.RepairsAPI.deleteRepair;
	```

    ![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image30.png)

3.  此外，还添加一个新的对话启动器，以便在第一个对话开始定义之后创建新的修复项。

	```
	@conversationStarter(#{
	  title: "Create repair",
	  text: "Create a new repair titled \"[TO_REPLACE]\" and assign it to me"
	})
	```

    ![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image31.png)

### 任务 2: 将自适应卡片添加到函数引用

在此任务中，您将使用自适应卡片增强参考卡或响应卡。让我们进行
**listRepairs**作，并为修复项添加自适应卡。

1.  在项目文件夹中，在 appPackage **文件夹**下创建一个名为 +++cards+++
    的新文件夹。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image32.png)

2.  在 **cards** 文件夹**中创建一个文件 +++repair.json+++**
    ，然后将代码片段按原样从下面粘贴到文件中。

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

3.  接下来，返回到 **actions.tsp** 文件并找到 **listRepairs**作。
    将作定义 **@get op listRepairs(@query assignedTo?: string):
    string;,**  行替换为以下 2 行代码。

	```
	@card(#{ dataPath: "$", title: "$.title",   url: "$.image", file: "cards/repair.json"})
	@get op listRepairs(@query assignedTo?: string): Repair[];
	```

    ![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image34.png)

4.  当您询问维修项目或代理携带项目列表作为参考时，代理将发送上述卡片响应。

5.  由于代理现在支持其他功能，因此请相应地更新说明以反映此增强功能。

6.  在同一个 **main.tsp**
    文件中，更新指令定义以具有代理的其他指令。将现有**的@instructions**代码块替换为以下代码块。

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

### 任务 3: 配置和测试代理

在此任务中，您将对更新后的代理进行测试，该代理现在也是维修分析师。

1.  选择代理工具包的扩展图标，从项目中打开其活动栏。

2.  在工具包的活动栏中，在**lifeCycle** 下，选择** Provision
    以**打包并上传新更新的代理进行测试。

    ![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image36.png)

3.  确保预配成功。

    ![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image37.png)

4.  返回打开的**浏览器**会话并执行**刷新**。

5.  在 **RepairServiceAgent**，首先使用对话启动器创建**Create
    repair**。替换提示的部分内容以添加标题，然后将其发送到聊天以启动交互。例如：

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image38.png)

6.  将**“\[TO REPLACE\]”** 替换为 +++后置摄像头问题+++ 并将其分配给我。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

7.  如果您注意到确认对话框的元数据比您发送的元数据更多，这要归功于新的说明。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png)

8.  通过确认**confirming** 继续添加项目。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

9.  代理使用丰富的**自适应卡片**中显示的**已创建项进行响应**。

    ![A screenshot of a chat AI-generated content may be
incorrect.](./media/image42.png)

10. 接下来，重新检查参考卡是否有效。在对话中发送以下提示。 
    
    +++List all my repairs+++.

    在确认对话框中选择“**Always allow** ”。

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image43.png)

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image44.png)

11. 代理将回复分配给您的维修清单。每个项目都引用自适应卡片。在这种情况下，应该只是您刚刚添加的后置摄像头问题。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

12. 接下来，您将测试代理的新分析能力。通过选择
    代理右上角的**新聊天**按钮打开新聊天。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

13. 接下来，复制下面的提示并将其粘贴到消息框中，然后按 Enter 键发送。

14. 根据标题将维修项目分为三个不同的类别：

15. 日常维护、关键和低优先级。然后，生成图表

16. 显示每个类别的百分比表示。

    ![A screenshot of a phone AI-generated content may be
incorrect.](./media/image47.png)

17. 您应该会得到类似于以下屏幕的响应。有时可能会有所不同。

    ![A screenshot of a data box AI-generated content may be
incorrect.](./media/image48.png)

**总结:**

在本实验室中，您拥有:

- 使用 **TypeSpec** 描述 API 并将其绑定到 Copilot作。

- 配置**自适应卡片**以丰富的视觉布局显示维修记录。

- 构建一个完整的场景，用户可以与 Copilot 自然交互以管理维修数据。

本实验室演示了声明式代理如何利用 **Copilot
平台的业务流程、基础模型和安全控制**来提供熟悉且一致的用户体验，同时与自定义业务数据和工作流集成。
