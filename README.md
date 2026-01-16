(function() {
    // 1. INJETANDO O CSS (Visual do Painel)
    const css = `
        body { background-color: #000; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; font-family: 'Courier New', Courier, monospace; color: white; overflow: hidden; background-image: radial-gradient(circle, #1a0000 0%, #000 80%); }
        #loginScreen { width: 320px; background: rgba(10, 0, 0, 0.95); border: 2px solid #ff0000; border-radius: 12px; padding: 20px; text-align: center; box-shadow: 0 0 30px rgba(255, 0, 0, 0.6); z-index: 200; }
        #mainPanel { display: none; width: 320px; background: rgba(10, 0, 0, 0.95); border: 2px solid #ff0000; border-radius: 12px; padding: 15px; box-shadow: 0 0 25px rgba(255, 0, 0, 0.4); position: relative; z-index: 10; }
        .header { text-align: center; font-weight: bold; margin-bottom: 15px; text-shadow: 0 0 8px red; color: #ff0000; letter-spacing: 1px; }
        .tabs { display: flex; gap: 5px; margin-bottom: 20px; }
        .tab-btn { flex: 1; padding: 8px 2px; border: 1px solid #ff0000; font-size: 10px; cursor: pointer; background: transparent; color: white; text-transform: uppercase; transition: 0.3s; }
        .tab-btn.active { background: #ff0000; box-shadow: 0 0 10px rgba(255, 0, 0, 0.5); color: black; font-weight: bold; }
        .content { display: none; min-height: 320px; max-height: 420px; overflow-y: auto; }
        .content.active { display: block; }
        .option-row { display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px; font-size: 13px; font-family: sans-serif; }
        .btn-action { width: 100%; padding: 12px; color: white; border-radius: 4px; font-weight: bold; text-transform: uppercase; font-size: 11px; margin-top: 10px; cursor: pointer; transition: 0.4s; border: none; }
        .btn-inject { background: #000; border: 1px solid #ff0000; color: #ff0000; }
        .btn-inject:hover { background: #ff0000; color: #000; }
        .input-key, .input-model { width: 100%; padding: 10px; background: #111; border: 1px solid #ff0000; color: white; margin-bottom: 15px; text-align: center; }
        #hackerOverlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.9); z-index: 500; display: none; pointer-events: none; }
        .hacker-text { position: absolute; color: #ff0000; font-size: 20px; writing-mode: vertical-rl; text-shadow: 0 0 5px red; animation: fall linear infinite; }
        @keyframes fall { to { transform: translateY(100vh); } }
        .ms-counter { text-align: center; color: #00ff00; margin-bottom: 10px; font-size: 12px; }
        .sensi-results { background: rgba(255,0,0,0.1); padding: 10px; border: 1px dashed red; display: none; margin-top: 10px; font-size: 12px; }
        .sensi-results.show { display: block; }
    `;
    const styleSheet = document.createElement("style");
    styleSheet.innerText = css;
    document.head.appendChild(styleSheet);

    // 2. ESTRUTURA DO SITE
    document.body.innerHTML = `
        <div id="loginScreen">
            <div class="header">SYSTEM AUTH</div>
            <input type="password" id="keyInput" class="input-key" placeholder="SUA KEY...">
            <button id="loginBtn" class="btn-action" style="background:red; color:black;">ENTRAR</button>
        </div>
        <div id="hackerOverlay"></div>
        <div id="mainPanel">
            <div class="header">@HSZINNZ_ PANEL</div>
            <div class="tabs">
                <button class="tab-btn active" data-tab="tab1">AIMBOT</button>
                <button class="tab-btn" data-tab="tab2">SENSI</button>
            </div>
            <div id="tab1" class="content active">
                <div class="ms-counter">PING: <span id="ping">15</span>ms</div>
                <div class="option-row"><span>AIMLOCK 95%</span><input type="checkbox" checked></div>
                <div class="option-row"><span>AUTO HEAD</span><input type="checkbox" checked></div>
                <button id="injectBtn" class="btn-action btn-inject">INJETAR E ABRIR FF</button>
            </div>
            <div id="tab2" class="content">
                <input type="text" id="model" class="input-model" placeholder="MODELO CELULAR">
                <button id="genBtn" class="btn-action" style="background:red; color:black;">GERAR SENSI</button>
                <div id="res" class="sensi-results">
                    DPI: <span id="dpi"></span><br>BOTÃO: <span id="btnS"></span>
                </div>
            </div>
        </div>
    `;

    // 3. LÓGICA DE FUNCIONAMENTO
    const keyCorreta = "Hszinnz-lindãodms";

    document.getElementById('loginBtn').onclick = () => {
        if(document.getElementById('keyInput').value === keyCorreta) {
            document.getElementById('loginScreen').style.display = 'none';
            document.getElementById('mainPanel').style.display = 'block';
        } else { alert("KEY ERRADA!"); }
    };

    // Botão Injetar + Abrir Jogo
    document.getElementById('injectBtn').onclick = () => {
        const overlay = document.getElementById('hackerOverlay');
        overlay.style.display = 'block';
        overlay.innerHTML = '';
        
        // Efeito Matrix Vermelho
        for(let i=0; i<30; i++) {
            const s = document.createElement('span');
            s.className = 'hacker-text';
            s.style.left = Math.random()*100+'vw';
            s.style.animationDuration = (Math.random()*2+1)+'s';
            s.innerText = "HSZINNZ_INJECTING_DATA_";
            overlay.appendChild(s);
        }

        setTimeout(() => {
            overlay.style.display = 'none';
            alert("INJETADO! ABRINDO FREE FIRE...");
            // COMANDO PARA ABRIR O APP
            window.location.href = "intent://#Intent;package=com.dts.freefireth;scheme=android-app;end";
        }, 3000);
    };

    // Gerador de Sensi
    document.getElementById('genBtn').onclick = () => {
        document.getElementById('dpi').innerText = Math.floor(Math.random()*200 + 500);
        document.getElementById('btnS').innerText = Math.floor(Math.random()*10 + 45) + "%";
        document.getElementById('res').classList.add('show');
    };

    // Tabs
    document.querySelectorAll('.tab-btn').forEach(b => {
        b.onclick = () => {
            document.querySelectorAll('.content').forEach(c => c.classList.remove('active'));
            document.querySelectorAll('.tab-btn').forEach(t => t.classList.remove('active'));
            document.getElementById(b.dataset.tab).classList.add('active');
            b.classList.add('active');
        }
    });

    // Loop do Ping
    setInterval(() => {
        if(document.getElementById('ping')) 
            document.getElementById('ping').innerText = Math.floor(Math.random()*20 + 5);
    }, 1000);

})();
