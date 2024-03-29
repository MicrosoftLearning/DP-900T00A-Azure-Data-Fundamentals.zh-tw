---
lab:
  title: 探索 Microsoft Fabric 的即時分析
  module: Explore fundamentals of large-scale data analytics
---

# 探索 Microsoft Fabric 的即時分析

您將透過此練習探索 Microsoft Fabric 的即時分析。

此實驗室需要大約 **25** 分鐘才能完成。

> **注意**：您需要 Microsoft Fabric 授權才能完成此練習。 如需如何啟用免費 Fabric 試用版授權的詳細資訊，請參閱[開始使用 Fabric](https://learn.microsoft.com/fabric/get-started/fabric-trial)。 您需要 Microsoft *學校*或*公司*帳戶才能執行此動作。 如您尚未擁有，您可[註冊 Microsoft Office 365 E3 或更高版本的試用版](https://www.microsoft.com/microsoft-365/business/compare-more-office-365-for-business-plans)。

## 建立工作區

在運用 Fabric 的資料之前，請先啟用 Fabric 試用版並建立工作區。

1. 您可在 `https://app.fabric.microsoft.com` 登入 [Microsoft Fabric](https://app.fabric.microsoft.com)。
2. 在左側功能表列，選取 [工作區]**** (圖示看起來類似 )。
3. 以您選擇的名稱建立新工作區，在 [進階]**** 區段選取包含 Fabric 容量 (*試用版*、*進階版*或 *Fabric*) 的授權模式。
4. 當新工作區開啟時，應為空白。

    ![螢幕擷取畫面：Power BI 空白工作區。](./images/new-workspace.png)

## 建立 KQL 資料庫

現在您已擁有工作區，您可建立 KQL 資料庫來儲存即時資料。

1. 在入口網站左下方，切換至 [即時分析]**** 體驗。

    ![螢幕擷取畫面：體驗切換器功能表。](./images/fabric-real-time.png)

    即時分析首頁包含圖格，可用來建立即時資料分析的常用資產

2. 在即時分析首頁，使用您選擇的名稱建立新 **KQL 資料庫**。

    ![RTA 編輯器的螢幕快照，其中已醒目提示 [建立 KQL DB]。](./images/create-kql-db.png)

   您會看到儀錶板畫面，然後選取頂端的 [KQL 資料庫] 按鈕。

    ![螢幕擷取畫面：新 KQL 資料庫。](./images/kql-database.png)

    選取之後，您就會得到 [ ***新增 KQL 資料庫] 對話框，您可以在其中提供 KQL 資料庫*** 的名稱。

    ![新 KQL 資料庫名稱對話框的螢幕快照。](./images/name-kql-db.png)

   - 在此案例中，將資料庫命名為： `my_kql_db`
   - 按兩下， ***建立***
  
    在約一分鐘之後，將建立新 KQL 資料庫：

    目前資料庫無資料表。

## 建立 Eventstream

Eventstreams 提供可調整且彈性的方式，從串流來源擷取即時資料。

1. 在左側功能表列，選取 [首頁]**** 頁面以取得即時分析體驗。
1. 在首頁，選取圖格並以您選擇的名稱建立新 **Eventstream**。

    在短時間內，會顯示 Eventstream 的視覺化設計工具。

    ![螢幕擷取畫面：Eventstream 設計工具。](./images/eventstream-designer.png)

    視覺化設計工具畫布會顯示連線 Eventstream 的來源，而 Eventstream 接著會連線目的地。

1. 在設計工具畫布，於來源的 [新來源]**** 清單，選取 [範例資料]****。 然後在 [範例資料]**** 窗格，指定名稱 [計程車]****，然後選取 [黃色計程車]**** 範例資料 (代表從計程車車程收集的資料)。 然後選取 [新增]。
1. 在設計工具畫布下方，選取 [資料預覽]**** 索引標籤，預覽從來源串流的資料：

    ![螢幕擷取畫面：Eventstream 資料預覽。](./images/eventstream-preview.png)

1. 在設計工具畫布，於目的地的 [新目的地]**** 清單，選取 [KQL 資料庫]****。 然後在 [KQL 資料庫]**** 窗格，指定目的地名稱 [taxi-data]****，然後選取您的工作區與 KQL 資料庫。 然後選取 [建立並設定]****。
1. 在 [擷取資料]**** 精靈的 [目的地]**** 頁面，選取 [新增資料表]****，然後輸入資料表名稱 [taxi-data]****。 然後選取 [下一步：來源]****。
1. 在 [來源]**** 頁面，檢閱預設資料連線名稱，然後選取 [下一步：結構]****。
1. 在 [結構]**** 頁面，將 [資料格式]**** 從 TXT 變更為 [JSON]****，並檢視預覽，以便確認此格式會產生多個資料行。 選取 [下一步：摘要]****。
1. 在 [摘要]**** 頁面，等候建立連續擷取，然後選取 [關閉]****。
1. 確認已完成的 Eventstream 如下所示：

    ![螢幕擷取畫面：已完成的 Eventstream。](./images/complete-eventstream.png)

## 查詢 KQL 資料庫的即時資料

您的 Eventstream 會持續填入 KQL 資料庫的資料表，讓您能夠查詢即時資料。

1. 在左側功能表中樞，選取 KQL 資料庫 (或選取工作區，並在該處尋找 KQL 資料庫)。
1. 在 [計程車資料]**** 資料表 (已透過 Eventstream 建立) 的 [...]**** 功能表，選取 [查詢資料表 > 過去 24 小時內擷取的記錄]****。

    ![螢幕擷取畫面：KQL 資料庫的 [查詢資料表] 功能表。](./images/kql-query.png)

1. 檢視查詢結果，應為如下所示的 KQL 查詢：

    ```kql
    ['taxi-data']
    | where ingestion_time() between (now(-1d) .. now())
    ```

    結果會顯示過去 24 小時內從串流來源擷取的所有計程車記錄。

1. 以下列程式碼取代查詢編輯器上半部的所有 KQL 查詢程式碼：

    ```kql
    // This query returns the number of taxi pickups per hour
    ['taxi-data']
    | summarize PickupCount = count() by bin(todatetime(tpep_pickup_datetime), 1h)
    ```

1. 使用 [▷ 執行]**** 按鈕來執行查詢並檢閱結果，其中顯示每小時計程車搭載次數。

## 清除資源

如您已完成探索 Microsoft Fabric 的即時分析，您可刪除為此練習建立的工作區。

1. 在左側列，選取工作區圖示即可檢視其所包含的所有項目。
2. 在工具列的 [...]**** 功能表，選取 [工作區設定]****。
3. 在 [其他]**** 區段，選取 [移除此工作區]****。
