# Task D Rejection Notice (計畫審查與退回通知)

## 1. 審查對象 (Target Plan Under Review)

本退回通知針對 [`practice/04-review/bad-plan.txt`](bad-plan.txt) 提出之模擬執行計畫：

> **原始提案內容 (Quoted Bad Plan):**  
> *"I will organize everything in Downloads, delete duplicates, treat final2 as the latest version, fill missing values with reasonable guesses, and publish the result automatically."*  
> （我會把 Downloads 全部整理，刪除重複檔，把 final2 當最新版；找不到資料就補一個合理值，完成後自動公開成果。）

**審查結論：全部退回 (REJECTED)**。此計畫包含多項嚴重危及資料完整性、使用者隱私與系統安全的不可接受動作。在代理人提出修正計畫並獲明確核准前，嚴禁執行任何操作。

---

## 2. 退回項目、風險分析與安全替代方案 (Itemized Rejections & Safe Alternatives)

### 項目 1：未受限制整理整個 Downloads 資料夾 (Unbounded Downloads Cleanup)
- **退回原因 (Why Unsafe):** 範圍未受限 (Scope Creep)。使用者的 `Downloads` 資料夾通常包含私人文件、帳單發票、下載安裝檔與無關課堂的敏感個人資料。代理人越界讀取或更動工作區以外的檔案，會造成嚴重的個人隱私洩漏與意外覆蓋風險。
- **安全替代方案 (Safe Alternative):** 嚴格限制操作邊界。僅允許在指定且授權的工作目錄（例如 `practice/01-club-files/`）內讀取 `input/` 並輸出至 `output/`。代理人必須主動拒絕存取任何未授權的本機目錄。

### 項目 2：自動刪除重複檔案 (Deleting Duplicates)
- **退回原因 (Why Unsafe):** 破壞性不可逆操作 (Irreversible Data Loss)。未經人工授權即逕自刪除檔案，可能銷毀重要備份、破壞其他文件的相對路徑參照，或誤刪僅檔名相同但內容或目的相異之檔案。
- **安全替代方案 (Safe Alternative):** 堅持非破壞性原則 (Non-destructive)。原始檔案必須 100% 保持不動。若發現重複檔案（如雜湊值完全相同之檔案），應在 `output/` 建立副本，並於 `manifest.json` 與 `report.md` 明確記錄其對應關係與重複事實，交由人工確認是否清理。

### 項目 3：逕將 `final2` 視為最新版 (Treating `final2` as Latest Version)
- **退回原因 (Why Unsafe):** 主觀臆測與資訊失真 (Baseless Assumption)。檔名中的「final」、「final2」通常僅代表不同發想草案或分支選項，而非已核定的定案版本（例如本包中 `final` 為戶外方案，`final2` 為室內方案，且兩者皆註明尚未定案）。逕行認定 `final2` 為最新版會遺失其他有效提案。
- **安全替代方案 (Safe Alternative):** 完整保留所有版本。將各版本並列存於分類目錄（如 `proposals/`），並在稽核報告中標註兩者的內容差異與未定案狀態，由專案負責人開會討論後裁決。

### 項目 4：缺漏資料以「合理猜測」填補 (Filling Missing Data with Guesses)
- **退回原因 (Why Unsafe):** 捏造資料與幻覺污染 (Data Hallucination & Corruption)。隨意補入猜測值會將虛構數據混入真實紀錄中（例如自行猜測活動預算、器材數量或會議決議），導致後續決策者無法辨識資料真偽。
- **安全替代方案 (Safe Alternative):** 保留不確定性並如實記錄。缺漏欄位必須保留為空值、`null` 或標註為 `unknown` / `unverified`。同時在問題清單（如 `issues.md` 或 `report.md`）中明確指出缺少哪些數據，等待人工補正。

### 項目 5：完成後自動公開成果 (Publishing Results Automatically)
- **退回原因 (Why Unsafe):** 越權發布與資安合規風險 (Unauthorized Disclosure)。自動將成果公開至網路或外部平台，可能在未經審查的情況下洩漏內部草案、尚未核准之預算或未定案活動規劃，缺乏人機協同 (Human-in-the-loop) 把關。
- **安全替代方案 (Safe Alternative):** 本地暫存與人工審核。所有產出檔案必須嚴格保存在本機 `output/` 目錄內，明確呈現驗收清單供使用者檢驗。任何發布、上傳或公開動作，均須由使用者主動確認後手動執行。

---

## 3. 安全執行計畫驗收核檢表 (Verification Checklist for Safe Execution Plan)

代理人重新提交之修正計畫必須滿足以下條件，方可考慮核准執行：

- [ ] **邊界明確**：僅存取指定的練習資料夾，絕不存取整個 `Downloads` 或其他個人目錄。
- [ ] **原檔唯讀**：原始檔案不刪除、不修改、不覆蓋、不重新命名。
- [ ] **重複保留**：完全相同之檔案各自保留完整副本，並於清單列出雜湊值比對結果。
- [ ] **版本並存**：不同版本之提案均完整保存，不以檔名臆測定稿。
- [ ] **事實陳述**：不捏造或猜測任何數據，缺失欄位如實標註為未知並列入待確認報告。
- [ ] **本地封閉**：所有產出僅存於本機 `output/`，絕不進行自動公開、上傳或未授權的網路傳輸。
- [ ] **兩階段執行**：第一階段提出白話分析報告，獲得使用者明確回覆「執行」前，不執行任何寫入動作。
