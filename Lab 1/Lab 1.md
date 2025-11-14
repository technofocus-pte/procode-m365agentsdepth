# 실습 1 - Microsoft 365 Agents Toolkit을 사용해 TypeSpec으로 정의된 RepairService 선언형 에이전트 구축

**목표**

이 실습에서는 Microsoft 365 Agents Toolkit을 사용해 TypeSpec으로 정의된
선언형 에이전트(Declarative Agent) 를 구축합니다.
RepairServiceAgent 라는 이름의 에이전트를 생성하게 되며, 이 에이전트는
기존 API 서비스를 통해 수리 데이터를 조회하고 상호작용해 사용자가 자동차
수리 기록을 관리할 수 있도록 돕습니다.

**선언형 에이전트(Declarative agents)**

**선언형 에이전**는 선언형 에이전트는 Microsoft 365용 에이전트의 한
유형입니다. Microsoft 365 Copilot을 확장해 구축할 수 있으며, 사용자 지정
지식과 사용자 지정 작업을 정의하여 특정 시나리오에 맞춤화된 에이전트를
생성할 수 있습니다.

선언형 에이전트는 Microsoft 365 Copilot과 동일한 인프라, 오케스트레이터,
파운데이션 모델 및 보안 제어를 사용하므로 일관되고 익숙한 사용자 경험을
제공합니다.

![Declarative agent architecture diagram. At the very basis there is the
foundational model of Microsoft 365 Copilot, as well as the same
orchestrator. The agent provides also custom knowledge and grounding
data, and custom skills as actions, triggers, and workflows.. The user
experience is available in Microsoft 365 Copilot.](./media/image1.png)

**TypeSpec이 선언형 에이전트에서 중요한 이유**

**TypeSpec이란?**

TypeSpec은 Microsoft가 개발한 언어로, API 계약을 구조화되고 타입 안전한
방식으로 설계하고 설명하기 위해 사용됩니다. 쉽게 말해, API가 어떤 데이터
형식을 받고, 어떤 데이터를 반환하며, API의 각 구성 요소와 동작이 어떻게
연결되어야 하는지를 정의하는 청사진(Blueprint)과 같은 역할을 합니다.

**에이전트에 TypeSpec을 사용하는 이유는?**

프런트엔드나 백엔드 코드에서 TypeScript가 구조를 강제하는 방식이 마음에
든다면, TypeSpec이 에이전트와 액션 같은 API 서비스에서 구조를 강제하는
방식은 더욱 마음에 드실 것입니다. TypeSpec은 Visual Studio Code와 같은
도구와 연계되는 설계 중심 개발 워크플로우에 완벽하게 적합합니다.

명확한 의사소통 - 에이전트가 어떻게 동작해야 하는지를 정의하는 단일
진실의 공급원(Single Source of Truth)을 제공해 선언형 에이전트처럼 여러
매니페스트 파일을 다룰 때 발생할 수 있는 혼란을 줄입니다.

일관성 - 에이전트의 모든 부분(액션, 기능 등)이 동일한 패턴을 따라
일관되게 설계되도록 보장합니다.

자동화 친화적 - OpenAPI 사양 및 기타 매니페스트를 자동으로 생성해 시간
절약과 인적 오류 감소에 도움을 줍니다.

조기 검증 - 실제 코드를 작성하기 전에 설계 단계에서 데이터 타입 불일치나
정의 모호성과 같은 문제를 미리 발견할 수 있습니다.

설계 우선 접근법 – 구현 단계로 바로 넘어가기 전에 에이전트와 API의 구조
및 계약을 먼저 고민하도록 유도해 장기적으로 더 나은 유지보수성과 품질을
확보할 수 있습니다.

## 연습 1: 실습 환경 설정

이 연습에서는 Microsoft 365 Copilot 을 활용해 맞춤형 AI 지원을 구현할 수
있도록, Copilot 에이전트를 빌드·테스트·배포하기 위한 개발 환경을
설정합니다.

### 작업 1: Agents Toolkit 설치

**Agents Toolkit for Visual Studio Code**을 사용하려면 Visual Studio
Code가 필요합니다. 이 작업에서는 Visual Studio Code에 Toolkit을 설치하는
과정을 진행합니다.

1.  VM에서**Visual Studio Code**를 여세요. 왼쪽 메뉴에서**Extensions**를
    선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image2.png)

2.  +++Microsoft 365 Agents Toolkit+++을 검색해 선택하세요.
    **Install**을 클릭하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image3.png)

3.  Toolkit이 정상적으로 설치되었는지 확인하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

4.  바탕화면에 +++ServiceAgent+++라는 새 폴더를 생성하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image5.png)

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image6.png)

## 연습 2: Microsoft 365 Agents Toolkit과 TypeSpec을 사용해 기본 에이전트 구축하기

이 연습에서는 **Declarative Agent**를 빌드하고, 정의를 추가하며, 액션을
업데이트하고 에이전트를 테스트합니다.

### 작업 1: Microsoft 365 Agents Toolkit을 사용해 기본 에이전트 프로젝트 스캐폴딩하기

이 작업에서는**Microsoft 365 Agents Toolkit**을 사용해 **TypeSpec**
정의를 포함한 **Declarative Agent**를 구축합니다. 기존 API 서비스를 통해
수리 데이터를 처리하며 사용자가 자동차 수리 기록을 관리할 수 있도록
지원하는 **RepairServiceAgent** 라는 에이전트를 생성합니다.

1.  VS Code 왼쪽 메뉴에서 **Microsoft 365 Agents Toolkit
    icon**을 ![m365atk-icon](./media/image7.png)  찾아 선택하세요. 활동
    표시줄(Activity Bar)이 열립니다. 활동 표시줄에서 **Create a New
    Agent/App** 버튼을 클릭하면Microsoft 365 Agents Toolkit에서 사용
    가능한 앱 템플릿 목록이 포함된 팔레트가 열립니다.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image8.png)

2.  템플릿 목록에서 **Declarative Agent**를 선택하세요.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image9.png)

3.  다음으로 TypeSpec을 사용해 에이전트를 정의하기 위해 **Start with
    TypeSpec for Microsoft 365 Copilot**을 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

4.  다음으로 Desktop에서 **ServiceAgent** 폴더를 선택하세요. 이 위치에
    Agents Toolkit이 에이전트 프로젝트를 스캐폴딩합니다.

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image11.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image12.png)

5.  다음으로 애플리케이션 이름을 +++RepairServiceAgent+++로 입력하고
    **Enter**를 눌러 과정을 완료하세요. 에이전트 프로젝트가 미리 로드된
    새 VS Code 창이 열립니다.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image13.png)

6.  에이전트를 업로드하고 테스트하려면 **Microsoft 365 Agents
    Toolkit**에 로그인해야 합니다.

7.  프로젝트 창에서 왼쪽 메뉴의 **Microsoft 365 Agents Toolkit
    icon** ![m365atk-icon](./media/image7.png) 을 다시 선택하세요.
    그러면, Accounts, Environment, Development 등의 섹션이 포함된 Agent
    Toolkit 활동 표시줄이 열립니다.

8.  **Accounts** 섹션에서**Sign in to Microsoft 365**를 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image14.png)

9.  에디터에서 Microsoft 365 개발자 샌드박스에 로그인하거나 생성 또는
    취소할 수 있는 대화 상자가 열립니다. **Sign in**을 선택하고 자격
    증명으로 로그인하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image15.png)

10. 로그인이 완료되면 브라우저를 **닫고** 로젝트 창으로 돌아가세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image16.png)

### 작업 2: 에이전트 정의하기

Agents Toolkit이 스캐폴드한 Declarative Agent 프로젝트에는 GitHub API에
연결해 저장소 문제를 표시하는 코드가 포함된 템플릿이 제공됩니다. 이번
실습에서는 자동차 수리 서비스와 통합되어 수리 데이터를 효율적으로 관리할
수 있는 다양한 기능을 지원하는 에이전트를 직접 구축해 보겠습니다.

프로젝트 폴더에는 **main.tsp**와 **actions.tsp** 두 개의
**TypeSpec** 파일이 있습니다. 에이전트는 **main.tsp** 파일에서
**메타데이터**, **지침** 및 **기능**과 함께 정의됩니다.  in the  file.
**actions.tsp** 파일은 **에이전트의 액션**을 정의하는 데 사용하세요. API
서비스 연결과 같은 액션이 에이전트에 포함되어 있다면, 이 파일에서
정의해야 합니다.

**main.tsp** 파일을 열어 기본 템플릿에 포함된 내용을 확인하세요. 이
템플릿을 수리 서비스 시나리오에 맞게 수정할 것입니다.

**에이전트 메타데이터 및 지침 업데이트**

**main.tsp** 파일에는 에이전트의 기본 구조가 포함되어 있습니다. Agents
Toolkit 템플릿에서 제공하는 내용은 다음과 같습니다:

- **Agent name** 및 **description** 1️⃣

- 기본 **instructions** 2️⃣

- **actions** 및 **capabilities**에 대한 예시 코드(주석 처리됨) 3️⃣

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image17.png)

1.  코드에서 **@agent** 및 **@instructions** 블록(10~17행)을 확인하세요.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image18.png)

2.  자동차 수리 시나리오에 맞게 에이전트를
    정의하세요. **@agent**와 **@instruction** 정의를 아래 코드
    스니펫으로 변경하세요.

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

3.  다음으로 에이전트의 대화 시작 문구(conversation starter)를
    추가하세요. @instructions 바로 아래에 주석 처리된 대화 시작 코드가
    있습니다(22~25행). 해당 @conversationStarter 블록을 아래 코드로
    변경하세요.

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

### 작업 3: 에이전트의 액션 업데이트

이 작업에서는 **actions.tsp** 파일을 열어 에이전트의 액션을 정의합니다.
나중에 main.tsp 파일로 돌아가 액션 참조를 포함한 에이전트 메타데이터를
완성하겠지만, 우선 액션 자체를 먼저 정의해야 합니다.

actions.tsp 파일의 기본 코드에는 GitHub 저장소의 열린 이슈를 검색하는
예제 코드가 포함되어 있습니다. 이 코드는 에이전트의 액션을 정의할 때
필요한 구성 요소—예를 들어 액션 메타데이터, API 호스트 URL, 그리고
작업(operations)이나 함수 정의—를 이해하도록 돕는 참고용 예시입니다.
이번 단계에서는 이 코드를 자동차 수리 서비스(Repair Service) 관련 코드로
변경할 것입니다.

1.  **actions.tsp** 파일을 여세요. **@service** 부터 **const
    SERVER_URL**까지 코드(7~25행) 를 아래 코드 블록으로 변경하세요.

이 업데이트는 액션의 메타데이터를 정의하고 서버 URL을 설정합니다. 또한,
namespace가 GitHubAPI에서 RepairsAPI로 변경된 점에 유의하세요.

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

2.  다음으로 템플릿 코드의 작업을 searchIssues에서 **listRepairs**로
    변경하세요. listRepairs는 수리 목록을 가져오는 작업으로, 자동차
    **수리** 데이터를 조회하는 기능을 수행합니다. SERVER_URL 정의 바로
    아래부터 마지막 닫는 중괄호 *직전*까지의 전체 코드 블록(27~37행)을
    아래 코드 스니펫으로 변경하세요. 마지막 닫는 중괄호(})는 삭제하지
    말고 그대로 남겨두어야 합니다.

	```
	/**
	* List repairs from the API 
	* @param assignedTo The user assigned to a repair item.
	*/

	@route("/repairs")
	@get  op listRepairs(@query assignedTo?: string): string;

	```

	![A screenshot of a computer program AI-generated content may be incorrect.](./media/image22.png)

3.  이제 **main.tsp** 파일로 돌아가, 방금 정의한 액션을 에이전트에
    추가하세요. 대화 시작 문구 이후의 전체 코드 블록을 아래 스니펫으로
    변경하세요.

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

### 작업 4: (읽기 전용)데코레이터 이해하기

Tdㅊ이 작업의 목적은 TypeSpec 파일에 정의된 내용을 이해하는 것입니다. 이
단계에서는 읽기만 하면 됩니다. main.tsp와 actions.tsp 파일에는 @로
시작하는 데코레이터, 네임스페이스, 모델 및 에이전트 정의와 관련된 다양한
요소가 포함되어 있습니다.

아래 내용을 참고해 각 데코레이터의 역할을 이해해 보세요.

- **@agent** - 에이전트의 네임스페이스(이름)와 설명을 정의합니다.

- **@instructions** - 에이전트의 동작 방식을 규정하는 지침을
  정의합니다(최대 8,000자).

- **@conversationStarter** - 에이전트의 대화 시작 문구를 정의합니다.

- op - 작업(operation)을 정의합니다. op GraphicArt, op CodeInterpreter와
  같은 에이전트 기능을 정의하거나, op listRepairs와 같은 API 작업을
  정의할 수 있습니다.

- **@server** - API의 서버 엔드포인트와 이름을 정의합니다.

- **@capabilities** - 함수 내에서 사용될 경우, 작업 수행 시 필요한
  간단한 확인 카드 등 Adaptive Card 형식의 기능을 정의합니다.

### 작업 5: 에이전트 테스트하기

이 작업에서는 방금 생성한 Repair Service Agent를 테스트합니다.

1.  프로젝트 내에서 **Agents Toolkit extension** 아이콘을 선택하여 활동
    표시줄(Activity Bar)을 엽니다.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image24.png)

2.  Agents Toolkit의 활동
    표시줄에서 **LifeCycle** 아래의 **Provision**을 선택하세요. 이
    작업을 통해 생성된 매니페스트 파일과 아이콘으로 구성된 앱 패키지가
    빌드되며, 테스트용으로 본인 계정에만 사이드로드되어 카탈로그에
    추가됩니다.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image25.png)

3.  웹 브라우저를 열고 +++<https://m365.cloud.microsoft/chat+++> 에
    접속해 Copilot 앱을 실행하세요.

4.  Microsoft 365 Copilot 인터페이스에 표시된 **Agents**
    목록에서 **RepairServiceAgent**를 선택하세요. 이 과정에는 다소
    시간이 걸릴 수 있으며, 프로비저닝 진행 상태를 알려주는
    토스터(toaster) 메시지가 화면에 표시됩니다.

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image26.png)

5.  대화 시작 문구 중 **List repairs**를 선택하고 프롬프트를 전송하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

6.  이로써 에이전트와의 대화가 시작되며, 에이전트가 수리 목록을 포함한
    응답을 표시하는 것을 확인할 수 있습니다.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

## 연습 3: 에이전트 기능 강화

이 연습에서는 에이전트에 더 많은 작업을 추가하고, Adaptive Card로 응답을
제공하도록 하며, 코드 인터프리터 기능을 통합하는 등 기능을 확장할
것입니다. 단계별로 각각의 향상점을 살펴보겠습니다. VS Code에서
프로젝트로 돌아가세요.

### 에이전트를 수정해 더 많은 작업 추가하기

이 작업에서는 에이전트를 수정하고 **createRepair**, **updateRepair,
deleteRepair**와 같은 작업을 추가합니다.

1.  **actions.tsp** 파일을 열고, **listRepairs** 작업 바로 다음에 아래
    스니펫을 복사하여 붙여 넣어 **createRepair**, **updateRepair,
    deleteRepair** 작업을 추가하세요. 이 코드에서는 Repair 항목의 데이터
    모델도 함께 정의합니다.

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

2.  이제 **main.tsp** 파일을 열고, 방금 추가한 새 작업들을 에이전트의
    액션에 포함시킵니다. **RepairServiceActions** namespace 내부에서
    **op listRepairs is global.RepairsAPI.listRepairs** 문장 다음에 아래
    스니펫을 **붙여**넣으세요.

	```
	op createRepair is global.RepairsAPI.createRepair;
	op updateRepair is global.RepairsAPI.updateRepair;
	op deleteRepair is global.RepairsAPI.deleteRepair;

	```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image30.png)

3.  첫 번째 대화 시작 문구 정의 바로 다음에, 새 수리 항목 생성을 위한
    새로운 대화 시작 문구도 추가하세요.

	```
	@conversationStarter(#{
	title: "Create repair",
	text: "Create a new repair titled \"[TO_REPLACE]\" and assign it to me"
	})

	```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image31.png)

### 작업 2: 함수 참조에 적응형 카드(Adaptive Card) 추가하기

이 작업에서는 적응형 카드를 활용해 참조 카드 또는 응답 카드를
개선합니다. **listRepairs** 작업에 수리 항목용 적응형 카드를 추가해
보겠습니다.

1.  프로젝트 폴더의**appPackage** 폴더 안에 +++cards+++라는 새 폴더를
    생성하세요.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image32.png)

2.  **cards** 폴더에  +++repair.json+++ 파일을 생성하고 아래의 코드
    스니펫을 그대로 파일에 붙여넣으세요.

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

3.  다음으로 **actions.tsp** 파일로 돌아가 **listRepairs** 작업을
    찾으세요.**@get op listRepairs(@query assignedTo?: string):
    string** 작업 정의 줄을 아래 2줄의 코드로 변경하세요.

	```
	@card(#{ dataPath: "$", title: "$.title",   url: "$.image", file: "cards/repair.json"})
	@get op listRepairs(@query assignedTo?: string): Repair[];

	```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image34.png)

4.  위 카드 응답은 사용자가 수리 항목을 조회할 때 또는 에이전트가 항목
    목록을 참조로 제공할 때 전송됩니다.

5.  에이전트가 이제 추가 기능을 지원하므로, 지침도 이를 반영하도록
    업데이트해야 합니다.

6.  동일한 **main.tsp** 파일에서 @instructions 정의를 수정해 에이전트에
    대한 추가 지시 사항을 포함시킵니다. 기존 **@instructions** 코드
    블록을 아래 코드 블록으로 변경하세요.

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

### 작업 3: 에이전트 프로비저닝 및 테스트하기

이 작업에서는 업데이트된 에이전트, 즉 수리 분석가 기능이 추가된
에이전트를 테스트합니다.

1.  프로젝트 내에서 Agents Toolkit 확장 아이콘을 선택해 활동 표시줄을
    여세요..

2.  Toolkit의 활동 표시줄에서 **LifeCycle** 아래 **Provision**을 선택해
    업데이트된 에이전트를 패키징하고 테스트용으로 업로드하세요.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image36.png)

3.  프로비저닝이 성공적으로 완료되었는지 확인하세요.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image37.png)

4.  열려 있는 **브라우저** 세션으로 돌아가서 **새로고침**하세요.

5.  **RepairServiceAgent**에서 **Create repair** 대화 시작 문구를
    선택하세요. 프롬프트의 일부를 수정해 제목을 추가한 후, 채팅에
    전송하여 상호작용을 시작하세요. 예를 들어:

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image38.png)

6.  **“\[TO REPLACE\]”** 부분을 +++rear camera issue+++로 변경하고,
    담당자를 본인으로 지정하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

7.  확인 대화 상자에는, 새로 추가된 지침 덕분에 전송한 내용보다 더 많은
    메타데이터가 표시되는 것을 확인할 수 있습니다.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png)

8.  대화 상자에서 **확인**을 눌러 항목을 추가하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

9.  에이전트가 **생성된 항목**을 풍부한 **적응형 카드**로 표시하며
    응답합니다.

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image42.png)

10. 다음으로 참조 카드가 제대로 작동하는지 다시 확인하세요. 대화에서
    아래 프롬프트를 전송하세요.

	+++List all my repairs+++.

	확인 대화 상자에서 **Always allow**을 선택하세요.

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image43.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image44.png)

11. 에이전트는 본인에게 할당된 수리 목록을 응답하며, 각 항목은 적응형
    카드로 참조됩니다. 이 경우 방금 추가한 rear camera issue만
    표시되어야 합니다.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

12. 다음으로 에이전트의 새로운 분석 기능을 테스트합니다. 에이전트 오른쪽
    상단의 **New chat** 버튼을 선택해 새 채팅을 엽니다.![A screenshot of
    a computer AI-generated content may be
    incorrect.](./media/image46.png)

13. 아래 프롬프트를 복사해 메시지 상자에 붙여넣고 Enter 키를 눌러
    전송합니다.

14. 수리 항목을 제목 기준으로 세 가지 범주로 분류하세요:

15. Routine Maintenance, Critical, Low Priority. 그런 다음 각 범주의

16. 백분율 표현을 표시하는 차트를 생성하세요.

	![A screenshot of a phone AI-generated content may be
incorrect.](./media/image47.png)

17. 아래 화면과 유사한 응답을 확인할 수 있습니다. 단, 결과는 상황에 따라
    다를 수 있습니다.

	![A screenshot of a data box AI-generated content may be
incorrect.](./media/image48.png)

**요약:**

이번 실습에서 다음을 수행했습니다:

- **TypeSpec** 을 사용해 API를 설명하고 이를 Copilot 작업과
  연결했습니다.

- **Adaptive Cards** 를 구성해 수리 기록을 시각적으로 풍부하게
  표시했습니다.

- 사용자가 Copilot과 자연스럽게 상호작용하며 수리 데이터를 관리할 수
  있는 완전한 시나리오를 구축했습니다.

이번 실습을 통해 선언형 에이전트(Declarative Agents)가 **Copilot
플랫폼의 오케스트레이션, 파운데이션 모델, 보안 제어**를 활용해
사용자에게 친숙하고 일관된 경험을 제공하면서 맞춤형 비즈니스 데이터 및
워크플로와 통합될 수 있음을 확인했습니다. 
