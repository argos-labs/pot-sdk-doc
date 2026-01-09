![top-header](Captures/top-header.png)

# ARGOS-Labs POT SDK2 on Windows, Linux, Mac

欢迎使用 ARGOS 低代码平台的 Python-to-Operation Toolset (POT) SDK2。本文档将向您展示如何通过您的 Python 解决方案开发并发布插件。

> * 除非另有说明，否则适用于 Windows、Linux 和 Mac。
> * 如有必要，会针对每个操作系统提供单独的说明。

## 开发环境构建
首先，新的 POT-SDK2 是使用 [uv](https://docs.astral.sh/uv/) 安装的。以下说明了使用 uv 的优势。

### 主要特点 (Highlights)
* 🚀 一个替代 pip, pip-tools, pipx, poetry, pyenv, twine, virtualenv 等的单一工具。
* ⚡️ 比 pip 快 10-100 倍。
* 🗂️ 提供全面的项目管理，带有通用锁文件。
* ❇️ 运行脚本，支持内联依赖元数据。
* 🐍 安装和管理 Python 版本。
* 🛠️ 运行和安装作为 Python 包发布的工具。
* 🔩 包含 pip 兼容接口，通过熟悉的 CLI 提升性能。
* 🏢 支持 Cargo 风格的工作空间，适用于可扩展项目。
* 💾 节省磁盘空间，带有用于依赖去重的全局缓存。
* ⏬ 可通过 curl 或 pip 安装，无需 Rust 或 Python。
* 🖥️ 支持 macOS, Linux 和 Windows。

### uv 安装方法

> 请参阅 uv 文档中的 [安装](https://docs.astral.sh/uv/getting-started/installation/) 部分。

#### Windows

运行命令窗口 (CMD.exe)，然后输入以下命令。

```bash
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

![uv 安装示例](./Captures2/01-prepare-win/010010-install-uv.png)

> 安装后，uv 命令可能不会立即生效，您可能需要打开一个新的命令窗口才能看到它生效。

#### Linux, Mac

运行终端 (Terminal)，然后输入以下命令。

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

![uv 安装示例](./Captures2/02-prepare-linux/010010-install-uv.png)

> 安装后，uv 命令可能不会立即生效，您可能需要打开一个新的终端才能看到它生效。

### Python 安装
当前运行 POT-SDK2 的默认 Python 解释器设置为 3.11。

使用 uv 安装 3.11 版本。

```bash
uv python install 3.11
```

按如下方式查看已安装的 Python 解释器。

```bash
uv python list
```

![uv python list](./Captures2/02-prepare-linux/010040-uv-python-list.png)

> 您可以安装任何您想要的 Python 版本，例如 `uv python install 3.13`。


### POT-SDK2 安装

使用 uv 工具安装 POT-SDK2。

#### 安装 alabs.ppm2

```bash
uv tool install --python 3.11 --extra-index-url https://pypi-official.argos-labs.com/simple --index-strategy unsafe-best-match alabs.ppm2
```
> 如果您想升级已安装的 alabs.ppm2 工具，请在上述命令中使用 `upgrade` 代替 `install`。

![alabs.ppm2 安装示例](./Captures2/02-prepare-linux/010052-install-ppm2-mac.png)


#### 安装 alabs.icon2

```bash
uv tool install --python 3.11 --extra-index-url https://pypi-official.argos-labs.com/simple --index-strategy unsafe-best-match alabs.icon2
```
> 如果您想升级已安装的 alabs.icon2 工具，请在上述命令中使用 `upgrade` 代替 `install`。

![alabs.icon2 安装示例](./Captures2/02-prepare-linux/010092-install-icon2-mac.png)


#### 确认安装

```bash
uv tool list --show-python
```

![uv tool list](./Captures2/02-prepare-linux/010102-uv-tool-list.png)

> 注意！Python 版本必须为 3.11.x，即必须安装为 3.11。


### IDE 安装

在之前的文档中，我们使用了 PyCharm 作为集成开发环境，但在本版本中，我们使用 Visual Studio Code。

> Google 的 `Antigravity` 或 CursorAI 的 `Cursor` 均基于 Visual Studio Code，因此它们的工作方式相同。
> 本文档中的示例是基于 `Antigravity` 编写的。

安装 Visual Studio Code 系列的 IDE。

## 模板下载

* 下载 `plugin-template2.zip` 并将其解压到您的工作空间。
* 假设它被解压到 `~/home/user~/work/plugin-template2`。

## 插件开发、调试、测试及构建

### 运行 IDE
* 运行 IDE。
* 使用 `Folder Open` 菜单打开解压后的 plugin-template2 文件夹。

![运行 IDE](./Captures2/03-ide/020010-start.png)

### 安装 Python 扩展
* 您需要安装 `Python Extension` 以进行 Python 开发和调试。

![安装 Python 扩展](./Captures2/03-ide/020012-python-extension.png)

### 构建 Python 虚拟环境
* 构建 Python 虚拟环境：使用您想要开发的 Python 版本构建虚拟环境。

![构建 Python 虚拟环境](./Captures2/03-ide/020020-uv-venv.png)

> * 在 IDE 中按 `Control+J` (Windows, Linux) 或 `Command+J` (Mac) 运行终端。
> * 在顶级文件夹 (`~/home/user~/work/plugin-template2`) 中运行命令 `uv venv -p 3.11`。
> * 您可以使用任何您想要的 Python 版本来代替 3.11。（3.8 或更高版本）

### 在 IDE 中设置 Python 解释器

* 使用 IDE 中的 `Python: Select Interpreter` 菜单设置 Python 解释器。
* 在 Linux 或 Mac 上，选择 `./.venv/bin/python`。 
* 在 Windows 上，选择 `.\.venv\Scripts\python.exe`。 

![在 IDE 中设置 Python 解释器](./Captures2/03-ide/020045-python-interpretor.png)

> * 查看右下角，您可以看到 `Python 3.11.x ('.venv': venv)`，这表明当前的 Python 解释器是一个虚拟环境。


### 安装必要包

* 在 IDE 中运行终端后，进入插件主源码 `__init__.py` 所在的路径。
* 在模板示例中，进入 `argoslabs/demo/helloworld`。
* 在 Linux 或 Mac 上，运行命令 `bash requirements.sh`。
* 在 Windows 上，运行命令 `requirements.bat`。

> 在 `requirements.txt` 文件中指定并安装插件开发所需的外部 Python 包。

![安装必要包](./Captures2/03-ide/020031-install-requirements.png)

### 调试

#### 创建或修改 launch.json

* 选择 IDE 左侧的 `Run and Debug` 图标，然后选择 `create a launch.json file`。
* 选择 `Python Debugger`，然后选择 `Python File Debug the current active Python file`。
* 然后，检查生成的 `launch.json` 文件并进行如下更改。

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

> * `args` 指定要传递给执行的 Python 文件的参数。出于演示目的，指定了 `Tom` 和 `Jerry`。根据需要进行指定。 
> * `cwd` 指定要执行的 Python 文件的当前工作目录。
> * `env` 指定要执行的 Python 文件的环境变量。指定了 `PYTHONPATH` 以便找到 `argoslabs...` 包。

![launch.json](./Captures2/03-ide/020050-launch.json.png)  

#### 运行调试

* 打开包含实际插件逻辑的 `__init__.py` 文件，按 `F9` 设置断点。（在演示中，它是 `argoslabs/demo/helloworld` 中的 `__init__.py` 文件。）
* 打开同一文件夹下的 `__main__.py` 文件，按 `F5` 运行。
* 然后，您可以调试设置了断点的 `__init__.py` 文件，如下所示。

![运行调试](./Captures2/03-ide/020080-debug.png)

### 测试

* 打开主逻辑所在的 `__init__.py` 下 `tests` 文件夹中的 `test_me.py` 测试文件。
* 该测试文件使用 Python 的 `unittest` 功能进行单元测试。
* 按 `F5` 执行测试。
* 通过全面添加成功以及失败案例来执行测试。

> 如果执行了测试，它将在随后的 `build` 过程中以相同的方式停止，因此您必须在此过程中成功执行测试。

![测试执行](./Captures2/03-ide/020120-test-debug.png)

### 图标及版本确认

#### 准备图标

* 检查工作文件夹中的 `icon-my.png` 文件。

> 实际上，与演示不同，请准备并使用一个适当的图标以显示在 STU 上。

![确认图标](./Captures2/03-ide/020090-icon-my.png)

#### 为 STU 生成图标

* 在 Linux 或 Mac 上，运行命令 `bash build-icon.sh`。
* 在 Windows 上，运行命令 `build-icon.bat`。

 ![为 STU 生成图标](./Captures2/03-ide/020100-build-icon.png)

然后您可以找到生成的 `icon.png` 文件，如下所示。

![确认图标](./Captures2/03-ide/020110-built-icon.png)

#### 确认版本

* 检查并修改 `setup.yaml` 中的 `version` 部分。
* 我们建议采用以下格式的版本。 
  * 如果当前时间是 2026 年 1 月 9 日上午 11:34，请设置为 `2026.109.1134`。

![确认版本](./Captures2/03-ide/020130-change-version.png)

### 构建

#### 确认用于构建的 Python 版本

* 在 Linux 或 Mac 上，打开 `build.sh` 文件。
* 在 Windows 上，打开 `build.bat` 文件。
* 检查并修改 `PYVER=3.11` 部分。
*   > 您必须使用与最初创建虚拟环境时相同的 Python 版本。
*   > 例如，如果在通过 `uv venv -p 3.13` 命令创建虚拟环境时使用的 Python 版本是 3.13，请设置 `PYVER=3.13`。 

![确认用于构建的 Python 版本](./Captures2/03-ide/020135-build-python-version.png)

#### 运行构建

* 在 Linux 或 Mac 上，运行命令 `bash build.sh`。
* 在 Windows 上，运行命令 `build.bat`。

构建过程如下：

* `clear-all`：删除之前创建的所有用于构建的虚拟环境。（`~/.alabs-ppm2/pot-venvs` 文件夹）
* `test`：在类似于 `~/.alabs-ppm2/pot-venvs/3.x` 的地方创建一个专门用于构建的虚拟环境，安装必要的 `requirements.txt` 包，然后执行 `tests\test_me.py` 测试。
* `plugin unique`：检查私有仓库或官方仓库 (`https://pypi-official.argos-labs.com`) 中是否已安装相同版本的插件。如果已存在，则停止构建。
* `build`：使用相同的构建专用虚拟环境 (`~/.alabs-ppm2/pot-venvs/3.x`) 构建插件。
* `upload`：将构建好的插件上传到私有仓库。

![运行构建](./Captures2/03-ide/020140-build.png)

> * 在查询是否已安装同名同版本的插件 (`plugin uniquey`) 以及上传到私有仓库的部分，会询问管理员账号和密码。

![账号确认](./Captures2/03-ide/020150-unique-user.png)

> 如果所有构建均成功执行，将出现以下 `Build all success!` 消息。

![构建成功](./Captures2/03-ide/020170-build-success.png)

## 编写您自己的插件

* `plugin-template2` 模板的插件包名为 `argoslabs.demo.helloworld`。
* 如果您想将此插件更改为（例如）`argoslabs.my.plugin`，请使用 IDE 左侧的 `Code Search` 工具在所有文件中按如下方式更改包名。

![代码搜索](./Captures2/03-ide/020200-change-pkg-name.png)

* 相应地，您还应该在 `argoslabs/demo/helloworld` 文件夹中将文件夹名从 `demo` 更改为 `my`，将 `helloworld` 更改为 `plugin`。
* 其余部分保持不变。
