      align-items: center;<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Dao of Reviews — Manhua · Donghua · Cosplay · Games · Novels</title>
  <meta name="description" content="Dao of Reviews — a stylized Xianxia + sci‑fi HUD review hub for manhua, donghua, cosplayers, video games, and novels."/>
  <meta name="theme-color" content="#00f0ff" />
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Unbounded:wght@500;700&family=Share+Tech+Mono&display=swap" rel="stylesheet">

  <style>
    :root{
      --bg:#070b12;--text:#e9f1ff;--muted:#9ab0c6;--panel:rgba(255,255,255,.04);
      --border:#1e3244;--accent:#00f0ff;--accent-2:#24ffd4;--gold:#f7c66b;--shadow:0 10px 40px #0008
    }
    *{box-sizing:border-box}html,body{height:100%}
    body{margin:0;font-family:"Share Tech Mono",ui-monospace,SFMono-Regular,Menlo,monospace;color:var(--text);
      background:radial-gradient(1200px 800px at 70% 30%,#0b1423,var(--bg) 60%);overflow-x:hidden}
    body.theme-jade{--accent:#00f0ff;--accent-2:#24ffd4}
    body.theme-crimson{--accent:#ff365d;--accent-2:#ff7a4e}
    #qi-canvas{position:fixed;inset:0;z-index:-1;pointer-events:none}
    .topbar{display:grid;grid-template-columns:1fr auto;align-items:center;gap:1rem;padding:.75rem 1rem;border-bottom:1px solid var(--border);
      background:linear-gradient(180deg,rgba(255,255,255,.03),rgba(255,255,255,.01));backdrop-filter:blur(6px);position:sticky;top:0;z-index:10}
    .brand{display:flex;align-items:baseline;gap:.5rem}.brand-title{font-family:"Unbounded",system-ui;letter-spacing:.5px;margin:0}
    .brand-sub{opacity:.7;font-size:.9rem}.brand-logo{filter:drop-shadow(0 0 6px var(--accent))}
    .actions{display:flex;gap:.5rem;align-items:center;flex-wrap:wrap}
    .search-wrap{display:flex;align-items:stretch;border:1px solid var(--border);border-radius:10px;overflow:hidden;background:var(--panel)}
    #search{padding:.6rem .75rem;background:transparent;color:var(--text);border:0;width:min(36vw,380px)}
    #clearSearch{padding:.6rem .7rem;color:var(--muted);display:none}
    select,.chip,.ghost,.primary{font:inherit;color:var(--text);background:var(--panel);border:1px solid var(--border);
      border-radius:10px;padding:.55rem .75rem;cursor:pointer}
    .chip.primary{background:linear-gradient(180deg,var(--accent),var(--accent-2));color:#001018;border:1px solid transparent;font-weight:700}
    .chip.primary:hover{filter:brightness(.95)}.ghost{background:transparent}select{min-width:150px}
    .footer{margin-top:2rem;border-top:1px solid var(--border);display:flex;justify-content:space-between;align-items:center;padding:1rem;color:var(--muted);
      background:linear-gradient(0deg,rgba(255,255,255,.03),rgba(255,255,255,.01))}.footer a{color:var(--muted);text-decoration:none}.footer a:hover{color:var(--accent)}
    #app{padding:1.25rem 1rem 2rem}
    .ring-wrap{position:relative;margin:4vh auto 2rem;width:min(560px,90vw);aspect-ratio:1/1;display:grid;place-items:center;filter:drop-shadow(0 0 20px rgba(0,0,0,.6))}
    .ring{position:absolute;inset:0;border-radius:50%;border:2px dashed color-mix(in srgb,var(--accent) 60%,#fff 20%);animation:ringSpin 32s linear infinite}
    .ring::after{content:"";position:absolute;inset:10%;border-radius:50%;border:1px solid color-mix(in srgb,var(--accent) 40%,transparent);
      box-shadow:inset 0 0 40px color-mix(in srgb,var(--accent) 18%,transparent)}
    @keyframes ringSpin{to{transform:rotate(360deg)}}
    .ring-center{z-index:2;text-align:center;font-family:"Unbounded",system-ui;color:var(--accent);
      text-shadow:0 0 12px color-mix(in srgb,var(--accent) 60%,transparent)}
    .ring-center h2{margin:0;font-weight:700}.ring-center p{margin:.25rem 0 0;color:var(--muted)}
    .radial-menu{position:absolute;inset:0}
    .radial-item{position:absolute;width:88px;height:88px;border-radius:50%;display:grid;place-items:center;font-size:1.6rem;color:var(--accent);
      background:rgba(255,255,255,.04);border:1px solid var(--border);box-shadow:inset 0 0 22px rgba(0,0,0,.35);
      transition:transform .25s ease,box-shadow .25s ease,background .25s ease;user-select:none}
    .radial-item:hover{transform:scale(1.12);box-shadow:0 0 22px color-mix(in srgb,var(--accent) 55%,transparent);
      background:color-mix(in srgb,var(--accent) 10%, rgba(255,255,255,.06));cursor:pointer}
    /* 5-way ring: 18°, 90°, 162°, 234°, 306° */
    .radial-item[data-type="manhua"]{--deg:18deg}
    .radial-item[data-type="donghua"]{--deg:90deg}
    .radial-item[data-type="cosplay"]{--deg:162deg}
    .radial-item[data-type="game"]{--deg:234deg}
    .radial-item[data-type="novel"]{--deg:306deg}
    .radial-item{top:calc(50% - 44px);left:calc(50% - 44px);
      transform:rotate(var(--deg)) translateX(calc(min(560px,90vw)/2.25)) rotate(calc(-1*var(--deg)))}
    .preview-strip{margin:1rem auto 0;max-width:1100px;display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:.9rem}
    .card{background:var(--panel);border:1px solid var(--border);border-radius:12px;padding:.9rem;box-shadow:var(--shadow);
      transition:transform .2s ease,border-color .2s ease}
    .card:hover{transform:translateY(-4px);border-color:var(--accent)}
    .card .thumb{width:100%;aspect-ratio:16/9;border-radius:8px;overflow:hidden;margin-bottom:.6rem;background:#0c1725}
    .card .thumb img{width:100%;height:100%;object-fit:cover;display:block}
    .card h3{margin:.25rem 0 .35rem;font-family:"Unbounded";font-size:1.05rem}
    .meta{font-size:.85rem;color:var(--muted);display:flex;gap:.6rem;align-items:center}
    .tags{display:flex;gap:.35rem;flex-wrap:wrap;margin-top:.5rem}.tag{font-size:.75rem;padding:.25rem .45rem;border-radius:999px;border:1px solid var(--border);color:var(--muted)}
    .controls{margin:.5rem 0 1rem;display:flex;gap:.5rem;flex-wrap:wrap;align-items:center}
    .toggle{padding:.45rem .6rem;border-radius:999px;border:1px solid var(--border);background:var(--panel);color:var(--text);cursor:pointer;text-decoration:none}
    .toggle.active{border-color:var(--accent);color:var(--accent)}
    .grid{display:grid;gap:1rem;grid-template-columns:repeat(auto-fill,minmax(260px,1fr))}
    .detail{display:grid;gap:1.2rem;grid-template-columns:360px 1fr}
    @media(max-width:900px){.detail{grid-template-columns:1fr}}
    .detail .cover{border:1px solid var(--border);border-radius:12px;overflow:hidden;background:#0c1725;box-shadow:var(--shadow)}
    .detail .cover img{width:100%;height:auto;display:block}
    .detail h2{margin:0;font-family:"Unbounded"}
    .rating{display:inline-flex;align-items:center;gap:.45rem;line-height:1;padding:.35rem .55rem;border:1px solid var(--border);border-radius:999px;background:var(--panel)}
    .stars{display:inline-flex;gap:.15rem;cursor:pointer}.star{filter:drop-shadow(0 0 6px transparent);transition:transform .15s}
    .star:hover{transform:translateY(-1px) scale(1.05)}.star.filled{color:var(--gold);filter:drop-shadow(0 0 6px rgba(247,198,107,.5))}
    .detail .chips{display:flex;gap:.35rem;flex-wrap:wrap}.detail .chip{background:var(--panel);border:1px solid var(--border);border-radius:999px;padding:.35rem .6rem}
    .detail .actions{display:flex;gap:.5rem;flex-wrap:wrap}.detail p{color:#d7e6ff;opacity:.9}
    .form{display:grid;gap:.75rem;max-width:820px}.form-row{display:grid;gap:.5rem}.form-row.cols{grid-template-columns:repeat(2,1fr)}
    @media(max-width:720px){.form-row.cols{grid-template-columns:1fr}}
    .form input,.form textarea,.form select{width:100%;border-radius:10px;border:1px solid var(--border);background:var(--panel);color:var(--text);padding:.7rem .75rem;font:inherit}
    .form textarea{min-height:160px;resize:vertical}.form .help{color:var(--muted);font-size:.85rem}
    .center{text-align:center}.hidden{display:none!important}.small{font-size:.85rem;color:var(--muted)}.hr{height:1px;background:var(--border);margin:.75rem 0}
    :focus-visible{outline:2px solid var(--accent);outline-offset:2px}
  </style>
</head>
<body class="theme-jade">
  <canvas id="qi-canvas" aria-hidden="true"></canvas>

  <header class="topbar" role="banner">
    <div class="brand">
      <span class="brand-logo" aria-hidden="true">🜲</span>
      <h1 class="brand-title">Dao of Reviews</h1>
      <span class="brand-sub">Reviews</span>
    </div>

    <div class="actions">
      <div class="search-wrap">
        <input id="search" type="search" placeholder="Search titles, tags…" aria-label="Search"/>
        <button id="clearSearch" class="ghost" title="Clear search" aria-label="Clear search">✕</button>
      </div>

      <select id="sortBy" aria-label="Sort reviews">
        <option value="featured">Sort: Featured</option>
        <option value="rating">Sort: Rating</option>
        <option value="newest">Sort: Newest</option>
        <option value="title">Sort: Title</option>
      </select>

      <button id="themeToggle" class="chip" title="Toggle theme" aria-pressed="false">Theme</button>
      <button id="sfxToggle" class="chip" title="Toggle sounds" aria-pressed="false">SFX</button>
      <a id="addBtn" class="chip primary" href="#/submit" title="Add Review">+ Add</a>
    </div>
  </header>

  <main id="app" role="main" tabindex="-1"></main>

  <footer class="footer">
    <span>© <span id="year"></span> Dao of Reviews</span>
    <nav class="footer-links">
      <a href="#/about">About</a>
      <a href="#/home">Home</a>
      <a href="#/submit">Submit</a>
      <a href="#/all">All Reviews</a>
    </nav>
  </footer>

  <!-- Seed data (added a Novel example) -->
  <script>
    window.IR_SEED = (() => {
      const items = [
        {
          id:"soul-reaper-immortal",type:"manhua",title:"Soul Reaper Immortal",author:"Qin Yao Studio",year:2024,
          coverUrl:"https://images.unsplash.com/photo-1612036782180-6f0b6fcdc3c6?q=80&w=1200&auto=format&fit=crop",
          rating:4.6,tags:["cultivation","dark-fantasy","action"],
          summary:"A reaper who harvests souls to refine his Qi breaks the heavenly order.",
          body:"In a realm where death cycles into spiritual energy, a mortal reaper ascends. Pacing is brisk with lethal choreography. Art leans moody ink-wash meets neon etching.",
          createdAt:Date.now()-1000*60*60*24*40
        },
        {
          id:"ling-cage-pilot",type:"donghua",title:"Ling Cage: Pilot Redux",author:"YHKT Entertainment",year:2023,
          coverUrl:"https://images.unsplash.com/photo-1520975922284-9f79f0283f1b?q=80&w=1200&auto=format&fit=crop",
          rating:4.8,tags:["sci-fi","post-apoc","mecha"],
          summary:"Sacred-tech ruins, biohazards, and a city clinging to light.",
          body:"Phenomenal atmospheric worldbuilding. HUD overlays and sacred geometry motifs elevate tension. Minor pacing dips but visuals carry.",
          createdAt:Date.now()-1000*60*60*24*62
        },
        {
          id:"emerald-lotus",type:"cosplay",title:"Emerald Lotus (Qinglian)",author:"@QingLianForge",year:2025,
          coverUrl:"https://images.unsplash.com/photo-1520974955349-9b25d54f9981?q=80&w=1200&auto=format&fit=crop",
          rating:4.7,tags:["xianxia","craft","armor"],
          summary:"Jade-lacquer breastplate with thread-light glyphs.",
          body:"Material alchemy masterclass: painted resin + EL wire + etched runes. Photoset staged with ink mist — flawless.",
          createdAt:Date.now()-1000*60*60*24*9
        },
        {
          id:"immersion-overclocked",type:"game",title:"Immersion Overclocked",author:"Reality Overdrive Studio",year:2025,
          coverUrl:"https://images.unsplash.com/photo-1605901309584-818e25960a8b?q=80&w=1200&auto=format&fit=crop",
          rating:4.4,tags:["vrmmorpg","hardcore","systems"],
          summary:"A VR that feels *too real* — pain toggles included.",
          body:"Combat systems are punishing yet fair. Crafting loops reward mastery. Sound design slaps. Needs better new-player onboarding.",
          createdAt:Date.now()-1000*60*60*24*3
        },
        {
          id:"jade-emperor-apprentice",type:"novel",title:"Jade Emperor’s Apprentice",author:"Mu Qing",year:2025,
          coverUrl:"https://images.unsplash.com/photo-1549880338-65ddcdfd017b?q=80&w=1200&auto=format&fit=crop",
          rating:4.5,tags:["xianxia","growth","adventure"],
          summary:"A mortal scribe inherits a fractured dao and must rewrite the heavens.",
          body:"Balances intrigue and cultivation theory with crisp, readable prose. Power progression is steady; sect politics feel grounded. Occasional exposition dumps, but worth it.",
          createdAt:Date.now()-1000*60*60*24*6
        }
      ];
      return { items };
    })();
  </script>

  <!-- App logic -->
  <script>
    (() => {
      const $=s=>document.querySelector(s), $$=s=>[...document.querySelectorAll(s)];
      const app=$("#app"), searchInput=$("#search"), clearSearchBtn=$("#clearSearch"),
            sortSel=$("#sortBy"), themeToggle=$("#themeToggle"), sfxToggle=$("#sfxToggle");
      $("#year").textContent=new Date().getFullYear();

      const TYPES=["manhua","donghua","cosplay","game","novel"];
      const STORAGE_KEY="IR_USER_DATA_V2"; // bump for new category
      const store={_mem:null,_load(){try{const raw=localStorage.getItem(STORAGE_KEY);
        if(raw)this._mem=JSON.parse(raw);else this._mem={reviews:IR_SEED.items,ratings:{},sfx:false,theme:"jade"}}
        catch{this._mem={reviews:IR_SEED.items,ratings:{},sfx:false,theme:"jade"}}
        const known=new Set(this._mem.reviews.map(r=>r.id)); IR_SEED.items.forEach(r=>{if(!known.has(r.id))this._mem.reviews.push(r)});
        document.body.classList.toggle("theme-crimson",this._mem.theme==="crimson");
        document.body.classList.toggle("theme-jade",this._mem.theme!=="crimson"); return this._mem},
        get(){return this._mem||this._load()}, save(){try{localStorage.setItem(STORAGE_KEY,JSON.stringify(this._mem))}catch{}}};
      store._load();

      const routes={"#/home":renderHome,"#/all":renderAll,"#/list":renderList,"#/review":renderDetail,"#/submit":renderSubmit,"#/about":renderAbout};
      function parseHash(){const hash=location.hash||"#/home";const [path,qs]=hash.split("?");return{path,params:new URLSearchParams(qs||"")}}
      addEventListener("hashchange",()=>{const {path}=parseHash();(routes[path]||renderHome)();app.focus({preventScroll:true})});

      let audioCtx; function playChime(freq=660,dur=.08){if(!store.get().sfx)return;try{
        audioCtx=audioCtx||new (window.AudioContext||window.webkitAudioContext)();const o=audioCtx.createOscillator(),g=audioCtx.createGain();
        o.type="sine";o.frequency.value=freq;g.gain.value=.06;o.connect(g);g.connect(audioCtx.destination);const t=audioCtx.currentTime;
        o.start(t);g.gain.exponentialRampToValueAtTime(.0001,t+dur);o.stop(t+dur);}catch{}}

      const html=(a,...b)=>a.reduce((x,s,i)=>x+s+(b[i]??""),"");
      const esc=s=>(s+"").replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
      const fmtStars=x=>"★".repeat(Math.round(x))+"☆".repeat(5-Math.round(x));
      const slugify=s=>s.toLowerCase().replace(/[^a-z0-9]+/g,"-").replace(/(^-|-$)/g,"");
      const avgRating=(base,user)=>user?(base+user)/2:base;
      const getAllReviews=()=>store.get().reviews.slice().sort((a,b)=>b.createdAt-a.createdAt);
      const getByType=t=>getAllReviews().filter(r=>r.type===t);
      const getById=id=>getAllReviews().find(r=>r.id===id);

      function renderHome(){if(location.hash!=="#/home")location.hash="#/home";
        const recent=getAllReviews().slice(0,5);
        app.innerHTML=html`
          <section class="ring-wrap" aria-label="Main circular navigation">
            <div class="ring" aria-hidden="true"></div>
            <div class="ring-center"><h2>🔮 Dao of Reviews</h2><p>Choose your path</p></div>
            <div class="radial-menu">
              ${radialItem("manhua","📚","Manhua")}
              ${radialItem("donghua","🎥","Donghua")}
              ${radialItem("cosplay","🧝","Cosplay")}
              ${radialItem("game","🕹️","Games")}
              ${radialItem("novel","📖","Novels")}
            </div>
          </section>
          <section aria-label="Featured previews" class="preview-strip">
            ${recent.map(card).join("")}
          </section>`;
        $$(".radial-item").forEach(el=>{
          el.addEventListener("click",()=>{playChime(720);location.hash=`#/list?type=${el.dataset.type}`});
          el.addEventListener("mouseenter",()=>playChime(820,.06));
        });
        $$(".card").forEach(el=>{
          const go=()=>{playChime(640);location.hash=`#/review?id=${el.dataset.id}`};
          el.addEventListener("click",go);
          el.addEventListener("keydown",e=>{if(e.key==="Enter"||e.key===" "){e.preventDefault();go();}});
        });
      }
      const radialItem=(type,icon,label)=>html`<button class="radial-item" data-type="${type}" aria-label="${label}"><span aria-hidden="true">${icon}</span></button>`;
      function card(r){const user=store.get().ratings[r.id];const rating=avgRating(r.rating,user);
        const meta=`${r.type.toUpperCase()} • ${r.author||"Unknown"} • ${r.year||"—"}`;
        return html`<article class="card clickable" data-id="${esc(r.id)}" role="button" tabindex="0" aria-label="${esc(r.title)}">
          <div class="thumb"><img src="${esc(r.coverUrl)}" alt="${esc(r.title)} cover"></div>
          <h3>${esc(r.title)}</h3>
          <div class="meta"><span class="small">${esc(meta)}</span><span class="rating small">${fmtStars(rating)} (${rating.toFixed(1)})</span></div>
          <div class="tags">${r.tags.slice(0,4).map(t=>`<span class="tag">#${esc(t)}</span>`).join("")}</div>
        </article>`}
      function renderAll(){const list=getAllReviews();
        app.innerHTML=html`<h2>All Reviews</h2>${filtersBar()}<section class="grid">${list.map(card).join("")}</section>`; bindCommonListHandlers()}
      function renderList(){const{params}=parseHash();const type=(params.get("type")||"manhua").toLowerCase();
        const valid=TYPES.includes(type)?type:"manhua";const title=valid.charAt(0).toUpperCase()+valid.slice(1);
        let list=getByType(valid); list=applySearchSort(list);
        app.innerHTML=html`<h2>${esc(title)} Reviews</h2>${filtersBar(valid)}<section class="grid">${list.map(card).join("")}</section>`;
        bindCommonListHandlers(valid)}
      function filtersBar(activeType){return html`<div class="controls" role="toolbar" aria-label="Filters">
        ${TYPES.map(t=>{const label=t[0].toUpperCase()+t.slice(1);const active=activeType===t?"active":"";return `<a class="toggle ${active}" href="#/list?type=${t}">${label}</a>`}).join("")}
        <a class="toggle" href="#/all">All</a><span class="small">Tip: Use the search and sort controls in the top bar.</span></div>`}
      function applySearchSort(list){const q=(searchInput.value||"").trim().toLowerCase();
        if(q){list=list.filter(r=>r.title.toLowerCase().includes(q)||(r.author||"").toLowerCase().includes(q)||r.tags.some(t=>t.toLowerCase().includes(q)));}
        switch(sortSel.value){
          case "rating": list.sort((a,b)=>avgRating(b.rating,store.get().ratings[b.id])-avgRating(a.rating,store.get().ratings[a.id]));break;
          case "newest": list.sort((a,b)=>b.createdAt-a.createdAt);break;
          case "title": list.sort((a,b)=>a.title.localeCompare(b.title));break;
          default: { const score=r=>avgRating(r.rating,store.get().ratings[r.id])*2 + r.createdAt/1e11; list.sort((a,b)=>score(b)-score(a));}
        } return list}
      function bindCommonListHandlers(currType){$$(".card").forEach(el=>{const go=()=>{playChime(640);location.hash=`#/review?id=${el.dataset.id}`};
        el.addEventListener("click",go); el.addEventListener("keydown",e=>{if(e.key==="Enter"||e.key===" "){e.preventDefault();go();}})});
        if(currType){$$(".toggle").forEach(t=>t.classList.toggle("active",t.textContent.toLowerCase().includes(currType)));}}
      function renderDetail(){const{params}=parseHash();const id=params.get("id");const r=getById(id);
        if(!r){app.innerHTML=`<p>Not found. <a href="#/home">Back home</a></p>`;return}
        const user=store.get().ratings[r.id];const rating=avgRating(r.rating,user);
        app.innerHTML=html`<nav style="margin-bottom:.6rem;"><a class="chip" href="#/list?type=${r.type}">← Back to ${r.type}</a></nav>
        <section class="detail" aria-label="Review details">
          <div class="cover"><img src="${esc(r.coverUrl)}" alt="${esc(r.title)} cover"></div>
          <div>
            <h2>${esc(r.title)}</h2>
            <div style="display:flex;gap:.6rem;align-items:center;flex-wrap:wrap;margin:.35rem 0 .5rem;">
              <span class="rating" title="Average rating"><strong>${rating.toFixed(1)}</strong>
                <span class="stars" aria-label="Your rating">
                  ${[1,2,3,4,5].map(n=>`<span class="star ${user>=n?'filled':''}" data-n="${n}">★</span>`).join("")}
                </span>
              </span>
              <span class="small">${(r.type.toUpperCase())} • ${esc(r.author||"Unknown")} • ${esc(r.year||"—")}</span>
            </div>
            <div class="chips">${r.tags.map(t=>`<span class="chip">#${esc(t)}</span>`).join("")}</div>
            <div class="hr"></div>
            <p><em>${esc(r.summary)}</em></p>
            <p>${esc(r.body)}</p>
            <div class="actions" style="margin-top:.6rem;">
              <button class="chip" id="copyLink">🔗 Copy Link</button>
              <button class="chip" id="shareSys">📤 Share</button>
            </div>
          </div>
        </section>`;
        $$(".star").forEach(el=>{
          el.addEventListener("click",()=>{const n=Number(el.dataset.n);store.get().ratings[r.id]=n;store.save();playChime(540+n*40,.09);renderDetail()});
          el.addEventListener("mouseenter",()=>playChime(840,.05));
        });
        $("#copyLink").addEventListener("click",async()=>{const url=`${location.origin}${location.pathname}#/review?id=${r.id}`;
          try{await navigator.clipboard.writeText(url)}catch{} const btn=$("#copyLink");btn.textContent="✅ Copied!";setTimeout(()=>btn.textContent="🔗 Copy Link",1e3);playChime(760);});
        $("#shareSys").addEventListener("click",async()=>{const url=`${location.origin}${location.pathname}#/review?id=${r.id}`;
          try{await navigator.share({title:r.title,text:r.summary,url})}catch{}});
      }
      function renderSubmit(){app.innerHTML=html`<h2>Submit a Review</h2>
        <form class="form" id="submitForm">
          <div class="form-row cols">
            <div><label>Title</label><input required name="title" placeholder="e.g. Jade Emperor's Path"></div>
            <div><label>Type</label>
              <select name="type" required>
                <option value="">Choose…</option>
                <option value="manhua">Manhua</option>
                <option value="donghua">Donghua</option>
                <option value="cosplay">Cosplay</option>
                <option value="game">Game</option>
                <option value="novel">Novel</option>
              </select>
            </div>
          </div>
          <div class="form-row cols">
            <div><label>Author / Creator</label><input name="author" placeholder="@creator or studio"></div>
            <div><label>Year</label><input name="year" type="number" min="1900" max="2100" placeholder="2025"></div>
          </div>
          <div class="form-row"><label>Cover Image URL</label><input name="coverUrl" placeholder="https://...">
            <div class="help">Use a direct image link (JPG/PNG). Optional; a placeholder is used if empty.</div></div>
          <div class="form-row"><label>Summary</label><input name="summary" placeholder="Short hook… (1–2 sentences)" maxlength="180" required></div>
          <div class="form-row"><label>Full Review</label><textarea name="body" placeholder="Write your thoughts…" required></textarea></div>
          <div class="form-row"><label>Tags (comma‑separated)</label><input name="tags" placeholder="cultivation, action, sci‑fi"></div>
          <div class="form-row cols">
            <div><label>Initial Rating</label><input name="rating" type="number" min="1" max="5" step="0.1" value="4.0"></div>
            <div><label>&nbsp;</label><button class="chip primary" type="submit">Publish</button></div>
          </div>
          <p class="small">Stored locally in your browser (no server). You can export later.</p>
        </form>`;
        $("#submitForm").addEventListener("submit",e=>{
          e.preventDefault(); const fd=new FormData(e.currentTarget);
          const title=(fd.get("title")+"").trim(), type=fd.get("type")+"", author=(fd.get("author")+"").trim(),
                year=Number(fd.get("year")||""), coverUrl=(fd.get("coverUrl")+"").trim()||"https://placehold.co/1200x675/0c1725/9ab0c6?text=Dao+of+Reviews",
                summary=(fd.get("summary")+"").trim(), body=(fd.get("body")+"").trim(),
                tags=(fd.get("tags")+"").split(",").map(t=>t.trim()).filter(Boolean),
                rating=Math.max(1,Math.min(5,Number(fd.get("rating")||4)));
          if(!title||!type||!summary||!body){alert("Please fill required fields.");return}
          const id=slugify(title); if(getById(id)){alert("A review with that title already exists. Try a different title.");return}
          store.get().reviews.unshift({id,type,title,author,year,coverUrl,rating,tags,summary,body,createdAt:Date.now()});
          store.save(); playChime(880,.12); location.hash=`#/review?id=${id}`;
        });
      }
      function renderAbout(){app.innerHTML=html`<h2>About</h2>
        <p><strong>Dao of Reviews</strong> is a stylized review hub for <strong>manhua</strong>, <strong>donghua</strong>, <strong>cosplayers</strong>, <strong>video games</strong>, and <strong>novels</strong> — presented as a sci‑fi/Xianxia hybrid HUD.</p>
        <ul><li>No backend; everything runs in your browser.</li><li>Add reviews; they persist via <code>localStorage</code>.</li><li>Rate with stars; share deep links.</li></ul>
        <p class="small">Tip: Toggle <em>Theme</em> to switch Jade ↔ Crimson. Toggle <em>SFX</em> for chimes.</p>`}

      // Topbar binds
      const updateClearBtn=()=>{clearSearchBtn.style.display=searchInput.value?"inline-block":"none"}; updateClearBtn();
      searchInput.addEventListener("input",()=>{updateClearBtn(); const {path}=parseHash(); if(path==="#/list")renderList(); else if(path==="#/all")renderAll()});
      clearSearchBtn.addEventListener("click",()=>{searchInput.value=""; updateClearBtn(); const {path}=parseHash(); if(path==="#/list")renderList(); else if(path==="#/all")renderAll()});
      sortSel.addEventListener("change",()=>{const {path}=parseHash(); if(path==="#/list")renderList(); else if(path==="#/all")renderAll()});
      const themeApply=()=>{const s=store.get(); document.body.classList.toggle("theme-crimson",s.theme==="crimson");
        document.body.classList.toggle("theme-jade",s.theme!=="crimson"); themeToggle.setAttribute("aria-pressed",String(s.theme==="crimson"))};
      themeToggle.addEventListener("click",()=>{const s=store.get(); s.theme=s.theme==="crimson"?"jade":"crimson"; store.save(); themeApply(); playChime(600)}); themeApply();
      sfxToggle.addEventListener("click",()=>{const s=store.get(); s.sfx=!s.sfx; store.save(); sfxToggle.classList.toggle("active",s.sfx); sfxToggle.setAttribute("aria-pressed",String(s.sfx)); s.sfx&&playChime(720)});
      if(store.get().sfx){sfxToggle.classList.add("active"); sfxToggle.setAttribute("aria-pressed","true")}

      // Qi particles
      const canvas=document.getElementById("qi-canvas"), ctx=canvas.getContext("2d",{alpha:true}); let W,H,DPR,particles=[];
      const P_BASE=180; function resize(){DPR=Math.min(2,devicePixelRatio||1); W=canvas.width=Math.floor(innerWidth*DPR);
        H=canvas.height=Math.floor(innerHeight*DPR); canvas.style.width=innerWidth+"px"; canvas.style.height=innerHeight+"px"; initParticles()}
      addEventListener("resize",resize);
      function initParticles(){const count=Math.round(P_BASE*Math.min(1.4,(innerWidth*innerHeight)/(1200*800)));
        particles=Array.from({length:count},()=>({r:.6+Math.random()*1.8,ang:Math.random()*Math.PI*2,rad:Math.random()*Math.min(W,H)/2,speed:(.0008+Math.random()*.0016)*(Math.random()<.5?-1:1)}))}
      function draw(){ctx.clearRect(0,0,W,H); const cx=W/2,cy=H/2; const accent=getComputedStyle(document.body).getPropertyValue('--accent').trim()||"#00f0ff";
        for(const p of particles){p.ang+=p.speed; p.rad+=Math.sin((performance.now()/1400)+p.ang)*.04; const x=cx+Math.cos(p.ang)*p.rad, y=cy+Math.sin(p.ang)*p.rad*.62;
          const g=ctx.createRadialGradient(x,y,0,x,y,16*DPR); g.addColorStop(0,accent+"cc"); g.addColorStop(1,"#0000"); ctx.fillStyle=g; ctx.beginPath(); ctx.arc(x,y,p.r*DPR*2.2,0,Math.PI*2); ctx.fill();}
        requestAnimationFrame(draw)}
      resize(); draw();

      (routes[parseHash().path]||renderHome)();
    })();
  </script>

  <noscript><div style="padding:1rem;background:#111;color:#fff;text-align:center;">This app requires JavaScript.</div></noscript>
</body>
</html>

      gap: 1rem;
      padding: .75rem 1rem;
      border-bottom: 1px solid var(--border);
      background: linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.01));
      backdrop-filter: blur(6px);
      position: sticky; top: 0; z-index: 10;
    }
    .brand { display: flex; align-items: baseline; gap: .5rem; }
    .brand-title {
      font-family: "Unbounded", system-ui; letter-spacing: .5px; margin: 0;
    }
    .brand-sub { opacity: .7; font-size: .9rem; }
    .brand-logo { filter: drop-shadow(0 0 6px var(--accent)); }

    .actions { display: flex; gap: .5rem; align-items: center; flex-wrap: wrap; }
    .search-wrap {
      display: flex; align-items: stretch; border: 1px solid var(--border);
      border-radius: 10px; overflow: hidden; background: var(--panel);
    }
    #search {
      padding: .6rem .75rem; background: transparent; color: var(--text); border: 0; width: min(36vw, 380px);
    }
    #clearSearch { padding: .6rem .7rem; color: var(--muted); display: none; }
    select, .chip, .ghost, .primary {
      font: inherit; color: var(--text); background: var(--panel);
      border: 1px solid var(--border); border-radius: 10px; padding: .55rem .75rem;
      cursor: pointer;
    }
    .chip.primary { background: linear-gradient(180deg, var(--accent), var(--accent-2));
      color: #001018; border: 1px solid transparent; font-weight: 700; }
    .chip.primary:hover { filter: brightness(.95); }
    .ghost { background: transparent; }
    select { min-width: 150px; }

    /* Footer */
    .footer {
      margin-top: 2rem; border-top: 1px solid var(--border);
      display: flex; justify-content: space-between; align-items: center;
      padding: 1rem; color: var(--muted);
      background: linear-gradient(0deg, rgba(255,255,255,0.03), rgba(255,255,255,0.01));
    }
    .footer a { color: var(--muted); text-decoration: none; }
    .footer a:hover { color: var(--accent); }

    /* Main layout */
    #app { padding: 1.25rem 1rem 2rem; }

    /* ===== HOME: Ring Menu ===== */
    .ring-wrap {
      position: relative;
      margin: 4vh auto 2rem;
      width: min(560px, 90vw);
      aspect-ratio: 1/1;
      display: grid; place-items: center;
      filter: drop-shadow(0 0 20px rgba(0,0,0,.6));
    }
    .ring {
      position: absolute; inset: 0; border-radius: 50%;
      border: 2px dashed rgba(255,255,255,0.2);
      border-color: color-mix(in srgb, var(--accent) 60%, #ffffff 20%);
      animation: ringSpin 32s linear infinite;
    }
    .ring::after {
      content: ""; position: absolute; inset: 10%; border-radius: 50%;
      border: 1px solid rgba(255,255,255,0.12);
      border-color: color-mix(in srgb, var(--accent) 40%, transparent);
      box-shadow: inset 0 0 40px color-mix(in srgb, var(--accent) 18%, transparent);
    }

    @keyframes ringSpin { to { transform: rotate(360deg); } }

    .ring-center {
      z-index: 2; text-align: center;
      font-family: "Unbounded", system-ui; color: var(--accent);
      text-shadow: 0 0 12px color-mix(in srgb, var(--accent) 60%, transparent);
    }
    .ring-center h2 { margin: 0; font-weight: 700; }
    .ring-center p { margin: .25rem 0 0; color: var(--muted); }

    .radial-menu { position: absolute; inset: 0; }
    .radial-item {
      position: absolute; width: 88px; height: 88px; border-radius: 50%;
      display: grid; place-items: center; font-size: 1.6rem;
      color: var(--accent); background: rgba(255,255,255,0.04);
      border: 1px solid var(--border);
      box-shadow: inset 0 0 22px rgba(0,0,0,.35);
      transition: transform .25s ease, box-shadow .25s ease, background .25s ease;
      user-select: none;
    }
    .radial-item:hover {
      transform: scale(1.12);
      box-shadow: 0 0 22px color-mix(in srgb, var(--accent) 55%, transparent);
      background: color-mix(in srgb, var(--accent) 10%, rgba(255,255,255,0.06));
      cursor: pointer;
    }
    .radial-item[data-type="manhua"] { --deg: 335deg; }
    .radial-item[data-type="donghua"]{ --deg: 65deg; }
    .radial-item[data-type="cosplay"]{ --deg: 155deg; }
    .radial-item[data-type="game"]   { --deg: 245deg; }

    .radial-item {
      /* Position items around circle */
      top: calc(50% - 44px); left: calc(50% - 44px);
      transform: rotate(var(--deg)) translateX(calc(min(560px, 90vw)/2.25)) rotate(calc(-1 * var(--deg)));
    }

    /* Preview strip under ring */
    .preview-strip {
      margin: 1rem auto 0; max-width: 1100px;
      display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: .9rem;
    }
    .card {
      background: var(--panel);
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: .9rem;
      box-shadow: var(--shadow);
      transition: transform .2s ease, border-color .2s ease;
    }
    .card:hover { transform: translateY(-4px); border-color: var(--accent); }
    .card .thumb {
      width: 100%; aspect-ratio: 16/9; border-radius: 8px; overflow: hidden; margin-bottom: .6rem;
      background: #0c1725;
    }
    .card .thumb img { width: 100%; height: 100%; object-fit: cover; display: block; }
    .card h3 { margin: .25rem 0 .35rem; font-family: "Unbounded"; font-size: 1.05rem; }
    .meta { font-size: .85rem; color: var(--muted); display: flex; gap: .6rem; align-items: center; }
    .tags { display: flex; gap: .35rem; flex-wrap: wrap; margin-top: .5rem; }
    .tag { font-size: .75rem; padding: .25rem .45rem; border-radius: 999px; border: 1px solid var(--border); color: var(--muted); }

    /* ===== LIST VIEW ===== */
    .controls {
      margin: .5rem 0 1rem;
      display: flex; gap: .5rem; flex-wrap: wrap; align-items: center;
    }
    .toggle {
      padding: .45rem .6rem; border-radius: 999px; border: 1px solid var(--border);
      background: var(--panel); color: var(--text); cursor: pointer; text-decoration: none;
    }
    .toggle.active { border-color: var(--accent); color: var(--accent); }
    .grid {
      display: grid; gap: 1rem; grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
    }

    /* ===== DETAIL VIEW ===== */
    .detail {
      display: grid; gap: 1.2rem; grid-template-columns: 360px 1fr;
    }
    @media (max-width: 900px) { .detail { grid-template-columns: 1fr; } }
    .detail .cover {
      border: 1px solid var(--border); border-radius: 12px; overflow: hidden; background: #0c1725;
      box-shadow: var(--shadow);
    }
    .detail .cover img { width: 100%; height: auto; display: block; }
    .detail h2 { margin: 0; font-family: "Unbounded"; }
    .rating {
      display: inline-flex; align-items: center; gap: .45rem; line-height: 1;
      padding: .35rem .55rem; border: 1px solid var(--border); border-radius: 999px; background: var(--panel);
    }
    .stars { display: inline-flex; gap: .15rem; cursor: pointer; }
    .star { filter: drop-shadow(0 0 6px transparent); transition: transform .15s; }
    .star:hover { transform: translateY(-1px) scale(1.05); }
    .star.filled { color: var(--gold); filter: drop-shadow(0 0 6px rgba(247,198,107,.5)); }
    .detail .chips { display: flex; gap: .35rem; flex-wrap: wrap; }
    .detail .chip {
      background: var(--panel); border: 1px solid var(--border); border-radius: 999px; padding: .35rem .6rem;
    }
    .detail .actions { display: flex; gap: .5rem; flex-wrap: wrap; }
    .detail p { color: #d7e6ff; opacity: .9; }

    /* ===== SUBMIT FORM ===== */
    .form {
      display: grid; gap: .75rem; max-width: 820px;
    }
    .form-row { display: grid; gap: .5rem; }
    .form-row.cols { grid-template-columns: repeat(2, 1fr); }
    @media (max-width: 720px) { .form-row.cols { grid-template-columns: 1fr; } }
    .form input, .form textarea, .form select {
      width: 100%; border-radius: 10px; border: 1px solid var(--border);
      background: var(--panel); color: var(--text); padding: .7rem .75rem;
      font: inherit;
    }
    .form textarea { min-height: 160px; resize: vertical; }
    .form .help { color: var(--muted); font-size: .85rem; }

    /* Utility */
    .center { text-align: center; }
    .hidden { display: none !important; }
    .small { font-size: .85rem; color: var(--muted); }
    .hr { height: 1px; background: var(--border); margin: .75rem 0; }

    /* Focus outlines */
    :focus-visible {
      outline: 2px solid var(--accent); outline-offset: 2px;
    }
  </style>
</head>
<body class="theme-jade">
  <!-- Ambient Qi/particle canvas -->
  <canvas id="qi-canvas" aria-hidden="true"></canvas>

  <!-- Top HUD Bar -->
  <header class="topbar" role="banner">
    <div class="brand">
      <span class="brand-logo" aria-hidden="true">🜲</span>
      <h1 class="brand-title">Immersion Realms</h1>
      <span class="brand-sub">Reviews</span>
    </div>

    <div class="actions">
      <div class="search-wrap">
        <input id="search" type="search" placeholder="Search titles, tags…" aria-label="Search"/>
        <button id="clearSearch" class="ghost" title="Clear search" aria-label="Clear search">✕</button>
      </div>

      <select id="sortBy" aria-label="Sort reviews">
        <option value="featured">Sort: Featured</option>
        <option value="rating">Sort: Rating</option>
        <option value="newest">Sort: Newest</option>
        <option value="title">Sort: Title</option>
      </select>

      <button id="themeToggle" class="chip" title="Toggle theme" aria-pressed="false">Theme</button>
      <button id="sfxToggle" class="chip" title="Toggle sounds" aria-pressed="false">SFX</button>
      <a id="addBtn" class="chip primary" href="#/submit" title="Add Review">+ Add</a>
    </div>
  </header>

  <!-- Main App -->
  <main id="app" role="main" tabindex="-1"></main>

  <!-- Footer -->
  <footer class="footer">
    <span>© <span id="year"></span> Immersion Realms</span>
    <nav class="footer-links">
      <a href="#/about">About</a>
      <a href="#/home">Home</a>
      <a href="#/submit">Submit</a>
      <a href="#/all">All Reviews</a>
    </nav>
  </footer>

  <!-- Seed data -->
  <script>
    window.IR_SEED = (() => {
      const items = [
        {
          id: "soul-reaper-immortal",
          type: "manhua",
          title: "Soul Reaper Immortal",
          author: "Qin Yao Studio",
          year: 2024,
          coverUrl: "https://images.unsplash.com/photo-1612036782180-6f0b6fcdc3c6?q=80&w=1200&auto=format&fit=crop",
          rating: 4.6,
          tags: ["cultivation", "dark-fantasy", "action"],
          summary: "A reaper who harvests souls to refine his Qi breaks the heavenly order.",
          body: "In a realm where death cycles into spiritual energy, a mortal reaper ascends. Pacing is brisk with lethal choreography. Art leans moody ink-wash meets neon etching.",
          createdAt: Date.now() - 1000*60*60*24*40
        },
        {
          id: "ling-cage-pilot",
          type: "donghua",
          title: "Ling Cage: Pilot Redux",
          author: "YHKT Entertainment",
          year: 2023,
          coverUrl: "https://images.unsplash.com/photo-1520975922284-9f79f0283f1b?q=80&w=1200&auto=format&fit=crop",
          rating: 4.8,
          tags: ["sci-fi", "post-apoc", "mecha"],
          summary: "Sacred-tech ruins, biohazards, and a city clinging to light.",
          body: "Phenomenal atmospheric worldbuilding. HUD overlays and sacred geometry motifs elevate tension. Minor pacing dips but visuals carry.",
          createdAt: Date.now() - 1000*60*60*24*62
        },
        {
          id: "emerald-lotus",
          type: "cosplay",
          title: "Emerald Lotus (Qinglian)",
          author: "@QingLianForge",
          year: 2025,
          coverUrl: "https://images.unsplash.com/photo-1520974955349-9b25d54f9981?q=80&w=1200&auto=format&fit=crop",
          rating: 4.7,
          tags: ["xianxia", "craft", "armor"],
          summary: "Jade-lacquer breastplate with thread-light glyphs.",
          body: "Material alchemy masterclass: painted resin + EL wire + etched runes. Photoset staged with ink mist — flawless.",
          createdAt: Date.now() - 1000*60*60*24*9
        },
        {
          id: "immersion-overclocked",
          type: "game",
          title: "Immersion Overclocked",
          author: "Reality Overdrive Studio",
          year: 2025,
          coverUrl: "https://images.unsplash.com/photo-1605901309584-818e25960a8b?q=80&w=1200&auto=format&fit=crop",
          rating: 4.4,
          tags: ["vrmmorpg", "hardcore", "systems"],
          summary: "A VR that feels *too real* — pain toggles included.",
          body: "Combat systems are punishing yet fair. Crafting loops reward mastery. Sound design slaps. Needs better new-player onboarding.",
          createdAt: Date.now() - 1000*60*60*24*3
        }
      ];
      return { items };
    })();
  </script>

  <!-- App logic -->
  <script>
    /* Immersion Realms — SPA app (single file)
       - Circular HUD home
       - List & detail views
       - Add review form
       - Search/sort/filter
       - LocalStorage persistence
       - Theme + SFX toggles
       - Qi particle background canvas
    */

    (() => {
      const $ = sel => document.querySelector(sel);
      const $$ = sel => [...document.querySelectorAll(sel)];
      const app = $("#app");
      const searchInput = $("#search");
      const clearSearchBtn = $("#clearSearch");
      const sortSel = $("#sortBy");
      const themeToggle = $("#themeToggle");
      const sfxToggle = $("#sfxToggle");
      const yearEl = $("#year");
      yearEl.textContent = new Date().getFullYear();

      /* ---------- State ---------- */
      const TYPES = ["manhua","donghua","cosplay","game"];
      const STORAGE_KEY = "IR_USER_DATA_V1";
      const store = {
        _mem: null,
        _load() {
          try {
            const raw = localStorage.getItem(STORAGE_KEY);
            if (raw) this._mem = JSON.parse(raw);
            else this._mem = { reviews: IR_SEED.items, ratings: {}, sfx: false, theme: "jade" };
          } catch {
            this._mem = { reviews: IR_SEED.items, ratings: {}, sfx: false, theme: "jade" };
          }
          // Merge seeds (avoid duplicates on updates)
          const known = new Set(this._mem.reviews.map(r => r.id));
          IR_SEED.items.forEach(r => { if (!known.has(r.id)) this._mem.reviews.push(r); });
          document.body.classList.toggle("theme-crimson", this._mem.theme === "crimson");
          document.body.classList.toggle("theme-jade", this._mem.theme !== "crimson");
          return this._mem;
        },
        get() { return this._mem || this._load(); },
        save() { try { localStorage.setItem(STORAGE_KEY, JSON.stringify(this._mem)); } catch {} }
      };
      store._load();

      /* ---------- Tiny Router ---------- */
      const routes = {
        "#/home": renderHome,
        "#/all": renderAll,
        "#/list": renderList,                // expects ?type=manhua
        "#/review": renderDetail,            // expects ?id=slug
        "#/submit": renderSubmit,
        "#/about": renderAbout
      };

      function parseHash() {
        const hash = location.hash || "#/home";
        const [path, queryString] = hash.split("?");
        const params = new URLSearchParams(queryString || "");
        return { path, params };
      }
      window.addEventListener("hashchange", () => {
        const { path } = parseHash();
        (routes[path] || renderHome)();
        app.focus({ preventScroll: true });
      });

      /* ---------- SFX (WebAudio) ---------- */
      let audioCtx;
      function playChime(freq = 660, dur = 0.08) {
        if (!store.get().sfx) return;
        try {
          audioCtx = audioCtx || new (window.AudioContext || window.webkitAudioContext)();
          const o = audioCtx.createOscillator();
          const g = audioCtx.createGain();
          o.type = "sine"; o.frequency.value = freq;
          g.gain.value = 0.06;
          o.connect(g); g.connect(audioCtx.destination);
          const t = audioCtx.currentTime;
          o.start(t);
          g.gain.exponentialRampToValueAtTime(0.0001, t + dur);
          o.stop(t + dur);
        } catch { /* ignore */ }
      }

      /* ---------- Helpers ---------- */
      function html(strings, ...vals) {
        return strings.reduce((acc, s, i) => acc + s + (vals[i] ?? ""), "");
      }
      function esc(s) { return (s+"").replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c])); }
      function fmtStars(x) { return "★".repeat(Math.round(x)) + "☆".repeat(5 - Math.round(x)); }
      function slugify(s) { return s.toLowerCase().replace(/[^a-z0-9]+/g, "-").replace(/(^-|-$)/g,""); }
      function avgRating(base, user) { return user ? (base + user) / 2 : base; }

      const getAllReviews = () => store.get().reviews.slice().sort((a,b) => b.createdAt - a.createdAt);
      const getByType = t => getAllReviews().filter(r => r.type === t);
      const getById = id => getAllReviews().find(r => r.id === id);

      /* ---------- Views ---------- */

      function renderHome() {
        if (location.hash !== "#/home") location.hash = "#/home";
        const recent = getAllReviews().slice(0, 4);
        app.innerHTML = html`
          <section class="ring-wrap" aria-label="Main circular navigation">
            <div class="ring" aria-hidden="true"></div>
            <div class="ring-center">
              <h2>🔮 Immersion Hub</h2>
              <p>Choose your path</p>
            </div>
            <div class="radial-menu">
              ${radialItem("manhua","📚","Manhua")}
              ${radialItem("donghua","🎥","Donghua")}
              ${radialItem("cosplay","🧝","Cosplay")}
              ${radialItem("game","🕹️","Games")}
            </div>
          </section>

          <section aria-label="Featured previews" class="preview-strip">
            ${recent.map(card).join("")}
          </section>
        `;

        $$(".radial-item").forEach(el => {
          el.addEventListener("click", () => {
            const t = el.dataset.type;
            playChime(720);
            location.hash = `#/list?type=${t}`;
          });
          el.addEventListener("mouseenter", () => playChime(820, 0.06));
        });

        // card click & keyboard
        $$(".card").forEach(el => {
          const go = () => { playChime(640); location.hash = `#/review?id=${el.dataset.id}`; };
          el.addEventListener("click", go);
          el.addEventListener("keydown", e => { if (e.key === "Enter" || e.key === " ") { e.preventDefault(); go(); } });
        });
      }

      const radialItem = (type, icon, label) => html`
        <button class="radial-item" data-type="${type}" aria-label="${label}">
          <span aria-hidden="true">${icon}</span>
        </button>`;

      function card(r) {
        const user = store.get().ratings[r.id];
        const rating = avgRating(r.rating, user);
        const meta = `${r.type.toUpperCase()} • ${r.author || "Unknown"} • ${r.year || "—"}`;
        return html`
          <article class="card clickable" data-id="${esc(r.id)}" role="button" tabindex="0" aria-label="${esc(r.title)}">
            <div class="thumb"><img src="${esc(r.coverUrl)}" alt="${esc(r.title)} cover"/></div>
            <h3>${esc(r.title)}</h3>
            <div class="meta">
              <span class="small">${esc(meta)}</span>
              <span class="rating small">${fmtStars(rating)} (${rating.toFixed(1)})</span>
            </div>
            <div class="tags">
              ${r.tags.slice(0,4).map(t => `<span class="tag">#${esc(t)}</span>`).join("")}
            </div>
          </article>
        `;
      }

      function renderAll() {
        const list = getAllReviews();
        app.innerHTML = html`
          <h2>All Reviews</h2>
          ${filtersBar()}
          <section class="grid">
            ${list.map(card).join("")}
          </section>
        `;
        bindCommonListHandlers();
      }

      function renderList() {
        const { params } = parseHash();
        const type = (params.get("type") || "manhua").toLowerCase();
        const valid = TYPES.includes(type) ? type : "manhua";
        const title = valid.charAt(0).toUpperCase() + valid.slice(1);
        let list = getByType(valid);
        list = applySearchSort(list);

        app.innerHTML = html`
          <h2>${esc(title)} Reviews</h2>
          ${filtersBar(valid)}
          <section class="grid">
            ${list.map(card).join("")}
          </section>
        `;
        bindCommonListHandlers(valid);
      }

      function filtersBar(activeType) {
        return html`
          <div class="controls" role="toolbar" aria-label="Filters">
            ${["manhua","donghua","cosplay","game"].map(t => {
              const label = t[0].toUpperCase() + t.slice(1);
              const active = activeType === t ? "active" : "";
              return `<a class="toggle ${active}" href="#/list?type=${t}">${label}</a>`;
            }).join("")}
            <a class="toggle" href="#/all">All</a>
            <span class="small">Tip: Use the search and sort controls in the top bar.</span>
          </div>
        `;
      }

      function applySearchSort(list) {
        const q = (searchInput.value || "").trim().toLowerCase();
        if (q) {
          list = list.filter(r =>
            r.title.toLowerCase().includes(q) ||
            (r.author||"").toLowerCase().includes(q) ||
            r.tags.some(tag => tag.toLowerCase().includes(q))
          );
        }
        switch (sortSel.value) {
          case "rating":
            list.sort((a,b) => avgRating(b.rating,store.get().ratings[b.id]) - avgRating(a.rating,store.get().ratings[a.id]));
            break;
          case "newest":
            list.sort((a,b) => b.createdAt - a.createdAt);
            break;
          case "title":
            list.sort((a,b) => a.title.localeCompare(b.title));
            break;
          default: {
            const score = r => (avgRating(r.rating,store.get().ratings[r.id])*2 + r.createdAt/1e11);
            list.sort((a,b) => score(b) - score(a));
          }
        }
        return list;
      }

      function bindCommonListHandlers(currType) {
        $$(".card").forEach(el => {
          const go = () => { playChime(640); location.hash = `#/review?id=${el.dataset.id}`; };
          el.addEventListener("click", go);
          el.addEventListener("keydown", e => { if (e.key === "Enter" || e.key === " ") { e.preventDefault(); go(); } });
        });
        if (currType) {
          $$(".toggle").forEach(t => t.classList.toggle("active", t.textContent.toLowerCase().includes(currType)));
        }
      }

      function renderDetail() {
        const { params } = parseHash();
        const id = params.get("id");
        const r = getById(id);
        if (!r) {
          app.innerHTML = `<p>Not found. <a href="#/home">Back home</a></p>`;
          return;
        }
        const user = store.get().ratings[r.id];
        const rating = avgRating(r.rating, user);
        app.innerHTML = html`
          <nav style="margin-bottom:.6rem;">
            <a class="chip" href="#/list?type=${r.type}">← Back to ${r.type}</a>
          </nav>
          <section class="detail" aria-label="Review details">
            <div class="cover"><img src="${esc(r.coverUrl)}" alt="${esc(r.title)} cover"/></div>
            <div>
              <h2>${esc(r.title)}</h2>
              <div style="display:flex; gap:.6rem; align-items:center; flex-wrap:wrap; margin:.35rem 0 .5rem;">
                <span class="rating" title="Average rating">
                  <strong>${rating.toFixed(1)}</strong>
                  <span class="stars" aria-label="Your rating">
                    ${[1,2,3,4,5].map(n => `<span class="star ${user>=n?'filled':''}" data-n="${n}">★</span>`).join("")}
                  </span>
                </span>
                <span class="small">${(r.type.toUpperCase())} • ${esc(r.author||"Unknown")} • ${esc(r.year||"—")}</span>
              </div>

              <div class="chips">
                ${r.tags.map(t => `<span class="chip">#${esc(t)}</span>`).join("")}
              </div>

              <div class="hr"></div>
              <p><em>${esc(r.summary)}</em></p>
              <p>${esc(r.body)}</p>

              <div class="actions" style="margin-top:.6rem;">
                <button class="chip" id="copyLink">🔗 Copy Link</button>
                <button class="chip" id="shareSys">📤 Share</button>
              </div>
            </div>
          </section>
        `;

        // Bind stars
        $$(".star").forEach(el => {
          el.addEventListener("click", () => {
            const n = Number(el.dataset.n);
            store.get().ratings[r.id] = n;
            store.save();
            playChime(540 + n*40, 0.09);
            renderDetail(); // re-render to update
          });
          el.addEventListener("mouseenter", () => playChime(840, 0.05));
        });

        $("#copyLink").addEventListener("click", async () => {
          const url = `${location.origin}${location.pathname}#/review?id=${r.id}`;
          try { await navigator.clipboard.writeText(url); } catch {}
          const btn = $("#copyLink");
          btn.textContent = "✅ Copied!";
          setTimeout(() => btn.textContent = "🔗 Copy Link", 1000);
          playChime(760);
        });

        $("#shareSys").addEventListener("click", async () => {
          const url = `${location.origin}${location.pathname}#/review?id=${r.id}`;
          try {
            await navigator.share({ title: r.title, text: r.summary, url });
          } catch { /* cancelled */ }
        });
      }

      function renderSubmit() {
        app.innerHTML = html`
          <h2>Submit a Review</h2>
          <form class="form" id="submitForm">
            <div class="form-row cols">
              <div>
                <label>Title</label>
                <input required name="title" placeholder="e.g. Jade Emperor's Path">
              </div>
              <div>
                <label>Type</label>
                <select name="type" required>
                  <option value="">Choose…</option>
                  <option value="manhua">Manhua</option>
                  <option value="donghua">Donghua</option>
                  <option value="cosplay">Cosplay</option>
                  <option value="game">Game</option>
                </select>
              </div>
            </div>
            <div class="form-row cols">
              <div>
                <label>Author / Creator</label>
                <input name="author" placeholder="@creator or studio">
              </div>
              <div>
                <label>Year</label>
                <input name="year" type="number" min="1900" max="2100" placeholder="2025">
              </div>
            </div>
            <div class="form-row">
              <label>Cover Image URL</label>
              <input name="coverUrl" placeholder="https://...">
              <div class="help">Use a direct image link (JPG/PNG). Optional; a placeholder is used if empty.</div>
            </div>
            <div class="form-row">
              <label>Summary</label>
              <input name="summary" placeholder="Short hook… (1–2 sentences)" maxlength="180" required>
            </div>
            <div class="form-row">
              <label>Full Review</label>
              <textarea name="body" placeholder="Write your thoughts…" required></textarea>
            </div>
            <div class="form-row">
              <label>Tags (comma‑separated)</label>
              <input name="tags" placeholder="cultivation, action, sci‑fi">
            </div>
            <div class="form-row cols">
              <div>
                <label>Initial Rating</label>
                <input name="rating" type="number" min="1" max="5" step="0.1" value="4.0">
              </div>
              <div>
                <label>&nbsp;</label>
                <button class="chip primary" type="submit">Publish</button>
              </div>
            </div>
            <p class="small">By submitting, you agree your review will be stored locally in your browser (no server). You can export your data later.</p>
          </form>
        `;

        $("#submitForm").addEventListener("submit", (e) => {
          e.preventDefault();
          const fd = new FormData(e.currentTarget);
          const title = (fd.get("title")+"").trim();
          const type = fd.get("type")+"";
          const author = (fd.get("author")+"").trim();
          const year = Number(fd.get("year")||"");
          const coverUrl = (fd.get("coverUrl")+"").trim() || "https://placehold.co/1200x675/0c1725/9ab0c6?text=Immersion+Realms";
          const summary = (fd.get("summary")+"").trim();
          const body = (fd.get("body")+"").trim();
          const tags = (fd.get("tags")+"").split(",").map(t => t.trim()).filter(Boolean);
          const rating = Math.max(1, Math.min(5, Number(fd.get("rating")||4)));

          if (!title || !type || !summary || !body) { alert("Please fill required fields."); return; }

          const id = slugify(title);
          const exists = getById(id);
          if (exists) { alert("A review with that title/slug already exists. Try a different title."); return; }

          store.get().reviews.unshift({
            id, type, title, author, year,
            coverUrl, rating: rating, tags,
            summary, body,
            createdAt: Date.now()
          });
          store.save();
          playChime(880, .12);
          location.hash = `#/review?id=${id}`;
        });
      }

      function renderAbout() {
        app.innerHTML = html`
          <h2>About</h2>
          <p>Immersion Realms is a stylized review hub for <strong>manhua</strong>, <strong>donghua</strong>, <strong>cosplayers</strong>, and <strong>video games</strong> — presented as a sci‑fi/Xianxia hybrid HUD.</p>
          <ul>
            <li>No backend; everything runs in your browser.</li>
            <li>Use <em>Add</em> to publish reviews; they persist via <code>localStorage</code>.</li>
            <li>Rate with stars; share deep links to detail pages.</li>
          </ul>
          <p class="small">Tip: Toggle <em>Theme</em> to switch Jade ↔ Crimson. Toggle <em>SFX</em> for chimes.</p>
        `;
      }

      /* ---------- Topbar binds ---------- */
      // live search UI (show/hide clear button)
      const updateClearBtn = () => { clearSearchBtn.style.display = searchInput.value ? "inline-block" : "none"; };
      updateClearBtn();

      searchInput.addEventListener("input", () => {
        updateClearBtn();
        const { path } = parseHash();
        if (path === "#/list") renderList();
        else if (path === "#/all") renderAll();
      });
      clearSearchBtn.addEventListener("click", () => {
        searchInput.value = "";
        updateClearBtn();
        const { path } = parseHash();
        if (path === "#/list") renderList();
        else if (path === "#/all") renderAll();
      });
      sortSel.addEventListener("change", () => {
        const { path } = parseHash();
        if (path === "#/list") renderList();
        else if (path === "#/all") renderAll();
      });

      const themeApply = () => {
        const s = store.get();
        document.body.classList.toggle("theme-crimson", s.theme === "crimson");
        document.body.classList.toggle("theme-jade", s.theme !== "crimson");
        themeToggle.setAttribute("aria-pressed", String(s.theme === "crimson"));
      };

      themeToggle.addEventListener("click", () => {
        const s = store.get();
        s.theme = s.theme === "crimson" ? "jade" : "crimson";
        store.save();
        themeApply();
        playChime(600);
      });
      themeApply();

      sfxToggle.addEventListener("click", () => {
        const s = store.get();
        s.sfx = !s.sfx; store.save();
        sfxToggle.classList.toggle("active", s.sfx);
        sfxToggle.setAttribute("aria-pressed", String(s.sfx));
        s.sfx && playChime(720);
      });
      if (store.get().sfx) {
        sfxToggle.classList.add("active");
        sfxToggle.setAttribute("aria-pressed", "true");
      }

      /* ---------- Qi Particle Canvas ---------- */
      const canvas = document.getElementById("qi-canvas");
      const ctx = canvas.getContext("2d", { alpha: true });
      let W, H, DPR;
      let particles = [];
      const P_COUNT_BASE = 180;

      function resize() {
        DPR = Math.min(2, window.devicePixelRatio || 1);
        W = canvas.width = Math.floor(innerWidth * DPR);
        H = canvas.height = Math.floor((innerHeight) * DPR);
        canvas.style.width = innerWidth + "px";
        canvas.style.height = innerHeight + "px";
        initParticles();
      }
      window.addEventListener("resize", resize);

      function initParticles() {
        const count = Math.round(P_COUNT_BASE * Math.min(1.4, (innerWidth * innerHeight) / (1200*800)));
        particles = Array.from({ length: count }, () => ({
          r: 0.6 + Math.random()*1.8,
          ang: Math.random() * Math.PI*2,
          rad: Math.random() * Math.min(W,H)/2,
          speed: (0.0008 + Math.random()*0.0016) * (Math.random()<.5?-1:1),
          hue: Math.random()*30 - 15
        }));
      }

      function draw() {
        ctx.clearRect(0,0,W,H);
        const cx = W/2, cy = H/2;
        const accent = getComputedStyle(document.body).getPropertyValue('--accent').trim() || "#00f0ff";
        for (const p of particles) {
          p.ang += p.speed;
          p.rad += Math.sin((performance.now()/1400) + p.ang)*0.04;
          const x = cx + Math.cos(p.ang)*p.rad;
          const y = cy + Math.sin(p.ang)*p.rad*0.62; // slight ellipse
          const g = ctx.createRadialGradient(x,y,0, x,y, 16*DPR);
          g.addColorStop(0, accent + "cc");
          g.addColorStop(1, "#00000000");
          ctx.fillStyle = g;
          ctx.beginPath();
          ctx.arc(x,y, p.r*DPR*2.2, 0, Math.PI*2);
          ctx.fill();
        }
        requestAnimationFrame(draw);
      }
      resize(); draw();

      /* ---------- Boot ---------- */
      (routes[parseHash().path] || renderHome)();
    })();
  </script>

  <noscript>
    <div style="padding:1rem; background:#111; color:#fff; text-align:center;">
      This app requires JavaScript to run. Please enable JS and reload.
    </div>
  </noscript>
</body>
</html>
