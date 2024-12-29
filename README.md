# Obsidian_to_Anki  
이 플러그인은 텍스트 또는 마크다운 파일에서 플래시카드를 Anki로 추가하는 기능을 제공합니다. 
Obsidian에서 플러그인으로 실행하거나 명령줄에서 Python 스크립트로 실행할 수 있습니다. Obsidian 마크다운 문법을 염두에 두고 제작되었으며, **사용자 정의 플래시카드 문법**을 지원합니다.  
추가 예정 기능은 [Trello](https://trello.com/b/6MXEizGg/obsidiantoanki)에서 확인하세요.

기능 추가 요청은 lemonaatree@gmail.com 이나 코리안키 네이버 카페에서 제시해주세요.
https://cafe.naver.com/koreanki

## 시작하기  

설치 및 사용법에 대한 자세한 내용은 [Wiki](https://github.com/Pseudonium/Obsidian_to_Anki/wiki)를 참조하세요! 
아래는 기본적인 요약입니다.

---

## 설정  

### 모든 사용자  
1. [Anki](https://apps.ankiweb.net/)를 실행하고 원하는 프로필로 이동합니다.  
2. [AnkiConnect](https://git.foosoft.net/alex/anki-connect)를 설치합니다.  

### Obsidian 플러그인 사용자  
3. [Obsidian](https://obsidian.md/)을 다운로드합니다.  
4. '커뮤니티 플러그인' 목록에서 이 플러그인을 검색합니다.  
5. 플러그인을 설치합니다.  
6. Anki에서 *도구 > 추가 기능 > AnkiConnect > 설정*으로 이동하여 아래와 같이 구성합니다.  
<pre>
{
    "apiKey": null,
    "apiLogPath": null,
    "webBindAddress": "127.0.0.1",
    "webBindPort": 8765,
    "webCorsOrigin": "http://localhost",
    "webCorsOriginList": [
        "http://localhost",
        "app://obsidian.md"
    ]
}
</pre>  

7. 위 설정을 적용하려면 Anki를 다시 시작합니다.  
8. Anki가 실행 중인 상태에서 플러그인을 로드합니다. 이렇게 하면 플러그인 설정이 생성됩니다.  

**참고:** 이후 Obsidian을 실행할 때는 Anki가 실행 중이지 않아도 됩니다. 그러나 플러그인을 사용하려면 Anki가 백그라운드에서 실행 중이어야 합니다.  

플러그인을 실행하려면 Obsidian 리본 메뉴(예: '그래프 보기 열기', '퀵 스위처 열기'와 같은 버튼이 있는 곳)에서 Anki 아이콘을 찾으세요.  
사용법에 대한 추가 정보는 [Wiki](https://github.com/Pseudonium/Obsidian_to_Anki/wiki)를 확인하세요!  

### Python 스크립트 사용자  
3. 최신 버전의 [Python](https://www.python.org/downloads/)을 설치합니다.  
4. 신규 사용자는 [릴리스 페이지](https://github.com/Pseudonium/Obsidian_to_Anki/releases)에서 `obstoanki_setup.py`를 다운로드하고 스크립트를 설치하려는 폴더(예: 노트 폴더)에 저장합니다.  
5. 파일 탐색기에서 `obstoanki_setup.py`를 더블 클릭하여 실행합니다. 그러면 최신 버전의 스크립트와 필요한 종속 항목이 자동으로 다운로드됩니다. 기존 사용자는 기존 `obstoanki_setup.py`를 실행하여 최신 버전으로 업데이트할 수 있습니다.  
6. 아래의 권한 탭을 확인하여 스크립트를 실행할 수 있도록 설정합니다.  
7. 파일 탐색기에서 `obsidian_to_anki.py`를 더블 클릭하여 실행합니다. 그러면 설정 파일인 `obsidian_to_anki_config.ini`가 생성됩니다.  

#### 권한  
스크립트는 다음 작업을 수행할 수 있어야 합니다:  
* 스크립트가 설치된 디렉터리에 설정 파일 생성.  
* 사용 중인 디렉터리의 파일 읽기.  
* 사용 중인 디렉터리에 백업 파일 생성.  
* 사용 중인 디렉터리에서 파일 이름 변경.  
* 사용 중인 디렉터리에서 백업 파일 삭제.  
* 현재 작업 디렉터리를 일시적으로 변경(로컬 이미지 경로를 올바르게 확인하기 위해).  

---

## 주요 기능  

**현재 지원 기능** (Wiki에서 자세히 확인 가능):  
* **사용자 정의 노트 유형** - Anki의 기본 제공 6가지 노트 유형에 제한되지 않습니다.  
* **사용자 정의 스캔 디렉터리**  
  * 기본적으로 전체 Vault를 스캔합니다.  
  * 플러그인 설정을 통해 특정 디렉터리(하위 디렉터리 포함)로 스캔 범위를 제한할 수 있습니다.  
* **폴더 및 파일 무시**  
  * 무시할 파일 및 폴더를 지정할 수 있습니다.  
  * 플러그인 설정에서 [Glob 문법](https://en.wikipedia.org/wiki/Glob_(programming)#Syntax)을 사용해 설정 가능합니다.  
  * 예제:  
    * `**/*.excalidraw.md` - `.excalidraw.md`로 끝나는 모든 파일 무시.  
    * `Template/**` - `Template` 폴더(하위 폴더 포함)의 모든 파일 무시.  
    * `**/private/**` - Vault 내 `private` 폴더에 있는 모든 파일 무시.  

---  

**플래시카드 생성 문법 예제**와 추가 정보는 Wiki에서 확인하세요!  
