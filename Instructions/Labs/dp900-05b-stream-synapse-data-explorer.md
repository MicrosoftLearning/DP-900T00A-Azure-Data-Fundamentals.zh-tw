---
lab:
  title: 探索 Azure Synapse 資料總管
  module: Explore fundamentals of real-time analytics
---

# <a name="explore-azure-synapse-data-explorer"></a>探索 Azure Synapse 資料總管

在本練習中，您將使用 Azure Synapse Data Explorer 分析時間序列資料。

此實驗室需要大約 **25** 分鐘才能完成。

## <a name="before-you-start"></a>在您開始使用 Intune 之前

您將需要具有系統管理層級存取權的 [Azure 訂用帳戶](https://azure.microsoft.com/free)。

## <a name="provision-a-synapse-analytics-workspace"></a>佈建 Synapse Analytics 工作區

> **提示**：若您已具有來自上個練習的 Azure Synapse 工作區，請跳過本節並直接移至 **[建立資料總管集區](#create-a-data-explorer-pool)** 。

1. 在 [https://portal.azure/com](https://portal.azure.com?azure-portal=true) 開啟 Azure 入口網站，使用與 Azure 訂用帳戶相關聯的認證登入。

    > <bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: Ensure you are working in the directory containing your subscription - indicated at the top right under your user ID. If not, select the user icon and switch directory.

1. 在 Azure 入口網站的 [首頁] 頁面上，使用 [&#65291; 建立資源] 圖示來建立新的資源。
1. 搜尋 *Azure Synapse Analytics*，並使用下列設定建立新的 **Azure Synapse Analytics** 資源：
    - **訂用帳戶**：您的 Azure 訂用帳戶
        - **資源群組**：建立具有適當名稱的新資源群組，例如 "synapse-rg"
        - **受控資源群組**：輸入適當的名稱，例如 "synapse-managed-rg"。
    - **工作區名稱**：*輸入唯一的工作區名稱，例如「synapse-ws-<your_name>」* 。
    - **區域**：選取任何可用區域。
    - **選取 Data Lake Storage Gen 2**：從訂閱
        - **帳戶名稱**：*建立具有唯一名稱的新帳戶，例如「datalake<your_name>」* 。
        - **檔案系統名稱**：*建立具有唯一名稱的新檔案系統，例如「fs<your_name>」* 。

    > <bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: A Synapse Analytics workspace requires two resource groups in your Azure subscription; one for resources you explicitly create, and another for managed resources used by the service. It also requires a Data Lake storage account in which to store data, scripts, and other artifacts.

1. 輸入這些詳細資料後，請選取 [檢閱 + 建立]，然後選取 [建立] 以建立工作區。
1. 等候建立工作區 - 這可能需要五分鐘的時間。
1. 部署完成後，請移至已建立的資源群組，並注意到其包含您的 Synapse Analytics 工作區和 Data Lake Storage 帳戶。
1. 選取 Synapse 工作區，然後在其 [概觀] 頁面的 [開啟 Synapse Studio] 卡片中，選取 [開啟] 以在新瀏覽器索引標籤中開啟 Synapse Studio。Synapse Studio 是一種 Web 介面，可讓您用來處理 Synapse Analytics 工作區。
1. 在 Synapse Studio 左側，使用 **&rsaquo;&rsaquo;** 圖示展開功能表，這會顯示 Synapse Studio 中的不同頁面，您將使用這些頁面來管理資源和執行資料分析工作

## <a name="create-a-data-explorer-pool"></a>建立資料總管集區

1. 在 Synapse Studio 中，選取 [管理] 頁面。
1. 選取 [資料總管集區] 索引標籤，然後使用 **&#65291; 新增**圖示建立具有下列設定的新集區：
    - **資料總管集區名稱**：dxpool
    - **工作負載**：最佳化計算
    - **大小**：超小型 (2 核心)
1. 選取 [下一步：其他設定 >]，並啟用 [串流擷取] 設定 - 這可讓資料總管從串流來源擷取新的資料，例如 Azure 事件中樞。
1. 選取 [檢閱並建立] 以建立資料總管集區，然後等候部署該集區 (可能需要 15 分鐘或更長的時間 -狀態會從 [建立] 變更為 [線上])。

## <a name="create-a-database-and-ingest-data"></a>建立資料庫並擷取資料

1. 在 Synapse Studio 中，選取 [資料] 頁面。
1. 確認選取 [工作區] 索引標籤，並視需要選取頁面左上方的 **&#8635;** 圖示重新整理檢視，以列出**資料總管資料庫**。
1. 展開 [資料總管資料庫]，並確認已列出 **dxpool**。
1. 在 [資料] 窗格中，使用 **&#65291;** 圖示，在名稱為 **iot-data** 的 **dxpool** 集區中，建立新的**資料總管資料庫**。
1. 等候建立資料庫時，請從 [https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/data/devices.csv](https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/data/devices.csv?azure-portal=true) 下載 **devices.csv**，並將其儲存在本機電腦上的任何資料夾中。
1. 在 Synapse Studio 中，視需要等候建立資料庫，然後在 [...] 功能表中選取新的 **iot-data** 資料庫，選取 [在 Azure Data Explorer 中開啟]。
1. 在包含 Azure Data Explorer 的新瀏覽器索引標籤中，選取 [資料] 索引標籤上的 [內嵌新資料]。
1. 在 [目的地] 頁面中，選取下列設定：
    - **叢集**：*Azure Synapse 工作區中的 **dxpool** 資料總管集區*
    - **資料庫**：iot-data
    - **資料表**：建立名為 **devices** 的新資料表
1. 選取 [下一步：來源]，然後在 [來源] 頁面上，選取下列選項：
    - **來源類型**：檔案
    - **檔案**：從本機電腦上傳 **devices.csv** 檔案。
1. 選取 [下一步：結構描述]，然後在 [結構描述] 頁面上，確認下列設定正確：
    - **壓縮類型**：未壓縮
    - **資料格式**：CSV
    - **忽略第一筆記錄**：已選取
    - **對應**：devices_mapping
1. Ensure the column data types have been correctly identified as <bpt id="p1">*</bpt>Time (datetime)<ept id="p1">*</ept>, <bpt id="p2">*</bpt>Device (string)<ept id="p2">*</ept>, and <bpt id="p3">*</bpt>Value (long)<ept id="p3">*</ept>). Then select <bpt id="p1">**</bpt>Next: Start Ingestion<ept id="p1">**</ept>.
1. 擷取完成時，請選取 [關閉]。
1. 在 Azure Data Explorer 的 [查詢] 索引標籤上，確認已選取 **iot-data** 資料庫，然後在查詢窗格中輸入下列查詢。

    ```kusto
    devices
    ```

1. 在工具列上，選取 [&#9655; 執行] 按鈕來執行查詢和檢閱結果，其看起來應會類似如下：

    | 時間 | 裝置 | 值 |
    | --- | --- | --- |
    | 2022-01-01T00:00:00Z | Dev1 | 7 |
    | 2022-01-01T00:00:01Z | Dev2 | 4 |
    | ... | ... | ... |

    若您的結果符合此內容，表示您已順利從檔案中的資料建立**裝置**資料表。

    > <bpt id="p1">**</bpt>Tip<ept id="p1">**</ept>: In this example, you imported a very small amount of batch data from a file, which is fine for the purposes of this exercise. In reality, you can use Data Explorer to analyze much larger volumes of data; and since you enabled stream ingestion, you could also have configured Data Explorer to ingest data into the table from a streaming source such as Azure Event Hubs.

## <a name="use-kusto-query-language-to-query-the-table-in-synapse-studio"></a>使用 Kusto 查詢語言來查詢 Synapse Studio 中的資料表

1. 關閉 [Azure Data Explorer] 瀏覽器索引標籤，並回到包含 Synapse Studio 的索引標籤。
1. On the <bpt id="p1">**</bpt>Data<ept id="p1">**</ept> page, expand the <bpt id="p2">**</bpt>iot-data<ept id="p2">**</ept> database and its <bpt id="p3">**</bpt>Tables<ept id="p3">**</ept> folder. Then in the <bpt id="p1">**</bpt>...<ept id="p1">**</ept> menu for the <bpt id="p2">**</bpt>devices<ept id="p2">**</ept> table, select <bpt id="p3">**</bpt>New KQL Script<ept id="p3">**</ept><ph id="ph1"> &gt; </ph><bpt id="p4">**</bpt>Take 1000 rows<ept id="p4">**</ept>.
1. Review the generated query and its results. The query should contain the following code:

    ```kusto
    devices
    | take 1000
    ```

    查詢的結果包含前 1000 個資料列。

1. 修改查詢，如下所示：

    ```kusto
    devices
    | where Device == 'Dev1'
    ```

1. Select <bpt id="p1">**</bpt>&amp;#9655; Run<ept id="p1">**</ept> to run the query. Then review the results, which should contain only the rows for the <bpt id="p1">*</bpt>Dev1<ept id="p1">*</ept> device.

1. 修改查詢，如下所示：

    ```kusto
    devices
    | where Device == 'Dev1'
    | where Time > datetime(2022-01-07)
    ```

1. 執行查詢並檢閱結果，其應該只包含 2022 年 1 月 7 日以後的 *Dev1* 裝置。

1. 修改查詢，如下所示：

    ```kusto
    devices
    | where Time between (datetime(2022-01-01 00:00:00) .. datetime(2022-07-01 23:59:59))
    | summarize AvgVal = avg(Value) by Device
    | sort by Device asc
    ```

1. 執行查詢並檢閱結果，其應包含在 2022 年 1 月 1 日至 1 月 7 日之間記錄的平均裝置值 (依裝置名稱遞增排序)。

1. 關閉 [KQL查詢] 索引標籤，捨棄您的變更。

## <a name="delete-azure-resources"></a>刪除 Azure 資源

完成探索 Azure Synapse Analytics 後，您應刪除已建立的資源，以避免不必要的 Azure 成本。

1. 關閉 Synapse Studio 瀏覽器索引標籤而不儲存任何變更，並回到 Azure 入口網站。
1. 在 Azure 入口網站的 [首頁] 上，選取 [資源群組]。
1. 選取 Synapse Analytics 工作區的資源群組 (非受控資源群組)，並確認其包含 Synapse 工作區、儲存體帳戶，以及工作區的資料總管集區 (若您已完成上一個練習，其亦會包含 Spark 集區)。
1. 在資源群組的 [概觀] 頁面頂端，選取 [刪除資源群組]。
1. 輸入資源群組名稱以確認您想要將其刪除，然後選取 [刪除]。

    幾分鐘後，系統將會刪除您的 Azure Synapse 工作區和與其相關聯的受控工作區。
