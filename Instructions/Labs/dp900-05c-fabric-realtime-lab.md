---
lab:
  title: 探索 Microsoft Fabric 中的即時分析
  module: Explore fundamentals of large-scale data analytics
---

# 探索 Microsoft Fabric 中的即時分析

在此練習中，您將探索 Microsoft Fabric 中的即時分析。

此實驗室需要大約 **25** 分鐘才能完成。

> **注意**：您需要 Microsoft Fabric 授權才能完成此練習。 如需如何啟用免費網狀架構試用版授權的詳細資訊，請參閱 [開始使用 Fabric](https://learn.microsoft.com/fabric/get-started/fabric-trial) 。 您將需要 Microsoft *學校* 或 *公司* 帳戶才能執行此動作。 如果您沒有帳戶，您可以[註冊 Microsoft Office 365 E3 或更高版本的試用版](https://www.microsoft.com/microsoft-365/business/compare-more-office-365-for-business-plans)。

## 建立工作區

使用 Fabric 中的資料之前，請先建立已啟用 Fabric 試用版的工作區。

1. 在 登入 [Microsoft Fabric](https://app.fabric.microsoft.com) `https://app.fabric.microsoft.com` 。
2. 在左側功能表列中，選取 [ **工作區** ] (圖示看起來類似于 &#128455;) 。
3. 使用您選擇的名稱建立新的工作區，並在 [ **進階** ] 區段中選取包含 Fabric 容量 (*試用版*、 *進階*或 *網狀架構*) 的授權模式。
4. 當您的新工作區開啟時，它應該是空的。

    ![Power BI 中空白工作區的螢幕擷取畫面。](./images/new-workspace.png)

## 建立 KQL 資料庫

現在您已擁有工作區，您可以建立 KQL 資料庫來儲存即時資料。

1. 在入口網站的左下角，切換至**即時分析**體驗。

    ![體驗切換器功能表的螢幕擷取畫面。](./images/fabric-real-time.png)

    即時分析首頁包含圖格，可用來建立即時資料分析的常用資產

2. 在即時分析首頁中，使用您選擇的名稱建立新的 **KQL Database** 。

    一分鐘之後，將會建立新的 KQL 資料庫：

    ![新 KQL 資料庫的螢幕擷取畫面。](./images/kql-database.png)

    目前資料庫中沒有資料表。

## 建立 eventstream

Eventstream 提供可調整且彈性的方式，從串流來源擷取即時資料。

1. 在左側功能表列中，選取 [ **首頁** ] 以取得即時分析體驗。
1. 在首頁上，選取圖格以建立具有您選擇的名稱的新 **Eventstream** 。

    在短時間內，會顯示事件串流的視覺化設計工具。

    ![Eventstream 設計工具的螢幕擷取畫面。](./images/eventstream-designer.png)

    視覺化設計工具畫布會顯示連線到事件串流的來源，接著會連線到目的地。

1. 在設計工具畫布上，于來源的 [ **新增來源** ] 清單中，選取 **[範例資料**]。 然後在 [ **範例資料** ] 窗格中，指定計程車名稱 **，** 然後選取 **黃色計程車** 範例資料 (，代表從計程車旅程) 收集的資料。 然後選取 [新增]。
1. 在設計工具畫布下方，選取 [ **資料預覽** ] 索引標籤以預覽從來源串流處理的資料：

    ![Eventstream 資料預覽的螢幕擷取畫面。](./images/eventstream-preview.png)

1. 在設計工具畫布上，于目的地的 [ **新增目的地** ] 清單中，選取 **[KQL 資料庫**]。 然後在 **[KQL 資料庫** ] 窗格中，指定目的地名稱 **taxi-data** ，然後選取您的工作區和 KQL 資料庫。 然後選取 **[建立並設定**]。
1. 在 [擷 **取資料** 精靈] 的 [ **目的地]** 頁面上，選取 [ **新增資料表** ]，然後輸入資料表名稱 **taxi-data**。 然後選取 **[下一步：來源**]。
1. 在 [ **來源]** 頁面上，檢閱預設資料連線名稱，然後選取 [ **下一步：架構**]。
1. 在 [ **架構** ] 頁面上，將 **[資料格式** ] 從 TXT 變更為 **JSON**，然後檢視預覽，以確認此格式會產生多個資料行。 然後選取 **[下一步：摘要**]。
1. 在 [ **摘要]** 頁面上，等候建立連續擷取，然後選取 [ **關閉**]。
1. 確認已完成的事件串流看起來像這樣：

    ![已完成 Eventstream 的螢幕擷取畫面。](./images/complete-eventstream.png)

## 查詢 KQL 資料庫中的即時資料

您的 eventstream 會持續填入 KQL 資料庫中的資料表，讓您能夠查詢即時資料。

1. 在左側功能表中樞中，選取您的 KQL 資料庫 (，或選取您的工作區，並在該處尋找您的 KQL 資料庫) 。
1. 在您的 eventstream () 所建立**計程車資料**資料表的 **...** 功能表中，選取 **[查詢資料表] > 過去 24 小時內內嵌的 [記錄**]。

    ![KQL 資料庫中 [查詢資料表] 功能表的螢幕擷取畫面。](./images/kql-query.png)

1. 檢視查詢的結果，這應該是 KQL 查詢，如下所示：

    ```kql
    ['taxi-data']
    | where ingestion_time() between (now(-1d) .. now())
    ```

    結果會顯示過去 24 小時內從串流來源內嵌的所有計程車記錄。

1. 以下列程式碼取代查詢編輯器上半部的所有 KQL 查詢程式碼：

    ```kql
    // This query returns the number of taxi pickups per hour
    ['taxi-data']
    | summarize PickupCount = count() by bin(tpep_pickup_datetime, 1h)
    ```

1. 使用 ** [&#9655; 執行** ] 按鈕來執行查詢並檢閱結果，以顯示每小時計程車取貨次數。

## 清除資源

如果您已完成在 Microsoft Fabric 中探索即時分析，您可以刪除您為此練習建立的工作區。

1. 在左側的列中，選取工作區的圖示，以檢視其包含的所有專案。
2. 在工具列的 **[...]** 功能表中，選取 **[工作區設定**]。
3. 在 **[其他]** 區段中，選取 **[移除此工作區**]。
