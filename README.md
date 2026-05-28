
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>MateVida Digital: Desafío Infinito Inclusivo</title>
    <style>
        :root {
            --bg-dark: #0F172A;
            --neon-blue: #00D2FF;
            --neon-purple: #9D00FF;
            --neon-green: #39FF14;
            --neon-yellow: #FFD700;
            --neon-red: #FF0055;
            --card-bg: #1E293B;
            --text-light: #FFFFFF;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Roboto, sans-serif;
            user-select: none;
            -webkit-user-select: none;
        }

        body {
            background-color: var(--bg-dark);
            background-image: radial-gradient(circle at 50% 50%, #1E1B4B 0%, var(--bg-dark) 80%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: clamp(10px, 3vw, 30px);
        }

        .contenedor-juego {
            background: rgba(15, 23, 42, 0.95);
            width: 100%;
            max-width: 500px;
            min-height: 540px;
            border-radius: 24px;
            border: 4px solid var(--neon-blue);
            box-shadow: 0 0 25px rgba(0, 210, 255, 0.25);
            display: flex;
            flex-direction: column;
            overflow: hidden;
            transition: all 0.3s ease;
        }

        .barra-progreso-superior {
            background: #090D16;
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            color: var(--text-light);
            font-weight: 800;
            font-size: clamp(13px, 3.8vw, 16px);
            border-bottom: 2px solid rgba(255, 255, 255, 0.1);
        }

        .medidor {
            color: var(--neon-yellow);
            background: rgba(255, 215, 0, 0.1);
            padding: 4px 10px;
            border-radius: 8px;
            border: 1px solid var(--neon-yellow);
            white-space: nowrap;
        }

        .puntos-marcador {
            color: var(--neon-green);
            background: rgba(57, 255, 20, 0.1);
            padding: 4px 10px;
            border-radius: 8px;
            border: 1px solid var(--neon-green);
        }

        .pantalla {
            padding: clamp(15px, 5vw, 30px) clamp(10px, 4vw, 25px);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 20px;
            text-align: center;
            flex-grow: 1;
            justify-content: center;
        }

        #escenario-juego, #escenario-final { display: none; }

        .titulo-neon {
            font-size: clamp(24px, 6vw, 32px);
            color: var(--text-light);
            font-weight: 900;
            text-shadow: 0 0 10px var(--neon-purple);
            text-transform: uppercase;
        }

        .descripcion {
            color: #94A3B8;
            font-size: clamp(14px, 3.5vw, 16px);
            line-height: 1.5;
            max-width: 400px;
        }

        .btn-principal {
            background: var(--neon-green);
            color: #0F172A;
            border: none;
            padding: 14px 40px;
            border-radius: 18px;
            font-size: clamp(16px, 4vw, 19px);
            font-weight: 800;
            cursor: pointer;
            box-shadow: 0 5px 0 #28C90F;
            transition: all 0.1s;
        }
        .btn-principal:active { transform: translateY(4px); box-shadow: none; }

        .btn-audio-repetir {
            background: rgba(0, 210, 255, 0.1);
            border: 2px solid var(--neon-blue);
            color: var(--neon-blue);
            border-radius: 50%;
            width: 44px;
            height: 44px;
            font-size: 18px;
            cursor: pointer;
            display: flex;
            justify-content: center;
            align-items: center;
            box-shadow: 0 0 8px rgba(0, 210, 255, 0.2);
        }
        .btn-audio-repetir:active { transform: scale(0.95); }

        .zona-ejercicio {
            background: var(--card-bg);
            border: 3px solid var(--neon-purple);
            border-radius: 20px;
            width: 100%;
            padding: clamp(15px, 5vw, 25px);
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 15px;
            flex-wrap: wrap;
            box-shadow: inset 0 0 15px rgba(157, 0, 255, 0.2);
        }

        .texto-operacion {
            font-size: clamp(32px, 8vw, 46px);
            font-weight: 900;
            color: var(--text-light);
            letter-spacing: 1px;
        }

        .caja-respuesta {
            width: clamp(90px, 25vw, 120px);
            height: clamp(55px, 15vw, 70px);
            background: #0F172A;
            border: 3px solid var(--neon-blue);
            border-radius: 14px;
            color: var(--neon-blue);
            font-size: clamp(28px, 7vw, 40px);
            font-weight: 900;
            display: flex;
            justify-content: center;
            align-items: center;
            text-shadow: 0 0 8px rgba(0, 210, 255, 0.5);
        }

        #feedback-operacion {
            min-height: 22px;
            font-weight: 800;
            font-size: 15px;
        }

        .teclado-numerico {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: clamp(6px, 2vw, 12px);
            width: 100%;
            max-width: 360px;
            margin-top: auto;
        }

        .btn-tecla {
            background: #1E293B;
            border: 2px solid #475569;
            color: var(--text-light);
            padding: clamp(12px, 3.5vw, 18px) 0;
            font-size: clamp(20px, 5vw, 26px);
            font-weight: 800;
            border-radius: 14px;
            cursor: pointer;
            box-shadow: 0 4px 0 #0F172A;
            transition: background 0.1s;
        }
        .btn-tecla:active { transform: translateY(2px); box-shadow: none; }
        .btn-tecla.borrar { color: var(--neon-red); border-color: var(--neon-red); }

        .panel-resultados {
            background: var(--card-bg);
            border: 2px solid var(--neon-purple);
            border-radius: 16px;
            width: 100%;
            padding: 15px;
            display: flex;
            justify-content: space-around;
            align-items: center;
            margin: 10px 0;
        }

        .resultado-item {
            display: flex;
            flex-direction: column;
            gap: 5px;
        }

        .resultado-label {
            font-size: 13px;
            color: #94A3B8;
            font-weight: 700;
            text-transform: uppercase;
        }

        .resultado-valor {
            font-size: clamp(24px, 6vw, 32px);
            font-weight: 900;
        }
    </style>
</head>
<body>

    <div class="contenedor-juego">
        <div class="barra-progreso-superior">
            <span class="puntos-marcador">⭐ <span id="marcador-puntos">100</span> pts</span>
            <span class="medidor">Progreso: <span id="num-pregunta">1</span> / 20</span>
        </div>

        <!-- PANTALLA 1: BIENVENIDA -->
        <div id="escenario-inicio" class="pantalla">
            <h3 class="titulo-neon">Reto Infinito 🧠</h3>
            <p class="descripcion">¡Cada partida es totalmente diferente! Resuelve 20 nuevas operaciones creadas al azar por el sistema de MateVida Digital.</p>
            <button class="btn-principal" onclick="iniciarMaraton()">¡Comenzar! 🚀</button>
        </div>

        <!-- PANTALLA 2: JUEGO -->
        <div id="escenario-juego" class="pantalla">
            <div style="display: flex; align-items: center; gap: 10px; width: 100%; justify-content: center;">
                <div class="zona-ejercicio">
                    <span class="texto-operacion" id="bloque-pregunta">0 + 0 =</span>
                    <div class="caja-respuesta" id="bloque-respuesta">?</div>
                </div>
                <button class="btn-audio-repetir" onclick="reproducirPreguntaPorVoz()" title="Escuchar de nuevo">🔊</button>
            </div>

            <div id="feedback-operacion"></div>

            <div class="teclado-numerico">
                <button class="btn-tecla" onclick="marcarNumero('1')">1</button>
                <button class="btn-tecla" onclick="marcarNumero('2')">2</button>
                <button class="btn-tecla" onclick="marcarNumero('3')">3</button>
                <button class="btn-tecla" onclick="marcarNumero('4')">4</button>
                <button class="btn-tecla" onclick="marcarNumero('5')">5</button>
                <button class="btn-tecla" onclick="marcarNumero('6')">6</button>
                <button class="btn-tecla" onclick="marcarNumero('7')">7</button>
                <button class="btn-tecla" onclick="marcarNumero('8')">8</button>
                <button class="btn-tecla" onclick="marcarNumero('9')">9</button>
                <button class="btn-tecla borrar" onclick="marcarNumero('❌')">⌫</button>
                <button class="btn-tecla" onclick="marcarNumero('0')">0</button>
            </div>
        </div>

        <!-- PANTALLA 3: RESULTADOS -->
        <div id="escenario-final" class="pantalla">
            <h2 class="titulo-neon">¡Reto Logrado! 🏆</h2>
            
            <div class="panel-resultados">
                <div class="resultado-item">
                    <span class="resultado-label">Puntaje Final</span>
                    <span class="resultado-valor" id="puntaje-final" style="color: var(--neon-green);">100</span>
                </div>
                <div class="resultado-item">
                    <span class="resultado-label">Precisión</span>
                    <span class="resultado-valor" id="porcentaje-final" style="color: var(--neon-blue);">100%</span>
                </div>
            </div>

            <p class="descripcion" id="mensaje-motivador-final"></p>
            <button class="btn-principal" onclick="volverAlInicio()">Nueva Partida 🔄</button>
        </div>
    </div>

    <script>
        let listaEjercicios = [];
        let indiceActual = 0;
        let respuestaUsuario = "";
        let puntos = 100;
        let totalErrores = 0;
        let audioCtx = null;

        // FÁBRICA MATEMÁTICA EN TIEMPO REAL (Genera ejercicios infinitos y únicos)
        function generarEjerciciosAleatorios() {
            let bancoNuevo = [];
            const tipos = ['suma', 'resta', 'multiplicacion', 'division'];
            
            for (let i = 0; i < 20; i++) {
                // Elige un tipo equitativamente o al azar por rondas
                let tipo = tipos[Math.floor(Math.random() * tipos.length)];
                let num1, num2, resultado, opTexto, vozTexto;

                if (tipo === 'suma') {
                    num1 = Math.floor(Math.random() * 80) + 15; // 15 a 95
                    num2 = Math.floor(Math.random() * 70) + 10; // 10 a 79
                    resultado = num1 + num2;
                    opTexto = `${num1} + ${num2} =`;
                    vozTexto = `${num1} más ${num2}`;
                } 
                else if (tipo === 'resta') {
                    num1 = Math.floor(Math.random() * 150) + 50; // 50 a 199
                    num2 = Math.floor(Math.random() * (num1 - 10)) + 5; // Asegura resultado positivo y lógico
                    resultado = num1 - num2;
                    opTexto = `${num1} - ${num2} =`;
                    vozTexto = `${num1} menos ${num2}`;
                } 
                else if (tipo === 'multiplicacion') {
                    num1 = Math.floor(Math.random() * 11) + 2; // Tablas del 2 al 12
                    num2 = Math.floor(Math.random() * 11) + 2; 
                    resultado = num1 * num2;
                    opTexto = `${num1} × ${num2} =`;
                    vozTexto = `${num1} por ${num2}`;
                } 
                else if (tipo === 'division') {
                    let divisor = Math.floor(Math.random() * 11) + 2; // Divisores del 2 al 12
                    let cociente = Math.floor(Math.random() * 11) + 2; // Resultados del 2 al 12
                    let dividendo = divisor * cociente; // Así garantizamos que sea división exacta
                    resultado = cociente;
                    opTexto = `${dividendo} ÷ ${divisor} =`;
                    vozTexto = `${dividendo} entre ${divisor}`;
                }

                bancoNuevo.push({
                    operacion: opTexto,
                    respuesta: resultado.toString(),
                    textoVoz: vozTexto
                });
            }
            return bancoNuevo;
        }

        function generarAudio() {
            if (!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        }

        function decirTexto(texto) {
            if ('speechSynthesis' in window) {
                window.speechSynthesis.cancel();
                const enunciado = new SpeechSynthesisUtterance(texto);
                enunciado.lang = 'es-ES';
                enunciado.rate = 0.95;
                window.speechSynthesis.speak(enunciado);
            }
        }

        function emitirSonido(evento) {
            generarAudio();
            if(!audioCtx) return;

            const osc = audioCtx.createOscillator();
            const gain = audioCtx.createGain();
            osc.connect(gain); gain.connect(audioCtx.destination);

            if (evento === 'exito') {
                osc.type = 'triangle';
                osc.frequency.setValueAtTime(440, audioCtx.currentTime);
                osc.frequency.exponentialRampToValueAtTime(1320, audioCtx.currentTime + 0.2);
                gain.gain.setValueAtTime(0.12, audioCtx.currentTime);
                osc.start(); osc.stop(audioCtx.currentTime + 0.2);
            } else if (evento === 'fallo') {
                osc.type = 'sawtooth';
                osc.frequency.setValueAtTime(180, audioCtx.currentTime);
                osc.frequency.linearRampToValueAtTime(90, audioCtx.currentTime + 0.25);
                gain.gain.setValueAtTime(0.15, audioCtx.currentTime);
                osc.start(); osc.stop(audioCtx.currentTime + 0.25);
            } else if (evento === 'click') {
                osc.type = 'sine';
                osc.frequency.setValueAtTime(580, audioCtx.currentTime);
                gain.gain.setValueAtTime(0.04, audioCtx.currentTime);
                osc.start(); osc.stop(audioCtx.currentTime + 0.04);
            } else if (evento === 'fanfarria') {
                osc.type = 'sine'; osc.frequency.setValueAtTime(523.25, audioCtx.currentTime);
                gain.gain.setValueAtTime(0.1, audioCtx.currentTime);
                osc.start(); osc.stop(audioCtx.currentTime + 0.4);
            }
        }

        function iniciarMaraton() {
            generarAudio();
            indiceActual = 0;
            respuestaUsuario = "";
            puntos = 100;
            totalErrores = 0;
            
            document.getElementById('marcador-puntos').innerText = puntos;
            
            // ¡Aquí ocurre la magia! Cada inicio produce datos 100% nuevos
            listaEjercicios = generarEjerciciosAleatorios();

            document.getElementById('escenario-inicio').style.display = 'none';
            document.getElementById('escenario-juego').style.display = 'flex';
            
            cargarPreguntaActual();
        }

        function cargarPreguntaActual() {
            respuestaUsuario = "";
            document.getElementById('bloque-respuesta').innerText = "?";
            document.getElementById('bloque-respuesta').style.color = "var(--neon-blue)";
            document.getElementById('feedback-operacion').innerText = "";
            document.getElementById('num-pregunta').innerText = (indiceActual + 1);
            document.getElementById('bloque-pregunta').innerText = listaEjercicios[indiceActual].operacion;
            
            setTimeout(reproducirPreguntaPorVoz, 200);
        }

        function reproducirPreguntaPorVoz() {
            let numPreguntaLector = indiceActual + 1;
            let textoFila = "Pregunta " + numPreguntaLector + ". " + listaEjercicios[indiceActual].textoVoz + " es igual a...";
            decirTexto(textoFila);
        }

        function marcarNumero(valor) {
            emitirSonido('click');
            const fb = document.getElementById('feedback-operacion');
            fb.innerText = "";

            if (valor === '❌') {
                respuestaUsuario = respuestaUsuario.slice(0, -1);
                document.getElementById('bloque-respuesta').innerText = respuestaUsuario || "?";
                return;
            }

            if (respuestaUsuario.length >= 4) return;

            respuestaUsuario += valor;
            document.getElementById('bloque-respuesta').innerText = respuestaUsuario;

            let solucionCorrecta = listaEjercicios[indiceActual].respuesta;

            if (respuestaUsuario === solucionCorrecta) {
                emitirSonido('exito');
                decirTexto("¡Excelente!");
                document.getElementById('bloque-respuesta').style.color = "var(--neon-green)";
                fb.innerText = "¡Excelente! 🎉";
                fb.style.color = "var(--neon-green)";
                
                setTimeout(() => {
                    indiceActual++;
                    if (indiceActual < listaEjercicios.length) {
                        cargarPreguntaActual();
                    } else {
                        finalizarMaraton();
                    }
                }, 700);
            } else {
                if (respuestaUsuario.length >= solucionCorrecta.length) {
                    emitirSonido('fallo');
                    decirTexto("Vuelve a calcularlo.");
                    document.getElementById('bloque-respuesta').style.color = "var(--neon-red)";
                    fb.innerText = "¡Vuelve a calcularlo, tú puedes! 🔍";
                    fb.style.color = "var(--neon-red)";
                    
                    totalErrores++;
                    puntos = Math.max(0, puntos - 5);
                    document.getElementById('marcador-puntos').innerText = puntos;
                    
                    setTimeout(() => {
                        respuestaUsuario = "";
                        document.getElementById('bloque-respuesta').innerText = "?";
                        document.getElementById('bloque-respuesta').style.color = "var(--neon-blue)";
                    }, 800);
                }
            }
        }

        function finalizarMaraton() {
            emitirSonido('fanfarria');
            document.getElementById('escenario-juego').style.display = 'none';
            document.getElementById('escenario-final').style.display = 'flex';

            let intentosTotales = 20 + totalErrores;
            let porcentajePrecision = Math.round((20 / intentosTotales) * 100);

            document.getElementById('puntaje-final').innerText = puntos + " pts";
            document.getElementById('porcentaje-final').innerText = porcentajePrecision + "%";

            let msg = "";
            if (porcentajePrecision >= 90) {
                msg = "¡Espectacular! Demostraste una precisión impecable en este set aleatorio. ¡Eres un maestro de los números! 🚀✨";
            } else if (porcentajePrecision >= 70) {
                msg = "¡Muy buen trabajo! Tu agilidad mental resolvió operaciones completamente nuevas. ¡Felicidades! 💪🧠";
            } else {
                msg = "¡Reto terminado! Sigue jugando para entrenar a tu cerebro con combinaciones matemáticas infinitas. 🌟🎈";
            }
            
            document.getElementById('mensaje-motivador-final').innerText = msg;
            decirTexto("¡Reto logrado! " + msg);
        }

        function volverAlInicio() {
            if ('speechSynthesis' in window) window.speechSynthesis.cancel();
            document.getElementById('escenario-final').style.display = 'none';
            document.getElementById('escenario-inicio').style.display = 'flex';
            document.getElementById('marcador-puntos').innerText = "100";
            document.getElementById('num-pregunta').innerText = "1";
        }
    </script>
</body>
</html>
