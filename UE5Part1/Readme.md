# Unreal study 


## 1. Hello Unreal
<details>
<summary>접기/펴기</summary>

- `Unreal Engine 5.1` 설치.
- `Visual Studio 2022`에 C++ 게임 개발 환경 설정.
- `Unreal Engine` 설정 변경
- `Edit`->`Editor Preferences` -> `General` -> `Region & Langeage` -> `Editor Language` -> `English`
- `Edit`->`Editor Preferences` -> `General` -> `Source Code` -> `Source Code Editor` -> `Visual Studio 2022`

- unreal engine은 기본적인 프로그램의 뼈대를 자체적으로 제공한다. 이 뼈대에 필요한 로직을 붙여넣는 것이 엔진을 사용한 개발의 기본이다.
- 엔진의 구조에 맞춰 적절한 클래스를 생성하여 투입해야 한다.
### 1. 1장의 목표
- Unreal Engine을 사용하여 새로운 프로젝트를 생성한다.
- 새로운 클래스를 생성하고, 이 클래스를 사용하여 문자열을 출력하는 기능을 구현한다.
- Unreal Engine의 기본적인 구조를 이해한다.
1.1 기본적인 흐름.
- Hello Unreal이라는 문자열을 출력하기 위해서, `GameInstance`라는 클래스를 사용한다.
- `GameInstance` 클래스를 상속받아 새로운 클래스를 생성하고, 문자열을 출력하는 기능을 작성한다.
- 생성한 클래스를 엔진에 끼워넣어 기본 `GameInstance`를 대체하여 프로그램을 초기화한다.
### 2. 실습
#### 2.1 프로젝트 생성
- Unreal Engine을 실행하고, 새로운 프로젝트를 생성한다.
- `Games` -> `Blank` -> `Next` -> `C++` -> `Create Project`
- 프로젝트명을 HelloUnreal로 설정하고, Create Project를 클릭하여 프로젝트를 생성한다.
- 프로젝트가 생성되면 Visual Studio가 실행되고, 솔루션을 빌드한다.
- Unreal Editor의 로드 시간을 줄이기 위해, 기본 그래픽 뷰를 제거한다.
	 `Edit` -> `Project Settings` -> `Maps & Modes` -> `Editor Startup Map` -> `None`
	 `Edit` -> `Project Settings` -> `Maps & Modes` -> `Game Default Map` -> `None`
#### 2.2 만들어진 솔루션의 구조
<details>
<summary>HelloUnreal</summary>

  ├─Binaries
  │  └─Win64
  ├─Config
  ├─Content
  │  ├─Collections
  │  └─Developers
  │      └─image
  │          └─Collections
  ├─DerivedDataCache
  │  └─VT
  ├─Intermediate
  │  ├─Build
  │  │  ├─BuildRules
  │  │  ├─Unused
  │  │  └─Win64
  │  │      ├─HelloUnrealEditor
  │  │      │  └─Development
  │  │      │      └─Engine
  │  │      └─UnrealEditor
  │  │          ├─Development
  │  │          │  └─HelloUnreal
  │  │          └─Inc
  │  │              └─HelloUnreal
  │  │                  └─UHT
  │  ├─Config
  │  │  └─CoalescedSourceConfigs
  │  ├─DatasmithContentTemp
  │  ├─ProjectFiles
  │  ├─ReimportCache
  │  └─ShaderAutogen
  │      ├─PCD3D_ES3_1
  │      ├─PCD3D_SM5
  │      └─PCD3D_SM6
  ├─Saved
  │  ├─Autosaves
  │  ├─Collections
  │  ├─Config
  │  │  ├─CrashReportClient
  │  │  │  ├─UECC-Windows-586224B542AD93AE59BF558673876E06
  │  │  │  └─UECC-Windows-62DED33F4ACC6C73866AB1A4E5611109
  │  │  └─WindowsEditor
  │  └─Logs
  └─Source
      └─HelloUnreal
</details>

#### 2.3 클래스 생성		
- 언리얼 에디터에서 `Tools` -> `New C	++ Class`를 선택.
- `All Classes`에서 `GameInstance`로 검색하여 선택 후	 `Next`를 클릭.
- 원하는 클래스명을 설정 한 후 `Create Class`를 클릭하면 새로 생성한 클래스를 포함해 프로젝트를 다시 빌드한다. 									
- 컴파일이 완료되면 `Visual Studio`에 `reload` 여부를 묻는 확인창이 출력되고, `reload all`을 선택해 솔루션을 다시 로드한다.
#### 2.4 기능 구현
- 엔진에 존재하는 `Init`메서드를 `override`한다. 이 때, 반드시 부모클래스인 `UGameInstance`의 `Init`메서드를 가장 먼저 호출 한 뒤에 기능을 추가해야 한다.
```c++
void UHelloUnrealGameInstance::Init()
{
	Super::Init();
	// TODO : 기능 작성
	// ...
}
```
- 게임상에 문자열을 출력하려면 에디터를 익혀야 하기 때문에, 당장은 로그를 출력하는 기능을 추가한다.
```c++
UE_LOG(LogTemp, Log, TEXT("%s"), TEXT("Hello Unreal!!!"));
```
- `UE_LOG`의 구조 : `UE_LOG(로그종류, 로그레벨, 출력할 문자열 포맷, 출력할 문자열)`
- `Unreal Engine`에서는 문자열을 2byte로 처리한다. 따라서 처리의 편의성을 위해 `TEXT`매크로를 사용한다.
#### 2.5 확인
- `Unreal Editor`에서 Edit -> Project Settings -> Maps & Modes -> Game Instance Class를 오늘 작성한 클래스로 설정한다.
- `Unreal Editor`를 다시 실행하고, Play버튼을 눌러 게임을 실행한다.
- `Output Log`에서 `Hello Unreal!!!`이라는 문자열이 출력되는지 확인한다.
	- `Output Log`는 `Window` -> `Developer Tools` -> `Output Log`에서 확인할 수 있다.
	- 제대로 로그가 출력되었는지 찾기 힘들 때, `Filter`를 설정하여 찾을 수 있다.
	- 혹은 `LogTemp`, 또는 내가 입력한 문자열을 검색하여 찾을 수 있다.
#### 2.6 주의사항
##### 2.6.1 컴파일 할 때의 주의사항.
- `*.h` (헤더)파일이 변경된 경우 : 언리얼 에디터를 종료하고 `Visual Studio`에서 컴파일한다.
- `*.cpp` (소스)파일이 변경된 경우 : `Ctrl`+`Alt`+`F11`을 입력해 언리얼 에디터의 라이브 코딩으로 컴파일한다.
</details>

## 2. Coding Standard
<details>
<summary>접기/펴기</summary>

### 2.1 코딩 표준이란
- 프로그램을 작성 할 때 지켜야 하는 규약. 명명 규칙, 작성 방법등을 정한 가이드라인이다.
- 절대적으로 좋은 규약은 없다.
- 가장 중요한 부분은 정해진 규약을 따르는 것이다.
- 한 프로젝트의 모든 코드는 한 사람이 만든 것 처럼 보여야 한다.
### 2.2 `Unreal Engine`의 코딩 표준
- `Unreal Engine` 자체적으로 정해진 표준이 있다.
- `Unreal Engine`의 코딩 표준은 `C++`의 표준과는 다르다.
- 따라서 사용하던 표준이 있다 하더라도 `Unreal Engine`으로 개발 할 때는 `Unreal Engine`의 표준을 따라야 한다.
- 
</details>