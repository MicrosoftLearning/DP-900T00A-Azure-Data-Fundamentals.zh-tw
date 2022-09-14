---
lab:
  title: 探索 Azure Cosmos DB
  module: Explore fundamentals of Azure Cosmos DB
---
# <a name="explore-azure-cosmos-db"></a>探索 Azure Cosmos DB

在此練習中，您必須在自己的 Azure 訂閱中佈建 Azure Cosmos DB 資料庫，並探索各種使用該資料庫儲存非關聯式資料的方法。

此實驗室需要大約 **15** 分鐘才能完成。

## <a name="before-you-start"></a>開始之前

您將需要具有系統管理層級存取權的 [Azure 訂用帳戶](https://azure.microsoft.com/free)。

## <a name="create-a-cosmos-db-account"></a>建立 Cosmos DB 帳戶

To use Cosmos DB, you must provision a Cosmos DB account in your Azure subscription. In this exercise, you'll provision a Cosmos DB account that uses the core (SQL) API.

1. In the Azure portal, select <bpt id="p1">**</bpt>+ Create a resource<ept id="p1">**</ept> at the top left, and search for <bpt id="p2">*</bpt>Azure Cosmos DB<ept id="p2">*</ept>.  In the results, select <bpt id="p1">**</bpt>Azure Cosmos DB<ept id="p1">**</ept> and select  <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.
1. 在 **[核心 (SQL) - 建議]** 圖格中，選取 **[建立]**。
1. 輸入下列詳細資料，並選取 **[檢閱 + 建立]**：
    - <bpt id="p1">**</bpt>Subscription<ept id="p1">**</ept>: If you're using a sandbox, select <bpt id="p2">*</bpt>Concierge Subscription<ept id="p2">*</ept>. Otherwise, select your Azure subscription.
    - **資源群組**：若您使用沙箱，請選取現有的資源群組 (名稱類似 *learn-xxxx...* )。否則，請使用您選擇的名稱建立新的資源群組。
    - **帳戶名稱**：輸入唯一名稱
    - **位置**：選擇任何建議位置
    - **容量模式**：佈建的輸送量
    - **套用免費層折扣**：若可用，請選取套用
    - **限制帳戶總輸送量**：取消選取
1. 驗證組態後，選取 **[建立]**。
1. Wait for deployment to complete. Then go to the deployed resource.

## <a name="create-a-sample-database"></a>建立範例資料庫

*在此程序進行期間，請關閉入口網站所顯示的任何秘訣*。

1. 在新 Cosmos DB 帳戶的頁面左窗格中，選取 [資料總管]。
1. 在 [資料總管] 頁面中，選取 [啟動快速入門]。
1. 在 [新增容器] 索引標籤中，檢閱範例資料庫預先填入的設定，並選取 [確定]。
1. 觀察畫面底部面板的狀態，直到已建立 ** SampleDB** 資料庫及其 **SampleContainer** 容器 (可能需要一分鐘左右)。

## <a name="view-and-create-items"></a>檢視和建立項目

1. In the Data Explorer page, expand the <bpt id="p1">**</bpt>SampleDB<ept id="p1">**</ept> database and the <bpt id="p2">**</bpt>SampleContainer<ept id="p2">**</ept> container, and select <bpt id="p3">**</bpt>Items<ept id="p3">**</ept> to see a list of items in the container. The items represent addresses, each with a unique id and other properties.
1. 選取清單中的任何項目，以查看項目資料的 JSON 標記法。
1. 選取頁面頂端的 **[新增項目]**，以建立新的空白項目。
1. 修改新項目的 JSON (如下所示)，接著選取 **[儲存]**。

    ```json
    {
        "address": "1 Any St.",
        "id": "123456789"
    }
    ```

1. 請注意，儲存新項目後會自動新增其他中繼資料屬性。

## <a name="query-the-database"></a>查詢資料庫

1. 在 **[資料總管]** 頁面中，選取 **[新增 SQL 查詢]** 圖示。
1. 在 SQL 查詢編輯器中檢閱預設查詢 (`SELECT * FROM c`)，並使用 **[執行查詢]** 按鈕來執行查詢。
1. 檢閱結果，其中包含所有項目的完整 JSON 標記法。
1. 修改查詢如下：

    ```sql
    SELECT c.id, c.address
    FROM c
    WHERE CONTAINS(c.address, "Any St.")
    ```

1. 使用 [執行查詢] 按鈕來執行修訂的查詢並檢閱結果，其中包含 [位址] 欄位具有「Any St.」文字的項目 JSON 實體。
1. 關閉 SQL 查詢編輯器，捨棄您的變更。

    You've seen how to create and query JSON entities in a Cosmos DB database by using the data explorer interface in the Azure portal. In a real scenario, an application developer would use one of the many programming language specific software development kits (SDKs) to call the core (SQL) API and work with data in the database.

> **提示**：若您已完成探索 Azure Cosmos DB，則可刪除在此練習中建立的資源群組。
