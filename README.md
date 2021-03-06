# C#, F# and Visual Basic project system

|Release|Branch|Unit Tests (Debug)|Unit Tests (Release)| Localization | Coverage (Debug)
|---|---|:--:|:--:|:--:|:--:|
|[15.9.x](docs/repo/roadmap.md)|[dev15.9.x](https://github.com/dotnet/project-system/tree/dev15.9.x)|[![Build Status](https://dev.azure.com/dnceng/public/_apis/build/status/dotnet/project-system/unit-tests.debug.batched?branchName=dev15.9.x&label=build)](https://dev.azure.com/dnceng/public/_build/latest?definitionId=152&branchName=dev15.9.x)|[![Build Status](https://dev.azure.com/dnceng/public/_apis/build/status/dotnet/project-system/unit-tests.release.batched?branchName=dev15.9.x&label=build)](https://dev.azure.com/dnceng/public/_build/latest?definitionId=153&branchName=dev15.9.x)|[![Build Status](https://dev.azure.com/dnceng/public/_apis/build/status/dotnet/project-system/unit-tests.debug.spainish.batched?branchName=dev15.9.x&label=build)](https://dev.azure.com/dnceng/public/_build/latest?definitionId=157&branchName=dev15.9.x)|[![codecov](https://codecov.io/gh/dotnet/project-system/branch/dev15.9.x/graph/badge.svg)](https://codecov.io/gh/dotnet/project-system/branch/dev15.9.x)
|[16.0 Preview 2](docs/repo/roadmap.md)|[dev16.0.x](https://github.com/dotnet/project-system/tree/dev16.0.x)|[![Build Status](https://dev.azure.com/dnceng/public/_apis/build/status/dotnet/project-system/unit-tests.debug.batched?branchName=dev16.0.x&label=build)](https://dev.azure.com/dnceng/public/_build/latest?definitionId=152&branchName=dev16.0.x) |[![Build Status](https://dev.azure.com/dnceng/public/_apis/build/status/dotnet/project-system/unit-tests.release.batched?branchName=dev16.0.x&label=build)](https://dev.azure.com/dnceng/public/_build/latest?definitionId=153&branchName=dev16.0.x)| [![Build Status](https://dev.azure.com/dnceng/public/_apis/build/status/dotnet/project-system/unit-tests.debug.spainish.batched?branchName=dev16.0.x&label=build)](https://dev.azure.com/dnceng/public/_build/latest?definitionId=157&branchName=dev16.0.x) |[![codecov](https://codecov.io/gh/dotnet/project-system/branch/dev16.0.x/graph/badge.svg)](https://codecov.io/gh/dotnet/project-system)
|[16.0 Preview 3](docs/repo/roadmap.md)|[master](https://github.com/dotnet/project-system/tree/master)|[![Build Status](https://dev.azure.com/dnceng/public/_apis/build/status/dotnet/project-system/unit-tests.debug.batched?branchName=master&label=build)](https://dev.azure.com/dnceng/public/_build/latest?definitionId=152&branchName=master)|[![Build Status](https://dev.azure.com/dnceng/public/_apis/build/status/dotnet/project-system/unit-tests.release.batched?branchName=master&label=build)](https://dev.azure.com/dnceng/public/_build/latest?definitionId=153&branchName=master)| [![Build Status](https://dev.azure.com/dnceng/public/_apis/build/status/dotnet/project-system/unit-tests.debug.spainish.batched?branchName=master&label=build)](https://dev.azure.com/dnceng/public/_build/latest?definitionId=157&branchName=master) |[![codecov](https://codecov.io/gh/dotnet/project-system/branch/master/graph/badge.svg)](https://codecov.io/gh/dotnet/project-system)
|[16.0 Preview 3](docs/repo/roadmap.md)|[contributors](https://github.com/dotnet/project-system/tree/contributors)|[![Build Status](https://dev.azure.com/dnceng/public/_apis/build/status/dotnet/project-system/unit-tests.debug.batched?branchName=contributors&label=build)](https://dev.azure.com/dnceng/public/_build/latest?definitionId=152&branchName=contributors)|[![Build Status](https://dev.azure.com/dnceng/public/_apis/build/status/dotnet/project-system/unit-tests.release.batched?branchName=contributors&label=build)](https://dev.azure.com/dnceng/public/_build/latest?definitionId=153&branchName=contributors)| |

[![Join the chat at https://gitter.im/dotnet/project-system](https://badges.gitter.im/dotnet/project-system.svg)](https://gitter.im/dotnet/project-system?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

This repository contains the new C#, F# and Visual Basic project system that has been rewritten on top of the [Common Project System (CPS)](https://github.com/microsoft/vsprojectsystem). In [Visual Studio 2017](https://www.visualstudio.com/vs/), this project system is used by default for Shared Projects (C# and Visual Basic), and .NET Core (C#, F# and Visual Basic) project types, however, [long term](docs/repo/roadmap.md) it will be the basis of all C#, F# and Visual Basic project types. For a list of feature differences between the project systems, see [Feature Comparison](https://github.com/dotnet/project-system/blob/master/docs/feature-comparison.md).

The existing C# and Visual Basic project systems (csproj.dll and msvbprj.dll), which first shipped back in Visual Studio.net nearly 15 years ago, have served us well but are:

- Native and COM-based
- Single threaded and bound to the UI thread
- Hard to extend outside of aggregation via the use of `<ProjectTypeGuids>` and [sub types (flavors)](https://docs.microsoft.com/en-us/visualstudio/extensibility/internals/project-types)
- Tied to Visual Studio

The new C#, F# and Visual Basic project system is:

- Managed and managed-interface based
- Multi-threaded, scalable, and responsive
- Easy to extend via the use of the  Managed Extensibility Framework (MEF) and composable. Many parties, including 3rd parties, can contribute to a single project system
- Hostable outside of Visual Studio

## What is a project system?
A project system sits between a project file on disk (for example, .csproj and .vbproj) and various Visual Studio features including, but not limited to, Solution Explorer, designers, the debugger, language services, build and deployment. Almost all interaction that occurs with files contained in a project file, happens through the project system.

There are many technologies that come together to make up the .NET project system:

- [MSBuild](https://github.com/microsoft/msbuild) provides the build engine and file format.
- [SDK](https://github.com/dotnet/sdk) provides the MSBuild tasks and targets needed to build .NET projects.
- [Common Project System](https://github.com/microsoft/vsprojectsystem) provides the base building blocks for the project system including (but not limited to) project tree, build and debugger coordination and Visual Studio integration.
- [Roslyn](https://github.com/dotnet/roslyn) provides C# and Visual Basic language support including compilers, IntelliSense, refactorings, analyzers and code fixes.
- [Visual F# tools](https://github.com/Microsoft/visualfsharp) provides F# language support.
- [CLI](https://github.com/dotnet/cli) is the .NET command-line interface for building, running and interacting with .NET projects.

![image](https://cloud.githubusercontent.com/assets/1103906/24277819/d1e48eba-1093-11e7-811f-ae5debcc1e6c.png)

## How do I engage and contribute?
We welcome you to try things out, [file issues](https://github.com/dotnet/roslyn-project-system/issues), make feature requests and join us in design conversations. If you are looking for something to work on, take a look at our [help wanted issues](https://github.com/dotnet/roslyn-project-system/issues?q=is%3Aopen+is%3Aissue+label%3A%22Help+Wanted%22) for a great place to start. Also be sure to check out our [contributing guide](CONTRIBUTING.md).

This project has adopted a code of conduct adapted from the [Contributor Covenant](http://contributor-covenant.org/) to clarify expected behavior in our community. This code of conduct has been [adopted by many other projects](http://contributor-covenant.org/adopters/). For more information see [Contributors Code of conduct](https://github.com/dotnet/home/blob/master/guidance/be-nice.md). 
