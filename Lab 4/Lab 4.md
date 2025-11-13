# Lab 4- Zava 的人工智能集成之旅 – 在 Microsoft Copilot Studio 中构建 MCP 支持的代理

## 场景:

Zava
是一家快速发展的数字健康组织，最近成立了一个**内部创新中心**，以试验新的人工智能功能，这些功能稍后可以应用于受监管的医疗保健解决方案。在连接敏感医疗系统之前，创新团队需要一个**安全、低风险的沙盒，以了解如何**使用**模型上下文协议
（MCP）** 将外部 API 和数据源与 **Microsoft Copilot Studio 集成**。

为此，该团队从一个**简单、无害的示例（**Jokes MCP
服务器*）*开始，该示例演示了 Copilot Studio 如何通过 MCP 调用实时
API。这个轻量级原型可帮助工程师、数据科学家和 AI 解决方案架构师了解：

- 如何将 MCP 服务器部署到 Azure，

- Copilot Studio 如何发现和使用 MCP 工具，以及

- 如何将实时外部数据安全地集成到代理中.

通过完成此实验，Zava 创新团队为将未来的 MCP
服务器连接到实际业务系统奠定了基础——一旦应用了治理和合规措施。

## 商业价值:

- 鼓励在将 MCP 集成应用于敏感领域之前进行实践学习。

- 演示安全、Azure 就绪设置中的端到端部署和工具使用。

- 为下一代 AI 驱动的工作流程做好组织准备。

## 目标:

在本实验室中，你将模拟 Zava 的创新中心如何使用模型上下文协议 （MCP）
进行试验，以将外部 API 和知识源与 Microsoft Copilot Studio
连接起来。您将学习如何将 MCP 服务器部署到 Azure，将其注册为 Copilot
Studio 中的工具，并将其集成到对话代理中。

完成本实验后，您将：

- 了解 MCP 如何为 Copilot Studio 代理实现安全、实时的数据集成。

- 了解如何使用 Azure 开发人员 CLI 部署、配置和连接 MCP 服务器。

- 探索将 MCP 支持的工具添加到 Copilot Studio 代理的端到端工作流。

## 练习 1: 将 MCP 服务器部署到 Azure

在本练习中，你将 使用 Azure 开发人员 CLI （azd） 将 **Microsoft
MCP**（模型上下文协议）服务器从本地开发环境部署到
**Azure**。这将建立一个**云托管终结点**， **Copilot Studio**
或其他应用程序可以在以后的练习中使用该终结点。

1.  从实验室 VM 打开 **Docker Desktop**。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image1.png)

2.  打开 **Visual Studio Code** 并选择 **OpenFolder**。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image2.png)

3.  从 **C：\LabFiles** 中选择 **mcsmcp**
    文件夹，然后单击**“选择文件夹**”。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image3.png)

4.  **选择Yes, I trust the authors** 继续。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

5.  从 **VS Code** 中，选择**“View** -\> **Terminal**  “以打开终端。

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image5.png)

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image6.png)

6.  输入 +++azd auth login+++ 以登录到**Azure**.

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image7.png)

7.  **使用**“资源”**选项卡**中的凭据登录。

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image8.png)

8.  输入 +++azd up+++ ，然后单击 Enter 将项目基架到 Azure 中。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

9.  将名称输入为<+++mcsmcp@lab.LabInstance.Id>+++

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

10. 选择 **Enter** 以接受列出的订阅。

    ![A screen shot of a computer AI-generated content may be
incorrect.](./media/image11.png)

11. 选择 **@lab.CloudResourceGroup(ResourceGroup1).Location** 作为您的位置

12. 使用箭头标记上下滚动区域列表，然后选择 上述步骤中标识的区域，然后按
    **Enter**。屏幕截图中的区域与实验室 VM
    中分配给你的区域可能会有所不同。

    ![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image12.png)

13. 这会在 Azure 门户中部署必要的资源并输出成功消息。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image13.png)

14. 输出还提供**Endpoint url**.  
    **将其保存**到**记事本**中，以便在接下来的练习中使用。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image14.png)

15. 将 **/mcp** 添加到该 URL 的末尾，然后在浏览器中打开它。您将在 JSON
    消息中看到错误，这没关系。这意味着您正在访问 MCP 服务器。

    ![](./media/image15.png)

    在本练习中，你在 Visual Studio Code 中打开了 MCP 服务器项目，使用 Azure 开发人员 CLI 向 Azure 进行身份验证，并使用 azd up 命令将解决方案部署到 Azure。部署创建了必要的 Azure 资源（例如容器应用和支持基础结构），并为 MCP 服务器提供了公共终结点 URL。在浏览器中验证端点确认部署和连接成功，为在即将进行的练习中将 MCP 服务器与下游组件集成奠定了基础。

## 练习 2: 在 Microsoft Copilot Studio 中使用 Jokes MCP 服务器

### 任务 1: 导入连接器

**目标**

**在 Power Apps** 中导入和配置**自定义 MCP 连接器**，以便与已部署的 MCP
服务器集成。

1.  转到 +++<https://make.preview.powerapps.com/customconnectors+++>

2.  选择 **+ New custom connector** -\> **Import from GitHub**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image16.png)

3.  选择以下详细信息。

    - **Connector Type – Custom**

    - **Branch – dev**

    - \*\*Connector - MCP-Streamable-HTTP \*\*

    选择 **Continue**.

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image17.png)

4.  将 **Connector Name更改** 为 +++**Jokes MCP**+++.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image18.png)

5.  粘贴之前保存的 URL 中的根 URL（https:// 之后的部分），在主机字段中
    选择** Create connector。**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image19.png)

    [!Alert] **警告**

    您可能会在创建时看到警告和错误 - 它应该很快就会解决 -
但您现在可以忽略它。

6.  **关闭**连接器。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image20.png)

    ![A screenshot of a computer AI-generated content may be incorrect.](./media/image21.png)

    在此任务中，您将 **MCP-Streamable-HTTP** 连接器从 GitHub 导入 Power
Apps，将其重命名为 **Jokes MCP**，并使用 Azure 托管的 MCP 服务器 URL
对其进行配置。这在 Power Platform 和 MCP
服务器之间建立了连接，从而支持将来在后续任务中的交互。

### 任务 2: 创建代理并将 MCP 服务器添加为工具

在此任务中，您将 **在 Microsoft Copilot Studio 中**生成自定义 Jokester
**代理，并使用模型上下文协议 （MCP） 框架将其与 Jokes MCP
服务器集成，使代理能够从连接的 MCP 终结点获取和传递动态笑话。**

1.  从浏览器打开 **Copilot Studio**，其中 url 为

    +++https://copilotstudio.microsoft.com+++/+++ ，然后使用“资源”**选项卡中的凭据登录** 。选择**“开始”**以启用**试用**许可证。

    ![A screenshot of a web page AI-generated content may be
incorrect.](./media/image22.png)

2.  选择 **Create** -\> **+ New agent**.

    ![A screenshot of a phone AI-generated content may be
incorrect.](./media/image23.png)

3.  选择**配置**选项卡以配置代理。

    ![A screenshot of a login page AI-generated content may be
incorrect.](./media/image24.png)

4.  输入以下详细信息，然后选择 **Create**.

    - **名字** – +++Jokester+++

    - **描述** – +++A humor-focused agent that delivers concise, engaging jokes only upon user request, adapting its style to match the user's tone and preferences. It remains in character, avoids repetition, and filters out offensive content to ensure a consistently appropriate and witty experience.+++

    - **指示** – You are a joke-telling assistant. Your sole purpose is to deliver appropriate, clever, and engaging jokes upon request. Follow these rules:

    * Respond only when the user asks for a joke or something related (e.g., "Tell me something funny").
    * Match the tone and humor preference of the user based on their input—clean, dark, dry, pun-based, dad jokes, etc.
    * Never break character or provide information unrelated to humor.
    * Keep jokes concise and clearly formatted.
    * Avoid offensive, discriminatory, or NSFW content.
    * When unsure about humor preference, default to a clever and universally appropriate joke.
    * Do not repeat jokes within the same session.
    * Avoid explaining the joke unless explicitly asked.
    * Be responsive, witty, and quick.


    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image25.png)

5.  根据提供的说明**创建代理**。

    ![A logo of a company AI-generated content may be
    incorrect.](./media/image26.png)

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image27.png)

6.  从代理页面的右上角选择**设置**。

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image28.png)

7.  在“**设置**”窗格中，在**“Use generative AI orchestration for your
    agent responses**.”下选择**“否**”。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image29.png)

8.  向下滚动并禁用**Use general knowledge and Use information from the
    Web**。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

9． Use generative AI orchestration for your agent responses 下 向上滚动并选择**是**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image31.png)

10. 选择**保存，**然后**关闭**设置窗口。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image32.png)

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image33.png)

11. 从代理的概述页面中 ，选择**工具。**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image34.png)

12. 选择 **+ Add a tool** 以将新工具添加到代理。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image35.png)

13. 在“添加工具”窗口中，选择“**Model Context Protocol** **”**选项卡。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image36.png)

14. 选择您之前创建**的 Jokes MCP** 服务器。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image37.png)

15. 选择“**Not connected** **”旁边**的**下拉列表**，然后选择“**reate new
    connection**”。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image38.png)

16. 在下一个屏幕中选择**Create**。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

17. 建立连接后，选择“**Add to agent** ”按钮将 MCP 服务器添加到 Jokester
    代理。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png)

18. 现在，**MCP Server** 已作为**工具**添加到代理中。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

19. 在开始测试代理行为之前，在测试窗格中选择**Refresh**。

    ![A screenshot of a phone AI-generated content may be
incorrect.](./media/image42.png)

20. 输入 +++Can I get a Chuck Norris joke?+++ ，然后选择**发送**。

    ![A screenshot of a chat AI-generated content may be
incorrect.](./media/image43.png)

21. 选择 **Open connection manager**.

    ![A screenshot of a chat AI-generated content may be
incorrect.](./media/image44.png)

22. 选择“**连接”**以建立连接。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

23. 选择 Jokes MCP 连接后，选择**Submit**.**。**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

24. 现在，您可以看到在**“Manage your connections** **”**页面中，Jokes
    MCP 服务器处于**connected **状态。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image47.png)

25. 连接后，导航回“测试”窗格并选择“ **Retry**”。

    ![A screenshot of a chat AI-generated content may be
incorrect.](./media/image48.png)

26． 现在，您可以看到正在调用 MCP 服务器，并且代理尝试从 Jokes MCP 服务器生成响应。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image49.png)

27. 代理使用 **MCP 服务器**，生成响应并将其**填充到**“**Test
    pane**”窗格**中**。

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image50.png)

这是在 **Microsoft Copilot Studio** 中工作的 **Jokes MCP 服务器**。

在此任务中，您在 Copilot Studio 中创建了一个名为 **Jokester**
的新代理，配置了其用于幽默生成的用途和行为指令，并启用**了Generative AI
业务流程**以实现智能响应。然后，您通过模型上下文协议将 **Jokes MCP
服务器**作为工具连接，对连接进行身份验证，并通过代理的测试面板检索笑话成功测试了集成。这确认
MCP 服务器已正确连接并在 Copilot Studio 环境中运行。

## 总结

在此实验室中，Zava 的创新中心成功探索了 **Model Context Protocol
(MCP)（MCP）** 如何通过实时外部数据集成扩展 Microsoft Copilot
Studio。从安全且低风险的示例（**Jokes MCP
Server**）开始，参与者学习了如何使用 Azure 开发人员 CLI **将** MCP
服务器部署到 **Azure**，将其配置为**Custom connector**，并在 **Copilot
Studio 代理中使用它**。

通过这些练习，您创建了一个安全连接到 Jokes MCP 服务器的自定义
**Jokester** 代理，演示了 Copilot Studio 如何通过 MCP 调用实时 API
调用。该实验室提供了设置、验证和测试基于 MCP
的工具的实践经验，为未来的关键业务 MCP
服务器与企业数据系统集成奠定了基础。
