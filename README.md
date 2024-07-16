# WebProject
This is a sample repo for dotnet/sdk#<TBD>

## Description
`WebProject` is an ASP .NET Core project targeting .NET 6 (doesn't matter much). The project disables the MSBuild editor cofig file generation through `<GenerateMSBuildEditorConfigFile>false</GenerateMSBuildEditorConfigFile>` ([dotnet/roslyn#43617](https://github.com/dotnet/roslyn/pull/43617)).When built with .NET 8 SDK, it fails with 
>error RZ3600: Invalid value ''' for RazorLangVersion

The MSBuild editor config generation is disabled on our real CI/CD pieplines for a good reason: the file creation fails for some projects because of a too long path exceeding Windows limit of 260 characters (yes we do have projects structured inside folders leading to long file paths).

## Excpected behavior
Build the project `dotnet build WebProject.csproj` using any version of **.NET 8 SDK**

>Build succeeded.
>    0 Warning(s)
>   0 Error(s)

## Actual behavior

> CSC : error RZ3600: Invalid value ''' for RazorLangVersion. Valid values include 'Latest' or a valid version in range 1
.0 to 8.0. [d:\git\web-sample\WebProject.csproj]
>
>Build FAILED.

