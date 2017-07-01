**Please note:** This buildpack is an experimental project and is not officially supported.

# .NET Core 1.1+ Buildpack

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpack) for building [.NET Core](https://www.microsoft.com/net/core) apps using [`.csproj` files](https://docs.microsoft.com/en-us/dotnet/articles/core/tools/project-json).

## Usage with [HerokuCLI](https://devcenter.heroku.com/articles/heroku-cli)

Example usage:

    $ heroku create --buildpack https://github.com/PWNTechIT/heroku-dotnet1.1-buildpack-vs2017.git
    $ git push heroku master

The buildpack will detect your app as .NET Core if it has `.csproj`. 
If the source code you want to build contains multiple `.csproj` files, 
it will compile the `.csproj` that has the same name of your solution file `.sln`.

## Buildpack will publish your project as "Release" Build

    dotnet publish ${PROJECT_FILE} --output ${BUILD_DIR} --runtime ubuntu.14.04-x64 --configuration Release

## NuGet - Additional Package Sources needed

It will use `NuGet.Config` placed in root directory, when `dotnet restore` is called for restore NuGet packages where you can specify additional `<packageSources>`.

Example `NuGet.Config`:
```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <packageSources>
    <add key="NuGet" value="https://api.nuget.org/v3/index.json" />
	<add key="xxx" value="https://xxx/index.json" />
    <add key="yyy" value="https://yyy/index.json" />
  </packageSources>
</configuration>
```
