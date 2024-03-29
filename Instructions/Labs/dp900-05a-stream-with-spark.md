---
lab:
  title: 探索 Azure Synapse Analytics 中的 Spark 串流
  module: Explore fundamentals of real-time analytics
---

# 探索 Azure Synapse Analytics 中的 Spark 串流

在此練習中，您將使用 Azure Synapse Analytics 中的 *Spark 結構化串流*和*差異資料表*來處理串流資料。

此實驗室需要大約 **15** 分鐘才能完成。

## 在您開始使用 Intune 之前

您將需要具有系統管理層級存取權的 [Azure 訂用帳戶](https://azure.microsoft.com/free)。

## 佈建 Synapse Analytics 工作區

若要使用 Synapse Analytics，您必須在 Azure 訂用帳戶中佈建 Synapse Analytics 工作區資源。

1. 在 [[Azure 入口網站]](https://portal.azure.com?azure-portal=true) 開啟 Azure 入口網站，使用與 Azure 訂用帳戶相關聯的認證登入。

    > **注意**：請確定您是在包含專屬訂用帳戶的目錄中工作 - 請見畫面右上角，您的使用者識別碼下方。 否則，請選取使用者圖示並切換目錄。

2. 在 Azure 入口網站的 [首頁]**** 頁面上，使用 [&#65291; 建立資源]**** 圖示來建立新的資源。
3. 搜尋 Azure Synapse Analytics**，並使用下列設定建立新的 **Azure Synapse Analytics** 資源：
    - **訂用帳戶**：您的 Azure 訂用帳戶**
        - **資源群組**：建立具有適當名稱的新資源群組，例如 "synapse-rg"**
        - **受控資源群組**：輸入適當的名稱，例如 "synapse-managed-rg"**。
    - **工作區名稱**：*輸入唯一的工作區名稱，例如「synapse-ws-<your_name>」*。
    - **區域**：選取任何可用區域**。
    - **選取 Data Lake Storage Gen 2**：從訂用帳戶
        - **帳戶名稱**：*建立具有唯一名稱的新帳戶，例如「datalake<your_name>」*。
        - **檔案系統名稱**：*建立具有唯一名稱的新檔案系統，例如「fs<your_name>」*。

    > **注意**：Synapse Analytics 工作區需要 Azure 訂用帳戶中的兩個資源群組：一個用於您明確建立的資源，另一個用於服務所使用的受控資源。 還需要 Data Lake Storage 帳戶來儲存資料、指令碼和其他成品。

4. 輸入這些詳細資料後，請選取 [檢閱 + 建立]****，然後選取 [建立]**** 以建立工作區。
5. 等候工作區建立，可能需要大約五分鐘。
6. 部署完成後，請移至已建立的資源群組，並注意其包含 Synapse Analytics 工作區和 Data Lake Storage 帳戶。
7. 選取 Synapse 工作區，然後在 [概觀]**** 頁面的 [開啟 Synapse Studio]**** 卡片中，選取 [開啟]****，以在新瀏覽器索引標籤中開啟 Synapse Studio。Synapse Studio 是 Web 介面，可用來處理 Synapse Analytics 工作區。
8. 在 Synapse Studio 左側，使用 **&rsaquo;&rsaquo;** 圖示展開功能表，這會顯示 Synapse Studio 中的不同頁面，您將使用這些頁面來管理資源和執行資料分析工作，如下所示：

    ![Synapse Studio](images/synapse-studio.png)

## 建立 Spark 集區

若要使用 Spark 來處理串流資料，您必須將 Spark 集區新增至 Azure Synapse 工作區。

1. 在 Synapse Studio 中，選取 [管理]**** 頁面。
2. 選取 [Apache Spark 集區]**** 索引標籤，然後使用 [&#65291; 新增]**** 圖示，建立具有下列設定的新 Spark 集區：
    - **Apache Spark 集區名稱**：sparkpool
    - **節點大小系列**：記憶體最佳化
    - **節點大小**：小型 (4 個虛擬核心 / 32 GB)
    - **自動調整**：已啟用
    - **節點數目** 3----3
3. 檢閱並建立 Spark 集區，然後等候部署完成 (這可能需要幾分鐘)。

## 探索串流處理

若要使用 Spark 探索串流處理，您將使用包含 Python 程式碼和筆記的筆記本，協助您使用 Spark 結構化串流和差異資料表執行一些基本串流處理。

1. 將 [Structured Streaming and Delta Tables.ipynb](https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/Spark%20Structured%20Streaming%20and%20Delta%20Tables.ipynb) 筆記本下載至本地電腦 (如果筆記本是以瀏覽器中的文字檔開啟，請將其儲存到本地資料夾；請小心將其儲存為 **Structured Streaming and Delta Tables.ipynb**，而不是 .txt檔案)
2. 在 Synapse Studio 中，選取 [開發]**** 頁面。
3. 在 [&#65291;]**** 功能表上，選取 [&#8612; 匯入]****，然後選取本地電腦上的 **Structured Streaming and Delta Tables.ipynb** 檔案。
4. 依照筆記本中的指示將其附加至 Spark 集區，並執行其所包含的程式碼資料格，以探索使用 Spark 進行串流處理的各種方式。

## 刪除 Azure 資源

> **注意**：如果您想要完成使用 Azure Synapse Analytics 的其他練習，您可以略過本節。 否則，請遵循下列步驟來避免不必要的 Azure 成本。

1. 關閉 Synapse Studio 瀏覽器索引標籤而不儲存任何變更，並回到 Azure 入口網站。
1. 在 Azure 入口網站的 [首頁]****，選取 [資源群組]****。
1. 選取 Synapse Analytics 工作區的資源群組 (非受控資源群組)，並確認其包含 Synapse 工作區、儲存體帳戶，以及工作區的資料總管集區 (若您已完成上一個練習，其亦會包含 Spark 集區)。
1. 在資源群組的 [概觀]**** 頁面頂端，選取 [刪除資源群組]****。
1. 輸入資源群組名稱以確認要刪除，然後選取 [刪除]****。

    幾分鐘後，將會刪除您的 Azure Synapse Analytics 工作區及其相關聯的受控工作區。
