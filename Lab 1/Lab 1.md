# Lab 1 - Crie um agente declarativo RepairService com definição de TypeSpec usando o Microsoft 365 Agents Toolkit

**Objetivo**

Neste laboratório, você criará um Agente Declarativo com definição de
TypeSpec usando o Microsoft 365 Agents Toolkit. Você criará um agente
chamado RepairServiceAgent, que interage com os dados de reparos por
meio de um serviço de API existente para ajudar os usuários a gerenciar
registros de reparos de automóveis.

**Agentes declarativos**

**Agentes declarativos** são um tipo de agentes para o Microsoft 365.
Você pode criar um estendendo o Microsoft 365 Copilot. Você define
conhecimento personalizado e ações personalizadas para criar agentes
personalizados para um cenário específico.

Declarative agents use the same infrastructure, orchestrator, foundation
model, and security controls as Microsoft 365 Copilot, which ensures a
consistent and familiar user experience.

![Declarative agent architecture diagram. At the very basis there is the
foundational model of Microsoft 365 Copilot, as well as the same
orchestrator. The agent provides also custom knowledge and grounding
data, and custom skills as actions, triggers, and workflows.. The user
experience is available in Microsoft 365 Copilot.](./media/image1.png)

**Importância do TypeSpec para agentes declarativos**

**O que é TypeSpec**

TypeSpec é uma linguagem desenvolvida pela Microsoft para projetar e
descrever contratos de API de maneira estruturada e com segurança de
tipo. Pense nisso como um plano de como uma API deve parecer e se
comportar, incluindo quais dados ela aceita, retorna e como diferentes
partes da API e suas ações estão conectadas.

**Por que TypeSpec para agentes?**

Se você gosta de como o TypeScript impõe estrutura em seu código de
front-end/back-end, vai adorar como o TypeSpec impõe a estrutura no seu
agente e nos seus serviços de API, como ações. Ele se encaixa
perfeitamente em fluxos de trabalho de desenvolvimento que priorizam o
design e se alinham com ferramentas como o Visual Studio Code.

Comunicação clara - fornece uma única fonte de verdade que define como
seu agente deve se comportar, evitando confusão ao lidar com vários
arquivos de manifesto, como no caso de Agentes Declarativos.

Consistência - garante que todas as partes do seu agente e suas ações,
recursos, etc. sejam projetados consistentemente seguindo o mesmo
padrão.

Automação amigável - gera automaticamente especificações OpenAPI e
outros manifestos, economizando tempo e reduzindo erros humanos.

Validação antecipada - detecta problemas de design antes de escrever o
código real, por exemplo, tipos de dados incompatíveis ou definições
pouco claras.

Abordagem de design em primeiro lugar - incentiva a pensar sobre a
estrutura e os contratos do agente e da API antes de entrar na
implementação, levando a uma melhor manutenção a longo prazo.

## Exercício 1: Configurar o ambiente de laboratório

Neste exercício, você configurará o ambiente de desenvolvimento para
criar, testar e implementar os agentes do Copilot, que o ajudarão a
obter assistência de AI personalizada usando o Microsoft 365 Copilot.

### Tarefa 1: Instalar o Agents Toolkit

O **Agents Toolkit for Visual Studio Code** requer o Visual Studio Code.
Neste exercício, você instalará o tolkit no Visual Studio Code.

1.  Abra o **Visual Studio Code** da VM. Selecione **Extensions** no
    menu à esquerda.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image2.png)

2.  Search and select +++Microsoft 365 Agents Toolkit+++ e clique
    em **Install**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image3.png)

3.  Certifique-se de que o toolkit esteja instalado.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

4.  Crie uma nova pasta chamada +++ServiceAgent+++ na sua área de
    trabalho.

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image5.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image6.png)

## Exercício 2: Criar o agente base com TypeSpec usando o Microsoft 365 Agents Toolkit

Neste exercício, você criará um **Agente Declarativo**, o definirá,
atualizará as ações e testará o agente.

### Tarefa 1: Estruturar seu projeto de agente base usando o Microsoft 365 Agents Toolkit

Nesta tarefa, você criará o **Agente Declarativo** com **a definição**
de TypeSpec usando o **Microsoft 365 Agents Toolkit**. Você criará um
agente chamado **RepairServiceAgent**, que interage com os dados de
reparos por meio de um serviço de API existente para ajudar os usuários
a gerenciar registros de reparos de automóveis.

1.  Localize o **ícone do Microsoft 365 Agents Toolkit**
    ![m365atk-icon](./media/image7.png) no menu VS Code à esquerda e
    selecione-o. Uma barra de atividades será aberta. Selecione o botão
    **Create a New Agent/App** na barra de atividades que abrirá a
    paleta com uma lista de modelos de aplicativos disponíveis no
    Microsoft 365 Agents Toolkit.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image8.png)

2.  Escolha **Declarative Agent** na lista de modelos.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image9.png)

3.  Em seguida, selecione **Start with TypeSpec for Microsoft 365
    Copilot** para definir seu agente usando TypeSpec.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

4.  Em seguida, selecione a pasta **ServiceAgent** na área de trabalho.
    Este é o local onde você deseja que o toolkit dos agentes crie a
    estrutura do projeto do agente.

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image11.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image12.png)

5.  Em seguida, insira o nome do aplicativo como
    +++RepairServiceAgent+++ e selecione **Enter** para concluir o
    processo. Você verá uma nova janela do VS Code com o projeto do
    agente pré-carregado.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image13.png)

6.  Você precisará entrar no **Microsoft 365 Agents Toolkit** para
    carregar e testar seu agente de dentro dele.

7.  Na janela do projeto, selecione o **ícone do Microsoft 365 Agents
    Toolkit** ![m365atk-icon](./media/image7.png) novamente no menu do
    lado esquerdo. Isso abrirá a barra de atividades do Kit de
    ferramentas do agente com seções como **Accounts**, **Environment**,
    **Development** etc.

8.  Na seção **Accounts** selecione **Sign in to Microsoft 365**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image14.png)

9.  Isso abrirá uma caixa de diálogo do editor para entrar ou criar uma
    área restrita do desenvolvedor do Microsoft 365 ou Cancelar.
    Selecione **Sign in** e faça login com suas credenciais.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image15.png)

10. Depois de fazer login, **feche** o navegador e volte para a janela
    do projeto.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image16.png)

### Tarefa 2: Definir seu agente

O projeto Declarative Agent, desenvolvido pelo Agents Toolkit, fornece
um modelo que inclui código para conectar um agente à API do GitHub para
exibir problemas do repositório. Neste laboratório, você criará seu
próprio agente que se integra a um serviço de reparo de automóveis,
oferecendo suporte a várias operações para gerenciar dados de reparo.

Na pasta do projeto, você encontrará dois **arquivos** TypeSpec
**main.tsp** e **actions.tsp**. O agente é definido com seus
**metadados**, **instruções** e **recursos** no arquivo **main.tsp**.
Use o arquivo **actions.tsp** para definir **as ações do agente**. Se o
seu agente incluir ações como conectar-se a um serviço de API, esse será
o arquivo em que ele deverá ser definido.

Abra **main.tsp** e inspecione o que está lá no modelo padrão, que você
modificará para o cenário de serviço de reparo do nosso agente.

**Atualizar os metadados e as instruções do agente**

No arquivo **main.tsp** você encontrará a estrutura básica do agente.
Revise o conteúdo fornecido pelo modelo de kit de ferramentas de
agentes, que inclui: -

- **Agent name** e **description** 1️⃣

- **Instructions** básicas 2️⃣

- Código de espaço reservado para **actions **e** capabilities**
  (comentado) 3️⃣

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image17.png)

1.  Identifique os blocos de código **@agent** e **@instructions** (da
    linha 10 a 17).

![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image18.png)

2.  Comece definindo seu agente para o cenário de reparo. Substitua as
    definições de **@agent** e **@instruction** pelo snippet de código
    abaixo.

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

3.  Em seguida, adicione um iniciador de conversa para o agente. Logo
    abaixo das instruções, você verá um código comentado para iniciar
    uma conversa. Substitua o bloco @conversationStarter (devem ser as
    linhas de 22 a 25) pelo código abaixo.

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

### Tarefa 3: Atualizar a ação do agente

In this task, you will define the action for your agent by opening
the **actions.tsp** file. You’ll return to the main.tsp file later to
complete the agent metadata with the action reference, but first, the
action itself must be defined.

The placeholder code in actions.tsp is designed to search for open
issues in a GitHub repository. It serves as a starting point to help
newcomers understand how to define an action for their agent like
action’s metadata, API host url and operations or functions and their
definitions. You will replace all this with repair service.

1.  Open the file **actions.tsp**. Replace the code starting
    with **@service** till **const SERVER_URL** (line numbers should be
    7 to 25) with the below code block.

	Esta atualização introduz os metadados da ação e define a URL do
servidor. Além disso, observe que o namespace foi alterado de GitHubAPI
para RepairsAPI.

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

2.  Em seguida, substitua a operação no código do modelo de searchIssues
    para **listRepairs,** que é uma operação de reparo para obter a
    lista de **repairs**. Substitua todo o bloco de código começando
    logo após a definição SERVER_URL e terminando *antes* das chaves de
    fechamento finais pelo snippet abaixo. Certifique-se de deixar os
    suportes de fechamento intactos. (Os números das linhas devem ser de
    27 a 37)

	```
	/**
	* List repairs from the API 
	* @param assignedTo The user assigned to a repair item.
	*/

	@route("/repairs")
	@get  op listRepairs(@query assignedTo?: string): string;

	```

	![A screenshot of a computer program AI-generated content may be incorrect.](./media/image22.png)

3.  Agora volte para o arquivo **main.tsp** e adicione a ação que você
    acabou de definir no agente. Após os iniciadores da conversa,
    substitua todo o bloco de código pelo trecho abaixo.

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

### Tarefa 4: (Somente leitura) Entenda os elementos

Esta é uma tarefa para entender o que definimos no arquivo TypeSpec.
Basta ler esta tarefa. Nos arquivos TypeSpec main.tsp e actions.tsp,
você encontrará elementos (começando com @), namespaces, models e outras
definições para seu agente.

Confira os detalhes abaixo para entender alguns dos elementos usados
nesses arquivos

- **@agent** - Define o namespace (nome) e a descrição do agente

- **@instructions** - Define as instruções que prescrevem o
  comportamento do agente. 8000 caracteres ou menos

- **@conversationStarter** - Define iniciadores de conversa para o
  agente

- op - Define qualquer operação. Pode ser uma operação para definir os
  recursos do agente, como op GraphicArt, op CodeInterpreter etc., ou
  definir operações de API, como op listRepairs

- **@server** - Define o ponto de extremidade do servidor da API e seu
  nome

- **@capabilities** - Quando usado dentro de uma função, ele define
  cartões adaptáveis simples com pequenas definições, como um cartão de
  confirmação para a operação

### Tarefa 5: Testar seu agente

Nesta tarefa, você testará o Agente do Serviço de Reparo que acabou de
criar.

1.  Selecione o ícone de **extensão Agents Toolkit**, para abrir a barra
    de atividades de dentro do seu projeto.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image24.png)

2.  Na barra de atividades do Agents Toolkit,
    em **LifeCycle** selecione **Provision**. Isso criará o pacote do
    aplicativo que consiste nos arquivos e ícones de manifesto gerados e
    carregará o aplicativo no catálogo apenas para você testar.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image25.png)

3.  Abra seu navegador e vá até
    +++https://m365.cloud.microsoft/chat+++ para abrir o aplicativo
    Copilot.

4.  Selecione o **RepairServiceAgent** na lista de **Agentes**
    disponíveis na interface do Microsoft 365 Copilot. Isso levará um
    tempo e você poderá ver uma mensagem de torradeira mostrando o
    progresso da tarefa a ser provisionada.

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image26.png)

5.  Selecione o início da conversa **List repairs** e envie o prompt.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

6.  Isso inicia a conversa com seu agente e você pode ver a resposta do
    agente com a lista de reparos.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

## Exercício 3: Aprimorar os recursos do agente

Neste exercício, você aprimorará o agente adicionando mais operações,
habilitando respostas com Cartões Adaptáveis e incorporando recursos de
interpretador de código. Vamos explorar cada um desses aprimoramentos
passo a passo. Voltar para o projeto no VS Code.

### Tarefa 1: Modificar o agente para adicionar mais operações

Nesta tarefa, você modificará o agente e adicionará operações
como **createRepair**, **updateRepair** e **deleteRepair.**

1.  Vá para o arquivo **actions.tsp** e copie e cole o trecho abaixo
    logo após a operação **listRepairs** para adicionar essas novas
    operações **createRepair**, **updateRepair** e **deleteRepair**.
    Aqui você também está definindo o modelo de dados Item de reparo.

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

2.  Agora, abra o arquivo **main.tsp** e adicione essas novas operações
    à ação do agente. **Cole** o snippet abaixo depois que a linha **op
    listRepairs for global. ReparosAPI.listRepairs;** dentro do
    namespace **RepairServiceActions**.

	```
	op createRepair is global.RepairsAPI.createRepair;
	op updateRepair is global.RepairsAPI.updateRepair;
	op deleteRepair is global.RepairsAPI.deleteRepair;

	```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image30.png)

3.  Adicione também um novo iniciador de conversa para criar um novo
    item de reparo logo após a definição de início da primeira conversa.

	```
	@conversationStarter(#{
	title: "Create repair",
	text: "Create a new repair titled \"[TO_REPLACE]\" and assign it to me"
	})

	```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image31.png)

### Tarefa 2: Adicionar cartão adaptável à referência de função

Nesta tarefa, você aprimorará os cartões de referência ou cartões de
resposta usando cartões adaptáveis. Vamos pegar a operação
**listRepairs** e adicionar um cartão adaptável para o item de reparo.

1.  Na pasta do projeto, crie uma nova pasta chamada +++cards+++ na
    pasta **appPackage**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image32.png)

2.  Crie um arquivo +++repair.json+++ na pasta **cards** e cole o trecho
    de código como está abaixo no arquivo.

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

3.  Em seguida, volte para o arquivo **actions.tsp** e localize a
    operação **listRepairs**. Substitua a definição de operação **@get
    op listRepairs(@query assignedTo?: string): string;** linha com as 2
    linhas de código abaixo.

	```
	@card(#{ dataPath: "$", title: "$.title",   url: "$.image", file: "cards/repair.json"})
	@get op listRepairs(@query assignedTo?: string): Repair[];

	```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image34.png)

4.  A resposta do cartão acima será enviada pelo agente quando você
    perguntar sobre um item de reparo ou quando o agente trouxer uma
    lista de itens como referência.

5.  Como o agente agora oferece suporte a funcionalidades adicionais,
    atualize as instruções de acordo para refletir esse aprimoramento.

6.  No mesmo arquivo **main.tsp**, atualize a definição de instruções
    para ter diretivas adicionais para o agente. Substitua o bloco **de
    código @instructions** existente pelo bloco de código abaixo.

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

### Tarefa 3: Provisionar e testar o agente

Nesta tarefa, você levará o agente atualizado que agora também é um
analista de reparos para testar.

1.  Selecione o ícone de extensão do Agents Toolkit para abrir sua barra
    de atividades no seu projeto.

2.  Na barra de atividades do kit de ferramentas, em
    **LifeCycle** selecione **Provision** para empacotar e carregar o
    agente recém-atualizado para teste.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image36.png)

3.  Certifique-se que o provisionamento seja bem-sucedido.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image37.png)

4.  Volte para a sessão aberta do **navegador** e faça uma
    **atualização**.

5.  No **RepairServiceAgent**, comece usando o iniciador de conversa
    **Create repair**. Substitua partes do prompt para adicionar um
    título e envie-o para o chat para iniciar a interação. Por exemplo:

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image38.png)

6.  Substitua o **“\[TO REPLACE\]”** por +++rear camera issue+++ e
    **assign it to me**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

7.  A caixa de diálogo de confirmação, se você notar, tem mais metadados
    do que o que você enviou, graças às novas instruções.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png)

8.  Prossiga para adicionar o item clicando em **Confirm** na caixa de
    diálogo.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

9.  O agente responde com o **item criado** mostrado em um **cartão
    adaptável avançado**.

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image42.png)

10. Em seguida, verifique novamente se os cartões de referência
    funcionam. Envie o prompt abaixo na conversa.

	+++List all my repairs+++.

	Selecione **Always allow **na caixa de diálogo de confirmação.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image43.png)

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image44.png)

11. O agente responderá com a lista de reparos atribuídos a você. com
    cada item referenciado com um cartão adaptável. Nesse caso, deve ser
    apenas o problema da câmera traseira que você acabou de adicionar.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

12. Em seguida, você testará a nova capacidade analítica do seu agente.
    Abra um novo chat selecionando o botão **New chat** no canto
    superior direito do seu agente.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

13. Em seguida, copie o prompt abaixo e cole-o na caixa de mensagem e
    pressione Enter para enviá-lo.

14. Classifique os itens de reparo com base no título em três categorias
    distintas: **Routine Maintenance, Critical** e **Low Priority**. Em
    seguida, gere um gráfico exibindo a representação percentual de cada
    categoria.

	![A screenshot of a phone AI-generated content may be
incorrect.](./media/image47.png)

15. Você deve obter alguma resposta semelhante à tela abaixo. Pode
    variar às vezes.

	![A screenshot of a data box AI-generated content may be
incorrect.](./media/image48.png)

**Resumo:**

Neste laboratório, você:

- Usou **TypeSpec** para descrever APIs e vinculá-las às ações do
  Copilot.

- Configurou **Cartões Adaptáveis** para exibir registros de reparo em
  um layout visual avançado.

- Criou um cenário completo em que os usuários possam interagir
  naturalmente com o Copilot para gerenciar dados de reparo.

Este laboratório demonstrou como os Agentes Declarativos aproveitam a
**orquestração, os modelos de base e os controles de segurança da
plataforma Copilot** para oferecer uma experiência de usuário familiar e
consistente, integrando-se a dados e fluxos de trabalho de negócios
personalizados. 
