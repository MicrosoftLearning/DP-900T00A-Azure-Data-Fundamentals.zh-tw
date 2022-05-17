---
title: 線上託管說明
permalink: index.html
layout: home
ms.openlocfilehash: 928f59a9cdc6a3f70d5ad651fb1b5a45b405cee8
ms.sourcegitcommit: 1117342052bce0bbd5a703bd1f763862b9129807
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2022
ms.locfileid: "140682423"
---
# <a name="azure-data-fundamentals-exercises"></a>Azure 資料基本概念練習

請使用下列連結完成 Microsoft 課程 [DP-900 *Microsoft Azure 資料基本概念*](https://docs.microsoft.com/learn/certifications/courses/dp-900t00)的實作教室練習。

您將需要 Microsoft Azure 訂用帳戶，以完成這些練習。 若您的講師沒有為您提供 Microsoft Azure 訂閱，您可以在 [https://azure.microsoft.com](https://azure.microsoft.com) 註冊免費試用版。

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| 模組 | 實驗室 |
| --- | --- | 
{% for activity in labs  %}| {{ activity.lab.module }} | [{{ activity.lab.title }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
