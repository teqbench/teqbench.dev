# System MongoDB Models

## Overview
Collection of common template and prop files for inclusion into .NET projects. The intention of these files is to have common .NET project configuration settings in a central location for easy inclusion into a project via a submodule.

# Contents
- [Developer Environment Setup](#Developer+Environment+Setup)
- [Usage](#Usage)
- [DevOps - Configurations, Builds and Deployments](#DevOps)
- [License](#License)

# Developer Environment Setup

## Tooling
- Text Editor, i.e. Visual Studio Code

## Dependencies
> [!NOTE]
> Referenced/restored via the project file

- none

# Usage
To be able to reference the prop and template files, a submodule must be added to a repository and the repository's .NET projects files updated with references to the props files. After adding the submodule, it must be initialized and/or updated.

## Add Submodule
To add submodule to a repo, from a terminal prompt, navigate to the repo root and issue the following command:

```bash
git submodule add https://github.com/teqbench/teqbench.dev.git .submodules/teqbench.dev
```

## Init Submodule
Adding a submodule to a repo, does NOT pull/update the submodule repo locally; it's necessary to initialize and update the submodule once it's added to the repo.

From a terminal prompt, navigate to the repo root and issue the following commands:

```bash
git submodule init
git submodule update
```

## Update Submodule
If the submodule origin repo is ever updated, it's necessary to update the submodule.

From a terminal prompt, navigate to the repo root and issue the following command:
```bash
git submodule update --remote
```

## Add Props Files To Project File

### .NET Sdk Project
```xml
<?xml version="1.0" encoding="utf-8"?>
<Project Sdk="Microsoft.NET.Sdk">
	<!--
	Import common project file settings via teqbench.dev submodule.
	-->
	<Import Project="../.submodules/teqbench.dev/TeqBench.Dev.Project.Config.props" />
	<Import Project="../.submodules/teqbench.dev/TeqBench.Dev.Project.Tooling.props" />
	<Import Project="../.submodules/teqbench.dev/TeqBench.Dev.Project.Packaging.props" />
	<Import Project="../.submodules/teqbench.dev/TeqBench.Dev.Project.Versioning.props" />

	<PropertyGroup>
		<RootNamespace>TeqBench.System.Data.NoSql.MongoDB.Models</RootNamespace>
		<AssemblyName>TeqBench.System.Data.NoSql.MongoDB.Models</AssemblyName>
	</PropertyGroup>
	<ItemGroup>
		<PackageReference Include="MongoDB.Bson" Version="2.23.1" />
	</ItemGroup>
</Project>
```

### .NET Test Project
```xml
<?xml version="1.0" encoding="UTF-8"?>
<Project Sdk="Microsoft.NET.Sdk">
	<!--
	Import common project file settings via teqbench.dev submodule.
    NOTE: Test project is NOT versioned nor packaged, so those props files are not referenced.
	-->
	<Import Project="../.submodules/teqbench.dev/TeqBench.Dev.Project.Config.props" />
	<Import Project="../.submodules/teqbench.dev/TeqBench.Dev.Test.Project.Config.props" />
	<Import Project="../.submodules/teqbench.dev/TeqBench.Dev.Test.Coverage.props" />
	<ItemGroup>
		<PackageReference Include="Microsoft.NET.Test.Sdk" Version="17.8.0" />
		<PackageReference Include="MSTest.TestAdapter" Version="3.1.1" />
		<PackageReference Include="MSTest.TestFramework" Version="3.1.1" />
		<PackageReference Include="Moq" Version="4.20.70" />
		<PackageReference Include="TeqBench.System.Data.NoSql.Models" Version="2.1.0" />
	</ItemGroup>
	<ItemGroup>
		<ProjectReference Include="..\src\TeqBench.System.Data.NoSql.MongoDB.Models.csproj" />
	</ItemGroup>
</Project>
```

# DevOps

## Branching Strategy
- GitHub Flow
  - [Introduction From GitHub](https://docs.github.com/en/get-started/quickstart/github-flow)
  - [Indepth Overview](https://githubflow.github.io)

## Branches
- main (production)

## Local - Build, Pack(age) & Deploy
- Prop files (and template files referenced via prop files) are imported via a .NET project's project file; no build, packaging, deployments are necessary for reference/inclusion.

# License
&copy; 2023 TeqBench. All source code in this repository is only allowed for use by TeqBench; other usage by internal or external parties requires written consent from TeqBench.
