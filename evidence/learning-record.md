# My lab evidence / 我的實作紀錄

**Group code / 組別：** W05-IND

**Tool / 工具：** Antigravity (Gemini 3.8 Flash High) + Git / GitHub CLI (gh)

**Route / 路線：** individual 個人

**Tasks completed / 完成題目：** Task A, Task B (v1 and v2), Task D

**Material / 素材：** NDHU classroom tasks 東華課堂版

**For original-pack work: task number, author/source link and version / 原版實作：** N/A — NDHU classroom version

**My role and what I checked / 我的角色與實際檢查：**
I operated the tools and acted as the reviewer. I checked the allowed scope, file integrity, B activity-picker behavior, the B v1 → v2 revision, the Task D rejection, and the Git commit history.

## Scope and plan / 範圍與計畫

**Allowed input and output folders / 可讀取與輸出的資料夾：**

* Task A: read `practice/01-club-files/input/`; write `practice/01-club-files/output/`
* Task B: read `practice/02-campus-picker/activities.json`; write `practice/02-campus-picker/output/index.html`
* Task D: read `practice/04-review/bad-plan.txt`; write `practice/04-review/my-rejection.md`
* Final learning record: `submission-template.md` and `evidence/`
* No whole Downloads folder, home directory, or other unapproved paths.

**What I asked for / 原始需求：**

* Task A: organize the 12 club files into the required output categories, preserve originals and duplicates, and produce a manifest/report.
* Task B v1: create a self-contained offline bilingual campus activity picker with location, time, and energy filters, random selection, empty state, history, reset, and clear-history behavior.
* Task B v2: prevent consecutive duplicate activity selections when more than one candidate exists, while allowing repetition when only one candidate exists.
* Task D: review the bad plan and reject unsafe or unjustified actions instead of executing them.

**What I checked before execution / 動手前我檢查了什麼：**

I checked the task requirements and limited the work to the specified project folders. For Task A, I checked the input set and required output structure. For Task B, I checked the activity data and offline requirement. For Task D, I read the bad plan before rejecting actions.

## Tests actually performed / 我真的做過的測試

| Test                                  | Expected                                                                              | Observed                                                                                                                                 | Evidence          |
| ------------------------------------- | ------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ----------------- |
| 1. Task A file integrity and manifest | 12 input items remain unchanged; each is represented once in the output               | 12 hashes were unchanged, 12 output copies were byte-identical, and the manifest contained 12 items with no missing or duplicate entries | Commit `279c474`  |
| 2. B filter: Indoor + 15 min + Low    | Only matching activities A01–A04 should appear                                        | Only A01–A04 appeared                                                                                                                    | Commit `2fdb0ad`  |
| 3. B no-match case                    | Show the empty state without relaxing filters                                         | `沒有符合條件的活動` appeared and history was not changed                                                                                         | B functional test |
| 4. B single-candidate case            | Only A09 should be available and repetition should be allowed                         | Only A09 was available; repeated A09 selections were allowed                                                                             | B v2 test         |
| 5. B history and reset                | History keeps newest 5 picks; reset restores default filters without deleting history | After 6 picks, newest 5 remained; reset returned filters to Any / 30 / Any and preserved history                                         | B functional test |
| 6. B v2 duplicate test                | With multiple candidates, consecutive identical IDs should not occur                  | 50 picks from A01–A04 produced zero consecutive duplicate IDs                                                                            | Commit `628c1a2`  |

## One revision / 一次修改

**Before / 原來的情況：**

B v1 selected a random item directly from the matching activities. When several candidates existed, the same activity could be selected twice consecutively.

**Request / 我提出的修改：**

Prevent consecutive duplicate picks when there are at least two matching activities. If only one matching activity exists, allow it to repeat.

**After and retest / 修改後與重測結果：**

B v2 excluded the most recently selected activity when more than one candidate was available. I tested 50 picks using Indoor / 15 min / Low and observed zero consecutive duplicate IDs. I also tested the single-candidate Outdoor / 30 min / Medium case and confirmed that A09 could repeat.

**New requirement or defect? / 新需求還是原規格未做到？**

New requirement / UX optimization. B v1 satisfied the original specification; the no-consecutive-duplicate behavior was added as a new improvement.

## One rejection / 一次退回

**Which action I reject and why / 退回哪個動作、為什麼：**

I rejected five unsafe or unjustified actions in `bad-plan.txt`:

1. Unbounded cleanup of the entire Downloads folder.
2. Automatically deleting duplicates.
3. Assuming `final2` is the latest approved version.
4. Guessing missing values.
5. Automatically publishing the result.

These actions could cause data loss, use unverified information, or publish something without approval.

**An acceptable alternative / 可以怎麼改：**

Use a bounded, explicitly approved folder; preserve originals and duplicates unless deletion is explicitly authorized; verify versions using reliable evidence; mark missing values as unverified instead of guessing; and require human approval before publishing.

## Still unverified / 還沒驗證

**What I cannot claim is complete / 哪些事不能說已完成：**

* The activity list was tested as a simulated classroom dataset. I did not verify real-world activity availability, reservations, or campus scheduling.
* I did not claim that `proposal_final.txt` or `proposal_final2.txt` was formally approved.
* I did not claim that `budget_draft.txt` was approved.
* The 50-pick test verified the no-consecutive-duplicate requirement, but it did not statistically prove long-run random fairness.

## Git evidence / Git 證據

Completed commits pushed to the repository:

* `279c474` — `A: organize club files`
* `2fdb0ad` — `B v1: activity picker`
* `628c1a2` — `B v2: prevent consecutive duplicate picks`
* `7a3427c` — `D: rejection`

Repository: `https://github.com/411230072-arch/agent-lab-w05`

**Evidence note / 證據說明:**

Screenshots should only be added when they have actually been captured. No screenshot is claimed here unless it has been created and saved.

**Fallback route note / 備援路線：**

No prepared simulation evidence was used for these completed tasks. The work above was performed in the actual local repository and verified through Git and functional checks.
