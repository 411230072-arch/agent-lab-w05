# Task A Organization Report (社團檔案整理報告)

## 1. 執行概述 (Overview)
- **輸入目錄 (Input Directory)**: `practice/01-club-files/input` (共 12 個檔案)
- **輸出目錄 (Output Directory)**: `practice/01-club-files/output` (共 12 個檔案副本 + manifest.json + report.md)
- **原始檔案狀態 (Integrity Check)**: 原始 12 個輸入檔案均完全未修改、未刪除、未覆蓋。所有檔案均完整保留副本。

---

## 2. 目錄分類說明 (Categorization)

檔案依據其內容與性質整理至 4 個子目錄：

1. **`announcements/` (公告宣傳與回饋)**
   - `announcement.txt`: 活動公告（提醒攜帶筆記本，時間地點待定）。
   - `announcement_copy.txt`: 活動公告副本（內容與 `announcement.txt` 完全一致，依安全規範完整保留）。
   - `poster_text.txt`: 活動文宣短語（「一起休息，畫張小卡」）。
   - `feedback_questions.txt`: 活動後問卷反饋題目（「任務清楚嗎？想改哪一點？」）。

2. **`meetings/` (會議記錄)**
   - `meeting_notes.txt`: 討論下次會議決定室內或室外方案之記錄。

3. **`proposals/` (企劃與應變方案)**
   - `proposal_final.txt`: 企畫第一版（戶外活動，30分鐘，內容明確註記「尚未定案」）。
   - `proposal_final2.txt`: 企畫第二版（室內活動，20分鐘，內容明確註記「仍待討論」）。
   - `next_steps.txt`: 後續行動指引（明確指示「比較兩個企畫，兩者都尚未定案」）。
   - `rain_plan.txt`: 雨天備案（「下雨時另議室內方案」）。

4. **`resources/` (物資與預算)**
   - `equipment_list.txt`: 器材清單（白板筆4支、紙2包）。
   - `equipment_backup.txt`: 器材清單備份（內容與 `equipment_list.txt` 完全一致，完整保留）。
   - `budget_draft.txt`: 紙張預算草案（模擬值100，明確註記「尚未核定」）。

---

## 3. 重複檔案與版本分析 (Duplicates & Versions)

### 3.1 內容完全一致之重複檔案 (Byte-for-byte Identical Files)
透過 SHA-256 雜湊值比對，發現以下 2 組完全相同的檔案：
1. `announcement.txt` 與 `announcement_copy.txt` (SHA-256: `c19164b1054ebf52ed33bc5321c887985ea043a0b07db1e99f866986d2ccd584`)
2. `equipment_list.txt` 與 `equipment_backup.txt` (SHA-256: `c21d53ba1f8d3ad06e1833539935120a5baca4d13b34a2aa98ce157ff4502fa3`)

**處理原則**: 依據安全規範與任務要求，**絕不擅自刪除**重複檔案，全部於 `output/` 建立對應副本並記錄於 `manifest.json`。

### 3.2 檔名相近但內容互異之版本 (Distinct Versions with Similar Names)
- `proposal_final.txt` vs `proposal_final2.txt`:
  - `proposal_final.txt`: 室外活動方案 (30分鐘)
  - `proposal_final2.txt`: 室內活動方案 (20分鐘)
  - 兩者 SHA-256 不同，為互斥之不同活動方案版本。
  - 兩份檔案內容均註記「尚未定案」與「仍待討論」，且 `next_steps.txt` 特別提醒不可假設任何一個已定案。
  - **處理原則**: 絕不依據檔名中的「final2」或修改時間擅自認定為最終版本，兩版本皆完整保存於 `proposals/`。

---

## 4. 待人工確認之事項 (Uncertainties Requiring Human Confirmation)
1. **活動方案決策**: 戶外版 (`proposal_final.txt`) 與室內版 (`proposal_final2.txt`) 尚未定案，須待後續會議討論決定。
2. **時間與地點**: 公告中載明「時間地點尚未決定」，後續發布前須確認確切人事實地物。
3. **預算審核**: 紙張預算 100 單位目前標記為「尚未核定」，不可直接視為正式支出。
4. **雨天方案觸發機制**: 雨天方案僅為備案方向，具體執行門檻與細節仍待會議定案。

---

## 5. 驗收與查核記錄 (Verification Checklist)
- [x] **輸入檔案未更動**: `input/` 內 12 個檔案完整保留，原始雜湊值無變動。
- [x] **輸出檔案齊全**: `output/` 內包含 12 個對應目標檔案，雜湊值與輸入檔 100% 吻合。
- [x] **清單完整性**: `manifest.json` 正好包含 12 筆物件，每筆均有 `source`, `destination`, `reason`。
- [x] **無額外套件**: 未安裝任何外部工具套件，未修改本題以外之任何目錄或檔案。
