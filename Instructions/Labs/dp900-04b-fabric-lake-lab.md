---
lab:
  title: 探索 Microsoft Fabric 的資料分析
  module: Explore fundamentals of large-scale data analytics
---

# 探索 Microsoft Fabric 的資料分析

您將透過此練習探索 Microsoft Fabric Lakehouse 的資料擷取及分析。

此實驗室需要大約 **25** 分鐘才能完成。

> **注意**：您需要 Microsoft Fabric 授權才能完成此練習。 如需如何啟用免費 Fabric 試用版授權的詳細資訊，請參閱[開始使用 Fabric](https://learn.microsoft.com/fabric/get-started/fabric-trial)。 您需要 Microsoft *學校*或*公司*帳戶才能執行此動作。 如您尚未擁有，您可[註冊 Microsoft Office 365 E3 或更高版本的試用版](https://www.microsoft.com/microsoft-365/business/compare-more-office-365-for-business-plans)。

*第一次使用任何Microsoft Fabric 功能時，可能會出現提示提示的提示。關閉這些。*

## 建立工作區

在運用 Fabric 的資料之前，請先啟用 Fabric 試用版並建立工作區。

1. 您可在 `https://app.fabric.microsoft.com` 登入 [Microsoft Fabric](https://app.fabric.microsoft.com)。
1. 在功能表欄的左下方，切換至 **資料工程師** 體驗。

    ![螢幕擷取畫面：體驗切換器功能表。](./images/fabric-switcher.png)

1. 在左側功能表列，選取 [工作區]**** (圖示看起來類似 )。
1. 以您選擇的名稱建立新工作區，在 [進階]**** 區段選取包含 Fabric 容量 (*試用版*、*進階版*或 *Fabric*) 的授權模式。
1. 當新工作區開啟時，應為空白。

    ![螢幕擷取畫面：Power BI 空白工作區。](./images/new-workspace.png)

## 建立 Lakehouse

現在您已擁有工作區，現在可以為您的數據檔建立 Data Lakehouse。

1. 在工作區的首頁中，使用您選擇的名稱建立新的 **Lakehouse** 。

    在約一分鐘之後，將建立新 Lakehouse：

    ![螢幕擷取畫面：新 Lakehouse。](./images/new-lakehouse.png)

1. 檢視新 Lakehouse，並注意左側的 [Lakehouse 總管]**** 窗格可讓您瀏覽 Lakehouse 的資料表與檔案：
    - [資料表]**** 資料夾包含可利用 SQL 查詢的資料表。 Microsoft Fabric Lakehouse 的資料表是以 Apache Spark 常用的 *Delta Lake* 檔案格式為基礎。
    - [檔案]**** 資料夾包含 OneLake 儲存體的資料檔，且其與受管理差異資料表的 Lakehouse 無關。 您也可在此資料夾建立*捷徑*，以便參考外部儲存資料。

    Lakehouse 目前無資料表或檔案。

## 內嵌資料

擷取資料的簡單方式是，利用管線的**複製資料**活動從來源擷取資料，並將其複製到 Lakehouse 的檔案。

1. 在 Lakehouse 首頁的 **** [取得數據 **] 選單中，** 選取 **[新增數據管線]，然後建立名為 **[內嵌數據**] 的新數據管線**。
1. 在 [複製數據精**靈] 的 [** 選擇數據源 **] 頁面上，選取 **[取樣數據**]，然後選取**NYC計程車 - 綠色**範例**數據集。

    ![螢幕擷取畫面：[選取資料來源] 頁面。](./images/choose-data-source.png)

1. 在 [ **連接到數據源]** 頁面上，檢視數據源中的數據表。 應該有一個數據表，其中包含紐約市計程車車程的詳細數據。 然後選取 [下一步]****，繼續進行 [選擇資料目的地]**** 頁面。
1. 在 [選擇資料目的地]**** 頁面，選取現有 Lakehouse。 然後選取**下一步**。
1. 設定下列資料目的地選項，然後選取 [下一步]****：
    - **根資料夾**：資料表
    - **載入設定**：載入至新資料表
    - **目的地資料表名稱**：taxi_rides *（您可能需要等待顯示資料行對應預覽，才能變更此專案）*
    - **資料行對應**：*保留預設對應不變*
    - **啟用資料分割**：*未選取*
1. 在 [檢閱 + 儲存]**** 頁面，確定已選取 [立即啟動資料傳輸]**** 選項，然後選取 [儲存 + 執行]****。

    系統會建立包含**複製資料**活動的新管線，如下所示：

    ![螢幕擷取畫面：具有複製資料活動的管線。](./images/copy-data-pipeline.png)

    當管線開始執行時，您可透過管線設計工具的 [輸出]**** 窗格監視其狀態。 **使用 &#8635;** （*重新*整理） 圖示來重新整理狀態，並等到它被起訴（可能需要 10 分鐘以上）。

1. 在左側中樞功能表列，選取您的 Lakehouse。
1. 在 [首頁 **] 頁面的 ****[Lakehouse 總**管] 窗格中，選取** **[數據表 **] 節點的 **[...] 功能表中，選取 **[重新**整理]，然後展開 **[數據表**] 以確認**已建立taxi_rides**數據表。

    > **注意**：如果新數據表列為 *不明*數據表，請使用其 **[重新** 整理] 功能表選項來重新整理檢視。

1. **選取taxi_rides**數據表以檢視其內容。

    ![taxi_rides數據表的螢幕快照。](./images/dimProduct.png)

## 查詢 Lakehouse 的資料

現在您已擷取資料至 Lakehouse 的資料表，您可利用 SQL 來查詢。

1. 在 Lakehouse 頁面的右上方，從 **Lakehouse 檢視切換至 **Lakehouse** 的 SQL 分析端點**。

1. 在工具列，選取 [新增 SQL 查詢]****。 然後，輸入以下 SQL 程式碼至查詢編輯器。

    ```sql
    SELECT  DATENAME(dw,lpepPickupDatetime) AS Day,
            AVG(tripDistance) As AvgDistance
    FROM taxi_rides
    GROUP BY DATENAME(dw,lpepPickupDatetime)
    ```

1. **選取 &#9655;[執行**] 按鈕以執行查詢並檢閱結果，其中應該包含一周中每一天的平均車程距離。

    ![螢幕擷取畫面：SQL 查詢。](./images/sql-query.png)

## 視覺化 Lakehouse 的資料

Microsoft Fabric Lakehouse 會以語意資料模型組織所有資料表，您可以將其用來建立視覺效果和報表。

1. 在頁面左下方的 [總**管] 窗格底下**，選取 **[模型**] 索引標籤以查看 Lakehouse 中數據表的數據模型（這包括系統數據表，以及**taxi_rides**數據表）。
1. 在工具列中，選取 **[新增報表** ] 以根據 **taxi_rides**建立新的報表。
1. 在報表設計工具中：
    1. 在 [ **數據** ] 窗格中，展開 **[taxi_rides** ] 數據表，然後選取 **[lpepPickupDatetime** ] 和 **[passengerCount]** 字段。
    1. 在 [ **視覺效果]** 窗格中，選取 **折線圖** 視覺效果。 然後確定 **X 軸** 包含 **lpepPickupDatetime** 欄位，而 **Y** 軸包含 **passengerCount** 的總和。

        ![螢幕擷取畫面：Power BI 報表。](./images/fabric-report.png)

    > **提示**：您可利用 **>>** 圖示來隱藏報表設計工具窗格，以便更清楚看見報表。

1. 在 [ **檔案]** 功能表上，選取 [ **儲存** ] 以將報表儲存為 **[網狀架構] 工作區中的 [計程車車程報表** ]。

    您現可關閉包含報表的瀏覽器索引標籤，並返回 Lakehouse。 您可在 Microsoft Fabric 入口網站的工作區頁面找到報表。

## 清除資源

如您已完成探索 Microsoft Fabric，您可刪除您為此練習建立的工作區。

1. 在左側列，選取工作區圖示即可檢視其所包含的所有項目。
2. 在工具列的 [...]**** 功能表，選取 [工作區設定]****。
3. 在 [其他]**** 區段，選取 [移除此工作區]****。
