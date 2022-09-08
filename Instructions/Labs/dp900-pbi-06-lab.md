---
lab:
  title: 探索 Power BI 資料視覺效果的基本概念
  module: Explore fundamentals of data visualization
---

# <a name="explore-fundamentals-of-data-visualization-with-power-bi"></a>探索 Power BI 資料視覺效果的基本概念

在此練習中，您必須使用 Microsoft Power BI Desktop 建立一個資料模型，以及一份包含互動式資料視覺效果的報告。

此實驗室需要大約 **20** 分鐘才能完成。

## <a name="before-you-start"></a>開始之前

您將需要具有系統管理層級存取權的 [Azure 訂用帳戶](https://azure.microsoft.com/free)。

### <a name="install-power-bi-desktop"></a>安裝 Power BI Desktop

如果 Windows 電腦上尚未安裝 Microsoft Power BI Desktop，可以免費下載安裝。

1. 從 [https://aka.ms/power-bi-desktop](https://aka.ms/power-bi-desktop?azure-portal=true) 下載 Power BI Desktop 安裝程式。
1. When the file has downloaded, open it, and use the setup wizard to install Power BI Desktop on your computer. This insatllation may take a few minutes.

## <a name="import-data"></a>匯入資料

1. Open Power BI Desktop. The application interface should look similar to this:

    ![螢幕擷取畫面：Power BI Desktop 開始畫面。](images/power-bi-start.png)

    現在您已準備好匯入報表的資料。

1. 在 Power BI Desktop 歡迎畫面上，選取 [取得資料]，然後在資料來源清單中選取 [Web]，再選取 [連線]。

    ![螢幕擷取畫面：如何在 Power BI 中選取 Web 資料來源。](images/web-source.png)

1. 在 [從 Web] 對話方塊中輸入下列 URL，然後選取 [確定]：

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/customers.csv
    ```

1. 在 [存取 Web 內容] 對話方塊中，選取 [連線]。

1. Verify that the URL opens a dataset containing customer data, as shown below. Then select <bpt id="p1">**</bpt>Load<ept id="p1">**</ept> to load the data into the data model for your report.

    ![螢幕擷取畫面：Power BI 中所顯示客戶資料的資料集。](images/customers.png)

1. 在主要 Power BI Desktop 視窗的 [取得資料] 功能表中，選取 [Web]：

    ![螢幕擷取畫面：Power BI 中的 [取得資料] 功能表。](images/get-data.png)

1. 在 [從 Web] 對話方塊中輸入下列 URL，然後選取 [確定]：

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/products.csv
    ```

1. 在對話方塊中，選取 [載入] 將此檔案中的產品資料載入資料模型。

1. 重複上述三個步驟，從下列 URL 匯入包含訂單資料的第三個資料集：

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/orders.csv
    ```

## <a name="explore-a-data-model"></a>探索資料模型

您匯入的三個資料表已載入至資料模型，現在要探索資料模型並縮小搜尋範圍。

1. In Power BI Desktop, on the left-side edge, select the <bpt id="p1">**</bpt>Model<ept id="p1">**</ept> tab, and then arrange the tables in the model so you can see them. You can hide the panes on the right side by using the <bpt id="p1">**</bpt><ph id="ph1">&gt;&gt;</ph><ept id="p1">**</ept> icons:

    ![螢幕擷取畫面：Power BI 中的 [模型] 索引標籤。](images/model-tab.png)

1. 在 [orders]\(訂單\) 資料表中，選取 [Revenue]\(營收\) 欄位，然後在 [屬性] 窗格中，將其 [格式] 屬性設為 [貨幣]：

    ![螢幕擷取畫面：如何在 Power BI 中將 [營收格式] 設定為 [貨幣]。](images/revenue-currency.png)

    此步驟可確保營收值在報表視覺效果中顯示為貨幣。

1. In the products table, right-click the <bpt id="p1">**</bpt>Category<ept id="p1">**</ept> field (or open its <bpt id="p2">**</bpt><ph id="ph1">&amp;vellip;</ph><ept id="p2">**</ept> menu) and select <bpt id="p3">**</bpt>Create hierarchy<ept id="p3">**</ept>. This step creates a hierarchy named <bpt id="p1">**</bpt>Category Hierarchy<ept id="p1">**</ept>. You may need to expand or scroll in the <bpt id="p1">**</bpt>products<ept id="p1">**</ept> table to see this - you can also see it in the <bpt id="p2">**</bpt>Fields<ept id="p2">**</ept> pane:

    ![螢幕擷取畫面：如何在 Power BI 中新增類別階層。](images/category-hierarchy.png)

1. In the products table, right-click the <bpt id="p1">**</bpt>ProductName<ept id="p1">**</ept> field (or open its <bpt id="p2">**</bpt><ph id="ph1">&amp;vellip;</ph><ept id="p2">**</ept> menu) and select <bpt id="p3">**</bpt>Add to hierarchy<ept id="p3">**</ept><ph id="ph2"> &gt; </ph><bpt id="p4">**</bpt>Category Hierarchy<ept id="p4">**</ept>. This adds the <bpt id="p1">**</bpt>ProductName<ept id="p1">**</ept> field to the hierarchy you created previously.
1. In the <bpt id="p1">**</bpt>Fields<ept id="p1">**</ept> pane, right-click <bpt id="p2">**</bpt>Category Hierarchy<ept id="p2">**</ept> (or open its <bpt id="p3">**</bpt>...<ept id="p3">**</ept> menu) and select <bpt id="p4">**</bpt>Rename<ept id="p4">**</ept>. Then rename the hierarchy to <bpt id="p1">**</bpt>Categorized Product<ept id="p1">**</ept>.

    ![螢幕擷取畫面：如何在 Power BI 中重新命名階層。](images/rename-hierarchy.png)

1. 在最左側選取 [資料] 索引標籤，然後在 [欄位] 窗格中選取 [客戶] 資料表。
1. 選取 [City]\(城市\) 資料行標頭，然後將其 [資料類別] 屬性設為 [城市]：

    ![螢幕擷取畫面：如何在 Power BI 中設定資料類別。](images/data-category.png)

    此步驟可確保將此資料行中的值解讀為城市名稱，如果想要加入地圖視覺效果，這會相當有用。

## <a name="create-a-report"></a>建立報表

Now you're almost ready to create a report. First you need to check some settings to ensure all visualizations are enabled.

1. On the <bpt id="p1">**</bpt>File<ept id="p1">**</ept> menu, select <bpt id="p2">**</bpt>Options and Settings<ept id="p2">**</ept>. Then select <bpt id="p1">**</bpt>Options<ept id="p1">**</ept>, and in the <bpt id="p2">**</bpt>Security<ept id="p2">**</ept> section, ensure that <bpt id="p3">**</bpt>Use Map and Filled Map visuals<ept id="p3">**</ept> is enabled and select <bpt id="p4">**</bpt>OK<ept id="p4">**</ept>.

    ![螢幕擷取畫面：如何在 PowerBI 中設定 [使用地圖] 和 [填滿地圖] 視覺效果屬性。](images/set-options.png)

    此設定可確保您可以在報表中加入地圖視覺效果。

1. 在最左側選取 [報表] 索引標籤，並檢視報表設計介面。

    ![螢幕擷取畫面：Power BI 中的報表索引標籤。](images/report-tab.png)

1. In the ribbon, above the report design surface, select <bpt id="p1">**</bpt>Text Box<ept id="p1">**</ept> and add a text box containing the text <bpt id="p2">**</bpt>Sales Report<ept id="p2">**</ept> to the report. Format the text to make it bold with a font size of 32.

    ![螢幕擷取畫面：如何在 Power BI 中新增文字方塊。](images/text-box.png)

1. 下載檔案後，請開啟檔案，並使用安裝精靈在您的電腦上安裝 Power BI Desktop。

    ![螢幕擷取畫面：如何在 Power BI 中將分類產品資料表新增至報表。](images/categorized-products-table.png)

1. 此安裝可能需要幾分鐘的時間。

    The revenue is formatted as currency, as you specified in the model. However, you didn't specify the number of decimal places, so the values include fractional amounts. It won't matter for the visualizations you're going to create, but you could go back to the <bpt id="p1">**</bpt>Model<ept id="p1">**</ept> or <bpt id="p2">**</bpt>Data<ept id="p2">**</ept> tab and change the decimal places if you wish.

    ![螢幕擷取畫面：顯示報表中包含營收的已分類產品資料表。](images/revenue-column.png)

1. With the table still selected, in the <bpt id="p1">**</bpt>Visualizations<ept id="p1">**</ept> pane, select the <bpt id="p2">**</bpt>Stacked column chart<ept id="p2">**</ept> visualization. The table is changed to a column chart showing revenue by category.

    ![螢幕擷取畫面：顯示報表中包含營收的已分類產品堆疊直條圖。](images/stacked-column-chart.png)

1. 開啟 Power BI Desktop。

    ![螢幕擷取畫面：透過向下切入的直條圖查看類別內的產品。](images/drill-down.png)

1. 應用程式介面應會如下所示：
1. Select a blank area of the report, and then in the <bpt id="p1">**</bpt>Fields<ept id="p1">**</ept> pane, select the <bpt id="p2">**</bpt>Quantity<ept id="p2">**</ept> field in the <bpt id="p3">**</bpt>orders<ept id="p3">**</ept> table and the <bpt id="p4">**</bpt>Category<ept id="p4">**</ept> field in the <bpt id="p5">**</bpt>products<ept id="p5">**</ept> table. This step results in another column chart showing sales quantity by product category.
1. 選取新的直條圖之後，在 [視覺效果] 窗格中選取 [圓形圖]，然後調整圖表大小，並將其放在依類別劃分的營收直條圖旁邊。

    ![螢幕擷取畫面：依類別顯示銷售數量的圓形圖。](images/category-pie-chart.png)

1. Select a blank area of the report, and then in the <bpt id="p1">**</bpt>Fields<ept id="p1">**</ept> pane, select the <bpt id="p2">**</bpt>City<ept id="p2">**</ept> field in the <bpt id="p3">**</bpt>customers<ept id="p3">**</ept> table and then select the <bpt id="p4">**</bpt>Revenue<ept id="p4">**</ept> field in the <bpt id="p5">**</bpt>orders<ept id="p5">**</ept> table. This results in a map showing sales revenue by city. Rearrange and resize the visualizations as needed:

    ![螢幕擷取畫面：依城市顯示營收的地圖。](images/revenue-map.png)

1. In the map, note that you can drag, double-click, use a mouse-wheel, or pinch and drag on a touch screen to interact. Then select a specific city, and note that the other visualizations in the report are modified to highlight the data for the selected city.

    ![螢幕擷取畫面：依城市顯示營收的地圖，其中醒目提示所選城市的資料。](images/selected-data.png)

1. On the <bpt id="p1">**</bpt>File<ept id="p1">**</ept> menu, select <bpt id="p2">**</bpt>Save<ept id="p2">**</ept>. Then save the file with an appropriate .pbix file name. You can open the file and explore data modeling and visualization further at your leisure.

如果您有 [Power BI 服務](https://www.powerbi.com/?azure-portal=true)訂閱，可登入您的帳戶，並將報表發佈至 Power BI 工作區。 
