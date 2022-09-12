---
lab:
  title: 探索適用於 MySQL 的 Azure 資料庫
  module: Explore relational data in Azure
---

# <a name="explore-azure-database-for-mysql"></a>探索適用於 MySQL 的 Azure 資料庫

在此練習中，需在您的 Azure 訂用帳戶中佈建適用於 MySQL 資源的 Azure 資料庫。

此實驗室需要大約 **5** 分鐘才能完成。

## <a name="before-you-start"></a>開始之前

您將需要具有系統管理層級存取權的 [Azure 訂用帳戶](https://azure.microsoft.com/free)。

## <a name="provision-an-azure-database-for-mysql-resource"></a>佈建適用於 MySQL 的 Azure 資料庫資源

在此練習中，需佈建適用於 MySQL 資源的 Azure 資料庫。

1. In the Azure portal, select <bpt id="p1">**</bpt>&amp;#65291; Create a resource<ept id="p1">**</ept> from the upper left-hand corner and search for <bpt id="p2">*</bpt>Azure Database for MySQL<ept id="p2">*</ept>. Then in the resulting <bpt id="p1">**</bpt>Azure Database for MySQL<ept id="p1">**</ept> page, select <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.

1. Review the Azure Database for MySQL options that are available. Then for <bpt id="p1">**</bpt>Resource type<ept id="p1">**</ept>, select <bpt id="p2">**</bpt>Flexible Server<ept id="p2">**</ept> and select <bpt id="p3">**</bpt>Create<ept id="p3">**</ept>.

    ![適用於 MySQL 的 Azure 資料庫部署選項螢幕擷取畫面](images/mysql-options.png)

1. 在 [建立 SQL Database] 頁面上輸入下列值：
    - 訂用帳戶：選取 Azure 訂用帳戶。
    - **資源群組**：以您選擇的名稱建立新的資源群組。
    - 伺服器名稱：輸入唯一名稱
    - **區域**：您附近的任何可用位置。
    - **MySQL 版本**：保持不變。
    - **工作負載類型**：用於開發或興趣專案。
    - **計算 + 儲存體**：保持不變。
    - **可用性區域**：保持不變。
    - **啟用高可用性**：保持不變。
    -               [系統管理使用者名稱]：您的名稱
    -               [密碼] 和 [確認密碼]：複雜性合適的密碼

1. 選取 [下一步：**網路]**。

1. 在 [防火牆規則] 下，選取 [&#65291; 新增目前的用戶端 IP 位址]。

1. 選取 [檢閱 + 建立]，然後選取 [建立] 以建立您的 Azure MySQL 資料庫。

1. Wait for deployment to complete. Then go to the resource that was deployed, which should look like this:

    ![螢幕擷取畫面：Azure 入口網站，顯示適用於 MySQL 的 Azure 資料庫頁面。](images/mysql-portal.png)

1. 檢閱管理適用於 MySQL 的 Azure 資料庫資源的選項。

> **提示**：如果您已完成探索適用於 MySQL 的 Azure Database，則可刪除您在此練習中建立的資源群組。
