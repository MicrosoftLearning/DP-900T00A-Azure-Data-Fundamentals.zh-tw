---
lab:
  title: 探索 Microsoft Fabric 的即時分析
  module: Explore real-time analytics in Microsoft Fabric
---

# 探索 Microsoft Fabric 的即時分析

Microsoft Fabric 提供即時智慧，可讓您建立實時數據流的分析解決方案。 在此練習中，您將使用 Microsoft Fabric 中的即時智慧功能，從計程車公司內嵌、分析及可視化即時數據流。

此實驗室需要大約 **30** 分鐘才能完成。

> **注意**：您需要Microsoft [Fabric 租使用者](https://learn.microsoft.com/fabric/get-started/fabric-trial) 才能完成此練習。

## 建立工作區

使用 Fabric 中的數據之前，您必須建立已啟用 Fabric 容量的工作區。

1. 瀏覽至[瀏覽器中的 Microsoft Fabric 首頁](https://app.fabric.microsoft.com/home?experience=fabric)`https://app.fabric.microsoft.com/home?experience=fabric`，並使用您的 Fabric 認證登入。
1. 在左側功能表列，選取 [工作區]**** (圖示看起來類似 )。
1. 使用您選擇的名稱建立新的工作區，選取包含網狀架構容量的授權模式（*試用版*、 *進階*或 *網狀架構*）。
1. 當新工作區開啟時，應為空白。

    ![Fabric 中空白工作區的螢幕快照。](./images/new-workspace.png)

## 建立 Eventstream

現在您已準備好從串流來源尋找和內嵌實時數據。 若要這樣做，您將從網狀架構實時中樞開始。

> **提示**：第一次使用即時中樞時，可能會顯示一些 *入門* 提示。 您可以關閉這些專案。

1. 在左側功能表欄中，選取 **[即時** ] 中樞。

    即時中樞可讓您輕鬆尋找及管理串流數據的來源。

    ![網狀架構中即時中樞的螢幕快照。](./images/real-time-hub.png)

1. 在即時中樞的 **[連線到** ] 區段中，選取 **[數據源**]。
1. 尋找黃色 **計程車** 範例數據源，然後選取 [ **聯機**]。 然後在 [連線**精靈] 中**，為來源`taxi`命名並編輯預設事件數據流名稱，將其變更為 `taxi-data`。 與此數據相關聯的默認數據流會自動命名 *為 taxi-data-stream*：

    ![新事件數據流的螢幕快照。](./images/name-eventstream.png)

1. 選取 **[下一步** ]，並等候建立來源和事件串流，然後選取 [ **開啟事件串流**]。 Eventstream 會在設計畫布上顯示**計程車來源和 **taxi-data-stream****：

   ![Eventstream 畫布的螢幕快照。](./images/new-taxi-stream.png)

## 建立 eventhouse

eventstream 會內嵌實時庫存數據，但目前不會使用它執行任何動作。 讓我們建立一個 eventhouse，我們可以將擷取的數據儲存在數據表中。

1. 在左側功能表欄上，選取 [ **建立**]。 在 [*新增*] 頁面的 [即時 Inteligence *] 區段底下*，選取 **[Eventhouse**]。 為它指定您選擇的唯一名稱。

    >**注意**：如果未將 [ **建立]** 選項釘選到提要欄，您必須先選取省略號 （**...**） 選項。

    關閉顯示的任何提示或提示，直到您看到新的空白事件屋為止。

    ![新事件屋的螢幕快照](./images/create-eventhouse.png)

1. 請注意，在左側窗格中，您的 eventhouse 包含與 eventhouse 同名的 KQL 資料庫。 您可以為此資料庫中的即時數據建立數據表，或視需要建立其他資料庫。
1. 選取資料庫，並注意有相關聯的 *查詢集*。 此檔案包含一些可用來開始查詢資料庫中數據表的 KQL 查詢範例。

    不過，目前沒有數據表可查詢。 讓我們藉由將數據從 eventstream 取得到新的數據表來解決此問題。

1. 在 KQL 資料庫的主頁面中，選取 [ **取得數據**]。
1. 針對數據源，選取 **[Eventstream Existing eventstream > ******]。
1. 在 [ **選取或建立目的地數據表** ] 窗格中，建立名為 `taxi`的新數據表。 然後在 [ **設定資料來源]** 窗格中，選取您的工作區和 **計程車數據** 事件串流，並將連線 `taxi-table`命名為 。

   ![從事件數據流載入數據表的組態螢幕快照。](./images/configure-destination.png)

1. 使用 [ **下一步** ] 按鈕完成步驟來檢查數據，然後完成設定。 然後關閉組態視窗，以使用庫存資料表來查看您的事件存放區。

   ![具有數據表的和 eventhouse 螢幕快照。](./images/eventhouse-with-table.png)

    已建立數據流與數據表之間的連線。 讓我們在 eventstream 中確認 。

1. 在左側功能表欄中，選取 **[即時** 中樞]，然後檢視 [ **我的數據流]** 頁面。 在 taxi-data-stream 數據流**數據流的 **...** 功能表中，選取 [**開啟事件串流**]。**

    eventstream 現在會顯示數據流的目的地：

   ![具有目的地的事件串流螢幕快照。](./images/eventstream-destination.png)

    > **提示**：選取設計畫布上的目的地，如果未顯示任何數據預覽，請選取 [ **重新整理**]。

    在此練習中，您已建立非常簡單的事件串流，以擷取實時數據並將其載入數據表中。 在實際的解決方案中，您通常會新增轉換，以匯總時態時間範圍的數據（例如，擷取每隻股票在五分鐘內的平均價格）。

    現在讓我們來探索如何查詢和分析擷取的數據。

## 查詢擷取的數據

Eventstream 會擷取即時計程車車資數據，並將其載入 KQL 資料庫中的數據表。 您可以查詢此資料表以查看擷取的數據。

1. 在左側功能表欄中，選取您的 Eventhouse 資料庫。
1. *選取資料庫的查詢集*。
1. 在查詢窗格中，修改第一個範例查詢，如下所示：

    ```kql
    taxi
    | take 100
    ```

1. 選取查詢程式代碼並加以執行，以查看資料表中的100個資料列。

    ![KQL 查詢的螢幕快照。](./images/kql-stock-query.png)

1. 檢閱結果，然後修改查詢以顯示每小時計程車取車次數：

    ```kql
    taxi
    | summarize PickupCount = count() by bin(todatetime(tpep_pickup_datetime), 1h)
    ```

1. 反白顯示修改過的查詢，然後執行它以查看結果。
1. 等候幾秒鐘后再執行它，指出取貨次數隨著新數據從即時串流新增至數據表而變更。

## 清除資源

在此練習中，您已使用事件串流建立 eventhouse、內嵌實時數據、查詢 KQL 資料庫數據表中擷取的數據、建立即時儀錶板以可視化實時數據，以及使用啟動器設定警示。

如果您已完成在 Fabric 中探索即時智慧，您可以刪除您為此練習建立的工作區。

1. 在左側的列中，選取工作區的圖示。
2. 在工具列中，選取 [ **工作區設定**]。
3. 在 [ **一般]** 區段中，選取 [ **移除此工作區**]。
