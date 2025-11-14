# 실습 4 – Zava의 AI 통합 여정: Microsoft Copilot Studio에서 MCP 기반 에이전트 구축

## 시나리오:

빠르게 성장하는 디지털 헬스 조직인 Zava는 최근 내부 혁신 허브(**Internal
Innovation Hub**)를 설립해, 향후 규제된 의료 솔루션에 적용될 수 있는
새로운 AI 기능을 실험하고자 합니다. 민감한 의료 시스템을 연결하기 전에,
혁신 팀은 **Model Context Protocol(MCP)**을 사용해 외부 API 및 데이터
소스를 **Microsoft Copilot Studio**와 통합하는 방법을 학습할 수 있는
**안전하고 위험도가 낮은 샌드박스**가 필요합니다.

이를 위해 팀은 **간단하고 무해한 예제**인 *Jokes MCP Server*로
시작합니다. 이는 Copilot Studio가 MCP를 통해 실시간 API를 호출하는
방법을 보여줍니다. 이 가벼운 프로토타입은 엔지니어, 데이터 과학자 및 AI
솔루션 아키텍트가 다음을 이해하는 데 도움을 줍니다.

- MCP 서버를 Azure에 배포하는 방법

- Copilot Studio가 MCP 도구를 발견하고 활용하는 방법

- 실시간 외부 데이터를 에이전트에 안전하게 통합하는 방법

이 실습을 완료하면 Zava 혁신 팀은 향후 MCP 서버를 실제 비즈니스 시스템과
연결할 기반을 마련할 수 있습니다(규제 및 컴플라이언스 적용 후).

## 비즈니스 가치:

- 민감한 도메인에 적용하기 전 MCP 통합을 직접 경험하며 학습 가능

- 보안이 확보된 Azure 환경에서 엔드 투 엔드 배포 및 도구 활용 시연

- 차세대 AI 기반 워크플로우를 위한 조직 준비 강화

## 목표:

이번 실습에서는 Zava 혁신 허브가 MCP(Model Context Protocol)를 실험해
외부 API와 지식 소스를 Microsoft Copilot Studio와 연결하는 과정을
시뮬레이션합니다. MCP 서버를 Azure에 배포하고, Copilot Studio에서 도구로
등록하고, 대화형 에이전트에 통합하는 방법을 배웁니다.

이 실습을 완료하면:

- MCP가 Copilot Studio 에이전트에 실시간 데이터를 안전하게 통합하는
  방법을 이해

- Azure Developer CLI를 사용하여 MCP 서버를 배포, 구성, 연결하는 방법
  학습

- MCP 기반 도구를 Copilot Studio 에이전트에 추가하는 엔드 투 엔드
  워크플로우 탐색

## 연습 1: Azure에 MCP Server 배포

이번 실습에서는 로컬 개발 환경에서 **Microsoft MCP**(Model Context
Protocol) 서버를 Azure에 **배포**합니다. Azure Developer CLI(azd)를
사용해 **클라우드 호스팅 엔드포인트**를 생성하며, 이후 실습에서
**Copilot Studio** 또는 다른 애플리케이션에서 이 엔드포인트를 **활용**할
수 있습니다.

1.  Lab VM에서**Docker Desktop**을 여세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image1.png)

2.  **Visual Studio Code**을 열고 **OpenFolder**를 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image2.png)

3.  **mcsmcp**에 있는 **C:\LabFiles** 폴더를 선택한 후 **Select
    Folder**를 클릭하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image3.png)

4.  계속 진행하려면 **Yes, I trust the authors**를 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

5.  **VS Code**에서 **View** -\> **Terminal**을 선택해 터미널을 여세요.

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image5.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image6.png)

6.  터미널에 +++azd auth login+++을 입력해 **Azure**에 로그인하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image7.png)

7.  **Resources** 탭에 있는 계정 정보를 사용하여 **로그인**하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image8.png)

8.  +++azd up+++ 명령어를 입력하고 Enter 키를 눌러 프로젝트를 Azure에
    배포하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

9.  이름을 <+++mcsmcp@lab.LabInstance.Id>+++로 입력하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

10. 표시된 구독을 확인하고 **Enter** 키를 눌러 수락하세요.

	![A screen shot of a computer AI-generated content may be
incorrect.](./media/image11.png)

11. **@lab.CloudResourceGroup(ResourceGroup1).Location**을 위치로
    선택하세요.

12. 화살표 키를 사용해 지역 목록을 위아래로 스크롤하고 위 단계에서
    식별된 지역(**region**)을 선택한 후 **Enter**를 누르세요. 스크린샷의
    지역과 실습 VM에 할당된 지역은 다를 수 있습니다.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image12.png)

13. 이 단계는 Azure 포털에 필요한 리소스를 배포하며, 완료되면 성공
    메시지가 출력됩니다.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image13.png)

14. 출력 결과에는 **Endpoint url**도 제공됩니다. 이후 실습에서 사용할 수
    있도록 **메모장**에 **저장**하세요. 

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image14.png)

15. 해당 URL 끝 **/mcp**를 추가하고 브라우저에서 열어보세요. JSON 메시지
    안에 오류가 표시되더라도 괜찮습니다. 이는 MCP 서버에 정상적으로
    접근하고 있음을 의미합니다.

![](./media/image15.png)

이번 실습에서는 Visual Studio Code에서 MCP Server 프로젝트를 열고, Azure Developer CLI를 사용해 Azure에 인증한 후 azd up 명령으로 솔루션을 Azure에 배포했습니다. 이 배포 과정에서 컨테이너 앱과 관련 인프라 같은 필요한 Azure 리소스가 생성되었으며, MCP Server용 퍼블릭 엔드포인트 URL도 제공되었습니다. 브라우저에서 엔드포인트를 확인함으로써 배포와 연결이 성공적으로 이루어졌음을 검증했으며, 이후 실습에서 MCP Server를 다른 구성 요소와 통합할 수 있는 기반을 마련했습니다.

## 연습 2: Microsoft Copilot Studio에서 Jokes MCP Server 사용

### 작업 1: 커넥터 가져오기

**목표**

배포된 MCP Server와 통합하기 위해 **Power Apps**에서 **맞춤 MCP
커넥터**를 가져오고 구성합니다.

1.  +++https://make.preview.powerapps.com/customconnectors+++로
    이동하세요.

2.  **+ New custom connector** -\> **Import from GitHub**를 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image16.png)

3.  다음 세부 정보를 선택하세요.

    - **Connector Type – Custom**

    - **Branch – dev**

    - **Connector - MCP-Streamable-HTTP**

	**Continue**를 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image17.png)

4.  **Connector Name**을 +++**Jokes MCP**+++로 변경하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image18.png)

5.  이전에 저장한 URL에서 https:// 이후 부분을 **Host** 필드에
    붙여넣고, **Create connector**를 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image19.png)

	[!Alert] **Warning**

	성 과정에서 경고나 오류가 나타날 수 있지만, 곧 해결되므로 지금은
무시해도 됩니다.

6.  커넥터 창을 **닫으세요**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image20.png)

	![A screenshot of a computer AI-generated content may be incorrect.](./media/image21.png)

이번 작업에서는 GitHub에서 **MCP-Streamable-HTTP** 커넥터를 Power Apps로
가져오고, 이름을 **Jokes MCP**로 변경한 뒤, Azure에 호스팅된 MCP 서버
URL로 구성했습니다. 이를 통해 Power Platform과 MCP 서버 간 연결이
설정되어, 이후 작업에서 상호작용할 수 있는 기반이 마련됩니다.

### 작업 2: 에이전트 생성 및 MCP 서버 도구 추가

이번 작업에서는 Microsoft Copilot Studio에서 맞춤형 **Jokester**
에이전트를 구축하고, Model Context Protocol(MCP) 프레임워크를
사용해 **Jokes MCP Server**와 통합합니다. 이를 통해 에이전트가 연결된
MCP 엔드포인트에서 동적으로 농담을 가져와 제공할 수 있습니다.

1.  브라우저에서 **Copilot Studio**를 열고 URL
    +++[https://copilotstudio.microsoft.com+++](https://copilotstudio.microsoft.com+++/)로 접속한
    후, **Resources** **탭**의 자격 증명을 사용해 로그인하세요.
    Select **Get Started** 를 선택해 **trial** 라이선스를 활성화하세요.

	![A screenshot of a web page AI-generated content may be
incorrect.](./media/image22.png)

2.  **Create** -\> **+ New agent**를 선택하세요.

	![A screenshot of a phone AI-generated content may be
incorrect.](./media/image23.png)

3.  **Configure** 탭을 선택해 에이전트를 구성하세요.

	![A screenshot of a login page AI-generated content may be
incorrect.](./media/image24.png)

4.  아래 정보를 입력하고 **Create**를 선택하세요.

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

5.  제공한 정보를 기반으로 **에이전트**가 **생성**됩니다.

	![A logo of a company AI-generated content may be
	incorrect.](./media/image26.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image27.png)

6.  에이전트 페이지 우측 상단에서 **Settings**을 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

7.  **Settings** 창에서 **Use generative AI orchestration for your agent
    responses** 옵션을 **No**로 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image29.png)

8.  아래로 스크롤해 Knowledge 섹션에서 **Use general knowledge**와 **Use
    information from the Web** 옵션을 모두 비활성화하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

9.  위로 스크롤해 **Use generative AI orchestration for your agent
    responses** 옵션을 **Yes**로 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image31.png)

10. **Save**을 선택한 후 Settings 창을 **닫으세요**.

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image32.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image33.png)

11. 에이전트의 **Overview** 페이지에서 **Tools**를 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image34.png)

12. **+ Add a tool**를 선택해 에이전트에 새 도구를 추가하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image35.png)

13. Add a tool 창에서 **Model Context Protocol** 탭을 선택하세요.![A
    screenshot of a computer AI-generated content may be
    incorrect.](./media/image36.png)

14. 이전에 생성한 **Jokes MCP** Server를 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image37.png)

15. **Not connected** 옆의 **드롭다운**을 선택한 후 **Create new
    connection**을 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image38.png)

16. 다음 화면에서 **Create**를 선택하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

17. 연결이 완료되면 **Add to agent** 버튼을 선택해 MCP Server를 Jokester
    에이전트에 추가하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png)

18. 이제 **MCP Server**가 에이전트의 **도구**로 추가되었습니다.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

19. 이전트 동작을 테스트하기 전에 Test 창에서 **Refresh**를 선택하세요.

	![A screenshot of a phone AI-generated content may be
incorrect.](./media/image42.png)

20. +++Can I get a Chuck Norris joke?+++ 를 입력하고 **Send**를
    선택하세요.

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image43.png)

21. **Open connection manager**를 선택하세요.

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image44.png)

22. **Connect**를 선택해 연결을 설정하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

23. Jokes MCP 연결을 선택한 후 **Submit**을 클릭하세요.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

24. 이제 **Manage your connections** 페이지에서 Jokes MCP Server가
    **connected** 상태임을 확인할 수 있습니다.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image47.png)

25. 연결이 완료되었으므로, Test 창으로 돌아가서 **Retry**를 선택하세요.

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image48.png)

26. 이제 MCP 서버가 호출되는 것을 확인할 수 있으며, 에이전트가 Jokes MCP
    Server부터 응답을 생성하려고 시도합니다.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image49.png)

27. 에이전트가 **MCP Server**를 사용해 응답을 생성하고, 생성된 응답이
    **Test pane**에 **표시**됩니다.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image50.png)

이것은 **Microsoft Copilot Studio**에서 작동하는 **Jokes MCP
Server**입니다.

이번 과제에서는 Copilot Studio에서 **Jokester**라는 새로운 에이전트를
생성하고, 유머 생성용 목적과 동작 지침을 설정한 뒤, 지능형 응답을 위해
**Generative AI Orchestration**을 활성화했습니다. 이후 Model Context
Protocol을 통해 **Jokes MCP Server**를 도구로 연결하고, 인증을 완료한 뒤
테스트 패널에서 에이전트를 통해 농담을 가져오는 방식으로 통합을
성공적으로 검증했습니다. 이를 통해 MCP 서버가 Copilot Studio 환경 내에서
올바르게 연결되고 작동함을 확인할 수 있었습니다.

## 요약

이번 실습에서 Zava의 혁신 허브는 **Model Context Protocol(MCP)**이
Microsoft Copilot Studio에 실시간 외부 데이터 통합 기능을 확장할 수 있는
방법을 탐색했습니다. 안전하고 낮은 위험의 예제인 **Jokes MCP Server**를
시작으로, 참가자들은 Azure Developer CLI를 사용하여 MCP 서버를
**Azure**에 배포하고, 이를 커스텀 커넥터로 구성한 뒤 **Copilot Studio
에이전트** 내에서 활용하는 방법을 배웠습니다.

실습을 통해 참가자들은 Jokes MCP 서버에 안전하게 연결된 맞춤형
**Jokester** 에이전트를 생성하고, Copilot Studio가 MCP를 통해 라이브 API
호출을 수행할 수 있음을 확인했습니다. 또한 MCP 기반 도구를 설정, 인증,
테스트하는 실무 경험을 제공하여, 향후 기업 데이터 시스템과 통합되는 핵심
MCP 서버 구현을 위한 기초를 마련했습니다.
