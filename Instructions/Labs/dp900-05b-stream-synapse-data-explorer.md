---
lab:
  title: 探索 Azure Synapse 資料總管
  module: Explore fundamentals of real-time analytics
---

# 探索 Azure Synapse 資料總管

> **注意**：由於產品變更，此實驗室的 **建立資料庫和內嵌資料** 區段有一些已知問題。 我們正努力解決這些問題。

在本練習中，您將使用 Azure Synapse Data Explorer 分析時間序列資料。

此實驗室需要大約 **25** 分鐘才能完成。

## 在您開始使用 Intune 之前

您將需要具有系統管理層級存取權的 [Azure 訂用帳戶](https://azure.microsoft.com/free)。

## 佈建 Synapse Analytics 工作區

> **提示**：若您已具有來自上個練習的 Azure Synapse 工作區，請跳過本節並直接移至 **[建立資料總管集區](#create-a-data-explorer-pool)** 。

1. 在 [https://portal.azure/com](https://portal.azure.com?azure-portal=true) 開啟 Azure 入口網站，使用與 Azure 訂用帳戶相關聯的認證登入。

    >                 **注意**：請確定位於您訂用帳戶所在的目錄，如右上角的使用者識別碼下方所示。 否則，請選取使用者圖示並切換目錄。

1. 在 Azure 入口網站的 [首頁] 頁面上，使用 [&#65291; 建立資源] 圖示來建立新的資源。
1. 搜尋 *Azure Synapse Analytics*，並使用下列設定建立新的 **Azure Synapse Analytics** 資源：
    - **訂用帳戶**：Azure 訂閱
        - **資源群組**：建立具有適當名稱的新資源群組，例如 "synapse-rg"
        - **受控資源群組**：輸入適當的名稱，例如 "synapse-managed-rg"。
    - **工作區名稱**：*輸入唯一的工作區名稱，例如「synapse-ws-<your_name>」* 。
    - **區域**：選取任何可用區域。
    - **選取 Data Lake Storage Gen 2**：從訂閱
        - **帳戶名稱**：*建立具有唯一名稱的新帳戶，例如「datalake<your_name>」* 。
        - **檔案系統名稱**：*建立具有唯一名稱的新檔案系統，例如「fs<your_name>」* 。

    >                 **注意**：Synapse Analytics 工作區需要 Azure 訂用帳戶中的兩個資源群組：一個用於您明確建立的資源，另一個用於服務所使用的受控資源。 其還需要 Data Lake Storage 帳戶來儲存資料、指令碼和其他成品。

1. 輸入這些詳細資料後，請選取 [檢閱 + 建立]，然後選取 [建立] 以建立工作區。
1. 等候建立工作區 - 這可能需要五分鐘的時間。
1. 部署完成後，請移至已建立的資源群組，並注意到其包含您的 Synapse Analytics 工作區和 Data Lake Storage 帳戶。
1. 選取 Synapse 工作區，然後在其 [概觀] 頁面的 [開啟 Synapse Studio] 卡片中，選取 [開啟] 以在新瀏覽器索引標籤中開啟 Synapse Studio。Synapse Studio 是一種 Web 介面，可讓您用來處理 Synapse Analytics 工作區。
1. 在Synapse Studio左側，使用 **&rsaquo;&rsaquo;** 圖示展開功能表 - 這會顯示您將用來管理資源和執行資料分析工作之Synapse Studio內的不同頁面。

## 建立資料總管集區

1. 在 Synapse Studio 中，選取 [管理] 頁面。
1. 選取 [資料總管集區] 索引標籤，然後使用 **&#65291; 新增**圖示建立具有下列設定的新集區：
    - **資料總管集區名稱**：dxpool
    - **工作負載**：最佳化計算
    - **大小**：超小型 (2 核心)
1. 選取 [下一步：其他設定 >]，並啟用 [串流擷取] 設定 - 這可讓資料總管從串流來源擷取新的資料，例如 Azure 事件中樞。
1. 選取 [檢閱並建立] 以建立資料總管集區，然後等候部署該集區 (可能需要 15 分鐘或更長的時間 -狀態會從 [建立] 變更為 [線上])。

## 建立資料庫並擷取資料

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
1. 確認資料行資料類型已正確識別為 [時間 (日期時間)]、[裝置 (字串)] 和 [值 (長)]。 然後選取 [下一步：開始擷取]。
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

    >                 **提示**：在本範例中，您已從檔案匯入非常少量的批次資料，其非常適合本練習的用途。 實際上，您可使用資料總管來分析更大的資料量；由於您已啟用串流擷取，因此亦可設定資料總管，將資料從 Azure 事件中樞等串流來源內嵌至資料表。

## 使用 Kusto 查詢語言來查詢 Synapse Studio 中的資料表

1. 關閉 [Azure Data Explorer] 瀏覽器索引標籤，並回到包含 Synapse Studio 的索引標籤。
1. 在 [資料] 頁面上，展開 **iot-data** 資料庫及其**資料表**資料夾。 然後在**裝置**資料表的 [...] 功能表中，選取 [新增 KQL 指令碼]  >  [接受 1000 個資料列]。
1. 檢閱產生的查詢及其結果。 查詢應會包含下列程式碼：

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

1. 選取 [&#9655; 執行] 執行查詢。 然後檢閱結果，其應僅包含 *Dev1* 裝置的資料列。

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

## 刪除 Azure 資源

完成探索 Azure Synapse Analytics 後，您應刪除已建立的資源，以避免不必要的 Azure 成本。

1. 關閉 Synapse Studio 瀏覽器索引標籤而不儲存任何變更，並回到 Azure 入口網站。
1. 在 Azure 入口網站的 [首頁] 上，選取 [資源群組]。
1. 選取 Synapse Analytics 工作區的資源群組 (非受控資源群組)，並確認其包含 Synapse 工作區、儲存體帳戶，以及工作區的資料總管集區 (若您已完成上一個練習，其亦會包含 Spark 集區)。
1. 在資源群組的 [概觀] 頁面頂端，選取 [刪除資源群組]。
1. 輸入資源群組名稱以確認您想要將其刪除，然後選取 [刪除]。

    幾分鐘後，系統將會刪除您的 Azure Synapse 工作區和與其相關聯的受控工作區。
