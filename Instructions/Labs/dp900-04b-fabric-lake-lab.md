---
lab:
  title: 探索 Microsoft Fabric 中的資料分析
  module: Explore fundamentals of large-scale data analytics
---

# 探索 Microsoft Fabric 中的資料分析

在此練習中，您將探索 Microsoft Fabric Lakehouse 中的資料擷取和分析。

此實驗室需要大約 **25** 分鐘才能完成。

> **注意**：您需要 Microsoft Fabric 授權才能完成此練習。 如需如何啟用免費 Fabric 試用版授權的詳細資訊，請參閱 [開始使用 Fabric](https://learn.microsoft.com/fabric/get-started/fabric-trial) 。 您需要 Microsoft *學校* 或 *公司* 帳戶才能執行此動作。 如果您沒有帳戶，您可以[註冊 Microsoft Office 365 E3 或更新版本的試用版](https://www.microsoft.com/microsoft-365/business/compare-more-office-365-for-business-plans)。

## 建立工作區

在 Fabric 中使用資料之前，請先建立已啟用 Fabric 試用版的工作區。

1. 在 登入 [Microsoft Fabric](https://app.fabric.microsoft.com) `https://app.fabric.microsoft.com` 。
2. 在左側功能表列中，選取 [ **工作區** ] (圖示看起來類似 &#128455;) 。
3. 使用您選擇的名稱建立新的工作區，並在 [ **進階** ] 區段中選取授權模式，其中包含 Fabric 容量 (*試用版*、 *進階*或 *網* 狀架構) 。
4. 當您的新工作區開啟時，它應該是空的。

    ![Power BI 中空白工作區的螢幕擷取畫面。](./images/new-workspace.png)

## 建立 Lakehouse

現在您已擁有工作區，現在可以切換至入口網站中的資料 *工程* 體驗，並為您的資料檔案建立 Data Lakehouse。

1. 在入口網站的左下角，切換至**資料工程**體驗。

    ![體驗切換器功能表的螢幕擷取畫面。](./images/fabric-switcher.png)

    資料工程首頁包含用來建立常用資料工程資產的磚。

2. 在 **[資料工程** ] 首頁中，使用您選擇的名稱建立新的 **Lakehouse** 。

    一分鐘之後，將會建立新的 Lakehouse：

    ![新 Lakehouse 的螢幕擷取畫面。](./images/new-lakehouse.png)

3. 檢視新的 Lakehouse，並注意左側的 **Lakehouse** 總管窗格可讓您流覽 Lakehouse 中的資料表和檔案：
    - **Tables**資料夾包含您可以使用 SQL 查詢的資料表。 Microsoft Fabric Lakehouse 中的資料表是以開放原始碼*Delta Lake*檔案格式為基礎，通常用於 Apache Spark。
    - [ **檔案]** 資料夾包含與受控差異資料表無關之 Lakehouse OneLake 儲存體中的資料檔。 您也可以在此資料夾中建立 *快捷方式* ，以參考外部儲存的資料。

    目前，Lakehouse 中沒有資料表或檔案。

## 擷取資料

擷取資料的簡單方法是使用管線中的 **複製資料** 活動，從來源擷取資料，並將它複製到 Lakehouse 中的檔案。

1. 在 Lakehouse 的 [ **首頁** ] 頁面上，選取 [ **取得資料** ] 功能表中的 [ **新增資料管線**]，然後建立名為 **[擷取銷售資料**] 的新資料管線。
1. 在 [ **複製資料** 精靈] 的 [ **選擇資料來源** ] 頁面上， **從 Wide World Importers 範例資料集選取 [零售資料模型** ]。

    ![[選擇資料來源] 頁面的螢幕擷取畫面。](./images/choose-data-source.png)

1. 選取 **[下一步** ]，然後檢視 [ **連接到資料來源** ] 頁面上資料來源中的資料表。
1. 選取包含產品記錄 **的dimension_stock_item** 資料表。 然後選取 **[下一步** ] 以進度移至 **[選擇資料目的地]** 頁面。
1. 在 [ **選擇資料目的地** ] 頁面上，選取現有的 Lakehouse。 然後，選取 [下一步]。
1. 設定下列資料目的地選項，然後選取 [ **下一步**]：
    - **根資料夾**：資料表
    - **載入設定**：載入至新資料表
    - **目的地資料表名稱**：dimension_stock_item
    - **資料行對應**： *保留預設對應原狀*
    - **啟用分割**區： *未選取*
1. 在 [ **檢閱 + 儲存** ] 頁面上，確定已選取 [ **立即啟動資料傳輸** ] 選項，然後選取 [ **儲存 + 執行**]。

    系統會建立包含 **複製資料** 活動的新管線，如下所示：

    ![具有複製資料活動的管線螢幕擷取畫面。](./images/copy-data-pipeline.png)

    當管線開始執行時，您可以在管線設計工具下的 [ **輸出** ] 窗格中監視其狀態。 使用 **&#8635;** (重新 *整理) 圖示* 來重新整理狀態，並等到它已停止為止。

1. 在左側的中樞功能表列中，選取您的 Lakehouse。
1. 在 [ **首頁** ] 的 [ **Lakehouse** 總管] 窗格中，展開 [ **資料表** ]，並確認已建立 **dimension_stock_item** 資料表。

    > **注意**：如果新資料表列為 *未識別*，請使用 Lakehouse 工具列中的 [ **重新** 整理] 按鈕來重新整理檢視。

1. 選取 **dimension_stock_item** 資料表以檢視其內容。

    ![dimension_stock_item資料表的螢幕擷取畫面。](./images/dimProduct.png)

## 查詢 Lakehouse 中的資料

既然您已將資料內嵌到 Lakehouse 中的資料表，您可以使用 SQL 來查詢它。

1. 在 Lakehouse 頁面右上方，切換至 Lakehouse 的 **SQL 端點** 。

    ![SQL 端點功能表的螢幕擷取畫面。](./images/endpoint-switcher.png)

1. 在工具列中，選取 **[新增 SQL 查詢**]。 然後在查詢編輯器中輸入下列 SQL 程式碼：

    ```sql
    SELECT Brand, COUNT(StockItemKey) AS Products
    FROM dimension_stock_item
    GROUP BY Brand
    ```

1. 選取 ** [&#9655; 執行** ] 按鈕以執行查詢並檢閱結果，其中應該會顯示兩個品牌值 (*N/A* 和 *Northwind*) ，並顯示每個產品的數目。

    ![SQL 查詢的螢幕擷取畫面。](./images/sql-query.png)

## 將 Lakehouse 中的資料視覺化

Microsoft Fabric Lakehouse 會組織資料模型中的所有資料表，您可以使用這些資料模型來建立視覺效果和報表。

1. 在頁面左下方的 [ **總** 管] 窗格底下，選取 [ **模型** ] 索引標籤，以查看 Lakehouse 中資料表的資料模型 (在此情況下，只有一個資料表) 。

    ![網狀架構 Lakehouse 中模型頁面的螢幕擷取畫面。](./images/fabric-model.png)

1. 在工具列中，選取 [ **新增報表** ] 以開啟包含 Power BI 報表設計師的新瀏覽器索引標籤。
1. 在報表設計師中：
    1. 在 [ **資料** ] 窗格中，展開 **[dimension_stock_item** ] 資料表，然後選取 [ **Brand** ] 和 [ **StockItemKey** ] 欄位。
    1. 在 [ **視覺效果]** 窗格中，選取堆疊 **橫條圖視覺效果** ， (它是第一個列出的) 。 然後，確定 **Y 軸** 包含 [ **品牌** ] 欄位，並將 **X 軸** 中的匯總變更為 **Count** ，使其包含 **StockItemKey 欄位的 Count** 。 最後，調整報表畫布中的視覺效果大小以填滿可用空間。

        ![Power BI 報表的螢幕擷取畫面。](./images/fabric-report.png)

    > **提示**：您可以使用 **>>** 圖示來隱藏報表設計師窗格，以便更清楚地查看報表。

1. 在 [ **檔案]** 功能表上，選取 [ **儲存** ] 以將報表儲存為 [網狀架構] 工作區中的 [ **品牌數量報表** ]。

    您現在可以關閉報表的瀏覽器索引標籤，以返回您的 Lakehouse。 您可以在 Microsoft Fabric 入口網站的工作區頁面中找到報表。

## 清除資源

如果您已完成探索 Microsoft Fabric，可以刪除您為此練習建立的工作區。

1. 在左側的列中，選取工作區的圖示，以檢視它包含的所有專案。
2. 在工具列上的 **[...]** 功能表中，選取 **[工作區設定**]。
3. 在 **[其他]** 區段中，選取 [ **移除此工作區**]。
