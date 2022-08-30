---
lab:
  title: 探索 Azure 串流分析
  module: Explore data analytics in Azure
---

## <a name="explore-azure-stream-analytics"></a>探索 Azure 串流分析

在此練習中，您必須在自己的 Azure 訂閱中佈建 Azure 串流分析作業，用於處理即時資料流。

> <bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: The exercise is part of a module on Microsoft Learn, and includes an option to use a <bpt id="p2">*</bpt>sandbox<ept id="p2">*</ept> Azure subscription. However, if you are completing this exercise as part of an instructor-led class, you should use the Azure subscription provided as part of the class instead of the sandbox.

開始在 Microsoft Learn 上進行這項練習前，您必須先為 Azure 訂閱準備 Cloud Shell 環境。

1. 前往位於 `https://portal.azure.com` 的 [Azure 入口網站](https://portal.azure.com)，使用您的 Azure 訂閱登入資訊來登入帳戶。
2. Use the <bpt id="p1">**</bpt>[<ph id="ph1">\&gt;</ph>_]<ept id="p1">**</ept> button to the right of the search bar at the top of the page to create a new Cloud Shell in the Azure portal, selecting a <bpt id="p2">***</bpt>Bash<ept id="p2">***</ept> environment and creating storage if prompted. The cloud shell provides a command line interface in a pane at the bottom of the Azure portal, as shown here:

    ![顯示 Cloud Shell 窗格的 Azure 入口網站](./images/cloud-shell.png)

3. Note that you can resize the cloud shell by dragging the separator bar at the top of the pane, or by using the <bpt id="p1">**</bpt>&amp;#8212;<ept id="p1">**</ept>, <bpt id="p2">**</bpt>&amp;#9723;<ept id="p2">**</ept>, and <bpt id="p3">**</bpt>X<ept id="p3">**</ept> icons at the top right of the pane to minimize, maximize, and close the pane. For more information about using the Azure Cloud Shell, see the <bpt id="p1">[</bpt>Azure Cloud Shell documentation<ept id="p1">](https://docs.microsoft.com/azure/cloud-shell/overview)</ept>.

4. 現在您已準備妥當，可在 Microsoft Learn 中完成練習。請使用 Azure 入口網站中的 Cloud Shell，而非 Learn 模組中的 (空白) Cloud Shell (使用沙箱訂閱的自學型學員專用)。

    請使用下方連結在 Microsoft Learn 上開啟本練習。

    **[前往 Microsoft Learn](https://docs.microsoft.com/learn/modules/explore-fundamentals-stream-processing/5-exercise-stream-analytics#create-azure-resources)**

> **進一步學習**：如果您稍後有時間，可返回這個 Microsoft Learn 模組並嘗試完成其他練習，包含探索 Spark Streaming 與 Azure Synapse Analytics 資料總管。
