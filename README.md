<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>S.I.A. | AGENTE SANTOS</title>
    <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap" rel="stylesheet">
    <style>
        @font-face {
            font-family: 'Zuume Rough';
            src: local('Zuume Rough Bold'), local('Zuume-Rough-Bold');
        }

        :root {
            --paper: #d9ceb2;
            --ink: #1a1a1a;
            --red-stamp: #a32a2a;
            --font-main: 'Bebas Neue', sans-serif;
            --font-title: 'Zuume Rough', 'Bebas Neue', sans-serif;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            background-color: #121212;
            color: var(--ink);
            font-family: var(--font-main);
            letter-spacing: 1.5px;
        }

        /* --- LOGIN --- */
        #login {
            position: fixed; inset: 0; background: #000; z-index: 10000;
            display: flex; justify-content: center; align-items: center;
        }
        .login-box {
            background: var(--paper); padding: 50px; border-left: 20px solid #8b7e5d;
            box-shadow: 0 0 100px rgba(0,0,0,0.9); text-align: center; width: 90%; max-width: 450px;
        }
        .login-box h1 { font-family: var(--font-title); font-size: 3rem; color: var(--red-stamp); }
        .login-box input {
            width: 100%; padding: 15px; margin: 15px 0; border: 2px solid var(--ink);
            background: rgba(255,255,255,0.2); font-family: var(--font-main); font-size: 1.5rem; text-align: center;
        }

        /* --- CONTENEDOR EXPEDIENTE --- */
        .folder-wrapper {
            background: var(--paper);
            background-image: url('https://www.transparenttextures.com/patterns/paper-fibers.png');
            max-width: 950px; margin: 30px auto; min-height: 100vh;
            padding: 60px; position: relative; display: none;
            box-shadow: 0 0 50px rgba(0,0,0,0.5);
        }

        .confidential-stamp {
            position: absolute; top: 50px; right: 50px;
            border: 4px solid var(--red-stamp); color: var(--red-stamp);
            padding: 10px 20px; font-family: var(--font-title); font-size: 2rem;
            transform: rotate(12deg); opacity: 0.7;
        }

        header { border-bottom: 4px double var(--ink); margin-bottom: 40px; padding-bottom: 10px; }
        h1 { font-family: var(--font-title); font-size: 5rem; line-height: 0.8; }
        
        nav { display: flex; gap: 10px; margin-bottom: 50px; flex-wrap: wrap; }
        .nav-tab {
            background: #b5a585; border: none; padding: 12px 25px;
            font-family: var(--font-main); font-size: 1.4rem; cursor: pointer;
            border-radius: 4px 4px 0 0; transition: 0.3s;
        }
        .nav-tab.active { background: var(--paper); border: 2px solid #b5a585; border-bottom: 4px solid var(--paper); margin-bottom: -4px; }

        .section { display: none; animation: fadeIn 0.6s ease; }
        .section.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* --- PERFIL --- */
        .profile-container { display: grid; grid-template-columns: 320px 1fr; gap: 40px; }
        .profile-photo {
            border: 15px solid #fff; box-shadow: 5px 5px 15px rgba(0,0,0,0.3);
            transform: rotate(-3deg); width: 100%; height: 400px; overflow: hidden;
        }
        .profile-photo img { width: 100%; height: 100%; object-fit: cover; filter: sepia(0.4); }
        .profile-data h2 { font-size: 3.5rem; margin-bottom: 10px; color: var(--ink); }
        .data-line { border-bottom: 1px solid rgba(0,0,0,0.1); padding: 8px 0; font-size: 1.2rem; }
        .data-line b { color: #555; margin-right: 10px; }

        /* --- GALERÍA MIXTA (FOTOS Y VIDEOS) --- */
        .timeline { border-left: 2px solid var(--ink); padding-left: 30px; }
        .mission-box { margin-bottom: 60px; position: relative; }
        .mission-box::before {
            content: ''; position: absolute; left: -37px; top: 10px;
            width: 12px; height: 12px; background: var(--ink); border-radius: 50%;
        }
        .mission-box h3 { font-size: 2.2rem; background: rgba(0,0,0,0.05); padding: 5px 10px; margin-bottom: 20px; }
        
        .photo-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(160px, 1fr)); gap: 15px; }
        
        .media-item { 
            background: #fff; padding: 10px; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); 
            position: relative; transition: 0.3s;
        }
        .media-item::after {
            content: ''; position: absolute; top: -10px; left: 50%; transform: translateX(-50%);
            width: 50px; height: 15px; background: rgba(210,190,140,0.4);
        }
        .media-item img, .media-item video { 
            width: 100%; aspect-ratio: 1; object-fit: cover; filter: grayscale(1); 
        }
        .media-item:hover { transform: scale(1.05) rotate(0deg); z-index: 5; }
        .media-item:hover img, .media-item:hover video { filter: grayscale(0); }

        /* --- REPORTES Y MODAL --- */
        .typica-report {
            background: #fff; padding: 50px; border: 1px solid #ccc;
            background-image: repeating-linear-gradient(#fff, #fff 31px, #e5e5e5 31px, #e5e5e5 32px);
            line-height: 32px; font-size: 1.4rem;
        }

        .case-summary { border: 4px solid var(--ink); padding: 40px; text-align: center; }
        .accept-btn {
            background: var(--red-stamp); color: white; border: none;
            padding: 20px 50px; font-family: var(--font-title); font-size: 2.5rem;
            cursor: pointer; transition: 0.4s; margin-top: 30px;
        }

        #meeting-modal {
            position: fixed; inset: 0; background: rgba(0,0,0,0.9);
            display: none; justify-content: center; align-items: center; z-index: 11000;
        }
        .modal-content {
            background: #1a1a1a; color: #00ff00;
            padding: 40px; border: 2px solid #00ff00; font-family: monospace;
            max-width: 500px; width: 90%; text-align: center;
            box-shadow: 0 0 30px #00ff00;
        }

        .audio-fix { position: fixed; bottom: 20px; left: 20px; background: var(--ink); color: #fff; padding: 10px; font-size: 0.8rem; z-index: 900; }

        @media (max-width: 768px) {
            .profile-container { grid-template-columns: 1fr; }
            h1 { font-size: 3rem; }
            .folder-wrapper { padding: 20px; }
        }
    </style>
</head>
<body>

<div id="login">
    <div class="login-box">
        <h1>S.I.A. ARCHIVE</h1>
        <p>RESTRICCIÓN DE NIVEL 7</p>
        <input type="text" id="u" placeholder="INVESTIGADORA">
        <input type="password" id="p" placeholder="CLAVE (DD.MM.AAAA)">
        <button onclick="auth()" class="accept-btn" style="font-size: 1.5rem; width: 100%;">VALIDAR CREDENCIALES</button>
    </div>
</div>

<div class="folder-wrapper" id="main">
    <div class="confidential-stamp">TOP SECRET</div>
    
    <header>
        <p>REGISTRO DE INTELIGENCIA AMOROSA // REF_0-8</p>
        <h1>DOSSIER SANTOS</h1>
    </header>

    <nav>
        <button class="nav-tab active" onclick="tab(event, 'p1')">PERFIL AGENTE</button>
        <button class="nav-tab" onclick="tab(event, 'p2')">HISTORIAL DE MISIONES</button>
        <button class="nav-tab" onclick="tab(event, 'p3')">ULTIMA MISION</button>
        <button class="nav-tab" onclick="tab(event, 'p4')">NUEVA MISIÓN</button>
    </nav>

    <section id="p1" class="section active">
        <div class="profile-container">
            <div class="profile-photo">
                <img src="Ilsen_1.png" alt="Agente Santos">
            </div>
            <div class="profile-data">
                <h2>ILSEN MILENKA SANTOS VILLCA</h2>
                <div class="data-line"><b>APODOS:</b> ILS, MI AMOR, CORAZÓN, PILSEN</div>
                <div class="data-line"><b>NACIMIENTO:</b> 25/07/2004</div>
                <div class="data-line"><b>RESIDENCIA:</b> LA PAZ - ORURO - COCHABAMBA</div>
                <div class="data-line"><b>HIMNO:</b> MI SUERTE - MORAT</div>
                <div class="data-line"><b>FLOR:</b> TULIPÁN (ROSADO)</div>
                <div class="data-line"><b>DEBILIDAD:</b> HELADO</div>
                <p style="margin-top: 30px; opacity: 0.6; font-style: italic;">
                    * NOTA DEL ASISTENTE M: LA AGENTE PRESENTA UNA RESISTENCIA NULA ANTE EL HELADO Y UNA AFINIDAD CRÍTICA HACIA LOS TULIPANES.
                </p>
            </div>
        </div>
    </section>

    <section id="p2" class="section">
        <div class="timeline">
            
            <div class="mission-box">
                <h3>MISIÓN: CHIMUELO</h3>
                <div class="photo-grid">
                    <div class="media-item"><video src="Chimuelo_1.mp4" loop muted onmouseover="this.play()" onmouseout="this.pause()"></video></div>
                    <script>for(let i=2; i<=9; i++) document.write(`<div class="media-item"><img src="Chimuelo_${i}.jpg"></div>`);</script>
                </div>
            </div>

            <div class="mission-box">
                <h3>MISIÓN: CUMPLEAÑOS</h3>
                <div class="photo-grid">
                    <div class="media-item"><video src="Cumple_1.mp4" loop muted onmouseover="this.play()" onmouseout="this.pause()"></video></div>
                    <script>for(let i=2; i<=16; i++) document.write(`<div class="media-item"><img src="Cumple_${i}.jpg"></div>`);</script>
                </div>
            </div>

            <div class="mission-box">
                <h3>MISIÓN: PIPIRIPI</h3>
                <div class="photo-grid">
                    <div class="media-item"><video src="Pipiripi_1.mp4" loop muted onmouseover="this.play()" onmouseout="this.pause()"></video></div>
                    <script>for(let i=2; i<=9; i++) document.write(`<div class="media-item"><img src="Pipiripi_${i}.jpg"></div>`);</script>
                </div>
            </div>

            <div class="mission-box">
                <h3>MISIÓN: IMPOSICIÓN DE BATA</h3>
                <div class="photo-grid"><script>for(let i=1; i<=7; i++) document.write(`<div class="media-item"><img src="bata_${i}.jpg"></div>`);</script></div>
            </div>

            <div class="mission-box">
                <h3>MISIÓN: STITCH</h3>
                <div class="photo-grid"><script>for(let i=1; i<=3; i++) document.write(`<div class="media-item"><img src="Stitch_${i}.jpg"></div>`);</script></div>
            </div>

            <div class="mission-box">
                <h3>MISIÓN: PIZZA</h3>
                <div class="photo-grid"><script>for(let i=1; i<=9; i++) document.write(`<div class="media-item"><img src="pizza_${i}.jpg"></div>`);</script></div>
            </div>

            <div class="mission-box">
                <h3>MISIÓN: MANQA (ORIGEN)</h3>
                <div class="photo-grid">
                    <div class="media-item"><img src="manqa_1.jpg"></div>
                    <div class="media-item"><img src="manqa_2.jpg"></div>
                </div>
            </div>
        </div>
    </section>

    <section id="p3" class="section">
        <div class="typica-report">
            <h2 style="font-family: var(--font-title); font-size: 3rem; color: var(--red-stamp);">REPORTE TYPICA // 18-02</h2>
            <p>
                A LAS <strong>17:30 HORAS</strong>, LAS COORDENADAS SE ALINEARON EN EL CAFÉ TYPICA. <br><br>
                FUE UN ENCUENTRO QUE DESAFÍO EL CALENDARIO ESTÁNDAR; MIENTRAS EL MUNDO CELEBRABA EL 14, NOSOTRAS CONSTRUIMOS NUESTRO PROPIO TIEMPO EL 18. <br><br>
                LA ATMÓSFERA SE TORNÓ <strong>MÁGICA</strong>. ENTRE EL AROMA A CAFÉ Y LAS MIRADAS COMPLICES, LO BONITO NO FUE EL LUGAR, SINO LA CERTEZA DE ESTAR AHÍ. <br><br>
                <strong>ESTADO DEL REPORTE:</strong> MEMORIA INBORRABLE. ÉXITO ABSOLUTO.
            </p>
        </div>
    </section>

    <section id="p4" class="section">
        <div class="case-summary">
            <h1 style="color: var(--red-stamp);">ASIGNACIÓN: CASO 0-8</h1>
            <div style="text-align: left; max-width: 400px; margin: 30px auto; font-size: 1.5rem; border-left: 5px solid var(--red-stamp); padding-left: 20px;">
                <p><strong>CLASIFICACIÓN:</strong> CONFIDENCIAL </p>
                <p><strong>APERTURA:</strong> 08/01/2024</p>
                <p><strong>ESTADO:</strong> ACTIVO</p>
                <p><strong>INVESTIGADORA:</strong> ILSEN SANTOS</p>
                <p><strong>ASISTENTE:</strong> AGENTE M</p>
            </div>
            <p style="font-size: 1.2rem; margin-bottom: 20px;">
                ESTE CASO NO BUSCA CULPABLES, BUSCA REVELACIONES. EL PORTAFOLIO ESTÁ LISTO PARA SU ENTREGA FINAL.
            </p>
            <button class="accept-btn" onclick="openModal()">ACEPTAR MISIÓN</button>
        </div>
    </section>
</div>

<div id="meeting-modal">
    <div class="modal-content">
        <h2>MISIÓN CONFIRMADA</h2>
        <p>>>> ACCESO CONCEDIDO</p>
        <p>LA REUNIÓN HA SIDO AGENDADA EXITOSAMENTE.</p>
        <div style="border: 1px solid #00ff00; padding: 20px; margin: 20px 0;">
            <p>FECHA: 19/02/2026</p>
            <p>HORA: 13:30</p>
            <p>AGENTE DE CONTACTO: M</p>
            <p>LUGAR: CANCILLERÍA</p>
        </div>
        <p>>>> LAS HERRAMIENTAS DE INVESTIGACIÓN LA ESPERAN, DETECTIVE SANTOS.</p>
        <button onclick="closeModal()" style="background: #00ff00; color: #000; border: none; padding: 10px 20px; font-family: monospace; font-weight: bold; cursor: pointer;">CERRAR TERMINAL</button>
    </div>
</div>

<div class="audio-fix">
    RADIO_SIA: 
    <select onchange="playM(this)" style="background:none; color:white; border:none; font-family:'Bebas Neue';">
        <option value="idiota.mp3">MORAT - IDIOTA</option>
        <option value="la_correcta.mp3">MORAT - LA CORRECTA</option>
    </select>
    <audio id="ap"></audio>
</div>

<script>
    function auth() {
        if(document.getElementById('u').value.toLowerCase() === 'imsantos' && document.getElementById('p').value === '25.07.2004') {
            document.getElementById('login').style.display = 'none';
            document.getElementById('main').style.display = 'block';
        } else { alert("ACCESO DENEGADO"); }
    }

    function tab(e, id) {
        document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
        document.querySelectorAll('.nav-tab').forEach(b => b.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        e.currentTarget.classList.add('active');
    }

    function openModal() { document.getElementById('meeting-modal').style.display = 'flex'; }
    function closeModal() { document.getElementById('meeting-modal').style.display = 'none'; }

    function playM(el) {
        let a = document.getElementById('ap');
        a.src = el.value;
        a.play();
    }
</script>

</body>
</html>
