<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>HWG/JPY</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<style>
  html, body { height: 100%; margin: 0; }
  body { background:#0d0d0d; color:#e6f7e1; font-family:Inter,Arial, sans-serif; height:100vh; display:flex; }
  .container { width:100%; height:100%; margin:0; padding:18px; box-sizing:border-box; display:flex; flex-direction:column; }
  .header { display:flex; justify-content:space-between; align-items:center; gap:12px }
  h2{margin:0}
  .card { background:linear-gradient(180deg,#07101a,#07161f); border:1px solid rgba(120,255,150,0.06); padding:12px; border-radius:10px; flex:1; display:flex; flex-direction:column; }
  #score { font-size:28px; font-weight:700 }
  #pillars { display:flex; gap:12px; flex-wrap:wrap; margin-bottom:8px }
  .pill { background:rgba(255,255,255,0.03); padding:6px 8px; border-radius:6px; font-size:13px }
  canvas { width:100% !important; height:100% !important; display:block; margin-top:12px; flex:1 1 auto; }
  .small { font-size:13px; color:#9fb0d8 }
  /* make header and info not exceed space */
  .topRow { display:flex; justify-content:space-between; align-items:flex-start; gap:12px }
  .infoBox { display:flex; flex-direction:column; align-items:flex-end }
</style>
<style>
html, body { margin:0; padding:0; width:100%; height:100%; }
#app, .container, .main-wrapper { width:100vw; height:100vh; }
canvas { width:100% !important; height:100% !important; }
</style></head>
<body>
<div class="container">
  <div class="header">
    <h2>HWG/JPY</h2>
    <div class="small">本命: 甲申 / 辛未 / 壬子 / 戊申 ・ 大運: 癸酉</div>
  </div>

  <div class="card">
    <div id="pillars">
      <div class="pill">大運: <span id="pill-dayun">--</span></div>
      <div class="pill">年運: <span id="pill-year">--</span></div>
      <div class="pill">月運: <span id="pill-month">--</span></div>
      <div class="pill">日運: <span id="pill-day">--</span></div>
      <div class="pill">時運: <span id="pill-hour">--</span></div>
      <div class="pill">秒運: <span id="pill-second">--</span></div>
    </div>

    <div style="display:flex;justify-content:space-between;align-items:center">
      <div>
        
        
        <div id="kanshi">現在の秒干支: --</div>
        
      </div>
      <div style="text-align:right">
        <div id="marketcap" class="small">時価総額: -- 円</div>
        <div id="score">--</div>
<div id="daily-change" class="text-sm text-gray-500">前月比： --%</div>
        
      </div>
    </div>

    <canvas id="lineChart"></canvas>
  </div>
</div>

<script>
// ----- 設定 -----
const STEM_MOD = { '癸': -5,'乙': -2,'己': -3,'丙': +5,'丁': +1,'戊': +4,'壬': +1,'庚': -2,'辛': +1,'甲': +3 };
const BAZI = { year:['甲','申'], month:['辛','未'], day:['壬','子'], hour:['戊','申'] };
function getDayunByDate(d){
  const y = d.getFullYear();
  const m = d.getMonth()+1;
  // 月運切り替え時期を6月と仮定
  const afterJune = (m >= 6);

  if (y < 2026 || (y === 2026 && !afterJune)) return ['癸','酉']; // 現行
  if (y < 2036 || (y === 2036 && !afterJune)) return ['甲','戌'];
  if (y < 2046 || (y === 2046 && !afterJune)) return ['乙','亥'];
  return ['丙','子'];
}

// 旧: const DAYUN = ['癸','酉'];
const STEMS=['甲','乙','丙','丁','戊','己','庚','辛','壬','癸'];
const BRANCHES=['子','丑','寅','卯','辰','巳','午','未','申','酉','戌','亥'];
// 五行マップ（参考）
const STEM_WX = { '甲':'木','乙':'木','丙':'火','丁':'火','戊':'土','己':'土','庚':'金','辛':'金','壬':'水','癸':'水' };
const BRANCH_WX = { '子':'水','丑':'土','寅':'木','卯':'木','辰':'土','巳':'火','午':'火','未':'土','申':'金','酉':'金','戌':'土','亥':'水' };

// Chart.js
const ctx = document.getElementById('lineChart').getContext('2d');
const chart = new Chart(ctx, {
  type:'line', data:{ labels:[], datasets:[{ label:'Fortune Score', data:[], borderWidth:2, tension:0.3, pointRadius:0, borderColor:'#7CFC00' }] },
  options:{ responsive:true, animation:false, scales:{ y:{ beginAtZero:true } }, plugins:{ legend:{ display:false } } }
});

// ---- 干支算出ユーティリティ（簡易だが一貫した算出） ----
function yearPillarByDate(d){
  // 立春(2/4) を境に年が変わるルールの簡易実装
  const y = d.getFullYear();
  const lichun = new Date(y,1,4); // 2/4 (approx)
  const yearForGanZhi = (d >= lichun) ? y : y-1;
  const idx = (yearForGanZhi - 4) % 60; // 1984 を甲子(=4)基準
  const stem = STEMS[(yearForGanZhi - 4) % 10];
  const branch = BRANCHES[(yearForGanZhi - 4) % 12];
  return [stem, branch];
}

function monthPillarByDate(d){
  // 立春起点で月支を決める（簡易）。月番号 1=寅
  const month = d.getMonth() + 1; // 1..12
  const day = d.getDate();
  // if before Feb4 consider previous year shift for month mapping
  // monthIndex: 0..11 -> 寅..丑
  // compute offset from Feb
  const offset = ((month - 2) + (day >= 4 ? 0 : -1) + 12) % 12;
  const branch = ['寅','卯','辰','巳','午','未','申','酉','戌','亥','子','丑'][offset];
  // month stem rule: (yearStemIdx*2 + monthNumber -1) %10
  const yearStem = yearPillarByDate(d)[0];
  const yIdx = STEMS.indexOf(yearStem);
  const monthNumber = offset + 1;
  const stem = STEMS[(yIdx*2 + monthNumber -1) % 10];
  return [stem, branch];
}

function dayPillarByDate(d){
  // 基準日 1984-02-02 を甲子日とする
  const base = new Date(Date.UTC(1984,1,2,0,0,0));
  const cur = new Date(Date.UTC(d.getFullYear(), d.getMonth(), d.getDate(),0,0,0));
  const diff = Math.round((cur - base)/86400000);
  const stem = STEMS[(diff % 10 + 10) % 10];
  const branch = BRANCHES[(diff % 12 + 12) % 12];
  return [stem, branch];
}

function hourPillarByDate(d){
  // 時支 index: ((hour+1)//2) %12
  const dayStem = dayPillarByDate(d)[0];
  const hour = d.getHours();
  const idx = Math.floor((hour + 1) / 2) % 12;
  const branch = BRANCHES[idx];
  const dayIdx = STEMS.indexOf(dayStem);
  const stem = STEMS[(dayIdx*2 + idx) % 10];
  return [stem, branch];
}

function secondPillarByDate(d){
  const s = d.getSeconds();
  const stem = STEMS[s % 10];
  const branch = BRANCHES[s % 12];
  return [stem, branch];
}

// ---- 総合スコア算出 ----
function computeFullScore(d){
  // compute pillars
  const dayun = getDayunByDate(d); // given
  const year = yearPillarByDate(d);
  const month = monthPillarByDate(d);
  const day = dayPillarByDate(d);
  const hour = hourPillarByDate(d);
  const second = secondPillarByDate(d);

  // weights (importance)
  const weights = { dayun:20, year:5, month:3, day:1, hour:0.5, second:0.1 };

  // accumulate stem mods
  let total = 0;
  total += (STEM_MOD[dayun[0]] || 0) * weights.dayun;
  total += (STEM_MOD[year[0]] || 0) * weights.year;
  total += (STEM_MOD[month[0]] || 0) * weights.month;
  total += (STEM_MOD[day[0]] || 0) * weights.day;
  total += (STEM_MOD[hour[0]] || 0) * weights.hour;
  total += (STEM_MOD[second[0]] || 0) * weights.second;

  // branch numeric contribution (1..12 scaled)
  const bval = function(br){ return (BRANCHES.indexOf(br) + 1) * 0.2; };
  total += bval(dayun[1]) * weights.dayun;
  total += bval(year[1]) * weights.year;
  total += bval(month[1]) * weights.month;
  total += bval(day[1]) * weights.day;
  total += bval(hour[1]) * weights.hour;
  total += bval(second[1]) * weights.second;

  // --- 三合判定（＋方合判定追加済） ---
  function checkSanhe(pillars){
    const groups = {
      '金': ['酉','巳','丑'],
      '火': ['午','寅','戌'],
      '水': ['子','申','辰'],
      '木': ['卯','亥','未']
    };
    const baseScore = { '金': -4, '火': 5, '水': -3, '木': 4 };

    const list = [BAZI.year[1], BAZI.month[1], pillars.dayun[1], pillars.year[1], pillars.month[1]];
    let score = 0;

    for(const k in groups){
      const g = groups[k];
      if(g.every(x => list.includes(x))) score = baseScore[k];
    }

    if(score === 0) return 0;

    const baziSet = new Set([BAZI.year[1], BAZI.month[1]]);
    const hitsBazi = g => g.filter(x => baziSet.has(x)).length;

    const g = Object.values(groups).find(group => group.every(x => list.includes(x)));

    const inBazi = g.filter(x => baziSet.has(x)).length;
    const inDayun = g.includes(pillars.dayun[1]);
    const inYear = g.includes(pillars.year[1]);
    const inMonth = g.includes(pillars.month[1]);

    if(inBazi >= 1 && inDayun) return score * 5;
    if(inDayun && inYear) return score * 3;
    if(inDayun && inMonth) return score * 1;
    if(inBazi >= 1 && inYear) return score * 2;

    return score;
  }
  total += checkSanhe({dayun, year, month});

  // --- 方合判定（すべて凶：-30） ---
  function checkFanghe(pillars){
    const groups = [
      ['寅','卯','辰'], // 木局
      ['申','酉','戌'], // 金局
      ['巳','午','未'], // 火局
      ['亥','子','丑']  // 水局
    ];
    const list = [BAZI.year[1], BAZI.month[1], pillars.dayun[1], pillars.year[1], pillars.month[1]];
    for(const g of groups){ if(g.every(x => list.includes(x))) return -20; }
    return 0;
  }
  total += checkFanghe({dayun, year, month});

  // --- 半会判定 ---
  function checkBanHui(pillars){
    const pairs = {
      '子申': 1,
      '子辰': 1,
      '酉巳': -5,
      '酉丑': -5,
      '午戌': 3,
      '午寅': 4,
      '卯亥': 3,
      '卯未': 2
    };

    const baseList = [BAZI.year[1], BAZI.month[1]];
    const list = [BAZI.year[1], BAZI.month[1], pillars.dayun[1], pillars.year[1], pillars.month[1]];

    let totalScore = 0;

    for(const p in pairs){
      const a = p.charAt(0);
      const b = p.charAt(1);
      if(!(list.includes(a) && list.includes(b))) continue;

      let base = pairs[p];
      let mult = 1;
      const inBazi = baseList.includes(a) || baseList.includes(b);
      const inDayun = (pillars.dayun[1] === a || pillars.dayun[1] === b);
      const inYear = (pillars.year[1] === a || pillars.year[1] === b);
      const inMonth = (pillars.month[1] === a || pillars.month[1] === b);

      if(inBazi && inDayun) mult = 3;
      else if(inDayun && inYear) mult = 2;
      else if(inDayun && inMonth) mult = 1;
      else if(inBazi && inYear) mult = 2;
      else mult = 1;

      totalScore += base * mult;
    }
    return totalScore;
  }
  total += checkBanHui({dayun, year, month});

   checkSanhe({dayun, year, month});

  // base + total
  const base = 100;
  let core = base + total;

  // FX-like dynamics (momentum + shock)
  if (typeof computeFullScore.prev === 'undefined') computeFullScore.prev = core;
  if (typeof computeFullScore.vol === 'undefined') computeFullScore.vol = 1.0;
  const prev = computeFullScore.prev;
  let momentum = (core - prev) * 0.6;
  const shock = (Math.random() - 0.5) * 6 * computeFullScore.vol;
  const meanRev = (core - prev) * 0.1;
  const next = prev + momentum + shock + meanRev;
  computeFullScore.vol = 0.85 * computeFullScore.vol + 0.15 * Math.abs(shock) / 3.0;
  computeFullScore.prev = next;

  return {
    score: next,
    pillars: { dayun, year, month, day, hour, second },
    breakdown: { total }
  };
}

// ---- 描画ループ ----
function updateUI(){
  const now = new Date();
  const res = computeFullScore(now);
  // fill pillars
  document.getElementById('pill-dayun').innerText = res.pillars.dayun.join('');
  document.getElementById('pill-year').innerText = res.pillars.year.join('');
  document.getElementById('pill-month').innerText = res.pillars.month.join('');
  document.getElementById('pill-day').innerText = res.pillars.day.join('');
  document.getElementById('pill-hour').innerText = res.pillars.hour.join('');
  document.getElementById('pill-second').innerText = res.pillars.second.join('');

  document.getElementById('kanshi').innerText = `現在の秒干支: ${res.pillars.second.join('')}`;
  document.getElementById('score').innerText = `${res.score.toFixed(2)} 円`;
  

  // 合局詳細の表示
  

  // 前月比の計算
  const prevDate = new Date(now.getFullYear(), now.getMonth() - 1, now.getDate());
  const prevRes = computeFullScore(prevDate);
  const mom = ((res.score - prevRes.score) / prevRes.score) * 100;
  document.getElementById('daily-change').innerText = `前月比： ${mom.toFixed(2)}%`;

  // 時価総額（例：スコア × 1000）
  const marketcap = (res.score * 10000).toFixed(0);
  document.getElementById('marketcap').innerText = `時価総額: ${marketcap} 円`;

  // push chart
  const t = now.toLocaleTimeString();
  chart.data.labels.push(t);
  chart.data.datasets[0].data.push(res.score);
  if(chart.data.labels.length>240){ chart.data.labels.shift(); chart.data.datasets[0].data.shift(); }
  chart.update('none');
}

setInterval(updateUI, 1000);
updateUI();
</script>
</body>
</html>
