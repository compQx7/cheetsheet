
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


