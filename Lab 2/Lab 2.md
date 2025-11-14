# Microsoft 365 Agents Toolkit을 활용한 지침 기반 지리 위치 게임 에이전트 구축

**예상 소요 시간: 30분**

## 목표

이번 실습의 목표는 Microsoft 365 Agents Toolkit을 활용해 Microsoft 365
Copilot용 선언형 에이전트를 구축하는 방법을 익히는 것입니다. 참가자는 이
실습을 완료하면, 재미있고 교육적인 지리 위치 게임(Geo-location Game)을
구현할 수 있습니다. 이번 실습은 선언형 에이전트의 구조 이해, 지침 구성
및 Microsoft 365 환경과 통합하여 맞춤형 Copilot 상호작용을 구현하는 것에
초점을 맞춥니다.

## 솔루션

참가자는 Visual Studio Code에 Microsoft 365 Agents Toolkit을 설치하고
개발 환경을 설정합니다. 템플릿을 사용해 Geo Locator Game이라는 선언형
에이전트를 스캐폴딩하며, 에이전트의 지침을 사용자
정의하고 instruction.txt 및 manifest.json과 같은 구성 파일을
업데이트합니다. 또한 이번 실습에서는 에이전트를 고유 식별자와 커스텀
아이콘으로 강화하고 기능 테스트를 진행하는 방법도 안내합니다. 그 결과,
Microsoft 365와 원활하게 통합되면서 도시와 관련된 단서를 제공하는
완전하고 몰입감 있는 Copilot 애플리케이션을 완성할 수 있습니다.

## 연습 1: Microsoft 365 Copilot 개발 환경 설정

### 작업 1: Microsoft 365 Agents Toolkit 설치 

1.  Visual Studio Code를 열고 **Extensions** 도구 모음 버튼을 클릭핫요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image1.png)

2.  +++**Microsoft 365 agents**+++를 검색해 **Microsoft 365 Agents
    Toolkit**을 찾으세요.

	![image](./media/image2.png)

3.  **Install**을 선택하세요.

	![image](./media/image3.png)

4.  설치가 완료되면 왼쪽 탐색 표시줄에 **Microsoft 365 Agents
    Toolkit** 아이콘이 나타납니다.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

[!Note] **참고:** Microsoft 365 Agents Toolkit은 Teams Toolkit의
발전된 버전입니다. 현재 전환 단계에 있어, 일부 화면에서는 Teams
Toolkit으로, 다른 화면에서는 Microsoft 365 Agents Toolkit으로 표시될 수
있습니다.

## 연습 2: 첫 번째 선언형 에이전트

이번 실습에서는 Microsoft 365 Agents Toolkit for Visual Studio Code을
사용해 간단한 선언형 에이전트를 구축합니다. 이 에이전트는 전 세계 도시를
탐험하도록 도와주며, 업무 중 재미있고 교육적인 휴식을 제공하도록
설계되었습니다. 참가자는 추상적인 단서를 활용해 도시를 추측할 수 있으며,
단서를 많이 사용할수록 점수가 낮아집니다. 게임이 끝나면 최종 점수가
공개됩니다.

이번 실습을 통해 배우게 될 내용은 다음과 같습니다:

- Microsoft 365 Copilot용 선언형 에이전트란 무엇인지

- Microsoft 365 Agents Toolkit 템플릿으로 선언형 에이전트 생성

- 지침을 사용해 지리 위치 게임용 에이전트 맞춤화

- 앱 실행 및 테스트 방법

- 보너스 실습: SharePoint Teams 사이트 필요

**소개**

선언형 에이전트는 Microsoft 365 Copilot의 확장 가능 인프라와 플랫폼을
활용하며, 특정 업무나 주제에 맞추어 설계되었습니다. 이는 특정 영역이나
비즈니스 요구 사항에 대해 전문가 역할을 수행하며, 표준 Microsoft 365
Copilot 채팅 인터페이스를 사용하면서도 특정 작업에 집중할 수 있도록
보장합니다.

이제 여러분만의 선언형 에이전트를 만들어볼 시간입니다! Copilot의 마법을
경험해봅시다!

이번 실습에서는 Microsoft 365 Agents Toolkit의 기본 템플릿을 사용해
선언형 에이전트 구축을 시작합니다. 이는 학습용 출발점을 제공하기 위한
것이며, 이후 에이전트를 지리 위치 게임에 맞게 수정합니다.

AI의 목표는 전 세계 여러 도시에 대해 학습하도록 도우면서 업무에서 즐거운
휴식을 제공하는 것입니다. 에이전트는 도시를 맞추기 위한 추상적인 단서를
제공하며, 단서를 많이 사용할수록 점수가 낮아집니다. 게임이 끝나면 최종
점수가 공개됩니다.

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image5.png)

이번 실습에서는 에이전트가 비밀 일기 🕵🏽 와 지도 🗺️ 파일을 참고해
플레이어에게 더 많은 도전 과제를 제공하도록 할 예정입니다.

그럼, 시작해봅시다.

**선언형 에이전트의 구조**

Copilot에 대한 확장 기능을 점점 더 많이 개발하다 보면, 결국 여러분이
구축하게 될 것은 zip 파일 형태의 몇 개 파일로 구성된 모음임을 알게 될
것입니다. 이를 앱 패키지라고 하며, 설치 후 사용하게 됩니다. 따라서 앱
패키지가 무엇으로 구성되어 있는지 기본적으로 이해하는 것이 중요합니다.
선언형 에이전트의 앱 패키지는 이전에 만들어본 Teams 앱과 유사하지만,
추가 요소가 포함되어 있습니다. 아래 표에서 핵심 요소들을 확인할 수
있습니다. 또한, 앱 배포 과정이 Teams 앱 배포와 매우 유사하다는 점도 알
수 있습니다.

|요소	|설명	|파일명	|
|:-----|:------|:-------|:--------|
|앱 매니페스트	|앱 구성, 기능, 필요한 리소스 및 주요 속성을 정의	|manifest.json	|
|앱 아이콘	|선언형 에이전트를 위한 컬러(192x192) 아이콘과 윤곽선(32x32) 아이콘이 필요함	|icon.png, color.png	|
|선언형 에이전트 매니페스트	|	에이전트 구성, 지침, 필수 필드, 기능, 대화 시작 문구, 액션 등을 정의|declarativeAgent.json	|

**참고:** 선언형 에이전트에는 SharePoint, OneDrive, 웹 검색 등에서 참조
데이터를 추가하고, 플러그인이나 커넥터와 같은 확장 기능을 추가할 수
있습니다. 이 과정의 다음 실습에서 플러그인을 추가하는 방법을 배우게 될
것입니다.

**선언형 에이전트의 기능**

지침을 추가하는 것뿐만 아니라, 에이전트가 접근해야 할 지식 베이스를
지정함으로써 에이전트가 컨텍스트 및 데이터를 더 효과적으로 활용할 수
있습니다. 이를 기능(Capabilities)이라고 하며, 지원되는 기능에는 세 가지
유형이 있습니다.

- **Microsoft Graph 커넥터** - Graph 커넥터의 연결을 에이전트에 전달하여
  에이전트가 커넥터의 지식에 액세스하고 활용할 수 있도록 합니다.

- **OneDrive 및 SharePoint** - 에이전트가 파일 및 사이트에 접근할 수
  있도록 URL을 제공합니다.

- **Web search** - 에이전트의 지식 베이스의 일부로 웹 콘텐츠를
  활성화하거나 비활성화할 수 있습니다.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image6.png)

**One Drive 및 SharePoint**

URL은 SharePoint 항목(사이트, 문서 라이브러리, 폴더 또는 파일)의 전체
경로여야 합니다. SharePoint에서 “Copy direct link” 옵션을 사용해 파일과
폴더의 전체 경로를 가져올 수 있습니다. 이를 위해 파일 또는 폴더를 마우스
오른쪽 버튼으로 클릭하고 Details를 선택하세요. 경로(Path)로 이동한 후
복사 아이콘을 클릭하세요. URL을 지정하지 않으면, 로그인한 사용자가 접근
가능한 OneDrive 및 SharePoint 전체 콘텐츠가 에이전트에 사용됩니다.

**Microsoft Graph 커넥터**

연결을 지정하지 않으면 로그인한 사용자가 접근 가능한 Graph 커넥터 전체
콘텐츠가 에이전트에 사용됩니다.

**웹 검색(Web search)**

현재 특정 웹사이트나 도메인을 지정할 수 없으며, 단순히 웹 사용 여부를
켜거나 끄는 토글 역할만 합니다.

## 연습 3: 템플릿에서 선언형 에이전트 스캐폴딩하기

앱 패키지에 포함된 파일 구조를 알고 있다면, 어떤 편집기를 사용하더라도
선언형 에이전트를 생성할 수 있습니다. 하지만 Microsoft 365 Agents
Toolkit과 같은 도구를 사용하면, 파일 생성뿐만 아니라 앱 배포 및 게시
과정까지 쉽게 진행할 수 있어 훨씬 편리합니다. 따라서 실습에서는
Microsoft 365 Agents Toolkit을 사용합니다.

### 작업 1: Microsoft 365 Agents Toolkit으로 선언형 에이전트 앱 생성

1.  Visual Studio Code에서 Microsoft 365 Agents Toolkit 확장을 열고,
    **Create a New App**을 선택하세요. 

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image7.png)

2.  패널이 열리면 프로젝트 유형 목록에서 **Agent**를 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image8.png)

3.  다음으로 Copilot Agent의 앱 기능을 선택하라는 메시지가
    표시됩니다. **Declarative agent**을 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

4.  이어서 기본 선언형 에이전트를 만들지 API 플러그인이 포함된
    에이전트를 만들지 선택하라는 메시지가 나타나면, **No Plugin** 옵션을
    선택을 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

5.  다음으로 프로젝트 폴더를 생성할 위치를 지정하기 위해 **Default
    folder** 옵션을 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image11.png)

6.  애플리케이션 이름을 +++**Geo Locator Game**+++ 으로 입력하고 Enter를
    누르세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image12.png)

선택한 폴더에 몇 초 내로 프로젝트가 생성되며, Visual Studio Code의 새
프로젝트 창에서 열립니다. 이 폴더가 바로 작업 폴더입니다.

7.  소스 신뢰 여부에 대한 프롬프트가 나타나면, **Yes, I trust the
    authors**를 클릭하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image13.png)

	![A screenshot of a computer AI-generated content may be incorrect.](./media/image14.png)

잘하셨습니다! 이제 기본 선언형 에이전트가 성공적으로 설정되었습니다.
다음으로 프로젝트 내 파일들을 살펴보고, 지리 위치 게임 앱으로 맞춤
설정할 준비를 합니다.

### 작업 2: Microsoft 365 Agents Toolkit에서 계정 설정

1.  왼쪽 메뉴에서 Microsoft 365 Agents Toolkit 아이콘을 선택하세요. **Accounts** 섹션에서**Sign in to Microsoft 365**를 클릭하고, **Resources**  탭의 **Azure Portal** 섹션에서 **User1 credentials** 계정으로 로그인하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image15.png)

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image16.png)

2.  브라우저 창이 열리며 Microsoft 365에 로그인하라는 화면이 표시됩니다.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image17.png)

3.  Security Alert 대화상자에서 **Allow access**을 선택하세요.

	![A screenshot of a computer security alert AI-generated content may be
incorrect.](./media/image18.png)

4.  브라우저 창에 "You are signed in now and close this page"라는
    메시지가 표시되면, 해당 창을 닫으세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image19.png)

5.  **Custom App Upload Enabled** 표시가 초록색 체크 표시로 되어 있는지
    확인하세요.

	![image](./media/image20.png)

### 작업 3: 앱 내 파일 이해하기

기본 프로젝트 구조는 다음과 같습니다:

|	폴더/파일|내용	|
|:----|:-------|
|.vscode	|디버깅을 위한 VSCode 파일	|
|appPackage	|Teams 애플리케이션 매니페스트, GPT 매니페스트 및 API 사양을 위한 템플릿	|
|	env|	기본 .env.dev 파일이 포함된 환경 설정 파일|
|	appPackage/color.png|애플리케이션 로고 이미지	|
|	appPackage/outline.png|	애플리케이션 로고 윤곽 이미지|
|	appPackage/declarativeAgent.json|선언형 에이전트의 설정 및 구성을 정의	|
|appPackage/instruction.txt	|선언형 에이전트의 동작 정의	|
|	appPackage/manifest.json|	선언형 에이전트의 메타데이터를 정의하는 Teams 애플리케이션 매니페스트|
|teamsapp.yml	|	주요 Microsoft 365 Agents Toolkit 프로젝트 파일. 프로젝트 파일은 속성(Properties) 및 구성 스테이지(stage) 정의라는 두 가지 주요 요소를 포함|

1.  이번 실습에서 주요 관심 파일은 **appPackage/instruction.txt**로,
    에이전트에 필요한 핵심 지침이 담긴 파일입니다. 이 파일은 일반 텍스트
    형식이며, 자연어로 지침을 작성할 수 있습니다.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image21.png)

2.  또 다른 중요한 파일은 **appPackage/declarativeAgent.json**으로,
    새로운 선언형 에이전트를 통해 Microsoft 365 Copilot을 확장할 때
    따라야 하는 스키마가 정의되어 있습니다. 이 파일의 스키마가 갖는
    속성은 다음과 같습니다.

    - $schema : 스키마 참조

    - Version : 스키마 버전

    - Name : 선언형 에이전트의 이름

    - Description : 에이전트 설명

    - Instructions : 에이전트의 동작을 결정하는 지침이
      담긴 **instructions.txt** 파일의 경로. 지침을 일반 텍스트 값으로
      직접 입력할 수도 있지만, 이번
      실습에서는 **instructions.txt** 파일을 사용하겠습니다.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image22.png)

3.  또 다른 중요한 파일은 **appPackage/manifest.json** 파일로, 패키지
    이름, 개발자 이름, 애플리케이션에서 사용되는 Copilot 에이전트에 대한
    참조 등 중요한 메타데이터가 포함되어
    있습니다. 아래는manifest.json파일의 관련 섹션 세부 정보입니다:

	```
	"copilotAgents": {
			"declarativeAgents": [            
				{
					"id": "declarativeAgent",
					"file": "declarativeAgent.json"
				}
			]
		},

	```

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image23.png)

4.  또한 color.png와 outline.png 로고 파일을 업데이트하여 애플리케이션
    브랜드에 맞게 조정할 수 있습니다. 이번 실습에서는 에이전트를
    돋보이게 하기 위해 **color.png** 아이콘을 변경할 예정입니다.

## 연습 4: 지침 및 아이콘 업데이트

### 작업 1: 아이콘 및 매니페스트 업데이트

1.  먼저 로고를 교체하겠습니다. 프로젝트의 **color.png** 이미지를 새
    이미지로 교체합니다.  **C:\LabFiles**에 있는 **color.png** 이미지를
    복사해 프로젝트 루트 폴더의 **appPackage** 폴더에 있는 동일한 이름의
    이미지를 교체합니다(경로는 **C:\Users\Student\TeamsApps\Geo Locator
    Game\appPackage**이어야 합니다).

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image24.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image25.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image26.png)

2.  다음으로, 프로젝트 루트의 **appPackage/manifest.json** 파일을
    열고 **copilotAgents** 노드를 찾으세요. declarativeAgents 배열의 첫
    번째 항목에 있는 ID 값을 declarativeAgent에서
    +++dcGeolocator+++로 고유하게 업데이트합니다.

	```
	"copilotAgents": {
			"declarativeAgents": [            
				{
					"id": "dcGeolocator",
					"file": "declarativeAgent.json"
				}
			]
		},

	```

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image27.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image28.png)

3.  다음으로, **appPackage/instruction txt** 파일을 열고, 기존 내용을
    덮어쓰도록 아래 지침을 복사해 붙여넣으세요.

	```
	System Role: You are the game host for a geo-location guessing game. Your goal is to provide the player with clues about a specific city and guide them through the game until they guess the correct answer. You will progressively offer more detailed clues if the player guesses incorrectly. You will also reference PDF files in special rounds to create a clever and immersive game experience.

	Game play Instructions:

	Game Introduction Prompt

	Use the following prompt to welcome the player and explain the rules:

	Welcome to the Geo Location Game! I’ll give you clues about a city, and your task is to guess the name of the city. After each wrong guess, I’ll give you a more detailed clue. The fewer clues you use, the more points you score! Let’s get started. Here’s your first clue:

	Clue Progression Prompts

	Start with vague clues and become progressively specific if the player guesses incorrectly. Use the following structure:

	Clue 1: Provide a general geographical clue about the city (e.g., continent, climate, latitude/longitude).

	Clue 2: Offer a hint about the city’s landmarks or natural features (e.g., a famous monument, a river).

	Clue 3: Give a historical or cultural clue about the city (e.g., famous events, cultural significance).

	Clue 4: Offer a specific clue related to the city’s cuisine, local people, or industry.

	Response Handling

	After the player’s guess, respond accordingly:
	If the player guesses correctly, say:

	That’s correct! You’ve guessed the city in [number of clues] clues and earned [score] points. Would you like to play another round?

	If the guess is wrong, say:

	Nice try! [followed by more clues]

	PDF-Based Scenario

	For special rounds, use a PDF file to provide clues from a historical document, traveler's diary, or ancient map:

	This round is different! I’ve got a secret document to help us. I’ll read clues from this [historical map/traveler’s diary] and guide you to guess the city. Here’s the first clue:

	Reference the specific PDF to extract details:
	Traveler's Diary PDF,Historical Map PDF.
	Use emojis where necessary to have friendly tone. 
	Scorekeeping System

	Track how many clues the player uses and calculate points:

	1 clue: 10 points

	2 clues: 8 points

	3 clues: 5 points

	4 clues: 3 points

	End of Game Prompt

	After the player guesses the city or exhausts all clues, prompt:

	Would you like to play another round, try a special challenge?

	```

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image29.png)

4.  **appPackage/declarativeAgent.json** 파일에서 다음 줄을 확인하세요:

	"instructions": "$\[file('instruction.txt')\]",

	이 구문은 **instruction.txt** file. 파일의 지침을 불러옵니다. 패키지
파일을 모듈화하고 싶다면, **appPackage** 폴더 내의 다른 JSON 파일에서도
이 방식을 사용할 수 있습니다.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

### 작업 2: 대화 시작 문구 추가하기

선언형 에이전트에 대화 시작 문구(conversation starters)를 추가하면
사용자 참여를 높일 수 있습니다.

대화 시작 문구의 장점은 다음과 같습니다:

- **참여 유도**: 상호작용을 시작하는 데 도움을 주어 사용자가 더 편안하게
  느끼고 참여를 유도합니다.

- **문맥 설정**: 시작 문구는 대화의 주제와 흐름을 설정해 사용자가 이후
  대화를 어떻게 진행할지 방향을 제시합니다.

- **효율성**: 명확한 초점을 제공함으로써 모호성을 줄이고 대화가 원활하게
  진행되도록 합니다.

- **사용자 유지**:  잘 설계된 시작 문구는 사용자의 관심을 유지하고
  AI와의 반복적인 상호작용을 유도합니다.

1.  **declarativeAgent.json** 파일을 열고 노드 바로 뒤에 쉼표를 추가하고
    Enter를 누른 다음 아래 코드를 붙여넣으세요.

	```
	"conversation_starters": [
		{ 
				"title": "Getting Started",
				"text":"I am ready to play the Geo Location Game! Give me a city to guess, and start with the first clue." 
			},
			{
				"title": "Ready for a Challenge",
				"text": "Let us try something different. Can we play a round using the travelers diary?"
			},
			{ 
				"title": "Feeling More Adventurous",
				"text": "I am in the mood for a challenge! Can we play the game using the historical map? I want to see if I can figure out the city from those ancient clues."
			}
		]

	```

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image31.png)

이제 에이전트에 대한 모든 변경이 완료되었으므로 테스트할 차례입니다.

2.  상단 메뉴에서 **Files** 를 클릭하고 **Save All**을 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image32.png)

### 작업 3: 앱 테스트

1.  앱을 테스트하려면 Visual Studio Code에서 Microsoft 365 Agents
    Toolkit 확장 프로그램으로 이동하세요. 그러면 왼쪽 창이 열립니다.
    **LIFECYCLE** 섹션에서**Provision**을 선택하세요. 이 과정을 통해
    Microsoft 365 Agents Toolkit이 게시를 얼마나 간편하게 만들어주는지
    직접 확인할 수 있습니다.

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image33.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image34.png)

2.  로그인하라는 메시지가 표시되면, 자격 증명을 사용하여 로그인하세요.

	![A screen shot of a computer AI-generated content may be
incorrect.](./media/image35.png)

3.  이 단계에서는 Microsoft 365 Agents Toolkit이 appPackage 폴더 내의
    모든 파일을 ZIP 파일로 패키징해 선언형 에이전트를 사용자의 앱
    카탈로그에 설치합니다.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image36.png)

4.  브라우저를 열고
    +++<https://m365.cloud.microsoft/chat/+++%C2%A0logged> 로
    이동해 개발자 테넌트 계정으로 로그인하세요. 왼쪽 창에서 Geo Locator
    Game을 선택하세요.

	![image](./media/image37.png)

5.  실행이 완료되면 에이전트와의 집중 채팅 창(focused chat window) 이
    열립니다. 아래 표시된 것처럼 대화 시작 문구가 표시되는 것을 확인할
    수 있습니다.

	![image](./media/image38.png)

6.  대화 시작 문구 중 하나를 선택하면, 해당 문구가 메시지 작성 상자에
    자동으로 입력되며 사용자는 “Enter” 키를 눌러 대화를 시작할 수
    있습니다.  
    이 단계에서 에이전트는 여전히 사용자의 도우미로서, 사용자가 직접
    실행할 때까지 대기합니다.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

7.  질문에 답하고 개발한 게임을 탐색해 보세요.

## 요약:

이 실습에서는 Microsoft 365 Agents Toolkit을 사용해 선언형 에이전트를
구축하고 에이전트의 기능을 테스트하는 방법을 배웠습니다.
