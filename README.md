<!DOCTYPE html>

<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ALBA — Manifiesto Fundacional</title>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;0,700;1,300;1,400;1,700&family=Outfit:wght@200;300;400;500;600;700&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<style>
  :root {
    --night: #0F1A2E;
    --night-mid: #162240;
    --predawn: #1E2D4F;
    --horizon: #2A3A5C;
    --amber: #D4870E;
    --amber-light: #F2C94C;
    --amber-soft: #E8A83E;
    --amber-glow: rgba(212, 135, 14, 0.15);
    --sunrise-pink: #C4616A;
    --sunrise-lavender: #8B7BA5;
    --dawn-warm: #D4A574;
    --morning: #F0E4D0;
    --daylight: #FAF6EF;
    --cream: #FFFDF7;
    --ink: #1A1A2E;
    --ink-soft: #2E3450;
    --smoke-light: #7A8299;
    --smoke-dark: #9AA0B4;
    --ash: #5A6078;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  html {
    scroll-behavior: smooth;
    scrollbar-width: thin;
    scrollbar-color: var(--amber) var(--night);
  }

  body {
    font-family: 'Outfit', sans-serif;
    font-weight: 300;
    overflow-x: hidden;
    cursor: default;
    background: var(--night);
  }

  body::after {
    content: '';
    position: fixed;
    top: 0; left: 0; width: 100%; height: 100%;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.025'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 9999;
  }

  .progress-bar {
    position: fixed;
    top: 0; left: 0;
    height: 3px;
    background: linear-gradient(90deg, var(--sunrise-lavender), var(--amber), var(--amber-light));
    width: 0%;
    z-index: 1000;
    transition: width 0.1s linear;
  }

  .autoplay-btn {
    position: fixed;
    bottom: 32px;
    right: 32px;
    z-index: 1000;
    background: rgba(255,255,255,0.08);
    border: 1px solid rgba(255,255,255,0.15);
    color: rgba(255,255,255,0.7);
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 14px 24px;
    cursor: pointer;
    border-radius: 50px;
    backdrop-filter: blur(16px);
    -webkit-backdrop-filter: blur(16px);
    transition: all 0.4s ease;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .autoplay-btn:hover {
    background: rgba(255,255,255,0.14);
    border-color: rgba(255,255,255,0.25);
    transform: scale(1.05);
  }

  .autoplay-btn.playing {
    background: rgba(212, 135, 14, 0.2);
    border-color: var(--amber);
    color: var(--amber-light);
  }

  .autoplay-btn .play-icon {
    width: 0; height: 0;
    border-style: solid;
    border-width: 5px 0 5px 9px;
    border-color: transparent transparent transparent currentColor;
    transition: all 0.3s;
  }

  .autoplay-btn.playing .play-icon {
    width: 8px; height: 10px;
    border-width: 0;
    border-left: 2.5px solid var(--amber-light);
    border-right: 2.5px solid var(--amber-light);
  }

  .autoplay-btn.on-light {
    background: rgba(0,0,0,0.05);
    border-color: rgba(0,0,0,0.12);
    color: var(--ash);
  }
  .autoplay-btn.on-light:hover {
    background: rgba(0,0,0,0.1);
  }
  .autoplay-btn.on-light.playing {
    background: rgba(212, 135, 14, 0.15);
    border-color: var(--amber);
    color: var(--amber);
  }

  .scene {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 80px 40px;
    position: relative;
    overflow: hidden;
  }

  .scene-inner {
    max-width: 800px;
    width: 100%;
    position: relative;
    z-index: 2;
  }

  .reveal {
    opacity: 0;
    transform: translateY(60px);
    transition: opacity 1s cubic-bezier(0.25, 0.46, 0.45, 0.94),
                transform 1s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }
  .reveal-delay-1 { transition-delay: 0.15s; }
  .reveal-delay-2 { transition-delay: 0.3s; }
  .reveal-delay-3 { transition-delay: 0.45s; }
  .reveal-delay-4 { transition-delay: 0.6s; }
  .reveal-delay-5 { transition-delay: 0.75s; }

  .reveal-scale {
    opacity: 0;
    transform: scale(0.92);
    transition: opacity 0.8s ease, transform 0.8s ease;
  }
  .reveal-scale.visible { opacity: 1; transform: scale(1); }

  .scene-night {
    background: linear-gradient(180deg, #0B1220 0%, var(--night) 50%, var(--night-mid) 100%);
    color: #E8E4DC;
  }

  .scene-night::before {
    content: '';
    position: absolute;
    top: 35%; left: 50%;
    width: 500px; height: 500px;
    background: radial-gradient(circle, rgba(139, 123, 165, 0.08) 0%, transparent 70%);
    transform: translate(-50%, -50%);
    animation: pulse-glow 8s ease-in-out infinite;
  }

  .scene-predawn {
    background: linear-gradient(180deg, var(--night-mid) 0%, var(--predawn) 40%, #2D3B63 100%);
    color: #D8D4CC;
  }

  .scene-horizon {
    background: linear-gradient(180deg, #2D3B63 0%, var(--horizon) 30%, #3D4A6B 60%, #4A4E6A 100%);
    color: #E0DCD4;
    position: relative;
  }

  .scene-horizon::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 40%;
    background: linear-gradient(180deg, transparent 0%, rgba(212, 135, 14, 0.06) 100%);
  }

  .scene-firstlight {
    background: linear-gradient(180deg, #3A4568 0%, #4E4A5E 25%, #6B5A5A 50%, #8B6B52 75%, #A07A4A 100%);
    color: #F0EAE0;
  }

  .scene-firstlight::before {
    content: '';
    position: absolute;
    bottom: 20%; left: 50%;
    width: 120%; height: 300px;
    background: radial-gradient(ellipse, rgba(232, 168, 62, 0.12) 0%, transparent 60%);
    transform: translateX(-50%);
  }

  .scene-sunrise {
    background: linear-gradient(180deg, #8B6B52 0%, #B08050 20%, #C8935A 50%, #D4A574 80%, var(--morning) 100%);
    color: #2A1F18;
  }

  .scene-sunrise .section-label { color: #8B4513; }
  .scene-sunrise .section-label::after { background: linear-gradient(to right, #8B4513, transparent); }
  .scene-sunrise h2 strong { color: #8B4513; }
  .scene-sunrise .body-text { color: #4A3628; }
  .scene-sunrise .body-text strong { color: #2A1F18; }

  .scene-golden {
    background: linear-gradient(180deg, var(--morning) 0%, #F2E6D0 40%, #F5EDD8 100%);
    color: var(--ink);
  }

  .scene-morning {
    background: linear-gradient(180deg, #F5EDD8 0%, var(--daylight) 50%, var(--cream) 100%);
    color: var(--ink);
  }

  .scene-daylight {
    background: var(--cream);
    color: var(--ink);
  }

  .scene-nextdawn {
    background: linear-gradient(180deg, var(--cream) 0%, #F5EDD8 20%, #E8D8C0 50%, #D4B896 80%, #C8A878 100%);
    color: var(--ink);
  }

  .scene-footer-dawn {
    background: linear-gradient(180deg, #C8A878 0%, #8B7A60 20%, #5A5A6A 50%, var(--predawn) 80%, var(--night) 100%);
    color: #E0DCD4;
    min-height: 60vh;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    padding: 80px 40px;
  }

  @keyframes pulse-glow {
    0%, 100% { opacity: 0.4; transform: translate(-50%, -50%) scale(1); }
    50% { opacity: 0.7; transform: translate(-50%, -50%) scale(1.1); }
  }

  .section-label {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--amber);
    margin-bottom: 28px;
    display: flex;
    align-items: center;
    gap: 16px;
  }

  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: linear-gradient(to right, var(--amber), transparent);
  }

  h2 {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(32px, 5vw, 52px);
    font-weight: 300;
    line-height: 1.15;
    margin-bottom: 32px;
    letter-spacing: -1px;
  }

  h2 strong {
    font-weight: 700;
    color: var(--amber);
  }

  .body-text {
    font-size: clamp(16px, 2vw, 19px);
    line-height: 1.8;
    font-weight: 300;
    margin-bottom: 20px;
  }

  .body-text:last-child { margin-bottom: 0; }
  .body-text strong { font-weight: 600; }

  .scene-night .body-text,
  .scene-predawn .body-text { color: var(--smoke-dark); }
  .scene-night .body-text strong,
  .scene-predawn .body-text strong { color: #E8E4DC; }

  .scene-horizon .body-text { color: #A0A8C0; }
  .scene-horizon .body-text strong { color: #D8D4CC; }

  .scene-firstlight .body-text { color: #C8BFA8; }
  .scene-firstlight .body-text strong { color: #F0EAE0; }

  .scene-golden .body-text,
  .scene-morning .body-text,
  .scene-daylight .body-text,
  .scene-nextdawn .body-text { color: var(--ash); }

  .scene-golden .body-text strong,
  .scene-morning .body-text strong,
  .scene-daylight .body-text strong,
  .scene-nextdawn .body-text strong { color: var(--ink); }

  .scene-golden .section-label,
  .scene-morning .section-label,
  .scene-daylight .section-label,
  .scene-nextdawn .section-label { color: var(--amber); }

  .scene-golden h2 strong,
  .scene-morning h2 strong,
  .scene-daylight h2 strong,
  .scene-nextdawn h2 strong { color: var(--amber); }

  .opening-label {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 5px;
    text-transform: uppercase;
    color: var(--sunrise-lavender);
    margin-bottom: 40px;
    text-align: center;
  }

  .opening-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(72px, 14vw, 140px);
    font-weight: 300;
    text-align: center;
    line-height: 0.9;
    letter-spacing: -3px;
    margin-bottom: 24px;
    color: #E8E4DC;
  }

  .opening-title .accent { color: var(--amber-soft); font-weight: 700; }

  .opening-subtitle {
    font-family: 'Outfit', sans-serif;
    font-weight: 200;
    font-size: clamp(13px, 2vw, 17px);
    letter-spacing: 4px;
    text-transform: uppercase;
    text-align: center;
    color: var(--smoke-dark);
    margin-bottom: 60px;
  }

  .opening-tagline {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(18px, 2.5vw, 24px);
    font-style: italic;
    text-align: center;
    color: var(--smoke-dark);
    font-weight: 300;
    max-width: 500px;
    margin: 0 auto;
    line-height: 1.5;
  }

  .scroll-hint {
    position: absolute;
    bottom: 40px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    animation: float 3s ease-in-out infinite;
  }

  .scroll-hint span {
    font-family: 'Space Mono', monospace;
    font-size: 9px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--smoke-light);
  }

  .scroll-hint .arrow {
    width: 1px; height: 40px;
    background: linear-gradient(to bottom, var(--sunrise-lavender), transparent);
  }

  @keyframes float {
    0%, 100% { transform: translateX(-50%) translateY(0); }
    50% { transform: translateX(-50%) translateY(8px); }
  }

  .big-quote {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(28px, 5vw, 48px);
    font-weight: 300;
    font-style: italic;
    line-height: 1.3;
    text-align: center;
    max-width: 700px;
    margin: 0 auto;
  }

  .scene-predawn .big-quote { color: #D8D4CC; }
  .scene-predawn .big-quote .amber { color: var(--amber-soft); }

  .scene-firstlight .big-quote { color: #F0EAE0; }
  .scene-firstlight .big-quote .amber { color: var(--amber-light); }

  .principle {
    display: flex;
    gap: 28px;
    margin-bottom: 40px;
    align-items: flex-start;
  }

  .principle-num {
    font-family: 'Cormorant Garamond', serif;
    font-size: 48px;
    font-weight: 700;
    line-height: 1;
    min-width: 48px;
    opacity: 0.3;
  }

  .scene-sunrise .principle-num { color: #8B4513; }

  .principle-content h3 {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(20px, 3vw, 26px);
    font-weight: 600;
    margin-bottom: 6px;
  }

  .scene-sunrise .principle-content h3 { color: #2A1F18; }
  .scene-sunrise .principle-content p { color: #4A3628; font-size: 16px; line-height: 1.6; font-weight: 300; }

  .tech-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 24px;
    margin-top: 32px;
  }

  @media (max-width: 640px) { .tech-grid { grid-template-columns: 1fr; } }

  .tech-card {
    padding: 28px;
    border-radius: 12px;
    transition: all 0.4s ease;
  }

  .scene-golden .tech-card {
    background: rgba(212, 135, 14, 0.06);
    border: 1px solid rgba(212, 135, 14, 0.12);
  }

  .scene-golden .tech-card:hover {
    border-color: rgba(212, 135, 14, 0.25);
    background: rgba(212, 135, 14, 0.1);
    transform: translateY(-2px);
  }

  .tech-card h4 {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--amber);
    margin-bottom: 10px;
  }

  .tech-card p {
    font-size: 15px;
    color: var(--ash);
    line-height: 1.55;
    font-weight: 300;
  }

  .pitch-block {
    background: linear-gradient(135deg, var(--amber) 0%, #B8720A 100%);
    padding: 56px 48px;
    border-radius: 16px;
    text-align: center;
    box-shadow: 0 20px 60px rgba(212, 135, 14, 0.15);
  }

  .pitch-block h2 {
    color: #FFF;
    font-size: clamp(22px, 3.5vw, 32px);
    font-weight: 600;
    margin-bottom: 16px;
  }

  .pitch-block h2 strong { color: #FFF; }

  .pitch-block p {
    color: rgba(255, 255, 255, 0.7);
    font-size: 15px;
    font-weight: 400;
  }

  .audience-item {
    margin-bottom: 28px;
    padding-left: 20px;
    border-left: 2px solid rgba(212, 135, 14, 0.25);
  }

  .audience-item .label {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--amber);
    margin-bottom: 6px;
  }

  .audience-item p {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(17px, 2.2vw, 21px);
    font-style: italic;
    color: var(--ash);
    line-height: 1.5;
    font-weight: 300;
  }

  .closing-text {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(18px, 2.5vw, 24px);
    line-height: 1.6;
    font-weight: 300;
    margin-bottom: 20px;
  }

  .scene-nextdawn .closing-text { color: var(--ash); }
  .scene-nextdawn .closing-text strong { color: var(--ink); font-weight: 600; }

  .footer-brand {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(48px, 8vw, 80px);
    font-weight: 300;
    letter-spacing: -2px;
    margin-bottom: 16px;
    color: #E0DCD4;
  }

  .footer-brand .accent { color: var(--amber-soft); font-weight: 700; }

  .footer-desc {
    font-family: 'Outfit', sans-serif;
    font-size: 13px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--smoke-light);
    font-weight: 200;
    margin-bottom: 40px;
  }

  .footer-cronica {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(15px, 2vw, 18px);
    font-style: italic;
    color: var(--smoke-dark);
    max-width: 560px;
    margin: 0 auto;
    line-height: 1.6;
    font-weight: 300;
  }

  @media (max-width: 640px) {
    .scene { padding: 60px 24px; }
    .pitch-block { padding: 40px 28px; }
    .principle { gap: 16px; }
    .principle-num { font-size: 36px; min-width: 36px; }
    .autoplay-btn { bottom: 20px; right: 20px; padding: 12px 18px; font-size: 10px; }
  }
</style>
</head>
<body>

<div class="progress-bar" id="progressBar"></div>

<button class="autoplay-btn" id="autoplayBtn" onclick="toggleAutoplay()">
  <div class="play-icon"></div>
  <span>Presentar</span>
</button>

<section class="scene scene-night" data-theme="dark">
  <div class="scene-inner" style="text-align:center;">
    <div class="opening-label reveal">Texto Fundacional</div>
    <div class="opening-title reveal reveal-delay-1">
      <span class="accent">A</span>LBA
    </div>
    <div class="opening-subtitle reveal reveal-delay-2">
      Alfabetización Basada en Acompañamiento
    </div>
    <p class="opening-tagline reveal reveal-delay-3">
      Donde cada clase genera datos<br>y cada dato mejora la siguiente clase.
    </p>
  </div>
  <div class="scroll-hint">
    <span>Scroll</span>
    <div class="arrow"></div>
  </div>
</section>

<section class="scene scene-predawn" data-theme="dark">
  <div class="scene-inner" style="text-align:center;">
    <div class="big-quote reveal">
      Hay un segundo exacto en que las letras dejan de ser dibujo y empiezan a ser <span class="amber">voz</span>.
    </div>
    <p class="body-text reveal reveal-delay-2" style="text-align:center; margin-top:40px; max-width:500px; margin-left:auto; margin-right:auto;">
      Ese segundo existe. Ocurre miles de veces por día en miles de aulas. Nadie lo registra. <strong>Hasta ahora.</strong>
    </p>
  </div>
</section>

<section class="scene scene-horizon" data-theme="dark">
  <div class="scene-inner">
    <div class="section-label reveal">Manifiesto</div>
    <h2 class="reveal reveal-delay-1">Antes del día, <strong>el alba</strong>.</h2>
    <p class="body-text reveal reveal-delay-2">
      ALBA nace de una convicción simple: <strong>la alfabetización es la llama que enciende todo lo que viene después</strong>. No hay pensamiento crítico, ni ciudadanía, ni ciencia, ni democracia sin esa llama. Y sin embargo, enseñamos a alfabetizar casi a ciegas — sin datos, sin evidencia en tiempo real, sin memoria del proceso.
    </p>
    <p class="body-text reveal reveal-delay-3">
      No construimos tecnología para el aula. <strong>Construimos el aula que finalmente puede escucharse a sí misma.</strong>
    </p>
    <p class="body-text reveal reveal-delay-4">
      La docente ya sabe. Su ojo clínico detecta al niño que se traba, al que finge leer, al que avanzó sin que nadie lo celebre. Lo que falta no es saber pedagógico — sobra. Lo que falta es infraestructura para que ese saber se ordene, se acumule, se conecte y escale.
    </p>
    <p class="body-text reveal reveal-delay-5" style="margin-top:12px;">
      <strong>El docente genera el conocimiento. ALBA lo ordena, lo potencia y lo escala.</strong>
    </p>
  </div>
</section>

<section class="scene scene-firstlight" data-theme="dark">
  <div class="scene-inner" style="text-align:center;">
    <div class="big-quote reveal">
      Veintiocho signos caben en la mano de un niño.<br>
      <span class="amber">Civilizaciones enteras</span> caben en esos veintiocho signos.
    </div>
  </div>
</section>

<section class="scene scene-sunrise" data-theme="light" style="min-height:auto; padding-top:100px; padding-bottom:60px;">
  <div class="scene-inner">
    <div class="section-label reveal">Principios</div>
    <h2 class="reveal reveal-delay-1">Cinco certezas que nos guían</h2>
  </div>
</section>

<section class="scene scene-sunrise" data-theme="light" style="min-height:auto; padding-top:0; padding-bottom:100px;">
  <div class="scene-inner">
    <div class="principle reveal">
      <div class="principle-num">1</div>
      <div class="principle-content">
        <h3>Cada aula es un nodo de aprendizaje.</h3>
        <p>No un lugar aislado. Un punto en una red que genera conocimiento colectivo si alguien conecta los datos.</p>
      </div>
    </div>
    <div class="principle reveal reveal-delay-1">
      <div class="principle-num">2</div>
      <div class="principle-content">
        <h3>La IA acompaña; no reemplaza.</h3>
        <p>La inteligencia artificial amplifica lo que la docente ya ve. Ofrece visibilidad, no directivas. Evidencia, no recetas.</p>
      </div>
    </div>
    <div class="principle reveal reveal-delay-2">
      <div class="principle-num">3</div>
      <div class="principle-content">
        <h3>Simplicidad es respeto.</h3>
        <p>Si un docente necesita más de 30 segundos para registrar un avance, el sistema falló. Menos fricción es más adopción.</p>
      </div>
    </div>
    <div class="principle reveal reveal-delay-3">
      <div class="principle-num">4</div>
      <div class="principle-content">
        <h3>Medir no es controlar.</h3>
        <p>Los datos existen para iluminar, no para vigilar. Cada métrica se diseña para la mejora continua, nunca para el castigo.</p>
      </div>
    </div>
    <div class="principle reveal reveal-delay-4">
      <div class="principle-num">5</div>
      <div class="principle-content">
        <h3>Veintiocho signos, infinitas posibilidades.</h3>
        <p>Veintiocho letras caben en la mano de un niño. Civilizaciones enteras caben en esas veintiocho letras.</p>
      </div>
    </div>
  </div>
</section>

<section class="scene scene-golden" data-theme="light">
  <div class="scene-inner">
    <div class="section-label reveal">Descriptor técnico</div>
    <h2 class="reveal reveal-delay-1">Qué es ALBA, <strong>en concreto</strong></h2>
    <p class="body-text reveal reveal-delay-2">
      ALBA es una <strong>infraestructura de inteligencia pedagógica</strong> para la alfabetización inicial. Captura evidencia de aprendizaje en tiempo real, la organiza mediante inteligencia artificial y la devuelve como acompañamiento accionable para docentes, equipos directivos y decisores de política educativa.
    </p>
    <div class="tech-grid">
      <div class="tech-card reveal reveal-delay-1">
        <h4>Capa de registro</h4>
        <p>Captura ultra-simple en aula: la docente registra avances en segundos, sin formularios, sin abandonar la clase.</p>
      </div>
      <div class="tech-card reveal reveal-delay-2">
        <h4>Capa de inteligencia</h4>
        <p>IA que detecta patrones, anticipa dificultades y sugiere intervenciones basadas en la evidencia acumulada de toda la red.</p>
      </div>
      <div class="tech-card reveal reveal-delay-3">
        <h4>Capa de visibilidad</h4>
        <p>Dashboards en tiempo real para docentes, directivos y ministerios. Cada nivel ve lo que necesita, con la granularidad justa.</p>
      </div>
      <div class="tech-card reveal reveal-delay-4">
        <h4>Capa de escala</h4>
        <p>Cada aula que se suma mejora el modelo. Cada dato alimenta la inteligencia colectiva. La red aprende mientras enseña.</p>
      </div>
    </div>
  </div>
</section>

<section class="scene scene-morning" data-theme="light">
  <div class="scene-inner">
    <div class="pitch-block reveal reveal-scale">
      <h2>ALBA convierte cada clase de alfabetización en datos accionables y cada dato en mejor enseñanza. En tiempo real. A escala nacional.</h2>
      <p>Infraestructura de inteligencia pedagógica para que la alfabetización deje de ser invisible.</p>
    </div>
  </div>
</section>

<section class="scene scene-daylight" data-theme="light">
  <div class="scene-inner">
    <div class="section-label reveal">Cómo se dice, según a quién</div>

    <div class="audience-item reveal reveal-delay-1">
      <div class="label">Para una docente</div>
      <p>ALBA te muestra lo que ya sabés de tus alumnos, organizado. Y te sugiere qué hacer mañana con lo que pasó hoy.</p>
    </div>
    <div class="audience-item reveal reveal-delay-2">
      <div class="label">Para un directivo</div>
      <p>ALBA te da visibilidad en tiempo real de cómo avanza la alfabetización en tu escuela, sin esperar al final del trimestre.</p>
    </div>
    <div class="audience-item reveal reveal-delay-3">
      <div class="label">Para un ministerio</div>
      <p>ALBA genera evidencia continua a nivel de aula, escuela, distrito y jurisdicción. Decisiones basadas en datos, no en supuestos.</p>
    </div>
    <div class="audience-item reveal reveal-delay-4">
      <div class="label">Para un inversor</div>
      <p>ALBA es la capa de inteligencia que falta entre el aula y la política educativa. Cada escuela que se suma mejora el modelo. Cada dato capturado es una ventaja competitiva irreversible.</p>
    </div>
    <div class="audience-item reveal reveal-delay-5">
      <div class="label">Para un congreso académico</div>
      <p>ALBA opera sobre una hipótesis verificable: la alfabetización mejora cuando el ciclo entre evidencia y decisión pedagógica se acorta de meses a horas.</p>
    </div>
  </div>
</section>

<section class="scene scene-nextdawn" data-theme="light">
  <div class="scene-inner">
    <div class="section-label reveal">Cierre</div>
    <h2 class="reveal reveal-delay-1">La casa que <strong>todavía no existe</strong></h2>

    <p class="closing-text reveal reveal-delay-2">
      Ray Bradbury imaginó un futuro donde cada persona se convertía en un libro vivo — caminaba, respiraba y transmitía una historia que de otro modo se habría perdido para siempre. <strong>Cada niño que aprende a leer se convierte en eso: un libro que camina.</strong> Y hay una docente que sabe exactamente en qué página de ese libro está cada niño.
    </p>
    <p class="closing-text reveal reveal-delay-3">
      ALBA no inventa ese saber. Lo hace visible. Lo conecta. Lo escala. Para que cada niño que aprende a leer encienda una habitación en una casa que todavía no existe — pero que estamos construyendo, clase a clase, dato a dato, <strong>alba tras alba</strong>.
    </p>
  </div>
</section>

<section class="scene-footer-dawn" data-theme="dark">
  <div class="scene-inner" style="text-align:center;">
    <div class="footer-brand reveal"><span class="accent">A</span>LBA</div>
    <div class="footer-desc reveal reveal-delay-1">Alfabetización Basada en Acompañamiento</div>
    <p class="footer-cronica reveal reveal-delay-2">
      Cada clase es una crónica que nadie escribe. ALBA la escribe, la comparte, la universaliza — y la devuelve al aula para que la próxima crónica sea mejor.
    </p>
  </div>
</section>

<script>
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) entry.target.classList.add('visible');
    });
  }, { threshold: 0.12, rootMargin: '0px 0px -30px 0px' });

  document.querySelectorAll('.reveal, .reveal-scale').forEach(el => observer.observe(el));

  const progressBar = document.getElementById('progressBar');
  const btn = document.getElementById('autoplayBtn');
  const scenes = document.querySelectorAll('[data-theme]');

  function updateButton() {
    const scrollY = window.scrollY + window.innerHeight * 0.9;
    let currentTheme = 'dark';
    scenes.forEach(scene => {
      if (scene.offsetTop < scrollY) currentTheme = scene.dataset.theme;
    });
    btn.classList.toggle('on-light', currentTheme === 'light');
  }

  window.addEventListener('scroll', () => {
    const scrollTop = window.scrollY;
    const docHeight = document.documentElement.scrollHeight - window.innerHeight;
    progressBar.style.width = (scrollTop / docHeight) * 100 + '%';
    updateButton();
  });

  let isPlaying = false;
  let autoplayInterval = null;
  const btnLabel = btn.querySelector('span');

  function toggleAutoplay() {
    isPlaying ? stopAutoplay() : startAutoplay();
  }

  function startAutoplay() {
    isPlaying = true;
    btn.classList.add('playing');
    btnLabel.textContent = 'Pausar';
    autoplayInterval = setInterval(() => {
      const docHeight = document.documentElement.scrollHeight - window.innerHeight;
      if (window.scrollY >= docHeight - 10) { stopAutoplay(); return; }
      window.scrollBy({ top: 1.5, behavior: 'auto' });
    }, 16);
  }

  function stopAutoplay() {
    isPlaying = false;
    btn.classList.remove('playing');
    btnLabel.textContent = 'Presentar';
    if (autoplayInterval) { clearInterval(autoplayInterval); autoplayInterval = null; }
  }

  window.addEventListener('wheel', () => { if (isPlaying) stopAutoplay(); });
  window.addEventListener('touchstart', () => { if (isPlaying) stopAutoplay(); });
  window.addEventListener('keydown', (e) => {
    if (e.key === ' ' || e.key === 'Spacebar') { e.preventDefault(); toggleAutoplay(); }
  });

  setTimeout(() => {
    document.querySelectorAll('.scene-night .reveal').forEach(el => el.classList.add('visible'));
  }, 300);
</script>

</body>
</html>
