<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Trustly ABA — Business Tracker</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700&family=DM+Serif+Display:ital@0;1&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --brand:#f06d59;
  --brand-dark:#d4533f;
  --brand-light:#fde8e5;
  --brand-mid:#f9b5ab;
  --bg:#dcf0fa;
  --bg2:#cce6f5;
  --bg3:#b8d8ee;
  --surface:#ffffff;
  --surface2:#f0f9ff;
  --ink:#1a2e38;
  --muted:#4a6b7a;
  --text-secondary:#5a7d8e;
  --text-tertiary:#8aaab8;
  --border:#c2dcea;
  --border2:#a8ccd8;
  --amber:#c17c1a;
  --amber-pale:#fef3e0;
  --teal:#1D9E75;
  --teal-pale:#E1F5EE;
  --teal-mid:#9FE1CB;
  --teal-dark:#0F6E56;
  font-family:'Plus Jakarta Sans',sans-serif;
}

body{background:var(--bg);color:var(--ink);min-height:100vh}

.header{background:var(--surface);border-bottom:1.5px solid var(--border);padding:1rem 2rem;display:flex;align-items:center;justify-content:space-between;gap:1rem;flex-wrap:wrap;position:sticky;top:0;z-index:50;box-shadow:0 2px 12px rgba(26,46,56,.06)}
.logo-area{display:flex;align-items:center;gap:1rem}
.logo-img{height:52px;width:auto}
.header-text .header-title{font-size:12px;font-weight:700;color:var(--brand);letter-spacing:.1em;text-transform:uppercase}
.header-text .header-sub{font-size:11px;color:var(--text-tertiary);margin-top:2px}
.phase-badge{font-size:12px;padding:6px 16px;border-radius:20px;background:var(--brand-light);color:var(--brand-dark);font-weight:700;border:1.5px solid var(--brand-mid);white-space:nowrap}

.page{max-width:920px;margin:0 auto;padding:2rem 1.5rem 3rem}

.metrics{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:1.75rem}
@media(max-width:640px){.metrics{grid-template-columns:repeat(2,1fr)}}
.metric{background:var(--surface);border-radius:14px;padding:1.125rem 1.25rem;border:1.5px solid var(--border);position:relative;overflow:hidden}
.metric::before{content:'';position:absolute;top:0;left:0;right:0;height:3px;background:linear-gradient(90deg,var(--brand),var(--brand-mid))}
.metric-label{font-size:10px;color:var(--text-tertiary);margin-bottom:6px;text-transform:uppercase;letter-spacing:.08em;font-weight:700}
.metric-val{font-size:26px;font-weight:700;color:var(--ink);letter-spacing:-.02em;line-height:1}
.metric-sub{font-size:11px;color:var(--text-secondary);margin-top:5px}

.overall-card{background:var(--surface);border:1.5px solid var(--border);border-radius:16px;padding:1.25rem 1.5rem;margin-bottom:1.75rem}
.overall-top{display:flex;justify-content:space-between;align-items:center;margin-bottom:.875rem}
.overall-title{font-family:'DM Serif Display',serif;font-size:16px;color:var(--ink)}
.overall-pct{font-size:16px;font-weight:700;color:var(--brand)}
.bar-track{height:10px;background:var(--bg2);border-radius:5px;overflow:hidden;border:1px solid var(--border)}
.bar-fill{height:100%;border-radius:5px;background:linear-gradient(90deg,var(--brand-dark),var(--brand),#f4957f);transition:width .5s cubic-bezier(.4,0,.2,1)}
.phase-dots{display:flex;justify-content:space-between;margin-top:10px}
.phase-dot-label{font-size:10px;color:var(--text-tertiary);text-align:center;width:14%;font-weight:500}
.phase-dot-label.active-dot{color:var(--brand-dark);font-weight:700}

.legend-row{display:flex;gap:1rem;margin-bottom:1.25rem;flex-wrap:wrap;align-items:center}
.leg{display:flex;align-items:center;gap:6px;font-size:12px;color:var(--text-secondary);font-weight:500}
.leg-dot{width:9px;height:9px;border-radius:3px;flex-shrink:0}
.hint{font-size:11px;color:var(--text-tertiary);margin-left:auto;font-style:italic}

.phase-nav{display:flex;gap:6px;margin-bottom:1.25rem;flex-wrap:wrap}
.phase-btn{font-size:12px;padding:6px 14px;border-radius:20px;border:1.5px solid var(--border2);background:var(--surface);color:var(--text-secondary);cursor:pointer;font-family:inherit;font-weight:500;transition:all .15s;white-space:nowrap}
.phase-btn:hover{background:var(--bg2);border-color:var(--brand-mid)}
.phase-btn.active{background:var(--brand);color:#fff;border-color:var(--brand);font-weight:700}
.phase-btn.current-phase:not(.active){border-color:var(--brand);color:var(--brand-dark);font-weight:600}

.phase-panel{background:var(--surface);border:1.5px solid var(--border);border-radius:20px;overflow:hidden;margin-bottom:1.25rem}
.phase-header{padding:1.25rem 1.5rem;border-bottom:1.5px solid var(--border);display:flex;align-items:center;justify-content:space-between;gap:1rem;background:var(--surface2)}
.phase-title-group{display:flex;align-items:center;gap:.875rem}
.phase-num{width:34px;height:34px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:13px;font-weight:700;flex-shrink:0}
.phase-name{font-family:'DM Serif Display',serif;font-size:19px;color:var(--ink);display:flex;align-items:center;gap:.625rem;flex-wrap:wrap}
.phase-desc{font-size:12px;color:var(--text-secondary);margin-top:3px}
.phase-pct{font-size:18px;font-weight:700;min-width:44px;text-align:right;letter-spacing:-.02em}
.current-pill{font-size:10px;background:var(--brand-light);color:var(--brand-dark);padding:3px 10px;border-radius:20px;font-weight:700;border:1.5px solid var(--brand-mid);font-family:'Plus Jakarta Sans',sans-serif;letter-spacing:.04em;text-transform:uppercase}

.ws-list{padding:1rem 1.25rem;display:flex;flex-direction:column;gap:.625rem}
.ws-row{border:1.5px solid var(--border);border-radius:10px;overflow:hidden;transition:border-color .15s}
.ws-row:hover{border-color:var(--brand-mid)}
.ws-header-row{display:flex;align-items:center;gap:.75rem;padding:.875rem 1rem;cursor:pointer;background:var(--surface);user-select:none;transition:background .15s}
.ws-header-row:hover{background:var(--surface2)}
.ws-title-text{font-size:13px;font-weight:600;color:var(--ink);flex:1}
.ws-count{font-size:12px;color:var(--text-tertiary);min-width:30px;text-align:right;font-weight:500}
.mini-bar{width:72px;height:5px;background:var(--bg2);border-radius:3px;overflow:hidden;flex-shrink:0}
.mini-fill{height:100%;border-radius:3px;transition:width .3s}
.chevron{font-size:9px;color:var(--text-tertiary);transition:transform .2s;flex-shrink:0}
.chevron.open{transform:rotate(90deg)}
.task-list{border-top:1.5px solid var(--border);background:var(--surface2);padding:.75rem 1rem;display:none;flex-direction:column;gap:2px}
.task-list.open{display:flex}

.task-row{display:flex;align-items:center;gap:.75rem;padding:7px 6px;cursor:pointer;border-radius:8px;transition:background .1s}
.task-row:hover{background:var(--bg2)}
.task-check{width:18px;height:18px;border-radius:5px;border:1.5px solid var(--border2);display:flex;align-items:center;justify-content:center;flex-shrink:0;transition:all .15s;background:white}
.task-check.done{background:var(--teal);border-color:var(--teal)}
.task-check.prog{background:var(--amber-pale);border-color:var(--amber)}
.task-check svg{width:10px;height:10px}
.task-label{font-size:13px;color:var(--ink);flex:1;line-height:1.45}
.task-label.done{color:var(--text-tertiary);text-decoration:line-through;text-decoration-color:var(--border2)}
.task-tag{font-size:10px;padding:3px 9px;border-radius:20px;white-space:nowrap;flex-shrink:0;font-weight:600;letter-spacing:.02em}

.footer{text-align:center;padding:2.5rem 0 1rem;font-size:12px;color:var(--text-tertiary)}
.footer em{color:var(--brand);font-style:normal;font-weight:600}
</style>
</head>
<body>

<div class="header">
  <div class="logo-area">
    <img src="5.png" class="logo-img" alt="Trustly ABA" onerror="this.style.display='none';document.getElementById('fallback-logo').style.display='block'">
    <div id="fallback-logo" style="display:none;font-family:'DM Serif Display',serif;font-size:22px;color:var(--brand)">trustly <span style="font-size:14px;font-family:'Plus Jakarta Sans',sans-serif;font-weight:600;color:var(--text-secondary)">aba</span></div>
    <div class="header-text">
      <div class="header-title">Business Tracker</div>
      <div class="header-sub">Click any task to update · progress auto-saved</div>
    </div>
  </div>
  <div class="phase-badge" id="current-phase-badge">Phase 3 — Formation</div>
</div>

<div class="page">

  <div class="metrics">
    <div class="metric"><div class="metric-label">Current phase</div><div class="metric-val" id="m-phase">3 of 7</div><div class="metric-sub" id="m-phase-sub">Formation</div></div>
    <div class="metric"><div class="metric-label">Tasks complete</div><div class="metric-val" id="m-done">0</div><div class="metric-sub" id="m-done-sub">of 0 total</div></div>
    <div class="metric"><div class="metric-label">Phase progress</div><div class="metric-val" id="m-pct">0%</div><div class="metric-sub">active phase</div></div>
    <div class="metric"><div class="metric-label">Overall progress</div><div class="metric-val" id="m-overall">0%</div><div class="metric-sub">across all phases</div></div>
  </div>

  <div class="overall-card">
    <div class="overall-top">
      <div class="overall-title">Overall journey</div>
      <div class="overall-pct" id="overall-pct-label">0%</div>
    </div>
    <div class="bar-track"><div class="bar-fill" id="overall-bar" style="width:0%"></div></div>
    <div class="phase-dots">
      <div class="phase-dot-label" id="pdot-0">Ideation</div>
      <div class="phase-dot-label" id="pdot-1">Validation</div>
      <div class="phase-dot-label active-dot" id="pdot-2">Formation</div>
      <div class="phase-dot-label" id="pdot-3">Pre-launch</div>
      <div class="phase-dot-label" id="pdot-4">Launch</div>
      <div class="phase-dot-label" id="pdot-5">Growth</div>
      <div class="phase-dot-label" id="pdot-6">Scale</div>
    </div>
  </div>

  <div class="legend-row">
    <div class="leg"><div class="leg-dot" style="background:var(--teal)"></div>Complete</div>
    <div class="leg"><div class="leg-dot" style="background:var(--amber)"></div>In progress</div>
    <div class="leg"><div class="leg-dot" style="background:var(--border2)"></div>Not started</div>
    <div class="hint">Click any task to cycle status →</div>
  </div>

  <div class="phase-nav" id="phase-nav"></div>
  <div id="phase-content"></div>

  <div class="footer">Made with care for <em>trustly aba</em> · Find the clinics that deserve you.</div>
</div>

<script>
const STORAGE_KEY='trustly_tracker_v2';
const phases=[
  {name:"Ideation",desc:"Problem, concept, initial research",workstreams:[
    {name:"Problem definition",tasks:[
      {label:"Identify core problem for BCBAs",s:"done"},
      {label:"Define target audience",s:"done"},
      {label:"Research competitive landscape",s:"done"}
    ]},
    {name:"Concept development",tasks:[
      {label:"Platform concept articulated",s:"done"},
      {label:"Core value proposition written",s:"done"}
    ]}
  ]},
  {name:"Validation",desc:"Test assumptions, find PMF signal",workstreams:[
    {name:"Market research",tasks:[
      {label:"BCBA interviews / surveys conducted",s:"done"},
      {label:"Clinic pain points documented",s:"done"},
      {label:"Demand signal confirmed",s:"done"}
    ]},
    {name:"Concept testing",tasks:[
      {label:"Concept shared with BCBA network",s:"done"},
      {label:"Feedback incorporated into platform design",s:"done"},
      {label:"Early interest list started",s:"done"}
    ]}
  ]},
  {name:"Formation",desc:"Entity, brand, systems, early partners",workstreams:[
    {name:"Legal & entity",tasks:[
      {label:"Business entity formed",s:"done"},
      {label:"Contractor agreement — Danielle (NJ, profit share)",s:"done"},
      {label:"IP ownership documented",s:"prog"},
      {label:"Terms of service + privacy policy drafted",s:"todo"},
      {label:"Ambassador / affiliate agreement template",s:"todo"}
    ]},
    {name:"Brand & identity",tasks:[
      {label:"Name, tagline, brand voice finalized",s:"done"},
      {label:"Color system established",s:"done"},
      {label:"Logo created",s:"done"},
      {label:"Platform pillars named",s:"done"},
      {label:"Homepage live — waitlist capturing",s:"prog"}
    ]},
    {name:"Product architecture",tasks:[
      {label:"Platform structure + user flows defined",s:"done"},
      {label:"Trustly Verified standard scoped",s:"done"},
      {label:"Clinivise API integration proposal",s:"prog"},
      {label:"MVP build — The Board + waitlist",s:"todo"},
      {label:"Clinic-facing Talent Hub dashboard",s:"todo"}
    ]},
    {name:"Revenue model",tasks:[
      {label:"Placement fee model defined",s:"done"},
      {label:"Referral / affiliate fee structure scoped",s:"done"},
      {label:"Clinivise licensing + rev share formalizing",s:"prog"},
      {label:"Clinic subscription / Verified access pricing",s:"todo"},
      {label:"Financial model — unit economics, runway",s:"todo"}
    ]},
    {name:"Distribution & partnerships",tasks:[
      {label:"Ambassador program structure defined",s:"done"},
      {label:"Christina Torres (ABA Made Ez) outreach",s:"prog"},
      {label:"Social content strategy — IG carousels + reels",s:"prog"},
      {label:"First 5–10 clinics in Verified pipeline",s:"todo"},
      {label:"First 500 BCBA waitlist signups",s:"todo"}
    ]}
  ]},
  {name:"Pre-launch",desc:"Waitlist, ambassadors, product build",workstreams:[
    {name:"Audience building",tasks:[
      {label:"Ambassador program live (Phase 1)",s:"todo"},
      {label:"500 BCBA signups reached",s:"todo"},
      {label:"10 verified clinics onboarded",s:"todo"}
    ]},
    {name:"Product readiness",tasks:[
      {label:"The Board MVP functional",s:"todo"},
      {label:"Trustly Verified process end-to-end tested",s:"todo"},
      {label:"Talent Hub clinic dashboard functional",s:"todo"},
      {label:"Payment / billing infrastructure set up",s:"todo"}
    ]},
    {name:"Go-to-market prep",tasks:[
      {label:"Launch announcement drafted",s:"todo"},
      {label:"Email sequence for waitlist built",s:"todo"},
      {label:"Social launch campaign ready",s:"todo"}
    ]}
  ]},
  {name:"Launch",desc:"Go live, first users, first revenue",workstreams:[
    {name:"Platform launch",tasks:[
      {label:"The Board publicly live",s:"todo"},
      {label:"First 10 job listings posted",s:"todo"},
      {label:"collABArate community open",s:"todo"}
    ]},
    {name:"First revenue",tasks:[
      {label:"First BCBA placement completed",s:"todo"},
      {label:"First clinic Trustly Verified subscription",s:"todo"},
      {label:"Ambassador Phase 2 bonuses paid out",s:"todo"}
    ]}
  ]},
  {name:"Growth",desc:"Scale users, revenue, team, partnerships",workstreams:[
    {name:"User growth",tasks:[
      {label:"2,500 active BCBAs on platform",s:"todo"},
      {label:"50 verified clinics",s:"todo"},
      {label:"Presence in 15+ states",s:"todo"}
    ]},
    {name:"Revenue scale",tasks:[
      {label:"10+ placements per month",s:"todo"},
      {label:"Recurring clinic subscription revenue",s:"todo"},
      {label:"Profitable unit economics confirmed",s:"todo"}
    ]}
  ]},
  {name:"Scale",desc:"Optimize, expand, defend position",workstreams:[
    {name:"Expansion",tasks:[
      {label:"National coverage — all 50 states",s:"todo"},
      {label:"RBT and other ABA roles added",s:"todo"},
      {label:"Enterprise clinic partnerships",s:"todo"}
    ]},
    {name:"Platform maturity",tasks:[
      {label:"Data / insights product for clinics",s:"todo"},
      {label:"BCBA credentialing API licensed to 3rd parties",s:"todo"}
    ]}
  ]}
];

const sBg={done:'#E1F5EE',prog:'#fef3e0',todo:'#eef6fb'};
const sCol={done:'#085041',prog:'#8a5200',todo:'#6a9ab0'};
const sLbl={done:'Done ✓',prog:'In progress',todo:'Not started'};

let state={},active=2;

function load(){try{const s=localStorage.getItem(STORAGE_KEY);if(s)state=JSON.parse(s);else init();}catch(e){init();}}
function save(){try{localStorage.setItem(STORAGE_KEY,JSON.stringify(state));}catch(e){}}
function init(){phases.forEach((p,pi)=>p.workstreams.forEach((w,wi)=>w.tasks.forEach((t,ti)=>{state[`${pi}-${wi}-${ti}`]=t.s;})));}
function cycle(k){const o=['todo','prog','done'];state[k]=o[(o.indexOf(state[k])+1)%3];save();renderAll();}
function prog(pi){let t=0,d=0;phases[pi].workstreams.forEach((w,wi)=>w.tasks.forEach((_,ti)=>{t++;if(state[`${pi}-${wi}-${ti}`]==='done')d++;}));return{t,d,pct:t?Math.round(d/t*100):0};}
function overall(){let t=0,d=0;phases.forEach((_,i)=>{const p=prog(i);t+=p.t;d+=p.d;});return t?Math.round(d/t*100):0;}
function curPhase(){for(let i=0;i<phases.length;i++){if(prog(i).pct<100)return i;}return phases.length-1;}

function renderNav(){
  document.getElementById('phase-nav').innerHTML=phases.map((p,i)=>{
    const {pct}=prog(i),cur=i===curPhase();
    return`<button class="phase-btn${i===active?' active':''}${cur?' current-phase':''}" onclick="setPhase(${i})">${i+1}. ${p.name}${pct>0?' · '+pct+'%':''}</button>`;
  }).join('');
}

function renderPhase(){
  const ph=phases[active];const{pct}=prog(active);const cur=active===curPhase();
  const nBg=cur?'#fde8e5':'#eef6fb',nCol=cur?'#d4533f':'#6a9ab0';
  const pCol=pct===100?'var(--teal)':pct>0?'var(--amber)':'var(--text-tertiary)';
  let html=`<div class="phase-panel"><div class="phase-header"><div class="phase-title-group"><div class="phase-num" style="background:${nBg};color:${nCol}">${active+1}</div><div><div class="phase-name">${ph.name}${cur?'<span class="current-pill">Now</span>':''}</div><div class="phase-desc">${ph.desc}</div></div></div><div class="phase-pct" style="color:${pCol}">${pct}%</div></div><div class="ws-list">`;
  ph.workstreams.forEach((ws,wi)=>{
    const wd=ws.tasks.filter((_,ti)=>state[`${active}-${wi}-${ti}`]==='done').length;
    const wt=ws.tasks.length,wp=wt?Math.round(wd/wt*100):0;
    const id=`ws-${active}-${wi}`,bc=wp===100?'var(--teal)':wp>0?'var(--amber)':'var(--border2)';
    html+=`<div class="ws-row"><div class="ws-header-row" onclick="toggleWs('${id}')"><div class="chevron" id="chev-${id}">▶</div><div class="ws-title-text">${ws.name}</div><div class="mini-bar"><div class="mini-fill" style="width:${wp}%;background:${bc}"></div></div><div class="ws-count">${wd}/${wt}</div></div><div class="task-list" id="${id}">`;
    ws.tasks.forEach((_,ti)=>{
      const k=`${active}-${wi}-${ti}`,s=state[k],lbl=ws.tasks[ti].label;
      const chk=s==='done'?`<svg viewBox="0 0 10 10" fill="none" stroke="white" stroke-width="2.2" stroke-linecap="round"><path d="M1.5 5l2.5 2.5 4.5-4.5"/></svg>`:s==='prog'?`<svg viewBox="0 0 10 10" fill="none" stroke="#c17c1a" stroke-width="2" stroke-linecap="round"><path d="M5 2v3l2 2"/></svg>`:'';
      html+=`<div class="task-row" onclick="cycle('${k}')"><div class="task-check ${s}">${chk}</div><div class="task-label${s==='done'?' done':''}">${lbl}</div><div class="task-tag" style="background:${sBg[s]};color:${sCol[s]}">${sLbl[s]}</div></div>`;
    });
    html+=`</div></div>`;
  });
  html+=`</div></div>`;
  document.getElementById('phase-content').innerHTML=html;
}

function renderMetrics(){
  const c=curPhase();const{pct}=prog(c);
  const at=phases.reduce((a,_,i)=>a+prog(i).t,0);
  const ad=phases.reduce((a,_,i)=>a+prog(i).d,0);
  const ov=overall();
  document.getElementById('m-phase').textContent=`${c+1} of 7`;
  document.getElementById('m-phase-sub').textContent=phases[c].name;
  document.getElementById('m-done').textContent=ad;
  document.getElementById('m-done-sub').textContent=`of ${at} total`;
  document.getElementById('m-pct').textContent=pct+'%';
  document.getElementById('m-overall').textContent=ov+'%';
  document.getElementById('overall-bar').style.width=ov+'%';
  document.getElementById('overall-pct-label').textContent=ov+'%';
  document.getElementById('current-phase-badge').textContent=`Phase ${c+1} — ${phases[c].name}`;
  for(let i=0;i<7;i++){const e=document.getElementById(`pdot-${i}`);if(e)e.className='phase-dot-label'+(i===c?' active-dot':'');}
}

function renderAll(){renderMetrics();renderNav();renderPhase();}
function setPhase(i){active=i;renderAll();}
function toggleWs(id){const e=document.getElementById(id),ch=document.getElementById('chev-'+id);e.classList.toggle('open');if(ch)ch.classList.toggle('open',e.classList.contains('open'));}

load();renderAll();
</script>
</body>
</html>

