# Laboratório 4 - A jornada da Zava para a integração da AI – Criando agentes com tecnologia MCP no Microsoft Copilot Studio

## Cenário:

A Zava, uma organização de saúde digital em rápido crescimento, formou
recentemente um **Internal Innovation Hub** para experimentar novos
recursos de AI que poderiam ser posteriormente adaptados em soluções de
saúde regulamentadas. Antes de conectar sistemas médicos confidenciais,
a equipe de inovação precisa de uma **área restrita segura e de baixo
risco** para aprender a integrar APIs externas e fontes de dados ao
**Microsoft Copilot Studio** usando o **Model Context Protocol (MCP)**.

Para fazer isso, a equipe começa com um **exemplo simples e inofensivo**
— um *Jokes MCP Server* — que demonstra como o Copilot Studio pode
chamar APIs em tempo real por meio do MCP. Este protótipo leve ajuda
engenheiros, cientistas de dados e arquitetos de soluções de AI a
entender:

- como os servidores MCP são implementados no Azure,

- como o Copilot Studio pode descobrir e consumir ferramentas MCP e

- como os dados externos em tempo real podem ser integrados com
  segurança aos agentes.

Ao concluir este laboratório, a equipe de inovação da Zava estabelece a
base para conectar futuros servidores MCP a sistemas de negócios reais,
uma vez que as medidas de governança e conformidade sejam aplicadas.

## Valor comercial:

- Incentiva o aprendizado prático com a integração do MCP antes de
  aplicá-lo a domínios confidenciais.

- Demonstra a implementação de ponta a ponta e o consumo de ferramentas
  em uma configuração segura e pronta para o Azure.

- Cria prontidão organizacional para fluxos de trabalho orientados por
  IA de última geração.

## Objetivo:

Neste laboratório, você simulará como o Hub de Inovação da Zava
experimenta com o Model Context Protocol (MCP) para conectar APIs
externas e fontes de conhecimento com o Microsoft Copilot Studio. Você
aprenderá a implantar um servidor MCP no Azure, registrá-lo como uma
ferramenta no Copilot Studio e integrá-lo a um agente de conversação.

Ao concluir este laboratório, você irá:

- Entender como o MCP permite a integração segura e em tempo real de
  dados para os agentes do Copilot Studio.

- Aprender a implementar, configurar e conectar um servidor MCP usando
  Azure Developer CLI.

- Explorar o fluxo de trabalho completo de adicionar uma ferramenta com
  tecnologia MCP a um agente do Copilot Studio.

## Exercício 1: Implementar o servidor MCP no Azure

Neste exercício, você **implementará** o servidor **Microsoft
MCP** (Model Context Protocol) de um ambiente de desenvolvimento local
para o **Azure** usando o Azure Developer CLI (azd). Isso estabelece um
**endpoint hospedado na nuvem** que pode ser **consumido** pelo
**Copilot Studio** ou outros aplicativos em exercícios posteriores.

1.  Abra o **Docker Desktop** da VM do laboratório.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image1.png)

2.  Abra o **Visual Studio Code** e selecione **OpenFolder**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image2.png)

3.  Selecione a pasta **mcsmcp** de **C:\LabFiles** e clique em **Select
    Folder**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image3.png)

4.  Selecione **Yes, I trust the authors** para continuar.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

5.  No **VS Code**, selecione **View** -\> **Terminal** para abrir o
    terminal.

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image5.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image6.png)

6.  Insira +++azd auth login+++ para fazer login no **Azure**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image7.png)

7.  **Faça login** usando as credenciais da guia **Resources**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image8.png)

8.  Insira +++azd up+++ e pressione Enter para criar o projeto no Azure.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

9.  Digite o nome como <+++mcsmcp@lab.LabInstance.Id>+++

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

10. Clique em **Enter** para aceitar a assinatura listada.

	![A screen shot of a computer AI-generated content may be
incorrect.](./media/image11.png)

11. Selecione **@lab.CloudResourceGroup(ResourceGroup1).Location** como
    sua localização

12. Use as marcas de seta para rolar para cima e para baixo na lista de
    regiões e selecione a **região** identificada na etapa acima e
    pressione **Enter**. A região na captura de tela e a atribuída a
    você na VM do laboratório podem variar.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image12.png)

13. Isso implementa os recursos necessários no portal do Azure e gera
    uma mensagem de êxito.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image13.png)

14. A saída também fornece uma **URL de endpoint**. **Salve-a** em um
    **bloco de notas** para ser usada nos próximos exercícios.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image14.png)

15. Adicione **/mcp** ao final desse URL e abra-o em um navegador. Você
    verá um erro dentro de uma mensagem JSON, o que está ok. Isso
    significa que você está acessando o servidor MCP.

	![](./media/image15.png)

Neste exercício, você abriu o projeto do MCP Server no Visual Studio Code, autenticou no Azure usando a CLI do Desenvolvedor do Azure e implantou a solução no Azure usando o comando azd up. A implementação criou os recursos necessários do Azure (como um Aplicativo de Contêiner e infraestrutura de suporte) e forneceu uma URL de ponto de extremidade pública para o Servidor MCP. A verificação do endpoint em um navegador confirmou a implantação e a conectividade bem-sucedidas, configurando a base para integrar o MCP Server com componentes downstream nos próximos exercícios.

## Exercício 2: Usar o servidor MCP Jokes no Microsoft Copilot Studio

### Tarefa 1: Importar o conector

**Objetivo**

Para importar e configurar um **conector MCP personalizado** no **Power
Apps** para integração com o servidor MCP implantado.

1.  Vá em +++https://make.preview.powerapps.com/customconnectors+++

2.  Selecione **+ New custom connector** -\> **Import from GitHub**.

	[A screenshot of a computer AI-generated content may be
incorrect.](./media/image16.png)

3.  Selecione os detalhes abaixo.

    - **Connector Type – Custom**

    - **Branch – dev**

    - **Connector - MCP-Streamable-HTTP**

	Selecione **Continue**.

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image17.png)

4.  Altere o **Connector Name** para +++**Jokes MCP**+++.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image18.png)

5.  Cole a URL raiz (a parte após https://) da URL que você salvou
    anteriormente, no campo **Host**, selecione **Create connector**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image19.png)

	[Alerta!] **Aviso**

	Você pode ver um aviso e um erro na criação - deve ser resolvido em
	breve - mas você pode ignorá-lo por enquanto.

6.  Clique em **Close** para fechar o conector.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image20.png)

	![A screenshot of a computer AI-generated content may be incorrect.](./media/image21.png)

	Nesta tarefa, você importou o conector **MCP-Streamable-HTTP** do GitHub
para o Power Apps, renomeou-o para **Jokes MCP** e configurou-o com a
URL do servidor MCP hospedada no Azure. Isso estabelece uma conexão
entre o Power Platform e o MCP Server, permitindo interações futuras em
tarefas subsequentes.

### Tarefa 2: Criar um agente e adicionar o servidor MCP como uma ferramenta

Nesta tarefa, você criará um agente **Jokester** personalizado no
Microsoft Copilot Studio e o integrará ao **Jokes MCP Server** usando a
estrutura MCP (Model Context Protocol), permitindo que o agente busque e
entregue piadas dinâmicas do endpoint MCP conectado.

1.  Abra o **Copilot Studio** em um navegador com a url,
    +++https://copilotstudio.microsoft.com+++/ e
    faça login com as credenciais na guia **Resources**. Selecione **Get
    Started** para habilitar a licença de **teste**.

	![A screenshot of a web page AI-generated content may be
incorrect.](./media/image22.png)

2.  Selecione **Create** -\> **+ New agent**.

	![A screenshot of a phone AI-generated content may be
incorrect.](./media/image23.png)

3.  Selecione a guia **Configure** para configurar seu agente.

	![A screenshot of a login page AI-generated content may be
incorrect.](./media/image24.png)

4.  Insira os detalhes abaixo e selecione **Create**.

	- **Name** – +++Jokester+++

	- **Description** – +++A humor-focused agent that delivers concise, engaging jokes only upon user request, adapting its style to match the user's tone and preferences. It remains in character, avoids repetition, and filters out offensive content to ensure a consistently appropriate and witty experience.+++

	- **Instructions** –
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

5.  O **agente** é **criado** de acordo com as instruções fornecidas.

	![A logo of a company AI-generated content may be
	incorrect.](./media/image26.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image27.png)

6.  Selecione **Settings** no canto superior direito da página do
    agente.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

7.  No painel **Settings**, selecione **No** em **Use generative AI
    orchestration for your agent responses**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image29.png)

8.  Role para baixo e desative **Use general knowledge** e**Use
    information from the Web** na seção **Knowledge**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

9.  Role para cima e selecione **Yes** em **Use generative AI
    orchestration for your agent responses**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image31.png)

10. Selecione **Save** e feche a janela Settings.

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image32.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image33.png)

11. Na página **Overview** do agente, selecione **Tools**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image34.png)

12. Selecione **+ Add a tool** para adicionar uma nova ferramenta ao
    agente.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image35.png)

13. Na janela **Add a tool**, selecione a guia **Model Context
    Protocol**

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image36.png)

14. Selecione o **Jokes MCP Server** que você criou anteriormente.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image37.png)

15. Selecione o **menu suspenso** ao lado de **Not connected** e, em
    seguida, selecione **Create new connection**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image38.png)

16. Selecione **Create** na próxima tela.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

17. Depois que a conexão for estabelecida, selecione o botão **Add to
    agent** para adicionar o servidor MCP ao agente Jokester.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png)

18. Agora, o **servidor MCP** foi adicionado como uma **tool** ao
    agente.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

19. Selecione **Refresh** no painel **Test** antes de começar a testar o
    comportamento do agente.

	![A screenshot of a phone AI-generated content may be
incorrect.](./media/image42.png)

20. Insira +++Can I get a Chuck Norris joke?+++ e selecione **Send**.

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image43.png)

21. Selecione **Open connection manager**.

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image44.png)

22. Selecione **Connect** para estabelecer a conexão.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

23. Depois que a conexão Jokes MCP for selecionada,
    selecione **Submit**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

24. Agora você pode ver isso na página **Manage your connections**, o
    servidor MCP do Jokes está com o **Status** como **Connected**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image47.png)

25. Agora que ele está conectado, navegue de volta para o painel
    **Test** e selecione **Retry**.

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image48.png)

26. Agora você pode ver que o servidor MCP está sendo invocado e o
    agente tenta gerar uma resposta do servidor MCP Jokes.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image49.png)

27. O agente usa o **servidor MCP**, gera uma resposta e a preenche no
    **painel Teste**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image50.png)

E este é o **Jokes MCP Server** trabalhando no **Microsoft Copilot
Studio**.

Nesta tarefa, você criou um novo agente chamado **Jokester** no Copilot
Studio, configurou sua finalidade e instruções comportamentais para
geração de humor e ativou a **Orquestração de AI generativa** para
respostas inteligentes. Em seguida, você conectou o **Jokes MCP Server**
como uma ferramenta por meio do Model Context Protocol, autenticou a
conexão e testou com êxito a integração recuperando piadas por meio do
painel de teste do agente. Isso confirmou que o servidor MCP estava
conectado corretamente e funcionando no ambiente do Copilot Studio.

## Resumo

Neste laboratório, o Centro de Inovação da Zava explorou com sucesso
como o **Model Context Protocol (MCP)** pode estender o Microsoft
Copilot Studio com integração de dados externos em tempo real. Começando
com um exemplo seguro e de baixo risco — o **Jokes MCP Server** — os
participantes aprenderam a implantar um servidor MCP no **Azure** usando
a CLI do **Azure Developer**, configurá-lo como um **conector
personalizado** e consumi-lo em um **agente do Copilot Studio**.

Por meio dos exercícios, você criou um agente **Jokester personalizado**
que se conectou com segurança ao Jokes MCP Server, demonstrando como o
Copilot Studio pode invocar chamadas de API ao vivo por meio do MCP. O
laboratório forneceu experiência prática na configuração, autenticação e
teste de ferramentas baseadas em MCP - estabelecendo a base para
integrar futuros servidores MCP críticos para os negócios com sistemas
de dados corporativos.
