# Unreal Engine Plugin

## Project Structure

### Directories

- Binaries
  - Compiled game libraries & debug databases
  - 컴파일 할 때마다 프로젝트의 .dll 파일 하나가 여기에 재생성됨.
- Config
  - Default configuration files
- Content
  - Content asset packages
- Intermediate
  - Temporary files
  - 언제든지 안전하게 삭제할 수 있음.
- Saved
  - Runtime configuration files & log files
- Source
  - C++ source code

### Files

- {ProjectName}.uproject
  - Project descriptor file
  - JSON 포맷 텍스트 파일로 프로젝트의 설명을 담고 있음.
- {ProjectName}.sln
  - Visual Studio solution file
- {ProjectName}.Target.cs
  - Build target configuration (Game)
- {ProjectName}Editor.Target.cs
  - Build target configuration (Editor)
- {ProjectName}.Build.cs
  - Build rules & configuration
- {ProjectName}.cpp / .h
  - Main project moduel implementation

### 플러그인과 프로젝트 구조 비교

<img src="C:\Users\devJoo\Documents\TIL\UnrealEngine\PluginTutorial\Images\Image1.png" alt="Image1" style="zoom:50%;" />

- 구조 공통점
  - Binaries
    - 플러그인의 컴파일된 바이너리가 포함됨
  - Content
  - Intermediate
  - Source
  - {PluginName}.uplugin
    - 플러그인 디스크립터
- 구조 차이점
  - Resource
    - 기본적으로 플러그인용 아이콘 하나만 가짐



## Modules & Engine Structure

- 프로젝트 혹은 플러그인에 작성한 모든 코드 파일들은 모듈안에 존재 해야함.
- 모듈은 디스크의 폴더 격으로 Build.cs 파일은 C# 파일과 함께 모듈의 컴파일 방식을 설명함.
- 프로젝트 혹은 플러그인을 컴파일할 때 UBT는 모든 모듈을 인터라이브러리로 컴파일하고 만드는 빌드가 모노리식인지 아니면 논모노리식인지에 따라 스태틱 라이브러리가 될 수도 있고 다이내믹 라이브러리가 될 수도 있음.
- Source 폴더 아래 있는 프로젝트 이름의 폴더가 또 있는 걸 확인할 수 있는데 이것은 기본 설정상 언리얼 엔진 런처가 프로젝트와 동일한 이름의 모듈 하나를 만들기 때문임.
  - 모듈에는 모듈 이름의 .h 파일과 .cpp파일, 그리고 컴파일 방식을 설명해주는 .cs파일도 있음
- 제작했던 플러그인에서 동일한 구조를 확인할 수 있음.

### Engine Structure

![Image2](C:\Users\devJoo\Documents\TIL\UnrealEngine\PluginTutorial\Images\Image2.png)

- Module Types
  1. Developer
     - For any applications, but used during development only
     - 모두 개발에만 사용하기로 의도된 모듈.
     - 디버깅 툴일 수도 있고 혹은 콘텐츠 제작자가 게임을 만들 때 사용하는 툴일 수도 있음.
     - 최종사용자에게는 절대 제공하지 않을 모듈임.
  2. Editor
     - For use Unreal Editor only
  3. Runtime
     - For any application at any time
     - 게임, 에디터, 또는 독립형 어플리케이션 등 어디서든 사용될 수 있는 모듈이 전부 들어있음.
     - 대부분 항상 필요한 핵심 기능들을 포함함.
  4. ThirdParty
     - Code and libraries from external third parties
     - 실제로 에픽에서 만들지 않은 모든 모듈이 포함됨.
     - 언리얼 엔진은 다른 회사와 사람들이 작성한 라이브러리도 많이 사용하기 때문에 굳이 기본적인 도구까지 새로 만들 필요가 없도록 하는 것.
- 맨 처음 새 코드 프로젝트나 코드 플러그인을 만들 때 모듈 하나가 만들어 질테지만 실제로 플러그인이나 프로젝트에 둘수 있는 모듈의 수에는 제한이 없음.
- 또한 가능하다면 코드 베이스를 다수의 모듈로 분해한 다음 그 용도를 나타내는 방식으로 다시 정리하는 것이 좋음.
- 예컨대 플러그인이 에디터에서만 사용하도록 의도된 기능을 가졌다면 에디터 특화 모듈에 넣고, 그렇지 않다면 런타임 모듈에 넣는 것임.

