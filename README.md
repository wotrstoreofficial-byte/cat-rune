　<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover" />
  <meta name="theme-color" content="#0b0b0f" />
  <title>ねこ×ルーン｜今日の運勢</title>
  <style>
    :root{
      --bg:#0b0b0f; --card:#141421; --text:#f3f3ff; --muted:#b9b9d6;
      --accent:#8df; --good:#7CFFB2; --warn:#FFD37C; --bad:#FF7CA3;
      --pad: max(14px, env(safe-area-inset-left));
      --padR: max(14px, env(safe-area-inset-right));
      --padT: max(14px, env(safe-area-inset-top));
      --padB: max(14px, env(safe-area-inset-bottom));
      --radius: 18px;
    }
    *{box-sizing:border-box; -webkit-tap-highlight-color: transparent;}
    html,body{height:100%; margin:0; font-family: -apple-system, system-ui, "Hiragino Sans", "Noto Sans JP", sans-serif; background:var(--bg); color:var(--text);}
    body{display:flex; justify-content:center; align-items:stretch;}
    .app{
      width:min(520px, 100%);
      padding: calc(var(--padT) + 10px) var(--padR) calc(var(--padB) + 14px) var(--pad);
      display:flex; flex-direction:column; gap:12px;
    }
    header{
      display:flex; justify-content:space-between; align-items:center;
      padding:10px 12px; border-radius: var(--radius);
      background:linear-gradient(180deg, rgba(141,221,255,.18), rgba(20,20,33,.6));
      border:1px solid rgba(255,255,255,.08);
    }
    header .title{font-weight:800; letter-spacing:.5px}
    header .mini{font-size:12px; color:var(--muted)}
    .card{
      background:rgba(20,20,33,.85);
      border:1px solid rgba(255,255,255,.08);
      border-radius: var(--radius);
      padding:14px;
    }
    .row{display:flex; gap:10px; align-items:center;}
    .grow{flex:1}
    input{
      width:100%; padding:12px 12px; border-radius:14px;
      border:1px solid rgba(255,255,255,.12);
      background:rgba(255,255,255,.06); color:var(--text);
      font-size:16px; outline:none;
    }
    input::placeholder{color:rgba(185,185,214,.75)}
    button{
      width:100%;
      padding:14px 14px;
      border-radius: 16px;
      border:1px solid rgba(255,255,255,.10);
      background: linear-gradient(180deg, rgba(141,221,255,.20), rgba(141,221,255,.08));
      color:var(--text);
      font-weight:800;
      font-size:16px;
      cursor:pointer;
      touch-action: manipulation;
    }
    button.secondary{
      background:rgba(255,255,255,.06);
      font-weight:700;
    }
    button:disabled{opacity:.45; cursor:not-allowed}
    .hint{font-size:13px; color:var(--muted); line-height:1.45}
    .screen{display:none; flex-direction:column; gap:12px;}
    .screen.active{display:flex;}
    .catline{
      display:flex; gap:10px; align-items:center; justify-content:space-between;
      padding:12px 14px; border-radius:16px;
      background:rgba(255,255,255,.05);
      border:1px dashed rgba(141,221,255,.25);
      font-size:14px;
    }
    .badge{
      display:inline-flex; align-items:center; gap:8px;
      padding:8px 10px; border-radius:999px;
      background:rgba(141,221,255,.12);
      border:1px solid rgba(141,221,255,.18);
      font-size:12px; color:var(--muted);
    }
    .big{
      font-size:20px; font-weight:900; letter-spacing:.3px;
    }
    .runeBox{
      padding:16px; border-radius:18px;
      background: radial-gradient(120% 120% at 50% 0%, rgba(141,221,255,.16), rgba(20,20,33,.85));
      border:1px solid rgba(255,255,255,.10);
    }
    .runeName{font-size:24px; font-weight:900}
    .runeSub{color:var(--muted); margin-top:2px; font-size:13px}
    .fort{
      margin-top:10px;
      display:flex; justify-content:space-between; align-items:center;
      gap:10px;
      padding:12px 12px;
      border-radius: 16px;
      border:1px solid rgba(255,255,255,.10);
      background:rgba(255,255,255,.05);
    }
    .fort .label{font-weight:900}
    .barWrap{
      padding:14px; border-radius:18px; border:1px solid rgba(255,255,255,.10);
      background:rgba(255,255,255,.04);
    }
    .bar{
      position:relative; height:18px; border-radius:999px; overflow:hidden;
      background:rgba(255,255,255,.08);
      border:1px solid rgba(255,255,255,.10);
    }
    .zone{
      position:absolute; top:0; bottom:0;
      left:42%; width:16%;
      background:linear-gradient(90deg, rgba(124,255,178,.20), rgba(124,255,178,.45), rgba(124,255,178,.20));
      border-left:1px solid rgba(124,255,178,.35);
      border-right:1px solid rgba(124,255,178,.35);
    }
    .marker{
      position:absolute; top:-6px; width:4px; height:30px;
      background:rgba(255,255,255,.95);
      box-shadow:0 0 10px rgba(141,221,255,.55);
      left:0%;
      transform:translateX(-50%);
      border-radius: 999px;
    }
    .scoreLine{display:flex; justify-content:space-between; color:var(--muted); font-size:13px; margin-top:10px}
    .toast{
      position:fixed; left:50%; bottom:14px;
      transform:translateX(-50%);
      background:rgba(20,20,33,.92);
      border:1px solid rgba(255,255,255,.12);
      padding:10px 12px;
      border-radius: 14px;
      font-size:13px;
      color:var(--text);
      display:none;
      max-width:min(560px, calc(100% - 24px));
    }
    .toast.show{display:block}
    .tiny{font-size:12px; color:var(--muted)}
    .two{display:grid; grid-template-columns: 1fr 1fr; gap:10px;}
    @media (max-width: 380px){ .two{grid-template-columns:1fr;} }
  </style>
</head>
<body>
  <div class="app">
    <header>
      <div>
        <div class="title">🐾 ねこ×ルーン｜今日の運勢</div>
        <div class="mini" id="todayLabel"></div>
      </div>
      <div class="badge" id="streakBadge">🔥 連続: 0日</div>
    </header>

    <!-- HOME -->
    <section class="screen active" id="home">
      <div class="card">
        <div class="big">1日1回、ねこがルーンを引く。</div>
        <p class="hint" style="margin:8px 0 0">
          先にミニゲーム（タイミングタップ）で「運の強さ」を決めてから、今日のルーンを表示します。
        </p>
      </div>

      <div class="card">
        <div class="row">
          <div class="grow">
            <div class="tiny">あなたの名前（任意）</div>
            <input id="nameInput" placeholder="例：imu / Taro / ねこ好き" maxlength="20" />
            <div class="hint" style="margin-top:8px">
              名前を入れると、同じ日でも少しだけ結果が変わります（友達同士で盛り上がる用）。
            </div>
          </div>
        </div>
      </div>

      <div class="card">
        <div class="catline">
          <div>🐱 今日のミニゲーム：<b>ゲージSTOP</b></div>
          <div class="badge">タップ1回</div>
        </div>
        <button id="startBtn">▶️ ミニゲームを始める</button>
        <div class="hint" style="margin-top:10px">
          目標は、ゲージの白い線を <span style="color:var(--good); font-weight:800;">緑ゾーン</span> に止めること。
        </div>
      </div>

      <div class="card">
        <div class="hint">
          配布のしかた：このゲームはWebなので「リンクを送るだけ」でOK。あとでホーム画面に追加もできます。
        </div>
      </div>
    </section>

    <!-- MINI GAME -->
    <section class="screen" id="mini">
      <div class="card">
        <div class="big">🎯 タップで止めて！</div>
        <div class="hint">緑ゾーンに入るほど「運の強さ」が上がるよ。</div>
      </div>

      <div class="barWrap">
        <div class="bar" aria-label="timing bar">
          <div class="zone"></div>
          <div class="marker" id="marker"></div>
        </div>
        <div class="scoreLine">
          <div>MISS</div><div>PERFECT</div><div>MISS</div>
        </div>
      </div>

      <div class="two">
        <button id="stopBtn">🖐️ いま！止める</button>
        <button class="secondary" id="cancelBtn">← 戻る</button>
      </div>

      <div class="card">
        <div class="hint">コツ：焦らないで、緑ゾーンの“真ん中”を狙う。</div>
      </div>
    </section>

    <!-- RESULT -->
    <section class="screen" id="result">
      <div class="runeBox">
        <div class="runeName" id="runeName">Fehu</div>
        <div class="runeSub" id="runeSub">ᚠ / 富・流れ・スタート</div>
        <div class="fort">
          <div>
            <div class="label" id="fortuneLabel">今日の運勢：大吉</div>
            <div class="tiny" id="powerLabel">運の強さ：92/100</div>
          </div>
          <div class="badge" id="moodBadge">😼 強運</div>
        </div>
        <div style="margin-top:12px" class="hint" id="messageText"></div>
      </div>

      <div class="card">
        <div class="big">🐾 ねこから一言</div>
        <div class="hint" id="catText" style="margin-top:8px"></div>
      </div>

      <div class="two">
        <button id="shareBtn">📤 結果を共有</button>
        <button class="secondary" id="againBtn">🔁 もう一回（練習）</button>
      </div>

      <button class="secondary" id="homeBtn">🏠 最初へ</button>

      <div class="card">
        <div class="hint">
          ※「今日の結果」は1日1回固定（名前を入れた場合はその人用に固定）。<br/>
          練習は何回でもできるけど、今日の確定結果は変わりません。
        </div>
      </div>
    </section>

    <div class="toast" id="toast"></div>
  </div>

  <script>
    // ---------- Utilities ----------
    const $ = (id) => document.getElementById(id);
    const show = (screenId) => {
      ["home","mini","result"].forEach(s => $(s).classList.remove("active"));
      $(screenId).classList.add("active");
      window.scrollTo(0,0);
    };

    const toast = (msg) => {
      const t = $("toast");
      t.textContent = msg;
      t.classList.add("show");
      setTimeout(() => t.classList.remove("show"), 2200);
    };

    // Simple seeded RNG (xorshift32)
    function xorshift32(seed){
      let x = seed >>> 0;
      return function(){
        x ^= x << 13; x >>>= 0;
        x ^= x >> 17; x >>>= 0;
        x ^= x << 5;  x >>>= 0;
        return (x >>> 0) / 4294967296;
      }
    }

    function hashStringToInt(str){
      // FNV-1a 32-bit
      let h = 2166136261;
      for(let i=0;i<str.length;i++){
        h ^= str.charCodeAt(i);
        h = Math.imul(h, 16777619);
      }
      return h >>> 0;
    }

    function ymdLocal(){
      const d = new Date();
      const y = d.getFullYear();
      const m = String(d.getMonth()+1).padStart(2,"0");
      const day = String(d.getDate()).padStart(2,"0");
      return `${y}-${m}-${day}`;
    }

    // ---------- Rune Data (Elder Futhark 24) ----------
    const RUNES = [
      {name:"Fehu",  glyph:"ᚠ", jp:"富・流れ・スタート", kw:["始める","循環","チャンス"]},
      {name:"Uruz",  glyph:"ᚢ", jp:"力・回復・根性", kw:["体力","粘り","復活"]},
      {name:"Thurisaz", glyph:"ᚦ", jp:"防御・境界・一撃", kw:["守る","決断","注意"]},
      {name:"Ansuz", glyph:"ᚨ", jp:"言葉・ひらめき・導き", kw:["会話","学び","サイン"]},
      {name:"Raidho", glyph:"ᚱ", jp:"旅・流れ・タイミング", kw:["移動","段取り","調整"]},
      {name:"Kenaz", glyph:"ᚲ", jp:"灯火・理解・創作", kw:["発見","表現","改善"]},
      {name:"Gebo", glyph:"ᚷ", jp:"贈り物・縁・交換", kw:["協力","ギブ&テイク","出会い"]},
      {name:"Wunjo", glyph:"ᚹ", jp:"喜び・調和・ご褒美", kw:["楽しい","安心","達成"]},
      {name:"Hagalaz", glyph:"ᚺ", jp:"変化・リセット・天候", kw:["切り替え","整理","荒波"]},
      {name:"Nauthiz", glyph:"ᚾ", jp:"必要・制限・忍耐", kw:["我慢","優先順位","節約"]},
      {name:"Isa", glyph:"ᛁ", jp:"静止・冷静・一点集中", kw:["止める","観察","ミニマム"]},
      {name:"Jera", glyph:"ᛃ", jp:"収穫・周期・積み上げ", kw:["継続","結果","育つ"]},
      {name:"Eihwaz", glyph:"ᛇ", jp:"芯・守り・逆境突破", kw:["折れない","長期戦","耐える"]},
      {name:"Perthro", glyph:"ᛈ", jp:"運・秘密・くじ", kw:["ガチャ","偶然","直感"]},
      {name:"Algiz", glyph:"ᛉ", jp:"守護・直感・アンテナ", kw:["守る","察知","避ける"]},
      {name:"Sowilo", glyph:"ᛋ", jp:"太陽・勝利・前進", kw:["勢い","成功","自信"]},
      {name:"Tiwaz", glyph:"ᛏ", jp:"正義・勇気・筋を通す", kw:["正攻法","決意","責任"]},
      {name:"Berkano", glyph:"ᛒ", jp:"成長・癒し・芽吹き", kw:["回復","育てる","やさしさ"]},
      {name:"Ehwaz", glyph:"ᛖ", jp:"相棒・前進・連携", kw:["チーム","信頼","進展"]},
      {name:"Mannaz", glyph:"ᛗ", jp:"人・自分・関係性", kw:["理解","交流","客観視"]},
      {name:"Laguz", glyph:"ᛚ", jp:"水・感情・流れ", kw:["柔軟","共感","漂う"]},
      {name:"Ingwaz", glyph:"ᛜ", jp:"蓄える・内側・完成", kw:["準備","熟成","区切り"]},
      {name:"Dagaz", glyph:"ᛞ", jp:"夜明け・転換・突破", kw:["好転","気づき","新局面"]},
      {name:"Othala", glyph:"ᛟ", jp:"基盤・家・受け継ぐ", kw:["土台","守る","整える"]},
    ];

    // ---------- State ----------
    const KEY = "cat_rune_daily_v1";
    const state = JSON.parse(localStorage.getItem(KEY) || "{}");

    const today = ymdLocal();
    $("todayLabel").textContent = `📅 ${today}（端末の日時 기준）`;

    // streak
    function updateStreak(){
      const last = state.lastDate;
      const streak = state.streak || 0;
      $("streakBadge").textContent = `🔥 連続: ${streak}日`;
      if(last !== today){
        $("streakBadge").style.opacity = "0.9";
      }
    }
    updateStreak();

    // ---------- Mini Game ----------
    let anim = null;
    let markerPos = 0;   // 0..100
    let dir = 1;
    let speed = 0.9;     // base speed
    let running = false;

    function startMini(){
      markerPos = 0;
      dir = 1;
      speed = 0.9 + Math.random()*0.6;
      running = true;
      const marker = $("marker");

      const loop = () => {
        if(!running) return;
        markerPos += dir * speed;
        if(markerPos >= 100){ markerPos = 100; dir = -1; }
        if(markerPos <= 0){ markerPos = 0; dir = 1; }
        marker.style.left = markerPos + "%";
        anim = requestAnimationFrame(loop);
      };
      anim = requestAnimationFrame(loop);
    }

    function stopMini(){
      running = false;
      if(anim) cancelAnimationFrame(anim);

      // Score: closer to center of green zone (50) gets higher
      const center = 50;
      const dist = Math.abs(markerPos - center); // 0..50
      let score = Math.max(0, Math.round(100 - (dist * 2.2))); // 0..100
      score = Math.min(100, Math.max(0, score));
      return score;
    }

    // ---------- Daily Result ----------
    function computeDailyResult(name, power){
      const baseKey = `${today}|${(name||"").trim().toLowerCase()}`;
      const seed = hashStringToInt(baseKey);
      const rng = xorshift32(seed);

      const runeIndex = Math.floor(rng() * RUNES.length);
      const rune = RUNES[runeIndex];

      // Fortune tier influenced by power + randomness
      const luck = Math.round((power * 0.78) + (rng()*22)); // 0..100 approx
      const tier =
        luck >= 85 ? "大吉" :
        luck >= 65 ? "中吉" :
        luck >= 45 ? "小吉" :
        luck >= 25 ? "末吉" : "凶";

      const mood =
        tier === "大吉" ? "😼 強運" :
        tier === "中吉" ? "😺 いい感じ" :
        tier === "小吉" ? "😸 まあまあ" :
        tier === "末吉" ? "😿 慎重" : "🙀 注意";

      const msgPool = [
        `キーワード：${rune.kw.join(" / ")}`,
        `今日は「${rune.kw[0]}」から入ると流れが良くなる。`,
        `遠回りに見えても「${rune.kw[1]}」が最短になる日。`,
        `迷ったら「${rune.kw[2]}」を優先。`,
      ];
      const msg = msgPool[Math.floor(rng()*msgPool.length)];

      const catPool = [
        "ねこは知ってる。焦ると、だいたい机から落ちる。",
        "ねこ的アドバイス：1つ片づけたら、1つご褒美。",
        "今日の勝ち筋は“静かにやる”。ドヤらない。",
        "運は拾うもの。まず床に落ちてるチャンスを見ろ。",
        "いちばん強いのは、やめる勇気。今日それ。",
        "なんか嫌な予感がしたら、だいたい当たる。避けろ。",
      ];
      const cat = catPool[Math.floor(rng()*catPool.length)];

      return { rune, tier, mood, luck, msg, cat };
    }

    function saveDaily(name, power, result){
      const prevDate = state.lastDate;
      if(prevDate === today){
        // already saved today: do nothing
      } else {
        // update streak
        const d0 = prevDate ? new Date(prevDate) : null;
        const d1 = new Date(today);
        let newStreak = 1;
        if(d0){
          const diff = Math.round((d1 - d0) / (1000*60*60*24));
          if(diff === 1) newStreak = (state.streak || 0) + 1;
          else newStreak = 1;
        }
        state.streak = newStreak;
        state.lastDate = today;
      }

      state.name = (name||"").trim();
      state.daily = {
        date: today,
        name: (name||"").trim(),
        power,
        runeName: result.rune.name
      };
      state.result = result;
      localStorage.setItem(KEY, JSON.stringify(state));
      updateStreak();
    }

    function renderResult(power, result){
      $("runeName").textContent = `${result.rune.name}`;
      $("runeSub").textContent = `${result.rune.glyph} / ${result.rune.jp}`;
      $("fortuneLabel").textContent = `今日の運勢：${result.tier}`;
      $("powerLabel").textContent = `運の強さ：${power}/100`;
      $("moodBadge").textContent = result.mood;
      $("messageText").textContent = result.msg;
      $("catText").textContent = result.cat;
    }

    function getName(){
      return ($("nameInput").value || "").trim();
    }

    // ---------- Buttons ----------
    $("startBtn").addEventListener("click", () => {
      // if already has today's fixed result, show it immediately
      const nm = getName();
      const stored = state.result && state.daily && state.daily.date === today && (state.daily.name || "") === nm;
      if(stored){
        renderResult(state.daily.power, state.result);
        show("result");
        toast("今日の結果を表示したよ（固定）");
        return;
      }
      show("mini");
      startMini();
    });

    $("cancelBtn").addEventListener("click", () => {
      running = false;
      if(anim) cancelAnimationFrame(anim);
      show("home");
    });

    $("stopBtn").addEventListener("click", () => {
      if(!running) return;
      const power = stopMini();

      const nm = getName();
      // If already fixed today for this name, keep fixed
      const already = state.result && state.daily && state.daily.date === today && (state.daily.name || "") === nm;
      let result;
      if(already){
        result = state.result;
        renderResult(state.daily.power, result);
        toast("今日の結果は固定だよ（練習はOK）");
      }else{
        result = computeDailyResult(nm, power);
        saveDaily(nm, power, result);
        renderResult(power, result);
        toast("結果を確定したよ！");
      }
      show("result");
    });

    $("againBtn").addEventListener("click", () => {
      show("mini");
      startMini();
    });

    $("homeBtn").addEventListener("click", () => show("home"));

    $("shareBtn").addEventListener("click", async () => {
      const nm = getName();
      const res = (state.result && state.daily && state.daily.date === today && (state.daily.name || "") === nm)
        ? state.result
        : computeDailyResult(nm, 50);

      const pwr = (state.daily && state.daily.date === today && (state.daily.name || "") === nm)
        ? state.daily.power : 50;

      const text =
`🐾 ねこ×ルーン（${today}）
${nm ? "名前: " + nm + "\n" : ""}運の強さ: ${pwr}/100
ルーン: ${res.rune.name} ${res.rune.glyph}
運勢: ${res.tier}
一言: ${res.msg}

#ねこルーン #今日の運勢`;

      // Try native share (works on iOS Safari 15+ in secure contexts)  [oai_citation:3‡みかづきブログ・カスタム](https://blog.kimizuka.org/entry/2021/09/24/124559?utm_source=chatgpt.com)
      try{
        if(navigator.share){
          await navigator.share({ title:"ねこ×ルーン｜今日の運勢", text, url: location.href });
          toast("共有したよ！");
          return;
        }
      }catch(e){
        // fall through to clipboard
      }

      try{
        await navigator.clipboard.writeText(text + "\n" + location.href);
        toast("結果をコピーしたよ（貼り付けて送ってね）");
      }catch(e){
        // last resort
        prompt("コピーして送ってね：", text + "\n" + location.href);
      }
    });

    // preload name from storage
    if(state.name) $("nameInput").value = state.name;

    // If there is already a saved result for today and same name, keep button label
    $("nameInput").addEventListener("input", () => {
      const nm = getName();
      const stored = state.result && state.daily && state.daily.date === today && (state.daily.name || "") === nm;
      $("startBtn").textContent = stored ? "📜 今日の結果を見る（固定）" : "▶️ ミニゲームを始める";
    });
    // initialize label
    $("nameInput").dispatchEvent(new Event("input"));
  </script>
</body>
</html>