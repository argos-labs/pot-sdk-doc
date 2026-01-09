![top-header](Captures/top-header.png)

# ARGOS-Labs POT SDK2 (Windows, Linux, Mac 版)

ARGOS Low-code プラットフォーム用 Python-to-Operation Toolset (POT) SDK2 へようこそ。このドキュメントでは、Python ソリューションからプラグインを開発してリリースする方法について説明します。

> * 特に断りのない限り、Windows、Linux、Mac すべてに適用されます。
> * 必要に応じて、各オペレーティングシステムごとの個別の説明を添えます。

## 開発環境の構築
まず、新しい POT-SDK2 は [uv](https://docs.astral.sh/uv/) を使用してインストールします。以下に uv を使用することの利点について説明します。

### 主要特徴 (Highlights)
* 🚀 pip、pip-tools、pipx、poetry、pyenv、twine、virtualenv などを置き換える単一のツールです。
* ⚡️ pip より 10 ～ 100 倍高速です。
* 🗂️ ユニバーサルロックファイルによる包括的なプロジェクト管理を提供します。
* ❇️ インライン依存関係メタデータを使用してスクリプトを実行します。
* 🐍 Python のバージョンをインストールして管理します。
* 🛠️ Python パッケージとして公開されたツールを実行、インストールします。
* 🔩 慣れ親しんだ CLI とパフォーマンス向上のための pip 互換インターフェースが含まれています。
* 🏢 拡張可能なプロジェクトのための Cargo スタイルのワークスペースをサポートしています。
* 💾 依存関係の重複を排除するグローバルキャッシュを使用し、ディスク容量を効率的に利用します。
* ⏬ curl または pip を介して、Rust や Python なしでインストール可能です。
* 🖥️ macOS、Linux、Windows をサポートしています。

### uv のインストール方法

> uv ドキュメント内の [インストール](https://docs.astral.sh/uv/getting-started/installation/) を参照してください。

#### Windows

コマンドプロンプト (CMD.exe) を実行し、次のコマンドを入力します。

```bash
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

![uv インストール例](./Captures2/01-prepare-win/010010-install-uv.png)

> インストール後、uv コマンドがすぐに反映されない場合があります。その場合は、新しいコマンドプロンプトを立ち上げて反映を確認してください。

#### Linux, Mac

ターミナル (Terminal) を実行し、次のコマンドを入力します。

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

![uv インストール例](./Captures2/02-prepare-linux/010010-install-uv.png)

> インストール後、uv コマンドがすぐに反映されない場合があります。その場合は、新しいターミナルを立ち上げて反映を確認してください。

### Python のインストール
現在 POT-SDK2 が実行されるデフォルトの Python インタープリタは 3.11 に設定されています。

uv を使用して 3.11 バージョンをインストールします。

```bash
uv python install 3.11
```

インストールされた Python インタープリタを次のように確認します。

```bash
uv python list
```

![uv python list](./Captures2/02-prepare-linux/010040-uv-python-list.png)

> `uv python install 3.13` のように、お好みの Python バージョンをインストールできます。


### POT-SDK2 のインストール

uv ツールを使用して POT-SDK2 をインストールします。

#### alabs.ppm2 のインストール

```bash
uv tool install --python 3.11 --extra-index-url https://pypi-official.argos-labs.com/simple --index-strategy unsafe-best-match alabs.ppm2
```
> インストール済みの alabs.ppm2 ツールをアップグレードするには、上記のコマンドで `install` の代わりに `upgrade` を使用してください。

![alabs.ppm2 インストール例](./Captures2/02-prepare-linux/010052-install-ppm2-mac.png)


#### alabs.icon2 のインストール

```bash
uv tool install --python 3.11 --extra-index-url https://pypi-official.argos-labs.com/simple --index-strategy unsafe-best-match alabs.icon2
```
> インストール済みの alabs.icon2 ツールをアップグレードするには、上記のコマンドで `install` の代わりに `upgrade` を使用してください。

![alabs.icon2 インストール例](./Captures2/02-prepare-linux/010092-install-icon2-mac.png)


#### インストールの確認

```bash
uv tool list --show-python
```

![uv tool list](./Captures2/02-prepare-linux/010102-uv-tool-list.png)

> 注意! Python のバージョンが 3.11.x (3.11) でインストールされている必要があります。


### IDE のインストール

以前のドキュメントでは統合開発環境として PyCharm を使用していましたが、今回のバージョンでは Visual Studio Code を使用します。

> Google の `Antigravity` や CursorAI の `Cursor` はどちらも Visual Studio Code をベースにしているため、同様に動作します。
> 本ドキュメントの例は `Antigravity` をベースに作成されています。

Visual Studio Code 系列の IDE をインストールします。

## テンプレートのダウンロード

* `plugin-template2.zip` をダウンロードし、作業スペースに解凍してください。
* `~/home/user~/work/plugin-template2` に解凍されたものと想定します。

## プラグインの開発、デバッグ、テスト、ビルド

### IDE の実行
* IDE を実行します。
* `Folder Open` メニューを使用して、解凍された plugin-template2 フォルダを開いてください。

![IDE 実行](./Captures2/03-ide/020010-start.png)

### Python Extension のインストール
* Python の開発やデバッグのために `Python Extension` をインストールする必要があります。

![Python Extension インストール](./Captures2/03-ide/020012-python-extension.png)

### Python 仮想環境の構築
* Python 仮想環境の構築：開発したい Python バージョンで仮想環境を構築します。

![Python 仮想環境の構築](./Captures2/03-ide/020020-uv-venv.png)

> * IDE で `Control+J` (Windows, Linux) または `Command+J` (Mac) を押してターミナルを実行します。
> * 最上位フォルダ (`~/home/user~/work/plugin-template2`) で `uv venv -p 3.11` コマンドを実行します。
> * 3.11 の代わりに、お好みの Python バージョン (3.8 以上) を使用できます。

### IDE への Python インタープリタ設定

* IDE の `Python: Select Interpreter` メニューを使用して、Python インタープリタを設定します。
* Linux または Mac では `./.venv/bin/python` を選択します。 
* Windows では `.\.venv\Scripts\python.exe` を選択します。 

![IDE への Python インタープリタ設定](./Captures2/03-ide/020045-python-interpretor.png)

> * 右下を確認すると `Python 3.11.x ('.venv': venv)` と表示され、現在使用している Python インタープリタが仮想環境であることが確認できます。


### 必要パッケージのインストール

* IDE でターミナルを実行し、プラグインのメインソースがある `__init__.py` の場所に移動します。
* テンプレートの例では `argoslabs/demo/helloworld` に移動します。
* Linux または Mac では `bash requirements.sh` を実行します。
* Windows では `requirements.bat` を実行します。

> プラグイン開発に必要な外部 Python パッケージを `requirements.txt` ファイルに明記してインストールします。

![必要パッケージのインストール](./Captures2/03-ide/020031-install-requirements.png)

### デバッグ

#### launch.json の作成または修正

* IDE の左側のアイコンから `Run and Debug` を選択し、`create a launch.json file` を選択します。
* `Python Debugger` を選択し、`Python File Debug the current active Python file` を選択します。
* 作成された `launch.json` ファイルを確認し、次のように変更します。

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

> * `args` は実行する Python ファイルに渡す引数を指定します。デモ用に `Tom`、`Jerry` を指定しています。必要に応じて指定してください。 
> * `cwd` は実行する Python ファイルのカレントディレクトリを指定します。
> * `env` は実行する Python ファイルの環境変数を指定します。`argoslabs...` パッケージを見つけられるように `PYTHONPATH` を指定しています。

![launch.json](./Captures2/03-ide/020050-launch.json.png)  

#### デバッグの実行

* 実際のプラグインロジックが含まれている `__init__.py` ファイルを開き、`F9` を押してブレークポイントを指定します。(デモでは `argoslabs/demo/helloworld` にある `__init__.py` ファイルです。)
* 同じフォルダにある `__main__.py` ファイルを開き、`F5` を押して実行します。
* すると、次のようにブレークポイントが設定された `__init__.py` ファイルでデバッグできます。

![デバッグの実行](./Captures2/03-ide/020080-debug.png)

### テスト

* メインロジックが含まれている `__init__.py` の `tests` フォルダにある `test_me.py` テストファイルを開きます。
* このテストファイルは Python の `unittest` 機能を使用してユニットテストを実行します。
* `F5` を押してテストを実行します。
* 成功ケースだけでなく、失敗ケースも網羅的に追加してテストを実行してください。

> このテストが実行されると、その後の `build` プロセスでも同様に停止するため、この段階でテストを成功させる必要があります。

![テストの実行](./Captures2/03-ide/020120-test-debug.png)

### アイコンとバージョンの確認

#### アイコンの準備

* 作業フォルダにある `icon-my.png` ファイルを確認します。

> 実際にはデモと異なり、STU に表示される適切なアイコンを準備して置き換えて使用します。

![アイコンの確認](./Captures2/03-ide/020090-icon-my.png)

#### STU 用アイコンの生成

* Linux または Mac では `bash build-icon.sh` を実行します。
* Windows では `build-icon.bat` を実行します。

 ![STU 用アイコンの生成](./Captures2/03-ide/020100-build-icon.png)

生成された `icon.png` ファイルを確認します。

![アイコンの確認](./Captures2/03-ide/020110-built-icon.png)

#### バージョンの確認

* `setup.yaml` の `version` 部分を確認して修正します。
* 次のような形式のバージョンを推奨します。 
  * 現在時刻が 2026年1月9日 11時34分であれば、`2026.109.1134` に設定します。

![バージョンの確認](./Captures2/03-ide/020130-change-version.png)

### ビルド

#### ビルド用 Python バージョンの確認

* Linux または Mac では `build.sh` を開きます。
* Windows では `build.bat` を開きます。
* `PYVER=3.11` 部分を確認して修正します。
*   > 最初に仮想環境を作成したときと同じ Python バージョンを使用する必要があります。
*   > 例えば、`uv venv -p 3.13` コマンドで仮想環境を作成した際の Python バージョンが 3.13 であったなら、`PYVER=3.13` に設定します。 

![ビルド用 Python バージョンの確認](./Captures2/03-ide/020135-build-python-version.png)

#### ビルドの実行

* Linux または Mac では `bash build.sh` を実行します。
* Windows では `build.bat` を実行します。

ビルドプロセスは以下の通りです。

* `clear-all`: 以前に作成されたビルド用の仮想環境をすべて削除します。 (`~/.alabs-ppm2/pot-venvs` フォルダ)
* `test`: `~/.alabs-ppm2/pot-venvs/3.x` のような場所にビルド専用の仮想環境を作成し、必要な `requirements.txt` パッケージをインストールした後、`tests\test_me.py` テストを実行します。
* `plugin unique`: 同一バージョンのプラグインがプライベートリポジトリまたは公式リポジトリ (`https://pypi-official.argos-labs.com`) に既にインストールされているかを確認します。存在する場合はビルドを中断します。
* `build`: 同一のビルド用仮想環境 (`~/.alabs-ppm2/pot-venvs/3.x`) を使用してプラグインをビル드します。
* `upload`: ビルドされたプラグインをプライベートリポジトリにアップロードします。

![ビルドの実行](./Captures2/03-ide/020140-build.png)

> * 同一名の同バージョンが既にインストールされているかの調査 (`plugin uniquey`) と、プライベートリポジトリへのアップロード時に、スーパーバイザーのアカウントとパスワードを尋ねられます。

![ログイン確認](./Captures2/03-ide/020150-unique-user.png)

> すべてのビルドが成功すると、`Build all success!` メッセージが表示されます。

![ビルド成功](./Captures2/03-ide/020170-build-success.png)

## 独自のプラグイン作成

* `plugin-template2` テンプレートのプラグインパッケージ名は `argoslabs.demo.helloworld` です。
* このプラグインを、例えば `argoslabs.my.plugin` のように変更したい場合は、IDE 左側の `Code Search` ツールを使用して、次のようにすべてのファイルでパッケージ名を変更して作業してください。

![コード検索](./Captures2/03-ide/020200-change-pkg-name.png)

* それに伴い、`argoslabs/demo/helloworld` フォルダの名前も `demo` を `my` に、`helloworld` を `plugin` に変更する必要があります。
* その他は同様に作業します。
