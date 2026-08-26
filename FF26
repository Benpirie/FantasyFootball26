<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<title>Draft Room — 12-Team Mock Draft Simulator</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Oswald:wght@400;500;600;700&family=Inter:wght@400;500;600;700;800&family=JetBrains+Mono:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
:root{
  --bg-void:#0A0E13;
  --bg-panel:#121821;
  --bg-raised:#1A222C;
  --bg-raised-2:#212B36;
  --line:#242E39;
  --line-soft:#1C2530;
  --text-1:#EAF0F5;
  --text-2:#93A2B0;
  --text-3:#5E6B78;
  --gold:#FFB238;
  --gold-dim:#8A6423;
  --gold-glow:rgba(255,178,56,0.16);
  --user-glow:rgba(255,178,56,0.10);
  --pos-QB:#F4615C;
  --pos-RB:#3ADC9B;
  --pos-WR:#5B9DF9;
  --pos-TE:#E8A33D;
  --pos-DST:#9AA5B1;
  --pos-K:#B98CF0;
  --pos-QB-bg:rgba(244,97,92,0.14);
  --pos-RB-bg:rgba(58,220,155,0.14);
  --pos-WR-bg:rgba(91,157,249,0.14);
  --pos-TE-bg:rgba(232,163,61,0.14);
  --pos-DST-bg:rgba(154,165,177,0.14);
  --pos-K-bg:rgba(185,140,240,0.14);
  --radius:10px;
  --radius-sm:6px;
  --font-display:'Oswald',sans-serif;
  --font-body:'Inter',sans-serif;
  --font-mono:'JetBrains Mono',monospace;
}
*{box-sizing:border-box;}
html,body{margin:0;padding:0;}
body{
  background:var(--bg-void);
  color:var(--text-1);
  font-family:var(--font-body);
  -webkit-font-smoothing:antialiased;
  min-height:100vh;
}
body::before{
  content:'';
  position:fixed;inset:0;
  background:
    radial-gradient(ellipse 900px 500px at 50% -10%, rgba(255,178,56,0.06), transparent 60%),
    repeating-linear-gradient(180deg, rgba(255,255,255,0.012) 0px, rgba(255,255,255,0.012) 1px, transparent 1px, transparent 3px);
  pointer-events:none;
  z-index:0;
}
.wrap{position:relative;z-index:1;max-width:760px;margin:0 auto;padding:0 14px 90px;}
a{color:inherit;}
button{font-family:var(--font-body);cursor:pointer;}
::selection{background:var(--gold-dim);color:#fff;}
:focus-visible{outline:2px solid var(--gold);outline-offset:2px;}
@media (prefers-reduced-motion: reduce){*{animation-duration:0.01ms !important;transition-duration:0.01ms !important;}}

/* ---------- Top masthead ---------- */
.masthead{
  padding:22px 0 14px;
  text-align:center;
}
.masthead .eyebrow{
  font-family:var(--font-mono);
  font-size:11px;
  letter-spacing:0.18em;
  color:var(--gold);
  text-transform:uppercase;
  margin-bottom:6px;
}
.masthead h1{
  font-family:var(--font-display);
  font-weight:700;
  font-size:30px;
  letter-spacing:0.01em;
  margin:0;
  text-transform:uppercase;
}
.masthead h1 span{color:var(--gold);}
.masthead p{color:var(--text-2);font-size:13.5px;margin:6px 0 0;}

/* ---------- Cards / layout ---------- */
.card{
  background:var(--bg-panel);
  border:1px solid var(--line);
  border-radius:var(--radius);
  padding:18px;
  margin-bottom:14px;
}
.card h2{
  font-family:var(--font-display);
  font-size:16px;
  text-transform:uppercase;
  letter-spacing:0.04em;
  margin:0 0 4px;
  font-weight:600;
}
.card .sub{color:var(--text-2);font-size:13px;margin:0 0 16px;line-height:1.5;}
.section-label{
  font-family:var(--font-mono);
  font-size:10.5px;
  letter-spacing:0.12em;
  text-transform:uppercase;
  color:var(--text-3);
  margin:0 0 10px;
}

/* ---------- Buttons ---------- */
.btn{
  border:1px solid var(--line);
  background:var(--bg-raised);
  color:var(--text-1);
  border-radius:var(--radius-sm);
  padding:10px 16px;
  font-size:13.5px;
  font-weight:600;
  transition:background .15s, border-color .15s, transform .1s;
}
.btn:hover{background:var(--bg-raised-2);border-color:#33404d;}
.btn:active{transform:scale(0.98);}
.btn-primary{
  background:var(--gold);
  border-color:var(--gold);
  color:#1A1200;
  font-weight:700;
}
.btn-primary:hover{background:#ffc35e;}
.btn-primary:disabled{opacity:0.4;cursor:not-allowed;}
.btn-block{width:100%;text-align:center;padding:13px;font-size:14px;}
.btn-sm{padding:6px 11px;font-size:12px;border-radius:6px;}
.btn-ghost{background:transparent;}

/* ---------- Setup: slot grid ---------- */
.slot-grid{
  display:grid;
  grid-template-columns:repeat(6,1fr);
  gap:8px;
  margin-bottom:4px;
}
.slot-btn{
  aspect-ratio:1;
  border:1px solid var(--line);
  background:var(--bg-raised);
  border-radius:var(--radius-sm);
  color:var(--text-2);
  font-family:var(--font-mono);
  font-weight:600;
  font-size:15px;
  display:flex;align-items:center;justify-content:center;
  transition:all .12s;
}
.slot-btn:hover{border-color:var(--gold-dim);color:var(--text-1);}
.slot-btn.selected{
  background:var(--gold);
  border-color:var(--gold);
  color:#1A1200;
}

/* ---------- Setup: roster config ---------- */
.roster-grid{
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:10px;
  margin-bottom:6px;
}
@media (max-width:420px){.roster-grid{grid-template-columns:repeat(3,1fr);}}
.roster-field{
  background:var(--bg-raised);
  border:1px solid var(--line);
  border-radius:var(--radius-sm);
  padding:8px 6px;
  text-align:center;
}
.roster-field label{
  display:block;
  font-family:var(--font-mono);
  font-size:10px;
  letter-spacing:0.06em;
  color:var(--text-3);
  margin-bottom:4px;
}
.stepper{display:flex;align-items:center;justify-content:center;gap:6px;}
.stepper button{
  width:22px;height:22px;
  border-radius:5px;
  border:1px solid var(--line);
  background:var(--bg-raised-2);
  color:var(--text-1);
  font-size:13px;
  line-height:1;
  display:flex;align-items:center;justify-content:center;
}
.stepper .val{
  font-family:var(--font-mono);
  font-weight:700;
  font-size:15px;
  min-width:18px;
  text-align:center;
}
.rounds-total{
  text-align:center;
  font-family:var(--font-mono);
  color:var(--text-2);
  font-size:12.5px;
  margin-top:10px;
  padding-top:10px;
  border-top:1px dashed var(--line);
}
.rounds-total b{color:var(--gold);font-size:14px;}

.toggle-row{
  display:flex;align-items:center;justify-content:space-between;
  padding:10px 2px;
}
.toggle-row .t-label{font-size:13.5px;font-weight:600;}
.toggle-row .t-desc{font-size:12px;color:var(--text-2);margin-top:2px;}
.switch{
  width:40px;height:23px;border-radius:99px;
  background:var(--bg-raised-2);border:1px solid var(--line);
  position:relative;flex-shrink:0;transition:background .15s;
}
.switch::after{
  content:'';position:absolute;top:2px;left:2px;
  width:17px;height:17px;border-radius:50%;background:var(--text-2);
  transition:left .15s, background .15s;
}
.switch.on{background:var(--gold-dim);border-color:var(--gold);}
.switch.on::after{left:19px;background:var(--gold);}

/* ---------- Badges ---------- */
.pos-badge{
  display:inline-flex;align-items:center;justify-content:center;
  font-family:var(--font-mono);font-weight:700;font-size:10.5px;
  padding:2px 6px;border-radius:4px;letter-spacing:0.02em;
  min-width:30px;
}
.pos-QB{color:var(--pos-QB);background:var(--pos-QB-bg);}
.pos-RB{color:var(--pos-RB);background:var(--pos-RB-bg);}
.pos-WR{color:var(--pos-WR);background:var(--pos-WR-bg);}
.pos-TE{color:var(--pos-TE);background:var(--pos-TE-bg);}
.pos-DST{color:var(--pos-DST);background:var(--pos-DST-bg);}
.pos-K{color:var(--pos-K);background:var(--pos-K-bg);}

/* ---------- Draft header (sticky) ---------- */
.draft-header{
  position:sticky;top:0;z-index:20;
  background:rgba(10,14,19,0.92);
  backdrop-filter:blur(10px);
  border-bottom:1px solid var(--line);
  padding:10px 14px;
  margin:0 -14px 14px;
}
.dh-row{display:flex;align-items:center;justify-content:space-between;gap:10px;}
.dh-pick{font-family:var(--font-mono);font-size:11px;color:var(--text-3);letter-spacing:0.08em;text-transform:uppercase;}
.dh-clock{
  font-family:var(--font-display);
  font-size:17px;font-weight:600;text-transform:uppercase;
  letter-spacing:0.02em;
}
.dh-clock.user-turn{color:var(--gold);}
.dh-progress{height:3px;background:var(--line-soft);border-radius:99px;margin-top:9px;overflow:hidden;}
.dh-progress-bar{height:100%;background:var(--gold);transition:width .3s;}
.dh-actions{display:flex;gap:8px;margin-top:9px;}

.onclock-banner{
  display:flex;align-items:center;gap:10px;
  background:var(--gold-glow);
  border:1px solid var(--gold-dim);
  border-radius:var(--radius-sm);
  padding:10px 12px;
  margin-bottom:12px;
  animation:pulse-border 1.8s ease-in-out infinite;
}
@keyframes pulse-border{
  0%,100%{border-color:var(--gold-dim);}
  50%{border-color:var(--gold);}
}
.onclock-banner .dot{width:8px;height:8px;border-radius:50%;background:var(--gold);flex-shrink:0;animation:dot-pulse 1.2s ease-in-out infinite;}
@keyframes dot-pulse{0%,100%{opacity:1;}50%{opacity:0.35;}}
.onclock-banner b{color:var(--gold);}

/* ---------- Tabs ---------- */
.tab-bar{
  display:flex;gap:4px;
  background:var(--bg-panel);
  border:1px solid var(--line);
  border-radius:var(--radius-sm);
  padding:4px;
  margin-bottom:14px;
}
.tab-btn{
  flex:1;
  background:transparent;border:none;
  color:var(--text-2);
  font-family:var(--font-mono);
  font-size:11.5px;font-weight:600;letter-spacing:0.03em;
  text-transform:uppercase;
  padding:9px 4px;border-radius:6px;
  transition:all .12s;
}
.tab-btn.active{background:var(--bg-raised-2);color:var(--gold);}
.tab-btn .n{color:var(--text-3);font-weight:400;}
.tab-btn.active .n{color:var(--text-2);}

/* ---------- Player pool ---------- */
.pool-controls{display:flex;gap:8px;margin-bottom:10px;}
.search-input{
  flex:1;
  background:var(--bg-raised);
  border:1px solid var(--line);
  border-radius:var(--radius-sm);
  padding:9px 11px;
  color:var(--text-1);
  font-size:13.5px;
}
.search-input::placeholder{color:var(--text-3);}
.pos-filter-row{display:flex;gap:6px;overflow-x:auto;margin-bottom:10px;padding-bottom:2px;}
.pos-filter{
  flex-shrink:0;
  background:var(--bg-raised);border:1px solid var(--line);
  color:var(--text-2);
  font-family:var(--font-mono);font-size:11.5px;font-weight:600;
  padding:7px 13px;border-radius:99px;
}
.pos-filter.active{background:var(--bg-raised-2);color:var(--text-1);border-color:#3a4757;}

.player-row{
  display:flex;align-items:center;gap:10px;
  padding:10px 8px;
  border-bottom:1px solid var(--line-soft);
}
.player-row:last-child{border-bottom:none;}
.player-rank{
  font-family:var(--font-mono);color:var(--text-3);font-size:11px;
  width:22px;text-align:right;flex-shrink:0;
}
.player-info{flex:1;min-width:0;}
.player-name{font-size:14px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.player-meta{font-size:11.5px;color:var(--text-2);font-family:var(--font-mono);margin-top:1px;}
.player-adp{
  font-family:var(--font-mono);font-size:12px;color:var(--text-2);
  text-align:right;flex-shrink:0;width:52px;
}
.player-adp .r{color:var(--text-3);font-size:10px;display:block;}
.draft-btn{
  flex-shrink:0;
  background:var(--gold);color:#1A1200;border:none;
  font-family:var(--font-mono);font-weight:700;font-size:11px;
  padding:8px 12px;border-radius:6px;
  text-transform:uppercase;
}
.draft-btn:hover{background:#ffc35e;}
.empty-note{text-align:center;color:var(--text-3);font-size:13px;padding:30px 10px;}

/* ---------- Roster ---------- */
.roster-list{display:flex;flex-direction:column;gap:6px;}
.roster-slot{
  display:flex;align-items:center;gap:10px;
  padding:9px 10px;
  background:var(--bg-raised);
  border:1px solid var(--line);
  border-radius:var(--radius-sm);
}
.roster-slot.empty{border-style:dashed;opacity:0.55;}
.slot-tag{
  font-family:var(--font-mono);font-size:10.5px;font-weight:700;color:var(--text-3);
  width:38px;flex-shrink:0;letter-spacing:0.03em;
}
.slot-player{flex:1;font-size:13.5px;font-weight:600;}
.slot-player.placeholder{color:var(--text-3);font-weight:400;font-style:italic;}
.slot-meta{font-family:var(--font-mono);font-size:11px;color:var(--text-3);}

/* ---------- Draft board ---------- */
.board-scroll{overflow-x:auto;margin:0 -18px;padding:0 18px 6px;}
.board-grid{
  display:grid;
  border-top:1px solid var(--line);
  border-left:1px solid var(--line);
  min-width:600px;
}
.board-head-cell,.board-cell{
  border-right:1px solid var(--line);
  border-bottom:1px solid var(--line);
  min-width:0;
}
.board-head-cell{
  font-family:var(--font-mono);font-size:10px;font-weight:700;color:var(--text-2);
  padding:6px 3px;text-align:center;background:var(--bg-raised);
  white-space:nowrap;overflow:hidden;text-overflow:ellipsis;
}
.board-head-cell.user{color:var(--gold);}
.board-cell{
  padding:4px 3px;min-height:38px;
  display:flex;flex-direction:column;align-items:center;justify-content:center;
  text-align:center;font-size:9.5px;line-height:1.25;
  position:relative;
}
.board-cell .bc-name{font-weight:700;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;max-width:100%;}
.board-cell .bc-pos{font-family:var(--font-mono);font-size:8px;opacity:0.8;margin-top:1px;}
.board-cell.onclock{background:var(--gold-glow);outline:1.5px solid var(--gold);outline-offset:-1.5px;}
.board-row-num{
  font-family:var(--font-mono);font-size:10px;color:var(--text-3);
  display:flex;align-items:center;justify-content:center;background:var(--bg-panel);
}

/* ---------- Log ---------- */
.log-list{display:flex;flex-direction:column;gap:2px;}
.log-entry{
  display:flex;align-items:center;gap:9px;
  padding:8px 4px;
  border-bottom:1px solid var(--line-soft);
  font-size:13px;
}
.log-pick-num{font-family:var(--font-mono);color:var(--text-3);font-size:11px;width:38px;flex-shrink:0;}
.log-team{color:var(--text-2);font-size:11.5px;width:64px;flex-shrink:0;font-family:var(--font-mono);}
.log-team.user{color:var(--gold);font-weight:700;}
.log-player{flex:1;font-weight:600;}
.log-tag{
  font-family:var(--font-mono);font-size:9.5px;font-weight:700;
  padding:2px 6px;border-radius:4px;text-transform:uppercase;flex-shrink:0;
}
.log-tag.reach{color:#F4615C;background:rgba(244,97,92,0.14);}
.log-tag.value{color:#3ADC9B;background:rgba(58,220,155,0.14);}

/* ---------- Results ---------- */
.result-team-card{
  background:var(--bg-panel);border:1px solid var(--line);border-radius:var(--radius);
  padding:14px;margin-bottom:10px;
}
.result-team-card.user{border-color:var(--gold-dim);background:var(--user-glow);}
.rt-head{display:flex;align-items:baseline;justify-content:space-between;margin-bottom:8px;flex-wrap:wrap;gap:4px;}
.rt-name{font-family:var(--font-display);font-size:16px;text-transform:uppercase;font-weight:600;}
.rt-name.user{color:var(--gold);}
.rt-arch{font-family:var(--font-mono);font-size:11px;color:var(--text-2);}
.rt-players{display:flex;flex-wrap:wrap;gap:5px;}
.rt-chip{
  display:flex;align-items:center;gap:5px;
  background:var(--bg-raised);border:1px solid var(--line);
  border-radius:5px;padding:4px 7px;font-size:11.5px;
}
.rt-blurb{color:var(--text-2);font-size:12px;margin-top:8px;line-height:1.5;font-style:italic;}

.footer-actions{display:flex;gap:10px;margin-top:18px;}
.footer-actions .btn{flex:1;}

.hidden{display:none !important;}
</style>
</head>
<body>
<div class="wrap" id="app"></div>
<script>
const PLAYERS=[
{id:1,name:'Jahmyr Gibbs',pos:'RB',team:'DET',bye:6,adp:1.5,sd:0.7},
{id:2,name:'Bijan Robinson',pos:'RB',team:'ATL',bye:11,adp:2.2,sd:0.7},
{id:3,name:'Puka Nacua',pos:'WR',team:'LAR',bye:11,adp:3.1,sd:0.9},
{id:4,name:'Ja\'Marr Chase',pos:'WR',team:'CIN',bye:6,adp:3.8,sd:1.0},
{id:5,name:'Jaxon Smith-Njigba',pos:'WR',team:'SEA',bye:11,adp:5.5,sd:1.1},
{id:6,name:'Amon-Ra St. Brown',pos:'WR',team:'DET',bye:6,adp:6.4,sd:1.3},
{id:7,name:'Christian McCaffrey',pos:'RB',team:'SF',bye:8,adp:6.6,sd:1.6},
{id:8,name:'Jonathan Taylor',pos:'RB',team:'IND',bye:13,adp:7.5,sd:1.7},
{id:9,name:'Drake London',pos:'WR',team:'ATL',bye:11,adp:10.1,sd:1.8},
{id:10,name:'De\'Von Achane',pos:'RB',team:'MIA',bye:6,adp:10.4,sd:1.9},
{id:11,name:'CeeDee Lamb',pos:'WR',team:'DAL',bye:14,adp:10.7,sd:1.9},
{id:12,name:'Justin Jefferson',pos:'WR',team:'MIN',bye:6,adp:11.7,sd:2.2},
{id:13,name:'James Cook III',pos:'RB',team:'BUF',bye:7,adp:12.8,sd:2.9},
{id:14,name:'Chase Brown',pos:'RB',team:'CIN',bye:6,adp:13.2,sd:2.5},
{id:15,name:'Rashee Rice',pos:'WR',team:'KC',bye:5,adp:14.9,sd:2.1},
{id:16,name:'Ashton Jeanty',pos:'RB',team:'LV',bye:13,adp:16.7,sd:5.4},
{id:17,name:'Derrick Henry',pos:'RB',team:'BAL',bye:13,adp:17.5,sd:2.6},
{id:18,name:'A.J. Brown',pos:'WR',team:'NE',bye:11,adp:18.0,sd:3.2},
{id:19,name:'Saquon Barkley',pos:'RB',team:'PHI',bye:10,adp:19.3,sd:3.4},
{id:20,name:'Chris Olave',pos:'WR',team:'NO',bye:8,adp:19.4,sd:3.3},
{id:21,name:'Nico Collins',pos:'WR',team:'HOU',bye:8,adp:20.7,sd:2.9},
{id:22,name:'George Pickens',pos:'WR',team:'DAL',bye:14,adp:20.7,sd:3.1},
{id:23,name:'Kenneth Walker',pos:'RB',team:'KC',bye:5,adp:21.5,sd:4.1},
{id:24,name:'Omarion Hampton',pos:'RB',team:'LAC',bye:7,adp:23.2,sd:4.3},
{id:25,name:'Garrett Wilson',pos:'WR',team:'NYJ',bye:13,adp:25.5,sd:3.0},
{id:26,name:'Zay Flowers',pos:'WR',team:'BAL',bye:13,adp:26.1,sd:3.1},
{id:27,name:'Malik Nabers',pos:'WR',team:'NYG',bye:8,adp:27.3,sd:3.3},
{id:28,name:'Jeremiyah Love',pos:'RB',team:'ARI',bye:14,adp:27.5,sd:3.6},
{id:29,name:'Trey McBride',pos:'TE',team:'ARI',bye:14,adp:29.0,sd:4.6},
{id:30,name:'DeVonta Smith',pos:'WR',team:'PHI',bye:10,adp:29.8,sd:3.4},
{id:31,name:'Josh Jacobs',pos:'RB',team:'GB',bye:11,adp:30.6,sd:3.6},
{id:32,name:'Kyren Williams',pos:'RB',team:'LAR',bye:11,adp:31.6,sd:4.2},
{id:33,name:'Tetairoa McMillan',pos:'WR',team:'CAR',bye:5,adp:31.8,sd:3.8},
{id:34,name:'Josh Allen',pos:'QB',team:'BUF',bye:7,adp:34.0,sd:9.0},
{id:35,name:'Emeka Egbuka',pos:'WR',team:'TB',bye:10,adp:34.7,sd:4.0},
{id:36,name:'Brock Bowers',pos:'TE',team:'LV',bye:13,adp:35.3,sd:7.3},
{id:37,name:'Breece Hall',pos:'RB',team:'NYJ',bye:13,adp:35.6,sd:4.5},
{id:38,name:'Javonte Williams',pos:'RB',team:'DAL',bye:14,adp:36.4,sd:4.6},
{id:39,name:'Tee Higgins',pos:'WR',team:'CIN',bye:6,adp:37.1,sd:4.9},
{id:40,name:'Cam Skattebo',pos:'RB',team:'NYG',bye:8,adp:37.5,sd:5.0},
{id:41,name:'Ladd McConkey',pos:'WR',team:'LAC',bye:7,adp:37.9,sd:4.4},
{id:42,name:'Travis Etienne Jr.',pos:'RB',team:'NO',bye:8,adp:38.3,sd:4.9},
{id:43,name:'Davante Adams',pos:'WR',team:'LAR',bye:11,adp:42.1,sd:4.4},
{id:44,name:'Jameson Williams',pos:'WR',team:'DET',bye:6,adp:44.4,sd:4.7},
{id:45,name:'Bucky Irving',pos:'RB',team:'TB',bye:10,adp:44.7,sd:4.3},
{id:46,name:'D\'Andre Swift',pos:'RB',team:'CHI',bye:10,adp:45.7,sd:4.3},
{id:47,name:'Jaylen Waddle',pos:'WR',team:'DEN',bye:10,adp:45.9,sd:5.3},
{id:48,name:'Terry McLaurin',pos:'WR',team:'WAS',bye:7,adp:47.1,sd:4.8},
{id:49,name:'DJ Moore',pos:'WR',team:'BUF',bye:7,adp:48.2,sd:6.3},
{id:50,name:'Quinshon Judkins',pos:'RB',team:'CLE',bye:11,adp:50.4,sd:5.0},
{id:51,name:'Drake Maye',pos:'QB',team:'NE',bye:11,adp:51.7,sd:7.8},
{id:52,name:'Bhayshul Tuten',pos:'RB',team:'JAX',bye:7,adp:52.1,sd:5.3},
{id:53,name:'Rome Odunze',pos:'WR',team:'CHI',bye:10,adp:53.3,sd:5.9},
{id:54,name:'Mike Evans',pos:'WR',team:'SF',bye:8,adp:54.7,sd:6.3},
{id:55,name:'Lamar Jackson',pos:'QB',team:'BAL',bye:13,adp:56.6,sd:7.0},
{id:56,name:'Colston Loveland',pos:'TE',team:'CHI',bye:10,adp:56.9,sd:9.0},
{id:57,name:'Luther Burden III',pos:'WR',team:'CHI',bye:10,adp:57.5,sd:7.6},
{id:58,name:'Joe Burrow',pos:'QB',team:'CIN',bye:6,adp:57.7,sd:7.6},
{id:59,name:'David Montgomery',pos:'RB',team:'HOU',bye:8,adp:58.2,sd:6.2},
{id:60,name:'Jaylen Warren',pos:'RB',team:'PIT',bye:9,adp:58.4,sd:5.9},
{id:61,name:'Christian Watson',pos:'WR',team:'GB',bye:11,adp:58.9,sd:6.5},
{id:62,name:'Courtland Sutton',pos:'WR',team:'DEN',bye:10,adp:59.7,sd:6.4},
{id:63,name:'TreVeyon Henderson',pos:'RB',team:'NE',bye:11,adp:62.1,sd:6.7},
{id:64,name:'DK Metcalf',pos:'WR',team:'PIT',bye:9,adp:64.5,sd:6.9},
{id:65,name:'Parker Washington',pos:'WR',team:'JAX',bye:7,adp:64.8,sd:7.4},
{id:66,name:'Rhamondre Stevenson',pos:'RB',team:'NE',bye:11,adp:65.1,sd:6.9},
{id:67,name:'Dak Prescott',pos:'QB',team:'DAL',bye:14,adp:65.3,sd:8.5},
{id:68,name:'Marvin Harrison Jr.',pos:'WR',team:'ARI',bye:14,adp:65.4,sd:7.5},
{id:69,name:'Tyler Warren',pos:'TE',team:'IND',bye:13,adp:65.5,sd:9.2},
{id:70,name:'Alec Pierce',pos:'WR',team:'IND',bye:13,adp:67.8,sd:7.8},
{id:71,name:'Tony Pollard',pos:'RB',team:'TEN',bye:9,adp:69.7,sd:6.5},
{id:72,name:'Jayden Daniels',pos:'QB',team:'WAS',bye:7,adp:72.2,sd:11.4},
{id:73,name:'Brian Thomas Jr.',pos:'WR',team:'JAX',bye:7,adp:72.7,sd:7.5},
{id:74,name:'Rico Dowdle',pos:'RB',team:'PIT',bye:9,adp:74.3,sd:7.3},
{id:75,name:'Michael Pittman Jr.',pos:'WR',team:'PIT',bye:9,adp:74.9,sd:7.8},
{id:76,name:'Kyle Pitts Sr.',pos:'TE',team:'ATL',bye:11,adp:75.1,sd:9.6},
{id:77,name:'Jadarian Price',pos:'RB',team:'SEA',bye:11,adp:75.6,sd:10.3},
{id:78,name:'Michael Wilson',pos:'WR',team:'ARI',bye:14,adp:76.2,sd:7.9},
{id:79,name:'Matthew Stafford',pos:'QB',team:'LAR',bye:11,adp:77.4,sd:11.1},
{id:80,name:'Jalen Hurts',pos:'QB',team:'PHI',bye:10,adp:78.0,sd:10.7},
{id:81,name:'Carnell Tate',pos:'WR',team:'TEN',bye:9,adp:78.3,sd:9.1},
{id:82,name:'Harold Fannin Jr.',pos:'TE',team:'CLE',bye:11,adp:78.4,sd:7.4},
{id:83,name:'Chris Godwin Jr.',pos:'WR',team:'TB',bye:10,adp:79.9,sd:8.2},
{id:84,name:'Chuba Hubbard',pos:'RB',team:'CAR',bye:5,adp:79.9,sd:9.7},
{id:85,name:'Seattle D/ST',pos:'DST',team:'SEA',bye:11,adp:82.6,sd:8.6},
{id:86,name:'Wan\'Dale Robinson',pos:'WR',team:'TEN',bye:9,adp:86.2,sd:8.3},
{id:87,name:'Josh Downs',pos:'WR',team:'IND',bye:13,adp:86.8,sd:8.2},
{id:88,name:'Jakobi Meyers',pos:'WR',team:'JAX',bye:7,adp:87.0,sd:7.7},
{id:89,name:'J.K. Dobbins',pos:'RB',team:'DEN',bye:10,adp:87.2,sd:9.9},
{id:90,name:'Denver D/ST',pos:'DST',team:'DEN',bye:10,adp:87.7,sd:7.2},
{id:91,name:'Brock Purdy',pos:'QB',team:'SF',bye:8,adp:87.7,sd:11.6},
{id:92,name:'RJ Harvey',pos:'RB',team:'DEN',bye:10,adp:89.7,sd:12.5},
{id:93,name:'Caleb Williams',pos:'QB',team:'CHI',bye:10,adp:90.8,sd:11.9},
{id:94,name:'Trevor Lawrence',pos:'QB',team:'JAX',bye:7,adp:91.0,sd:12.2},
{id:95,name:'Stefon Diggs',pos:'WR',team:'WAS',bye:7,adp:91.4,sd:9.0},
{id:96,name:'Kenny Gainwell',pos:'RB',team:'TB',bye:10,adp:91.6,sd:10.3},
{id:97,name:'Jayden Reed',pos:'WR',team:'GB',bye:11,adp:95.2,sd:8.3},
{id:98,name:'Jonathon Brooks',pos:'RB',team:'CAR',bye:5,adp:95.5,sd:13.7},
{id:99,name:'Quentin Johnston',pos:'WR',team:'LAC',bye:7,adp:97.0,sd:8.9},
{id:100,name:'Jordan Addison',pos:'WR',team:'MIN',bye:6,adp:97.3,sd:8.5},
{id:101,name:'Houston D/ST',pos:'DST',team:'HOU',bye:8,adp:98.4,sd:9.1},
{id:102,name:'Dallas Goedert',pos:'TE',team:'PHI',bye:10,adp:100.0,sd:20.4},
{id:103,name:'Jared Goff',pos:'QB',team:'DET',bye:6,adp:100.3,sd:13.0},
{id:104,name:'Tucker Kraft',pos:'TE',team:'GB',bye:11,adp:100.4,sd:19.7},
{id:105,name:'Khalil Shakir',pos:'WR',team:'BUF',bye:7,adp:102.3,sd:8.5},
{id:106,name:'Patrick Mahomes',pos:'QB',team:'KC',bye:5,adp:102.5,sd:12.6},
{id:107,name:'Aaron Jones Sr.',pos:'RB',team:'MIN',bye:6,adp:103.1,sd:11.7},
{id:108,name:'Travis Kelce',pos:'TE',team:'KC',bye:5,adp:104.1,sd:20.8},
{id:109,name:'Justin Herbert',pos:'QB',team:'LAC',bye:7,adp:105.2,sd:14.2},
{id:110,name:'Xavier Worthy',pos:'WR',team:'KC',bye:5,adp:105.5,sd:8.0},
{id:111,name:'Matthew Golden',pos:'WR',team:'GB',bye:11,adp:106.4,sd:8.7},
{id:112,name:'Deebo Samuel Sr.',pos:'WR',team:'SF',bye:8,adp:108.1,sd:10.5},
{id:113,name:'LA Rams D/ST',pos:'DST',team:'LAR',bye:11,adp:109.0,sd:11.1},
{id:114,name:'Kyle Monangai',pos:'RB',team:'CHI',bye:10,adp:109.1,sd:12.4},
{id:115,name:'Minnesota D/ST',pos:'DST',team:'MIN',bye:6,adp:109.6,sd:9.5},
{id:116,name:'Sam LaPorta',pos:'TE',team:'DET',bye:6,adp:111.6,sd:23.0},
{id:117,name:'Bo Nix',pos:'QB',team:'DEN',bye:10,adp:111.8,sd:13.1},
{id:118,name:'Rachaad White',pos:'RB',team:'WAS',bye:7,adp:112.2,sd:13.3},
{id:119,name:'Romeo Doubs',pos:'WR',team:'NE',bye:11,adp:114.3,sd:9.4},
{id:120,name:'George Kittle',pos:'TE',team:'SF',bye:8,adp:114.3,sd:20.3},
{id:121,name:'Jacory Croskey-Merritt',pos:'RB',team:'WAS',bye:7,adp:115.1,sd:14.6},
{id:122,name:'Makai Lemon',pos:'WR',team:'PHI',bye:10,adp:115.5,sd:10.6},
{id:123,name:'Jaxson Dart',pos:'QB',team:'NYG',bye:8,adp:116.7,sd:11.9},
{id:124,name:'Jordan Mason',pos:'RB',team:'MIN',bye:6,adp:117.0,sd:15.8},
{id:125,name:'KC Concepcion',pos:'WR',team:'CLE',bye:11,adp:121.2,sd:10.8},
{id:126,name:'Jalen Coker',pos:'WR',team:'CAR',bye:5,adp:121.9,sd:10.3},
{id:127,name:'Blake Corum',pos:'RB',team:'LAR',bye:11,adp:122.2,sd:16.5},
{id:128,name:'Jerry Jeudy',pos:'WR',team:'CLE',bye:11,adp:126.1,sd:11.4},
{id:129,name:'Mark Andrews',pos:'TE',team:'BAL',bye:13,adp:128.2,sd:18.5},
{id:130,name:'Rashid Shaheed',pos:'WR',team:'SEA',bye:11,adp:128.8,sd:11.4},
{id:131,name:'Brandon Aubrey',pos:'K',team:'DAL',bye:14,adp:128.9,sd:21.6},
{id:132,name:'Detroit D/ST',pos:'DST',team:'DET',bye:6,adp:128.9,sd:15.0},
{id:133,name:'Baker Mayfield',pos:'QB',team:'TB',bye:10,adp:129.6,sd:10.9},
{id:134,name:'Tyjae Spears',pos:'RB',team:'TEN',bye:9,adp:129.9,sd:11.5},
{id:135,name:'New England D/ST',pos:'DST',team:'NE',bye:11,adp:130.0,sd:15.4},
{id:136,name:'Jayden Higgins',pos:'WR',team:'HOU',bye:8,adp:131.0,sd:8.6},
{id:137,name:'Jake Ferguson',pos:'TE',team:'DAL',bye:14,adp:131.7,sd:17.2},
{id:138,name:'Tre Tucker',pos:'WR',team:'LV',bye:13,adp:131.9,sd:8.8},
{id:139,name:'Keenan Allen',pos:'WR',team:'IND',bye:13,adp:132.0,sd:12.3},
{id:140,name:'Pittsburgh D/ST',pos:'DST',team:'PIT',bye:9,adp:132.6,sd:14.9},
{id:141,name:'San Francisco D/ST',pos:'DST',team:'SF',bye:8,adp:133.0,sd:35.3},
{id:142,name:'Kyler Murray',pos:'QB',team:'MIN',bye:6,adp:133.3,sd:12.3},
{id:143,name:'Zach Charbonnet',pos:'RB',team:'SEA',bye:11,adp:133.7,sd:16.1},
{id:144,name:'Tyler Shough',pos:'QB',team:'NO',bye:8,adp:134.6,sd:12.8},
{id:145,name:'De\'Zhaun Stribling',pos:'WR',team:'SF',bye:8,adp:134.6,sd:16.9},
{id:146,name:'Jalen McMillan',pos:'WR',team:'TB',bye:10,adp:135.1,sd:12.0},
{id:147,name:'Isaiah Likely',pos:'TE',team:'NYG',bye:8,adp:136.5,sd:18.1},
{id:148,name:'Jason Myers',pos:'K',team:'SEA',bye:11,adp:137.4,sd:19.4},
{id:149,name:'Denzel Boston',pos:'WR',team:'CLE',bye:11,adp:138.3,sd:14.9},
{id:150,name:'Ka\'imi Fairbairn',pos:'K',team:'HOU',bye:8,adp:139.1,sd:20.1},
{id:151,name:'Philadelphia D/ST',pos:'DST',team:'PHI',bye:10,adp:139.6,sd:16.2},
{id:152,name:'LA Chargers D/ST',pos:'DST',team:'LAC',bye:7,adp:139.9,sd:14.5},
{id:153,name:'Woody Marks',pos:'RB',team:'HOU',bye:8,adp:139.9,sd:15.9},
{id:154,name:'Cameron Dicker',pos:'K',team:'LAC',bye:7,adp:142.5,sd:18.9},
{id:155,name:'Sam Darnold',pos:'QB',team:'SEA',bye:11,adp:142.6,sd:14.0},
{id:156,name:'Calvin Ridley',pos:'WR',team:'TEN',bye:9,adp:143.5,sd:11.4},
{id:157,name:'Juwan Johnson',pos:'TE',team:'NO',bye:8,adp:145.1,sd:19.8},
{id:158,name:'Alvin Kamara',pos:'RB',team:'NO',bye:8,adp:146.1,sd:22.5},
{id:159,name:'Mike Washington Jr.',pos:'RB',team:'LV',bye:13,adp:146.7,sd:26.2},
{id:160,name:'Jordan Love',pos:'QB',team:'GB',bye:11,adp:147.5,sd:13.0},
{id:161,name:'Jake Bates',pos:'K',team:'DET',bye:6,adp:147.5,sd:18.5},
{id:162,name:'Harrison Mevis',pos:'K',team:'LAR',bye:11,adp:147.8,sd:17.1},
{id:163,name:'Jauan Jennings',pos:'WR',team:'MIN',bye:6,adp:148.1,sd:10.3},
{id:164,name:'Jordan James',pos:'RB',team:'SF',bye:8,adp:148.3,sd:26.1},
{id:165,name:'Cyrus Allen',pos:'WR',team:'KC',bye:5,adp:148.8,sd:23.9},
{id:166,name:'Dalton Kincaid',pos:'TE',team:'BUF',bye:7,adp:148.9,sd:21.0},
{id:167,name:'Emari Demercado',pos:'RB',team:'KC',bye:5,adp:149.0,sd:14.1},
{id:168,name:'Malik Washington',pos:'WR',team:'MIA',bye:6,adp:149.1,sd:13.0},
{id:169,name:'Jordyn Tyson',pos:'WR',team:'NO',bye:8,adp:151.1,sd:18.7},
{id:170,name:'Jonah Coleman',pos:'RB',team:'DEN',bye:10,adp:151.1,sd:18.8},
{id:171,name:'Cooper Kupp',pos:'WR',team:'SEA',bye:11,adp:151.3,sd:19.0},
{id:172,name:'Isiah Pacheco',pos:'RB',team:'DET',bye:6,adp:152.2,sd:19.9},
{id:173,name:'Rashod Bateman',pos:'WR',team:'BAL',bye:13,adp:152.7,sd:14.9},
{id:174,name:'Cam Little',pos:'K',team:'JAX',bye:7,adp:153.0,sd:17.5},
{id:175,name:'Joey Slye',pos:'K',team:'TEN',bye:9,adp:153.2,sd:11.5},
{id:176,name:'Chase McLaughlin',pos:'K',team:'TB',bye:10,adp:153.2,sd:18.0},
{id:177,name:'Tyler Bass',pos:'K',team:'BUF',bye:7,adp:153.5,sd:26.5},
{id:178,name:'Tyler Allgeier',pos:'RB',team:'ARI',bye:14,adp:153.6,sd:20.6},
{id:179,name:'MarShawn Lloyd',pos:'RB',team:'GB',bye:11,adp:153.8,sd:20.7},
{id:180,name:'Jalen Nailor',pos:'WR',team:'LV',bye:13,adp:153.9,sd:16.3},
{id:181,name:'Hunter Henry',pos:'TE',team:'NE',bye:11,adp:153.9,sd:24.0},
{id:182,name:'David Njoku',pos:'TE',team:'LAC',bye:7,adp:154.0,sd:20.3},
{id:183,name:'Tyrone Tracy Jr.',pos:'RB',team:'NYG',bye:8,adp:155.6,sd:17.7},
{id:184,name:'Tampa Bay D/ST',pos:'DST',team:'TB',bye:10,adp:155.8,sd:32.9},
{id:185,name:'Tyler Loop',pos:'K',team:'BAL',bye:13,adp:155.9,sd:15.2},
{id:186,name:'Green Bay D/ST',pos:'DST',team:'GB',bye:11,adp:156.5,sd:15.2},
{id:187,name:'Tank Dell',pos:'WR',team:'HOU',bye:8,adp:156.5,sd:15.7},
{id:188,name:'Pat Bryant',pos:'WR',team:'DEN',bye:10,adp:156.6,sd:25.6},
{id:189,name:'AJ Barner',pos:'TE',team:'SEA',bye:11,adp:156.7,sd:28.1},
{id:190,name:'Jacksonville D/ST',pos:'DST',team:'JAX',bye:7,adp:157.2,sd:14.3},
{id:191,name:'Dylan Sampson',pos:'RB',team:'CLE',bye:11,adp:157.5,sd:14.0},
{id:192,name:'Keaton Mitchell',pos:'RB',team:'LAC',bye:7,adp:157.5,sd:21.3},
{id:193,name:'C.J. Stroud',pos:'QB',team:'HOU',bye:8,adp:157.7,sd:15.3},
{id:194,name:'Chig Okonkwo',pos:'TE',team:'WAS',bye:7,adp:158.0,sd:18.0},
{id:195,name:'Chris Rodriguez Jr.',pos:'RB',team:'JAX',bye:7,adp:158.1,sd:18.2},
{id:196,name:'Ja\'Kobi Lane',pos:'WR',team:'BAL',bye:13,adp:158.3,sd:19.6},
{id:197,name:'Cleveland D/ST',pos:'DST',team:'CLE',bye:11,adp:158.3,sd:14.7},
{id:198,name:'Emmett Johnson',pos:'RB',team:'KC',bye:5,adp:159.4,sd:14.0},
{id:199,name:'Braelon Allen',pos:'RB',team:'NYJ',bye:13,adp:159.5,sd:21.7},
{id:200,name:'Chris Boswell',pos:'K',team:'PIT',bye:9,adp:159.5,sd:20.3},
{id:201,name:'Trey Smack',pos:'K',team:'GB',bye:11,adp:160.2,sd:22.4},
{id:202,name:'Harrison Butker',pos:'K',team:'KC',bye:5,adp:160.4,sd:20.3},
{id:203,name:'Daniel Jones',pos:'QB',team:'IND',bye:13,adp:160.6,sd:12.2},
{id:204,name:'Terrance Ferguson',pos:'TE',team:'LAR',bye:11,adp:160.6,sd:16.2},
{id:205,name:'Brenton Strange',pos:'TE',team:'JAX',bye:7,adp:160.7,sd:20.1},
{id:206,name:'Kenyon Sadiq',pos:'TE',team:'NYJ',bye:13,adp:160.7,sd:15.7},
{id:207,name:'Malachi Fields',pos:'WR',team:'NYG',bye:8,adp:160.7,sd:33.7},
{id:208,name:'Kaelon Black',pos:'RB',team:'SF',bye:8,adp:160.9,sd:23.6},
{id:209,name:'Wil Lutz',pos:'K',team:'DEN',bye:10,adp:160.9,sd:15.8},
{id:210,name:'Buffalo D/ST',pos:'DST',team:'BUF',bye:7,adp:161.0,sd:15.7},
{id:211,name:'Malik Davis',pos:'RB',team:'DAL',bye:14,adp:161.3,sd:27.5},
{id:212,name:'Blake Grupe',pos:'K',team:'IND',bye:13,adp:161.5,sd:16.4},
{id:213,name:'Tank Bigsby',pos:'RB',team:'PHI',bye:10,adp:161.6,sd:21.6},
{id:214,name:'Will Reichard',pos:'K',team:'MIN',bye:6,adp:161.9,sd:16.6},
{id:215,name:'Omar Cooper Jr.',pos:'WR',team:'NYJ',bye:13,adp:162.3,sd:35.5},
{id:216,name:'Bryce Young',pos:'QB',team:'CAR',bye:5,adp:162.4,sd:19.3},
{id:217,name:'Dalton Schultz',pos:'TE',team:'HOU',bye:8,adp:162.7,sd:20.1},
{id:218,name:'Jaylin Noel',pos:'WR',team:'HOU',bye:8,adp:162.8,sd:13.7},
{id:219,name:'Ray Davis',pos:'RB',team:'BUF',bye:7,adp:162.8,sd:26.1},
{id:220,name:'Malik Willis',pos:'QB',team:'MIA',bye:6,adp:163.2,sd:13.8},
{id:221,name:'Devaughn Vele',pos:'WR',team:'NO',bye:8,adp:163.3,sd:17.1},
{id:222,name:'Najee Harris',pos:'RB',team:'NYG',bye:8,adp:163.3,sd:15.8},
{id:223,name:'Ryan Flournoy',pos:'WR',team:'DAL',bye:14,adp:163.6,sd:28.3},
{id:224,name:'Adonai Mitchell',pos:'WR',team:'NYJ',bye:13,adp:163.7,sd:14.5},
{id:225,name:'T.J. Hockenson',pos:'TE',team:'MIN',bye:6,adp:163.9,sd:23.4},
{id:226,name:'Kimani Vidal',pos:'RB',team:'LAC',bye:7,adp:164.0,sd:14.8},
{id:227,name:'Eddy Pineiro',pos:'K',team:'SF',bye:8,adp:164.2,sd:19.4},
{id:228,name:'Isaac TeSlaa',pos:'WR',team:'DET',bye:6,adp:164.9,sd:39.7},
{id:229,name:'Baltimore D/ST',pos:'DST',team:'BAL',bye:13,adp:165.6,sd:20.0},
{id:230,name:'Jaydon Blue',pos:'RB',team:'DAL',bye:14,adp:165.6,sd:14.2},
{id:231,name:'Oronde Gadsden',pos:'TE',team:'LAC',bye:7,adp:165.7,sd:17.6},
{id:232,name:'Kayshon Boutte',pos:'WR',team:'HOU',bye:8,adp:166.0,sd:18.9},
{id:233,name:'Aaron Rodgers',pos:'QB',team:'PIT',bye:9,adp:166.1,sd:32.6},
{id:234,name:'Justice Hill',pos:'RB',team:'BAL',bye:13,adp:166.1,sd:12.5},
{id:235,name:'Dallas D/ST',pos:'DST',team:'DAL',bye:14,adp:166.2,sd:22.9},
{id:236,name:'NY Giants D/ST',pos:'DST',team:'NYG',bye:8,adp:166.2,sd:18.1},
{id:237,name:'Brian Robinson',pos:'RB',team:'ATL',bye:11,adp:166.5,sd:24.3},
{id:238,name:'Dontayvion Wicks',pos:'WR',team:'PHI',bye:10,adp:166.5,sd:18.9},
{id:239,name:'Cairo Santos',pos:'K',team:'CHI',bye:10,adp:166.9,sd:19.0},
{id:240,name:'Bub Means',pos:'WR',team:'NO',bye:8,adp:167.8,sd:32.8},
{id:241,name:'Tre\' Harris',pos:'WR',team:'LAC',bye:7,adp:168.2,sd:26.2},
{id:242,name:'Travis Hunter',pos:'WR',team:'JAX',bye:7,adp:168.6,sd:12.2},
{id:243,name:'James Conner',pos:'RB',team:'ARI',bye:14,adp:168.9,sd:15.1},
{id:244,name:'Cam Ward',pos:'QB',team:'TEN',bye:9,adp:169.0,sd:13.5},
{id:245,name:'Germie Bernard',pos:'WR',team:'PIT',bye:9,adp:169.4,sd:9.5},
{id:246,name:'Evan McPherson',pos:'K',team:'CIN',bye:6,adp:170.4,sd:16.3},
{id:247,name:'Caleb Douglas',pos:'WR',team:'MIA',bye:6,adp:170.5,sd:18.6},
{id:248,name:'Tennessee D/ST',pos:'DST',team:'TEN',bye:9,adp:170.6,sd:11.6},
{id:249,name:'Andy Borregales',pos:'K',team:'NE',bye:11,adp:170.7,sd:15.6},
{id:250,name:'Nick Folk',pos:'K',team:'ATL',bye:11,adp:171.5,sd:30.9},
{id:251,name:'New Orleans D/ST',pos:'DST',team:'NO',bye:8,adp:171.6,sd:15.5},
{id:252,name:'Jacoby Brissett',pos:'QB',team:'ARI',bye:14,adp:172.1,sd:14.7},
{id:253,name:'Kaden Wetjen',pos:'WR',team:'PIT',bye:9,adp:172.5,sd:4.2},
{id:254,name:'Xavier Hutchinson',pos:'WR',team:'HOU',bye:8,adp:172.5,sd:23.9},
{id:255,name:'Chicago D/ST',pos:'DST',team:'CHI',bye:10,adp:173.7,sd:20.8},
{id:256,name:'Fernando Mendoza',pos:'QB',team:'LV',bye:13,adp:173.8,sd:23.1},
{id:257,name:'Troy Franklin',pos:'WR',team:'DEN',bye:10,adp:177.2,sd:19.6},
{id:258,name:'Darius Slayton',pos:'WR',team:'NYG',bye:8,adp:177.8,sd:11.1},
{id:259,name:'Atlanta D/ST',pos:'DST',team:'ATL',bye:11,adp:179.0,sd:21.4},
{id:260,name:'Xavier Legette',pos:'WR',team:'CAR',bye:5,adp:179.0,sd:17.8},
{id:261,name:'Geno Smith',pos:'QB',team:'NYJ',bye:13,adp:180.2,sd:9.9},
{id:262,name:'Greg Dulcich',pos:'TE',team:'MIA',bye:6,adp:182.3,sd:23.8},
{id:263,name:'Pat Freiermuth',pos:'TE',team:'PIT',bye:9,adp:183.0,sd:31.7},
{id:264,name:'Ty Johnson',pos:'RB',team:'BUF',bye:7,adp:183.8,sd:24.4},
{id:265,name:'Cincinnati D/ST',pos:'DST',team:'CIN',bye:6,adp:183.9,sd:33.3},
{id:266,name:'Washington D/ST',pos:'DST',team:'WAS',bye:7,adp:192.8,sd:26.3}
];
// ===================== DRAFT ENGINE =====================

const ARCHETYPES = {
  balanced: {
    label: "Best Player Available",
    blurb: "Drafts closest to consensus ADP with only mild personality.",
    weights: (rnd) => ({ QB: 1, RB: 1, WR: 1, TE: 1 }),
    noise: 0.12, reachiness: 0.12, volBias: 0
  },
  zeroRB: {
    label: "Zero RB",
    blurb: "Hoards elite WR/TE early, punts the RB position until the middle rounds.",
    weights: (rnd) => rnd <= 3
      ? { QB: 0.65, RB: 0.32, WR: 1.6, TE: 1.15 }
      : rnd <= 8
        ? { QB: 0.9, RB: 1.35, WR: 1.05, TE: 1 }
        : { QB: 1, RB: 1.15, WR: 1, TE: 1 },
    noise: 0.16, reachiness: 0.2, volBias: 0.15
  },
  heroRB: {
    label: "Hero RB",
    blurb: "Locks in one workhorse RB round 1, then goes WR-heavy before circling back to RB.",
    weights: (rnd) => rnd === 1
      ? { QB: 0.55, RB: 2.2, WR: 0.7, TE: 0.75 }
      : rnd <= 4
        ? { QB: 0.75, RB: 0.5, WR: 1.5, TE: 1.05 }
        : rnd <= 9
          ? { QB: 0.95, RB: 1.35, WR: 1, TE: 1 }
          : { QB: 1, RB: 1, WR: 1, TE: 1 },
    noise: 0.14, reachiness: 0.15, volBias: 0
  },
  doubleHeroRB: {
    label: "Double Hero RB",
    blurb: "Takes two 'hero' RBs early to anchor the position, then leans all-in on WR.",
    weights: (rnd) => rnd <= 2
      ? { QB: 0.55, RB: 1.9, WR: 0.75, TE: 0.75 }
      : rnd <= 6
        ? { QB: 0.8, RB: 0.45, WR: 1.55, TE: 1 }
        : rnd <= 10
          ? { QB: 0.95, RB: 1.2, WR: 1.05, TE: 1 }
          : { QB: 1, RB: 1, WR: 1, TE: 1 },
    noise: 0.15, reachiness: 0.17, volBias: 0.05
  },
  robustRB: {
    label: "Robust RB",
    blurb: "Piles up three-plus RBs early for volume and injury insurance.",
    weights: (rnd) => rnd <= 3
      ? { QB: 0.6, RB: 1.85, WR: 0.72, TE: 0.85 }
      : rnd <= 8
        ? { QB: 0.95, RB: 1.05, WR: 1.15, TE: 1 }
        : { QB: 1, RB: 1, WR: 1, TE: 1 },
    noise: 0.13, reachiness: 0.14, volBias: -0.05
  },
  tePremium: {
    label: "TE Premium",
    blurb: "Pays up for an elite tight end early to lock in a weekly positional edge.",
    weights: (rnd) => rnd <= 3
      ? { QB: 0.75, RB: 1, WR: 0.95, TE: 1.95 }
      : { QB: 1, RB: 1, WR: 1, TE: 1.2 },
    noise: 0.13, reachiness: 0.16, volBias: 0
  },
  earlyQB: {
    label: "QB Anchor",
    blurb: "Values elite rushing/passing QBs enough to take one in rounds 2-4.",
    weights: (rnd) => (rnd >= 2 && rnd <= 4)
      ? { QB: 2.0, RB: 1, WR: 1, TE: 0.9 }
      : { QB: 0.85, RB: 1, WR: 1, TE: 1 },
    noise: 0.13, reachiness: 0.15, volBias: 0
  },
  lateQB: {
    label: "Streaming QB",
    blurb: "Refuses to draft a QB until the double-digit rounds, banking skill-position depth.",
    weights: (rnd) => rnd <= 9
      ? { QB: 0.15, RB: 1.1, WR: 1.1, TE: 1 }
      : { QB: 2.1, RB: 1, WR: 1, TE: 1 },
    noise: 0.13, reachiness: 0.13, volBias: 0
  },
  upsideHunter: {
    label: "Upside Hunter",
    blurb: "Chases ceiling and buzz over safety, willing to reach for boom-or-bust names.",
    weights: (rnd) => ({ QB: 1, RB: 1.05, WR: 1.05, TE: 1 }),
    noise: 0.3, reachiness: 0.42, volBias: 0.6
  },
  safeFloor: {
    label: "Safe & Steady",
    blurb: "Prizes proven, low-variance production and rarely deviates from the pack.",
    weights: (rnd) => ({ QB: 1, RB: 1, WR: 1, TE: 1 }),
    noise: 0.06, reachiness: 0.05, volBias: -0.55
  },
  contrarianValue: {
    label: "Value Hunter",
    blurb: "Tracks who has fallen past ADP and pounces on the best bargain on the board.",
    weights: (rnd) => ({ QB: 1, RB: 1, WR: 1, TE: 1 }),
    noise: 0.08, reachiness: 0.06, volBias: 0, valueBias: 1.7
  }
};

const ARCHETYPE_KEYS = Object.keys(ARCHETYPES);

function gaussianRandom(mean, stdev) {
  let u = 0, v = 0;
  while (u === 0) u = Math.random();
  while (v === 0) v = Math.random();
  const z = Math.sqrt(-2 * Math.log(u)) * Math.cos(2 * Math.PI * v);
  return mean + z * stdev;
}

function shuffle(arr) {
  const a = arr.slice();
  for (let i = a.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [a[i], a[j]] = [a[j], a[i]];
  }
  return a;
}

// Build snake draft order: returns array of length numTeams*totalRounds,
// each element = teamIndex (0-based) on the clock for that overall pick.
function buildDraftOrder(numTeams, totalRounds) {
  const order = [];
  for (let r = 1; r <= totalRounds; r++) {
    const roundOrder = [];
    for (let i = 0; i < numTeams; i++) roundOrder.push(i);
    if (r % 2 === 0) roundOrder.reverse();
    order.push(...roundOrder);
  }
  return order;
}

function makeEmptyRosterCounts() {
  return { QB: 0, RB: 0, WR: 0, TE: 0, DST: 0, K: 0, BENCH: 0, total: 0 };
}

// Compute need tier (0=must-start,1=flex,2=bench-soft,3=bench-hard,4=blocked) for a position
function needTier(counts, pos, config) {
  const req = config.roster;
  if (pos === 'DST' || pos === 'K') {
    const have = counts[pos];
    const need = req[pos] - have;
    if (need > 0) return 0;
    return 4; // no backup K/DST in redraft leagues
  }
  const have = counts[pos];
  const reqPos = req[pos];
  const starterNeed = reqPos - have;
  if (starterNeed > 0) return 0;

  if (pos === 'RB' || pos === 'WR' || pos === 'TE') {
    // flex pool: extra RB/WR/TE beyond their own starter reqs
    const extraRB = Math.max(0, counts.RB - req.RB);
    const extraWR = Math.max(0, counts.WR - req.WR);
    const extraTE = Math.max(0, counts.TE - req.TE);
    const flexFilled = Math.min(extraRB + extraWR + extraTE, req.FLEX);
    if (flexFilled < req.FLEX) return 1;
  }

  const softCaps = { RB: req.RB + req.FLEX + 3, WR: req.WR + req.FLEX + 4, TE: req.TE + 2, QB: req.QB };
  const hardCaps = { RB: req.RB + req.FLEX + 6, WR: req.WR + req.FLEX + 7, TE: req.TE + 3, QB: req.QB + 1 };
  if (have < softCaps[pos]) return 2;
  if (have < hardCaps[pos]) return 3;
  return 4;
}

const TIER_MULT = { 0: 1.7, 1: 1.25, 2: 1.0, 3: 0.55, 4: -1 }; // -1 => blocked

function unfilledRequiredCount(counts, config) {
  const req = config.roster;
  let n = 0;
  n += Math.max(0, req.QB - counts.QB);
  n += Math.max(0, req.RB - counts.RB);
  n += Math.max(0, req.WR - counts.WR);
  n += Math.max(0, req.TE - counts.TE);
  const extraRB = Math.max(0, counts.RB - req.RB);
  const extraWR = Math.max(0, counts.WR - req.WR);
  const extraTE = Math.max(0, counts.TE - req.TE);
  const flexFilled = Math.min(extraRB + extraWR + extraTE, req.FLEX);
  n += Math.max(0, req.FLEX - flexFilled);
  n += Math.max(0, req.DST - counts.DST);
  n += Math.max(0, req.K - counts.K);
  return n;
}

function runMultiplier(pos, recentPicks) {
  const count = recentPicks.filter(p => p === pos).length;
  if (count >= 3) return 1.25;
  if (count === 2) return 1.1;
  return 1.0;
}

function scorePlayer(player, counts, config, round, totalRounds, pickNum, archetype, recentPicks, byeCounts, emergencyMode, emergencyPositions) {
  if (player.pos === 'DST' || player.pos === 'K') {
    const lastGate = totalRounds - 2; // last 3 rounds only
    if (round < lastGate) return -Infinity;
  }
  const tier = needTier(counts, player.pos, config);
  if (tier === 4) return -Infinity;

  if (emergencyMode) {
    if (!emergencyPositions.has(player.pos)) return -Infinity;
    // in emergency mode just take the best remaining value at a needed position
    return 1000 / (player.adp + 4);
  }

  const w = archetype.weights(round, totalRounds);
  let posMult = (w[player.pos] ?? 1) * TIER_MULT[tier];

  const volNorm = Math.min(player.sd / 20, 1.5);
  posMult *= (1 + archetype.volBias * volNorm * 0.6);

  if (archetype.valueBias) {
    const fallAmount = Math.max(0, pickNum - player.adp);
    posMult *= (1 + Math.min(fallAmount / 15, 1) * (archetype.valueBias - 1));
  }

  posMult *= runMultiplier(player.pos, recentPicks);

  if (round >= 4 && byeCounts[player.bye] >= 2) posMult *= 0.92;

  const spread = archetype.reachiness * (2.5 + round * 1.6);
  const adjustedAdp = Math.max(0.3, player.adp - gaussianRandom(0, spread));
  const base = 1000 / (adjustedAdp + 4);

  return base * posMult;
}

function pickForTeam(team, availablePlayers, config, round, totalRounds, pickNum, recentPicks) {
  const counts = team.counts;
  const remainingPicks = totalRounds - team.picks.length;
  const needed = unfilledRequiredCount(counts, config);
  const emergencyMode = remainingPicks <= needed;

  let emergencyPositions = null;
  if (emergencyMode) {
    emergencyPositions = new Set();
    const req = config.roster;
    if (req.QB - counts.QB > 0) emergencyPositions.add('QB');
    if (req.RB - counts.RB > 0) emergencyPositions.add('RB');
    if (req.WR - counts.WR > 0) emergencyPositions.add('WR');
    if (req.TE - counts.TE > 0) emergencyPositions.add('TE');
    const extraRB = Math.max(0, counts.RB - req.RB);
    const extraWR = Math.max(0, counts.WR - req.WR);
    const extraTE = Math.max(0, counts.TE - req.TE);
    const flexFilled = Math.min(extraRB + extraWR + extraTE, req.FLEX);
    if (req.FLEX - flexFilled > 0) { emergencyPositions.add('RB'); emergencyPositions.add('WR'); emergencyPositions.add('TE'); }
    if (req.DST - counts.DST > 0) emergencyPositions.add('DST');
    if (req.K - counts.K > 0) emergencyPositions.add('K');
  }

  const archetype = ARCHETYPES[team.archetype];
  let best = null, bestScore = -Infinity;
  for (const p of availablePlayers) {
    const s = scorePlayer(p, counts, config, round, totalRounds, pickNum, archetype, recentPicks, team.byeCounts, emergencyMode, emergencyPositions);
    if (s > bestScore) { bestScore = s; best = p; }
  }
  return best;
}

function draftPlayerToTeam(team, player, round, pickNum) {
  team.picks.push({ player, round, pickNum });
  team.counts[player.pos] = (team.counts[player.pos] || 0) + 1;
  team.counts.total += 1;
  team.byeCounts[player.bye] = (team.byeCounts[player.bye] || 0) + 1;
}

// ===================== APP STATE & UI =====================

const NUM_TEAMS = 12;
const ROSTER_LIMITS = { QB:[1,3], RB:[1,5], WR:[1,5], TE:[1,3], FLEX:[0,4], DST:[0,2], K:[0,2], BENCH:[0,12] };

function defaultRoster(){ return { QB:1, RB:2, WR:2, TE:1, FLEX:1, DST:1, K:1, BENCH:6 }; }
function totalRoundsFor(r){ return r.QB+r.RB+r.WR+r.TE+r.FLEX+r.DST+r.K+r.BENCH; }

let setupState = { userSlot: 6, roster: defaultRoster() };
let S = null; // active draft state (null until draft starts)

function fmtAdp(adp){
  const rnd = Math.max(1, Math.ceil(adp / NUM_TEAMS));
  let pickInRound = Math.round(adp - (rnd - 1) * NUM_TEAMS);
  if (pickInRound < 1) pickInRound = 1;
  if (pickInRound > NUM_TEAMS) pickInRound = NUM_TEAMS;
  return rnd + '.' + String(pickInRound).padStart(2, '0');
}

// ---------------- Draft setup / lifecycle ----------------

function assignArchetypes(userSlotIdx){
  const pool = shuffle(ARCHETYPE_KEYS.concat(ARCHETYPE_KEYS));
  let pi = 0;
  const result = [];
  for (let i = 0; i < NUM_TEAMS; i++){
    if (i === userSlotIdx) result.push(null);
    else result.push(pool[pi++]);
  }
  return result;
}

function buildTeams(userSlotIdx, archList){
  const teams = [];
  for (let i = 0; i < NUM_TEAMS; i++){
    teams.push({
      slotIndex: i,
      isUser: i === userSlotIdx,
      archetype: archList[i],
      name: i === userSlotIdx ? 'You' : 'Team ' + (i + 1),
      picks: [],
      counts: makeEmptyRosterCounts(),
      byeCounts: {}
    });
  }
  return teams;
}

function startDraft(){
  const roster = setupState.roster;
  const totalRounds = totalRoundsFor(roster);
  const userSlotIdx = setupState.userSlot - 1;
  const archList = assignArchetypes(userSlotIdx);
  S = {
    screen: 'draft',
    roster, totalRounds, userSlotIdx,
    players: PLAYERS.map(p => ({ ...p, drafted: false })),
    teams: buildTeams(userSlotIdx, archList),
    order: buildDraftOrder(NUM_TEAMS, totalRounds),
    currentPickIdx: 0,
    recentPicks: [],
    log: [],
    activeTab: 'pool',
    poolSearch: '',
    poolPosFilter: 'ALL',
    autoTimer: null
  };
  scheduleAdvance();
}

function restartSameSettings(){ startDraft(); }

function currentRound(){ return Math.floor(S.currentPickIdx / NUM_TEAMS) + 1; }
function currentOverallPick(){ return S.currentPickIdx + 1; }
function isDraftComplete(){ return S.currentPickIdx >= S.order.length; }
function currentTeam(){ return S.teams[S.order[S.currentPickIdx]]; }

function scheduleAdvance(){
  if (isDraftComplete()){ S.screen = 'results'; render(); return; }
  const team = currentTeam();
  if (team.isUser){ render(); return; }
  render();
  S.autoTimer = setTimeout(() => { doCpuPick(); scheduleAdvance(); }, 340);
}

function doCpuPick(){
  const team = currentTeam();
  const round = currentRound();
  const pickNum = currentOverallPick();
  const available = S.players.filter(p => !p.drafted);
  let pick = pickForTeam(team, available, { roster: S.roster }, round, S.totalRounds, pickNum, S.recentPicks);
  if (!pick){
    available.sort((a, b) => a.adp - b.adp);
    pick = available[0];
  }
  commitPick(team, pick, round, pickNum);
}

function commitPick(team, player, round, pickNum){
  player.drafted = true;
  draftPlayerToTeam(team, player, round, pickNum);
  S.recentPicks.push(player.pos);
  if (S.recentPicks.length > 5) S.recentPicks.shift();
  const delta = pickNum - player.adp;
  const tag = delta < -9 ? 'reach' : delta > 14 ? 'value' : null;
  S.log.unshift({ pickNum, round, teamName: team.name, isUser: team.isUser, playerName: player.name, pos: player.pos, tag });
  S.currentPickIdx++;
}

function userDraftPlayer(playerId){
  const team = currentTeam();
  if (!team.isUser) return;
  const player = S.players.find(p => p.id === playerId && !p.drafted);
  if (!player) return;
  const round = currentRound(), pickNum = currentOverallPick();
  commitPick(team, player, round, pickNum);
  scheduleAdvance();
}

function skipToMyPick(){
  clearTimeout(S.autoTimer);
  while (!isDraftComplete() && !currentTeam().isUser) doCpuPick();
  if (isDraftComplete()) S.screen = 'results';
  render();
}

// ---------------- Rendering ----------------

function render(){
  if (!S){ renderSetup(); return; }
  if (S.screen === 'draft'){ renderDraftRoom(); return; }
  if (S.screen === 'results'){ renderResults(); return; }
}

function rosterFieldHtml(key, label, val){
  return `<div class="roster-field">
    <label>${label}</label>
    <div class="stepper">
      <button data-action="rosterdec" data-key="${key}">&minus;</button>
      <div class="val">${val}</div>
      <button data-action="rosterinc" data-key="${key}">+</button>
    </div>
  </div>`;
}

function renderSetup(){
  const app = document.getElementById('app');
  const r = setupState.roster;
  const total = totalRoundsFor(r);
  app.innerHTML = `
    <div class="masthead">
      <div class="eyebrow">12-Team &middot; Full PPR &middot; Snake Draft</div>
      <h1>Draft <span>Room</span></h1>
      <p>Practice against 11 CPU GMs who draft like real people &mdash; zero&nbsp;RB, hero&nbsp;RB, robust&nbsp;RB, TE&nbsp;premium, and the occasional reach.</p>
    </div>
    <div class="card">
      <h2>Your Draft Slot</h2>
      <p class="sub">Pick 1 goes first overall. The order snakes back around each round.</p>
      <div class="slot-grid">
        ${Array.from({ length: NUM_TEAMS }, (_, i) => i + 1).map(n =>
          `<button class="slot-btn ${setupState.userSlot === n ? 'selected' : ''}" data-action="slot" data-slot="${n}">${n}</button>`
        ).join('')}
      </div>
    </div>
    <div class="card">
      <h2>Roster Settings</h2>
      <p class="sub">Defaults to a standard 12-team build &mdash; adjust to match your actual league.</p>
      <div class="roster-grid">
        ${rosterFieldHtml('QB', 'QB', r.QB)}
        ${rosterFieldHtml('RB', 'RB', r.RB)}
        ${rosterFieldHtml('WR', 'WR', r.WR)}
        ${rosterFieldHtml('TE', 'TE', r.TE)}
        ${rosterFieldHtml('FLEX', 'FLEX', r.FLEX)}
        ${rosterFieldHtml('DST', 'DST', r.DST)}
        ${rosterFieldHtml('K', 'K', r.K)}
        ${rosterFieldHtml('BENCH', 'BN', r.BENCH)}
      </div>
      <div class="rounds-total">Total rounds: <b>${total}</b></div>
    </div>
    <button class="btn btn-primary btn-block" data-action="start" ${total > 22 ? 'disabled' : ''}>Start Mock Draft</button>
    ${total > 22 ? '<p class="sub" style="text-align:center;color:#F4615C;margin-top:8px;">Trim your roster &mdash; 22 rounds max.</p>' : ''}
  `;
}

function renderDraftHeaderHtml(complete, team, isUserTurn){
  const round = complete ? S.totalRounds : currentRound();
  const pickNum = complete ? S.order.length : currentOverallPick();
  const progressPct = Math.min(100, Math.round((S.currentPickIdx / S.order.length) * 100));
  const clockText = complete ? 'Draft Complete' : (isUserTurn ? 'Your Pick' : team.name + ' is on the clock');
  return `
  <div class="draft-header">
    <div class="dh-row">
      <div>
        <div class="dh-pick">Pick ${pickNum} of ${S.order.length} &middot; Round ${round}</div>
        <div class="dh-clock ${isUserTurn ? 'user-turn' : ''}">${clockText}</div>
      </div>
      ${(!complete && !isUserTurn) ? `<button class="btn btn-sm" data-action="skip">Skip to my pick &#9193;</button>` : ''}
    </div>
    <div class="dh-progress"><div class="dh-progress-bar" style="width:${progressPct}%"></div></div>
  </div>`;
}

function poolPlayers(){
  let list = S.players.filter(p => !p.drafted);
  if (S.poolPosFilter !== 'ALL') list = list.filter(p => p.pos === S.poolPosFilter);
  if (S.poolSearch.trim()){
    const q = S.poolSearch.trim().toLowerCase();
    list = list.filter(p => p.name.toLowerCase().includes(q));
  }
  list.sort((a, b) => a.adp - b.adp);
  return list;
}

function playerRowHtml(p, idx, isUserTurn){
  return `<div class="player-row">
    <div class="player-rank">${idx + 1}</div>
    <div class="player-info">
      <div class="player-name">${p.name}</div>
      <div class="player-meta"><span class="pos-badge pos-${p.pos}">${p.pos}</span> ${p.team} &middot; BYE ${p.bye}</div>
    </div>
    <div class="player-adp">${p.adp.toFixed(1)}<span class="r">${fmtAdp(p.adp)}</span></div>
    ${isUserTurn ? `<button class="draft-btn" data-action="draft" data-id="${p.id}">Draft</button>` : ''}
  </div>`;
}

function renderPoolTab(isUserTurn){
  const posFilters = ['ALL', 'QB', 'RB', 'WR', 'TE', 'DST', 'K'];
  const list = poolPlayers();
  const rows = list.slice(0, 150).map((p, i) => playerRowHtml(p, i, isUserTurn)).join('');
  return `
  <div class="card">
    <div class="pool-controls">
      <input class="search-input" id="poolSearch" placeholder="Search players..." value="${S.poolSearch.replace(/"/g, '&quot;')}" autocomplete="off">
    </div>
    <div class="pos-filter-row">
      ${posFilters.map(f => `<button class="pos-filter ${S.poolPosFilter === f ? 'active' : ''}" data-action="posfilter" data-pos="${f}">${f}</button>`).join('')}
    </div>
    <div class="player-list">${rows || '<div class="empty-note">No players match.</div>'}</div>
  </div>`;
}

function buildDisplaySlots(team, roster){
  const byPos = { QB: [], RB: [], WR: [], TE: [], DST: [], K: [] };
  const sortedPicks = team.picks.slice().sort((a, b) => a.round - b.round);
  for (const pk of sortedPicks) byPos[pk.player.pos].push(pk.player);

  const slots = [];
  for (let i = 0; i < roster.QB; i++) slots.push({ label: 'QB', player: byPos.QB.shift() || null });
  for (let i = 0; i < roster.RB; i++) slots.push({ label: 'RB', player: byPos.RB.shift() || null });
  for (let i = 0; i < roster.WR; i++) slots.push({ label: 'WR', player: byPos.WR.shift() || null });
  for (let i = 0; i < roster.TE; i++) slots.push({ label: 'TE', player: byPos.TE.shift() || null });
  for (let i = 0; i < roster.FLEX; i++){
    const cands = [];
    if (byPos.RB[0]) cands.push(['RB', byPos.RB[0]]);
    if (byPos.WR[0]) cands.push(['WR', byPos.WR[0]]);
    if (byPos.TE[0]) cands.push(['TE', byPos.TE[0]]);
    if (cands.length){
      cands.sort((a, b) => a[1].adp - b[1].adp);
      const pos = cands[0][0];
      slots.push({ label: 'FLEX', player: byPos[pos].shift() });
    } else slots.push({ label: 'FLEX', player: null });
  }
  for (let i = 0; i < roster.DST; i++) slots.push({ label: 'DST', player: byPos.DST.shift() || null });
  for (let i = 0; i < roster.K; i++) slots.push({ label: 'K', player: byPos.K.shift() || null });
  const leftover = [...byPos.QB, ...byPos.RB, ...byPos.WR, ...byPos.TE, ...byPos.DST, ...byPos.K];
  for (let i = 0; i < roster.BENCH; i++) slots.push({ label: 'BN', player: leftover[i] || null });
  return slots;
}

function renderTeamTab(){
  const userTeam = S.teams[S.userSlotIdx];
  const slots = buildDisplaySlots(userTeam, S.roster);
  const rows = slots.map(s => `
    <div class="roster-slot ${s.player ? '' : 'empty'}">
      <div class="slot-tag">${s.label}</div>
      ${s.player
        ? `<div class="slot-player">${s.player.name} <span class="pos-badge pos-${s.player.pos}">${s.player.pos}</span></div><div class="slot-meta">${s.player.team}&middot;BYE${s.player.bye}</div>`
        : `<div class="slot-player placeholder">Empty</div>`}
    </div>`).join('');
  return `<div class="card"><h2>Your Roster</h2><p class="sub">${userTeam.picks.length} of ${S.totalRounds} picks made.</p><div class="roster-list">${rows}</div></div>`;
}

function renderBoardTab(){
  let headHtml = `<div class="board-head-cell">RD</div>`;
  for (const t of S.teams) headHtml += `<div class="board-head-cell ${t.isUser ? 'user' : ''}">${t.isUser ? 'YOU' : 'T' + (t.slotIndex + 1)}</div>`;

  const complete = isDraftComplete();
  const onClockTeamIdx = complete ? -1 : currentTeam().slotIndex;
  const onClockRound = complete ? -1 : currentRound();

  let bodyHtml = '';
  for (let r = 1; r <= S.totalRounds; r++){
    bodyHtml += `<div class="board-row-num">${r}</div>`;
    for (let ti = 0; ti < NUM_TEAMS; ti++){
      const team = S.teams[ti];
      const pk = team.picks.find(p => p.round === r);
      const isOnClock = (r === onClockRound && ti === onClockTeamIdx);
      if (pk){
        bodyHtml += `<div class="board-cell" style="background:var(--pos-${pk.player.pos}-bg)">
          <div class="bc-name" style="color:var(--pos-${pk.player.pos})">${pk.player.name}</div>
          <div class="bc-pos">${pk.player.pos} &middot; ${pk.pickNum}</div>
        </div>`;
      } else {
        bodyHtml += `<div class="board-cell ${isOnClock ? 'onclock' : ''}"></div>`;
      }
    }
  }
  return `<div class="card"><h2>Draft Board</h2><p class="sub">Snake order &mdash; round 1 runs left to right, round 2 reverses, and so on.</p>
    <div class="board-scroll">
      <div class="board-grid" style="grid-template-columns:34px repeat(${NUM_TEAMS},1fr);">
        ${headHtml}${bodyHtml}
      </div>
    </div>
  </div>`;
}

function renderLogTab(){
  const rows = S.log.map(l => `
    <div class="log-entry">
      <div class="log-pick-num">${l.pickNum}</div>
      <div class="log-team ${l.isUser ? 'user' : ''}">${l.isUser ? 'YOU' : l.teamName}</div>
      <div class="log-player">${l.playerName} <span class="pos-badge pos-${l.pos}">${l.pos}</span></div>
      ${l.tag ? `<span class="log-tag ${l.tag}">${l.tag}</span>` : ''}
    </div>`).join('');
  return `<div class="card"><h2>Pick Log</h2><p class="sub">Most recent picks first.</p><div class="log-list">${rows || '<div class="empty-note">No picks yet.</div>'}</div></div>`;
}

function renderDraftRoom(){
  const app = document.getElementById('app');
  const complete = isDraftComplete();
  const team = complete ? null : currentTeam();
  const isUserTurn = !complete && team.isUser;

  let bodyHtml = '';
  if (S.activeTab === 'pool') bodyHtml = renderPoolTab(isUserTurn);
  else if (S.activeTab === 'team') bodyHtml = renderTeamTab();
  else if (S.activeTab === 'board') bodyHtml = renderBoardTab();
  else if (S.activeTab === 'log') bodyHtml = renderLogTab();

  app.innerHTML = `
    ${renderDraftHeaderHtml(complete, team, isUserTurn)}
    ${isUserTurn ? `<div class="onclock-banner"><div class="dot"></div><div>You're on the clock &mdash; <b>Round ${currentRound()}, Pick ${currentOverallPick()}</b></div></div>` : ''}
    <div class="tab-bar">
      <button class="tab-btn ${S.activeTab === 'pool' ? 'active' : ''}" data-action="tab" data-tab="pool">Pool</button>
      <button class="tab-btn ${S.activeTab === 'team' ? 'active' : ''}" data-action="tab" data-tab="team">My Team</button>
      <button class="tab-btn ${S.activeTab === 'board' ? 'active' : ''}" data-action="tab" data-tab="board">Board</button>
      <button class="tab-btn ${S.activeTab === 'log' ? 'active' : ''}" data-action="tab" data-tab="log">Log <span class="n">${S.log.length}</span></button>
    </div>
    ${bodyHtml}
  `;
}

function renderResults(){
  const app = document.getElementById('app');
  let html = `
    <div class="masthead">
      <div class="eyebrow">Draft Complete</div>
      <h1>Final <span>Results</span></h1>
      <p>Here's the full room &mdash; including the strategy each CPU GM was actually running.</p>
    </div>
  `;
  const ordered = [S.teams[S.userSlotIdx], ...S.teams.filter(t => !t.isUser)];
  for (const team of ordered){
    const archInfo = team.isUser ? null : ARCHETYPES[team.archetype];
    const sortedPicks = team.picks.slice().sort((a, b) => a.round - b.round);
    const chips = sortedPicks.map(pk => `<div class="rt-chip"><span class="pos-badge pos-${pk.player.pos}">${pk.player.pos}</span>${pk.player.name}</div>`).join('');
    html += `
    <div class="result-team-card ${team.isUser ? 'user' : ''}">
      <div class="rt-head">
        <div class="rt-name ${team.isUser ? 'user' : ''}">${team.isUser ? 'Your Team' : team.name}</div>
        ${archInfo ? `<div class="rt-arch">${archInfo.label}</div>` : ''}
      </div>
      <div class="rt-players">${chips}</div>
      ${archInfo ? `<div class="rt-blurb">${archInfo.blurb}</div>` : ''}
    </div>`;
  }
  html += `
    <div class="footer-actions">
      <button class="btn" data-action="restart-new">New Setup</button>
      <button class="btn btn-primary" data-action="restart-same">Redraft (Same Settings)</button>
    </div>
  `;
  app.innerHTML = html;
}

// ---------------- Events ----------------

function adjustRoster(key, delta){
  const [min, max] = ROSTER_LIMITS[key];
  const r = setupState.roster;
  const proposed = r[key] + delta;
  if (proposed < min || proposed > max) return;
  const proposedTotal = totalRoundsFor({ ...r, [key]: proposed });
  if (proposedTotal > 22) return;
  r[key] = proposed;
  renderSetup();
}

function onAppClick(e){
  const el = e.target.closest('[data-action]');
  if (!el) return;
  const action = el.dataset.action;
  if (action === 'slot'){ setupState.userSlot = parseInt(el.dataset.slot, 10); renderSetup(); }
  else if (action === 'rosterinc'){ adjustRoster(el.dataset.key, 1); }
  else if (action === 'rosterdec'){ adjustRoster(el.dataset.key, -1); }
  else if (action === 'start'){ startDraft(); }
  else if (action === 'tab'){ S.activeTab = el.dataset.tab; render(); }
  else if (action === 'posfilter'){ S.poolPosFilter = el.dataset.pos; render(); }
  else if (action === 'draft'){ userDraftPlayer(parseInt(el.dataset.id, 10)); }
  else if (action === 'skip'){ skipToMyPick(); }
  else if (action === 'restart-same'){ restartSameSettings(); }
  else if (action === 'restart-new'){ S = null; render(); }
}

function onAppInput(e){
  if (e.target.id === 'poolSearch'){
    S.poolSearch = e.target.value;
    render();
    const el = document.getElementById('poolSearch');
    if (el){ el.focus(); const v = el.value; el.setSelectionRange(v.length, v.length); }
  }
}

document.getElementById('app').addEventListener('click', onAppClick);
document.getElementById('app').addEventListener('input', onAppInput);

render();
</script></body></html>
