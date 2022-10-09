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

若要使用 Cosmos DB，您必須在 Azure 訂用帳戶中佈建 Cosmos DB 帳戶。 在此練習中，您將佈建使用核心 (SQL) API 的 Cosmos DB 帳戶。

1. 在 Azure 入口網站中，選取左上方的 **[+ 建立資源]**，並搜尋 *Azure Cosmos DB*。  選取結果中的 **Azure Cosmos DB**，並選取 [建立]。
1. 在 **[核心 (SQL) - 建議]** 圖格中，選取 **[建立]**。
1. 輸入下列詳細資料，並選取 **[檢閱 + 建立]**：
    - **訂用帳戶**：若您使用沙箱，請選取 *[指引訂用帳戶]*。 否則，請選取您的 Azure 訂用帳戶。
    - **資源群組**：若您使用沙箱，請選取現有的資源群組 (名稱類似 *learn-xxxx...* )。否則，請使用您選擇的名稱建立新的資源群組。
    - **帳戶名稱**：輸入唯一名稱
    - **位置**：選擇任何建議位置
    - **容量模式**：佈建的輸送量
    - **套用免費層折扣**：若可用，請選取套用
    - **限制帳戶總輸送量**：取消選取
1. 驗證組態後，選取 **[建立]**。
1. 等候部署完成。 接著，移至所部署的資源。

## <a name="create-a-sample-database"></a>建立範例資料庫

*在此程序進行期間，請關閉入口網站所顯示的任何秘訣*。

1. 在新 Cosmos DB 帳戶的頁面左窗格中，選取 [資料總管]。
1. 在 [資料總管] 頁面中，選取 [啟動快速入門]。
1. 在 [新增容器] 索引標籤中，檢閱範例資料庫預先填入的設定，並選取 [確定]。
1. 觀察畫面底部面板的狀態，直到已建立 ** SampleDB** 資料庫及其 **SampleContainer** 容器 (可能需要一分鐘左右)。

## <a name="view-and-create-items"></a>檢視和建立項目

1. 在 [資料總管] 頁面中展開 **SampleDB** 資料庫和 **SampleContainer** 容器，並選取 [項目] 以查看容器中的項目清單。 項目代表位址，且各有唯一識別碼和其他屬性。
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

    您已了解如何使用 Azure 入口網站中的資料總管介面，在 Cosmos DB 資料庫中建立及查詢 JSON 實體。 在實際案例中，應用程式開發人員會使用眾多程式設計語言專屬的軟體發展工具組(SDK) 之一來呼叫核心 (SQL) API，並使用資料庫中的資料。

> **提示**：若您已完成探索 Azure Cosmos DB，則可刪除在此練習中建立的資源群組。
