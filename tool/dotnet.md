
# コマンド操作

## ソリューション
ソリューションファイルの作成：
dotnet new sln
プロジェクトの追加：
dotnet sln add [.csprojのパス]

## プロジェクト作成
参照の追加：
dotnet add reference [.csprojのパス]
コンソールアプリの場合：
dotnet new console --framework net6.0

## 実行
起動：
dotnet run

## Test
各コマンドでテストプロジェクトを作成後、テスト対象プロジェクトへの参照追加、ソリューションにテストプロジェクトの追加

xUnit：
dotnet new xunit
NUnit：
dotnet new -i NUnit3.DotNetNew.Template
dotnet new nunit
MSTest：
dotnet new msunit

テスト実行：
dotnet test
・プロジェクトで実行するとプロジェクト内のテストを、ソリューションで実行すると（すべてのプロジェクト内のテストを実行。



# コマンド実行時に参照する設定情報

## `dotnet test` コマンド実行時
以下のファイルや設定が参照される。

* **プロジェクトファイル (.csproj など)**: プロジェクトファイルは、ビルドプロセスやテストの実行に必要な依存関係、プロパティ、ターゲットを定義します。

* **テストフレームワークの設定ファイル**: 使用しているテストフレームワーク（例：xUnit、NUnit、MSTest）に依存した設定ファイル。これらのファイルはテストの実行方法や特定のテスト設定を定義します。

* **appsettings.json または 同様の設定ファイル**: アプリケーションやテストの実行に必要な設定情報を含むファイル。環境変数やアプリケーションの設定が含まれます。

* **.runsettings または .testsettings ファイル**: MSTestを使用している場合、これらのファイルはテストの実行に関する追加設定を提供します。

* **global.json**: これは、特定の .NET SDK バージョンを指定するために使用されるファイルです。このファイルがある場合、`dotnet test`は指定されたSDKバージョンを使用します。

* **launchSettings.json**: このファイルは通常、開発環境の設定を含んでいますが、テスト実行時の環境変数などに影響を与えることがあります。

* **ユーザーの環境変数**: システムやユーザーの環境変数は、テストの実行に影響を与えることがあります。

これらのファイルや設定は、テストのビルドと実行に影響を与え、特定の挙動を定義するために重要です。プロジェクトやテストの要件に応じて、これらのファイルを適切に設定することが重要です。