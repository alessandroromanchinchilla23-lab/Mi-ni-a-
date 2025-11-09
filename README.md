<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>¡El Libro de Nuestro Amor, mi Nutria! 💖</title>
  <style>
    /* VARIABLES (Colores de ella) */
    :root {
      --rojo-corazon: #e63946; /* Rojo, fuerte, accent1 */
      --rosa-favorito: #ff7bac; /* Rosa, accent2 */
      --azul-cielo: #89cff0; /* Azul cielo, sky */
      --bg-light: #fff0f2;
      --text-primary: #222;
      --shadow-base: 0 10px 30px rgba(0,0,0,0.08);
    }
    
    /* RESET and BASE STYLES */
    *, *::before, *::after {
      box-sizing: border-box;
    }
    body {
      margin: 0;
      font-family: 'Inter', system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
      background: linear-gradient(180deg, var(--bg-light), #fff);
      color: var(--text-primary);
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 24px;
      overflow: hidden; /* Oculta el scroll durante las transiciones */
    }
    
    /* LAYOUT COMPONENTS - EL LIBRO */
    .page-container {
        position: relative;
        width: 100%;
        max-width: 900px;
        height: 75vh; /* Altura fija para el efecto libro */
        max-height: 700px;
        box-shadow: 0 20px 50px rgba(0,0,0,0.15);
        border-radius: 18px;
        overflow: hidden; /* Importante para el efecto de transicion */
        background: white;
    }

    .page {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      padding: 24px;
      opacity: 0;
      visibility: hidden;
      transform: translateX(100%);
      transition: all 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94); /* Transición de "paso de página" */
      overflow-y: auto; /* Permite scroll si el contenido es largo */
      -webkit-overflow-scrolling: touch;
      /* Fondo base */
      background: linear-gradient(180deg, rgba(255,255,255,0.95), rgba(255,255,255,0.88));
    }
    .page.active {
      opacity: 1;
      visibility: visible;
      transform: translateX(0);
      z-index: 10;
    }

    /* ESTILOS ESPECÍFICOS DE LAS PÁGINAS */
    
    /* Page 1 - Portada */
    #page1 .card-inner {
        display: flex;
        gap: 24px;
        align-items: center;
    }
    .photo-wrap {
      flex: 0 0 250px;
      border-radius: 14px;
      overflow: hidden;
      position: relative;
      box-shadow: var(--shadow-base);
      aspect-ratio: 1 / 1.1; 
    }
    .photo-wrap img {
      display: block;
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
    
    /* Page 2 - Detalles Mágicos */
    #page2 {
        background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" opacity="0.1"><circle cx="50" cy="50" r="40" fill="%23ff7bac" /></svg>') repeat, 
                    linear-gradient(135deg, var(--azul-cielo) 0%, var(--rosa-favorito) 100%);
        background-blend-mode: multiply;
        color: white;
        text-shadow: 0 1px 3px rgba(0,0,0,0.2);
    }
    #page2 .detalle-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: 20px;
        margin-top: 20px;
    }
    .detalle-card {
        background: rgba(255,255,255,0.9);
        border-radius: 12px;
        padding: 16px;
        color: var(--text-primary);
        box-shadow: 0 8px 15px rgba(0,0,0,0.1);
        border-top: 4px solid var(--rojo-corazon);
    }
    .detalle-card h3 {
        color: var(--rojo-corazon);
        margin-top: 0;
        font-size: 1.2em;
        display: flex;
        align-items: center;
        gap: 8px;
    }

    /* Page 3 - Poema Final */
    #page3 {
        text-align: center;
        background: linear-gradient(180deg, #fce4ec 0%, #ffffff 100%);
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    .final-message-wrap {
        z-index: 20;
        background: rgba(255, 255, 255, 0.9);
        padding: 30px;
        border-radius: 20px;
        box-shadow: 0 15px 40px rgba(0,0,0,0.15);
        max-width: 600px;
        margin: 0 auto;
    }
    #page3 h2 {
        color: var(--rojo-corazon);
        font-size: 2.2em;
        margin-bottom: 10px;
    }
    #page3 p {
        font-size: 1.1em;
        line-height: 1.6;
        color: #444;
    }

    /* ESTILOS GENÉRICOS Y UTILITIES */
    .section-title {
        color: var(--rojo-corazon);
        text-align: center;
        margin-top: 0;
        padding-bottom: 10px;
        border-bottom: 2px dashed rgba(0,0,0,0.1);
    }
    
    .controls {
      display: flex;
      gap: 12px;
      flex-wrap: wrap;
      margin-top: 18px;
      align-items: center;
    }
    /* Estilos de botones (Mantener los de la versión anterior) */
    .btn, .btn-ghost {
      padding: 12px 18px; 
      border-radius: 12px;
      text-decoration: none;
      border: none;
      font-weight: 700;
      cursor: pointer;
      font-size: 14px;
      transition: all 0.2s ease-in-out; 
    }
    .btn-nav {
        background: linear-gradient(90deg, var(--rojo-corazon), var(--rosa-favorito));
        color: white;
        box-shadow: 0 4px 15px rgba(230, 57, 70, 0.4);
    }
    .btn-nav:hover {
      opacity: 0.9;
      transform: translateY(-1px);
    }
    
    /* Footer con control de página */
    .book-footer {
        position: absolute;
        bottom: 0;
        left: 0;
        right: 0;
        padding: 10px 24px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        background: rgba(255, 255, 255, 0.9);
        border-top: 1px solid rgba(0,0,0,0.05);
        z-index: 20;
    }
    .page-indicator {
        font-weight: 600;
        color: #666;
    }

    /* ANIMACIONES GLOBALES */
    
    /* 1. Corazones flotantes (Page 1) */
    .hearts{position:absolute;inset:0;pointer-events:none;overflow:hidden; z-index: 1}
    .heart{position:absolute;width:28px;height:28px;opacity:0.9;transform-origin:center;}
    .heart:before,.heart:after{content:'';position:absolute;width:14px;height:22px;background:var(--heart-color);border-radius:12px 12px 0 0;transform-origin:50% 100%}
    .heart:before{left:3px;transform:rotate(-45deg)}.heart:after{right:3px;transform:rotate(45deg)}

    /* 2. Pétalos cayendo (Page 3) */
    .petals-container {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        overflow: hidden;
        pointer-events: none;
        z-index: 1;
    }
    .petal {
        position: absolute;
        width: 15px;
        height: 15px;
        background: var(--rosa-favorito);
        border-radius: 50% 50% 50% 0;
        opacity: 0.8;
        transform: rotate(45deg);
        filter: blur(0.5px);
        animation: fall linear infinite;
    }
    @keyframes fall {
        0% { transform: translateY(-100px) rotate(0deg); opacity: 0.8; }
        100% { transform: translateY(calc(100vh + 100px)) rotate(360deg); opacity: 0; }
    }
    
    /* RESPONSIVENESS */
    @media (max-width: 768px) {
        .page-container {
            height: 90vh;
        }
        #page1 .card-inner {
            flex-direction: column;
        }
        .photo-wrap {
            flex: none;
            width: 100%;
            max-height: 250px;
        }
        .book-footer {
            flex-direction: column;
            gap: 5px;
        }
        .controls {
            justify-content: center;
        }
    }
  </style>
  
  <link rel="preload" href="photo-portada.jpg" as="image">
</head>
<body>
  <div class="page-container" role="document" aria-label="Libro de cumpleaños interactivo">

    <section class="page active" id="page1" aria-label="Página de bienvenida y dedicatoria">
      <div class="hearts" id="hearts" aria-hidden="true"></div>
      <div class="card-inner">
        <div class="photo-wrap">
          <img src="photo-portada.jpg" alt="Mi niña colochita trigueña" id="mainPhoto" role="presentation">
        </div>
        <div class="content">
          <h1>🎂 Feliz Cumpleaños, Mi Niña Bella</h1>
          <p class="lead">Feliz cumpleaños. Aunque estemos lejos, quiero que sepas que te amo más de lo que las palabras pueden decir. Estos meses juntos han llenado mis días de **alegría** y **amor**.</p>
          
          <ul class="phrases" aria-label="Cosas que me encantan de ti">
            <li class="phrase">Me encanta ser tuyo y que tú seas mía. Cada día contigo vale la pena.</li>
            <li class="phrase" style="border-left-color: var(--azul-cielo)">Me encanta jugar la granjita contigo y pasar horas ahí.</li>
            <li class="phrase" style="border-left-color: var(--rosa-favorito)">Eres mi hondureñita hermosa, mi **nutria** favorita. 💞</li>
          </ul>

          <div class="controls">
            <button class="btn" id="playBtn" aria-expanded="false" aria-controls="ytPlayerWrap">🎵 Escuchar Illegal/Dimple (BTS)</button>
            <button class="btn-ghost" id="muteBtn" style="display:none">🔊 Quitar silencio</button>
            <a class="btn-ghost" id="downloadBtn" href="#" download="regalo_mi_nina.html" role="button">Descargar HTML</a>
          </div>
          
          <div id="ytPlayerWrap"></div> 
        </div>
      </div>
    </section>

    <section class="page" id="page2" aria-label="Página de tus cualidades favoritas">
        <h2 class="section-title" style="color: white; border-bottom-color: rgba(255,255,255,0.5);">✨ Tus Detalles Más Mágicos ✨</h2>
        
        <p style="text-align: center; font-style: italic;">
            Mi vida es más brillante gracias a estos pequeños detalles que te hacen única y completamente mía.
        </p>

        <div class="detalle-grid">
            <div class="detalle-card">
                <h3><span role="img" aria-label="emoji corazón">💖</span> Tu Hermosa Carita</h3>
                <p>Amo tu carita, amo tus **ojitos** que brillan más que las estrellas y ese **lunarcito** perfecto en tu nariz que me vuelve loco.</p>
            </div>
            <div class="detalle-card">
                <h3><span role="img" aria-label="emoji nutria">🦦</span> Mi Nutria Nutricionista</h3>
                <p>Amo tu **inteligencia** y cómo me hablas de tu trabajo. Me encanta llamarte **"mi nutria"** y, por supuesto, lo linda que te ves cuando **usas leggings**.</p>
            </div>
            <div class="detalle-card">
                <h3><span role="img" aria-label="emoji risa">😂</span> Tu Risa de Alegría</h3>
                <p>Me encanta escuchar tu **risa**, esa risa que me alegra el día sin importar lo que esté pasando. Y sí, amo decir **"Chi"** contigo.</p>
            </div>
            <div class="detalle-card">
                <h3><span role="img" aria-label="emoji cabello rizado">👩‍🦱</span> Mi Belleza Trigueña</h3>
                <p>Tu belleza es única: mi **colochita** **trigueña**, la más linda de todas. Eres tan especial y elegante.</p>
            </div>
        </div>

        <div style="margin-top: 30px; text-align: center; padding: 10px; border: 2px dashed rgba(255,255,255,0.8); border-radius: 10px; background: rgba(0,0,0,0.1);">
            <p style="margin: 0; font-weight: bold;">
                <span style="color: var(--rojo-corazon);">ROJO</span>, <span style="color: var(--azul-cielo);">AZUL CIELO</span> y <span style="color: var(--rosa-favorito);">ROSA</span>: ¡Tus colores me recuerdan a ti, llena de vida!
            </p>
        </div>
        
        <p style="text-align: center; margin-top: 25px; font-size: 0.9em; opacity: 0.8;">
            *Si quieres agregar más fotos (como las que me enviaste), renómbralas: `photo-1.jpg`, `photo-2.jpg`, etc., y usa una galería de CSS/JS aquí.
        </p>
    </section>

    <section class="page" id="page3" aria-label="Página de mensaje final y promesa">
        <div class="petals-container" id="petals"></div>
        <div class="final-message-wrap">
            <h2>Mi Promesa de Amor Eterno 🌹</h2>
            <p>
                **Mi amor, mi vida, mi nutria,**<br><br>
                En este día especial, quiero prometerte no solo mi amor, sino mi apoyo incondicional en cada uno de tus sueños, desde la granjita hasta tu carrera. Eres la razón de mis sonrisas y la calma en mis días.<br><br>
                Cada llamada, cada mensaje, cada momento que compartimos, es un tesoro que guardo con celos. Gracias por ser tú: mi colochita, mi inteligente, mi hermosa. No hay distancia que pueda disminuir este amor tan grande.<br><br>
                **¡Feliz cumpleaños, mi niña bella! Te amo hasta el infinito y más allá.**
            </p>
            <p style="font-style: italic; margin-top: 20px; color: var(--rojo-corazon); font-weight: bold;">— Con todo mi corazón, tu novio 💖</p>
        </div>
    </section>
    
    <footer class="book-footer">
        <button class="btn-ghost" id="prevPageBtn" disabled>← Anterior</button>
        <div class="page-indicator" id="pageIndicator">Página 1 de 3</div>
        <button class="btn-nav" id="nextPageBtn">Siguiente →</button>
    </footer>
  </div>

  <script>
    (function() {
      // 1. CONSTANTES GLOBALES
      const YT_ID = 'O2I6soM04oA'; // ID: Illegal/Dimple con Sub. español
      const TOTAL_PAGES = 3;
      
      // Elementos del DOM
      const playBtn = document.getElementById('playBtn');
      const muteBtn = document.getElementById('muteBtn');
      const downloadBtn = document.getElementById('downloadBtn');
      const ytPlayerWrap = document.getElementById('ytPlayerWrap');
      const heartsEl = document.getElementById('hearts');
      const petalsEl = document.getElementById('petals');
      const prevPageBtn = document.getElementById('prevPageBtn');
      const nextPageBtn = document.getElementById('nextPageBtn');
      const pageIndicator = document.getElementById('pageIndicator');
      
      let iframe = null;
      let playing = false;
      let currentPage = 1;

      // 2. LÓGICA DEL REPRODUCTOR (Mismo código fiable)
      function createPlayer() {
        ytPlayerWrap.innerHTML = `<div class="youtube-player-wrap"><iframe id="ytplayer" width="100%" height="200" src="https://www.youtube.com/embed/${YT_ID}?rel=0&autoplay=1&mute=1&controls=1&enablejsapi=1" title="Nuestra canción: Illegal/Dimple de BTS" frameborder="0" allow="autoplay; encrypted-media; picture-in-picture" allowfullscreen></iframe></div>`;
        iframe = document.getElementById('ytplayer');
        muteBtn.style.display = 'inline-block';
        playing = true;
        playBtn.textContent = '⏸️ Pausa';
        playBtn.setAttribute('aria-expanded', 'true');
      }

      function togglePlayPause() {
        if (!iframe) {
          createPlayer();
        } else {
          const command = playing ? 'pauseVideo' : 'playVideo';
          const newStateText = playing ? '▶️ Reproducir' : '⏸️ Pausa';
          
          iframe.contentWindow.postMessage(JSON.stringify({ event: 'command', func: command }), '*');
          
          playing = !playing;
          playBtn.textContent = newStateText;
        }
      }
      
      function unmutePlayer() {
          if (!iframe) return;
          let src = iframe.src;
          if (src.includes('mute=1')) {
              src = src.replace('mute=1', 'mute=0');
          } else {
              if (!src.includes('autoplay=1')) {
                  src += src.includes('?') ? '&autoplay=1' : '?autoplay=1';
              }
          }
          iframe.src = src; 
          muteBtn.textContent = '🔊 ¡Sonando!';
          muteBtn.setAttribute('aria-label', 'Sonando');
          setTimeout(() => { muteBtn.style.display = 'none'; }, 1500);
      }
      
      // 3. LÓGICA DE PAGINACIÓN (NUEVA)
      
      /**
       * Cambia la página activa con transición.
       * @param {number} newPage - El número de la página de destino (1 a TOTAL_PAGES).
       */
      function changePage(newPage) {
        if (newPage < 1 || newPage > TOTAL_PAGES || newPage === currentPage) return;

        const currentEl = document.getElementById(`page${currentPage}`);
        const newEl = document.getElementById(`page${newPage}`);

        // 1. Quitar activo de la página actual
        currentEl.classList.remove('active');
        
        // 2. Transición y actualización
        currentPage = newPage;
        
        // 3. Activar nueva página
        newEl.classList.add('active');

        // 4. Actualizar botones e indicador
        prevPageBtn.disabled = currentPage === 1;
        nextPageBtn.disabled = currentPage === TOTAL_PAGES;
        pageIndicator.textContent = `Página ${currentPage} de ${TOTAL_PAGES}`;
      }

      // 4. LÓGICA DE ANIMACIONES
      
      // Corazones flotantes (Page 1)
      function spawnHeart() {
        if (currentPage !== 1) return; // Solo animar si está en la página 1
        const h = document.createElement('div');
        h.className = 'heart';
        const size = 20 + Math.random() * 36;
        h.style.width = size + 'px';
        h.style.height = size + 'px';
        h.style.left = Math.random() * 90 + '%';
        h.style.bottom = -10 + 'px'; 
        h.style.top = 'auto'; 
        
        const colorVar = Math.random() > 0.5 ? 'var(--rojo-corazon)' : 'var(--rosa-favorito)';
        h.style.setProperty('--heart-color', colorVar); 
        
        heartsEl.appendChild(h);
        const dur = 4000 + Math.random() * 2000;
        h.animate([
          { transform: 'translateY(0) scale(0.8)', opacity: 1 },
          { transform: 'translateY(-500px) scale(1.1) rotate(10deg)', opacity: 0 }
        ], { duration: dur, easing: 'ease-out' });
        
        setTimeout(() => h.remove(), dur + 50);
      }
      
      // Pétalos cayendo (Page 3)
      function spawnPetal() {
        if (currentPage !== 3) return; // Solo animar si está en la página 3
        const p = document.createElement('div');
        p.className = 'petal';
        const size = 10 + Math.random() * 8;
        p.style.width = size + 'px';
        p.style.height = size + 'px';
        p.style.left = Math.random() * 100 + '%';
        p.style.animationDuration = (5 + Math.random() * 5) + 's';
        p.style.animationDelay = (-Math.random() * 5) + 's'; // Distribuye el inicio
        
        petalsEl.appendChild(p);
        
        // Eliminar después de que termine la animación + un poco de margen
        setTimeout(() => p.remove(), 12000); 
      }
      
      // 5. LÓGICA DE DESCARGA
      function handleDownload(e) {
        e.preventDefault();
        const htmlContent = document.documentElement.outerHTML.replace(/src="photo-portada.jpg"/g,'src="photo-portada.jpg"');
        const blob = new Blob([`<!doctype html>\n` + htmlContent], {type:'text/html'});
        const url = URL.createObjectURL(blob);
        
        downloadBtn.href = url;
        downloadBtn.click();
        URL.revokeObjectURL(url);
      }


      // 6. INICIALIZACIÓN
      document.addEventListener('DOMContentLoaded', () => {
        // Asignar listeners
        playBtn.addEventListener('click', togglePlayPause);
        muteBtn.addEventListener('click', unmutePlayer);
        downloadBtn.addEventListener('click', handleDownload);
        prevPageBtn.addEventListener('click', () => changePage(currentPage - 1));
        nextPageBtn.addEventListener('click', () => changePage(currentPage + 1));
        
        // Iniciar animaciones con intervalos
        setInterval(spawnHeart, 700);
        setInterval(spawnPetal, 400); // Más frecuente para el efecto de caída
        
        // Mostrar la primera página
        document.getElementById('page1').classList.add('active');
      });
      
    })();
  </script>
</body>
</html>
