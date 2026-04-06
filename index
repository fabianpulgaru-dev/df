<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Revisor de Textos · Expresión Escrita</title>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,500;0,9..144,700;1,9..144,300;1,9..144,500&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #f4ede2; --bg2: #ebe3d4; --bg3: #e0d5c2;
  --w: #faf7f1; --ink: #1e1a14; --ink2: #3d3426; --dim: #8a7a65; --bdr: #cbbfa8;
  --plum: #5e3f72; --pl: #ede5f4; --pm: #a47fc0;
  --teal: #2a6458; --tl: #cce3df; --tm: #6fb5aa;
  --rust: #a84030; --rl: #f2e0da; --rm: #d4806a;
  --gold: #9e6e18; --gl: #f0e6cc; --gm: #c8a040;
  --ink-on-dark: rgba(255,255,255,.9);
}
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
html, body { height: 100%; background: var(--bg3); font-family: 'DM Sans', sans-serif; font-weight: 300; color: var(--ink); }

/* ── LAYOUT ── */
.app { display: grid; grid-template-columns: 340px 1fr; grid-template-rows: 60px 1fr; height: 100vh; }
.topbar { grid-column: 1 / -1; background: var(--ink); display: flex; align-items: center; padding: 0 24px; gap: 16px; border-bottom: 1px solid rgba(255,255,255,.08); }
.sidebar { background: var(--bg2); border-right: 1px solid var(--bdr); display: flex; flex-direction: column; overflow: hidden; }
.main { background: var(--bg); overflow-y: auto; display: flex; flex-direction: column; }

/* ── TOPBAR ── */
.brand { font-family: 'Fraunces', serif; font-size: 16px; color: var(--gm); font-style: italic; }
.brand span { color: rgba(255,255,255,.4); font-style: normal; font-size: 13px; margin-left: 8px; }
.topbar-right { margin-left: auto; display: flex; align-items: center; gap: 10px; }
.badge-count { background: var(--plum); color: white; font-size: 11px; padding: 3px 10px; border-radius: 100px; font-weight: 500; }

/* ── SIDEBAR ── */
.sidebar-section { padding: 16px; border-bottom: 1px solid var(--bdr); flex-shrink: 0; }
.sidebar-section h3 { font-size: 10px; letter-spacing: 3px; text-transform: uppercase; font-weight: 500; color: var(--dim); margin-bottom: 10px; }

/* Drop zone */
.dropzone { border: 2px dashed var(--bdr); border-radius: 10px; padding: 20px 16px; text-align: center; cursor: pointer; transition: all .2s; background: var(--w); }
.dropzone:hover, .dropzone.drag { border-color: var(--pm); background: var(--pl); }
.dropzone svg { width: 28px; height: 28px; margin-bottom: 8px; color: var(--dim); }
.dropzone p { font-size: 12px; color: var(--dim); line-height: 1.5; }
.dropzone strong { color: var(--plum); }
#fileInput { display: none; }

/* Student list */
.student-list { flex: 1; overflow-y: auto; padding: 8px; }
.student-item { display: flex; align-items: center; gap: 10px; padding: 10px 12px; border-radius: 8px; cursor: pointer; transition: all .2s; border: 1px solid transparent; margin-bottom: 4px; }
.student-item:hover { background: var(--w); border-color: var(--bdr); }
.student-item.active { background: var(--pl); border-color: var(--pm); }
.student-item.done { border-color: var(--tm); }
.s-avatar { width: 32px; height: 32px; border-radius: 50%; background: var(--bg3); display: flex; align-items: center; justify-content: center; font-family: 'Fraunces', serif; font-size: 14px; color: var(--dim); flex-shrink: 0; }
.student-item.done .s-avatar { background: var(--tl); color: var(--teal); }
.student-item.active .s-avatar { background: var(--pl); color: var(--plum); }
.s-info { flex: 1; min-width: 0; }
.s-name { font-size: 13px; font-weight: 500; color: var(--ink); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.s-file { font-size: 11px; color: var(--dim); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.s-status { font-size: 10px; padding: 2px 7px; border-radius: 100px; flex-shrink: 0; }
.s-status.pending { background: var(--bg3); color: var(--dim); }
.s-status.analyzing { background: var(--gl); color: var(--gold); }
.s-status.done { background: var(--tl); color: var(--teal); }
.s-status.error { background: var(--rl); color: var(--rust); }

/* Sidebar actions */
.sidebar-actions { padding: 12px; border-top: 1px solid var(--bdr); display: flex; flex-direction: column; gap: 8px; }
.btn { padding: 10px 16px; border-radius: 8px; border: none; font-family: 'DM Sans', sans-serif; font-size: 13px; font-weight: 500; cursor: pointer; transition: all .2s; display: flex; align-items: center; justify-content: center; gap: 7px; }
.btn:disabled { opacity: .4; cursor: default; }
.btn-plum { background: var(--plum); color: white; }
.btn-plum:hover:not(:disabled) { opacity: .87; }
.btn-teal { background: var(--teal); color: white; }
.btn-teal:hover:not(:disabled) { opacity: .87; }
.btn-outline { background: transparent; color: var(--ink2); border: 1px solid var(--bdr); }
.btn-outline:hover:not(:disabled) { background: var(--w); border-color: var(--pm); color: var(--plum); }

/* ── MAIN PANEL ── */
.main-empty { flex: 1; display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 12px; padding: 40px; }
.main-empty h2 { font-family: 'Fraunces', serif; font-size: 28px; color: var(--ink); font-weight: 300; }
.main-empty p { font-size: 14px; color: var(--dim); text-align: center; max-width: 360px; line-height: 1.7; }

/* Report */
.report { padding: 36px 40px; max-width: 860px; width: 100%; margin: 0 auto; }
.report-header { margin-bottom: 28px; padding-bottom: 20px; border-bottom: 1px solid var(--bdr); }
.report-header h1 { font-family: 'Fraunces', serif; font-size: 28px; font-weight: 300; color: var(--ink); margin-bottom: 6px; }
.report-header .meta { font-size: 12px; color: var(--dim); display: flex; gap: 16px; flex-wrap: wrap; }
.report-header .meta span { display: flex; align-items: center; gap: 4px; }

/* Score summary */
.score-summary { display: grid; grid-template-columns: auto 1fr 1fr; gap: 16px; margin-bottom: 28px; align-items: center; }
.score-big { text-align: center; background: var(--plum); color: white; border-radius: 14px; padding: 20px 24px; }
.score-big .num { font-family: 'Fraunces', serif; font-size: 48px; line-height: 1; margin-bottom: 4px; }
.score-big .lbl { font-size: 11px; opacity: .7; letter-spacing: 2px; text-transform: uppercase; }
.score-dim { background: var(--w); border: 1px solid var(--bdr); border-radius: 12px; padding: 16px 18px; }
.score-dim h4 { font-size: 11px; letter-spacing: 2px; text-transform: uppercase; color: var(--dim); margin-bottom: 8px; }
.score-dim .dim-num { font-family: 'Fraunces', serif; font-size: 28px; color: var(--ink); margin-bottom: 4px; }
.score-dim .dim-bar { height: 4px; border-radius: 100px; background: var(--bg3); margin-bottom: 6px; }
.score-dim .dim-bar-fill { height: 100%; border-radius: 100px; transition: width .6s; }
.score-dim .dim-nivel { font-size: 11px; font-weight: 500; }

/* Nivel colors */
.nivel-inicial { color: var(--rust); }
.nivel-desarrollo { color: var(--gold); }
.nivel-logrado { color: var(--teal); }
.nivel-destacado { color: var(--plum); }
.fill-inicial { background: var(--rm); }
.fill-desarrollo { background: var(--gm); }
.fill-logrado { background: var(--tm); }
.fill-destacado { background: var(--pm); }

/* Criterios */
.criterio-section { margin-bottom: 24px; }
.criterio-section h3 { font-family: 'Fraunces', serif; font-size: 18px; font-weight: 300; color: var(--ink); margin-bottom: 14px; padding-bottom: 8px; border-bottom: 2px solid var(--bdr); display: flex; align-items: center; gap: 10px; }
.criterio-section h3 .dim-tag { font-size: 10px; letter-spacing: 2px; text-transform: uppercase; padding: 3px 10px; border-radius: 100px; font-style: normal; }
.criterio-card { background: var(--w); border: 1px solid var(--bdr); border-radius: 10px; padding: 16px 18px; margin-bottom: 10px; }
.criterio-card.nivel-1 { border-left: 4px solid var(--rm); }
.criterio-card.nivel-2 { border-left: 4px solid var(--gm); }
.criterio-card.nivel-3 { border-left: 4px solid var(--tm); }
.criterio-card.nivel-4 { border-left: 4px solid var(--pm); }
.criterio-top { display: flex; align-items: flex-start; justify-content: space-between; gap: 12px; margin-bottom: 8px; }
.criterio-name { font-size: 13px; font-weight: 500; color: var(--ink); }
.criterio-score { display: flex; align-items: center; gap: 8px; flex-shrink: 0; }
.criterio-score .score-pill { font-size: 12px; font-weight: 600; padding: 3px 10px; border-radius: 100px; }
.criterio-fb { font-size: 13px; color: var(--ink2); line-height: 1.75; }
.criterio-fb .highlight { background: var(--gl); padding: 2px 5px; border-radius: 4px; font-size: 12px; color: var(--gold); display: inline-block; margin-bottom: 4px; }
.criterio-mejora { margin-top: 8px; background: var(--pl); border: 1px solid var(--pm); border-radius: 7px; padding: 8px 12px; font-size: 12px; color: var(--plum); line-height: 1.6; }
.criterio-mejora::before { content: '→ Para mejorar: '; font-weight: 500; }

/* Retroalimentación general */
.retro-general { background: var(--gl); border: 1px solid var(--gm); border-radius: 12px; padding: 18px 20px; margin-bottom: 24px; }
.retro-general h4 { font-size: 10px; letter-spacing: 3px; text-transform: uppercase; color: var(--gold); font-weight: 500; margin-bottom: 8px; }
.retro-general p { font-size: 14px; color: var(--ink2); line-height: 1.8; }

/* Loading */
.analyzing-state { flex: 1; display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 16px; }
.spinner { width: 40px; height: 40px; border: 3px solid var(--bdr); border-top-color: var(--plum); border-radius: 50%; animation: spin .8s linear infinite; }
@keyframes spin { to { transform: rotate(360deg); } }
.analyzing-state h3 { font-family: 'Fraunces', serif; font-size: 22px; font-weight: 300; color: var(--ink); }
.analyzing-state p { font-size: 13px; color: var(--dim); }

/* Consolidado */
.consolidado { padding: 36px 40px; max-width: 900px; width: 100%; margin: 0 auto; }
.consolidado h1 { font-family: 'Fraunces', serif; font-size: 26px; font-weight: 300; margin-bottom: 6px; }
.consolidado .meta { font-size: 12px; color: var(--dim); margin-bottom: 24px; }
.tabla-wrap { overflow-x: auto; margin-bottom: 24px; }
table { width: 100%; border-collapse: collapse; font-size: 12px; }
th { background: var(--plum); color: white; padding: 10px 12px; text-align: left; font-weight: 500; white-space: nowrap; }
td { padding: 9px 12px; border-bottom: 1px solid var(--bdr); }
tr:hover td { background: var(--pl); }
.nivel-chip { padding: 2px 8px; border-radius: 100px; font-size: 10px; font-weight: 500; white-space: nowrap; }

/* Progress bar inline */
.mini-bar { height: 6px; border-radius: 100px; background: var(--bg3); width: 60px; display: inline-block; vertical-align: middle; margin-left: 6px; overflow: hidden; }
.mini-bar-fill { height: 100%; border-radius: 100px; }
</style>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
</head>
<body>
<div class="app">

  <!-- TOPBAR -->
  <div class="topbar">
    <span class="brand">Revisor de Textos <span>Expresión Escrita 1 · UAH</span></span>
    <div class="topbar-right">
      <span class="badge-count" id="badgeCount">0 textos</span>
    </div>
  </div>

  <!-- SIDEBAR -->
  <div class="sidebar">
    <div class="sidebar-section">
      <h3>Cargar textos</h3>
      <div class="dropzone" id="dropzone" onclick="document.getElementById('fileInput').click()">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-8l-4-4m0 0L8 8m4-4v12"/></svg>
        <p><strong>Arrastra archivos aquí</strong> o haz clic<br>Word (.docx) o PDF · Uno por estudiante</p>
      </div>
      <input type="file" id="fileInput" multiple accept=".docx,.pdf,.txt,.doc">
    </div>

    <div class="sidebar-section" style="flex:1;overflow:hidden;display:flex;flex-direction:column;padding:0;">
      <div style="padding:16px 16px 8px;border-bottom:1px solid var(--bdr);flex-shrink:0;">
        <h3 style="margin:0;">Archivos cargados (<span id="totalCount">0</span>)</h3>
      </div>
      <div class="student-list" id="studentList">
        <div style="padding:20px;text-align:center;color:var(--dim);font-size:12px;">Sin archivos cargados</div>
      </div>
    </div>

    <div class="sidebar-actions">
      <button class="btn btn-plum" id="btnAnalizarTodos" disabled onclick="analizarTodos()">
        ▶ Analizar todos los textos
      </button>
      <button class="btn btn-teal" id="btnConsolidado" disabled onclick="verConsolidado()">
        ⬇ Ver informe consolidado
      </button>
      <button class="btn btn-outline" id="btnDescargaPDF" disabled onclick="descargarPDFIndividual()">
        ↓ Descargar retro en PDF
      </button>
      <button class="btn btn-outline" id="btnDescargar" disabled onclick="descargarConsolidado()">
        ↓ Descargar consolidado (.txt)
      </button>
    </div>
  </div>

  <!-- MAIN -->
  <div class="main" id="mainPanel">
    <div class="main-empty" id="emptyState">
      <svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="var(--bdr)" stroke-width="1.5"><path d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"/></svg>
      <h2>Revisor de Textos</h2>
      <p>Sube los archivos de tus estudiantes en el panel izquierdo. El sistema analizará el género argumentativo y el lenguaje académico con retroalimentación detallada por criterio.</p>
    </div>
  </div>

</div>

<script>
var students = []; // [{id, name, file, text, status, report}]
var currentId = null;
var API_URL = 'https://api.anthropic.com/v1/messages';
var ANTHROPIC_KEY = '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'; // ← reemplaza esto con tu sk-ant-...

// ── CRITERIOS ────────────────────────────────────────────────
var CRITERIOS = {
  genero: [
    { id:'c1', nombre:'Tesis o posición clara', desc:'El texto sostiene una posición identificable y sostenida a lo largo del escrito.' },
    { id:'c2', nombre:'Argumentos desarrollados', desc:'Hay argumentos que sostienen la tesis, no solo afirmaciones.' },
    { id:'c3', nombre:'Evidencia o respaldo', desc:'Los argumentos se apoyan en datos, ejemplos o referencias.' },
    { id:'c4', nombre:'Contraargumento o concesión', desc:'El texto reconoce o refuta una posición contraria.' },
    { id:'c5', nombre:'Cierre y conclusión', desc:'El texto cierra retomando la tesis con los argumentos desarrollados.' }
  ],
  lenguaje: [
    { id:'c6', nombre:'Registro formal', desc:'Evita coloquialismos, primera persona innecesaria e informalidad.' },
    { id:'c7', nombre:'Precisión léxica', desc:'Usa vocabulario específico y evita términos vagos o redundantes.' },
    { id:'c8', nombre:'Cohesión y conectores', desc:'Usa conectores argumentativos de forma correcta y variada.' },
    { id:'c9', nombre:'Distancia enunciativa', desc:'Cita, atribuye o modaliza en lugar de afirmar sin respaldo.' },
    { id:'c10', nombre:'Organización del texto', desc:'Párrafos delimitados, progresión temática clara, superestructura visible.' }
  ]
};

var NIVELES = {
  1: { label:'Inicial', cls:'nivel-inicial', fill:'fill-inicial', chip:'background:#f2e0da;color:#a84030;' },
  2: { label:'En desarrollo', cls:'nivel-desarrollo', fill:'fill-desarrollo', chip:'background:#f0e6cc;color:#9e6e18;' },
  3: { label:'Logrado', cls:'nivel-logrado', fill:'fill-logrado', chip:'background:#cce3df;color:#2a6458;' },
  4: { label:'Destacado', cls:'nivel-destacado', fill:'fill-destacado', chip:'background:#ede5f4;color:#5e3f72;' }
};

// ── UPLOAD ───────────────────────────────────────────────────
var dz = document.getElementById('dropzone');
dz.addEventListener('dragover', function(e){ e.preventDefault(); dz.classList.add('drag'); });
dz.addEventListener('dragleave', function(){ dz.classList.remove('drag'); });
dz.addEventListener('drop', function(e){
  e.preventDefault(); dz.classList.remove('drag');
  handleFiles(e.dataTransfer.files);
});
document.getElementById('fileInput').addEventListener('change', function(){
  handleFiles(this.files); this.value='';
});

function handleFiles(files) {
  Array.from(files).forEach(function(file) {
    var name = file.name.replace(/\.[^.]+$/, '').replace(/_/g,' ');
    var id = 'st_' + Date.now() + '_' + Math.random().toString(36).slice(2,6);
    var reader = new FileReader();
    reader.onload = function(e) {
      var text = '';
      if (file.name.endsWith('.txt')) {
        text = e.target.result;
      } else {
        // Para .docx y .pdf usamos el texto extraído por FileReader como base64
        // En producción usarías una librería, aquí lo manejamos como texto plano
        text = e.target.result;
      }
      var student = { id:id, name:name, fileName:file.name, text:text, status:'pending', report:null, file:file };
      students.push(student);
      renderSidebar();
      updateButtons();
    };
    // Leer como texto si es .txt, si no como DataURL para pasarlo a la API
    if (file.name.endsWith('.txt')) {
      reader.readAsText(file, 'UTF-8');
    } else {
      reader.readAsDataURL(file);
    }
  });
}

// ── SIDEBAR ──────────────────────────────────────────────────
function renderSidebar() {
  var list = document.getElementById('studentList');
  document.getElementById('totalCount').textContent = students.length;
  document.getElementById('badgeCount').textContent = students.length + ' texto' + (students.length !== 1 ? 's' : '');
  if (students.length === 0) {
    list.innerHTML = '<div style="padding:20px;text-align:center;color:var(--dim);font-size:12px;">Sin archivos cargados</div>';
    return;
  }
  list.innerHTML = students.map(function(s) {
    var initials = s.name.split(' ').slice(0,2).map(function(w){return w[0]||'';}).join('').toUpperCase();
    var statusLabel = {pending:'Pendiente',analyzing:'Analizando',done:'Listo',error:'Error'}[s.status];
    return '<div class="student-item' + (s.id===currentId?' active':'') + (s.status==='done'?' done':'') + '" onclick="selectStudent(\'' + s.id + '\')">' +
      '<div class="s-avatar">' + initials + '</div>' +
      '<div class="s-info"><div class="s-name">' + esc(s.name) + '</div><div class="s-file">' + esc(s.fileName) + '</div></div>' +
      '<span class="s-status ' + s.status + '">' + statusLabel + '</span>' +
    '</div>';
  }).join('');
}

function updateButtons() {
  var hasPending = students.some(function(s){ return s.status==='pending'; });
  var hasDone = students.some(function(s){ return s.status==='done'; });
  var currentDone = currentId && students.find(function(s){ return s.id===currentId && s.status==='done'; });
  document.getElementById('btnAnalizarTodos').disabled = !hasPending;
  document.getElementById('btnConsolidado').disabled = !hasDone;
  document.getElementById('btnDescargar').disabled = !hasDone;
  document.getElementById('btnDescargaPDF').disabled = !currentDone;
}

function selectStudent(id) {
  currentId = id;
  var s = students.find(function(x){ return x.id===id; });
  renderSidebar();
  updateButtons();
  if (s.status === 'done') renderReport(s);
  else if (s.status === 'pending') {
    showMain('<div class="main-empty"><svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="var(--bdr)" stroke-width="1.5"><path d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"/></svg><h2>' + esc(s.name) + '</h2><p style="margin-bottom:12px;">Archivo listo para analizar.</p><button class="btn btn-plum" onclick="analizarUno(\'' + s.id + '\')">▶ Analizar este texto</button></div>');
  }
}

// ── ANÁLISIS ─────────────────────────────────────────────────
function analizarTodos() {
  var pendientes = students.filter(function(s){ return s.status==='pending'; });
  if (pendientes.length === 0) return;
  pendientes.reduce(function(promise, student) {
    return promise.then(function() { return analizarUno(student.id); });
  }, Promise.resolve());
}

function analizarUno(id) {
  var s = students.find(function(x){ return x.id===id; });
  if (!s) return Promise.resolve();
  s.status = 'analyzing';
  currentId = id;
  renderSidebar();
  showMain('<div class="analyzing-state"><div class="spinner"></div><h3>Analizando texto</h3><p>Evaluando ' + esc(s.name) + ' con 10 criterios...</p></div>');
  return llamarAPI(s).then(function(report) {
    s.report = report;
    s.status = 'done';
    renderSidebar();
    renderReport(s);
    updateButtons();
  }).catch(function(err) {
    s.status = 'error';
    s.report = { error: err.toString() };
    renderSidebar();
    var esDocx = s.fileName.toLowerCase().endsWith('.docx') || s.fileName.toLowerCase().endsWith('.doc');
    var msg = esDocx
      ? '<strong>Los archivos .docx no son compatibles directamente.</strong><br><br>Soluciones:<br>① Guarda el archivo como <strong>.pdf</strong> desde Word (Archivo → Guardar como → PDF)<br>② O copia el texto y pégalo en un archivo <strong>.txt</strong>'
      : esc(err.toString());
    showMain('<div class="main-empty" style="text-align:left;align-items:flex-start;max-width:480px;margin:0 auto;">' +
      '<div style="background:var(--rl);border:1px solid var(--rm);border-radius:10px;padding:16px 18px;font-size:13px;color:var(--rust);line-height:1.7;">' + msg + '</div>' +
      '<button class="btn btn-outline" style="margin-top:12px;" onclick="analizarUno(\'' + id + '\')">Reintentar</button></div>');
    updateButtons();
  });
}

async function llamarAPI(student) {
  var textoParaAnalizar = student.text;
  var messages;

  if (textoParaAnalizar.startsWith('data:')) {
    var parts = textoParaAnalizar.split(',');
    var base64Data = parts[1];
    var isPdf = student.fileName.toLowerCase().endsWith('.pdf');

    if (isPdf) {
      // PDF: la API de Anthropic soporta documentos PDF nativamente
      messages = [{
        role: 'user',
        content: [
          {
            type: 'document',
            source: { type: 'base64', media_type: 'application/pdf', data: base64Data }
          },
          {
            type: 'text',
            text: 'Estudiante: ' + student.name + '\n\nAnaliza el texto del documento adjunto. Responde ÚNICAMENTE con el JSON especificado, sin ningún texto adicional antes o después.'
          }
        ]
      }];
    } else {
      // DOCX: no soportado nativamente — avisamos al usuario
      throw new Error('Los archivos .docx no se pueden procesar directamente. Por favor convierte el archivo a .pdf o copia el texto en un archivo .txt');
    }
  } else {
    // TXT: texto plano
    messages = [{
      role: 'user',
      content: 'Estudiante: ' + student.name + '\n\nTEXTO A ANALIZAR:\n"""\n' + textoParaAnalizar.slice(0, 10000) + '\n"""\n\nResponde ÚNICAMENTE con el JSON especificado, sin ningún texto adicional antes o después.'
    }];
  }

  var response = await fetch(API_URL, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'anthropic-version': '2023-06-01',
      'anthropic-dangerous-direct-browser-access': 'true',
      'x-api-key': ANTHROPIC_KEY
    },
    body: JSON.stringify({
      model: 'claude-sonnet-4-20250514',
      max_tokens: 2500,
      system: buildSystemPrompt(),
      messages: messages
    })
  });

  if (!response.ok) {
    var errBody = await response.text();
    throw new Error('API error ' + response.status + ': ' + errBody.slice(0, 200));
  }

  var data = await response.json();
  return parseReport(data);
}

function buildSystemPrompt() {
  return 'Eres un evaluador experto en escritura académica universitaria chilena, especializado en géneros discursivos y lenguaje académico.\n\n' +
'Tu tarea es analizar textos de estudiantes universitarios de primer año (recomendaciones escritas de 1-2 páginas) y entregar retroalimentación formativa detallada.\n\n' +
'Evalúa con estos 10 criterios exactos, escala 1-4 (1=Inicial, 2=En desarrollo, 3=Logrado, 4=Destacado):\n\n' +
'DIMENSIÓN 1 — GÉNERO ARGUMENTATIVO:\n' +
'c1: Tesis o posición clara — ¿el texto sostiene una posición identificable?\n' +
'c2: Argumentos desarrollados — ¿hay argumentos que sostienen la tesis, no solo afirmaciones?\n' +
'c3: Evidencia o respaldo — ¿los argumentos usan datos, ejemplos o referencias?\n' +
'c4: Contraargumento o concesión — ¿reconoce o refuta una posición contraria?\n' +
'c5: Cierre y conclusión — ¿el texto cierra retomando la tesis con los argumentos?\n\n' +
'DIMENSIÓN 2 — LENGUAJE ACADÉMICO:\n' +
'c6: Registro formal — ¿evita coloquialismos, primera persona innecesaria, informalidad?\n' +
'c7: Precisión léxica — ¿usa vocabulario específico y evita términos vagos?\n' +
'c8: Cohesión y conectores — ¿usa conectores argumentativos correctamente?\n' +
'c9: Distancia enunciativa — ¿cita, atribuye o modaliza en lugar de afirmar sin respaldo?\n' +
'c10: Organización del texto — ¿hay párrafos delimitados y progresión temática clara?\n\n' +
'INSTRUCCIÓN DE VOZ: Toda la retroalimentación debe estar dirigida DIRECTAMENTE al estudiante, en segunda persona (tú/tu). ' +
'Ejemplos: "Tu texto presenta...", "Lograste construir...", "Te recomiendo...", "En tu escrito se observa...". ' +
'El tono debe ser formativo, cercano y motivador — no evaluativo ni distante.\n\n' +
'INSTRUCCIÓN CRÍTICA: Responde SOLO con JSON válido. Sin texto antes ni después. Sin bloques de código markdown. Solo el objeto JSON puro.\n\n' +
'Formato exacto requerido:\n' +
'{"resumen_general":"texto aquí","criterios":{"c1":{"puntaje":2,"feedback":"texto","mejora":"texto"},"c2":{"puntaje":2,"feedback":"texto","mejora":"texto"},"c3":{"puntaje":2,"feedback":"texto","mejora":"texto"},"c4":{"puntaje":1,"feedback":"texto","mejora":"texto"},"c5":{"puntaje":2,"feedback":"texto","mejora":"texto"},"c6":{"puntaje":3,"feedback":"texto","mejora":"texto"},"c7":{"puntaje":2,"feedback":"texto","mejora":"texto"},"c8":{"puntaje":2,"feedback":"texto","mejora":"texto"},"c9":{"puntaje":1,"feedback":"texto","mejora":"texto"},"c10":{"puntaje":2,"feedback":"texto","mejora":"texto"}}}';
}

function parseReport(apiData) {
  // Extraer texto de la respuesta
  var text = '';
  if (apiData.content && Array.isArray(apiData.content)) {
    apiData.content.forEach(function(block) {
      if (block.type === 'text') text += block.text;
    });
  } else if (typeof apiData.content === 'string') {
    text = apiData.content;
  }

  // Verificar errores de la API
  if (apiData.type === 'error') {
    throw new Error('API: ' + (apiData.error && apiData.error.message ? apiData.error.message : JSON.stringify(apiData)));
  }
  if (!text) {
    throw new Error('Respuesta vacía de la API. Stop reason: ' + (apiData.stop_reason || 'desconocido'));
  }

  // Limpiar: quitar bloques markdown, espacios
  var clean = text
    .replace(/^```json\s*/i, '')
    .replace(/^```\s*/i, '')
    .replace(/\s*```\s*$/i, '')
    .trim();

  // Intentar parsear directo
  try {
    return JSON.parse(clean);
  } catch(e1) {
    // Intentar extraer el primer objeto JSON del texto
    var match = clean.match(/\{[\s\S]*\}/);
    if (match) {
      try {
        return JSON.parse(match[0]);
      } catch(e2) {
        // Mostrar el texto raw para diagnóstico
        throw new Error('JSON inválido. Respuesta recibida: ' + clean.slice(0, 300));
      }
    }
    throw new Error('No se encontró JSON en la respuesta: ' + clean.slice(0, 300));
  }
}

// ── RENDER REPORT ─────────────────────────────────────────────
function renderReport(student) {
  var r = student.report;
  if (!r || r.error) {
    showMain('<div class="main-empty"><p style="color:var(--rust);">Error en el análisis.</p></div>');
    return;
  }

  // Calcular puntajes
  var todosIds = ['c1','c2','c3','c4','c5','c6','c7','c8','c9','c10'];
  var puntajes = todosIds.map(function(id){ return (r.criterios[id] && r.criterios[id].puntaje) || 1; });
  var totalPts = puntajes.reduce(function(a,b){return a+b;},0);
  var totalMax = 40;
  var pct = Math.round(totalPts / totalMax * 100);

  var generoIds = ['c1','c2','c3','c4','c5'];
  var lenguajeIds = ['c6','c7','c8','c9','c10'];
  var ptsGenero   = generoIds.map(function(id){return r.criterios[id]?r.criterios[id].puntaje:1;}).reduce(function(a,b){return a+b;},0);
  var ptsLenguaje = lenguajeIds.map(function(id){return r.criterios[id]?r.criterios[id].puntaje:1;}).reduce(function(a,b){return a+b;},0);
  var pctG = Math.round(ptsGenero/20*100);
  var pctL = Math.round(ptsLenguaje/20*100);

  var nivelGlobal = totalPts <= 18 ? 1 : totalPts <= 27 ? 2 : totalPts <= 35 ? 3 : 4;
  var nG = NIVELES[nivelGlobal];

  var html = '<div class="report">';

  // Header
  html += '<div class="report-header">' +
    '<h1>' + esc(student.name) + '</h1>' +
    '<div class="meta">' +
    '<span>📄 ' + esc(student.fileName) + '</span>' +
    '<span>📅 ' + new Date().toLocaleDateString('es-CL') + '</span>' +
    '<span>🎯 Género argumentativo · Lenguaje académico</span>' +
    '</div></div>';

  // Score summary
  html += '<div class="score-summary">' +
    '<div class="score-big"><div class="num">' + totalPts + '</div><div style="font-size:13px;opacity:.8;margin-bottom:4px;">de 40 pts</div><div class="lbl">' + nG.label + '</div></div>' +
    '<div class="score-dim">' +
      '<h4>Género argumentativo</h4>' +
      '<div class="dim-num">' + ptsGenero + '/20</div>' +
      '<div class="dim-bar"><div class="dim-bar-fill ' + NIVELES[ptsGenero<=9?1:ptsGenero<=14?2:ptsGenero<=18?3:4].fill + '" style="width:' + pctG + '%"></div></div>' +
      '<div class="dim-nivel ' + NIVELES[ptsGenero<=9?1:ptsGenero<=14?2:ptsGenero<=18?3:4].cls + '">' + NIVELES[ptsGenero<=9?1:ptsGenero<=14?2:ptsGenero<=18?3:4].label + ' · ' + pctG + '%</div>' +
    '</div>' +
    '<div class="score-dim">' +
      '<h4>Lenguaje académico</h4>' +
      '<div class="dim-num">' + ptsLenguaje + '/20</div>' +
      '<div class="dim-bar"><div class="dim-bar-fill ' + NIVELES[ptsLenguaje<=9?1:ptsLenguaje<=14?2:ptsLenguaje<=18?3:4].fill + '" style="width:' + pctL + '%"></div></div>' +
      '<div class="dim-nivel ' + NIVELES[ptsLenguaje<=9?1:ptsLenguaje<=14?2:ptsLenguaje<=18?3:4].cls + '">' + NIVELES[ptsLenguaje<=9?1:ptsLenguaje<=14?2:ptsLenguaje<=18?3:4].label + ' · ' + pctL + '%</div>' +
    '</div>' +
  '</div>';

  // Resumen general
  if (r.resumen_general) {
    html += '<div class="retro-general"><h4>Retroalimentación general</h4><p>' + esc(r.resumen_general) + '</p></div>';
  }

  // Criterios por dimensión
  html += renderDimension('Dimensión 1 · Género argumentativo', 'background:var(--rl);color:var(--rust);', CRITERIOS.genero, r.criterios);
  html += renderDimension('Dimensión 2 · Lenguaje académico', 'background:var(--pl);color:var(--plum);', CRITERIOS.lenguaje, r.criterios);

  html += '</div>';
  showMain(html);
}

function renderDimension(titulo, tagStyle, criterios, datos) {
  var html = '<div class="criterio-section">' +
    '<h3><em style="font-style:normal;">' + titulo.split(' · ')[0] + '</em> <span class="dim-tag" style="' + tagStyle + '">' + titulo.split(' · ')[1] + '</span></h3>';
  criterios.forEach(function(c) {
    var d = datos[c.id] || { puntaje:1, feedback:'Sin datos', mejora:'' };
    var pts = d.puntaje || 1;
    var niv = NIVELES[pts];
    html += '<div class="criterio-card nivel-' + pts + '">' +
      '<div class="criterio-top">' +
        '<div>' +
          '<div class="criterio-name">' + esc(c.nombre) + '</div>' +
          '<div style="font-size:11px;color:var(--dim);margin-top:2px;">' + esc(c.desc) + '</div>' +
        '</div>' +
        '<div class="criterio-score">' +
          '<span class="score-pill" style="' + niv.chip + '">' + pts + '/4 · ' + niv.label + '</span>' +
        '</div>' +
      '</div>' +
      '<div class="criterio-fb">' + esc(d.feedback) + '</div>' +
      (d.mejora ? '<div class="criterio-mejora">' + esc(d.mejora) + '</div>' : '') +
    '</div>';
  });
  return html + '</div>';
}

// ── CONSOLIDADO ───────────────────────────────────────────────
function verConsolidado() {
  var done = students.filter(function(s){ return s.status==='done' && s.report && !s.report.error; });
  if (done.length === 0) return;

  var todosIds = ['c1','c2','c3','c4','c5','c6','c7','c8','c9','c10'];
  var allCriterios = CRITERIOS.genero.concat(CRITERIOS.lenguaje);

  var html = '<div class="consolidado">';
  html += '<h1>Informe consolidado del curso</h1>';
  html += '<div class="meta">' + done.length + ' estudiantes analizados · ' + new Date().toLocaleDateString('es-CL') + ' · Expresión Escrita 1 · UAH</div>';

  // Tabla
  html += '<div class="tabla-wrap"><table><thead><tr><th>Estudiante</th><th>Ptje</th><th>Nivel</th><th>Género<br>(1-20)</th><th>Lenguaje<br>(1-20)</th>';
  todosIds.forEach(function(id, i) { html += '<th>C' + (i+1) + '</th>'; });
  html += '</tr></thead><tbody>';

  var sumTotal = 0, sumGenero = 0, sumLenguaje = 0;
  var sumCriterios = todosIds.map(function(){return 0;});

  done.forEach(function(s) {
    var pts = todosIds.map(function(id){ return (s.report.criterios[id]&&s.report.criterios[id].puntaje)||1; });
    var total = pts.reduce(function(a,b){return a+b;},0);
    var genero = pts.slice(0,5).reduce(function(a,b){return a+b;},0);
    var lenguaje = pts.slice(5).reduce(function(a,b){return a+b;},0);
    var nivel = total<=18?1:total<=27?2:total<=35?3:4;
    var niv = NIVELES[nivel];
    sumTotal += total; sumGenero += genero; sumLenguaje += lenguaje;
    pts.forEach(function(p,i){sumCriterios[i]+=p;});

    html += '<tr><td style="font-weight:500;">' + esc(s.name) + '</td>' +
      '<td>' + total + '/40</td>' +
      '<td><span class="nivel-chip" style="' + niv.chip + '">' + niv.label + '</span></td>' +
      '<td>' + genero + ' <div class="mini-bar"><div class="mini-bar-fill ' + NIVELES[genero<=9?1:genero<=14?2:genero<=18?3:4].fill + '" style="width:' + Math.round(genero/20*100) + '%"></div></div></td>' +
      '<td>' + lenguaje + ' <div class="mini-bar"><div class="mini-bar-fill ' + NIVELES[lenguaje<=9?1:lenguaje<=14?2:lenguaje<=18?3:4].fill + '" style="width:' + Math.round(lenguaje/20*100) + '%"></div></div></td>' +
      pts.map(function(p){ return '<td><span class="nivel-chip" style="' + NIVELES[p].chip + '">' + p + '</span></td>'; }).join('') +
    '</tr>';
  });

  // Promedios
  var n = done.length;
  html += '<tr style="background:var(--pl);font-weight:500;">' +
    '<td>PROMEDIO CURSO</td>' +
    '<td>' + (sumTotal/n).toFixed(1) + '</td><td>—</td>' +
    '<td>' + (sumGenero/n).toFixed(1) + '</td>' +
    '<td>' + (sumLenguaje/n).toFixed(1) + '</td>' +
    sumCriterios.map(function(s){ return '<td>' + (s/n).toFixed(1) + '</td>'; }).join('') +
  '</tr>';

  html += '</tbody></table></div>';

  // Análisis de criterios más débiles
  var promedios = sumCriterios.map(function(s,i){ return {id:todosIds[i], nombre:allCriterios[i].nombre, avg: s/n}; });
  promedios.sort(function(a,b){return a.avg-b.avg;});
  var debiles = promedios.slice(0,3);

  html += '<div style="background:var(--gl);border:1px solid var(--gm);border-radius:12px;padding:18px 20px;">' +
    '<h4 style="font-size:10px;letter-spacing:3px;text-transform:uppercase;color:var(--gold);font-weight:500;margin-bottom:10px;">Criterios más débiles del curso</h4>';
  debiles.forEach(function(c, i) {
    html += '<div style="display:flex;align-items:center;gap:10px;margin-bottom:8px;">' +
      '<span style="font-family:\'Fraunces\',serif;font-size:20px;color:var(--gold);">' + (i+1) + '</span>' +
      '<div><div style="font-size:13px;font-weight:500;color:var(--ink);">' + esc(c.nombre) + '</div>' +
      '<div style="font-size:11px;color:var(--dim);">Promedio: ' + c.avg.toFixed(1) + '/4</div></div></div>';
  });
  html += '</div></div>';

  currentId = null;
  renderSidebar();
  showMain(html);
}

// ── DESCARGAR PDF INDIVIDUAL ──────────────────────────────────
function descargarPDFIndividual() {
  var s = currentId && students.find(function(x){ return x.id===currentId && x.status==='done'; });
  if (!s || !s.report || s.report.error) return;

  var { jsPDF } = window.jspdf;
  var doc = new jsPDF({ orientation:'portrait', unit:'mm', format:'a4' });
  var r = s.report;

  var todosIds = ['c1','c2','c3','c4','c5','c6','c7','c8','c9','c10'];
  var allCriterios = CRITERIOS.genero.concat(CRITERIOS.lenguaje);
  var pts = todosIds.map(function(id){ return (r.criterios[id]&&r.criterios[id].puntaje)||1; });
  var total = pts.reduce(function(a,b){return a+b;},0);
  var ptsGenero   = pts.slice(0,5).reduce(function(a,b){return a+b;},0);
  var ptsLenguaje = pts.slice(5).reduce(function(a,b){return a+b;},0);
  var nivelGlobal = total<=18?'Inicial':total<=27?'En desarrollo':total<=35?'Logrado':'Destacado';

  var W = 210, ml = 18, mr = 18, cw = W - ml - mr; // A4
  var y = 0;

  // Helpers
  function colorNivel(n) {
    if (n===4) return [94,63,114];
    if (n===3) return [42,100,88];
    if (n===2) return [158,110,24];
    return [168,64,48];
  }
  function addText(text, x, yy, opts) {
    opts = opts || {};
    doc.setFontSize(opts.size || 10);
    doc.setFont('helvetica', opts.style || 'normal');
    if (opts.color) doc.setTextColor.apply(doc, opts.color);
    else doc.setTextColor(30,26,20);
    var lines = doc.splitTextToSize(String(text||''), opts.maxW || cw);
    doc.text(lines, x, yy);
    return lines.length * ((opts.size||10) * 0.4 + 1.2);
  }
  function checkPage(needed) {
    if (y + needed > 272) { doc.addPage(); y = 18; }
  }

  // ── CABECERA ──
  doc.setFillColor(94,63,114);
  doc.rect(0,0,W,28,'F');
  doc.setFontSize(18); doc.setFont('helvetica','bold'); doc.setTextColor(255,255,255);
  doc.text('Retroalimentación de escritura', ml, 12);
  doc.setFontSize(10); doc.setFont('helvetica','normal'); doc.setTextColor(200,180,220);
  doc.text('Expresión Escrita 1 · Universidad Alberto Hurtado', ml, 19);
  doc.text(new Date().toLocaleDateString('es-CL'), W-mr, 19, {align:'right'});

  y = 36;

  // Nombre estudiante
  doc.setFontSize(16); doc.setFont('helvetica','bold'); doc.setTextColor(30,26,20);
  doc.text(s.name, ml, y); y += 8;
  doc.setFontSize(10); doc.setFont('helvetica','normal'); doc.setTextColor(138,122,101);
  doc.text(s.fileName, ml, y); y += 10;

  // ── PUNTAJE RESUMEN ──
  // Caja global
  doc.setFillColor(94,63,114);
  doc.roundedRect(ml, y, 38, 22, 3, 3, 'F');
  doc.setFontSize(22); doc.setFont('helvetica','bold'); doc.setTextColor(255,255,255);
  doc.text(String(total), ml+19, y+12, {align:'center'});
  doc.setFontSize(8); doc.setFont('helvetica','normal'); doc.setTextColor(200,180,220);
  doc.text('de 40 puntos', ml+19, y+18, {align:'center'});

  // Nivel badge
  var nc = colorNivel(total<=18?1:total<=27?2:total<=35?3:4);
  doc.setFillColor(nc[0],nc[1],nc[2]);
  doc.roundedRect(ml+42, y+2, 40, 8, 2, 2, 'F');
  doc.setFontSize(9); doc.setFont('helvetica','bold'); doc.setTextColor(255,255,255);
  doc.text(nivelGlobal, ml+62, y+7.5, {align:'center'});

  // Género y lenguaje
  doc.setFontSize(9); doc.setFont('helvetica','normal'); doc.setTextColor(30,26,20);
  doc.text('Género argumentativo: ' + ptsGenero + '/20', ml+42, y+16);
  doc.text('Lenguaje académico: ' + ptsLenguaje + '/20', ml+42, y+22);
  y += 30;

  // ── RETROALIMENTACIÓN GENERAL ──
  checkPage(20);
  doc.setFillColor(240,230,204);
  doc.roundedRect(ml, y, cw, 6, 2, 2, 'F');
  doc.setFontSize(8); doc.setFont('helvetica','bold'); doc.setTextColor(158,110,24);
  doc.text('RETROALIMENTACIÓN GENERAL', ml+4, y+4.2);
  y += 9;
  if (r.resumen_general) {
    var h = addText(r.resumen_general, ml, y, {size:10, maxW:cw});
    y += h + 6;
  }

  // ── CRITERIOS ──
  var dims = [
    { titulo:'Dimensión 1 · Género argumentativo', color:[168,64,48], bg:[242,224,218], criterios:CRITERIOS.genero },
    { titulo:'Dimensión 2 · Lenguaje académico',   color:[94,63,114],  bg:[237,229,244], criterios:CRITERIOS.lenguaje }
  ];

  dims.forEach(function(dim) {
    checkPage(16);
    // Título dimensión
    doc.setFillColor.apply(doc, dim.color);
    doc.rect(ml, y, cw, 7, 'F');
    doc.setFontSize(10); doc.setFont('helvetica','bold'); doc.setTextColor(255,255,255);
    doc.text(dim.titulo, ml+4, y+5);
    y += 11;

    dim.criterios.forEach(function(c) {
      var d = r.criterios[c.id] || {puntaje:1, feedback:'', mejora:''};
      var p = d.puntaje || 1;
      var nc2 = colorNivel(p);
      var nivelLabel = NIVELES[p].label;

      checkPage(24);

      // Línea izquierda de color
      doc.setFillColor.apply(doc, nc2);
      doc.rect(ml, y, 2, 18, 'F');

      // Nombre criterio + puntaje
      doc.setFontSize(10); doc.setFont('helvetica','bold'); doc.setTextColor(30,26,20);
      doc.text(c.nombre, ml+5, y+5);
      // Badge puntaje
      doc.setFillColor.apply(doc, nc2);
      doc.roundedRect(W-mr-28, y+1, 28, 6, 2, 2, 'F');
      doc.setFontSize(8); doc.setFont('helvetica','bold'); doc.setTextColor(255,255,255);
      doc.text(p+'/4 · '+nivelLabel, W-mr-14, y+5.2, {align:'center'});

      y += 8;
      // Feedback
      if (d.feedback) {
        var hFb = addText(d.feedback, ml+5, y, {size:9.5, maxW:cw-8, color:[61,52,38]});
        y += hFb + 1;
      }
      // Mejora
      if (d.mejora) {
        checkPage(10);
        doc.setFillColor.apply(doc, dim.bg);
        var mejoraLines = doc.splitTextToSize('→ Para mejorar: ' + d.mejora, cw-10);
        var mejoraH = mejoraLines.length * 4.5 + 4;
        doc.roundedRect(ml+4, y, cw-4, mejoraH, 2, 2, 'F');
        doc.setFontSize(9); doc.setFont('helvetica','normal'); doc.setTextColor.apply(doc, dim.color);
        doc.text(mejoraLines, ml+7, y+3.5);
        y += mejoraH + 3;
      }
      y += 4;
    });
    y += 4;
  });

  // ── PIE ──
  var totalPages = doc.internal.getNumberOfPages();
  for (var i = 1; i <= totalPages; i++) {
    doc.setPage(i);
    doc.setFontSize(8); doc.setFont('helvetica','normal'); doc.setTextColor(180,170,155);
    doc.text('Expresión Escrita 1 · UAH · Retroalimentación formativa', ml, 289);
    doc.text(i + '/' + totalPages, W-mr, 289, {align:'right'});
  }

  doc.save('retroalimentacion_' + s.name.replace(/\s+/g,'_').toLowerCase() + '.pdf');
}
function descargarConsolidado() {
  var done = students.filter(function(s){ return s.status==='done' && s.report && !s.report.error; });
  if (done.length === 0) return;
  var todosIds = ['c1','c2','c3','c4','c5','c6','c7','c8','c9','c10'];
  var allCriterios = CRITERIOS.genero.concat(CRITERIOS.lenguaje);

  var txt = 'INFORME CONSOLIDADO · EXPRESIÓN ESCRITA 1 · UAH\n';
  txt += 'Fecha: ' + new Date().toLocaleDateString('es-CL') + '\n';
  txt += '='.repeat(60) + '\n\n';

  done.forEach(function(s) {
    var pts = todosIds.map(function(id){ return (s.report.criterios[id]&&s.report.criterios[id].puntaje)||1; });
    var total = pts.reduce(function(a,b){return a+b;},0);
    var nivel = total<=18?'Inicial':total<=27?'En desarrollo':total<=35?'Logrado':'Destacado';
    txt += 'ESTUDIANTE: ' + s.name.toUpperCase() + '\n';
    txt += 'Puntaje total: ' + total + '/40 · Nivel: ' + nivel + '\n';
    txt += '-'.repeat(40) + '\n';
    if (s.report.resumen_general) txt += 'Retroalimentación general:\n' + s.report.resumen_general + '\n\n';
    allCriterios.forEach(function(c, i) {
      var d = s.report.criterios[c.id] || {puntaje:1,feedback:'',mejora:''};
      txt += c.nombre + ': ' + d.puntaje + '/4 · ' + NIVELES[d.puntaje||1].label + '\n';
      if (d.feedback) txt += '  → ' + d.feedback + '\n';
      if (d.mejora) txt += '  → Para mejorar: ' + d.mejora + '\n';
    });
    txt += '\n' + '='.repeat(60) + '\n\n';
  });

  var blob = new Blob([txt], {type:'text/plain;charset=utf-8'});
  var url = URL.createObjectURL(blob);
  var a = document.createElement('a');
  a.href = url; a.download = 'informe_consolidado_expresion_escrita.txt';
  a.click(); URL.revokeObjectURL(url);
}

// ── HELPERS ───────────────────────────────────────────────────
function showMain(html) {
  document.getElementById('mainPanel').innerHTML = html;
}
function esc(str) {
  return String(str||'').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');
}
</script>
</body>
</html>
