# Language

[Zonnon](http://zonnon.ethz.ch/) is a general-purpose programming language in the Pascal, Modula-2 
and Oberon family with focus on concurrency and ease of composition. Its conceptual model based on modules, 
objects, definitions and implementations. Its computing model based on active objects with 
their interaction defined by syntax controlled dialogs. It also features mathematical data 
types and operations as first-class language citizens.

# Command Line Compiler for .NET 10

This project is a fork of the ETH Zonnon compiler without Visual Studio integration. The solution
targets .NET 10. The command-line compiler and test runner use the bundled Mono CCI assemblies and
compile with the `ROTOR` symbol, which excludes the Visual Studio language-service integration.
OpenCL can also be used for computations with mathematical data types.

## Build

### Prerequisites

- Git
- .NET 10 SDK

Check that the .NET SDK is installed and available on `PATH`:

```powershell
dotnet --version
```

The command should report a `10.x` SDK version.

### Clone, restore, and build

Clone the repository into a directory where you want to keep it, then enter the checkout:

```powershell
git clone https://github.com/zonnonproject/compiler.git
cd compiler
```

From the repository root (the directory containing `solution`), restore dependencies and build:

```powershell
dotnet restore solution/Zonnon.sln
dotnet build solution/Zonnon.sln --configuration Release
```

To build an existing checkout, skip the `git clone` and `cd` commands. The solution build produces
the compiler, runtime library, and test runner under their respective `bin/Release/net10.0`
directories.

### Run the compiler

Pass compiler arguments after `--`:

```powershell
dotnet run --project solution/CommandLine/ETH.Zonnon.CommandLineCompiler.csproj --configuration Release -- [compiler options]
```

### Run the test suite

The test runner compiles the tests under `testsuite` and writes generated binaries to `temp`:

```powershell
dotnet run --project solution/Tester/Tester.csproj --configuration Release -- /testdir:testsuite /binarydir:temp
```

## Source code and CCI

This repository does not include the CCI source code. It includes three precompiled CCI libraries
for .NET and three for Mono; the .NET 10 projects reference the bundled Mono assemblies. The
compiler does not work with the latest public version of [CCI](https://github.com/microsoft/cci),
so use the bundled assemblies or a compatible CCI version. The older [Spec# project](http://specsharp.codeplex.com/)
contains similar CCI source, with additional code that may not be relevant to Zonnon.

## Licenses

The Zonnon compiler and runtime source files carry notices identifying the **[Microsoft Public
License (MS-PL)](https://opensource.org/license/ms-pl)**. When redistributing this source, retain
its copyright and attribution notices and include the complete MS-PL text with the distribution.
The repository also contains some BEL test-suite files marked **[GNU Lesser General Public License,
version 3 or (at your option) any later version](https://www.gnu.org/licenses/lgpl-3.0.html)**;
retain their notices and provide the LGPL terms for those files.

The bundled CCI assemblies in `solution/CCI` are third-party binaries. Their source and a separate
license notice are not included here, so verify and document the license for the specific binaries
before redistributing them. This repository contains components with different license notices;
do not treat every file as if it had one newly selected license.
