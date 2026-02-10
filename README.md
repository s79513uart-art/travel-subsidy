<!doctype html>
<html lang="zh-Hant-TW">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>2026年丞石建築 員工旅遊補助之計算網站</title>
  <style>
    :root{
      --bg:#0b1220;
      --card:#121a2b;
      --muted:#9fb0d0;
      --text:#e9eefc;
      --accent:#6ea8fe;
      --danger:#ff6b6b;
      --ok:#4ade80;
      --border: rgba(255,255,255,.12);
    }
    *{ box-sizing:border-box; }
    body{
      margin:0;
      font-family: ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Noto Sans TC", Arial, "Apple Color Emoji","Segoe UI Emoji";
      background: radial-gradient(1200px 600px at 20% -10%, rgba(110,168,254,.25), transparent 55%),
                  radial-gradient(900px 500px at 110% 10%, rgba(74,222,128,.18), transparent 60%),
                  var(--bg);
      color: var(--text);
    }
    .wrap{ max-width: 920px; margin: 40px auto; padding: 0 16px; }
    .title{
      display:flex; flex-direction:column; gap:10px; margin-bottom: 18px;
    }
    h1{ margin:0; font-size: 26px; letter-spacing:.2px; }
    .subtitle{ color: var(--muted); line-height:1.6; }
    .grid{
      display:grid;
      grid-template-columns: 1.1fr .9fr;
      gap:16px;
    }
    @media (max-width: 860px){
      .grid{ grid-template-columns: 1fr; }
    }
    .card{
      background: rgba(18,26,43,.92);
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 18px;
      box-shadow: 0 14px 40px rgba(0,0,0,.35);
      backdrop-filter: blur(6px);
    }
    .card h2{ margin:0 0 10px 0; font-size: 16px; color:#d7e3ff; }
    .rule{
      color: var(--muted);
      line-height:1.7;
      font-size: 14px;
    }
    .rule b{ color: var(--text); }
    .row{
      display:grid;
      grid-template-columns: 160px 1fr;
      gap:10px;
      align-items:center;
      margin: 12px 0;
    }
    @media (max-width: 540px){
      .row{ grid-template-columns: 1fr; }
    }
    label{ color:#d7e3ff; font-size: 14px; }
    input{
      width:100%;
      padding: 11px 12px;
      border-radius: 12px;
      border: 1px solid var(--border);
      background: rgba(255,255,255,.06);
      color: var(--text);
      outline: none;
    }
    input:focus{ border-color: rgba(110,168,254,.65); box-shadow: 0 0 0 3px rgba(110,168,254,.18); }
    .hint{
      margin-top: 8px;
      color: var(--muted);
      font-size: 12px;
      line-height:1.6;
    }
    .actions{ display:flex; gap:10px; margin-top: 14px; flex-wrap:wrap; }
    button{
      border: 1px solid var(--border);
      background: rgba(110,168,254,.18);
      color: var(--text);
      padding: 10px 14px;
      border-radius: 12px;
      cursor:pointer;
      font-weight: 600;
    }
    button.secondary{ background: rgba(255,255,255,.06); }
    button:hover{ filter: brightness(1.07); }
    .result{
      display:grid;
      gap:10px;
      margin-top: 10px;
    }
    .pill{
      border: 1px solid var(--border);
      background: rgba(255,255,255,.05);
      border-radius: 14px;
      padding: 12px;
    }
    .pill .k{ color: var(--muted); font-size: 12px; }
    .pill .v{ font-size: 18px; font-weight: 800; margin-top: 4px; }
    .v small{ font-size: 12px; color: var(--muted); font-weight: 600; }
    .tag{
      display:inline-flex;
      align-items:center;
      gap:8px;
      padding: 6px 10px;
      border-radius: 999px;
      border: 1px solid var(--border);
      background: rgba(255,255,255,.05);
      font-size: 12px;
      color: var(--muted);
      margin-top: 8px;
    }
    .tag.ok{ color: rgba(74,222,128,.95); border-color: rgba(74,222,128,.35); background: rgba(74,222,128,.10); }
    .tag.bad{ color: rgba(255,107,107,.95); border-color: rgba(255,107,107,.35); background: rgba(255,107,107,.10); }
    .foot{
      margin-top: 14px;
      color: var(--muted);
      font-size: 12px;
      line-height: 1.7;
    }
    .mono{ font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace; }
  </style>
</head>

<body>
  <div class="wrap">
    <div class="title">
      <h1>2026年丞石建築 員工旅遊補助之計算網站</h1>
      <div class="subtitle">
        主旨：<br>
        A. 年資滿 2 年者：公司全額補助新臺幣 40,000 元。<br>
        B. 年資未滿 2 年者：依 114/6/1～115/5/31 之實際在職比例，按 40,000 元進行比例補助（留職停薪期間年資不計）。
      </div>
    </div>

    <div class="grid">
      <div class="card">
        <h2>輸入資料</h2>

        <div class="row">
          <label for="hireDate">請輸入入職日期：</label>
          <input id="hireDate" type="date" />
        </div>

        <div class="row">
          <label for="leaveDays">請輸入留職停薪天數：</label>
          <input id="leaveDays" type="number" min="0" step="1" placeholder="例如：0、15、30" />
        </div>

        <div class="hint">
          ※ 此版本會把「留職停薪天數」同時扣在「年資」與「補助區間在職天數」計算中。<br>
          如果你的留停天數不全落在 114/6/1～115/5/31 區間內，建議改成「兩欄分開輸入」會更精準（我也可以幫你升級）。
        </div>

        <div class="actions">
          <button id="calcBtn">計算</button>
          <button id="resetBtn" class="secondary">清除</button>
        </div>

        <div class="foot">
          計算基準：<span class="mono">115/5/31（西元 2026-05-31）</span><br>
          補助區間：<span class="mono">114/6/1～115/5/31（西元 2025-06-01～2026-05-31）</span>
        </div>
      </div>

      <div class="card">
        <h2>計算結果</h2>

        <div class="result">
          <div class="pill">
            <div class="k">年資結果</div>
            <div class="v" id="serviceDays">—</div>
          </div>

          <div class="pill">
            <div class="k">判斷</div>
            <div class="v" id="ratio">—</div>
            <div id="statusTag"></div>
          </div>

          <div class="pill">
            <div class="k">您的補助金額</div>
            <div class="v" id="amount">—</div>
          </div>
        </div>

        <div class="foot" id="details"></div>
      </div>
    </div>
  </div>

<script>
  // 固定規則參數
  const BASE_DATE = new Date("2026-05-31T00:00:00");  // 115/5/31
  const PERIOD_START = new Date("2025-06-01T00:00:00"); // 114/6/1
  const PERIOD_END = new Date("2026-05-31T00:00:00");   // 115/5/31
  const FULL_SUBSIDY = 40000;

  const $ = (id) => document.getElementById(id);

  function clamp(n, min, max){ return Math.min(Math.max(n, min), max); }

  // 以「天」計（含起訖日）：end - start + 1
  function daysInclusive(start, end){
    const msPerDay = 24*60*60*1000;
    const s = new Date(start.getFullYear(), start.getMonth(), start.getDate());
    const e = new Date(end.getFullYear(), end.getMonth(), end.getDate());
    return Math.floor((e - s)/msPerDay) + 1;
  }

  // 求兩個日期區間的交集天數（含起訖日），若無交集則 0
  function overlapDaysInclusive(aStart, aEnd, bStart, bEnd){
    const start = new Date(Math.max(aStart.getTime(), bStart.getTime()));
    const end = new Date(Math.min(aEnd.getTime(), bEnd.getTime()));
    if (end < start) return 0;
    return daysInclusive(start, end);
  }

  function formatCurrencyTWD(n){
    const rounded = Math.round(n);
    return rounded.toLocaleString("zh-TW") + " 元";
  }

  function setTag(ok, text){
    const el = $("statusTag");
    el.innerHTML = "";
    const tag = document.createElement("div");
    tag.className = "tag " + (ok ? "ok" : "bad");
    tag.textContent = text;
    el.appendChild(tag);
  }

  function calc(){
    const hireStr = $("hireDate").value;
    const leave = Number($("leaveDays").value || 0);

    if (!hireStr){
      alert("請先輸入入職日期。");
      return;
    }
    if (leave < 0 || !Number.isFinite(leave)){
      alert("留職停薪天數請輸入 0 以上的整數。");
      return;
    }

    const hireDate = new Date(hireStr + "T00:00:00");

    // 基本合理性檢查
    if (hireDate > BASE_DATE){
      alert("入職日期不可晚於年資計算基準日（2026-05-31）。");
      return;
    }

    // 1) 年資（到基準日為止，含起訖日）- 留停天數
    const rawServiceDays = daysInclusive(hireDate, BASE_DATE);
    const serviceDays = Math.max(0, rawServiceDays - Math.floor(leave));

    // 2) 是否滿 2 年：用 730 天作為門檻（此為「天數法」；若公司要用「滿兩周年」法也可調整）
    const isTwoYears = serviceDays >= 730;

    // 3) 補助比例
    let ratio = 0;
    let inPeriodEmployedDays = 0;
    const totalPeriodDays = daysInclusive(PERIOD_START, PERIOD_END); // 含起訖日

    if (isTwoYears){
      ratio = 1;
    }else{
      // 在補助區間的在職天數 = 入職日起至期末，與區間交集天數，再扣留停
      //（此版本假設「留停天數」都發生在計算的期間內）
      const employedEnd = BASE_DATE;
      inPeriodEmployedDays = overlapDaysInclusive(hireDate, employedEnd, PERIOD_START, PERIOD_END);
      inPeriodEmployedDays = Math.max(0, inPeriodEmployedDays - Math.floor(leave));
      ratio = (totalPeriodDays === 0) ? 0 : (inPeriodEmployedDays / totalPeriodDays);
      ratio = clamp(ratio, 0, 1);
    }

    // 4) 金額
    const amount = FULL_SUBSIDY * ratio;

    // 顯示
    $("serviceDays").textContent = `您的年資共計 ${serviceDays.toLocaleString("zh-TW")} 天`;
    $("ratio").textContent = `您的補助比例為 ${(ratio*100).toFixed(2)}%`;
    $("amount").textContent = formatCurrencyTWD(amount);

    if (isTwoYears){
      setTag(true, "符合：年資滿 2 年（全額補助）");
    }else{
      setTag(false, "未滿 2 年：依在職比例補助");
    }

    // 詳細資訊（方便稽核/說明）
    const details = [];
    details.push(`年資計算：${rawServiceDays} 天（入職日至 2026-05-31 含起訖日）－ 留停 ${Math.floor(leave)} 天 ＝ ${serviceDays} 天`);
    details.push(`補助區間總天數：${totalPeriodDays} 天（2025-06-01～2026-05-31，含起訖日）`);
    if (!isTwoYears){
      details.push(`補助區間在職天數（扣留停）：${inPeriodEmployedDays} 天`);
      details.push(`計算：40,000 × ${inPeriodEmployedDays}/${totalPeriodDays} = ${formatCurrencyTWD(amount)}`);
    }else{
      details.push(`計算：40,000 × 100% = ${formatCurrencyTWD(amount)}`);
    }
    $("details").innerHTML = details.map(s => `• ${s}`).join("<br>");
  }

  function reset(){
    $("hireDate").value = "";
    $("leaveDays").value = "";
    $("serviceDays").textContent = "—";
    $("ratio").textContent = "—";
    $("amount").textContent = "—";
    $("statusTag").innerHTML = "";
    $("details").innerHTML = "";
  }

  $("calcBtn").addEventListener("click", calc);
  $("resetBtn").addEventListener("click", reset);

  // 預設幫使用者把基準日/區間資訊放在今天情境中也合理，但不強制。
</script>
</body>
</html>
