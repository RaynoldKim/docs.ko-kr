---
title: "dotnet-msbuild 명령 - .NET Core CLI"
description: "dotnet-msbuild 명령은 MSBuild 명령줄에 대한 액세스 권한을 제공합니다."
keywords: "dotnet-msmsbuild, CLI, CLI 명령, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 05/24/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: ffdc40ba-ef33-463e-aa35-b0af1fe615a2
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 1f02dcd779b9ed249ebd2fedb973383b1dcd8963
ms.contentlocale: ko-kr
ms.lasthandoff: 07/28/2017

---

# <a name="dotnet-msbuild"></a>dotnet-msbuild

## <a name="name"></a>이름

`dotnet-msbuild` - 프로젝트 및 모든 종속성을 빌드합니다.

## <a name="synopsis"></a>개요

`dotnet msbuild <msbuild_arguments> [-h]`

## <a name="description"></a>설명

`dotnet msbuild` 명령을 사용하면 모든 기능을 갖춘 MSBuild에 액세스할 수 있습니다.

이 명령에는 기존 MSBuild 명령줄 클라이언트와 정확히 동일한 기능이 있습니다. 옵션은 모두 동일합니다. [MSBuild 명령줄 참조](/visualstudio/msbuild/msbuild-command-line-reference)를 사용하여 사용 가능한 옵션에 대한 정보를 얻을 수 있습니다. 

## <a name="examples"></a>예제

프로젝트 및 해당 종속성을 빌드합니다.

`dotnet msbuild`

릴리스 구성을 사용하여 프로젝트 및 해당 종속성을 빌드합니다.

`dotnet msbuild /p:Configuration=Release`

게시 대상을 실행하고 `osx.10.11-x64` RID에 대해 게시합니다.

`dotnet msbuild /t:Publish /p:RuntimeIdentifiers=osx.10.11-x64`

SDK를 통해 포함된 모든 대상이 있는 전체 프로젝트를 확인합니다.

`dotnet msbuild /pp`

