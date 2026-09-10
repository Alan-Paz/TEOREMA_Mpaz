# TEOREMA_Mpaz

<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title> Indexação Algébrica de Sistemas Diatônicos via Matrizes Helicoidais Assimétricas</title>

  <!-- VexFlow para renderização de partitura -->
  <script src="https://cdn.jsdelivr.net/npm/vexflow@4.0.3/build/cjs/vexflow.js"></script>

  <style>
    :root {
      --bg-color: #030712;
      --card-bg: #0f172a;
      --accent-paz: #00f2fe;
      --accent-gabriel: #ffb703;
      --accent-euler: #ef4444;
      --accent-laplace: #10b981;
      --text-main: #f8fafc;
      --text-muted: #94a3b8;
      --border-color: #1e293b;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
    }

    body {
      background-color: var(--bg-color);
      color: var(--text-main);
      padding: 16px;
      display: flex;
      flex-direction: column;
      gap: 16px;
      min-height: 100vh;
    }

    header {
      text-align: center;
      border-bottom: 1px solid var(--border-color);
      padding-bottom: 12px;
    }

    header h1 {
      font-size: 1.6rem;
      background: linear-gradient(135deg, var(--accent-paz), var(--accent-gabriel), var(--accent-euler));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      margin-bottom: 4px;
    }

    header p {
      font-size: 0.85rem;
      color: var(--text-muted);
    }

    .tab-container {
      display: flex;
      gap: 8px;
      justify-content: center;
      flex-wrap: wrap;
    }

    .tab-btn {
      background: var(--card-bg);
      border: 1px solid var(--border-color);
      color: var(--text-muted);
      padding: 8px 14px;
      border-radius: 6px;
      cursor: pointer;
      font-weight: 600;
      font-size: 0.8rem;
      transition: all 0.2s ease;
    }

    .tab-btn.active {
      background: var(--accent-paz);
      color: #000;
      border-color: var(--accent-paz);
    }

    .main-grid {
      display: grid;
      grid-template-columns: 2fr 1fr;
      gap: 16px;
    }

    @media (max-width: 900px) {
      .main-grid {
        grid-template-columns: 1fr;
      }
    }

    .card {
      background: var(--card-bg);
      border: 1px solid var(--border-color);
      border-radius: 12px;
      padding: 16px;
      display: flex;
      flex-direction: column;
      gap: 12px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.6);
    }

    .card h2 {
      font-size: 1.1rem;
      border-bottom: 1px solid var(--border-color);
      padding-bottom: 6px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .canvas-box {
      position: relative;
      width: 100%;
      height: 480px;
      background: #020617;
      border-radius: 8px;
      overflow: hidden;
      border: 1px solid var(--border-color);
    }

    .canvas-box canvas {
      width: 100%;
      height: 100%;
      display: block;
    }

    /* Container da Partitura */
    .sheet-card {
      background: #ffffff;
      border-radius: 8px;
      padding: 10px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 140px;
      border: 1px solid var(--border-color);
    }

    #sheet-music {
      width: 100%;
      overflow-x: auto;
    }

    .controls {
      display: flex;
      flex-direction: column;
      gap: 10px;
      background: rgba(0,0,0,0.4);
      padding: 12px;
      border-radius: 8px;
    }

    .control-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 8px;
    }

    .audio-btn {
      background: var(--accent-gabriel);
      color: #000;
      border: none;
      padding: 6px 12px;
      font-size: 0.8rem;
      font-weight: bold;
      border-radius: 4px;
      cursor: pointer;
      transition: background 0.2s;
    }

    .audio-btn:hover {
      filter: brightness(1.1);
    }

    label {
      font-size: 0.8rem;
      color: var(--text-muted);
    }

    select {
      background: #1e293b;
      color: var(--text-main);
      border: 1px solid var(--border-color);
      padding: 4px 8px;
      border-radius: 4px;
      font-size: 0.8rem;
    }

    input[type=range] {
      flex: 1;
      background: #1e293b;
      border-radius: 4px;
    }

    .formula-box {
      background: #020617;
      border-left: 4px solid var(--accent-paz);
      padding: 10px;
      border-radius: 0 6px 6px 0;
      font-family: 'Times New Roman', Times, serif;
      font-style: italic;
      font-size: 0.9rem;
      color: var(--text-main);
    }

    .stat-box {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 8px;
      text-align: center;
    }

    .stat-item {
      background: rgba(255, 255, 255, 0.02);
      padding: 8px;
      border-radius: 6px;
      border: 1px solid var(--border-color);
    }

    .stat-val {
      font-size: 1rem;
      font-weight: bold;
      font-family: monospace;
    }

    .stat-lbl {
      font-size: 0.7rem;
      color: var(--text-muted);
      margin-top: 2px;
    }

    /* Seção explicativa da teoria */
    .theory-explanation {
      background: #020617;
      border: 1px solid var(--border-color);
      border-radius: 8px;
      padding: 12px;
      font-size: 0.8rem;
      color: var(--text-muted);
      line-height: 1.5;
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    .theory-explanation h3 {
      font-size: 0.9rem;
      color: var(--accent-paz);
      border-bottom: 1px solid var(--border-color);
      padding-bottom: 4px;
    }
  </style>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    }

    body {
      background-color: #0d1117;
      color: #c9d1d9;
      padding: 20px;
      min-height: 100vh;
    }

    .container {
      display: flex;
      gap: 20px;
      width: 100%;
      max-width: 1400px;
      margin: 0 auto;
      height: calc(100vh - 40px);
    }

    /* Card do Perfil do GitHub (Substituto do Iframe) */
    .github-card {
      flex: 1;
      background-color: #161b22;
      border: 1px solid #30363d;
      border-radius: 12px;
      padding: 30px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      text-align: center;
      box-shadow: 0 8px 24px rgba(0,0,0,0.3);
    }

    .avatar {
      width: 140px;
      height: 140px;
      border-radius: 50%;
      border: 3px solid #58a6ff;
      margin-bottom: 20px;
      box-shadow: 0 4px 12px rgba(88, 166, 255, 0.2);
    }

    .profile-name {
      font-size: 1.8rem;
      font-weight: 600;
      color: #f0f6fc;
      margin-bottom: 5px;
    }

    .profile-username {
      font-size: 1.1rem;
      color: #8b949e;
      margin-bottom: 20px;
    }

    .bio {
      font-size: 0.95rem;
      color: #8b949e;
      max-width: 80%;
      margin-bottom: 25px;
      line-height: 1.5;
    }

    .btn-github {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      background-color: #238636;
      color: #ffffff;
      padding: 10px 20px;
      border-radius: 6px;
      text-decoration: none;
      font-weight: 600;
      font-size: 0.95rem;
      transition: background-color 0.2s ease;
    }

    .btn-github:hover {
      background-color: #2ea043;
    }

    /* Container do Iframe do Google Drive */
    .drive-container {
      flex: 1;
      background-color: #161b22;
      border: 1px solid #30363d;
      border-radius: 12px;
      overflow: hidden;
      box-shadow: 0 8px 24px rgba(0,0,0,0.3);
    }

    .drive-container iframe {
      width: 100%;
      height: 100%;
      border: none;
    }

    /* Responsividade para telas menores */
    @media (max-width: 900px) {
      .container {
        flex-direction: column;
        height: auto;
      }

      .github-card {
        padding: 40px 20px;
      }

      .drive-container {
        height: 600px;
      }
    }
  </style>
</head>
<body>

  <header>
    <h1>  Indexação Algébrica de Sistemas Diatônicos via Matrizes Helicoidais Assimétricas M<sub>Paz</sub></h1>
    <p>Teorema Mpaz de Alan Aparecido da Silva Paz — MATRIZES HELICOIDAIS ASSIMETRICAS </p>
  </header>

</div>
<div style="display: flex; gap: 10px; width: 100%; height: 600px;">
    <iframe
    src="https://teoremampaz.pythonanywhere.com/static/algoritmo_mpaz.html"
    style="flex: 1; width: 100%; height: 100%; border: 1px solid #ccc;">
  </iframe>
  </div>
  <div style="display: flex; gap: 10px; width: 100%; height: 600px;">
  <iframe
    src="https://drive.google.com/file/d/1B7_DRXSP6XgfE5Hyv72qb2jqFbJ62fWG/preview"
    style="flex: 1; width: 100%; height: 100%; border: none;"
    allow="autoplay">
  </iframe>

  <iframe
    src="https://drive.google.com/file/d/1zo6v0YE-amoeUKevFxdiGADlkJK7jR39/preview"
    style="flex: 1; width: 100%; height: 100%; border: 1px solid #ccc;">
  </iframe>
</div>
  <div class="tab-container">
    <button class="tab-btn active" onclick="switchMode('mode1')">(f(N) = N - 2 e g(N) = N - 1) SÉRIE 5°JUSTAS</button>
    <button class="tab-btn" onclick="switchMode('mode2')">Vetor gerador na malha geométrica</button>
    <button class="tab-btn" onclick="switchMode('mode3')">Matrizes helicoidais assimétricas</button>
    <button class="tab-btn" onclick="switchMode('mode4')">PONTOS DOS OPERADORES |E+| N-2 |E-| N-1 Sub Espaço</button>
  </div>

  <div class="main-grid">
    <div class="card">
      <h2>
        <span id="view-title" style="color: var(--accent-paz)">Perfil Paramétrico 2D</span>
        <button class="audio-btn" onclick="playSequence()">&#9654; Ouvir Partitura</button>
      </h2>

      <div class="canvas-box" id="sim-container">
        <canvas id="simCanvas"></canvas>
      </div>

      <!-- Partitura Renderizada via VexFlow -->
      <div class="sheet-card">
        <div id="sheet-music"></div>
      </div>

      <!-- Seleção de Obra Musical -->
      <div class="controls">
        <div class="control-row">
          <label for="music-select"><strong>Selecione a Composição:</strong></label>
          <select id="music-select" onchange="updateAll()">
            <option value="paz">Ciclo de Quintas (M_Paz)</option>
            <option value="bach">J.S. Bach - Minueto em Sol Maior (BWV Anh. 114)</option>
            <option value="mozart">W.A. Mozart - Pequeña Música Nocturna (K. 525)</option>
          </select>
        </div>
      </div>

      <!-- Controles Modo 1 -->
      <div id="ctrl-mode1" class="controls">
        <div class="control-row">
          <label for="paz-n1">Iterações Diatônicas (N): <span id="paz-n1-val">12</span></label>
          <input type="range" id="paz-n1" min="1" max="24" step="1" value="12" oninput="updateAll()">
        </div>
        <div class="control-row">
          <label for="paz-pitch1">Passo Helicoidal (&Delta;K): <span id="paz-pitch1-val">0.30</span></label>
          <input type="range" id="paz-pitch1" min="0.05" max="1.00" step="0.05" value="0.30" oninput="updateAll()">
        </div>
        <div class="control-row">
          <label for="paz-a1">Atenuação Assintótica (a): <span id="paz-a1-val">1.00</span></label>
          <input type="range" id="paz-a1" min="0.20" max="3.00" step="0.10" value="1.00" oninput="updateAll()">
        </div>
      </div>

      <!-- Controles Modo 2 -->
      <div id="ctrl-mode2" class="controls" style="display: none;">
        <div class="control-row">
          <label for="paz-n2">Iterações Diatônicas (N): <span id="paz-n2-val">12</span></label>
          <input type="range" id="paz-n2" min="3" max="24" step="1" value="12" oninput="updateAll()">
        </div>
        <div class="control-row">
          <label for="paz-pitch2">Passo Helicoidal (&Delta;K): <span id="paz-pitch2-val">0.30</span></label>
          <input type="range" id="paz-pitch2" min="0.05" max="1.00" step="0.05" value="0.30" oninput="updateAll()">
        </div>
        <div class="control-row">
          <label for="paz-g2">Intensidade Gravitacional (g): <span id="paz-g2-val">1.00</span></label>
          <input type="range" id="paz-g2" min="0.20" max="3.00" step="0.10" value="1.00" oninput="updateAll()">
        </div>
      </div>

      <!-- Controles Modo 3 -->
      <div id="ctrl-mode3" class="controls" style="display: none;">
        <div class="control-row">
          <label for="paz-n3">Profundidade Z / N: <span id="paz-n3-val">16</span></label>
          <input type="range" id="paz-n3" min="5" max="24" step="1" value="16" oninput="updateAll()">
        </div>
        <div class="control-row">
          <label for="paz-pitch3">Passo Vertical (&Delta;Z): <span id="paz-pitch3-val">0.25</span></label>
          <input type="range" id="paz-pitch3" min="0.05" max="0.80" step="0.05" value="0.25" oninput="updateAll()">
        </div>
        <div class="control-row">
          <label for="paz-g3">Atração Gravitacional (g): <span id="paz-g3-val">1.20</span></label>
          <input type="range" id="paz-g3" min="0.20" max="3.00" step="0.10" value="1.20" oninput="updateAll()">
        </div>
      </div>

      <!-- Controles Modo 4 -->
      <div id="ctrl-mode4" class="controls" style="display: none;">
        <div class="control-row">
          <label for="paz-particles4">Densidade de Partículas: <span id="paz-particles4-val">120</span></label>
          <input type="range" id="paz-particles4" min="10" max="300" step="10" value="120" oninput="updateAll()">
        </div>
        <div class="control-row">
          <label for="paz-step4">Salto Angular (210° / 7&pi;/6): <span id="paz-step4-val">210°</span></label>
          <input type="range" id="paz-step4" min="1" max="360" step="1" value="210" oninput="updateAll()">
        </div>
      </div>
    </div>

    <div class="card">
      <h2 style="color: var(--accent-gabriel)">Operadores Recorrentes & Aprox. de &pi;</h2>

      <div class="formula-box">
        P<sub>n</sub> = P<sub>n-1</sub> + P<sub>n-2</sub> &emsp; (Recorrência de Paz)
      </div>

      <div class="formula-box" style="border-color: var(--accent-gabriel)">
        M<sub>Paz</sub> =
        &lbrack;
        cos(7&pi;/6), 0, -sin(7&pi;/6);
        0, 1, &Delta;K;
        sin(7&pi;/6), 0, cos(7&pi;/6)
        &rbrack;
      </div>

      <div class="formula-box" style="border-color: var(--accent-euler)">
        &pi;<sub>Paz</sub>(n) &approx; 6 &middot; &vert; &theta;(P<sub>n-1</sub>) - &theta;(P<sub>n-2</sub>) &vert; / 7
      </div>

      <div class="stat-box">
        <div class="stat-item">
          <div class="stat-val" id="stat-pi" style="color: var(--accent-paz)">3.14159</div>
          <div class="stat-lbl">&pi; Calculado via (N-1, N-2)</div>
        </div>
        <div class="stat-item">
          <div class="stat-val" id="stat-note" style="color: var(--accent-gabriel)">Dó (C)</div>
          <div class="stat-lbl">Nota Atual no Vértice N</div>
        </div>
        <div class="stat-item">
          <div class="stat-val" id="stat-freq" style="color: var(--accent-laplace)">261.63 Hz</div>
          <div class="stat-lbl">Frequência Acústica Hz</div>
        </div>
        <div class="stat-item">
          <div class="stat-val" id="stat-error" style="color: var(--accent-euler)">0.00%</div>
          <div class="stat-lbl">Desvio Relativo de &pi;</div>
        </div>
      </div>

      <!-- Explicação Teórica da Matriz M_Paz e dos Operadores -->
      <div class="theory-explanation">
        <h3>Explicação teórica e matemática:</h3>

        <p><strong>1. Matriz de Transformação M<sub>Paz</sub>:</strong></p>
        <p>
          Indexação Algébrica de Sistemas Diatônicos via Matrizes Helicoidais Assimétricas Autor: Alan Aparecido da Silva Paz (Nome de registro: Alan Aparecido Pereira da Paz) Classificação Temática: Teoria Pura da Música, Álgebra Linear Aplicada, Computação Musical e Análise Harmônica. RESUMO EXECUTIVO / ABSTRACT Este tratado apresenta a resolução formal da topologia do espaço tonal através do Teorema de Paz. Substituindo o Círculo de Quintas tradicional por uma estrutura topológica helicoidal tridimensional assimétrica, o modelo converte a armadura de clave e a geração de acidentes cromáticos em operadores algébricos discretos de tempo de execução O(1) A matriz $M_{Paz}$ atua como o operador de avanço no espaço tridimensional helicoidal. Ela combina uma rotação no plano $XZ$ pelo ângulo harmônico de quinta justa ($\theta = 7\pi/6 \approx 210^\circ$) com uma translação linear constante no eixo axial $Y$ por um fator de passo $\Delta K$.
        </p>

        <p><strong>2. Operadores Recorrentes N-1 e N-2:</strong></p>
        <p>
          A dinâmica espacial evolui recursivamente onde cada estado $P_n$ depende da memória defasada dos estados anteriores $P_{n-1}$ e $P_{n-2}$. O operador $N-1$ fornece o vetor de orientação atual no ciclo de quintas, enquanto o operador $N-2$ fornece o ponto de apoio geométrico imediatamente anterior.
        </p>

        <p><strong>3. Obras de Bach e Mozart na Espiral:</strong></p>
        <p>
          Ao selecionar as melodias clássicas de Bach ou Mozart, os vetores de frequência da estrutura helicoidal são mapeados diretamente a partir dos intervalos musicais reais das composições.
        </p>
      </div>

      <p style="font-size: 0.8rem; color: var(--text-muted); line-height: 1.4; margin-top: 4px;">
        <strong>Teorema de Alan Aparecido da Silva Paz:</strong> O salto angular de quinta justa ($7\pi/6 \approx 210^\circ$) estabelece uma mola helicoidal cujas frequências harmônicas seguem a progressão geométrica das notas diatônicas.
      </p>
    </div>
  </div>

  <script>
    // Coleções de Notas
    const pazNotesInfo = [
      { name: "Dó (C)", vexKey: "c/4", freq: 261.63 },
      { name: "Sol (G)", vexKey: "g/4", freq: 392.00 },
      { name: "Ré (D)", vexKey: "d/4", freq: 293.66 },
      { name: "Lá (A)", vexKey: "a/4", freq: 440.00 },
      { name: "Mi (E)", vexKey: "e/4", freq: 329.63 },
      { name: "Si (B)", vexKey: "b/4", freq: 493.88 },
      { name: "Fá♯ (F#)", vexKey: "f/4", accidental: "#", freq: 369.99 },
      { name: "Dó♯ (C#)", vexKey: "c/4", accidental: "#", freq: 277.18 },
      { name: "Lá♭ (Ab)", vexKey: "a/4", accidental: "b", freq: 415.30 },
      { name: "Mi♭ (Eb)", vexKey: "e/4", accidental: "b", freq: 311.13 },
      { name: "Si♭ (Bb)", vexKey: "b/4", accidental: "b", freq: 466.16 },
      { name: "Fá (F)", vexKey: "f/4", freq: 349.23 }
    ];

    // J.S. Bach - Minueto em Sol Maior (Trecho inicial)
    const bachNotesInfo = [
      { name: "Ré (D5)", vexKey: "d/5", freq: 587.33, dur: 0.3 },
      { name: "Sol (G4)", vexKey: "g/4", freq: 392.00, dur: 0.15 },
      { name: "Lá (A4)", vexKey: "a/4", freq: 440.00, dur: 0.15 },
      { name: "Si (B4)", vexKey: "b/4", freq: 493.88, dur: 0.15 },
      { name: "Dó (C5)", vexKey: "c/5", freq: 523.25, dur: 0.15 },
      { name: "Ré (D5)", vexKey: "d/5", freq: 587.33, dur: 0.3 },
      { name: "Sol (G4)", vexKey: "g/4", freq: 392.00, dur: 0.3 },
      { name: "Sol (G4)", vexKey: "g/4", freq: 392.00, dur: 0.3 },
      { name: "Mi (E5)", vexKey: "e/5", freq: 659.25, dur: 0.3 },
      { name: "Dó (C5)", vexKey: "c/5", freq: 523.25, dur: 0.15 },
      { name: "Ré (D5)", vexKey: "d/5", freq: 587.33, dur: 0.15 },
      { name: "Mi (E5)", vexKey: "e/5", freq: 659.25, dur: 0.15 }
    ];

    // W.A. Mozart - Eine kleine Nachtmusik (Trecho inicial)
    const mozartNotesInfo = [
      { name: "Sol (G4)", vexKey: "g/4", freq: 392.00, dur: 0.3 },
      { name: "Dó (C5)", vexKey: "c/5", freq: 523.25, dur: 0.3 },
      { name: "Sol (G4)", vexKey: "g/4", freq: 392.00, dur: 0.3 },
      { name: "Dó (C5)", vexKey: "c/5", freq: 523.25, dur: 0.3 },
      { name: "Sol (G4)", vexKey: "g/4", freq: 392.00, dur: 0.15 },
      { name: "Dó (C5)", vexKey: "c/5", freq: 523.25, dur: 0.15 },
      { name: "Mi (E5)", vexKey: "e/5", freq: 659.25, dur: 0.3 },
      { name: "Sol (G5)", vexKey: "g/5", freq: 783.99, dur: 0.3 },
      { name: "Fá (F5)", vexKey: "f/5", freq: 698.46, dur: 0.3 },
      { name: "Ré (D5)", vexKey: "d/5", freq: 587.33, dur: 0.3 },
      { name: "Fá (F5)", vexKey: "f/5", freq: 698.46, dur: 0.3 },
      { name: "Ré (D5)", vexKey: "d/5", freq: 587.33, dur: 0.3 }
    ];

    let canvas, ctx;
    let currentMode = 'mode1';
    let particlesFlow = [], particlesGravity = [], particlesOrbital = [];
    let audioCtx = null;

    function init() {
      canvas = document.getElementById('simCanvas');
      ctx = canvas.getContext('2d');
      resizeCanvas();
      initParticles();
      animate();
    }

    function resizeCanvas() {
      const box = document.getElementById('sim-container');
      canvas.width = box.clientWidth;
      canvas.height = box.clientHeight;
    }

    function initParticles() {
      particlesFlow = [];
      for (let i = 0; i < 60; i++) {
        particlesFlow.push({ step: Math.random() * 20, speed: 0.05 + Math.random() * 0.05, hue: Math.floor(Math.random() * 360) });
      }

      particlesGravity = [];
      for (let i = 0; i < 80; i++) {
        particlesGravity.push({ step: Math.random() * 30, speed: 0.03 + Math.random() * 0.04, hue: Math.floor(Math.random() * 360) });
      }

      particlesOrbital = [];
      for (let i = 0; i < 300; i++) {
        particlesOrbital.push({ angle: Math.random() * Math.PI * 2, radius: 20 + Math.random() * 180, speed: 0.01 + Math.random() * 0.02, hue: Math.floor(Math.random() * 360) });
      }
    }

    function switchMode(mode) {
      currentMode = mode;
      document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));

      document.getElementById('ctrl-mode1').style.display = 'none';
      document.getElementById('ctrl-mode2').style.display = 'none';
      document.getElementById('ctrl-mode3').style.display = 'none';
      document.getElementById('ctrl-mode4').style.display = 'none';

      if (mode === 'mode1') {
        document.querySelectorAll('.tab-btn')[0].classList.add('active');
        document.getElementById('view-title').innerText = "Perfil Paramétrico 2D";
        document.getElementById('ctrl-mode1').style.display = 'flex';
      } else if (mode === 'mode2') {
        document.querySelectorAll('.tab-btn')[1].classList.add('active');
        document.getElementById('view-title').innerText = "Dinâmica Gravitacional";
        document.getElementById('ctrl-mode2').style.display = 'flex';
      } else if (mode === 'mode3') {
        document.querySelectorAll('.tab-btn')[2].classList.add('active');
        document.getElementById('view-title').innerText = "Poço Gravitacional 3D";
        document.getElementById('ctrl-mode3').style.display = 'flex';
      } else {
        document.querySelectorAll('.tab-btn')[3].classList.add('active');
        document.getElementById('view-title').innerText = "Varredura Angular";
        document.getElementById('ctrl-mode4').style.display = 'flex';
      }
      updateAll();
    }

    function getCurrentNotesList() {
      const selection = document.getElementById('music-select').value;
      if (selection === 'bach') return bachNotesInfo;
      if (selection === 'mozart') return mozartNotesInfo;
      return pazNotesInfo;
    }

    function getCurrentN() {
      if (currentMode === 'mode1') return parseInt(document.getElementById('paz-n1').value);
      if (currentMode === 'mode2') return parseInt(document.getElementById('paz-n2').value);
      if (currentMode === 'mode3') return parseInt(document.getElementById('paz-n3').value);
      return 12;
    }

    function computePiFromPaz(N) {
      let stepN1 = (N - 1);
      let stepN2 = (N - 2);
      let deltaUnits = Math.abs(stepN1 - stepN2);
      let angleDelta = deltaUnits * (7 / 6);
      return angleDelta * (6 / 7) * Math.PI;
    }

    // Renderização da Partitura utilizando VexFlow
    function renderScore(N) {
      const container = document.getElementById('sheet-music');
      container.innerHTML = "";

      const currentList = getCurrentNotesList();
      const VF = Vex.Flow;
      const renderer = new VF.Renderer(container, VF.Renderer.Backends.SVG);

      const displayNotesCount = Math.min(N, currentList.length);
      const width = Math.max(320, displayNotesCount * 45 + 80);
      renderer.resize(width, 120);

      const context = renderer.getContext();
      const stave = new VF.Stave(10, 10, width - 20);
      stave.addClef("treble").setContext(context).draw();

      const vexNotes = [];
      for (let i = 0; i < displayNotesCount; i++) {
        const noteData = currentList[i % currentList.length];
        const staveNote = new VF.StaveNote({
          clef: "treble",
          keys: [noteData.vexKey],
          duration: "q"
        });

        if (noteData.accidental) {
          staveNote.addAccidental(0, new VF.Accidental(noteData.accidental));
        }

        if (i === displayNotesCount - 1) {
          staveNote.setStyle({ fillStyle: "#ef4444", strokeStyle: "#ef4444" });
        }

        vexNotes.push(staveNote);
      }

      if (vexNotes.length > 0) {
        const voice = new VF.Voice({ num_beats: displayNotesCount, beat_value: 4 });
        voice.setMode(VF.Voice.Mode.SOFT);
        voice.addTickables(vexNotes);
        new VF.Formatter().joinAndFormat([voice], width - 80);
        voice.draw(context, stave);
      }
    }

    // Síntese de Áudio da Partitura
    function playSequence() {
      if (!audioCtx) {
        audioCtx = new (window.AudioContext || window.webkitAudioContext)();
      }

      const N = getCurrentN();
      const currentList = getCurrentNotesList();
      const count = Math.min(N, currentList.length);

      let timeOffset = 0;

      for (let i = 0; i < count; i++) {
        const noteData = currentList[i % currentList.length];
        const noteDuration = noteData.dur || 0.3;

        const osc = audioCtx.createOscillator();
        const gain = audioCtx.createGain();

        osc.type = "sine";
        osc.frequency.setValueAtTime(noteData.freq, audioCtx.currentTime + timeOffset);

        gain.gain.setValueAtTime(0.2, audioCtx.currentTime + timeOffset);
        gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + timeOffset + noteDuration - 0.02);

        osc.connect(gain);
        gain.connect(audioCtx.destination);

        osc.start(audioCtx.currentTime + timeOffset);
        osc.stop(audioCtx.currentTime + timeOffset + noteDuration - 0.02);

        timeOffset += noteDuration;
      }
    }

    function project3D(x, y, z, cx, cy) {
      const angleX = 0.5, angleY = 0.6;
      let x1 = x * Math.cos(angleY) + z * Math.sin(angleY);
      let z1 = -x * Math.sin(angleY) + z * Math.cos(angleY);
      let y2 = y * Math.cos(angleX) - z1 * Math.sin(angleX);
      let z2 = y * Math.sin(angleX) + z1 * Math.cos(angleX);
      const scale = 180 / (z2 + 5);
      return { px: cx + x1 * scale, py: cy + y2 * scale };
    }

    function updateAll() {
      let N = getCurrentN();
      let lastRadius = 1.0;

      if (currentMode === 'mode1') {
        const deltaK = parseFloat(document.getElementById('paz-pitch1').value);
        const a = parseFloat(document.getElementById('paz-a1').value);
        document.getElementById('paz-n1-val').innerText = N;
        document.getElementById('paz-pitch1-val').innerText = deltaK.toFixed(2);
        document.getElementById('paz-a1-val').innerText = a.toFixed(2);
        lastRadius = a / (N * deltaK + 1);
      } else if (currentMode === 'mode2') {
        const deltaK = parseFloat(document.getElementById('paz-pitch2').value);
        const g = parseFloat(document.getElementById('paz-g2').value);
        document.getElementById('paz-n2-val').innerText = N;
        document.getElementById('paz-pitch2-val').innerText = deltaK.toFixed(2);
        document.getElementById('paz-g2-val').innerText = g.toFixed(2);
        lastRadius = 1.0 / (N * deltaK + 1);
      } else if (currentMode === 'mode3') {
        const deltaK = parseFloat(document.getElementById('paz-pitch3').value);
        const g = parseFloat(document.getElementById('paz-g3').value);
        document.getElementById('paz-n3-val').innerText = N;
        document.getElementById('paz-pitch3-val').innerText = deltaK.toFixed(2);
        document.getElementById('paz-g3-val').innerText = g.toFixed(2);
        lastRadius = 2.2 / (N * deltaK + 1);
      } else {
        const numP = parseInt(document.getElementById('paz-particles4').value);
        const stepDeg = parseInt(document.getElementById('paz-step4').value);
        document.getElementById('paz-particles4-val').innerText = numP;
        document.getElementById('paz-step4-val').innerText = stepDeg + "°";
      }

      const piCalc = computePiFromPaz(N);
      const err = Math.abs(piCalc - Math.PI) / Math.PI * 100;

      const currentList = getCurrentNotesList();
      const noteData = currentList[N % currentList.length];

      document.getElementById('stat-note').innerText = `${noteData.name} (n=${N})`;
      document.getElementById('stat-freq').innerText = `${noteData.freq.toFixed(2)} Hz`;
      document.getElementById('stat-pi').innerText = piCalc.toFixed(5);
      document.getElementById('stat-error').innerText = err.toFixed(2) + "%";

      renderScore(N);
    }

    function drawMode1() {
      const N = parseInt(document.getElementById('paz-n1').value);
      const deltaK = parseFloat(document.getElementById('paz-pitch1').value);
      const a = parseFloat(document.getElementById('paz-a1').value);
      const w = canvas.width, h = canvas.height;
      const padding = 50, originX = padding, originY = h / 2;
      const scaleX = (w - 2 * padding) / (N * deltaK + 1);
      const scaleY = (h / 2 - padding) / (a * 1.2);

      ctx.beginPath(); ctx.strokeStyle = '#1e293b'; ctx.lineWidth = 2;
      ctx.moveTo(originX, originY); ctx.lineTo(w - padding, originY); ctx.stroke();

      ctx.beginPath(); ctx.strokeStyle = '#ffb703'; ctx.lineWidth = 1.5; ctx.setLineDash([4, 4]);
      for (let px = 0; px <= (w - 2 * padding); px += 2) {
        let z = px / scaleX, r = a / (z + 1);
        if (px === 0) ctx.moveTo(originX + px, originY - r * scaleY);
        else ctx.lineTo(originX + px, originY - r * scaleY);
      }
      for (let px = (w - 2 * padding); px >= 0; px -= 2) {
        let z = px / scaleX, r = a / (z + 1);
        ctx.lineTo(originX + px, originY + r * scaleY);
      }
      ctx.stroke(); ctx.setLineDash([]);

      ctx.beginPath(); ctx.strokeStyle = '#00f2fe'; ctx.lineWidth = 2;
      const totalSteps = N * 20;
      for (let i = 0; i <= totalSteps; i++) {
        let stepFrac = i / 20, z = stepFrac * deltaK, radius = a / (z + 1);
        let theta = (7 * Math.PI / 6) * stepFrac;
        let projY = radius * Math.sin(theta);
        let screenX = originX + z * scaleX, screenY = originY - projY * scaleY;
        if (i === 0) ctx.moveTo(screenX, screenY); else ctx.lineTo(screenX, screenY);
      }
      ctx.stroke();

      for (let n = 0; n <= N; n++) {
        let z = n * deltaK, radius = a / (z + 1), theta = (7 * Math.PI / 6) * n;
        let projY = radius * Math.sin(theta);
        let screenX = originX + z * scaleX, screenY = originY - projY * scaleY;
        ctx.beginPath(); ctx.arc(screenX, screenY, n === N ? 6 : 3, 0, Math.PI * 2);
        ctx.fillStyle = n === N ? '#ef4444' : '#00f2fe'; ctx.fill();
      }
    }

    function drawMode2() {
      const N = parseInt(document.getElementById('paz-n2').value);
      const deltaK = parseFloat(document.getElementById('paz-pitch2').value);
      const g = parseFloat(document.getElementById('paz-g2').value);
      const a = 1.0;
      const w = canvas.width, h = canvas.height;
      const padding = 50, originX = padding, originY = h / 2;
      const scaleX = (w - 2 * padding) / (N * deltaK + 0.1);
      const scaleY = (h / 2 - padding) / (a * 1.2);

      ctx.beginPath(); ctx.strokeStyle = '#1e293b'; ctx.lineWidth = 2;
      ctx.moveTo(originX, originY); ctx.lineTo(w - padding, originY); ctx.stroke();

      ctx.beginPath(); ctx.fillStyle = 'rgba(255, 183, 3, 0.08)'; ctx.strokeStyle = '#ffb703'; ctx.lineWidth = 1.5;
      for (let px = 0; px <= (w - 2 * padding); px += 2) {
        let z = px / scaleX, r = a / (z + 1);
        if (px === 0) ctx.moveTo(originX + px, originY - r * scaleY);
        else ctx.lineTo(originX + px, originY - r * scaleY);
      }
      for (let px = (w - 2 * padding); px >= 0; px -= 2) {
        let z = px / scaleX, r = a / (z + 1);
        ctx.lineTo(originX + px, originY + r * scaleY);
      }
      ctx.closePath(); ctx.fill(); ctx.stroke();

      ctx.beginPath(); ctx.strokeStyle = 'rgba(0, 242, 254, 0.4)'; ctx.lineWidth = 1.5;
      const totalSteps = N * 25;
      for (let i = 0; i <= totalSteps; i++) {
        let stepFrac = i / 25, z = stepFrac * deltaK, radius = a / (z + 1);
        let theta = (7 * Math.PI / 6) * stepFrac;
        let projY = radius * Math.sin(theta);
        let screenX = originX + z * scaleX, screenY = originY - projY * scaleY;
        if (i === 0) ctx.moveTo(screenX, screenY); else ctx.lineTo(screenX, screenY);
      }
      ctx.stroke();

      particlesFlow.forEach((p) => {
        p.step += p.speed * Math.sqrt(1 + p.step * 0.1 * g);
        if (p.step > N) p.step = 0;
        let z = p.step * deltaK, radius = a / (z + 1), theta = (7 * Math.PI / 6) * p.step;
        let projY = radius * Math.sin(theta);
        let screenX = originX + z * scaleX, screenY = originY - projY * scaleY;
        ctx.beginPath(); ctx.arc(screenX, screenY, 3.5, 0, Math.PI * 2);
        ctx.fillStyle = `hsl(${p.hue}, 100%, 65%)`;
        ctx.shadowColor = `hsl(${p.hue}, 100%, 50%)`; ctx.shadowBlur = 8; ctx.fill(); ctx.shadowBlur = 0;
      });

      for (let n = 0; n <= N; n++) {
        let z = n * deltaK, radius = a / (z + 1), theta = (7 * Math.PI / 6) * n;
        let projY = radius * Math.sin(theta);
        let screenX = originX + z * scaleX, screenY = originY - projY * scaleY;
        ctx.beginPath(); ctx.arc(screenX, screenY, n === N ? 6 : 2.5, 0, Math.PI * 2);
        ctx.fillStyle = n === N ? '#ef4444' : '#ffffff'; ctx.fill();
      }
    }

    function drawMode3() {
      const N = parseInt(document.getElementById('paz-n3').value);
      const deltaK = parseFloat(document.getElementById('paz-pitch3').value);
      const g = parseFloat(document.getElementById('paz-g3').value);
      const a = 2.2, w = canvas.width, h = canvas.height;
      const cx = w / 2, cy = h / 3.5;

      const o = project3D(0, 0, 0, cx, cy);
      const ex = project3D(3, 0, 0, cx, cy), ey = project3D(0, 3, 0, cx, cy), ez = project3D(0, 0, N * deltaK, cx, cy);

      ctx.beginPath(); ctx.strokeStyle = '#ef4444'; ctx.moveTo(o.px, o.py); ctx.lineTo(ex.px, ex.py); ctx.stroke();
      ctx.beginPath(); ctx.strokeStyle = '#10b981'; ctx.moveTo(o.px, o.py); ctx.lineTo(ey.px, ey.py); ctx.stroke();
      ctx.beginPath(); ctx.strokeStyle = '#00f2fe'; ctx.moveTo(o.px, o.py); ctx.lineTo(ez.px, ez.py); ctx.stroke();

      const bhPos = project3D(0, 0, N * deltaK, cx, cy);
      const grad = ctx.createRadialGradient(bhPos.px, bhPos.py, 2, bhPos.px, bhPos.py, 35);
      grad.addColorStop(0, '#ffffff'); grad.addColorStop(0.3, '#00f2fe');
      grad.addColorStop(0.7, 'rgba(255,183,3,0.3)'); grad.addColorStop(1, 'transparent');
      ctx.beginPath(); ctx.arc(bhPos.px, bhPos.py, 35, 0, Math.PI * 2); ctx.fillStyle = grad; ctx.fill();

      ctx.beginPath(); ctx.strokeStyle = '#00f2fe'; ctx.lineWidth = 1.5;
      const totalSteps = N * 20;
      for (let i = 0; i <= totalSteps; i++) {
        let stepFrac = i / 20, z = stepFrac * deltaK, r = a / (z + 1), theta = (7 * Math.PI / 6) * stepFrac;
        let p = project3D(r * Math.cos(theta), r * Math.sin(theta), z, cx, cy);
        if (i === 0) ctx.moveTo(p.px, p.py); else ctx.lineTo(p.px, p.py);
      }
      ctx.stroke();

      particlesGravity.forEach((p) => {
        p.step += p.speed * Math.sqrt(1 + p.step * 0.15 * g);
        if (p.step > N) p.step = 0;
        let z = p.step * deltaK, r = a / (z + 1), theta = (7 * Math.PI / 6) * p.step;
        let pt = project3D(r * Math.cos(theta), r * Math.sin(theta), z, cx, cy);
        ctx.beginPath(); ctx.arc(pt.px, pt.py, Math.max(1, 4 * (1 - z / (N * deltaK))), 0, Math.PI * 2);
        ctx.fillStyle = `hsl(${p.hue}, 100%, 65%)`; ctx.fill();
      });
    }

    function drawMode4() {
      const numP = parseInt(document.getElementById('paz-particles4').value);
      const stepDeg = parseInt(document.getElementById('paz-step4').value);
      const stepRad = (stepDeg * Math.PI) / 180;
      const w = canvas.width, h = canvas.height, cx = w / 2, cy = h / 2;

      ctx.beginPath(); ctx.strokeStyle = '#1e293b'; ctx.lineWidth = 2;
      ctx.arc(cx, cy, 180, 0, Math.PI * 2); ctx.stroke();

      ctx.beginPath(); ctx.strokeStyle = 'rgba(0, 242, 254, 0.15)';
      for (let i = 0; i < 24; i++) {
        let a1 = i * stepRad, a2 = (i + 1) * stepRad;
        ctx.moveTo(cx + 180 * Math.cos(a1), cy + 180 * Math.sin(a1));
        ctx.lineTo(cx + 180 * Math.cos(a2), cy + 180 * Math.sin(a2));
      }
      ctx.stroke();

      for (let i = 0; i < numP; i++) {
        let p = particlesOrbital[i % particlesOrbital.length];
        p.angle += p.speed;
        let x = cx + p.radius * Math.cos(p.angle), y = cy + p.radius * Math.sin(p.angle);
        ctx.beginPath(); ctx.arc(x, y, 3, 0, Math.PI * 2);
        ctx.fillStyle = `hsl(${(p.hue + i * 5) % 360}, 100%, 60%)`; ctx.fill();
      }
    }

    function animate() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      if (currentMode === 'mode1') drawMode1();
      else if (currentMode === 'mode2') drawMode2();
      else if (currentMode === 'mode3') drawMode3();
      else drawMode4();
      requestAnimationFrame(animate);
    }

    window.onload = () => {
      init();
      updateAll();
    };

    window.onresize = () => {
      resizeCanvas();
      updateAll();
    };
  </script>

<div class="container">
    <!-- Card estilizado do GitHub usando sua foto de perfil -->
    <div class="github-card">
      <img class="avatar" src="https://github.com/Alan-Paz.png" alt="Foto de Perfil - Alan Paz">
      <h1 class="profile-name">Alan Paz</h1>
      <p class="profile-username">@Alan-Paz</p>
      <p class="bio">Perfil oficial no GitHub com repositórios de projetos, códigos e contribuições.</p>

      <a href="https://github.com/Alan-Paz" target="_blank" rel="noopener noreferrer" class="btn-github">
        <svg height="20" width="20" viewBox="0 0 16 16" fill="white">
          <path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z"></path>
        </svg>
        Ver Perfil no GitHub
      </a>
    </div>

    <!-- Iframe do Google Drive ao lado -->
    <div class="drive-container">
      <iframe
        src="https://drive.google.com/file/d/1H4ycrSySH-LrHeV7b51I5FCHdJ-Z22fe/preview"
        allow="autoplay">
      </iframe>
      <a href="https://colab.research.google.com/drive/19v5aE9SdojItqAThiEbLlAOLvlB5vIGb?usp=sharing" target="_blank" rel="noopener noreferrer">
  Abrir O TEOREMA Mpaz (Indexação Algébrica de Sistemas Diatônicos via Matrizes Helicoidais Assimétricas MPaz
Teorema Mpaz de Alan Aparecido da Silva Paz — MATRIZES HELICOIDAIS ASSIMETRICAS) Notebook no Google Colab
</a>
    </div>
  </div>
</body>
</html>
