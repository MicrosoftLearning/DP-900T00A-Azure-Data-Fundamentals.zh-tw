---
title: 線上託管說明
permalink: index.html
layout: home
---

# <a name="azure-data-fundamentals-exercises"></a>Azure 資料基本概念練習

這些實作練習是為了支援 [Microsoft Learn](https://docs.microsoft.com/training/) 上的訓練內容而設計。

如要完成這些練習，您需要有具備系統管理權限的 Microsoft Azure 訂閱。 您可以在 [https://azure.microsoft.com](https://azure.microsoft.com) 註冊免費試用。

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| 練習 |
| --- |
{% for activity in labs  %}| [{{ activity.lab.title }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
