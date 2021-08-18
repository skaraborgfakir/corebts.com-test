https://corebts.com/blog/how-to-use-dot-net-core-cli-create-multi-project/

logg:
git clone https://github.com/skaraborgfakir/corebts.com-test.git
cd corebts.com-test/
dotnet new gitignore
dotnet new sln -o .
dotnet new mvc -o MyWebApp.Client
dotnet new classlib -o MyWebApp.DataStore
dotnet new mstest -o MyWebApp.DataStoreTest
dotnet sln add ./MyWebApp.Client/MyWebApp.Client.csproj
dotnet sln add ./MyWebApp.DataStore/MyWebApp.DataStore.csproj
dotnet sln add ./MyWebApp.DataStoreTest/MyWebApp.DataStoreTest.csproj
dotnet add ./MyWebApp.Client/MyWebApp.Client.csproj reference ./MyWebApp.DataStore/MyWebApp.DataStore.csproj
dotnet add ./MyWebApp.DataStoreTest/MyWebApp.DataStoreTest.csproj reference ./MyWebApp.DataStore/MyWebApp.DataStore.csproj
// kör test av DataStore
dotnet test ./MyWebApp.DataStoreTest/MyWebApp.DataStoreTest.csproj
// kör webapp
dotnet run --project ./MyWebApp.Client/MyWebApp.Client.csproj --urls http://127.0.0.1:5002/
// publicera till apache
dotnet publish ./MyWebApp.Client/MyWebApp.Client.csproj -o /var/www/www.fakirenstenstorp.st/stefan/tmp/corebts.com
//  vilket inte fungerade direkt.
