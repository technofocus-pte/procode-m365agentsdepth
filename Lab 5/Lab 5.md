# Laboratório 5 – Crie um agente de varejo no Copilot Studio que aproveite o Azure AI Search e traga seu próprio modelo para seus prompts

Duração do laboratório – 60 minutos

## Objetivo

Em um site de loja de varejo, os clientes frequentemente perguntam sobre
especificações do produto, termos de garantia ou guias de solução de
problemas. Os chatbots estáticos de perguntas frequentes não podem
cobrir todas as variações.

Para ajudar nesse cenário, o seguinte será implementado neste
laboratório:

- Manuais de produtos, documentos de garantia e PDFs de perguntas
  frequentes serão indexados no **Azure AI Search**.

- Um agente do Copilot Studio que recupera o snippet correto quando um
  cliente faz uma pergunta sobre os produtos.

- O agente que fornece uma resposta em linguagem natural, além de um
  link para o manual do produto relevante.

Isso proporciona uma carga reduzida de central de atendimento, suporte
ao cliente 24 horas por dia, 7 dias por semana e maior satisfação do
cliente.

Também aprenderemos como trazer seu próprio modelo do Azure AI Foundry
para o Copilot Studio.

## Exercício 1: Criar um recurso do Azure AI Search

Neste exercício, primeiro criaremos um recurso do Azure AI Search, que
será usado para pesquisar os documentos.

1.  Na página inicial do portal do Azure, selecione **Azure AI
    Foundry.**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image1.png)

2.  Na página **AI Foundry**, selecione **AI Search** no painel esquerdo
    e selecione **+ Create**.

    ![A screenshot of a search engine AI-generated content may be
incorrect.](./media/image2.png)

3.  Insira os detalhes abaixo e selecione **Review + create**.

    - Subscription – Selecione sua **assinatura atribuída**

    - Resource group – Selecione seu **grupo de recursos atribuído**
    (**ResourceGroup1**)

    - Service name – +++ **documentstore53853922@lab.labinstanceid()**+++

    - Location – Selecione sua **região atribuída**

    ![](./media/image3.png)

4.  Depois que a validação for aprovada, selecione **Create**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

5.  A implementação leva alguns minutos. Selecione **Go to resource**
    quando o serviço de pesquisa for criado.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image5.png)

6.  Na página **Overview**, copie o valor da URL e salve-o em um bloco
    de notas para ser usado em um exercício futuro.

    ![](./media/image6.png)

7.  Selecione **Keys** em **Settings** no painel esquerdo. Copie a
    **Primary admin key** e salve em um bloco de notas para usá-la nos
    próximos exercícios.

    ![](./media/image7.png)

8.  Selecione **Identity** em **Settings** no painel esquerdo.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image8.png)

9.  Alterne o Status para **On** em **System assigned** e clique em
    **Save**.

    ![A screenshot of a computer screen AI-generated content may be
incorrect.](./media/image9.png)

10. Selecione **Yes** na caixa de diálogo de confirmação **Enable system
    assigned managed identity**. Essa configuração permitirá que o
    serviço de pesquisa seja listado nos recursos de identidade
    gerenciada, que podem receber funções conforme necessário.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

## Exercício 2: Criar uma conta de armazenamento

Este exercício é para criar uma conta de armazenamento com o
Armazenamento de Blobs e carregar os documentos necessários para dar
suporte aos clientes de varejo nela.

1.  Na página inicial do portal do Azure,
    (+++https://portal.azure.com/+++), selecione **Storage accounts**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image11.png)

2.  Selecione **+ Create** para criar uma nova conta de armazenamento.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image12.png)

3.  Insira os detalhes abaixo, aceite os valores padrão nos outros
    campos e clique em **Review + create**.

    - Subscription – Selecione sua **assinatura atribuída**

    - Resource group – Selecione seu **grupo de recursos atribuído**
    (**ResourceGroup1**)

    - Region – Selecione sua **região atribuída**

    - Storage account name – +++ **docstore@lab.LabInstanceId()**+++

    - Primary service – Selecione **Azure Blob Storage or Azure Data Lake
    Storage Gen 2**

    ![A screenshot of a computer AI-generated content may be incorrect.](./media/image13.png)

4.  Assim que a validação for aprovada, clique em **Create**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image14.png)

5.  Assim que a criação do recurso for bem-sucedida, clique em **Go to
    resource**

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image15.png)

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image16.png)

6.  Selecione **Containers** em **Data storage**. Selecione **+ Add
    container**, insira o nome como +++**documents**+++ e clique em
    **Create** para criar o contêiner.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image17.png)

7.  Selecione **documents** para carregar o documento de política de
    licença nele.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image18.png)

8.  Clique em **Upload** e, em seguida, selecione **Browse for files**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image19.png)

9.  Selecione **documents** na pasta **C:\LabFiles\AISearch** e, em
    seguida, clique em **Upload**

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image20.png)

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image21.png)

10. Navegue até a conta de armazenamento
    **<docstore@lab.LabInstanceId()>** (selecione **Storageaccounts** na
    **página inicial** do portal do Azure e selecione
    **docstore@lab.LabInstanceId()**) e selecione **Access Control
    (IAM)** no painel esquerdo. Selecione **Add -\> Add role
    assignment**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image22.png)

11. Busque +++**Storage Blob Data Reader**+++, selecione-o e clique em
    **Next**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image23.png)

12. Clique em **+Select members**, pesquise e selecione seu **ID de
    usuário**, selecione seu **ID de usuário** listado e clique em
    **Select**. Isso adiciona a função Leitor de Dados do Blob de
    Armazenamento ao seu ID de usuário.

    ![A screenshot of a group of people AI-generated content may be
incorrect.](./media/image24.png)

13. Selecione **Managed identity** e, em seguida, selecione **+ Select
    members**. Selecione **Search service** em **Managed identity** e
    selecione o serviço de pesquisa **searchleaves** que é listado.

    ![](./media/image25.png)

14. Clique em **Select** para selecionar o serviço de pesquisa.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image26.png)

15. De volta à tela **Add role assignment**, clique em **Review +
    assign**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

16. Selecione **Review + assign** novamente na próxima tela.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

17. Prossiga para a próxima etapa depois que as funções forem
    adicionadas.

    ![](./media/image29.png)

    Neste exercício, criamos uma conta de armazenamento e adicionamos os
documentos e as permissões de função necessárias a ela.

## Exercício 3: Criar um serviço OpenAI do Azure e implementar um modelo 

O serviço AI Search terá que vetorizar os dados carregados, a fim de
realizar a pesquisa sobre os documentos. Para vetorizar os dados, um
modelo de incorporação precisa ser implantado. Neste exercício, você
criará um Azure OpenAI Service e implementará o modelo de inserção de
texto nele.

1.  Na página inicial do portal do Azure, pesquise e selecione +++Azure
    OpenAI++.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

2.  Selecione **+ Create**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image31.png)

3.  Insira os detalhes abaixo e selecione **Next**.

    - Subscription – Selecione sua **assinatura atribuída**

    - Resource group – Selecione seu **grupo de recursos atribuído**
    (**ResourceGroup1**)

    - Region – Selecione sua **região atribuída**

    - Name – +++**openaiservice52374668**+++

    - Pricing tier – Selecione **Standard**

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image32.png)

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image33.png)

4.  Selecionet **Next** nas próximas duas telas, selecione **Create** na
    tela **Review + submit**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image34.png)

5.  Clique em **Go to resource** depois que o serviço for criado.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image35.png)

6.  Selecione **Access control (IAM)** no painel esquerdo, selecione **+
    Add -> Add role assignment**

    ![](./media/image36.png)

7.  Busque por +++**Cognitive Services OpenAI User**+++, selecione a
    função e clique em **Next**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image37.png)

8.  Selecione **+ Select members**, pesquise seu **ID de usuário**,
    selecione-o e clique em **Select**

    ![](./media/image38.png)

9.  De volta à tela **Add role assignment**, selecione **Managed
    identity**. Em seguida, selecione **+ Select members**. Na tela
    **Select managed identities**, selecione **Search service** em
    **Managed identity** e selecione o serviço
    **documentstore@lab.LabInstanceId()**

    ![](./media/image39.png)

10. Uma vez selecionado, clique em **Select**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png)

11. Selecione **Review + assign** nas próximas duas telas.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

12. Aguarde uma **mensagem** **de sucesso** nas adições de função antes
    de prosseguir com as próximas tarefas.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image42.png)

13. Da página **Overview** do recurso Azure OpenAI Service, selecione
    **Go to Azure AI Foundry portal** para abrir o Azure OpenAI Service
    e implementar um modelo.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image43.png)

14. Selecione **Deployments** no painel esquerdo. Selecione **+ Deploy
    model** -> **From base models**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image44.png)

15. Procure por +++**text-embedding**+++, selecione
    **text-embedding-3-large** e, em seguida, selecione **Confirm**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

16. Selecione **Deploy** em **Deploy text-embedding-3-large**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

17. O modelo é implementado e a tela é carregada com os detalhes da
    implementação.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image47.png)

## Exercício 4: Criar um índice de vetor

O recurso AI Search precisa de um índice vetor para realizar a pesquisa
vetorial. Você vetorizará os dados carregados neste exercício.

1.  No portal do Azure, vá ao **documentstore@lab.LabInstanceId()**, AI
    Search service resource. Selecione **Import and vectorize data**

    ![](./media/image48.png)

2.  Selecione a opção **Azure Blob Storage**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image49.png)

3.  Selecione a opção **RAG** na tela **What scenarios are you
    targeting?**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image50.png)

4.  Insira os detalhes abaixo, aceite os outros valores como padrão e
    clique em **Next**.

    - Subscription – Selecione sua **assinatura atribuída**

    - Storage account- Selecione **docstore@lab@LabInstanceId()**

    - Blob-container – Selecione **documents**

    ![](./media/image51.png)

5.  Na tela **Vectorize your text**, a assinatura é pré-preenchida.
    Insira os detalhes abaixo e clique em **Next**.

    - Azure OpenAI resource – Selecione
    **openaiservice@lab.LabInstanceId()**

    - Model deployment – Selecione **text-embedding-3-large**

    - Authentication type – Selecione **System assigned identity**

    - Marque a caixa de seleção para confirmar o alerta de custo do Azure
    OpenAI.

    ![A screenshot of a computer AI-generated content may be incorrect.](./media/image52.png)

6.  Selecione **Next** na tela **Vectorize and enrich your images** já
    que não estamos lidando com imagens aqui e selecione **Next** na
    tela **Advanced settings** também.

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image53.png)

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image54.png)

7.  Selecione **Create** na tela **Review + create**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image55.png)

8.  Clique em **Close** na caixa de diálogo de sucesso.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image56.png)

## Exercício 5: Criar um agente assistente de varejo

Neste exercício, você criará um agente assistente de varejo no Copilot
Studio.

1.  Faça login em +++https://copilotstudio.microsoft.com+++ usando suas
    credenciais de login.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image57.png)

2.  Selecione **Create** no painel esquerdo.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image58.png)

3.  Selecione **+ New agent** para criar um novo agente.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image59.png)

4.  Insira +++You are a Retail assistant agent for customers HR who will
    answer questions related to the store products+++ e selecione
    **Send**

    ![](./media/image60.png)

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image61.png)

5.  Depois que o agente for criado, no painel **Test**, insira +++What
    is the warranty period for Washing machine?+++ e clique em **Send.**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image62.png)

6.  Ele dá uma resposta generalizada como na captura de tela abaixo.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image63.png)

## Exercício 6: Adicionar o Azure AI Search como uma fonte de conhecimento

Neste exercício, você adicionará o Azure AI Search criado no portal do
Azure, como uma fonte de conhecimento para o agente de assistência de
varejo no Copilot Studio.

1.  Da página **Overview** do agente, selecione **+ Add knowledge**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image64.png)

2.  Selecione **Azure AI Search** da lista de fontes de conhecimento
    disponíveis.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image65.png)

3.  Clique no **menu suspenso** ao lado de **Not connected** na próxima
    tela e selecione **Create new connection**

    ![A screenshot of a search engine AI-generated content may be
incorrect.](./media/image66.png)

4.  Insira a URL do **endpoint** e os valores da **Admin key** que
    salvamos em um bloco de notas em um exercício anterior e clique em
    **Create** para criar a conexão.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image67.png)

5.  Depois que a conexão for estabelecida, o índice disponível será
    listado e já selecionado. Clique em **Add to agent**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image68.png)

6.  O serviço AI Search é adicionado como uma fonte de conhecimento ao
    agente e está no estado **Ready** agora.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image69.png)

7.  Agora, vamos testar o agente com a mesma pergunta que tentamos
    antes.

8.  No painel **Test**, insira +++ What is the warranty period for
    Washing machine?+++ e clique em **Send.**

    ![](./media/image70.png)

9.  Você pode ver que a resposta do agente agora é do documento
    carregado no serviço AI Search.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image71.png)

## Exercício 7: Implantar um modelo no Azure AI Foundry

Neste exercício, você implantará um modelo no Azure AI Foundry para
usá-lo no Copilot Studio (no próximo exercício).

1.  Abrir o recurso Azure AI Foundry Azure OpenAI criado anteriormente.

2.  No painel esquerdo, selecione **Deployments**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image72.png)

3.  Selecione o menu suspenso ao lado de **+ Deploy model** e selecione
    **Deploy base model**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image73.png)

4.  Selecione **gpt-4o** e clique em **Confirm**

    ![](./media/image74.png)

5.  Na caixa de diálogo **Deploy gpt-4o**, insira o **Deployment name**
    como +++**ModelforMCS**+++, aceite os outros padrões e selecione
    **Deploy**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image75.png)

6.  Copie o **Target URI** e os valores de **Key** para um bloco de
    notas a ser usado durante a criação da conexão do Copilot Studio.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image76.png)

Agora que o modelo está implantado, você pode usá-lo no prompt do agente
do Copilot Studio.

## Exercício 8: Criar um prompt no Copilot Studio e usar o modelo criado no Azure AI Foundry

Neste exercício, você aprenderá a trazer o modelo implantado do Azure AI
Foundry no Copilot Studio. Aqui, estamos usando um modelo base que é
implantado. Também podemos criar um modelo ajustado de acordo com os
requisitos de negócios e usá-lo no Copilot Studio.

1.  No agente do Copilot Studio, selecione **Tools** na barra de menus
    superior.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image77.png)

2.  Selecione **+ New tool** Para adicionar uma nova ferramenta ao
    agente.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image78.png)

3.  Selecione **Prompt**, pois vamos adicionar um novo prompt.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image79.png)

4.  Na tela **Custom prompt**, selecione o menu suspenso ao lado do
    **nome** do modelo.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image80.png)

5.  Selecione **+** em **Azure AI Foundry Models** para adicionar o
    modelo implementado no Azure AI Foundry e selecione **Connect a new
    model**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image81.png)

    ![A screenshot of a computer AI-generated content may be incorrect.](./media/image82.png)

6.  Insira os detalhes abaixo e clique em **Connect**

    - Model deployment name - +++ModelforMCS+++

    - Base model name - +++gpt-4o+++

    - Azure model endpoint URL – Insira o **Target url** salvo anteriormente

    - API Key – Insira a **API key** do modelo salva anteriormente.

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image83.png)

    ![A screen shot of a computer AI-generated content may be
    incorrect.](./media/image84.png)

7.  Uma vez conectado, selecione **Close**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image85.png)

8.  Você pode ver que o modelo ModelforMCS está selecionado agora.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image86.png)

9.  Renomeie o prompt para +++ +WM Types +++. Digite +++ What are the
    different types of Washing Machines? +++ e selecione **Test**.

    ![](./media/image87.png)

10. Selecione **Save** para salvar o prompt.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image88.png)

11. Selecione a opção **Add to agent** Para adicionar o prompt ao
    agente.

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image89.png)

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image90.png)

    Com esse recurso, podemos ajustar o modelo no Azure AI Foundry e usá-lo
no Copilot Studio com facilidade. Podemos trazer o vasto ecossistema dos
modelos no Azure AI Foundry facilmente para o Copilot Studio.

## Resumo

Neste laboratório, aprendemos a conectar o agente do Copilot Studio a um
serviço do Azure AI Search como uma fonte de conhecimento e testar o
agente com base na fonte. Também aprendemos a trazer o modelo implantado
no Azure AI Foundry para o Copilot Studio.
