# 30-day-no-alkohol-start
Tantangan 30 hari tanpa alkohol dan hidup sehat
<!DOCTYPE html><html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Sobriety Tracker – Vibe Sosmed (30 Hari)</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&family=Poppins:wght@500;700&display=swap" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js"></script>
  <style>
    :root{
      --bg:#0f1222;           /* Night gradient base */
      --bg2:#181b31;          /* Card bg */
      --pri:#7c5cff;          /* Purple */
      --sec:#18d3be;          /* Teal */
      --acc:#ff6b6b;          /* Coral */
      --sun:#ffd166;          /* Yellow */
      --txt:#e9ebff;          /* Light text */
      --mut:#a9add6;          /* Muted text */
      --good:#7bed9f;         /* Success */
    }
    *{box-sizing:border-box}
    body{
      margin:0; background: radial-gradient(1200px 800px at 80% -10%, rgba(124,92,255,.25), transparent),
                         radial-gradient(900px 600px at -10% 10%, rgba(24,211,190,.18), transparent),
                         var(--bg);
      color:var(--txt); font-family: Inter, system-ui, -apple-system, Segoe UI, Roboto, Poppins, Arial, sans-serif;
    }
    header{
      position:sticky; top:0; z-index:10; backdrop-filter: blur(10px);
      background:linear-gradient(180deg, rgba(15,18,34,.8), rgba(15,18,34,.3));
      border-bottom:1px solid rgba(255,255,255,.06);
    }
    .wrap{max-width:980px; margin:0 auto; padding:16px 18px}
    .brand{
      display:flex; align-items:center; gap:12px;
    }
    .logo{
      width:40px; height:40px; border-radius:12px; background:
        conic-gradient(from 200deg, var(--pri), var(--sec), var(--sun), var(--pri));
      box-shadow:0 6px 20px rgba(124,92,255,.4);
    }
    .brand h1{font-family:Poppins, Inter; font-size:20px; margin:0}
    .tag{color:var(--mut); font-size:12px}
    .grid{
      display:grid; gap:16px; grid-template-columns: 1.1fr .9fr;
    }
    @media(max-width:960px){ .grid{grid-template-columns:1fr} }.card{
  background:linear-gradient(180deg, rgba(255,255,255,.04), rgba(255,255,255,.02));
  border:1px solid rgba(255,255,255,.06);
  border-radius:20px; padding:16px; box-shadow: 0 10px 30px rgba(0,0,0,.25);
}
.card h2{margin:0 0 8px; font-size:18px; font-family:Poppins}
.mut{color:var(--mut)}

.story-bar{
  display:flex; gap:10px; overflow:auto; padding:10px 2px 6px;
}
.story{
  flex:0 0 auto; width:52px; aspect-ratio:1; border-radius:16px; border:3px solid transparent;
  background: linear-gradient(135deg, rgba(124,92,255,.2), rgba(24,211,190,.2));
  position:relative; display:grid; place-items:center; color:#fff; font-weight:800;
}
.story[data-active="true"]{ border-color: var(--sun) }
.story small{ position:absolute; bottom:4px; font-size:9px; opacity:.8 }

.progress{
  height:14px; background:#202446; border-radius:999px; overflow:hidden; border:1px solid rgba(255,255,255,.06);
}
.progress > div{ height:100%; width:0%; background:linear-gradient(90deg, var(--pri), var(--sec), var(--sun)); transition: width .6s ease }

.flex{display:flex; align-items:center; gap:10px; flex-wrap:wrap}
.row{display:flex; align-items:center; gap:10px}
.col{display:flex; flex-direction:column; gap:8px}

.btn{
  border:none; padding:10px 14px; border-radius:14px; font-weight:700; color:#0f1222; cursor:pointer;
  background:linear-gradient(180deg, #fff, #eaeaff);
}
.btn.ghost{ background:transparent; color:var(--txt); border:1px solid rgba(255,255,255,.14) }
.btn.primary{ background:linear-gradient(90deg, var(--pri), var(--sec)); color:#fff }

.chip{
  padding:8px 10px; border-radius:999px; border:1px solid rgba(255,255,255,.12); background:rgba(255,255,255,.04);
  font-size:12px; color:var(--mut)
}

.toggle{
  appearance:none; width:58px; height:34px; border-radius:999px; position:relative; border:1px solid rgba(255,255,255,.16);
  background:#252a52; cursor:pointer; outline:none; transition:all .2s ease;
}
.toggle:checked{ background:linear-gradient(90deg, #58f29c, var(--sec)); }
.toggle:before{
  content:""; position:absolute; top:3px; left:3px; width:28px; height:28px; border-radius:50%;
  background:#fff; box-shadow:0 4px 12px rgba(0,0,0,.35); transition:left .2s ease;
}
.toggle:checked:before{ left:27px }

.emoji-picker{ display:flex; gap:8px; flex-wrap:wrap }
.emoji{
  font-size:20px; padding:8px 10px; border-radius:12px; border:1px solid rgba(255,255,255,.14);
  background:rgba(255,255,255,.06); cursor:pointer; user-select:none
}
.emoji.active{ outline:2px solid var(--pri) }

textarea{
  width:100%; min-height:96px; resize:vertical; padding:12px; border-radius:14px; border:1px solid rgba(255,255,255,.16);
  background:#151736; color:var(--txt); font-family:Inter; font-size:14px
}

.reacts{ display:flex; gap:8px }
.reacts button{
  font-size:18px; padding:8px 10px; border-radius:12px; border:1px solid rgba(255,255,255,.14);
  background:rgba(255,255,255,.06); cursor:pointer; color:#fff
}
.stat{ font-weight:700 }
.success{ color:var(--good) }

.footer{ color:var(--mut); font-size:12px; text-align:center; padding:24px 0 }
.sep{ height:1px; background:linear-gradient(90deg, transparent, rgba(255,255,255,.12), transparent); margin:12px 0 }

.time-input{ background:#151736; border:1px solid rgba(255,255,255,.16); color:var(--txt); padding:8px; border-radius:10px }

  </style>
</head>
<body>
  <header>
    <div class="wrap">
      <div class="brand">
        <div class="logo" aria-hidden="true"></div>
        <div>
          <h1>Sobriety Tracker – Vibe Sosmed</h1>
          <div class="tag">30 Hari fokus: bebas minum & bebas campur dextro 🚫🍶</div>
        </div>
      </div>
    </div>
  </header>  <main class="wrap" style="padding-top:8px">
    <div class="grid">
      <!-- LEFT: Tracker -->
      <section class="card" id="trackerCard">
        <div class="row" style="justify-content:space-between; align-items:flex-end">
          <div>
            <h2 id="titleDay">Day 1 – Keep Going 💪</h2>
            <div class="mut">Centang status, pilih mood, tulis catatan. Data aman disimpan di HP lo (local storage).</div>
          </div>
          <div class="row">
            <button class="btn ghost" id="resetBtn" title="Reset 30 hari">↺ Reset</button>
            <button class="btn" id="exportBtn">⬇️ Export</button>
            <label class="btn ghost" for="importInput">⬆️ Import</label>
            <input id="importInput" type="file" accept="application/json" style="display:none"/>
          </div>
        </div><div class="sep"></div>

    <div class="story-bar" id="dayScroller" aria-label="Pilih hari">
      <!-- Days rendered by JS -->
    </div>

    <div class="sep"></div>

    <div class="col">
      <div class="row" style="justify-content:space-between">
        <div class="row" style="gap:14px">
          <span class="chip">Status hari ini</span>
          <label class="row" style="gap:8px; align-items:center">
            <span class="mut">Bebas Minum</span>
            <input type="checkbox" id="freeToggle" class="toggle"/>
          </label>
        </div>
        <div class="reacts" role="group" aria-label="Reaksi cepat">
          <button type="button" data-react="👍">👍</button>
          <button type="button" data-react="🔥">🔥</button>
          <button type="button" data-react="🧘">🧘</button>
          <button type="button" data-react="😴">😴</button>
        </div>
      </div>

      <div class="col">
        <span class="chip">Mood hari ini</span>
        <div class="emoji-picker" id="emojiPicker" role="listbox" aria-label="Pilih emoji mood">
          <!-- Emojis by JS -->
        </div>
      </div>

      <div class="col">
        <span class="chip">Catatan</span>
        <textarea id="note" placeholder="Tulis singkat: pemicu, yang bikin berhasil, dll..."></textarea>
      </div>

      <div class="row" style="justify-content:flex-end">
        <button class="btn primary" id="saveBtn">Simpan</button>
      </div>
    </div>
  </section>

  <!-- RIGHT: Stats -->
  <aside class="card">
    <h2>Progress Kamu</h2>
    <div class="col" style="gap:12px">
      <div class="progress" aria-label="Progress total"><div id="progBar"></div></div>
      <div class="row" style="justify-content:space-between">
        <div><span class="mut">Total Bebas:</span> <span class="stat" id="totalFree">0/30</span></div>
        <div><span class="mut">Streak:</span> <span class="stat" id="streak">0🔥</span></div>
        <div><span class="mut">Target:</span> <span class="stat success">30/30</span></div>
      </div>
      <canvas id="chart" height="140" aria-label="Grafik progress" role="img"></canvas>
    </div>

    <div class="sep"></div>
    <h2>Pengingat Harian 🔔</h2>
    <div class="row" style="justify-content:space-between">
      <div class="row" style="gap:8px">
        <input type="time" id="remindTime" class="time-input" />
        <button class="btn" id="enableNotif">Aktifkan Notifikasi</button>
      </div>
      <small class="mut">Notifikasi berjalan kalau tab ini kebuka di HP kamu.</small>
    </div>
  </aside>
</div>

<div class="footer">Made with 💜 • Jaga diri, no campur-campur dextro 🚫</div>

  </main>  <script>
    // --- Data Model ---
    const LS_KEY = 'sobriety30_v1';
    const defaultData = {
      days: Array.from({length:30}, (_,i)=>({
        free:false,
        mood: '',
        note: '',
        reacts: {}
      })),
      currentDay: 1,
      remind: { time: '' }
    };

    const state = load();

    function load(){
      try{
        const raw = localStorage.getItem(LS_KEY);
        if(!raw) return structuredClone(defaultData);
        const parsed = JSON.parse(raw);
        // simple migration
        if(!parsed.days || parsed.days.length!==30) parsed.days = structuredClone(defaultData.days);
        return parsed;
      }catch(e){
        console.error(e); return structuredClone(defaultData);
      }
    }
    function save(){ localStorage.setItem(LS_KEY, JSON.stringify(state)); }

    // --- UI Elements ---
    const dayScroller = document.getElementById('dayScroller');
    const titleDay = document.getElementById('titleDay');
    const freeToggle = document.getElementById('freeToggle');
    const noteEl = document.getElementById('note');
    const emojiPicker = document.getElementById('emojiPicker');
    const saveBtn = document.getElementById('saveBtn');
    const totalFreeEl = document.getElementById('totalFree');
    const progBar = document.getElementById('progBar');
    const streakEl = document.getElementById('streak');
    const resetBtn = document.getElementById('resetBtn');
    const exportBtn = document.getElementById('exportBtn');
    const importInput = document.getElementById('importInput');
    const remindTime = document.getElementById('remindTime');
    const enableNotifBtn = document.getElementById('enableNotif');

    const EMOJIS = ['😀','🙂','😌','😏','😎','😬','😴','😮‍💨','😤','😢','💪','🧘','🔥','🌊','🌈'];

    function renderDays(){
      dayScroller.innerHTML='';
      for(let i=1;i<=30;i++){
        const d = document.createElement('button');
        d.className = 'story';
        d.dataset.day=i;
        d.dataset.active = (i===state.currentDay);
        const done = state.days[i-1].free;
        d.innerHTML = done ? '✅<small>Day '+i+'</small>' : 'Day '+i + '<small>•</small>';
        d.addEventListener('click',()=>{ state.currentDay=i; save(); renderAll(); setTimeout(()=>d.scrollIntoView({behavior:'smooth', inline:'center'}),10); });
        dayScroller.appendChild(d);
      }
    }

    function renderPicker(){
      emojiPicker.innerHTML='';
      EMOJIS.forEach(e=>{
        const b=document.createElement('button');
        b.className='emoji'; b.textContent=e; b.title=e; b.setAttribute('aria-label','emoji '+e);
        if(state.days[state.currentDay-1].mood===e) b.classList.add('active');
        b.addEventListener('click',()=>{
          state.days[state.currentDay-1].mood = e; save(); renderPicker();
        });
        emojiPicker.appendChild(b);
      });
    }

    function renderForm(){
      const d = state.days[state.currentDay-1];
      titleDay.textContent = `Day ${state.currentDay} – Keep Going 💪`;
      freeToggle.checked = !!d.free;
      noteEl.value = d.note || '';
      renderPicker();
    }

    function calcStats(){
      const totalFree = state.days.filter(x=>x.free).length;
      // streak from day 1
      let s=0; for(const day of state.days){ if(day.free) s++; else break; }
      return { totalFree, streak:s, pct: Math.round(totalFree/30*100) };
    }

    function renderStats(){
      const {totalFree, streak, pct} = calcStats();
      totalFreeEl.textContent = `${totalFree}/30`;
      streakEl.textContent = `${streak}🔥`;
      progBar.style.width = pct+'%';
      updateChart();
    }

    // --- Chart ---
    const ctx = document.getElementById('chart');
    const chart = new Chart(ctx, {
      type: 'line',
      data: {
        labels: Array.from({length:30}, (_,i)=>'D'+(i+1)),
        datasets: [{
          label: 'Bebas Minum',
          data: state.days.map(d=> d.free ? 1 : 0),
          tension:.35,
          borderWidth:2,
          pointRadius:0,
          fill:true
        }]
      },
      options: {
        responsive:true,
        plugins:{ legend:{ display:false } },
        scales:{
          y:{ min:0, max:1, ticks:{ display:false }, grid:{ display:false } },
          x:{ ticks:{ color:'rgba(233,235,255,.6)' }, grid:{ color:'rgba(255,255,255,.08)' } }
        }
      }
    });
    function updateChart(){
      chart.data.datasets[0].data = state.days.map(d=> d.free ? 1 : 0);
      chart.update();
    }

    // --- Actions ---
    saveBtn.addEventListener('click',()=>{
      const d = state.days[state.currentDay-1];
      d.free = freeToggle.checked;
      d.note = noteEl.value.trim();
      save(); renderDays(); renderStats();
      toast('✅ Tersimpan! Good job.');
    });

    document.querySelectorAll('.reacts button').forEach(b=>{
      b.addEventListener('click',()=>{
        const key = b.dataset.react; const d = state.days[state.currentDay-1];
        d.reacts[key] = (d.reacts[key]||0)+1; save();
        burst(b);
      });
    });

    resetBtn.addEventListener('click',()=>{
      if(confirm('Reset seluruh progres 30 hari?')){
        Object.assign(state, structuredClone(defaultData)); save(); renderAll();
      }
    });

    exportBtn.addEventListener('click',()=>{
      const blob = new Blob([JSON.stringify(state,null,2)], {type:'application/json'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href=url; a.download='sobriety-30hari.json'; a.click();
      setTimeout(()=>URL.revokeObjectURL(url), 1000);
    });

    importInput.addEventListener('change', async (e)=>{
      const file = e.target.files[0]; if(!file) return;
      const text = await file.text();
      try{ const data = JSON.parse(text); Object.assign(state, data); save(); renderAll(); toast('✅ Data di-import.'); }
      catch{ alert('File tidak valid.'); }
    });

    // --- Notifications ---
    remindTime.value = state.remind.time || '';
    enableNotifBtn.addEventListener('click', async ()=>{
      state.remind.time = remindTime.value; save();
      const perm = await Notification.requestPermission();
      if(perm!=='granted'){ alert('Aktifkan izin notifikasi di browser.'); return; }
      toast('🔔 Notifikasi diaktifkan. Biarkan tab ini terbuka.');
    });

    setInterval(()=>{
      if(!state.remind.time) return;
      const now = new Date();
      const [hh,mm] = state.remind.time.split(':').map(Number);
      if(now.getHours()===hh && now.getMinutes()===mm && now.getSeconds()<3){
        if(document.visibilityState==='hidden' || document.hidden){
          try{ new Notification('Cek Sobriety Tracker ✨', { body:'Centang status dan tulis mood hari ini ya!'}); }catch(e){}
        } else {
          toast('🔔 Waktunya update progres hari ini!');
        }
      }
    }, 1000);

    // --- Tiny helpers ---
    function toast(msg){
      const t=document.createElement('div');
      t.textContent=msg; t.style.position='fixed'; t.style.bottom='18px'; t.style.left='50%'; t.style.transform='translateX(-50%)';
      t.style.padding='10px 14px'; t.style.background='rgba(20,24,50,.9)'; t.style.border='1px solid rgba(255,255,255,.18)'; t.style.borderRadius='12px';
      t.style.color='#fff'; t.style.zIndex=9999; t.style.boxShadow='0 10px 30px rgba(0,0,0,.35)';
      document.body.appendChild(t); setTimeout(()=>t.remove(), 2000);
    }
    function burst(el){
      const rect = el.getBoundingClientRect();
      for(let i=0;i<8;i++){
        const s=document.createElement('span'); s.textContent='✨'; s.style.position='fixed';
        s.style.left = (rect.left+rect.width/2)+'px'; s.style.top=(rect.top+rect.height/2)+'px';
        s.style.transition='transform .7s ease, opacity .7s ease'; s.style.opacity='1'; s.style.pointerEvents='none';
        document.body.appendChild(s);
        const ang = Math.random()*Math.PI*2; const dist = 40+Math.random()*30;
        requestAnimationFrame(()=>{
          s.style.transform = `translate(${Math.cos(ang)*dist}px, ${Math.sin(ang)*dist}px)`; s.style.opacity='0';
        });
        setTimeout(()=>s.remove(),700);
      }
    }

    function renderAll(){
      renderDays(); renderForm(); renderStats(); remindTime.value = state.remind.time || '';
    }

    // init
    renderAll();
    // scroll to current day on load
    setTimeout(()=>{
      const active = document.querySelector('.story[data-active="true"]');
      active && active.scrollIntoView({behavior:'smooth', inline:'center'});
    }, 50);
  </script></body>
</html>
