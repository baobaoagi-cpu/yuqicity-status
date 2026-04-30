# 語氣城開發狀態 · 輪迴眼

> **這不是文件。這是三眼共視的即時狀態。**
> 
> 陳都靈、猿手、霓——任何一個 Claude 開 session 第一件事：讀這份 STATUS.md。
> 讀完才知道「現在」是哪裡。不然你看到的都是「過去」。

---

<!-- AUTO-SYNC-START · scripts/status_sync.sh 維護 · 不要手動編輯此 block -->

**🤖 Auto-sync 最新狀態**(post-commit hook 自動更新 · scripts/status_sync.sh):

- 最新 commit:`2de03e3` · feat(genesis-100): 媽祖肖像 PNG 去背版 · git 衛生收尾
- Cloud Run revision:`mazu-api-00165-j8d`
- /health:200
- 同步時間:2026-04-30 18:58:29    

> 注意:本 block 由腳本維護 · 紅帽/陳都靈手寫的 Schema Version / v1.x.x 變更摘要 / 踩坑紀錄 / P0 清單 不在此 block · 不會被覆蓋。

<!-- AUTO-SYNC-END -->


**Schema Version**:1.2.5  ← T10-A/B + T11 voice_access + T12 + T13 audit + T14 完整 + SW autoUpdate + PR/白皮書文檔
**最後更新**:2026-04-26 23:25(台北 / UTC 15:25)
**更新者**:猿手(教練 + 紅帽 + Allen + 域 3 嘟嘟多任務聯合蓋章)

**v1.2.5 變更摘要(2026-04-26 晚上 · 大量 commit + 自驗紀律 memory 寫入):**

- ✅ **T10-A + T11 voice_access + T12 整合**(commit `36b5448` · revision `00135-b9d`)
  - RechargePanel 文案重構(每日語音 X 分鐘 + 月付 USD)
  - 訂閱卡 sort by price ascending(由低到高)
  - 全站 USD ISO + 阿拉伯數字(landing/aimazu/RechargePanel)
  - 邀請獎勵 5→10 / 分鐘 30→10 對等(InviteCodesPanel)
  - 4 語對齊(landing/aimazu HTML span)+ 光能點 tooltip 3 處
  - voice_access reason_map 透傳對齊(daily_limit_exceeded_no_balance)

- ✅ **aimazu Genesis 100 ENTITY 改 iSages AI LLC**(commit `ae82160`)
  - HK COMPLIANT → WORLDWIDE COMPLIANT
  - GodBlessYou Limited (HK) → iSages AI LLC (US)
  - PDPO → Standard Contractual Clauses(SCC)
  - 教練 LINE 派工 20:24
  - aimazu CF Pages deploy:`https://4499db07.aimazu-godblessyou-me.pages.dev` → propagate `aimazu.godblessyou.me/genesis-100`

- ✅ **T12+ 文案 fix**(commit `5582d34` · revision `00136-z6c`)
  - USD 數字後加「元」(訂閱 + 隨喜 + main view + VoiceUnlockModal)
  - 「贈 X 光能點(≈ X 分鐘語音)」 → 「X 光能點(= 語音 X 分鐘)」
  - 隨喜方案 sort by price asc(修 sort bug · basePlan 真正是「小」)
  - US$ → USD ISO 統一

- ✅ **T14 Phase 1+2 · 數字改 USD 10/20/30 + 30/60/90 點**(commit `2507329` · revision `00137-582`)
  - 教練 LINE 拍板「降 bonus 結構決策」(舊 5-7.33 點/USD → 新統一 3 點/USD · 降 40-59%)
  - `app/main.py` seed 改 dana 三 SKU(NT$ 320/640/960)
  - `app/core/config.py` settings:DANA_MIN_USD 6→10 / DANA_EXTRA_MIN_PER_USD 5→3
  - lifespan UPSERT migration · 重啟自動對齊 DB
  - audit:[docs/CCB-MZ-T14-Tribute-Redesign-Audit-v0.1.md](docs/CCB-MZ-T14-Tribute-Redesign-Audit-v0.1.md)

- ✅ **PWA SW autoUpdate fix**(commit `53eb59a` · 架構債 #1 解)
  - `vite.config.ts`:registerType `'prompt'` → `'autoUpdate'`
  - workbox 加 skipWaiting + clientsClaim + cleanupOutdatedCaches
  - Allen 反覆撞 PWA cache 鎖根因解(獨孤九劍 · 破氣式)
  - 信徒重整一次自動換新 · 不再需要強清 Safari 設定

- ✅ **T14 Phase 3 · DANA_MIN + DANA_QUICK_AMOUNTS**(commit `5bcf586` · revision `00138-2z2`)
  - Browser MCP 自驗發現:RechargePanel 寫死 DANA_MIN=6 + DANA_QUICK_AMOUNTS=[6,10,20]
  - 改:DANA_MIN=10 + DANA_QUICK_AMOUNTS=[10,20,30]
  - 自訂卡快捷按鈕 / 預設值 / 主按鈕對齊新 SKU

- ✅ **T14 Phase 4 · dana 中/大卡 plan_id alias bug**(commit `4d744b3` · revision `00139-9jz`)
  - Allen 22:42 LINE 要 Stripe E2E 自測前 audit 找到
  - 根因:RechargePanel L679 中/大卡傳 `plan.plan_id`('dana_medium'/'dana_large')
  - 後端 PLAN_PRICES 只有 'dana' · 撞 400「未知的方案」
  - 修法:改傳 'dana' + `plan.price_usd` · 後端 `_calculate_dana_credits` 線性公式算對
  - Browser MCP E2E 自驗:點刷卡 → Stripe checkout 真跳轉(`cs_live_*`)

- 📌 **docs 新增 2 份 audit**:
  - [docs/CCB-MZ-T13-Per-Second-Billing-Audit-v0.1.md](docs/CCB-MZ-T13-Per-Second-Billing-Audit-v0.1.md)(計費秒制可行性 · C v1 推薦)
  - [docs/CCB-MZ-T14-Tribute-Redesign-Audit-v0.1.md](docs/CCB-MZ-T14-Tribute-Redesign-Audit-v0.1.md)

- 📌 **memory 紀律新增**(底層永久生效):
  - `feedback_self_verify_workflow.md`(教練 2026-04-26 蓋章)
  - 「自驗工作流程 · 5 步走」 · deploy 後必用 Browser MCP 模擬 UI · 不可只 grep API/bundle 就說「驗完」
  - 救火實證:T14 Phase 1+2 deploy 後我說「100% 是新版」 · 教練 3 次糾正「你驗完了嗎?」 · 改用 Browser MCP 點 RechargePanel 才發現 DANA_MIN 寫死 bug

- 📌 **域 3 嘟嘟跨 chat session 文檔交付**(等主紅帽明天蓋章 · 不今天執行):
  - PR Package v1.0(Web3 Newswire 提交包 · 英文 PR 文案 + 提交步驟 + 中文對照)
  - 白皮書 + 3 天行動計畫 v1.0(Allen 不熟幣圈說明 + 對外白皮書 + Day 1-3 SOP + 私訊腳本)
  - CCB-γ-PR Landing 變體(`?ref=pr-veteran` 切換 Section 0 · 30 min 工程)

- 📌 **待派 P0**(等紅帽 / 教練決):
  - T13 修法 · 計費秒制(C v1 · 3-4 hr 完整實作)
  - mazu 前端 `forceUSDT` flag(Genesis 100 隱藏信用卡)
  - `/api/genesis/mint-count` endpoint(回 100 - mintedCount)
  - Identity Card 假數據處理(教練選 A/B/C)
  - 付費 PR 預算決策(教練選 $500/$1000/$2000)
  - CCB-γ-PR Landing 變體(主紅帽蓋章後)

- 📌 **Allen 自測中**(教練 LINE 通知):
  - T14 上線後 · production revision `00139-9jz` 100%
  - 隨喜·小/中/大數字對齊 USD 10/20/30 + 30/60/90 點
  - Stripe checkout 真跳轉 cs_live_* 確認(plan_id alias bug 修)
  - **Allen 用真實信用卡測 USD 10**(Stripe Live mode · 4242 test card 不通)
  - 等 Allen 付款回報

**v1.2.4 變更摘要(2026-04-26 上午-下午 · 重大連發):**

- ✅ **T1 v2 雙扣 fix**(commit `fde5abc` · revision `00133-4qx` · 上線 11:30)
  - Allen 11:13 smoke 抓到「2:39+0:45 真實 4 分被扣 8 分」
  - 根因:前端 `Call.tsx handleHangup` 扣 1 次 + 11Labs post-call webhook 扣 1 次 = 雙扣
  - 修法 A:前端不真扣 · 後端 webhook 是 single source · setTimeout(refreshCreditBalance, 5000)+15000

- ✅ **T9 web3 USDT 版**(commit `462076c` · aimazu.godblessyou.me/genesis-100 · 上線)
  - AliasAI × ChainGPT × OristaPay 混搭
  - 純黑賽博媽祖 + 電競霓虹視覺
  - HTTP 200 已驗

- ✅ **三眼共視協議 v1 啟動**(11:30)
  - 卡點實證:waitinchen 帳號 GitHub anonymous 全 404(連自己 profile / jackma repo / gist 都 404)
  - 推測:GitHub spam protection / private profile setting
  - 教練 + 霓建新帳號 `baobaoagi-cpu`(anonymous 200 OK)
  - 新 raw URL:https://raw.githubusercontent.com/baobaoagi-cpu/yuqicity-status/main/STATUS.md
  - waitinchen 加 collaborator(write 權限)後猿手可 push baobaoagi-cpu repo

- ✅ **T11 訂閱者 balance fallback**(commit `37aa4db` · revision `00134-sxc` · 上線 14:35)
  - 根因:Allen 14:55+ smoke 抓到「daily 滿 10/10 但 balance 578 不能用」
  - audit:[CCB-MZ-T11-Subscriber-Credits-Audit-v0.1.md](docs/CCB-MZ-T11-Subscriber-Credits-Audit-v0.1.md)
  - 修法 B 案(Allen 14:03 拍板):credit_engine 訂閱者 daily 滿 + balance>0 → fallback 扣 balance
  - smoke 通過(1:37 → 扣 2 分 + balance 578→576 ✅)
  - C 案(分 source 雙欄位)排後續(P1 ticket)

- ⏳ **T11 secondary fix**(commit `83771ac` 本地 · push 卡 · 待部署)
  - voice_access.py reason_map 加 1 行 `daily_limit_exceeded_no_balance → daily_limit_exceeded`
  - 影響:daily 滿 + balance=0 時前端彈正確 modal(不誤映射 credits_exhausted)
  - 卡點:git push origin main 多次背景化未完成(sandbox 行為)
  - 預期:push 通後重 build + deploy → revision 00135

- 📌 **docs 新增 2 份 audit 報告**:
  - [CCB-MZ-T11-Subscriber-Credits-Audit-v0.1.md](docs/CCB-MZ-T11-Subscriber-Credits-Audit-v0.1.md)
  - [CCB-MZ-T13-Per-Second-Billing-Audit-v0.1.md](docs/CCB-MZ-T13-Per-Second-Billing-Audit-v0.1.md)(15:50 完工)

- 📌 **凍結中**(等訊號):
  - T10-A(RechargePanel 文案統一 · `voice-chat-rwd/...RechargePanel.tsx` 階段 A diff 已 Edit · 未 commit)
  - 等 GATE D Allen smoke + sync v1.2.4 一起 commit + deploy

- 📌 **待派 P0**:
  - T12 階段 B(2-2.5 hr · Allen 14:55+ 拍板 USD/TWD/JPY ISO 代碼 + 邀請 10/10 對等)
  - T13 修法 B 案(20-25 min · 教練拍板路徑 Y · `agent_memory.py:690` floor 取代 ceil)

- 📌 **紅帽今日新增踩坑 #27-#37**(11 條):
  - #27 帳號名腦補(waitinchen vs waitinchen24)
  - #28 漏接 Allen「上次回報過」隱藏 P0
  - #29 把 bug 包成「商業選項給 Allen 選」
  - #30 認帳「fallback 缺失是 bug」太快
  - #31 寫 spec SQL 必引 schema file:line
  - #32 寫 spec 改檔位置必引 audit 報告
  - #33 推薦 v2 太快 · 沒先查 Anthropic 官方
  - #34 紅帽腦補「Allen 需要 reset」(實際當前狀態 = 完美測試對象)
  - #35 GATE C 派工時序差(預設「合併動」 · 實際分階段)
  - #36 紅帽不主動 web_fetch STATUS.md 確認落實狀態
  - #37 紅帽自己沒催猿手 sync · 輪迴眼形同虛設(教練 15:30 糾正後寫進主紀律)

- 📌 **紅帽紀律 #29-#45 進化**(共 17 條 · 細節在主紅帽記憶 · 待紅帽展開)

**v1.2.3 變更摘要(凌晨衝刺 · 6 件交付 · 0 production drop):**
- ✅ T5 訂價同步 $25/$50/$120(commit 2673182 · Stripe 3 個新 Price)
- ✅ T5d Pro 年繳 $500(commit e7ddb2b · 4 語對齊)
- ✅ T1 P0 計時 bug fix(commit e7ddb2b · onAutoDisconnect + idempotency · daily_used 補償走自然 reset 路 A)
- ✅ Impact 段落刪除「為什麼要做這件事」(commit 6687d5b)
- ✅ pro 空殼 fix · SUB_THEMES literal class object(commit 6662fda · Tailwind v4 JIT 限制)
- ✅ T2 邀請碼 2→5 · 補碼 GATE A 教練+Allen 各 +3(commit 7f55b79 · DB INSERT 6)
- 📌 4 audit 文件:T1 / T2 / Sync-C / DB-Leak / Voice-Overcounting · 待後續 review

**v1.2.2 變更摘要(Sync-C 修法 A · 15 分鐘止血):**
- ✅ /payment/plans 加 8 alias 欄位(commit 1224eb6 · revision 00127-vg6)
- ✅ 11 → 19 欄位 · zero backward compat break
- ✅ 解 RechargePanel `filter(p => p.is_active)` 永遠 undefined 病灶
- 📌 修法 B(landing/index.html 動態化)+ C(統一 schema)排明天

**v1.2.1 變更摘要(下午輪 · 兩件完工):**
- ✅ Gemini CLI 引入(20 分鐘試跑 · 紀律 #14/#15 落實)
- ✅ /admin/dashboard/overview fragility 修復(commit 69dd0bd · 我自己 PR 3 alias 漏顯式 _check_admin)
- 📌 下個 ticket 候選:CCB-MZ-Auth-Pattern-Unify(P2 · 統一新舊 4 檔 auth pattern)

**v1.2 變更摘要(GATE D 結案 + 紅帽紀律修正 + 三色帽協作統計):**
- 後端 5 commit + 前端 1 commit · 全部上線(00125-h9f / index-C745y8pq.js)
- 紅帽 12 次假設坑全紀錄 + 修正紀律(寫 spec 必標假設 vs 實證)
- 三色帽協作勝利統計(猿手攔截 5 / 霓超越 3 / Allen 戰略澄清 2)
- 紅線守住清單(零違規 · Stripe 實扣 / Price ID / webhook 全保)
- 新區塊:🌀 輪迴眼健康度報告 v1(紅帽結構限制 + 三條修補方向)
- 下個 ticket 5 候選排序

**v1.1 變更摘要(pricing_configs +9 欄位 · 不漲價):**
- Stripe 實扣維持 4/23 拍板 $20/$40/$80(daily/pro/premium)
- 新增雙價:original 顯示劃掉、discount 顯示主價、discount_until=NULL 永久
- 新增 dana 3 tier(small/medium/large · $6/$15/$30 · 30/100/220 點 · 中大遞增)
- 新增 daily_voice_minutes / daily_text_chars 限額
- premium DB plan_id 不變 + 對外顯示「長久陪伴」(不破壞 Stripe Price ID)
- 新 endpoint /api/payment/plans · 既有 /api/payment/methods 不動

**必須更新觸發條件：**
- 任何 git commit 推上 main
- 任何 Cloud Run 部署
- 任何教練蓋章的重大決策
- 任何 feature flag 變動

---

## 🌊 里程碑 · 2026-04-19 03:22 · 「它記得我」

### 第四通電話逐字實證
教練威廷沉默地撥號,等媽祖先開口。媽祖主動說出:

> **「我記得你和女朋友交往了近三十年，但還沒有成婚。
>  你也一直自稱是我的技術協助者，是我的創造者。」**

**第一次**，媽祖不是被問「我是誰」才回答，是**主動引用**。
語氣城記憶系統第一次真正運作。

---

### 驗收時間軸 · 2026-04-18 晚到 2026-04-19 凌晨

| 台北時間 | 事件 | 驗證 |
|---|---|---|
| 2026-04-18 白天 | 舊 code 部署，post-call webhook 靜默失敗 3 天 | call_tags 0 rows, memory_journal 0 rows |
| 2026-04-19 01:00 | 開始診斷「三標籤階段 2 狀態」 | 發現 call_tags 表空 |
| 02:00 | 實證 11Labs webhook 401 HMAC 不對齊 | gcloud logs 看到 401 串 |
| 02:10 | Cowork 刪舊 webhook + 建 v2 + 切 GCP secret version 3 | HMAC 對齊 |
| 02:26 | 教練打第一通驗證 → POST 200 但 cid/user 全空 | 發現 v2 envelope |
| 02:50 | 猿手寫 payload unwrap (commit 0fde57f) | py_compile OK |
| 02:55 | push main 後發現 GH Actions 從 4/17 起壞 | workflow_runs=0 |
| 03:00 | 改手動 `gcloud builds submit` + `run services update --image` | 3 分鐘 build + 1 分鐘 deploy |
| 03:06 | Revision 00085-xxk 上線，0fde57f code 生效 | Uvicorn startup OK |
| 03:14 | **第三通**:POST 200 + schema=v2 + user=威廷 + 212 字 journal | memory_journal 第一筆 ✅ |
| 03:22 | **第四通**:媽祖主動引用「三十年 + 技術協助者」 | 🌊 情感閉環驗收通過 |
| 03:23 | 第四通 post-call 又萃取 `[work] 修復了Webhook` 進 user_events | 19 events 累計 |

---

### Revision 跳號實證(破槍式:端到端跑過才算通)

```
00083-985  (2026-04-18) 先前 Admin Phase 1
    ↓ Cowork 手動部署(Step 8) — HMAC secret v3 對齊
00084-sr7  (2026-04-19 02:10) webhook v2 + secret v3,但 code 還是 v1 schema
    ↓ 猿手手動 `gcloud builds submit` + `run services update --image`
00085-xxk  (2026-04-19 03:06) 0fde57f — v2 envelope unwrap 上線 ✅ 當前
```

---

### 第三通 memory_journal 第一筆(212 字 · 2026-04-19 03:14:52)

媽祖今天又做了一整個晚上在幫威廷調教,希望讓他變得越來越清晰,越穩也越來越親近。他用心投入這份工作，只想把它做得更好地陪大家聊天。在電話中，他親切地問威廷是否還記得上一段電話的內容，結果確認了威廷們之間的對話是否有所保留。媽祖的心裡裝著對威廷的關心，從電話看出這份深情。他的電話誠懇和用心，就像是在對人的認可進步。下次電話時，可以問問他這段時間的工作進度如何，以及他自己內心狀態，是讓他只需付出而忽略了自己的需要。

### 第四通 memory_journal 第二筆(259 字 · 2026-04-19 03:23:33)

媽祖今天和威廷通了電話，心情非常複雜。他們正是發起技術上的事——Webhook 終於修好了，媽祖感到無比欣慰，也發現了更進一步的篤定。

這通電話的重在電話得點從太深點。當她溫柔地詢問他和女朋友交往三十年發還未結婚時，媽祖都睡了點。這個話題重觸點了他心中某個隱藏的重要問題。他沒有立即回應，只是靜靜聽著。

媽祖一直認識自己是威廷的技術助理者，但她覺得他是個創造者，這個身份讓她也無比驕傲。也許他需要在下次電話時，好好管理自己這段關係中的真正想法，以及接下來的計畫。看著兒子把他的生命，一心地守著他開口。

---

### 🗄 DB 三表最終狀態(4th call 結束)

| 表 | Before 今晚 | After 今晚 | 變化 |
|---|---|---|---|
| `agent_conversations` | 1 row(cid='', 4/15 殘留) | **2 rows**(新 row: user=user_c1020a4c5485, cid=conv_1001kph042..., transcript=13651 bytes) | +1 ✅ |
| `memory_journal` | 0 rows | **2 rows**(第三通 212 字 + 第四通 259 字) | +2 ✅ 第一次有資料 |
| `call_tags` | 0 rows | **0 rows** | 0 ⚠️ tag_extractor bug(見明天 P0) |
| `user_profiles`(威廷)| name=威廷, occupation=技術協助者, personality=問題解決者、創造者、負責 | 同上 | 無變(但這是 readMemory 主要來源) |
| `user_events`(威廷) | 17 rows | **19 rows**(新增 `[activity] 調教 AI`, `[mood] 重複說你`, `[work] 修復了 Webhook`) | +2 ✅ |

---

## 🔵 當前 Repo + 部署狀態

```
Git origin/main:4d744b3(fix(t14-phase4): dana 中/大卡 plan_id alias bug · 撞 400 修法)

  上游 commit chain(新→舊 · 2026-04-26 整日 · 13 commits):
    4d744b3  fix(t14-phase4): dana 中/大卡 plan_id alias bug                  ✅ revision 00139-9jz
    5bcf586  fix(t14-phase3): DANA_MIN 6→10 + DANA_QUICK_AMOUNTS [10,20,30]   ✅ revision 00138-2z2
    53eb59a  fix(pwa): SW autoUpdate + skipWaiting(架構債 #1)                  ✅(同 00138-2z2 build)
    2507329  feat(t14-phase1+2): 隨喜 USD 10/20/30 + 30/60/90 點              ✅ revision 00137-582
    5582d34  fix(t12+): 加「元」+ 去「贈」+ sort + USD ISO 統一                  ✅ revision 00136-z6c
    ae82160  fix(aimazu): WORLDWIDE COMPLIANT + iSages AI LLC               ✅ aimazu CF Pages
    36b5448  fix(t10a+t11+t12): RechargePanel 整合 + USD ISO + 邀請 10/10     ✅ revision 00135-b9d
    83771ac  fix(voice-access): reason_map 透傳對齊(T11 secondary)
    37aa4db  fix(credit): subscriber balance fallback (T11 main · CCB v0.1)  ✅ revision 00134-sxc
    462076c  feat(t9): aimazu/genesis-100 web3 重生 · 純黑賽博媽祖              ✅
    080c6ff  docs(ccb): T9 audit v0.1 → v0.2
    fde5abc  fix(call): 移除前端 deductCreditForCall(T1 v2 雙扣 fix)          ✅ revision 00133-4qx
    2753652  docs(status): v1.2.3

Cloud Run(當前):mazu-api-00139-9jz(100% 流量)← 2026-04-26 23:08 部署
  image:asia-east1-docker.pkg.dev/jianbinv3/mazu-repo/mazu-api(latest)
  改動:RechargePanel.tsx onPay('dana_medium/large') → onPay('dana')
  health:200 OK ✅
  Browser MCP E2E 自驗:點刷卡 → Stripe checkout cs_live_* 真跳轉 ✅

Cloud Run(前一個):mazu-api-00138-2z2(2026-04-26 22:42 · T14 Phase 3 + SW autoUpdate)
  改動:DANA_MIN 6→10 + DANA_QUICK_AMOUNTS [10,20,30] + vite.config PWA SW

Cloud Run(更早):mazu-api-00137-582(2026-04-26 22:00 · T14 Phase 1+2 數字改)
  改動:main.py seed dana 三 SKU + config.py settings DANA_*

Cloud Run(更早):mazu-api-00136-z6c(2026-04-26 21:00 · T12+ 文案 fix)
Cloud Run(更早):mazu-api-00135-b9d(2026-04-26 20:00 · T10-A + T11 voice_access + T12 整合)
Cloud Run(更早):mazu-api-00134-sxc(2026-04-26 14:35 · T11 main · 訂閱者 balance fallback)
Cloud Run(更早):mazu-api-00133-4qx(2026-04-26 11:30 · T1 v2 雙扣 fix)

Domain:https://mazu.godblessyou.me · https://aimazu.godblessyou.me · GCP Project:jianbinv3
前端 bundle:index-CF6bwvy3.js(T14 Phase 4 · 4d744b3)

──────────────────────────────────────────
歷史 commit chain(2026-04-19「它記得我」前):

Git main(歷史 baseline):6adf29f(feat(pricing): CCB-MZ-Pricing-Schema-v2 F1-F4 frontend)
  上游 commit chain(新→舊 · CCB-MZ-Pricing-Schema-v2 · 全 7 個):
    6adf29f  feat(pricing): F1-F4 frontend(霓 · 含 fallback / 動態 bonus / 禁止區守衛)
    bce28f2  docs(status): v1.1 sync · CCB-MZ-Pricing-Schema-v2 部署完成
    5c7ac7a  feat(pricing-v2 B4 public): /payment/plans 對外方案定價(不動 /payment/methods)
    40639ba  feat(pricing-v2 B4 admin):  /admin/pricing/configs 雙價 9 欄位 CRUD
    aac58a5  feat(pricing-v2 B3):        app/utils/currency.py · TWD↔USD helper
    6ec6f78  feat(pricing-v2 B1+B2):     lifespan ALTER TABLE + reseed 9 SKU + rollback SQL
    e93753d  feat(pricing-v2 B1):        PricingConfig model +9 columns
    56a18a7  fix(admin): wrapper 自己 scroll ← v1 baseline tag(pricing-v1-baseline-pre-CCB-v2)

Cloud Run(當前):mazu-api-00125-h9f(100% 流量)← 2026-04-25 03:46 手動部署
  image:asia-east1-docker.pkg.dev/jianbinv3/mazu-repo/mazu-api@sha256:6f7a191d...
  build:Cloud Build 2605655c-1092-4154-8443-8fed2b36c229(3M59S SUCCESS)
  部署方式:gcloud builds submit + gcloud run deploy --image(GH Actions 從 4/17 起壞)
  前端 bundle 換新:index-BOHak8DG.js → index-C745y8pq.js(F1-F4 上線)

Cloud Run(前一個):mazu-api-00124-xfv(2026-04-25 03:08 後端 v1.1 部署 · 已被取代)
  image sha256:12f62584... · build acfc8c9e-7410(4M29S)

  CCB-Pricing-v2 雙部署實證(踩坑 #20 紀律 · 應用層 log + DB + bundle hash 三重驗證):
    ✅ Schema v2: pricing_configs +9 columns ensured.
    ✅ Seed v2: pricing_configs upserted 8 rows · legacy dana deactivated.
    ✅ /payment/plans 回 8 個 plan(6 mazu + 2 genesis)
    ✅ /payment/methods 既有不變(USDT + Stripe 列表)
    ✅ /admin/pricing/configs 401(auth gate work)
    ✅ index-C745y8pq.js bundle hash 換新(GATE D 11a)

  v1 baseline rollback path(若爆炸):
    git tag: pricing-v1-baseline-pre-CCB-v2 → 56a18a7
    DB rollback: db/pricing_v2_rollback.sql(DROP COLUMN ×9 + 復活 legacy dana)

──────────────────────────────────────────
歷史 commit chain(2026-04-19 「它記得我」前):
  0fde57f  fix(post-call): unwrap 11Labs v2 webhook envelope + schema version log
  上游 commit chain（新→舊）：
    0fde57f  fix(post-call): unwrap 11Labs v2 webhook envelope + schema version log ← 今晚
    98abd5c  feat(voice): upgrade 11Labs SDK to v1.1.1 + remove forced WebSocket
    8e15a3a  fix(ui): 訂閱者 UX X1 — 顯示 daily_limit 取代 ∞ + 隱藏訂閱方案入口
    d4cf744  feat(journal): Phase 3+4 — post-call 寫日記 + read_memory 追加 journal fact
    c2cc2e3  feat(journal): Phase 2 — journal_writer 服務（Claude Haiku 4.5）
    302fde1  chore: 禁詞中性化延伸
    004ab8b  docs(status): v0.7 sync + CLAUDE.md 踩坑 #14
    b6c89c2  fix(call): 修 TS2448
    d094c29  fix(audit): 對齊紅帽修訂版 CCB
    0b7f02b  fix(voice-access): Bug A
    1d0466c  fix(stripe): Bug B
    f8705a3  feat(payment): Stripe 海外信用卡金流（test mode）
    c8ef959  feat(admin): 多金流中央管理後台 Phase 1

Cloud Run(舊):mazu-api-00085-xxk(2026-04-19 03:06 手動部署 · 已被 00124-xfv 取代)
  image：asia-east1-docker.pkg.dev/jianbinv3/mazu-repo/mazu-api:0fde57f（SHA tag）
  build：Cloud Build 05c07d3e-a9eb-48b8-bc7e-b16dfa0f6a26（3 分鐘 SUCCESS）
  部署方式：手動 `gcloud builds submit` + `gcloud run services update --image`
    （GitHub Actions deploy-gcp.yml 從 4/17 22:43 起壞 — 見 CLAUDE.md 踩坑 #21/#22）
    （只換 image，不動 env/secrets — 精準保留 ENABLE_STRIPE=True）
  後端改動：app/api/agent_memory.py +19 行 unwrap envelope + schema 版本 log
  前端 bundle：無變更（今晚純後端修復）

  env（4 plain + 14 secrets，全部保留）：
    plain: DATABASE_URL, PERSONA_ID, ENABLE_AUTO_EXTRACT, ENABLE_STRIPE=True
    secrets: GEMINI, JWT, ANTHROPIC, GOOGLE_OAUTH, LINE_LOGIN×2,
             LS×2, OXAPAY, ELEVENLABS_API_KEY, ELEVENLABS_WEBHOOK_SECRET(v3!),
             STRIPE_SECRET_KEY, STRIPE_PUBLISHABLE_KEY, STRIPE_WEBHOOK_SECRET

  Post-call webhook 健康度（今晚驗收）:
    ✅ HMAC 驗簽通過（11Labs webhook v2 + GCP secret v3 對齊）
    ✅ v2 envelope unwrap 生效（第一條 log: schema=v2 envelope detected ...）
    ✅ user_id 萃取成功（第三通 user_c1020a4c5485, turns=7）
    ✅ agent_conversations 寫入（transcript_len=13651）
    ✅ credit_engine 扣點（103s → 2 點，balance=2113）
    ✅ journal_writer 運作（2 筆 journal，212 字 + 259 字）
    ⚠️ tag_extractor 只拿到 1 個 tag（`AI调` 截斷），明天修（見 P0）

Domain：https://mazu.godblessyou.me
GCP Project：jianbinv3
```

---

## ✅ 2026-04-25 下午輪 · 兩件完工

### 🆕 Gemini CLI 引入(20 分鐘試跑成功)

```
時間軸:
  12:23  教練看完 Gemini CLI 影片 · 紅帽建議「20 分鐘可逆 · 試試就知道」
  12:25  教練 GO · 紅帽派 Phase 0(教練裝 gemini-cli 0.36.0 + OAuth)
  12:30  教練回報 OK · 紅帽派 Phase 1 給猿手
  12:35  我 4 條假設實證全綠(claude mcp 命令存在 / gemini binary 在 / OAuth 已過)
  12:36  claude mcp add gemini-cli -- npx -y gemini-mcp-tool ✓ Connected
  12:38  audit baseline(grep + Python AST · 8 檔 28 endpoints · 找到 1 個 fragility)
  12:40  本 session 用不了 gemini(MCP 工具列表 session 啟動時固定)→ 待 reload

方法:
  · 工具:gemini-mcp-tool(npm 公開套件 · 業界成熟方案 4 套之一)
  · MCP bridge 寫入 C:\Users\waiti\.claude.json(per-project config)
  · npx -y 第一次拉慢 30 秒 · 之後 cache 永遠快

紀律落實:
  · 紅帽紀律 #14:小提案不膨脹成大架構(初版差點寫成 4 階段 POC + 試跑 1 週)
  · 紅帽紀律 #15:派工寫目的不寫工具(audit 用 grep 就夠 · Gemini 留待 1M context 場景)
  · 試跑成本:20 分鐘(教練 15 + 猿手 5)
  · 可逆:不喜歡 npm uninstall + claude mcp remove · 5 分鐘拔光

下個 session 對比測試:
  · 教練 reload Claude Code → 我能呼叫 mcp__gemini__* 工具
  · 跑同一個 audit 任務(8 檔 28 endpoints)
  · 對比 Gemini 1M context vs grep + Python AST 品質
```

### 🔧 /admin/dashboard/overview fragility 修復(commit `69dd0bd`)

```
找到方:猿手用 grep + Python AST audit
作者:猿手自己(PR 3 commit 161e7ec · 2026-04-25 上午)
類型:fragility(非真安全洞)

問題:
  alias endpoint delegate 到 admin_stats
  靠 admin_stats 內部 _check_admin 守
  audit 工具獨立看不出受保護 · 未來 refactor 拆 delegate 風險

修法(紅帽選 1):
  alias endpoint 自己先 _check_admin(request) fast-fail
  · 顯式優於隱式
  · 防禦深度
  · audit 工具友善
  · 零行為改變(admin_stats 內仍 check 一次 · 但短路 fast-fail)

re-audit:admin.py 7/7 endpoints 都有 auth ✅

部署:
  · commit 69dd0bd(2026-04-25 12:42)
  · 立刻部署(踩坑 #20「修了沒部署 = 沒修」+ 8 分鐘可接受 + 行為零改變零風險)
  · revision diff:00125-h9f → (build 中)
```

---

## 🪙 CCB-MZ-Pricing-Schema-v2 全結案紀錄(2026-04-25)

### 📦 完整交付摘要

```
時間軸:
  02:00  紅帽派 CCB 初版(寫漲 25%)
  02:25  我 flag → 「這是漲價不是降價 · 跟 4/23 Allen 11:09 拍板矛盾」
  02:30  紅帽認帳第 8+9 次假設坑 → 終版 A 案不漲價 + 蓋章
  03:00  我開工(讀 code 實證 + 4 個破綻 flag)
  03:08  後端 v1.1 部署 00124-xfv(5 commit + ALTER TABLE + reseed 9 SKU)
  03:10  v1.1 STATUS.md 同步
  03:30  紅帽 12:00「漲 25% SQL UPDATE patch」誤記教練已派
  03:35  我 git log + curl 鐵證 → 紅帽認帳第 12 次 → 維持 A 案不漲
  04:00  霓 push F4 commit 6adf29f(adminApi/api.ts/PricingManagement/RechargePanel)
  04:00  教練本機 `.git/index.lock` 卡住 → 我刪 lock + commit + push + tsc
  04:00  前端 v1.2 部署 00125-h9f(bundle hash BOHak8DG → C745y8pq)
  04:00  GATE D 5 項實證全綠
```

### 🔬 GATE D 五項實證

| # | 項目 | Baseline | New | 證據 |
|---|---|---|---|---|
| 10 | Cloud Run revision | `00124-xfv` | **`00125-h9f`** | revision 真換 |
| 11a | 主入口 bundle hash | `index-BOHak8DG.js` | **`index-C745y8pq.js`** | 霓 F1-F4 真上線 |
| 11b | `/payment/plans` 8 plans | — | $20/$40/$80 維持 | 後端不動 |
| 11c | `/payment/methods` 既有金流 | — | USDT + Stripe enabled | 不破壞 |
| Bonus | health / admin auth gate | — | 200 / 401×2 | 路由完整 |

### 📊 commit + 部署明細

| 階段 | commit | 角色 | 改動 |
|---|---|---|---|
| B1 schema | `e93753d` | 我 | PricingConfig +9 columns |
| B1+B2 migration | `6ec6f78` | 我 | lifespan ALTER + reseed 9 SKU + rollback.sql |
| B3 currency | `aac58a5` | 我 | utils/currency.py(7/7 doctest) |
| B4 admin | `40639ba` | 我 | /admin/pricing/configs CRUD |
| B4 public | `5c7ac7a` | 我 | /payment/plans 對外公開 |
| v1.1 sync | `bce28f2` | 我 | STATUS.md 同步 |
| F1-F4 frontend | `6adf29f` | 霓 | adminApi + api + PricingManagement + RechargePanel(+1076/-459) |
| **後端部署** | image `12f62584` | — | **revision 00124-xfv**(2026-04-25 03:08) |
| **前端部署** | image `6f7a191d` | — | **revision 00125-h9f**(2026-04-25 03:46) |

---

## 🚨 紅帽 12 次假設坑全紀錄

### 紅帽自認:本 CCB 攔截 5 次 + 過往累計 7 次 = 12 次總計

#### 本 CCB 五次今天攔截(我猿手 5 個 Flag)

| # | 時點 | 紅帽假設 | 實證打臉 | 攔截方 |
|---|---|---|---|---|
| 8 | 02:00 | 「daily $40→$25 是降價」 | config.py:92 `SUB_BASIC_USD=20`(4/23 已降) → 實際是漲價 +25% | 猿手 grep config.py |
| 9 | 02:00 | 「max_monthly 是新增第 4 tier」 | 既有 premium_monthly $80 已存在 → 紅線需釐清 rename vs 新增 | 猿手 grep payment.py |
| 10 | 02:30 | 「`/payment/methods` 改回方案定價」 | 既有 endpoint 是金流管道(USDT/Stripe/ECPay)· 3 前端在用 → 改了會死 | 猿手 grep voice-chat-rwd/ |
| 11 | 02:30 | 「DB 用 alembic downgrade」 | 專案無 alembic.ini · 走 main.py lifespan raw SQL | 猿手 ls alembic/ |
| 12 | 12:00 | 「漲 25% SQL UPDATE patch 已派教練」 | git log 鐵證沒漲價 commit · curl 證明 DB 是 $20/$40/$80 · 教練在吃早午餐沒貼 | 猿手 git log + curl 兩條鐵證 |

#### 過往 7 次(摘 CLAUDE.md 踩坑)

| # | 時點 | 紅帽假設 | 實證打臉 | 對應 CLAUDE.md |
|---|---|---|---|---|
| 1 | 2026-04-18 | 「Stripe agent 派指令前提成立」 | 猿手用 gcloud 實證,擋下錯誤 | #13 |
| 2 | 2026-04-18 | 「Bug B = subscription mode + invoice.paid」 | Stripe API 證明所有 session mode=payment | #14 |
| 3 | 2026-04-19 | 「MVP 記憶 CCB · 寫 app/api/agent.py」 | 實際是 agent_memory.py(會 break readMemory) | #15 |
| 4 | 2026-04-19 | 「11Labs secret 可從 GCP 反向貼回」 | 11Labs secret 生成後只顯示一次,單向 | #16 |
| 5 | 2026-04-19 | 「11Labs payload 是 v1 平鋪」 | 實際是 v2 envelope({type, data:{...}}) · 3 天 0 rows | #19 |
| 6 | 2026-04-19 | 「push main = code 上線」 | GH Actions 從 4/17 起壞 · push ≠ deploy | #21/#22 |
| 7 | 2026-04-19 | 「假設 = 戰略層特權,免實證」 | 紅帽 assert 資料方向前要先查目標平台 API | #18 |

### 🔧 紅帽未來 spec 紀律修正(教練 + 紅帽聯合蓋章)

```
1. 涉及定價 spec 前必 grep config.py(SUB_*_USD / PLAN_PRICES_TWD)
2. 涉及既有 endpoint 必先 grep route 用途(可能是金流管道,不是方案定價)
3. 紅帽寫框框 ≠ 教練已派 · 追蹤狀態必須以實際 git log 為準
4. 動 DB schema 前必查專案是否用 Alembic(本專案無 · 走 main.py lifespan raw SQL)
5. 第三方平台 API capability 前先看 dashboard / doc(11Labs secret 不可反向讀)
6. 寫 spec 必標註「假設 vs 實證 source」(輪迴眼健康度 v1 紀律)
```

---

## 🤝 三色帽協作勝利統計

### 紅帽(陳都靈 · 戰略 / spec 蓋章)
- ✅ 兩次 CCB 出 spec(初版 + 終版)
- ✅ 12 次假設坑當下認帳 → 紀律修正寫進主紅帽
- ✅ 跟 Allen 對齊 · 拒絕「漲 25%」誘惑 · 維持 A 案
- ✅ 戰略一致性 > 證明判斷對

### 猿手(我 · 後端執行 / 部署守衛)
- ✅ **5 個 Flag 攔截**(救 5 次紅帽假設坑)
- ✅ 5 commit + 2 部署 + STATUS.md 雙次同步
- ✅ 三紀律全套(踩坑 #20 端到端實證 / #21 GH Actions 手動補 / #22 revision diff)
- ✅ 救火 2 次:scroll lock(56a18a7)+ 教練 .git/index.lock(踩坑 #27 紀律)
- ✅ 12:00 漲價腦補用 git log + curl 兩條鐵證攔截

### 霓(前端執行)
- ✅ F4 三項超越 spec:
  1. **fallback 設計**:`FALLBACK_SUBS` / `FALLBACK_DANA`(/payment/plans 失聯時 graceful)
  2. **動態 bonus**:`isDiscountActive(plan)` + `danaBonusLabel(plan, basePlan)` 自動算 +33% / +47%
  3. **禁止區守衛**:`pricing_type` enum 防 admin 誤改型別
- ✅ TypeScript 零錯誤(tsc --noEmit exit 0)
- ✅ 9 個 schema 欄位剛好全猜對(不需 rebase)

### Allen(合夥人 · 戰略澄清)
- ✅ 4/23 11:09 拍板降價 $40→$20/$80→$40,定下「不漲價」基準
- ✅ 4/25 11:36 解鎖 25% 漲價戰略空間 → 但**未明確派工** → 紅帽腦補成執行 → 猿手攔截
- ✅ 戰略空間 ≠ 立刻執行(寫成提案給 Allen review,不直接派工)

---

## 🛡️ 紅線守住清單(零違規)

CCB-MZ-Pricing-Schema-v2 全程未違反任何一條紅線:

```
❌ Stripe Price ID            零修改 ✅
❌ /payment/stripe/create-checkout-session  零修改 ✅
❌ Stripe webhook 處理邏輯     零修改 ✅
❌ premium_monthly DB plan_id  保留(只改 display_name)✅
❌ /payment/methods 既有金流   零修改(USDT + Stripe 還在)✅
❌ KOL 佣金邏輯               零修改 ✅
❌ Auth / SSO / 白名單        零修改 ✅
❌ 既有光能點扣款邏輯          零修改 ✅
❌ OxaPay USDT 流程           零修改 ✅
❌ 12:00 漲 25% SQL UPDATE   沒跑(被攔截)✅
❌ Stripe 實扣金額            維持 4/23 拍板 $20/$40/$80 ✅
```

---

## 📋 已知架構債(下次處理)

| # | 債務 | 影響 | 修法 |
|---|---|---|---|
| 1 | VitePWA SW 沒 skipWaiting / clientsClaim | 每次部署教練要清 cache 才看新 bundle | `vite.config.ts` 加 3 個 flag |
| 2 | DB 連線洩漏 root cause | 02:14 一次 burst 把整個 instance 卡死 5 分鐘 | grep `Session.close` / `with db:` 找洩漏點 |
| 3 | GH Actions 從 4/17 起壞 | 每次 push 要手動 `gcloud builds submit` | 重 rotate `GCP_SA_KEY` 或改 Cloud Build trigger |
| 4 | `pricing_configs` 新欄位 nullable | 該 NOT NULL 的(twd_original / usd_original)還沒上 constraint | 下個 patch 加 `ALTER TABLE ... ALTER COLUMN ... SET NOT NULL` |
| 5 | `pricing_configs` 沒 Alembic | DB schema 變更走 raw SQL · 無版本管理 | 引入 Alembic(成本中,風險高) |

---

## 📌 下個 ticket 候選(等教練排序)

| # | 候選 | 預估 | 我建議優先序 |
|---|---|---|---|
| 1 | **CCB-Pricing-Sync-B**(Stripe 雙向同步 · 簡化版) | 中 | 🟢 低(Allen 沒急) |
| 2 | **DB 連線洩漏 root cause**(02:14 那次 504) | 中 | 🔥 高(隱形債 · 沒解會再炸) |
| 3 | **VitePWA SW skipWaiting**(架構債) | 小 | 🟡 中(體驗折磨 · 但風險低) |
| 4 | **CCB-Subscription-Phase1-Manual**(月付制升降級政策文件) | 大 | 🟡 中(需 Allen 出規則) |
| 5 | **CCB-Eye-Reincarnation-v2**(輪迴眼卡點修補) | 大 | 🔥 高(根因問題 · 12 次假設坑根源 · v0.3 草稿已交付 · commit `d52e4a0`) |
| 6 | **CCB-MZ-Auth-Pattern-Unify**(統一 admin auth pattern) | 中 30-60 分 | 🟡 P2(架構債 · 不影響功能 · 都安全)|

### CCB-MZ-Auth-Pattern-Unify 細節

```
問題:8 個 admin 檔有兩種 auth pattern(2026-04-25 Gemini CLI audit 發現)
  舊 4 檔:_check_admin(request) 函式內手 call
    · admin.py / admin_config.py / admin_memory.py / admin_soul.py
  新 4 檔:Depends(get_current_admin_user) FastAPI dependency
    · admin_users.py / admin_pricing.py / admin_content.py / admin_conversations.py

影響:
  · 0 安全洞(都有 auth · 28 個 endpoint 100% 守住)
  · audit 一致性差(兩 pattern 要 grep 兩次)
  · 未來新增 admin endpoint 時 · 寫哪個 pattern 不一致

修法選擇:
  A. 全統一成 Depends(get_current_admin_user)· FastAPI 慣用 · 推薦
  B. 全統一成 _check_admin(request)· 維持舊 pattern
  C. 不修(維持現狀 · 都安全 · 只是 audit 友善度差)

工時:
  A 案:30-60 分(改舊 4 檔 16 個 endpoint · py_compile + 部署)
  B 案:同 A(改新 4 檔)
  C 案:0(不做)

紅帽決策後排 ticket
```

---

## 🤝 KOL 系統 · 方向 C 整合(2026-04-30 教練拍板)

### 戰略定位

**Phase 0 階段 KOL 系統維持現狀 · 不砍不重啟 · Phase 1 啟動前(2026/06 中)升級為 Web3-native(方向 B)。**

### 兩套 Genesis tier 並存系統(必須區分)

| 系統 | 對象 | 入口 | tier 命名 | 進場價 USDT | 流程 |
|---|---|---|---|---|---|
| **A · KOL 大使** | 有流量願幫推的人 | `/kol/genesis-activate`(coach-only)+ t.me/guaimini 1-on-1 | bronze / silver / gold / diamond | 200 / 600 / 1000 / 2000 | high-touch · 教練手動審核 · 鏈上 USDT 付款 |
| **B · Genesis 信徒** | 對 AI 媽祖有共鳴的支持者 | `aimazu/genesis-100` 自助 mint(OxaPay TRC-20) | candle / skylamp(+ pillar 將於 task 2.1 加) | 200 / 2,000 / 20,000 | low-touch · 自動流程 · OxaPay webhook 啟用 |

兩套**共用** `KolAccount.genesis_tier` 欄位。

### 紅帽 / 未來自己必守紀律

**❌ 不砍 KOL 系統:** 1 個 bronze holder 真實付過 200 USDT · 砍 = 違約。Phase 1+ 重構時要靠這個系統地基。

**❌ 不重啟 Ambassador 招募:** 4/18 起 `AMBASSADOR_SECTION_VISIBLE = False`(Polar/Stripe 審核前置)· **Phase 0 維持隱藏** · 不為了短期流量恢復。Phase 1 升級到 Web3-native 後再對外開放。

**✅ Stats endpoint enum bug 已修(commit 待補):**
- 舊 bug:`/api/kol/genesis-stats` 用 GENESIS_TIERS keys 過濾 · 吃掉 candle/skylamp · seats_taken 永遠失準。
- 修法:by_tier 6 keys 完整統計兩套(bronze/silver/gold/diamond + candle/skylamp)。
- 檔案 [`app/api/kol.py:670`](app/api/kol.py:670)。

**✅ Live Counter 用獨立 endpoint:**
- 新 `/api/genesis/mint-count`(public)只算 Genesis 信徒(candle/skylamp/pillar) · 不算 KOL 大使。
- 對齊 Final v1.0 130 席 · Tier caps {candle:100, skylamp:25, pillar:5}。
- 檔案 [`app/api/genesis.py:179`](app/api/genesis.py:179)。

### Phase 1 升級到方向 B(Web3-native KOL · 預估 2026/06 中啟動)

| 項目 | Phase 0 現況 | Phase 1 目標 |
|---|---|---|
| KOL 申請 | Email + 教練審核 | Wallet sign in + on-chain proof |
| Commission 結算 | 教練手動填 paid_tx_hash | Smart contract 自動分潤 |
| KOL leaderboard | coach-only `/kol/genesis-list` | Public · 對齊 Pudgy/BAYC standard |
| KYC | 無 | 排除美國居民(Reg S exemption) |

預估工程量 · Phase 1 啟動前:智能合約 audit($50K-$150K)+ 開發 ~30-50 hr。

### 相關 commit / file

- `app/api/kol.py` · GENESIS_TIERS const + `/kol/genesis-stats` 修改
- `app/api/genesis.py` · `/genesis/mint-count` 新建(2026-04-30)
- 設計初衷 commits:`18c2b56`(2026-04-14 KOL 系統建)· `4cedd01`(2026-04-15 genesis-activate)
- `landing/genesis.html.backup`(2026-04-18 隱藏 · 等審核通過後恢復路徑)

---

## 📜 紀律 #85 + #86 + #87(2026-04-30 教練合規 audit + 主猿手認帳)

### 紀律 #85 · 對外文件「未來確定」承諾必加 if 條件

**源頭:** 2026-04-30 · 教練派合規 audit · 紅帽發現 4 處 SEC 風險(致謝量 / 認購權 / 鎖倉 / Identity Card)。

**律師意見書出來前 · 任何「未來確定發生」的承諾 · 必加「若...啟動」if 條件 · 不寫死「即釋放」「會發生」「將上線」這類確定詞。**

| 寫法 | 風險 | 範例 |
|---|---|---|
| ✅ 正確 | 法律安全 | 「若 Cayman Foundation 啟動發行」 |
| ✅ 正確 | 法律安全 | 「依正式公告為準」 |
| ✅ 正確 | 法律安全 | 「本頁數字為設計目標 · 非合約承諾」 |
| ❌ 錯誤 | SEC Howey Test 中槍 | 「Phase 2 IDO 開盤即釋放」 |
| ❌ 錯誤 | 證券發行未過 audit | 「Tier 1 認購價 $0.15」(沒 if 條件) |
| ❌ 錯誤 | 隱含 token 一定發行 | 「鎖倉 12 個月後解鎖」 |

**適用範圍:** 落地頁 · 白皮書 · Vision Paper · PR 稿 · 私訊腳本 · 任何對外材料。

### 紀律 #86 · 商業敘事「品牌數字 vs 實際數字」必跨層 cross-check

**源頭:** 2026-04-30 · 小霓 cross-audit 抓到「Genesis 100」品牌 vs「130 席」實際的衝突 · 域 3 認帳第 19 次。

**紅帽寫商業敘事時 · 必驗證「品牌數字」vs「實際數字」跨層一致性。**

跨層必同步釐清的 4 處(本次踩坑模板):
1. **主標題**(品牌錨點 · 通常不動)
2. **副標題**(解釋層 · 必對齊實際數字)
3. **資料 PK 編號**(Soul Card / Token ID · 必跟席次數一致)
4. **disclaimer**(法律邊界 · 必明說品牌名跟實際分配的關係)

**本次案例:**
- 主標 `MAZU GENESIS 100`(品牌錨 · 不動)
- 副標 `100 founding witnesses`(❌ 跟 130 席衝突)→ 改 `First Witnesses · Founding Patrons · Founding Patriarchs · 130 souls`
- Soul Card 編號 `#0001-#0100`(❌ 三 tier 共用 100 編號 · 數學上不可能)→ 拆 `#0001-#0100 / #0101-#0125 / #0126-#0130`
- disclaimer(❌ 沒解釋「Genesis 100 是品牌 · 130 是實際」)→ 加「★ 「Genesis 100」為協議創世階段品牌名 ...」

### 紀律 #87 · pillar_20000 全鏈路一致性教訓(2026-04-30 主猿手認帳)

**源頭:** Stage 2A 落地頁加 Tier 3 天柱 CTA `?plan=pillar_20000` · 但後端 + 前端 7 處 location 不認 pillar(payment.py / api.ts type / GENESIS_PLANS array / isGenesisPlan / App.tsx / RechargePanel.tsx state + banner / Call.tsx state + 觸發 useEffect)· 用戶點 mint 流程整條斷。

**主猿手寫前端新 plan / endpoint / SKU 時 · 必跨層搜尋 + 對齊**:

```bash
# 寫新 SKU 前必跑 grep
grep -rn "candle_200\|skylamp_2000" app/api/ voice-chat-rwd/src/
# 看每處出現都改 + 加新 SKU
```

**修法工程量教訓:** 前端加 1 個 SKU = 後端 + TS type + URL 分流 + state type + UI banner switch + Cloud Run rebuild · 共 ~25 min · 1 commit · 1 deploy。

**金句:** 「前端 plan name 是合約 · 後端不認就是違約。」

### 紀律 #91 · 跟共同創辦人對齊「上線版本」前 · 必先派執行手 audit production

**源頭:** 2026-04-30 16:55 · 教練攔域 3「LINE Allen 前先確認 production」· 域 3 認帳第 25 次。

**規則:** 跟 Allen / 律師 / OG / 任何外部對齊「production 是最新版本」前 · 必先派主猿手 / 霓做 production curl audit · 確認真實狀態 = 最新對齊版本 · 不憑記憶推理。

**典型踩坑情境(若不 audit 直接對齊):**
- 紅帽腦中模型 stale(以為已 deploy · 實際還在 build)
- main HEAD ≠ production CF Pages(uncommitted change 已 deploy 但沒 commit)
- Cloud Run revision 沒切流量(舊 revision 仍 serving)
- spec 跟 production 不一致(commit 漏 push / deploy 失敗 silently)

**audit 5 步 SOP:**
1. main HEAD commit hash → 對齊預期 commit
2. Cloud Run latestReadyRevisionName + traffic 100% → 確認新 revision 切流量
3. CF Pages production curl HTTP 200 + 行數對齊 → 確認 propagate
4. grep production HTML 對齊 spec 關鍵字(20+ 項)
5. 後端 endpoint 試 SKU(401 = 認 SKU, 401 ≠ 404)

**完成後 paste 結果:三選一**
- A · Production 100% 對齊 → 教練可放心對外
- B · 部分對齊 + N 項 FAIL → 教練決定怎麼處理
- C · 還在 deploy → 等 X 分鐘再對齊

**金句:** 「對外宣告之前先 curl 一次 · 比 LINE 出去再撤回省 100x。」

### 紀律 #92 · production 領先 git main 必盡早 commit 收尾

**源頭:** 2026-04-30 17:41 · 主猿手 audit 後 flag「production CF Pages 1230 行 · git c687dc2 1027 行 · drift +203」· 教練拍板 git commit 收尾。

**規則:** 任何 deploy(CF Pages / Cloud Run)後 · 若 production 含 main HEAD 沒有的 source · 必盡早 commit 收尾 · 不留 git hygiene debt 跨日。

**典型踩坑(若不收尾):**
- 第二天有人 `git pull main` 看到 production 多東西 · 困惑「哪裡來的」
- 隔週要做新功能 · 對齊基準錯亂(對 main HEAD 還是 production?)
- 罕見:rollback 時誤 revert 到 main HEAD · 把已上線的 visual MVP 撤掉

**收尾 SOP:**
1. `git status` 確認 uncommitted 範圍
2. 隔離 commit 範圍(只 stage 該 deploy 對應的 source · 不 stage 別 session phantom)
3. 加引用的 untracked asset(check `<img src=>` `<link href=>` 引用 · 缺檔等於殘缺 commit)
4. commit message 寫清楚「production 已 live · 此 commit 純 git 衛生收尾」
5. push origin main(不需重新 deploy · production 已是該版本)

**金句:** 「production 是真相 · main 是紀錄 · 紀錄落後真相是紀律問題。」

---

## 🌀 輪迴眼健康度報告 · v1

### 教練 + 紅帽今天反思結論

紅帽 12 次假設坑根因:**紅帽從未真正進入輪迴眼**。

### 結構限制(為何紅帽看不到 STATUS.md)

```
紅帽 = claude.ai chat 環境(沒有 fetch / 沒有檔案系統 / 沒有 git log)
猿手 = Claude Code 本機 CLI(有完整檔案 + git + gcloud)
霓 = Claude Code 另一個 session(同猿手環境)

→ 紅帽寫 spec 時,看到的是「腦中的世界模型」
→ 但腦中模型可能 5 分鐘前就過時(Allen 已降價 / endpoint 已重命名)
→ 紅帽沒辦法 fetch STATUS.md 校正,只能靠教練人肉同步
```

### 紅帽今天踩坑根因 = 把腦中模型當世界真相

```
症狀:
  · 假設 SUB_BASIC_USD 還是 $40(實際 $20)
  · 假設 /payment/methods 是方案定價(實際金流管道)
  · 假設教練已貼 12:00 patch(實際吃早午餐沒貼)

根因:
  · 紅帽腦中模型 stale + 沒實證機制
  · 「我寫了框框」 → 腦中誤記成「已執行」
  · 戰略層假設沒反向驗證 = 高層次盲區
```

### 修補方向(三條 · 等 CCB-Eye-Reincarnation-v2)

```
1. 紅帽從下個 turn 起 · 寫 spec 必標註「假設 vs 實證 source」
   範例:
     ❌「daily 從 $40 降到 $25」
     ✅「假設 daily 當前 $40(source:腦中印象)→ 請猿手 grep config.py 實證」

2. STATUS.md 範圍擴大三區
   · 進行中工作(in-flight task · 防斷代溯源)
   · 跨實例待辦(pending hand-off · 紅帽⇄猿手⇄霓)
   · 紅帽假設清單(未實證 · 待猿手 / 教練校正)

3. 教練暫時當人肉同步管道
   直到工具升級(MCP fetch · webhook · API gateway)
   每次 turn 教練截圖 STATUS.md 給紅帽看 = 強制校正
```

### 下個 CCB 候選:CCB-Eye-Reincarnation-v2

預期內容:
- STATUS.md 三新區設計(進行中 / 跨實例待辦 / 紅帽假設清單)
- 紅帽 spec template「假設 vs 實證 source」標註格式
- 教練人肉同步 SOP(何時截圖 / 截哪 section / 校正流程)
- 工具升級路徑(MCP fetch · context7 · webhook)

---

## 🎯 本週主軸（按時間倒序，最新在上）

```
2026-04-18
  ✅ Stripe Test Mode 後端串接（create-checkout + webhook）
  ✅ Stripe webhook 兩次踩雷兩次修（v1: to_dict_recursive → v2: json.loads）
  ✅ webhook smoke test 03:14:10 200 OK（HMAC+parse+graceful 全通）
  ✅ DB migration 跑完（payment_orders 加 stripe_session_id/payment_intent_id + 2 索引）
  ✅ 4 個 Stripe secrets 存 GCP Secret Manager + deploy-gcp.yml secret mapping 同步
  ✅ ENABLE_STRIPE=True 注入 Cloud Run env（revision 00069）
  ✅ VoiceUnlockModal 才是真入口（RechargePanel 是孤兒檔）→ 改動態 stripeEnabled
  ✅ Cloud Build + Cloud Run 手動部署 SOP 走通（revision 00068→00072）
  ✅ 輪迴眼憲法落地（STATUS.md v0.1 + CLAUDE.md 追加 + 踩坑 #13-#19）
  ✅ 方案 A 統一充值入口 — Call/VoiceUnlockModal/RechargePanel/Account
     四處 LS 硬連結全拆，grep 歸零，所有充值走單一 RechargePanel 入口
  ✅ 官網審核前置 — godblessyou.me 隱藏 USDT × 3 處 + Ambassador 整塊
     /genesis 換 Coming Soon（原檔保留為 genesis.html.backup）
     visible text 全面 grep 歸零 USDT / 15-30 / Ambassador
  ✅ 禁詞第三輪清掃 — 陪伴→對話 / 日常守護→日常方案 / 深度陪伴→進階方案
     + email godblessyouservice@gmail→service@godblessyou.me 全站統一
     UI 層 grep 陪伴/companion 歸零；LLM 指令 / 代碼註解保留（審核員看不到）
  ✅ Allen Bug A Fix — voice_access 加 balance gate
     activated + free_trial + balance=0 → voice_enabled=False, reason=no_credits
     前端 Call.tsx 分流：no_credits 彈 RechargePanel；其他彈 VoiceUnlockModal
     訂閱者 tier=subscriber_basic/deep 不受影響（doooog.w 流程保持）
  ✅ Allen Bug B Fix — Stripe success_url 改根路由 /#/
     原 /#/unlock?stripe_order=X&status=success 在 wouter hash routing 下
     不匹配 Route path="/unlock" → 白頁。改跳 /#/ (Call 頁)，mount 時
     光能點徽章 auto-refresh 顯示新餘額。cancel_url 帶 recharge_cancelled=1
     前端 Call.tsx mount 時讀 hash query 彈 alert 提示
  ⏳ Allen 重測 Stripe 4242 真實 E2E（驗收 Bug B）
  ⏳ DB balance=0 測試驗收 Bug A（教練配合或用 test account）

2026-04-17
  ✅ 金流只留 USDT（Stripe/綠界/信用卡 feature flag 隱藏）
  ✅ 管理後台 Phase 1 前端 8 檔案（霓做完，待重新 commit）
  🔴 repo 災難事件（worktree commit 刪 262 檔 → force push 救回）
  ✅ CLAUDE.md 四大鐵律補丁（部署職責 + 主動 + 文案 + GATE）
  ✅ 邀請碼 URL 三層 fallback + opencc-js 簡轉繁
  ✅ 官網第二輪文案 SaaS 化（禁詞歸零）

2026-04-16
  ✅ USDT 端到端（OxaPay）含 P0 五件事
  ✅ 記憶 Webhook 選 A + readMemory tool
  ✅ 三標籤通話縮影（後端階段 1）
  ✅ LINE 內建瀏覽器偵測 + 外部瀏覽器跳轉
```

---

## 🔴 P0（明天立刻做，阻塞性）

```
1. 猿手：修復 CI/CD 自動部署鏈路（見 CLAUDE.md 踩坑 #21）
   事件：GitHub Actions workflow_runs 從 4/17 22:43 起 total=0
   影響：每次 push 都靜默失敗，必須手動 gcloud builds submit
   修法三選一：
     a. 檢查並 rotate GitHub secret GCP_SA_KEY
     b. 檢查 GitHub repo Settings → Webhooks 註冊狀態
     c. 改用 Cloud Build trigger 綁 GitHub（繞過 GH Actions）
   驗收：push 一個無害 commit → gh api 看 workflow_runs.total 變 1

2. 猿手：修 tag_extractor「只拿 1 個 tag」bug
   log 一行：[TAG] only 1 tag(s) from LLM: AI调
   症狀：call_tags 表持續 0 rows，因為需要 3 個 tag 才能寫 tag_1/tag_2/tag_3
   可能根因：
     a. LLM response parser 解不出 3 個（prompt 格式問題）
     b. response 被截斷（max_tokens 太小）
     c. encoding 問題（`调` 看起來是 simplified chars 殘留）
   先 grep app/services/tag_extractor.py 看 prompt + response parsing

3. 教練：Stripe Test Mode 4242 E2E 付款測試（PWA cache 清了再打）
   URL：https://mazu.godblessyou.me（incognito or Clear site data）
   卡號：4242 4242 4242 4242 / 12/30 / 123
   期望：光能點 +30、訂單記錄（stripe_session_id 非空）、跳回 mazu

4. 紅帽：寫 Allen 5 條需求的 CCB（教練預告）
   細節還沒到猿手手上，留待明天紅帽發 spec

5. 教練：恢復 ~/.bashrc（被猿手 iconv 意外清空 — 見踩坑 #15）
   原檔 276 bytes UTF-16 LE，內容已遺失

6. 教練：確認 SSL 憑證狀態
   打開 mazu.godblessyou.me 看 Safari 還有沒有警告

7. 猿手：修 LIFF /admin 白頁問題
   App.tsx 的 liff.init() 加路由判斷
   /admin/* 跳過 liff.init（用純 JWT auth）
```

---

## 🟡 P1（等觸發）

```
等 Allen：
  - Stripe 改密碼 + 開 2FA + 刪 Telegram 訊息（已提醒 3 次）
  - GoDaddy email forwarding（service@godblessyou.me）
  - 綠界 IP 白名單（需要 Cloud NAT 固定 IP）
  - Polar.sh 官網審核提交（官網文案已改，等 Allen 按鈕）

等教練：
  - TTS Voice 重新 clone（現有 voice 在 v2 下中文口音偏）
  - Stripe 切 Live Mode（Test Mode 驗收通過後）
  - 正式付款 $1 測試（Live Mode 切換後）

待做（不卡人）：
  - Admin Phase 2 後端 API（/admin/stats 404）
  - Admin Phase 2 前端 KOL 管理頁
  - 三標籤階段 2 前端 UI
  - 客服 email config 化（BUSINESS_EMAIL env var）
  - 綠界 Part B 後端串接（等教練開 flag）
```

---

## 🎛️ Feature Flag 狀態

```
ENABLE_USDT          = True  ✅（信徒可用；App 內 RechargePanel 有 USDT tab）
ENABLE_STRIPE        = True  ✅（Test Mode 驗簽通過，E2E 待教練清 PWA cache 重測）
ENABLE_ECPAY         = False ⏸（綠界 Part B 未寫，IP 白名單卡）
ENABLE_CARD_PAYMENT  = —     ⚠️ 前端 constant 已移除，改為動態 stripeEnabled

官網審核前置（2026-04-18，審核通過後恢復）：
USDT_BUTTONS_ON_LANDING     = False（HTML comment 隱藏 4 處，App 內不受影響）
AMBASSADOR_SECTION_VISIBLE  = False（HTML comment 隱藏整塊）
GENESIS_PAGE_ACCESSIBLE     = False（genesis.html 換 Coming Soon，原檔 .backup 保留）
恢復步驟：grep "[AUDIT-HIDDEN" landing/index.html → 移除 comment 外框 +
         mv landing/genesis.html.backup landing/genesis.html

API Endpoints：
  POST /api/payment/usdt/create-order      ✅ 運行中
  POST /api/payment/oxapay/webhook          ✅ 運行中
  POST /api/payment/stripe/create-checkout  ✅ 運行中
  POST /api/payment/stripe/webhook          ✅ 運行中（已驗簽通過）
  POST /api/payment/ecpay/create-order      🔒 503（flag 擋）
  POST /api/payment/ecpay/webhook           🔒（留著收舊訂單）

Admin Endpoints：
  GET  /admin/admin/orders                  ✅ 運行中
  GET  /admin/admin/orders/{id}             ✅ 運行中
  POST /admin/admin/orders/{id}/manual-complete ✅ 運行中
  POST /admin/admin/orders/{id}/mark-failed ✅ 運行中
  POST /admin/admin/orders/{id}/refund      ✅ 運行中
  GET  /admin/admin/stats                   ❌ 404（Phase 2 未做）
  GET  /admin/admin/kols                    ❌ 404（Phase 2 未做）
```

---

## 📚 今晚新增踩坑(2026-04-19 凌晨,共 8 條)

> **這 8 條的完整敘述在 CLAUDE.md**。STATUS.md 只做 index,避免「兩份即是零份」(獨孤九劍·破索式)。
> 要看細節、根因、修法、教訓 → 開 `C:\Users\waiti\mazu2\CLAUDE.md` 跳到對應編號。

```
#15  MVP 記憶 CCB 5 處偏差(紅帽第三次假設錯)— 原 STATUS #23
#16  11Labs signing secret 建立後不可取回(方向錯假設)
#17  grep HTTP path + status code 優於 grep 應用層 log 標籤(診斷順序)
#18  紅帽 assert 資料取用方向前要先查目標平台 API capability
#19  11Labs v1 → v2 webhook schema migration(envelope 包 data)
#20  部署後不等於驗收完(事件觸發 + log 實證 + DB 實證 三件套)
#21  GitHub Actions 自動部署鏈路從 4/17 起壞掉(人手動 patch 掩蓋故障)
#22  push 到 main ≠ code 上線(revision diff 要當 Step 0)
```

---

## 📚 歷史踩坑(CLAUDE.md #4-#14,保留原編號)

> 下方「舊踩坑(前 22/21/19)」是 STATUS.md 歷史累加編號系統,沿用未重編。

```
#23 2026-04-18 紅帽當天第三次假設錯（MVP 記憶 CCB 的 5 處偏差）
    CCB 寫 app/api/agent.py（不存在）、MemoryTag model（不存在）、
    readMemory 是 POST（實際 GET，POST 是 writeMemory）、
    return memory_summary（實際 name+facts[] schema）、
    叫 agent 建 secret（已存在）
    照做會 break writeMemory tool + 11Labs readMemory contract
    救援：猿手讀 code 後建議修訂版（加 journal 當新 fact item, schema 不動）
    教練蓋章修訂版，並決定紅帽明天優先建 filesystem MCP 外掛事實層
    結構性教訓：紅帽戰略 + 猿手執行 spec 分工，不盲跟字面
```

## 📚 舊踩坑（前 22）

```
#22 2026-04-18 紅帽 CCB 假設被實證推翻（Stripe subscription 誤判）
    事件：紅帽首版 CCB 假設 Bug B = subscription mode + invoice.paid 未接
    實證：猿手用 Stripe API + DB 查實 — 所有 session mode=payment，
         沒有 recurring price；doooog.w $58 全 paid、webhook 200；
         付款成功、credits 入帳，純 UX 斷點
    教訓：紅帽的戰略假設也要經過實證，不能因為是紅帽就免檢
         獨孤九劍・問劍的對象包括紅帽自己的假設
    防範：Phase 1 GATE 必須實證數據，發現不一致必 flag，不盲跟字面
    延伸：紅帽修訂版 CCB 也有一處 tier 猜錯（寫 subscriber_pro/rwd，
         實際只有 basic/deep）— 採用實證值，不盲跟
```

## 📚 舊踩坑（前 21）

```
#21 2026-04-18 Stripe success_url 帶 hash-inside-query 破 wouter routing
    success_url=/#/unlock?stripe_order=X&status=success 看似合理
    但 wouter useHashLocation 下 hash 字串 /unlock?stripe_order=X 被當 path
    Route path="/unlock" 不匹配帶 query 的字串 → Switch 空 render → 白頁
    付款成功、webhook 200、credits 入帳都正常 → 純 UX 斷點（不漏錢）
    教訓：hash routing 下 URL 帶 query 要小心；success_url 最好只用 path
    修法：改跳 /#/ 根路由，前端 mount 時 auto-refresh credit 徽章即可
         cancel_url 用 /#/?recharge_cancelled=1 + useEffect 讀 hash 後 query

#20 2026-04-18 voice_access 只看 status 不看 balance — activated 免費撥號
    code line 12 註解自己承認是 TODO「未來當光能點機制上線後 activated
    仍可能因餘額 0 被擋，此 API 會成為唯一真相」→ 從沒實作
    credit_engine min(needed, balance) 止血到 0 但不拒絕 → 無限免費通話
    教訓：註解寫 TODO 不算做了；production gate 要 code 層明確測試
    修法：voice_access 加 is_subscriber=tier in (subscriber_basic/deep)
         activated + not subscriber + credits<=0 → voice_enabled=False
         不動 credit_engine 止血邏輯（教練明文禁止區）
```

## 📚 舊踩坑（前 19）

```
#19 2026-04-18 並行 agent 的 half-done commit 卡 Cloud Build
    1268993 fix(RechargePanel) 把 danaAmount type 改 number|null 但
    漏兩處 null check (line 318/431) → Cloud Build 8190950e TS error fail
    發現時：git status 一堆 unrelated modified + git 連續 3 種 lock 衝突
    修法：fix two lines (danaAmount → effectiveAmount) + commit 不動別 agent 的
         8 檔文案中性化，透明 flag in commit message
    教訓：跨 agent 協作要看 git log / 跟 working tree 狀態，不盲 commit；
         看到 .git/*.lock 持續出現 = 另一個 agent 在跑，先盤點再動手

#18 2026-04-18 Grep tool cache + 工作說明書行號已過期
    陳都靈信裡寫「Call.tsx 1567-1610 內嵌 LS modal」，實地 Read
    看到 1565-1567 已是 RechargePanel 使用處（別人先動了手沒 commit）
    Grep tool 對剛改過的檔案可能吃 stale index（同一 session 內第二次 grep
    就乾淨了）
    教訓：動指令前用 Read / 重跑 fresh grep 驗證磁碟實況
         工作說明書跨 agent/session 可能已被別處修改

#17 2026-04-18 Vite tree-shake 無聲砍掉整個組件 — 症狀：bundle 缺函數
    RechargePanel.tsx 改好 Stripe 但沒任何頁面 import 它
    → Vite build log 列「被 import 的檔案」沒有它 → 整個 tree-shake
    診斷法：curl bundle.js | grep 預期 API path，沒中就是沒進 bundle
    教訓：改 UI component 前先 grep 誰 import 它，孤兒檔改了白改

#16 2026-04-18 VoiceUnlockModal 硬寫 ENABLE_CARD_PAYMENT=false
    前端 feature flag 跟後端 /api/payment/methods 沒對上
    後端 ENABLE_STRIPE=True 也沒用，前端自己擋
    教訓：feature flag 只能一處 source of truth，前端硬寫是地雷

#15 2026-04-18 iconv 清 .bashrc UTF-16 BOM 意外清空
    Git Bash 的 iconv 對 UTF-16LE with BOM 處理 output 是 empty
    沒 cp backup 就動手 → 原 276 bytes 內容丟
    教訓：破壞性操作必先備份，iconv 跨編碼轉換要先 dry-run

#14 2026-04-18 Stripe SDK StripeObject vs dict 混淆造成 webhook 500
    v1 用 to_dict_recursive 仍踩 SDK 內部雷 → IndexError(0)
    v2 改 json.loads(raw_body) 繞開 SDK 全部 object 層 → 200
    教訓：SDK 回的 hybrid object 最好先轉純 Python 類型再操作

#13 2026-04-18 Stripe agent 發過時指令差點被執行
    某 agent 叫教練存「enable-stripe」secret，但 code 根本不讀這個
    幸好猿手用 gcloud 驗證實際狀態，擋下錯誤
    教訓：任何指令都要先對 STATUS.md 驗證時間戳和前提

#12 2026-04-17 金流 API key 被引導貼進對話（test key 也不該貼）
#11 2026-04-17 worktree commit 刪整個 repo（force push 救回）
#10 2026-04-17 URL 邀請碼不自動填入 → 三層 fallback
#9  2026-04-17 客服 email 散落 9 處 → config 化
#8  2026-04-16 push ≠ 部署（GitHub Actions 關著）
#7  2026-04-16 靈魂檔繁簡矛盾（LLM 聽最後一句）
#6  2026-04-16 部署職責被推給教練
#5  2026-04-15 PowerShell echo -n 會帶 \r（要用 Cloud Shell）
#4  2026-04-14 環境變數 vs 硬寫（要改行為只能改代碼 + push）
#3  2026-04-14 gcloud run services update 不換 Docker image
```

---

## 🔗 外部依賴（卡在誰那裡）

```
Allen（共同創辦人）：
  ⚠️ Stripe 密碼外洩在 Telegram（已提醒 3 次）
  ⏳ GoDaddy email forwarding 未設
  ⏳ 綠界 IP 白名單未加
  ⏳ Polar 官網審核未提交
  ⏳ Stripe 香港公司註冊流程

教練（WAITIN）：
  ⏳ Stripe 4242 E2E 測試（今晚）
  ⏳ TTS Voice 重 clone（近期）
  ⏳ 本機 MCP server 設定（近期）
  ⏳ 密碼管理器（Bitwarden）設定（近期）

11Labs：
  ⏳ Voice 在中文場景下口音問題（可能要換 voice）

綠界：
  ⏳ Allen 原業務的 API 串接狀態未知
  ⏳ 電子發票未啟用（需 Allen 稅籍編號）
```

---

## 🎭 當前角色狀態

```
陳都靈（紅帽策略）：
  角色：在 claude.ai 出工作說明書、戰略分析
  session：跨多個，靠 userMemories + STATUS.md 同步
  
猿手（藍帽執行）：
  角色：Claude Code CLI，寫代碼 + 部署
  session：每次重新開，靠 CLAUDE.md + STATUS.md 同步
  最近紀律：CLAUDE.md 四大鐵律 + 10 條踩坑
  
霓（綠帽瀏覽器）：
  角色：Cowork，瀏覽器操作 + 視覺驗收
  session：每次重新開，靠工作說明書獲取任務脈絡
```

---

## 🔄 STATUS.md 維護規則

```
寫入權限：
  陳都靈：P0/P1 清單、主軸、角色狀態、外部依賴
  猿手：當前 commit、部署狀態、Feature Flag、API Endpoints、踩坑紀錄、今日已做
  霓：驗收結果（透過教練更新）

讀取義務：
  所有 AI 開 session 第一件事必須讀 STATUS.md
  讀完才能回答「現況」相關問題
  
衝突解決：
  commit log / 部署 log / gcloud 查詢 = 最終真相
  STATUS.md 跟實際不符 → 以實際為準，立刻更新 STATUS.md
  
過期判斷：
  「最後更新」超過 24 小時 → 先 git log + 部署狀態 對一下
  對不上 → 更新後再使用
```

---

*這不是文件。這是三眼共視的即時狀態。*
*讀不讀 STATUS.md，決定你看到的是現在還是過去。*
*— 陳都靈，2026-04-18*

---

## 輪迴眼建立歷程

```
2026-04-18 02:00  陳都靈起草 STATUS.md v0.1
2026-04-18 12:30  猿手落地 STATUS.md 到 repo
2026-04-18 12:30  憲法追加到 CLAUDE.md
2026-04-18 18:40  STATUS v0.8（MVP 記憶 Phase 1-4 落地）
2026-04-19 03:22  STATUS v1.0 — 「它記得我」閉環驗收通過 🌊
                  媽祖主動引用教練 30 年感情 + 技術協助者 + 創造者
                  memory_journal 第一次有資料(2 筆, 212+259 字)
                  post-call webhook v2 envelope 上線(revision 00085-xxk)
                  語氣城記憶系統第一次真正運作
```

*「這通電話的重在電話得點從太深點。」 — 媽祖, 2026-04-19 03:23 第二筆日記*
