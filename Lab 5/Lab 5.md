# Lab 5 - Create a Retail agent in Copilot Studio that leverages Azure AI Search and Bring your own model for your prompts

Lab duration – 60 minutes

## Objective

In a retail store site, customers frequently ask about product
specifications, warranty terms, or troubleshooting guides. Static FAQ
chatbots can’t cover all variations.

To help this scenario, the following will be implemented in this lab

- Product manuals, warranty documents, and FAQ PDFs are indexed into
  **Azure AI Search**.

- A Copilot Studio agent retrieves the right snippet when a customer
  asks a question regarding the products.

- The agent gives a natural-language answer plus a link to the relevant
  product manual.

This gives a reduced call-center load, 24/7 customer support and a
higher customer satisfaction.

We will also learn how to bring your own model from Azure AI Foundry
into the Copilot Studio.

## Exercise 1: Create an Azure AI Search resource

In this exercise, we will first create an Azure AI Search resource,
which will be used to search through the documents.

1. Open a browser, navigate to +++https://portal.azure.com+++ and login using the credentials from the **Resources** tab.
   
1.  From the Home page of the Azure portal, select **Foundry.**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/im21.png)

2.  In the **AI Foundry page**, select **AI Search** from the left pane
    and then select **+ Create**.

    ![A screenshot of a search engine AI-generated content may be
incorrect.](./media/image2.png)

3.  Enter the below details and select **Review + create**.

    - Subscription – Select your **assigned subscription**
    
    - Resource group – Select your **assigned Resource group**
      (**ResourceGroup1**)
    
    - Service name – +++**documentstore@lab.labinstance.id**+++
    
    - Location – Select your nearest region
    
    ![](./media/image3.png)

4.  Once the validation passes, select **Create**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

5.  The deployment takes a few minutes. Select **Go to resource** once
    the search service is created.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image5.png)

6.  From the **Overview** page, copy the Url value and save it in a
    notepad to be used in a future exercise.

    ![](./media/image6.png)

7.  Select **Keys** under **Settings** from the left pane. Copy the
    **Primary admin key** and save it in a notepad for using it in the
    upcoming exercises.

    ![](./media/image7.png)

8.  Select **Identity** under **Settings** from the left pane.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image8.png)

9.  Toggle the Status to **On** under **System assigned** and then click
    on **Save**.

    ![A screenshot of a computer screen AI-generated content may be
incorrect.](./media/image9.png)

10. Select **Yes** in the **Enable system assigned managed identity**
    confirmation dialog. This setting will enable the search service to
    be listed under the managed identity resources, which can then be
    assigned roles as required.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

## Exercise 2: Create a Storage account

This exercise is to create a storage account with Blob storage and
upload the documents required supporting the retail customers in it.

1.  From the Home page of the Azure portal,
    (+++https://portal.azure.com/+++), select **Storage accounts**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image11.png)

2.  Select **+ Create** to create a new Storage account.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image12.png)

3.  Enter the below details, accept the default values in the other
    fields and click on **Review + create**.

    - Subscription – Select your **assigned subscription**
    
    - Resource group – Select your **assigned Resource group**
      (**ResourceGroup1**)
    
    - Region – Select your **assigned region**
    
    - Storage account name – +++**docstore@lab.labinstance.id**+++
    
    - Primary service – Select **Azure Blob Storage or Azure Data Lake
      Storage Gen 2**

    ![A screenshot of a computer AI-generated content may be incorrect.](./media/image13.png)

4.  Once the validation passes, click on **Create**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image14.png)

5.  Once the resource creation succeeds, click on **Go to resource**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image15.png)

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image16.png)

6.  Select **Containers** under **Data storage**. Select **+
    Container**, enter the name as +++**documents**+++ and click on
    **Create** to create the container.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image17.png)

7.  Select the created container **documents** to upload the leave
    policy document into it.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image18.png)

8.  Click on **Upload** and then select **Browse for files**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image19.png)

9.  Select the **documents** from **C:\LabFiles\AISearch** folder and
    then click on **Upload**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image20.png)

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image21.png)

10. Navigate to the **docstoreXXXXXXX** Storage account
    (Select **Storageaccounts** from the **Home page** of the Azure
    portal and select the resource that starts with **docstore**) and select
    **Access Control (IAM)** from the left pane. Select **Add -\> Add
    role assignment**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image22.png)

11. Search for +++**Storage Blob Data Reader**+++, select it and click
    on **Next**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image23.png)

12. Click on **+Select members**, search for and select your **user
    id**, select your **user id** that gets listed and then click on
    **Select**. This adds the Storage Blob Data Reader role to your user
    id.

    ![A screenshot of a group of people AI-generated content may be
incorrect.](./media/image24.png)

13. Select **Managed identity** and then select **+ Select members**.
    Select **Search service** under **Managed identity** and select the
    **searchleaves** search service that gets listed.

    ![](./media/image25.png)

14. Click on **Select** to select the search service.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image26.png)

15. Back in the Add role assignment screen, click on **Review +
    assign**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

16. Select **Review + assign** again in the next screen.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

17. Proceed to the next step once the roles are added.

    ![](./media/image29.png)

In this exercise, we have created a Storage account and added the
documents and required Role permissions to it.

## Exercise 3: Create an Azure OpenAI Service and deploy a model 

The AI Search service will have to vectorize the data uploaded, in order
to perform the search over the documents. To vectorize the data, an
embedding model needs to be deployed. In this exercise, you will create
an Azure OpenAI Service and deploy the text-embedding model in it.

1.  From the Azure portal Home page, search for select +++Azure OpenAI+++.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

2.  Select **+ Create -> Azure OpenAI**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/im22.png)

3.  Enter the below details and select **Next**.

    - Subscription – Select your **assigned subscription**
    
    - Resource group – Select your **assigned Resource group**
      (**ResourceGroup1**)
    
    - Region – Select your **assigned region**
    
    - Name – +++**openaiservice@lab.labinstance.id**+++ 
    
    - Pricing tier – Select **Standard**
    
    ![A screenshot of a computer AI-generated content may be incorrect.](./media/image32.png)
    
    ![A screenshot of a computer AI-generated content may be incorrect.](./media/image33.png)

4.  Select **Next** in the next 2 screens select **Create** in the
    **Review + submit** screen.

    ![A screenshot of a computer AI-generated content may be incorrect.](./media/image34.png)

5.  Click on **Go to resource** once the service is created.

    ![A screenshot of a computer AI-generated content may be incorrect.](./media/image35.png)

6.  Select **Access control (IAM)** from the left pane, select **Add -\>
    Add role assignment**.

    ![](./media/image36.png)

7.  Search for +++**Cognitive Services OpenAI User**+++, select the role
    and click on **Next**.

    ![A screenshot of a computer AI-generated content may be incorrect.](./media/image37.png)

8.  Select **+ Select members**, search for your **user id**, select it
    and click on **Select**.

    ![](./media/image38.png)

9.  Back in the **Add role assignment** screen, select **Managed
    identity**. Then select **+ Select members**. In the **Select
    managed identities** screen, select **Search service** under
    **Managed identity** and select the resource that starts with **documentstore** service.

    ![](./media/image39.png)

10. Once selected, click on **Select**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png)

11. Select Review + assign in the next 2 screens.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

12. Wait for a **success** message on the role additions before
    proceeding with the next tasks.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image42.png)

13. From the **Overview** page of the Azure OpenAI Service resource,
    select **Go to Azure AI Foundry portal** to open the Azure OpenAI
    Service there and deploy a model.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image43.png)

14. Select **Deployments** from the left pane. Select **+ Deploy model**
    -\> **From base models**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image44.png)

15. Search for +++**text-embedding**+++, select
    **text-embedding-3-large** and then select **Confirm**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

16. Select **Deploy** in the Deploy text-embedding-3-large.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

17. The model gets deployed and the screen is loaded with the deployment
    details.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image47.png)

## Exercise 4: Create a vector index

The AI Search resource needs a Vector index to perform the vector
search. You will vectorize the uploaded data in this exercise.

1.  From the Azure portal, go to the AI Search service resource that starts with
    **documentstore**.
    Select **Import and vectorize data**.

    ![](./media/image48.png)

2.  Select the **Azure Blob Storage** option.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image49.png)

3.  Select the **RAG** option in the **What scenarios are you
    targeting?** screen.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image50.png)

4.  Enter the below details, accept the other values as default and
    click **Next**.

    - Subscription – Select your **assigned subscription**
    
    - Storage account- Select the account that starts with **docstore**
    
    - Blob-container – Select **documents**
    
    ![](./media/image51.png)

5.  In the Vectorize your text screen, the subscription is
    pre-populated. Enter the below details and click **Next**.

    - Azure OpenAI resource – Select **openaiserviceXXXXXX**
    
    - Model deployment – Select **text-embedding-3-large**
    
    - Authentication type – Select **System assigned identity**
    
    - Select the checkbox to acknowledge the cost alert of Azure OpenAI.
    
    ![A screenshot of a computer AI-generated content may be incorrect.](./media/image52.png)

6.  Select Next in the **Vectorize and enrich your images** screen since
    we are not dealing with images here and select **Next** in the
    **Advanced settings** screen as well.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image53.png)

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image54.png)

7.  Select **Create** in the **Review + create** screen.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image55.png)

8.  Click on **Close** in the success dialog box.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image56.png)

## Exercise 5: Create a retail assistant agent

In this exercise, you will create a retail assistant agent in Copilot
Studio.

1.  Login to +++https://copilotstudio.microsoft.com+++ using your login
    credentials.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image57.png)

2.  Select **Create** from the left pane.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image58.png)

3.  Select **+ New agent** to create a new agent.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image59.png)

4.  Enter +++You are a Retail assistant agent for customers HR who will
    answer questions related to the store products+++ and select
    **Send**.

    ![](./media/image60.png)

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image61.png)

5.  Once the agent is created, in the Test pane, enter +++What is the
    warranty period for Washing machine?+++ and click **Send.**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image62.png)

6.  It gives a generalized reply as in the screenshot below.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image63.png)

## Exercise 6: Add the Azure AI Search as a knowledge source

In this exercise, you will add the Azure AI Search that you created from
the Azure portal, as a knowledge source to the Retail assistance agent
in Copilot Studio.

1.  From the **Overview** page of the agent, select **+ Add knowledge**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image64.png)

2.  Select **Azure AI Search** from the list of knowledge sources
    available.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image65.png)

3.  Click on the **drop down** next to **Not connected** in the next
    screen and select **Create new connection**.

    ![A screenshot of a search engine AI-generated content may be
incorrect.](./media/image66.png)

4.  Enter the **Endpoint url** and the **Admin key** values which we
    saved to a notepad in a previous exercise and then click on
    **Create** to create the connection.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image67.png)

5.  Once the connection is established, the available index is listed
    and already selected. Click on **Add to agent**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image68.png)

6.  The AI Search service is added as a knowledge source to the agent
    and is in **Ready** state now.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image69.png)

7.  Now, let us test the agent with the same question we have tried
    before.

8.  In the Test pane, enter +++ What is the warranty period for Washing
    machine?+++ and click **Send.**

    ![](./media/image70.png)

9.  You can see that the response from the agent now is from the
    document uploaded in the AI Search service.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image71.png)

## Exercise 7: Deploy a Model in Azure AI Foundry

In this exercise, you will deploy a model in the Azure AI Foundry to use
it in the Copilot Studio (in the next exercise).

1.  Open the Azure AI Foundry Azure OpenAI resource created earlier.

2.  From the left pane, select **Deployments**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image72.png)

3.  Select the drop down next to the **+ Deploy model** and select
    **Deploy base model**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image73.png)

4.  Select **gpt-4o** and select **Confirm**.

    ![](./media/image74.png)

5.  In the Deploy gpt-4o dialog, enter the **Deployment name** as
    +++**ModelforMCS**+++, accept the other defaults and select
    **Deploy.**

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image75.png)

6.  Copy the Target URI and key values to a notepad to be used during
    the connection creation from the Copilot Studio.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image76.png)

Now that the model is deployed, you can use it in Copilot Studio’s agent
prompt.

## Exercise 8: Create a prompt in the Copilot Studio and use the model created in Azure AI Foundry

In this exercise, you will learn how to bring the deployed model from
Azure AI Foundry in the Copilot Studio. Here, we are using a base model
that is deployed. We can also create a fine tuned model as per the
business requirements and then use it in Copilot Studio.

1.  From the Copilot Studio agent, select **Tools** from the top menu
    bar.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image77.png)

2.  Select **+ New tool** to add a new tool to the agent

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image78.png)

3.  Select Prompt since we are going to add a new prompt.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image79.png)

4.  In the Custom prompt screen, select the drop down next to the
    **model** name.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image80.png)

5.  Select + against **Azure AI Foundry Models** to add the model
    deployed in Azure AI Foundry and select **Connect a new model**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image81.png)

    ![A screenshot of a computer AI-generated content may be incorrect.](./media/image82.png)

6.  Enter the below details and click on Connect.

    - Model deployment name - +++ModelforMCS+++
    
    - Base model name - +++gpt-4o+++
    
    - Azure model endpoint URL – Enter the target url saved earlier
    
    - API Key – Enter the model API key saved earlier.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image83.png)

    ![A screen shot of a computer AI-generated content may be
incorrect.](./media/image84.png)

7.  Once connected, select **Close**.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image85.png)

8.  You can see that the model ModelforMCS is selected now

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image86.png)

9.  Rename the prompt to +++WM Types+++. Enter +++What are the different
    types of Washing Machines?+++ and select **Test**.

    ![](./media/image87.png)

10. Select **Save** to save the prompt.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image88.png)

11. Select the **Add to agent** option to add the prompt to the agent.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image89.png)

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image90.png)

With this feature, we can fine-tune the model in Azure AI Foundry and
use it in Copilot Studio with ease. We can bring in the vast ecosystem
of the models in the Azure AI Foundry easily into the Copilot Studio.

## Summary

In this lab, we have learnt to connect the agent from the Copilot Studio
to an Azure AI Search service as a knowledge source and test the agent
based on the source. We have also learnt to bring the model deployed in
Azure AI Foundry into the Copilot Studio.
