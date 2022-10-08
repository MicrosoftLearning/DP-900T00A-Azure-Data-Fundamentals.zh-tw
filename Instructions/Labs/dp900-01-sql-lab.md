---
lab:
  title: 探索 Azure SQL Database
  module: Explore relational data in Azure
---

# <a name="explore-azure-sql-database"></a>探索 Azure SQL Database

在此練習中，您必須在您的 Azure 訂閱中佈建 Azure SQL 資料庫資源，然後使用 SQL 在關聯式資料庫中查詢資料表。

此實驗室需要大約 **15** 分鐘才能完成。

## <a name="before-you-start"></a>開始之前

您將需要具有系統管理層級存取權的 [Azure 訂用帳戶](https://azure.microsoft.com/free)。

## <a name="provision-an-azure-sql-database-resource"></a>佈建 Azure SQL Database 資源

1. 在 [Azure 入口網站](https://portal.azure.com?azure-portal=true)中，選取左上角的 [&#65291; 建立資源]，並搜尋 *Azure SQL*。 然後在產生的 [Azure SQL] 頁面中，選取 [建立]。

1. 檢閱可用的 Azure SQL 選項，然後在 [SQL資料庫] 圖格中，確定已選取 [單一資料庫]，然後選取 [建立]。

    ![Azure SQL 頁面的螢幕擷取畫面，其中顯示活動記錄。](images//azure-sql-portal.png)

1. 在 [建立 SQL Database] 頁面上輸入下列值：
    - 訂用帳戶：選取 Azure 訂用帳戶。
    - **資源群組**：以您選擇的名稱建立新的資源群組。
    -               [資料庫名稱]：AdventureWorks
    -                 **伺服器**：選取 [新建]，並在任何可用位置中建立具有唯一名稱的新伺服器。 使用 **SQL 驗證**，並將名稱指定為伺服器管理員登入，並設下合適複雜度的密碼 (請務必記住密碼，稍後會需要用到！)
    -               [想使用 SQL 彈性集區嗎？]：[否]
    -               [計算 + 儲存體]：保持不變
    -               [備份儲存體備援]：[本地異地備援備份儲存體]

1. 在 [建立 SQL Database] 頁面上，選取 [下一步：網路 >]，然後在 [網路] 頁面上的 [網路連線能力] 區段中，選取 [公用端點]。 然後，針對**防火牆規則**區段中的兩個選項選取 [是]，允許從 Azure 服務和您目前的用戶端 IP 位址存取資料庫伺服器。

1. 選取 [下一步：安全性 >]，並將 [啟用適用於 SQL 的 Microsoft Defender] 選項設定為 [暫時不要]。

1. 選取[下一步：其他設定 >]，然後在 [其他設定] 索引標籤上，將 [使用現有的資料] 選項設定為 [範例] (這會建立範例資料庫，供您稍後探索)。

1. 選取 [檢閱 + 建立]，然後選取 [建立] 以建立您的 Azure SQL 資料庫。

1. 等候部署完成。 然後前往已部署的資源，應會如下所示：

    ![Azure 入口網站的螢幕擷取畫面，其中顯示 SQL Database 頁面。](images//sql-database-portal.png)

1. 在頁面左側的窗格中，選取 [查詢編輯器(預覽)] ，然後使用您為伺服器指定的系統管理員登入名稱和密碼登入。
    
                  若顯示錯誤訊息且指出不允許用戶端 IP 位址，請選取訊息結尾的 [允許清單 IP…] 連結，允許存取並嘗試再次登入 (您先前已將電腦用戶端 IP 位址新增至防火牆規則，但查詢編輯器可能會根據網路設定從不同的位址連線。)
    
    查詢編輯器看起來像這樣：
    
    ![Azure 入口網站的螢幕擷取畫面，其中顯示查詢編輯器。](images//query-editor.png)

1. 展開 [資料表] 資料夾查看資料庫中的資料表。

1. 在 [查詢 1] 窗格中，輸入下列 SQL 程式碼：

    ```sql
    SELECT * FROM SalesLT.Product;
    ```

1. 選取查詢上方的 [&#9655; 執行] 執行並檢視結果，其中應該包含 **SalesLT.Product** 資料表中所有資料列的所有資料行，如下所示：

    ![Azure 入口網站的螢幕擷取畫面，其中顯示查詢編輯器和查詢結果。](images//sql-query-results.png)

1. 以下列程式碼取代 SELECT 陳述式，然後選取 [&#9655; 執行] 執行新的查詢，並檢閱結果 (其中僅包含 **ProductID**、**名稱**、**ListPrice**、**ProductCategoryID** 資料行)：

    ```sql
    SELECT ProductID, Name, ListPrice, ProductCategoryID
    FROM SalesLT.Product;
    ```

1. 現在請嘗試下列查詢，該查詢會使用 JOIN 從 **SalesLT.ProductCategory** 資料表取得類別名稱：

    ```sql
    SELECT p.ProductID, p.Name AS ProductName,
            c.Name AS Category, p.ListPrice
    FROM SalesLT.Product AS p
    JOIN [SalesLT].[ProductCategory] AS c
        ON p.ProductCategoryID = c.ProductCategoryID;
    ```

1. 關閉查詢編輯器窗格並捨棄編輯。

> **提示**：如果您已完成探索 Azure SQL Database，則可刪除您在此練習中建立的資源群組。
