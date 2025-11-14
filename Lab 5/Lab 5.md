# 실습 - Copilot Studio에서 Azure AI Search와 맞춤 모델을 활용한 리테일 에이전트 생성

**실습 소요 시간:** 60분

## 목표

리테일 매장 사이트에서는 고객들이 제품 사양, 보증 조건, 문제 해결 가이드
등에 대해 자주 문의합니다. 기존의 정적 FAQ 챗봇은 모든 변형을 처리할 수
없습니다.

이번 실습에서는 다음을 구현합니다:

- 제품 매뉴얼, 보증 문서, FAQ PDF를 **Azure AI Search**에 색인화

- Copilot Studio 에이전트가 고객 질문에 맞는 정보를 검색하고

- 자연어 답변과 관련 제품 매뉴얼 링크 제공

이를 통해 콜센터 부하 감소, 연중무휴 고객 지원 및 고객 만족도 향상을
달성할 수 있습니다.

또한 Azure AI Foundry에서 제공되는 맞춤 모델을 Copilot Studio에 연결하는
방법도 배웁니다.

## 연습 1: Azure AI Search 리소스 생성

이번 연습에서는 먼저 문서를 검색할 Azure AI Search 리소스를 생성합니다.

1.  Azure 포털 홈 페이지에서 **Azure AI Foundry**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image1.png)

2.  **AI Foundry 페이지**에서 왼쪽 메뉴의 **AI Search**를 선택한 후, **+
    Create**를 클릭하세요.

    ![A screenshot of a search engine AI-generated content may be
incorrect.](./media/image2.png)

3.  다음 세부 정보를 입력한 뒤, **Review + create**를 선택하세요.

    - Subscription –**assigned subscription** 선택

    - Resource group – **assigned Resource group** (**ResourceGroup1**) 선택

    - Service name – +++ **documentstore53853922@lab.labinstanceid()**+++

    - Location – 사용자의 **assigned region** 선택

    ![](./media/image3.png)

4.  검증이 완료되면 **Create**을 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

5.  배포가 완료되면 몇 분 정도 소요됩니다. 검색 서비스가 생성되면 **Go
    to resource**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image5.png)

6.  **Overview** 페이지에서 Url 값을 복사하고, 이후 실습에서 사용할 수
    있도록 메모장에 저장하세요.

    ![](./media/image6.png)

7.  왼쪽 패널의 **Settings**에서 **Keys**를 선택하세요. **Primary admin
    key**를 복사하고, 이후 실습에서 사용할 수 있도록 메모장에
    저장하세요.

    ![](./media/image7.png)

8.  왼쪽 패널의**Settings**에서 **Identity**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image8.png)

9.  **System assigned** 아래의 Status를 **On**으로 전환한 후 **Save**를
    클릭하세요.

    ![A screenshot of a computer screen AI-generated content may be
incorrect.](./media/image9.png)

10. **Enable system assigned managed identity** 확인 창에서 **Yes**를
    선택하세요. 이 설정을 통해 검색 서비스가 관리형 ID 리소스로
    등록되며, 필요에 따라 역할을 할당할 수 있습니다.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

## 연습 2: 스토리지 계정 생성

이 연습에서는 Blob 스토리지가 포함된 스토리지 계정을 생성하고, 리테일
고객 지원에 필요한 문서들을 업로드합니다.

1.  Azure 포털(+++https://portal.azure.com/+++) 홈 페이지에서 **Storage
    accounts**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image11.png)

2.  **+ Create**를 선택해 새 스토리지 계정을 생성하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image12.png)

3.  아래 세부 정보를 입력하고, 다른 필드는 기본값으로 두며 **Review +
    create**를 클릭하세요.

    - Subscription – **할당된 subscription**을 선택

    - Resource group – 할당된 **Resource group** (**ResourceGroup1**)을 선택

    - Region – 할당된 **region**을 선택

    - Storage account name – +++ **docstore@lab.LabInstanceId()**+++

    - Primary service –**Azure Blob Storage or Azure Data Lake Storage Gen
    2** 선택

    ![A screenshot of a computer AI-generated content may be incorrect.](./media/image13.png)

4.  검증이 완료되면 **Create** 버튼을 클릭하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image14.png)

5.  리소스 생성이 완료되면 **Go to resource** 버튼을 클릭하세요.

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image15.png)

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image16.png)

6.  **Data storage**에서**Containers**를 선택하세요. **+ Container** 를
    클릭하고 이름을 +++**documents**+++로 입력한 뒤, **Create**을 클릭해
    컨테이너를 생성하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image17.png)

7.  생성한 **documents** 컨테이너를 선택하여 휴가 정책 문서를
    업로드하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image18.png)

8.  **Upload**를 클릭한 후 **Browse for files**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image19.png)

9.  **C:\LabFiles\AISearch** 폴더에서 **documents**를 선택한 후
    **Upload**를 클릭하세요.

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image20.png)

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image21.png)

10. Azure 포털 **홈페이지**에서 **Storageaccounts**를 선택한 후
    **<docstore@lab.LabInstanceId()>** 스토리지 계정으로 이동하세요.
    왼쪽 창에서 **Access Control (IAM)**을 선택하고, **Add -\> Add role
    assignment**를 클릭하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image22.png)

11. +++**Storage Blob Data Reader**+++ 역할을 검색하고 선택한 뒤,
    **Next**를 클릭하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image23.png)

12. **+Select members**를 클릭하고, **user id**를 검색해 선택하세요.
    목록에 나타난 **user id**를 선택한 뒤 **Select**를 클릭하세요.
    이렇게 하면 사용자 ID에 Storage Blob Data Reader 역할이 할당됩니다.

    ![A screenshot of a group of people AI-generated content may be
incorrect.](./media/image24.png)

13. **Managed identity**를 선택한 후 **+ Select members**를 클릭하세요.
    **Managed identity** 목록에서 **Search service**를 찾아 선택하고,
    표시되는 **searchleaves** 검색 서비스를 선택하세요.

    ![](./media/image25.png)

14. **Select**를 클릭해 검색 서비스를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image26.png)

15. Add role assignment 화면에서 **Review + assign**을 클릭하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

16. 다음 화면에서도 **Review + assign**를 다시 클릭하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

17. 역할이 추가되면 다음 단계로 진행하세요.

    ![](./media/image29.png)

이번 연습에서는 스토리지 계정을 생성하고, 필요한 문서와 역할 권한(Role
permissions)을 추가했습니다.

## 연습 3: Azure OpenAI 서비스 생성 및 모델 배포 

AI Search 서비스가 업로드된 데이터를 검색할 수 있도록
벡터화(vectorize)하려면 임베딩(embedding) 모델이 필요합니다. 이번
연습에서는 Azure OpenAI 서비스를 생성하고 text-embedding 모델을
배포합니다.

1.  Azure Portal 홈페이지에서 +++Azure OpenAI++를 검색하고 선택하세뇨.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

2.  **+ Create**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image31.png)

3.  아래 정보를 입력하고 **Next**를 선택하세요.

    - Subscription – 할당된 **subscription** 선택

    - Resource group – 할당된 **Resource group** (**ResourceGroup1**) 선택

    - Region – 할당된 **region** 선택

    - Name – +++**openaiservice52374668**+++

    - Pricing tier – **Standard** 선택

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image32.png)

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image33.png)

4.  다음 두 화면에서 **Next**를 선택한 후, **Review + submit** 화면에서
    **Create**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image34.png)

5.  서비스가 생성되면 **Go to resource**를 클릭하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image35.png)

6.  왼쪽 메뉴에서 **Access control (IAM)** 왼쪽 메뉴에서 **Add -\> Add
    role assignment**를 클릭하세요.

    ![](./media/image36.png)

7.  +++**Cognitive Services OpenAI User**+++를 검색하고, 해당 역할을
    선택한 후 **Next**를 클릭하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image37.png)

8.  **+ Select members**를 클릭하고, **user id**를 검색해 선택한 후
    **Select**를 클릭하세요.

    ![](./media/image38.png)

9.  **Add role assignment** 화면으로 돌아가 **Managed identity**를
    선택하세요. 그런 다음, **+ Select members**를 클릭하세요. **Select
    managed identities** 화면에서 **Managed identity** 아래의**Search
    service**를 선택하고, **documentstore@lab.LabInstanceId()** 서비스를
    선택하세요.

    ![](./media/image39.png)

10. 선택이 완료되면 **Select** 버튼을 클릭하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png)

11. 다음 두 화면에서 Review + assign 버튼을 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

12. 역할 추가가 **성공**했다는 메시지가 나타날 때까지 기다린 후, 다음
    단계로 진행하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image42.png)

13. Azure OpenAI Service 리소스의 **Overview** 페이지에서**Go to Azure
    AI Foundry portal**을 선택해 Azure OpenAI Service를 열고 모델을
    배포하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image43.png)

14. 왼쪽 메뉴에서 **Deployments**를 선택한 후 **+ Deploy model** -\>
    **From base models**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image44.png)

15. +++**text-embedding**+++를 검색하고 **text-embedding-3-large**를
    선택한 후**Confirm**을 클릭하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

16. Deploy text-embedding-3-large 화면에서 **Deploy**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

17. 모델이 배포되면 배포 세부 정보 화면이 표시됩니다.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image47.png)

## 연습 4: 벡터 인덱스 생성

AI Search 리소스가 벡터 검색을 수행하려면 벡터 인덱스가 필요합니다. 이
연습에서는 업로드된 데이터를 벡터화합니다.

1.  Azure 포털에서 **documentstore@lab.LabInstanceId()**, AI Search
    서비스 리소스로 이동하세요. **Import and vectorize data**를
    선택하세요.

    ![](./media/image48.png)

2.  **Azure Blob Storage** 옵션을 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image49.png)

3.  **What scenarios are you targeting?** 화면에서 **RAG** 옵션을
    선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image50.png)

4.  아래 정보를 입력하고, 나머지 값은 기본값으로 두고 **Next**를
    클릭하세요.

    - Subscription – 지정된 **subscription** 선택

    - Storage account- **docstore@lab@LabInstanceId()** 선택

    - Blob-container – **documents** 선택

    ![](./media/image51.png)

5.  Vectorize your text 화면에서, 구독은 미리 채워져 있습니다. 아래
    정보를 입력하고 **Next**를 클릭하세요.

    - Azure OpenAI resource – **<openaiservice@lab.LabInstanceId()>** 선택

    - Model deployment – **text-embedding-3-large** 선택

    - Authentication type – **System assigned identity** 선택

    - Azure OpenAI 비용 경고 확인 체크박스를 선택하세요.

    ![A screenshot of a computer AI-generated content may be incorrect.](./media/image52.png)

6.  **Vectorize and enrich your images** 화면에서는 이미지 관련 작업이
    없으므로 **Next**를 선택하고, **Advanced settings**
    화면에서도 **Next**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image53.png)

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image54.png)

7.  **Review + create** 화면에서 **Create**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image55.png)

8.  성공 대화 상자에서 **Close**를 클릭하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image56.png)

## 연습 5: 리테일 어시스턴트 에이전트 생성

이 연습에서는 Copilot Studio에서 리테일 어시스턴트 에이전트를
생성합니다.

1.  로그인 자격 증명을 사용해
    +++https://copilotstudio.microsoft.com+++에 로그인하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image57.png)

2.  왼쪽 메뉴에서 **Create**를 선택한세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image58.png)

3.  **+ New agent**를 선택해 새 에이전트를 생성하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image59.png)

4.  설명란에 +++You are a Retail assistant agent for customers HR who
    will answer questions related to the store products+++ 를 입력하고
    **Send**를 선택하세요.

    ![](./media/image60.png)

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image61.png)

5.  에이전트가 생성되면, Test 창에서 +++What is the warranty period for
    Washing machine?+++를 입력하고 **Send**를 클릭하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image62.png)

6.  에이전트가 스크린샷과 같이 일반적인 답변을 제공합니다.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image63.png)

## 연습 6: Azure AI Search를 지식 소스로 추가하기

이 연습에서는 Azure Portal에서 생성한 Azure AI Search를 Copilot Studio의
리테일 어시스턴트 에이전트에 지식 소스로 추가합니다.

1.  에이전트의 **Overview** 페이지에서 **+ Add knowledge**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image64.png)

2.  사용 가능한 지식 소스 목록에서 **Azure AI Search**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image65.png)

3.  다음 화면에서 **Not connected** 옆의 **드롭다운**을 클릭하고
    **Create new connection**을 선택하세요.

    ![A screenshot of a search engine AI-generated content may be
incorrect.](./media/image66.png)

4.  이전 연습에서 메모장에 저장한 **Endpoint url**과 **Admin key** 값을
    입력한 후 **Create**을 클릭해 연결을 생성하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image67.png)

5.  연결이 설정되면 사용 가능한 인덱스가 나열되고 이미 선택되어
    있습니다. **Add to agent**를 클릭하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image68.png)

6.  AI Search 서비스가 에이전트에 지식 소스로 추가되었으며 이제
    **Ready** 상태입니다.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image69.png)

7.  이제 이전에 시도했던 것과 동일한 질문으로 에이전트를 테스트해
    보겠습니다.

8.  테스트 창에서 +++ What is the warranty period for Washing
    machine?+++을 입력하고 **Send**를 클릭하세요.

    ![](./media/image70.png)

9.  이제 에이전트의 응답이 AI Search 서비스에 업로드된 문서에서 가져온
    것임을 확인할 수 있습니다.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image71.png)

## 연습 7: Azure AI Foundry에서 모델 배포

이 연습에서는 Copilot Studio에서 사용할 수 있도록 Azure AI Foundry에
모델을 배포합니다.

1.  이전에 생성한 Azure AI Foundry Azure OpenAI 리소스를 여세요.

2.  왼쪽 창에서 **Deployments**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image72.png)

3.  **+ Deploy model** 옆의 드롭다운을 선택하고 **Deploy base model**을
    선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image73.png)

4.  **gpt-4o** 을 선택한 뒤, **Confirm**을 선택하세요.

    ![](./media/image74.png)

5.  Deploy gpt-4o 대화 상자에서 **Deployment name**을
    +++**ModelforMCS**+++로 입력하고, 다른 기본값을 그대로 두고
    **Deploy**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image75.png)

6.  Target URI와 Key 값을 복사해 메모장에 저장하세요. 나중에 Copilot
    Studio에서 연결을 생성할 때 사용됩니다.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image76.png)

이제 모델이 배포되었으므로 Copilot Studio의 에이전트 프롬프트에서 사용할
수 있습니다.

## 연습 8: Copilot Studio에서 프롬프트 생성 및 Azure AI Foundry에서 생성한 모델 사용하기

이번 연습에서는 Azure AI Foundry에서 배포한 모델을 Copilot Studio에
가져와 사용하는 방법을 학습합니다. 여기서는 배포된 기본 모델을
사용하지만, 비즈니스 요구사항에 따라 맞춤형(fine-tuned) 모델을 생성하고
Copilot Studio에서 사용할 수도 있습니다.

1.  Copilot Studio 에이전트에서 상단 메뉴 바의 **Tools**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image77.png)

2.  **+ New tool**을 선택해 에이전트에 새 도구를 추가하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image78.png)

3.  새 프롬프트를 추가할 것이므로 Prompt를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image79.png)

4.  Custom prompt 화면에서 **model**이름 옆 드롭다운을 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image80.png)

5.  **Azure AI Foundry Models** 옆의 +를 선택해 Azure AI Foundry에
    배포한 모델을 추가하고 **Connect a new model**을 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image81.png)

    ![A screenshot of a computer AI-generated content may be incorrect.](./media/image82.png)

6.  아래 세부 정보를 입력하고 Connect를 클릭하세요.

    - Model deployment name - +++ModelforMCS+++

    - Base model name - +++gpt-4o+++

    - Azure model endpoint URL – 이전에 저장한 Target URL 입력

    - API Key – 이전에 저장한 모델 API 키 입력

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image83.png)

    ![A screen shot of a computer AI-generated content may be
    incorrect.](./media/image84.png)

7.  연결이 완료되면 **Close**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image85.png)

8.  이제 ModelforMCS 모델이 선택된 것을 확인할 수 있습니다.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image86.png)

9.  프롬프트명을 +++WM Types+++로 변경하세요. +++What are the different
    types of Washing Machines? +++를 입력한 후 **Test**를 선택하세요.

    ![](./media/image87.png)

10. 프롬프트를 저장하려면 **Save**를 선택하세요.

    ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image88.png)

11. **Add to agent** 옵션을 선택해 프롬프트를 에이전트에 추가하세요.

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image89.png)

    ![A screenshot of a computer AI-generated content may be
    incorrect.](./media/image90.png)

이 기능을 통해 Azure AI Foundry에서 모델을 파인튜닝하고, 이를 Copilot
Studio에서 쉽게 사용할 수 있습니다. Azure AI Foundry의 방대한 모델
생태계를 Copilot Studio로 쉽게 가져올 수 있습니다.

## 요약

이 실습에서는 Copilot Studio의 에이전트를 Azure AI Search 서비스에 지식
소스로 연결하고, 해당 소스를 기반으로 에이전트를 테스트하는 방법을
학습했습니다. 또한 Azure AI Foundry에 배포된 모델을 Copilot Studio로
가져와 활용하는 방법도 학습했습니다.
