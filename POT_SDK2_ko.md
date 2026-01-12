![top-header](Captures/top-header.png)

# ARGOS-Labs POT SDK2 on Windows, Linux, Mac

ARGOS Low-code 플랫폼용 Python-to-Operation Toolset (POT) SDK2에 오신 것을 환영합니다. 이 문서는 귀하의 Python 솔루션에서 플러그인을 개발하고 릴리스하는 방법을 보여줍니다.

> * 별도의 언급이 없으면 윈도우, 리눅스, 맥 모두 적용됩니다.
> * 필요한 경우 각 운영체제 별 별도의 설명을 곁들입니다.

## 개발 환경 구축
우선 새로운 POT-SDK2는 [uv](https://docs.astral.sh/uv/)를 사용하여 설치합니다.
다음은 uv를 사용하는 것에 대한 장점을 설명합니다.

### 주요 특징 (Highlights)
* 🚀 pip, pip-tools, pipx, poetry, pyenv, twine, virtualenv 등을 대체하는 단일 도구입니다.
* ⚡️ pip보다 10~100배 빠릅니다.
* 🗂️ 유니버설 락파일을 통한 포괄적인 프로젝트 관리를 제공합니다.
* ❇️ 인라인 의존성 메타데이터를 지원하여 스크립트를 실행합니다.
* 🐍 Python 버전을 설치하고 관리합니다.
* 🛠️ Python 패키지로 배포된 도구들을 실행하고 설치합니다.
* 🔩 익숙한 CLI와 성능 향상을 위한 pip 호환 인터페이스를 포함합니다.
* 🏢 확장 가능한 프로젝트를 위한 Cargo 스타일의 워크스페이스를 지원합니다.
* 💾 의존성 중복 제거를 위한 글로벌 캐시를 사용하여 디스크 공간을 효율적으로 사용합니다.
* ⏬ curl이나 pip를 통해 Rust나 Python 없이도 설치 가능합니다.
* 🖥️ macOS, Linux, Windows를 지원합니다.

### uv 설치 방법

> uv 문서 내의 (설치)[https://docs.astral.sh/uv/getting-started/installation/]를 참조하세요.

#### Windows

명령창(CMD.exe)를 실행한 다음, 다음 명령어를 입력합니다.

```bash
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

![uv 설치 예](./Captures2/01-prepare-win/010010-install-uv.png)

> 설치 후 uv 명령이 바로 적용되지 않고 새로운 명령창을 띄워야 적용된 것을 확인할 수 있습니다.

#### Linux, Mac

터미널(Terminal)를 실행한 다음, 다음 명령어를 입력합니다.

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

![uv 설치 예](./Captures2/02-prepare-linux/010010-install-uv.png)

> 설치 후 uv 명령이 바로 적용되지 않고 새로운 터미널을 띄워야 적용된 것을 확인할 수 있습니다.

### Python 설치
현재 POT-SDK2가 실행되는 기본 파이썬 인터프리터는 3.11에 맞추어져 있습니다.

uv를 사용하여 3.11 버전을 설치합니다.

```bash
uv python install 3.11
```

설치된 파이썬 인터프리터를 다음과 같이 확인합니다.

```bash
uv python list
```

![uv python list](./Captures2/02-prepare-linux/010040-uv-python-list.png)

> `uv python install 3.13` 과 같이 원하는 파이썬 버전을 설치할 수 있습니다.


### POT-SDK2 설치

uv tool을 이용하여 POT-SDK2를 설치합니다.

#### alabs.ppm2 설치

```bash
uv tool install --python 3.11 --extra-index-url https://pypi-official.argos-labs.com/simple --index-strategy unsafe-best-match alabs.ppm2
```
> 만약 설치된 alabs.ppm2 툴을 업그레이드하려면 위에 명령에서 `install` 대신 `upgrade`를 사용하면 됩니다.

![alabs.ppm2 설치 예](./Captures2/02-prepare-linux/010052-install-ppm2-mac.png)


#### alabs.icon2 설치

```bash
uv tool install --python 3.11 --extra-index-url https://pypi-official.argos-labs.com/simple --index-strategy unsafe-best-match alabs.icon2
```
> 만약 설치된 alabs.icon2 툴을 업그레이드하려면 위에 명령에서 `install` 대신 `upgrade`를 사용하면 됩니다.

![alabs.icon2 설치 예](./Captures2/02-prepare-linux/010092-install-icon2-mac.png)


#### 설치 된 것 확인

```bash
uv tool list --show-python
```

![uv tool list](./Captures2/02-prepare-linux/010102-uv-tool-list.png)

> 주의! 파이썬 버전이 3.11.x 로 3.11로 설치되어 있어야 합니다.


### IDE 설치

이전 문서에서는 통합 개발 환경으로 PyCharm을 사용했었지만 이번 버전에서는 Visual Studio Code를 사용합니다.

> Google의 `Antigravity` 또는 CursorAI의 `Cursor` 모두 Visual Studio Code를 기반으로 하기 때문에 동일하게 동작합니다.
> 본 문서의 예제는 `Antigravity`를 기반으로 작성되었습니다.

`Visual Studio Code` 계열의 IDE를 설치합니다.

## 템플릿 다운로드

* [플러그인 다운로드](./pugin-template2.zip) 을 다운받아 작업할 공간에 풀어주세요.
* `~/home/user~/work/plugin-template2` 에 압축 해지 되었다고 가정합니다.
> 일부 리눅스에서 unzip 명령이 없으면 unzip 패키지를 설치합니다. (예, `sudo apt install unzip`)

## Plugin 개발, 디버그, 테스트 및 빌드

### IDE 실행
* IDE를 실행합니다.
* `Folder Open` 메뉴를 이용하여 압축 해지된 plugin-template2 폴더를 열어주세요.

![IDE 실행](./Captures2/03-ide/020010-start.png)

### Python Extension 설치
* 파이썬 개발 및 디버깅 등을 위해 `Python Extension`을 설치해야 합니다.

![Python Extension 설치](./Captures2/03-ide/020012-python-extension.png)

### 파이썬 가상환경 구축
* 파이썬 가상환경 구축: 개발을 원하는 파이썬 버전으로 가상환경을 구축합니다.

![Python 가상환경 구축](./Captures2/03-ide/020020-uv-venv.png)

> * IDE에서 Control+J (윈도우, 리눅스) 또는 Command+J (맥)를 눌러서 터미널을 실행합니다.
> * 최상위 폴더 (`~/home/user~/work/plugin-template2`)에서 `uv venv -p 3.11` 명령어를 실행합니다.
> * 3.11 대신 원하는 파이썬 버전을 사용할 수 있습니다. (3.8 이상)

### IDE에 파이썬 인터프리터 설정

* IDE에서 `Python: Select Interpreter` 메뉴를 이용하여 파이썬 인터프리터를 설정합니다.
* 리눅스나 맥에서는 `./.venv/bin/python` 을 선택합니다. 
* 윈도우에서는 `.\.venv\Scripts\python.exe` 을 선택합니다. 

![IDE에 파이썬 인터프리터 설정](./Captures2/03-ide/020045-python-interpretor.png)

> * 하단 우측 부분을 확인해 보면 `Python 3.11.x ('.venv': venv)`로 표시되어 현재 사용하고 있는 파이썬 인터프리터가 가상환경인 것을 확인할 수 있습니다.


### 필요 패키지 설치

* IDE에서 터미널을 실행한 후 해당 플러그인 메인 소스가 있는 `__init__.py` 위치로 들어갑니다.
* 템플릿 예제에서는 `argoslabs/demo/helloworld` 위치로 들어갑니다.
* 리눅스나 맥에서는 `bash requirements.sh` 명령어를 실행합니다.
* 윈도우에서는 `requirements.bat` 명령어를 실행합니다.

> 플러그인 개발에 필요한 외부 파이썬 패키지를 `requirements.txt` 파일에 명시하여 설치합니다.

![필수 패키지 설치](./Captures2/03-ide/020031-install-requirements.png)

### 디버깅

#### lanunch.json 생성 또는 수정

* IDE의 좌측 아이콘 중 `Run and Debug`를 선택하고 `create a launch.json file`을 선택합니다.
* `Python Debugger`를 선택하고 `Python File Debug the current active Ptyhon file`을 선택합니다.
* 그러면 나오는 `lanunch.json` 파일을 확인하고 다음과 같이 변경합니다.

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: Current File",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "args": ["Tom", "Jerry"],
            "cwd": "${fileDirname}",
            "env": {
                "PYTHONPATH": "${workspaceFolder}",
            },
            "console": "integratedTerminal"
        }
    ]
}
```

> * `args`는 실행할 파이썬 파일에 전달할 인자값을 지정하는데 데모용으로 `Tom`, `Jerry`를 지정했습니다. 필요에 따라 지정합니다. 
> * `cwd`는 실행할 파이썬 파일의 현재 작업 디렉토리를 지정합니다.
> * `env`는 실행할 파이썬 파일의 환경 변수를 지정하는데 `PYTHONPATH`를 지정하여 `argoslabs...` 패키지를 찾도록 했습니다.

![lanunch.json](./Captures2/03-ide/020050-launch.json.png)  

#### 디버깅 실행

* 실제 플러그인 로직이 들어있는 `__init__.py` 파일을 열어 `F9`를 눌러 브레이킹 포인트를 지정합니다. (데모에서는 `argoslabs/demo/helloworld`에 있는 `__init__.py` 파일입니다.)
* 같은 폴더에 있는 `__main__.py` 파일을 열고 `F5`를 눌러 실행합니다.
* 그러면 다음과 같이 브레이킹 포인트가 설정된 `__init__.py` 파일이 디버그 할 수 있습니다.

![디버깅 실행](./Captures2/03-ide/020080-debug.png)

### 테스트

* 메인 로직이 들어있는 `__init__.py` 의 `tests` 폴더에 있는 `test_me.py` 테스트 파일을 엽니다.
* 해당 테스트 파일은 파이썬의 `unittest` 기능을 사용하여 단위 테스트를 수행합니다.
* `F5`를 눌러 테스트를 수행합니다.
* 성공 뿐만 아니라 실패 케이스도 촘촘하게 추가하여 테스트를 수행합니다.

> 해당 테스트가 수행되면 이후 진행될 `build` 과정에서도 동일하게 멈추게 되므로 이 과정에서 테스트를 성공적으로 수행해야 합니다.

![테스트 수행](./Captures2/03-ide/020120-test-debug.png)

### 아이콘 및 버전 확인

#### 아이콘 준비

* 작업 폴더에 있는 `icon-my.png` 파일을 확인합니다.

> 실제는 데모와 달리 STU에 표시될 적당한 아이콘을 준비해서 바꿔서 사용합니다.

![아이콘 확인](./Captures2/03-ide/020090-icon-my.png)

#### STU용 아이콘 생성

* 리눅스나 맥에서는 `bash build-icon.sh` 명령어를 실행합니다.
* 윈도우에서는 `build-icon.bat` 명령어를 실행합니다.

 ![STU용 아이콘 생성](./Captures2/03-ide/020100-build-icon.png)

그러면 아래와 같이 생성된 결과의 `icon.png` 파일을 확인할 수 있습니다.

![아이콘 확인](./Captures2/03-ide/020110-built-icon.png)

#### 버전 확인

* `setup.yaml`에 `version` 부분을 확인하여 수정합니다.
* 다음과 같은 방식의 버전을 추천합니다. 
  * 현재 시각이 2026년 1월 9일 11시 34분이라면 `2026.109.1134`로 설정합니다.

![버전 확인](./Captures2/03-ide/020130-change-version.png)

### 빌드

#### 빌드할 파이썬 버전 확인

* 리눅스나 맥에서는 `build.sh` 파일을 엽니다.
* 윈도우에서는 `build.bat` 파일을 엽니다.
* `PYVER=3.11` 부분을 확인하여 수정합니다.
*   > 처음에 가상환경을 만들 때 사용했던 동일한 파이썬 버전을 사용해야 합니다.
*   > 예를 들어, `uv venv -p 3.13` 명령어로 가상환경을 만들 때 사용한 파이썬 버전이 3.13이었다면 `PYVER=3.13`으로 설정합니다. 

![빌드할 파이썬 버전 확인](./Captures2/03-ide/020135-build-python-version.png)

#### 빌드 실행

* 리눅스나 맥에서는 `bash build.sh` 명령어를 실행합니다.
* 윈도우에서는 `build.bat` 명령어를 실행합니다.

빌드 과정은 다음과 같습니다.

* `clear-all`: 이전에 생성된 모든 빌드용 가상 환경을 삭제합니다. (`~/.alabs-ppm2/pot-venvs` 폴더)
* `test`: `~/.alabs-ppm2/pot-venvs/3.x` 와 같은 곳에 build를 위한 전용 가상환경을 만들고 필요 `requirements.txt` 패키지를 설치한 다음 `tests\test_me.py` 테스트를 수행합니다.
* `plugin unique`: 동일한 버전의 플러그인이 사설 저장소 또는 공식 저장소(`https://pypi-official.argos-labs.com`)에 이미 설치되어 있는지 확인합니다. 만약 있다면 build를 중단합니다.
* `build`: 동일한 build용 가상 환경(`~/.alabs-ppm2/pot-venvs/3.x`)을 사용하여 플러그인을 빌드합니다.
* `upload`: build된 플러그인을 사설 저장소에 업로드합니다.

![빌드 실행](./Captures2/03-ide/020140-build.png)

> * 해당 플러그인이 동일 이름의 같은 버전이 이미 설치되어 있는가를 조사하는 부분(`plugin uniquey`)과 사설 저장소로 업로드하는 부분에서 수퍼바이저의 계정과 암호를 물어봅니다.

![계정확인](./Captures2/03-ide/020150-unique-user.png)

> 모든 빌드가 성공적으로 수행되면 다음과 같이 `Build all success!` 메시지가 나옵니다.

![빌드 성공](./Captures2/03-ide/020170-build-success.png)

## 자신의 플러그인 작성

* `plugin-template2` 템플릿의 플러그인 패키지 이름은 `argoslabs.demo.helloworld`입니다.
* 이 플러그인을 예시로 `argoslabs.my.plugin` 과 같이 변경하려면 IDE 좌측의 `Code Search` 툴을 이용하여 다음과 같이 패키지 이름을 모든 파일에서 변경하고 작업하면 됩니다.

![코드 검색](./Captures2/03-ide/020200-change-pkg-name.png)

* 그에 따라 `argoslabs/demo/helloworld` 폴더에서 `demo` 대신 `my`, `helloworld` 대신 `plugin`으로 폴더 이름도 변경하여야 합니다.
* 나머지는 동일하게 작업하면 됩니다.

