[index.html](https://github.com/user-attachments/files/32753352/index.html)
# yimeicatsitter.github.io
Cat sitting booking tool
<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Katzenbetreuung – Terminanfrage</title>
<style>
  :root{
    --bg:#faf6f0;
    --card:#ffffff;
    --text:#2b2420;
    --muted:#8a7f74;
    --border:#e7ddd0;
    --accent:#c07a4a;
    --accent-dark:#a3623a;
    --accent-soft:#f3e3d4;
    --success:#4a7c59;
    --radius:16px;
    --shadow:0 4px 20px rgba(60,40,20,0.08);
  }
  @media (prefers-color-scheme: dark){
    :root:not([data-theme="light"]){
      --bg:#1c1712;
      --card:#26201a;
      --text:#f2ece3;
      --muted:#a89a89;
      --border:#3a3128;
      --accent:#e0955f;
      --accent-dark:#c07a4a;
      --accent-soft:#3a2c1f;
      --success:#7fb894;
      --shadow:0 4px 20px rgba(0,0,0,0.3);
    }
  }
  :root[data-theme="dark"]{
    --bg:#1c1712;
    --card:#26201a;
    --text:#f2ece3;
    --muted:#a89a89;
    --border:#3a3128;
    --accent:#e0955f;
    --accent-dark:#c07a4a;
    --accent-soft:#3a2c1f;
    --success:#7fb894;
    --shadow:0 4px 20px rgba(0,0,0,0.3);
  }
  *{box-sizing:border-box;}
  html{scroll-padding-top:env(safe-area-inset-top,0px);}
  html,body{height:100%;}
  body{
    margin:0;
    background:var(--bg);
    color:var(--text);
    font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;
    padding-top:env(safe-area-inset-top,0px);
    padding-bottom:env(safe-area-inset-bottom,0px);
    -webkit-text-size-adjust:100%;
  }
  .wrap{
    max-width:480px;
    margin:0 auto;
    padding:28px 20px 60px;
  }
  .hero{
    text-align:center;
    margin-bottom:22px;
  }
  .hero .emoji{font-size:40px;display:block;margin-bottom:6px;}
  .hero h1{
    font-size:22px;
    margin:0 0 6px;
    font-weight:700;
  }
  .hero p{
    color:var(--muted);
    font-size:14px;
    margin:0;
    line-height:1.5;
  }
  .card{
    background:var(--card);
    border:1px solid var(--border);
    border-radius:var(--radius);
    box-shadow:var(--shadow);
    padding:22px 18px;
    margin-bottom:16px;
  }
  label{
    display:block;
    font-size:13px;
    font-weight:600;
    color:var(--muted);
    margin:0 0 6px;
    text-transform:uppercase;
    letter-spacing:.03em;
  }
  .field{margin-bottom:18px;}
  select,input[type="date"],textarea{
    width:100%;
    border:1.5px solid var(--border);
    background:var(--bg);
    color:var(--text);
    border-radius:12px;
    padding:12px 14px;
    font-size:16px;
    font-family:inherit;
    outline:none;
    transition:border-color .15s;
  }
  select:focus,input[type="date"]:focus,textarea:focus{
    border-color:var(--accent);
  }
  textarea{resize:vertical;min-height:64px;}
  .pill-group{
    display:flex;
    gap:8px;
    flex-wrap:wrap;
  }
  .pill{
    flex:1 1 auto;
    min-width:100px;
    text-align:center;
    padding:12px 10px;
    border-radius:12px;
    border:1.5px solid var(--border);
    background:var(--bg);
    color:var(--text);
    font-size:14px;
    font-weight:600;
    cursor:pointer;
    user-select:none;
    transition:all .15s;
  }
  .pill.active{
    background:var(--accent-soft);
    border-color:var(--accent);
    color:var(--accent-dark);
  }
  .hint{
    font-size:12.5px;
    color:var(--muted);
    margin-top:6px;
    line-height:1.4;
  }
  .send-row{
    display:flex;
    flex-direction:column;
    gap:10px;
    margin-top:6px;
  }
  button.send{
    display:flex;
    align-items:center;
    justify-content:center;
    gap:8px;
    width:100%;
    padding:15px 16px;
    border:none;
    border-radius:12px;
    font-size:15.5px;
    font-weight:700;
    cursor:pointer;
    transition:transform .1s, opacity .15s;
  }
  button.send:active{transform:scale(0.98);}
  button.send:disabled{opacity:.45;cursor:not-allowed;}
  .btn-whatsapp{background:#25D366;color:#0b3d21;}
  .btn-instagram{background:linear-gradient(135deg,#f58529,#dd2a7b,#8134af,#515bd4);color:#fff;}
  .summary{
    background:var(--accent-soft);
    border-radius:12px;
    padding:12px 14px;
    font-size:13.5px;
    color:var(--text);
    line-height:1.6;
    margin-bottom:16px;
    display:none;
  }
  .summary.show{display:block;}
  .summary b{color:var(--accent-dark);}
  footer{
    text-align:center;
    color:var(--muted);
    font-size:12px;
    margin-top:20px;
  }
  .toast{
    position:fixed;
    left:50%;
    bottom:calc(24px + env(safe-area-inset-bottom,0px));
    transform:translateX(-50%) translateY(20px);
    background:var(--success);
    color:#fff;
    padding:12px 20px;
    border-radius:999px;
    font-size:14px;
    font-weight:600;
    box-shadow:var(--shadow);
    opacity:0;
    pointer-events:none;
    transition:all .25s;
    max-width:90vw;
    text-align:center;
  }
  .toast.show{opacity:1;transform:translateX(-50%) translateY(0);}
</style>
</head>
<body>
<div class="wrap">
  <div class="hero">
    <span class="emoji">🐱</span>
    <h1>Katzenbetreuung mit Yimei</h1>
    <p>Terminanfrage senden – Yimei bestätigt dir kurz per WhatsApp oder Instagram.</p>
  </div>

  <div class="card">
    <div class="field">
      <label for="clientName">Dein Name</label>
      <input type="text" id="clientName" placeholder="Dein Name">
    </div>

    <div class="field">
      <label for="dateInput">Datum</label>
      <input type="date" id="dateInput">
    </div>

    <div class="field">
      <label>Häufigkeit</label>
      <div class="pill-group" id="freqGroup">
        <div class="pill active" data-freq="once">1× am Tag</div>
        <div class="pill" data-freq="twice">2× am Tag</div>
      </div>
    </div>

    <div class="field" id="timeField">
      <label>Uhrzeit (ungefähr)</label>
      <div class="pill-group" id="timeGroup">
        <div class="pill active" data-time="morning">Vormittags</div>
        <div class="pill" data-time="evening">Abends</div>
      </div>
      <div class="hint" id="timeHint"></div>
    </div>

    <div class="field">
      <label for="noteInput">Notiz (optional)</label>
      <textarea id="noteInput" placeholder="z. B. Wohnungsschlüssel, besondere Hinweise…"></textarea>
    </div>

    <div class="summary" id="summaryBox"></div>

    <div class="send-row">
      <button class="send btn-whatsapp" id="btnWhatsapp">📱 Per WhatsApp senden</button>
      <button class="send btn-instagram" id="btnInstagram">📷 Per Instagram senden</button>
    </div>
  </div>

  <footer>Deine Anfrage wird direkt an Yimei weitergeleitet.<br>Die Buchung gilt erst nach Bestätigung.</footer>
</div>

<div class="toast" id="toast"></div>

<script>
(function(){
  const WHATSAPP_NUMBER = "4917682543276"; // +49 176 8254 3276, no plus/spaces
  const INSTAGRAM_USERNAME = "Mayuyu_ym";

  const params = new URLSearchParams(window.location.search);
  const preClient = params.get('client');

  const clientName = document.getElementById('clientName');
  const dateInput = document.getElementById('dateInput');
  const freqGroup = document.getElementById('freqGroup');
  const timeField = document.getElementById('timeField');
  const timeGroup = document.getElementById('timeGroup');
  const timeHint = document.getElementById('timeHint');
  const noteInput = document.getElementById('noteInput');
  const summaryBox = document.getElementById('summaryBox');
  const btnWhatsapp = document.getElementById('btnWhatsapp');
  const btnInstagram = document.getElementById('btnInstagram');
  const toast = document.getElementById('toast');

  let freq = 'once';
  let time = 'morning';

  // preset client from ?client=
  if(preClient){
    clientName.value = preClient;
  }

  clientName.addEventListener('input', updateSummary);

  // default date = today
  const today = new Date();
  const pad = n => String(n).padStart(2,'0');
  dateInput.min = `${today.getFullYear()}-${pad(today.getMonth()+1)}-${pad(today.getDate())}`;
  dateInput.value = dateInput.min;

  freqGroup.addEventListener('click', (e)=>{
    const pill = e.target.closest('.pill');
    if(!pill) return;
    freq = pill.dataset.freq;
    [...freqGroup.children].forEach(p=>p.classList.toggle('active', p===pill));
    timeField.style.display = freq === 'twice' ? 'none' : '';
    timeHint.textContent = freq === 'twice' ? '' : '';
    updateSummary();
  });

  timeGroup.addEventListener('click', (e)=>{
    const pill = e.target.closest('.pill');
    if(!pill) return;
    time = pill.dataset.time;
    [...timeGroup.children].forEach(p=>p.classList.toggle('active', p===pill));
    updateSummary();
  });

  [dateInput, noteInput].forEach(el=>el.addEventListener('input', updateSummary));

  function getClientName(){
    return clientName.value.trim();
  }

  function formatDateHuman(iso){
    if(!iso) return '';
    const d = new Date(iso + 'T00:00:00');
    return d.toLocaleDateString('de-DE', { weekday:'long', day:'2-digit', month:'long', year:'numeric' });
  }

  function buildMessage(){
    const name = getClientName() || '(kein Name)';
    const dateHuman = formatDateHuman(dateInput.value);
    const freqLabel = freq === 'twice' ? '2× am Tag (vormittags & abends)' : (time === 'morning' ? '1× vormittags' : '1× abends');
    const note = noteInput.value.trim();
    let msg = `Neue Terminanfrage Katzenbetreuung\n\n`;
    msg += `Von: ${name}\n`;
    msg += `Datum: ${dateHuman}\n`;
    msg += `Häufigkeit: ${freqLabel}\n`;
    if(note) msg += `Notiz: ${note}\n`;
    return msg;
  }

  function updateSummary(){
    const name = getClientName();
    if(!name || !dateInput.value){
      summaryBox.classList.remove('show');
      return;
    }
    const freqLabel = freq === 'twice' ? '2× am Tag' : (time === 'morning' ? '1× vormittags' : '1× abends');
    summaryBox.innerHTML = `<b>${name}</b> möchte am <b>${formatDateHuman(dateInput.value)}</b> — <b>${freqLabel}</b> buchen.`;
    summaryBox.classList.add('show');
  }

  function validate(){
    if(!getClientName()){
      alert('Bitte gib deinen Namen an.');
      return false;
    }
    if(!dateInput.value){
      alert('Bitte wähle ein Datum.');
      return false;
    }
    return true;
  }

  function showToast(text){
    toast.textContent = text;
    toast.classList.add('show');
    setTimeout(()=>toast.classList.remove('show'), 3200);
  }

  function goTo(url){
    // Direct navigation is far more reliable than window.open() for
    // external deep links (wa.me, ig.me) inside mobile browsers/webviews,
    // which frequently block popups opened via window.open.
    try{
      const a = document.createElement('a');
      a.href = url;
      a.rel = 'noopener';
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      // Fallback in case the click-through didn't navigate (some webviews
      // ignore synthetic clicks on anchors without target/blank handling).
      setTimeout(()=>{ window.location.href = url; }, 60);
    } catch(e){
      window.location.href = url;
    }
  }

  btnWhatsapp.addEventListener('click', ()=>{
    if(!validate()) return;
    const text = encodeURIComponent(buildMessage());
    goTo(`https://wa.me/${WHATSAPP_NUMBER}?text=${text}`);
    showToast('WhatsApp wird geöffnet …');
  });

  btnInstagram.addEventListener('click', ()=>{
    if(!validate()) return;
    const text = buildMessage();
    const url = `https://ig.me/m/${INSTAGRAM_USERNAME}`;
    // Fire navigation immediately (same click/gesture) so it isn't blocked;
    // attempt the clipboard copy alongside it, best-effort.
    goTo(url);
    navigator.clipboard && navigator.clipboard.writeText(text).catch(()=>{});
    showToast('Instagram wird geöffnet – Text wurde kopiert, bitte einfügen & senden');
  });

  updateSummary();
})();
</script>
</body>
</html>
