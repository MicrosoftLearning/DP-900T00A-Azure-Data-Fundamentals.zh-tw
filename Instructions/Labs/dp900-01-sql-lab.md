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

1. In the <bpt id="p1">[</bpt>Azure portal<ept id="p1">](https://portal.azure.com?azure-portal=true)</ept>, select <bpt id="p2">**</bpt>&amp;#65291; Create a resource<ept id="p2">**</ept> from the upper left-hand corner and search for <bpt id="p3">*</bpt>Azure SQL<ept id="p3">*</ept>. Then in the resulting <bpt id="p1">**</bpt>Azure SQL<ept id="p1">**</ept> page, select <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.

1. 檢閱可用的 Azure SQL 選項，然後在 [SQL資料庫] 圖格中，確定已選取 [單一資料庫]，然後選取 [建立]。

    ![Azure SQL 頁面的螢幕擷取畫面，其中顯示活動記錄。](images//azure-sql-portal.png)

1. 在 [建立 SQL Database] 頁面上輸入下列值：
    - 訂用帳戶：選取 Azure 訂用帳戶。
    - **資源群組**：以您選擇的名稱建立新的資源群組。
    -               [資料庫名稱]：AdventureWorks
    - <bpt id="p1">**</bpt>Server<ept id="p1">**</ept>:  Select <bpt id="p2">**</bpt>Create new<ept id="p2">**</ept> and create a new server with a unique name in any available location. Use <bpt id="p1">**</bpt>SQL authentication<ept id="p1">**</ept> and specify your name as the server admin login and a suitably complex password (remember the password - you'll need it later!)
    -               [想使用 SQL 彈性集區嗎？]：[否]
    -               [計算 + 儲存體]：保持不變
    -               [備份儲存體備援]：[本地異地備援備份儲存體]

1. On the <bpt id="p1">**</bpt>Create SQL Database<ept id="p1">**</ept> page, select <bpt id="p2">**</bpt>Next :Networking &gt;<ept id="p2">**</ept>, and on the <bpt id="p3">**</bpt>Networking<ept id="p3">**</ept> page, in the <bpt id="p4">**</bpt>Network connectivity<ept id="p4">**</ept> section, select <bpt id="p5">**</bpt>Public endpoint<ept id="p5">**</ept>. Then select <bpt id="p1">**</bpt>Yes<ept id="p1">**</ept> for both options in the <bpt id="p2">**</bpt>Firewall rules<ept id="p2">**</ept> section to allow access to your database server from Azure services and your current client IP address.

1. 選取 [下一步：安全性 >]，並將 [啟用適用於 SQL 的 Microsoft Defender] 選項設定為 [暫時不要]。

1. 選取[下一步：其他設定 >]，然後在 [其他設定] 索引標籤上，將 [使用現有的資料] 選項設定為 [範例] (這會建立範例資料庫，供您稍後探索)。

1. 選取 [檢閱 + 建立]，然後選取 [建立] 以建立您的 Azure SQL 資料庫。

1. Wait for deployment to complete. Then go to the resource that was deployed, which should look like this:

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
