---
lab:
  title: 探索Azure 儲存體
  module: Explore Azure Storage for non-relational data
---

# <a name="explore-azure-storage"></a>探索Azure 儲存體

在此練習中，您必須在自己的 Azure 訂閱中佈建 Azure 儲存體帳戶，並探索使用該帳戶儲存資料的各種方法。

此實驗室需要大約 **15** 分鐘才能完成。

## <a name="before-you-start"></a>在您開始使用 Intune 之前

您將需要具有系統管理層級存取權的 [Azure 訂用帳戶](https://azure.microsoft.com/free)。

## <a name="provision-an-azure-storage-account"></a>佈建 Azure 儲存體帳戶

使用 Azure 儲存體的第一個步驟是在您的 Azure 訂用帳戶中佈建 Azure 儲存體帳戶。

1. 如果您尚未這麼做，請登入 [Azure 入口網站](https://portal.azure.com?azure-portal=true)。
1. On the Azure portal home page, select <bpt id="p1">**</bpt>&amp;#65291; Create a resource<ept id="p1">**</ept> from the upper left-hand corner and search for <bpt id="p2">*</bpt>Storage account<ept id="p2">*</ept>. Then in the resulting <bpt id="p1">**</bpt>Storage account<ept id="p1">**</ept> page, select <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.
1. 在 [建立儲存體帳戶] 頁面上，輸入下列值：
    - 訂用帳戶：選取 Azure 訂用帳戶。
    - **資源群組**：以您選擇的名稱建立新的資源群組。
    - **儲存體帳戶名稱**：使用小寫字母和數字輸入儲存體帳戶的唯一名稱。
    - **區域**：選取任何可用的位置。
    - **效能**：[標準]
    - **備援**：[本地備援儲存體 (LRS)]

1. Select <bpt id="p1">**</bpt>Next: Advanced &gt;<ept id="p1">**</ept> and view the advanced configuration options. In particular, note that this is where you can enable hierarchical namespace to support Azure Data Lake Storage Gen2. Leave this option <bpt id="p1">**</bpt><bpt id="p2">&lt;u&gt;</bpt>unselected<ept id="p2">&lt;/u&gt;</ept><ept id="p1">**</ept> (you'll enable it later), and then select <bpt id="p3">**</bpt>Next: Networking &gt;<ept id="p3">**</ept> to view the networking options for your storage account.
1. Select <bpt id="p1">**</bpt>Next: Data protection &gt;<ept id="p1">**</ept> and then in the <bpt id="p2">**</bpt>Recovery<ept id="p2">**</ept> section, <bpt id="p3">&lt;u&gt;</bpt>de<ept id="p3">&lt;/u&gt;</ept>select all of the <bpt id="p4">**</bpt>Enable soft delete...<ept id="p4">**</ept> options. These options retain deleted files for subsequent recovery, but can cause issues later when you enable hierarchical namespace.
1. 繼續檢視其餘的 [下一步 >] 頁面，而不變更任何預設設定，然後在 [檢閱 + 建立] 頁面上，等候您的選項經過驗證，即可選取 [建立] 以建立您的 Azure 儲存體帳戶。
1. Wait for deployment to complete. Then go to the resource that was deployed.

## <a name="explore-blob-storage"></a>探索 Blob 儲存體

擁有 Azure 儲存體帳戶後，現在您可以建立 Blob 資料的容器。

1. 從 `https://aka.ms/product1.json` 下載 [product1.json](https://aka.ms/product1.json?azure-portal=true) JSON 檔案，並儲存在您的電腦上 (可儲存在任何資料夾中 - 您稍後會將該檔案上傳至 Blob 儲存體)。

    *如果 JSON 檔案顯示在瀏覽器中，請將頁面儲存為 **product1.json**。*

1. 在儲存體容器的 Azure 入口網站頁面上，選取位於左側 [資料儲存體] 區段中的 [容器]。
1. 在 [容器] 頁面中，選取 [&#65291; 容器]，然後新增名為**資料**的新容器，將公用存取層級設為 [私人 (沒有匿名存取)]。
1. 建立 [資料] 容器後，確認 [容器] 頁面中列出了該容器。
1. In the pane on the left side, in the top section, select **Storage browser **. This page provides a browser-based interface that you can use to work with the data in your storage account.
1. 在儲存體瀏覽器頁面中，選取 [Blob 容器]，並確認您的 [資料] 容器已列出。
1. 選取 [資料] 容器，目前沒有任何內容。
1. 選取 [&#65291; 新增目錄] 並瀏覽資料夾的相關資訊，然後建立名為**產品**的新目錄。
1. 在儲存體瀏覽器中，確認目前的檢視顯示了剛建立的 [產品] 資料夾內容 - 觀察頁面頂端的「階層連結」是否反映出 **Blob 容器 > 資料 > 產品**的路徑。
1. 在階層連結中，選取 [資料] 以切換至 [資料] 容器，注意其中<u>沒有</u>名為 [產品] 的資料夾。

    Folders in blob storage are virtual, and only exist as part of the path of a blob. Since the <bpt id="p1">**</bpt>products<ept id="p1">**</ept> folder contained no blobs, it isn't really there!

1. 使用 [&#10514; 上傳] 按鈕開啟 [上傳 Blob] 面板。
1. In the <bpt id="p1">**</bpt>Upload blob<ept id="p1">**</ept> panel, select the <bpt id="p2">**</bpt>product1.json<ept id="p2">**</ept> file you saved on your local computer previously. Then in the <bpt id="p1">**</bpt>Advanced<ept id="p1">**</ept> section, in the <bpt id="p2">**</bpt>Upload to folder<ept id="p2">**</ept> box, enter <bpt id="p3">**</bpt>product_data<ept id="p3">**</ept> and select the <bpt id="p4">**</bpt>Upload<ept id="p4">**</ept> button.
1. 關閉 [上傳 Blob] 面板 (如果仍然開啟)，並確認已在 [資料] 容器中建立 [產品_資料] 虛擬資料夾。
1. 選取 [產品_資料] 資料夾，並確認其中含有您上傳的 **product1.json** Blob。
1. 在左側的 [資料儲存體] 區段中，選取 [容器]。
1. 開啟 [資料] 容器，並確認您建立的 [產品_資料] 資料夾已列出。
1. Select the <bpt id="p1">**</bpt>&amp;#x2027;&amp;#x2027;&amp;#x2027;<ept id="p1">**</ept> icon at the right-end of the folder, and note that it doesn't display any options. Folders in a flat namespace blob container are virtual, and can't be managed.
1. 使用 [資料] 頁面右上角的 **X** 圖示關閉頁面，並返回 [容器] 頁面。

## <a name="explore-azure-data-lake-storage-gen2"></a>探索 Azure Data Lake Storage Gen2

Azure Data Lake Store Gen2 support enables you to use hierarchical folders to organize and manage access to blobs. It also enables you to use Azure blob storage to host distributed file systems for common big data analytics platforms.

1. 從 `https://aka.ms/product2.json` 下載 [product2.json](https://aka.ms/product2.json?azure-portal=true) JSON 檔案，並儲存在先前下載 **product1.json** 的同一個資料夾中，您稍後會將該檔案上傳至 Blob 儲存體。
1. 在儲存體容器的 Azure 入口網站頁面左側，向下捲動至 [設定] 區段，然後選取 [Data Lake Gen2 升級]。
1. In the ****Data Lake Gen2 upgrade**** page, expand and complete each step to upgrade your storage account to enable hierarchical namespace and support Azure Data Lake Storage Gen 2. This may take some time.
1. 升級完成後，在左側窗格的頂端區段中，選取 [儲存體瀏覽器]，然後返回 [資料] Blob 容器的根目錄，其中仍包含 [產品_資料] 資料夾。
1. 選取 [產品_資料] 資料夾，並確認其中仍包含您先前上傳的 **product1.json** 檔案。
1. 使用 [&#10514; 上傳] 按鈕開啟 [上傳 Blob] 面板。
1. 在 Azure 入口網站首頁上，選取左上角的 [&#65291; 建立資源]，並搜尋*儲存體帳戶*。
1. 關閉 [上傳 Blob] 面板 (如果仍然開啟)，並確認 [產品_資料] 資料夾現已包含 **product2.json** 檔案。
1. 在左側的 [資料儲存體] 區段中，選取 [容器]。
1. 開啟 [資料] 容器，並確認您建立的 [產品_資料] 資料夾已列出。
1. 選取資料夾右端的 **&#x2027;&#x2027;&#x2027;** 圖示，請注意啟用階層命名空間後，您可以在資料夾層級執行設定工作，包括重新命名資料夾和設定權限。
1. 使用 [資料] 頁面右上角的 **X** 圖示關閉頁面，並返回 [容器] 頁面。

## <a name="explore-azure-files"></a>探索 Azure 檔案儲存體

Azure 檔案儲存體提供建立雲端式檔案共用的方法。

1. 在儲存體容器的 Azure 入口網站頁面上，選取位於左側 [資料儲存體] 區段中的 [檔案共用]。
1. 在 [檔案共用] 頁面中，選取 [&#65291 檔案共用]，然後使用 [交易最佳化] 層級新增名為**檔案**的新檔案共用。
1. 在 [檔案共用] 中，開啟新的 [檔案] 共用。
1. 然後在產生的 [儲存體帳戶] 頁面中，選取 [建立]。
1. 依序關閉 [連線] 窗格和 [檔案] 頁面，以返回 Azure 儲存體帳戶的 [檔案共用] 頁面。

## <a name="explore-azure-tables"></a>探索 Azure 資料表

Azure 資料表為需要儲存資料值，但不需要完整關聯式資料庫功能和結構的應用程式提供索引鍵/值存放區。

1. 在儲存體容器的 Azure 入口網站頁面上，選取位於左側 [資料儲存體] 區段中的 [資料表]。
1. 在 [資料表] 頁面上，選取 [&#65291; 資料表]，然後建立名為**產品**的新資料表。
1. 建立 [產品] 資料表後，在左側窗格的頂端區段中，選取 [儲存體瀏覽器]。
1. 在儲存體總管中，選取 [資料表]，並確認 [產品] 資料表已列出。
1. 選取 [產品] 資料表：
1. 在 [產品] 頁面中，選取 [&#65291; 新增實體]。
1. 在 [新增實體] 面板中，輸入下列索引鍵值：
    - **PartitionKey**：1
    - **RowKey**：1
1. 選取 [新增屬性]，然後建立具有下列值的新屬性：

    |屬性名稱 | 類型 | 值 |
    | ------------ | ---- | ----- |
    | 名稱 | String | 小工具 |

1. 新增具有下列值的第二個屬性：

    |屬性名稱 | 類型 | 值 |
    | ------------ | ---- | ----- |
    | 價格 | Double | 2.99 |

1. 選取 [插入]，將新實體的資料列插入資料表中。
1. 在儲存體瀏覽器中，確認資料列已新增至 [產品] 資料表，並已建立 [時間戳記] 資料行，以指出資料列上次修改的時間。
1. 將另一個具有下列屬性的實體新增至 [產品] 資料表：

    |屬性名稱 | 類型 | 值 |
    | ------------ | ---- | ----- |
    | PartitionKey | String | 1 |
    | RowKey | String | 2 |
    | Name | String | Kniknak |
    | 價格 | Double | 1.99 |
    | 已停用 | Boolean | true |

1. 插入新的實體之後，請確認資料表中顯示包含已中止產品的資料列。

    You have manually entered data into the table using the storage browser interface. In a real scenario, application developers can use the Azure Storage Table API to build applications that read and write values to tables, making it a cost effective and scalable solution for NoSQL storage.

> **提示**：如果您已完成探索 Azure 儲存體，則可刪除您在此練習中建立的資源群組。
