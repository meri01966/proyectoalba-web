<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Proyecto ALBA</title>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,700;1,300&family=Outfit:wght@200;300;400;500;600;700&family=Space+Mono:wght@400&display=swap" rel="stylesheet">
<style>
*{margin:0;padding:0;box-sizing:border-box}
html{scroll-behavior:smooth}
body{font-family:'Outfit',sans-serif;background:#0F1A2E;color:#E8E4DC;overflow-x:hidden}
.nav{position:fixed;top:0;left:0;right:0;z-index:50;padding:14px 24px;display:flex;align-items:center;justify-content:space-between;background:rgba(15,26,46,0.85);backdrop-filter:blur(16px);-webkit-backdrop-filter:blur(16px);border-bottom:1px solid rgba(255,255,255,0.04)}
.nav-logo{font-family:'Cormorant Garamond',serif;font-size:22px;font-weight:300;cursor:pointer}
.nav-logo .a{color:#D4870E;font-weight:700}
.nav-links{display:flex;gap:20px}
.nav-links a{font-size:11px;color:rgba(154,160,180,0.5);text-decoration:none;letter-spacing:1px;transition:color 0.3s}
.nav-links a:hover{color:#E85D26}
.sc{min-height:100vh;display:flex;align-items:center;justify-content:center;padding:80px 24px;position:relative;overflow:hidden}
.inner{max-width:720px;width:100%;position:relative;z-index:2}
.rv{opacity:0;transform:translateY(25px);transition:all 0.9s ease}.rv.v{opacity:1;transform:translateY(0)}
.d1{transition-delay:.15s}.d2{transition-delay:.3s}.d3{transition-delay:.45s}.d4{transition-delay:.6s}.d5{transition-delay:.75s}
.mono{font-family:'Space Mono',monospace;font-size:10px;letter-spacing:4px;text-transform:uppercase;color:#E85D26;margin-bottom:16px}
.serif{font-family:'Cormorant Garamond',serif}
.big{font-size:clamp(26px,5.5vw,46px);font-weight:300;line-height:1.12;letter-spacing:-1px;margin-bottom:14px}
.big b{font-weight:700;color:#E85D26}
.txt{font-size:14px;line-height:1.7;color:rgba(154,160,180,0.65);margin-bottom:10px}
.txt b{color:rgba(200,196,188,0.85)}
.lnc{width:40px;height:1px;background:#E85D26;margin:16px auto;opacity:.4}
.ln{width:40px;height:1px;background:#E85D26;margin:16px 0;opacity:.4}
.gl{position:absolute;border-radius:50%;filter:blur(80px);pointer-events:none}
.sc1{background:linear-gradient(180deg,#040810,#0F1A2E)}
.sc1::before{content:'';position:absolute;width:100%;height:100%;background:radial-gradient(1px 1px at 20% 30%,rgba(255,255,255,0.12),transparent),radial-gradient(1px 1px at 55% 65%,rgba(255,255,255,0.08),transparent),radial-gradient(1px 1px at 80% 20%,rgba(255,255,255,0.1),transparent);animation:tw 6s ease-in-out infinite}
@keyframes tw{0%,100%{opacity:.4}50%{opacity:.9}}
.sc2{background:linear-gradient(180deg,#0F1A2E,#162240)}
.sc3{background:linear-gradient(180deg,#162240,#1C2B4F)}
.sc4{background:linear-gradient(180deg,#1C2B4F,#2A3A5C)}
.sc5{background:linear-gradient(180deg,#2A3A5C,#3D4A6B)}
.sc6{background:linear-gradient(180deg,#3D4A6B,#2A3A5C,#0F1A2E)}
.stats{display:grid;grid-template-columns:1fr 1fr 1fr 1fr;gap:10px;margin-top:20px}
@media(max-width:600px){.stats{grid-template-columns:1fr 1fr}.nav-links{display:none}}
.stat{text-align:center;padding:18px 12px;border-radius:10px;background:rgba(255,255,255,0.02);border:1px solid rgba(255,255,255,0.05)}
.stat .n{font-family:'Cormorant Garamond',serif;font-size:30px;font-weight:700;color:#E85D26}
.stat p{font-size:10px;color:rgba(154,160,180,0.5);margin-top:4px;line-height:1.3}
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-top:18px}
@media(max-width:600px){.grid2{grid-template-columns:1fr}}
.card{padding:18px;border-radius:10px;background:rgba(255,255,255,0.02);border:1px solid rgba(255,255,255,0.05)}
.card h4{font-family:'Space Mono',monospace;font-size:9px;letter-spacing:2px;text-transform:uppercase;color:#E85D26;margin-bottom:6px}
.card p{font-size:12px;color:rgba(154,160,180,0.55);line-height:1.5}
.impact{display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;margin-top:18px}
@media(max-width:600px){.impact{grid-template-columns:1fr}}
.imp{padding:20px;border-radius:10px;text-align:center;border:1px solid rgba(255,255,255,0.05);background:rgba(255,255,255,0.02)}
.imp .n{font-family:'Cormorant Garamond',serif;font-size:36px;font-weight:700;margin-bottom:4px}
.imp p{font-size:11px;color:rgba(154,160,180,0.5);line-height:1.3}
.fire-box{padding:24px;border-radius:12px;background:linear-gradient(135deg,rgba(232,93,38,0.08),rgba(212,135,14,0.06));border:1px solid rgba(232,93,38,0.15);text-align:center;margin-top:20px}
.cta{display:inline-block;padding:14px 32px;border-radius:50px;background:#E85D26;color:#fff;text-decoration:none;font-size:13px;font-weight:600;letter-spacing:1px;transition:all 0.3s}
.cta:hover{transform:scale(1.05);box-shadow:0 4px 20px rgba(232,93,38,0.3)}
.progress{position:fixed;top:0;left:0;height:2px;background:linear-gradient(90deg,#8B7BA5,#E85D26,#D4870E);width:0%;z-index:100}
</style>
</head>
<body>

<div class="progress" id="prog"></div>

<nav class="nav">
  <div class="nav-logo"><span class="a">A</span>LBA</div>
  <div class="nav-links">
    <a href="#problema">Problema</a>
    <a href="#tesis">Tesis</a>
    <a href="#impacto">Impacto</a>
    <a href="#contacto">Contacto</a>
  </div>
</nav>

<!-- 1. HERO -->
<section class="sc sc1">
  <div class="gl" style="width:300px;height:300px;background:rgba(212,135,14,0.05);top:30%;left:42%"></div>
  <div class="inner" style="text-align:center">
    <div class="mono rv">P R O Y E C T O</div>
    <h1 class="serif rv d1" style="font-size:clamp(56px,12vw,110px);font-weight:300;letter-spacing:-3px;margin-bottom:8px"><span style="color:#D4870E;font-weight:700">A</span>LBA</h1>
    <div class="lnc rv d2"></div>
    <p class="rv d3" style="font-size:clamp(13px,2.5vw,16px);font-weight:300;color:rgba(154,160,180,0.6);max-width:400px;margin:0 auto;line-height:1.5">Tecnolog&iacute;a educativa pensada por quienes est&aacute;n en el aula</p>
    <p class="rv d4" style="font-size:12px;color:#E85D26;font-weight:600;letter-spacing:2px;text-transform:uppercase;margin-top:14px">Hackeando la brecha educativa</p>
  </div>
</section>

<!-- 2. QUIENES SOMOS -->
<section class="sc sc2">
  <div class="inner">
    <div class="mono rv">Quienes somos</div>
    <h2 class="serif big rv d1">Educadoras que construyen <b>tecnolog&iacute;a</b>.</h2>
    <p class="txt rv d2">Somos un equipo con <b>30 a&ntilde;os de experiencia directa</b> en aulas de nivel inicial, gesti&oacute;n institucional y formaci&oacute;n docente. Conocemos el sistema educativo por dentro: sus fortalezas, sus limitaciones y sus urgencias.</p>
    <p class="txt rv d3">Creemos que la mejor tecnolog&iacute;a educativa no la dise&ntilde;an ingenieros que leyeron sobre educaci&oacute;n. <b>La dise&ntilde;an educadores que aprendieron a usar tecnolog&iacute;a.</b> Porque solo quien vive el problema puede construir la soluci&oacute;n que realmente se adopta.</p>
    <p class="txt rv d4">Construimos ALBA solas. Sin equipo de desarrollo. Sin inversi&oacute;n externa. Usando las herramientas que hoy hacen posible que una idea se convierta en producto. <b>Eso es verdadera inclusi&oacute;n tecnol&oacute;gica.</b></p>
  </div>
</section>

<!-- 3. PROBLEMA -->
<section class="sc sc3" id="problema">
  <div class="inner">
    <div class="mono rv">El problema</div>
    <h2 class="serif big rv d1">La educaci&oacute;n toma decisiones <b>sin datos</b>.</h2>
    <p class="txt rv d2">El sistema educativo es el &uacute;ltimo gran sistema que opera sin informaci&oacute;n granular en tiempo real. Los hospitales tienen historias cl&iacute;nicas digitales. Los bancos tienen transacciones en milisegundos. Las escuelas tienen <b>planillas de papel y evaluaciones que llegan un a&ntilde;o tarde</b>.</p>
    <div class="stats rv d3">
      <div class="stat"><div class="n">46%</div><p>de ni&ntilde;os en Latam no alcanzan niveles m&iacute;nimos de lectura</p></div>
      <div class="stat"><div class="n">12</div><p>meses de rezago entre lo que pasa en el aula y lo que se mide</p></div>
      <div class="stat"><div class="n">0</div><p>sistemas capturan evidencia de alfabetizaci&oacute;n en tiempo real</p></div>
      <div class="stat"><div class="n">95%</div><p>de escuelas todav&iacute;a registran en papel o Excel</p></div>
    </div>
  </div>
</section>

<!-- 4. TESIS -->
<section class="sc sc4" id="tesis">
  <div class="inner">
    <div class="mono rv">Nuestra tesis</div>
    <h2 class="serif big rv d1">La brecha no se cierra <b>desde arriba</b>.</h2>
    <p class="txt rv d2">Se invierten millones en plataformas dise&ntilde;adas desde escritorios de ingenier&iacute;a que nadie usa en el aula. El enfoque top-down fracasa porque no entiende c&oacute;mo funciona una clase real.</p>
    <p class="txt rv d3"><b>La inteligencia pedag&oacute;gica se genera todos los d&iacute;as en cada aula.</b> Cada docente descubre qu&eacute; funciona y qu&eacute; no. Ese conocimiento es el recurso m&aacute;s valioso del sistema educativo. Y se pierde.</p>
    <div class="grid2 rv d4">
      <div class="card">
        <h4>Lo que se hace hoy</h4>
        <p>Evaluar una vez al a&ntilde;o. Recibir datos 12 meses tarde. Tomar decisiones por intuici&oacute;n. Enviar cajas de materiales.</p>
      </div>
      <div class="card" style="border-color:rgba(232,93,38,0.2)">
        <h4>Lo que deber&iacute;a pasar</h4>
        <p>Capturar evidencia en tiempo real. Detectar dificultades antes de que sean irreversibles. Conectar lo que funciona entre aulas.</p>
      </div>
    </div>
    <div class="fire-box rv d5">
      <p style="font-family:'Cormorant Garamond',serif;font-size:clamp(16px,2.5vw,22px);color:#E8E4DC;line-height:1.3">Cuando quienes piensan la tecnolog&iacute;a educativa son quienes est&aacute;n en el aula, <b style="color:#E85D26">todo cambia</b>.</p>
    </div>
  </div>
</section>

<!-- 5. IMPACTO -->
<section class="sc sc5" id="impacto">
  <div class="inner">
    <div class="mono rv">Impacto</div>
    <h2 class="serif big rv d1">Lo que pasa cuando la tecnolog&iacute;a <b>funciona</b>.</h2>
    <p class="txt rv d2">Resultados reales de nuestro piloto activo en escuela de Buenos Aires. No proyecciones. No simulaciones. <b>Datos de aula real.</b></p>
    <div class="impact rv d3">
      <div class="imp"><div class="n" style="color:#22c55e">-50%</div><p>reducci&oacute;n en carga administrativa docente</p></div>
      <div class="imp"><div class="n" style="color:#E85D26">10s</div><p>tiempo de registro por clase para 25 alumnos</p></div>
      <div class="imp"><div class="n" style="color:#D4870E">100%</div><p>de docentes siguen usando despu&eacute;s de la primera semana</p></div>
    </div>
    <div class="grid2 rv d4" style="margin-top:14px">
      <div class="imp"><div class="n" style="color:#6366F1;font-size:28px">3</div><p>alertas tempranas detectadas que el m&eacute;todo tradicional hubiera perdido</p></div>
      <div class="imp"><div class="n" style="color:#0D9488;font-size:28px">0%</div><p>de abandono. Ninguna docente dej&oacute; de usarlo</p></div>
    </div>
    <p class="txt rv d5" style="text-align:center;margin-top:18px"><b>&ldquo;Esto es brillante para nosotros.&rdquo;</b></p>
    <p class="rv d5" style="font-size:11px;color:rgba(154,160,180,0.4);text-align:center">&mdash; Docentes de nivel inicial, piloto Mayo 2026</p>
  </div>
</section>

<!-- 6. CONTACTO -->
<section class="sc sc6" id="contacto">
  <div class="inner" style="text-align:center">
    <div class="serif rv" style="font-size:clamp(44px,10vw,80px);font-weight:300;letter-spacing:-2px;margin-bottom:8px"><span style="color:#D4870E;font-weight:700">A</span><span style="color:rgba(232,228,220,0.8)">LBA</span></div>
    <div class="lnc rv d1"></div>
    <p class="rv d2" style="font-size:11px;color:rgba(154,160,180,0.5);letter-spacing:2px;text-transform:uppercase;margin-bottom:20px">Tecnolog&iacute;a educativa pensada desde el aula</p>
    <p class="rv d3" style="font-size:14px;color:rgba(200,196,188,0.5);max-width:440px;margin:0 auto 24px;line-height:1.6">
      Estamos construyendo algo que la educaci&oacute;n necesita y todav&iacute;a no tiene. Si sos docente, directivo, inversor, o simplemente te importa la alfabetizaci&oacute;n, hablemos.
    </p>
    <a href="mailto:mariana@proyectoalba.lat" class="cta rv d4">Contactanos</a>
    <p class="rv d5" style="font-size:11px;color:rgba(154,160,180,0.3);margin-top:16px">mariana@proyectoalba.lat &middot; Buenos Aires, Argentina</p>
    <p style="font-size:9px;color:rgba(154,160,180,0.15);margin-top:28px">&copy; 2026 Proyecto ALBA &mdash; Todos los derechos reservados</p>
  </div>
</section>

<script>
var o=new IntersectionObserver(function(e){e.forEach(function(x){if(x.isIntersecting)x.target.classList.add('v')})},{threshold:0.1});
document.querySelectorAll('.rv').forEach(function(el){o.observe(el)});
addEventListener('scroll',function(){var s=scrollY,d=document.documentElement.scrollHeight-innerHeight;document.getElementById('prog').style.width=(s/d)*100+'%'});
setTimeout(function(){document.querySelectorAll('.sc1 .rv').forEach(function(el){el.classList.add('v')})},300);
</script>
</body>
</html>
