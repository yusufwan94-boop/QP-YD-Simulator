<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>QP-YD | MRSM Gerik Quantum Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700;900&display=swap');
        body { font-family: 'Inter', sans-serif; background: #0f172a; color: #f8fafc; scroll-behavior: smooth; }
        .glass { background: rgba(30, 41, 59, 0.7); backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,0.1); }
        
        /* Simulation Styles */
        .metal-surface { position: relative; height: 280px; background: #1e293b; border-radius: 1.5rem; border: 2px solid #334155; overflow: hidden; }
        .barrier-line { position: absolute; left: 50%; top: 0; bottom: 0; width: 2px; background: rgba(239, 68, 68, 0.4); border-left: 2px dashed #ef4444; z-index: 10; }
        .electron { width: 14px; height: 14px; background: #60a5fa; border-radius: 50%; position: absolute; box-shadow: 0 0 12px #3b82f6; z-index: 20; transition: transform 0.6s cubic-bezier(0.23, 1, 0.32, 1), opacity 0.3s; }
        .photon { width: 12px; height: 12px; border-radius: 50%; position: absolute; left: -20px; z-index: 50; transition: background 0.3s, box-shadow 0.3s; }

        /* Flip Card Logic */
        .flip-card { height: 180px; perspective: 1000px; cursor: pointer; }
        .flip-card-inner { position: relative; width: 100%; height: 100%; transition: transform 0.6s; transform-style: preserve-3d; }
        .flip-card.is-flipped .flip-card-inner { transform: rotateY(180deg); }
        .flip-card-front, .flip-card-back { position: absolute; width: 100%; height: 100%; backface-visibility: hidden; display: flex; flex-direction: column; align-items: center; justify-content: center; padding: 20px; border-radius: 1rem; }
        .flip-card-front { background: #1e293b; border: 1px solid #334155; }
        .flip-card-back { background: #3b82f6; color: white; transform: rotateY(180deg); text-align: center; font-size: 0.85rem; }
        
        /* Custom Range Slider Styling */
        input[type=range] { accent-color: #3b82f6; }
    </style>
</head>
<body class="pb-20">

    <nav class="sticky top-0 z-50 glass border-b border-slate-700 py-4 px-6">
        <div class="max-w-7xl mx-auto flex justify-between items-center">
            <h1 class="text-3xl font-black tracking-tighter text-blue-400">QP-YD</h1>
            <div class="flex gap-6 text-xs font-bold uppercase tracking-widest text-slate-400">
                <a href="#lab" class="hover:text-white transition">Virtual Lab</a>
                <a href="#quiz" class="hover:text-white transition">Observation Logs</a>
            </div>
            <span class="bg-blue-600/20 text-blue-400 px-3 py-1 rounded-full text-[10px] font-bold border border-blue-500/30">MRSM GERIK</span>
        </div>
    </nav>

    <header class="max-w-7xl mx-auto pt-16 pb-12 px-6 text-center">
        <h2 class="text-5xl md:text-7xl font-black mb-6 tracking-tight text-white">The Spectrum <span class="text-blue-500">Effect.</span></h2>
        <p class="text-slate-400 max-w-2xl mx-auto text-lg leading-relaxed">
            Adjust the light frequency manually or select a predefined color to see how the visible spectrum determines electron emission.
        </p>
    </header>

    <main class="max-w-7xl mx-auto px-6 space-y-12">
        
        <section id="lab" class="grid lg:grid-cols-2 gap-8 items-start">
            
            <div class="glass p-8 rounded-3xl space-y-6 shadow-2xl">
                <div class="flex justify-between items-center">
                    <h3 class="text-xl font-bold uppercase tracking-tight text-slate-300 italic">Physical Pool</h3>
                    <div id="statusIndicator" class="text-[10px] bg-slate-500/20 text-slate-400 px-2 py-1 rounded border border-slate-500/20 font-mono">STANDBY</div>
                </div>
                
                <div class="metal-surface shadow-inner" id="arena">
                    <div class="barrier-line"></div>
                </div>

                <div class="space-y-3">
                    <label class="block text-[10px] font-black text-slate-400 uppercase tracking-widest">Select Light Source (Theoretical)</label>
                    <div class="grid grid-cols-4 gap-2">
                        <button onclick="setColor(40, '#ef4444')" class="py-2 rounded-lg bg-red-600/20 border border-red-600/50 hover:bg-red-600 text-xs font-bold transition-all">RED</button>
                        <button onclick="setColor(65, '#22c55e')" class="py-2 rounded-lg bg-green-600/20 border border-green-600/50 hover:bg-green-600 text-xs font-bold transition-all">GREEN</button>
                        <button onclick="setColor(95, '#3b82f6')" class="py-2 rounded-lg bg-blue-600/20 border border-blue-600/50 hover:bg-blue-600 text-xs font-bold transition-all">BLUE</button>
                        <button onclick="setColor(135, '#a855f7')" class="py-2 rounded-lg bg-purple-600/20 border border-purple-600/50 hover:bg-purple-600 text-xs font-bold transition-all">UV</button>
                    </div>
                </div>

                <div class="grid grid-cols-2 gap-4">
                    <div class="bg-slate-800/50 p-4 rounded-2xl border border-slate-700">
                        <label class="block text-[10px] font-black text-blue-400 uppercase mb-2">Photon Frequency (f)</label>
                        <input type="range" id="fIn" min="0" max="150" value="45" class="w-full" oninput="updateCore()">
                        <div id="fOut" class="text-2xl font-black mt-1">45</div>
                    </div>
                    <div class="bg-slate-800/50 p-4 rounded-2xl border border-slate-700">
                        <label class="block text-[10px] font-black text-red-400 uppercase mb-2">Work Function (Φ)</label>
                        <input type="range" id="tIn" min="20" max="100" value="70" class="w-full" oninput="updateCore()">
                        <div id="tOut" class="text-2xl font-black mt-1">70</div>
                    </div>
                </div>

                <button onclick="fireExperiment()" class="w-full bg-blue-600 hover:bg-blue-500 py-5 rounded-2xl font-black text-lg shadow-xl active:scale-95 transition-all uppercase tracking-widest">
                    Execute Emission
                </button>
            </div>

            <div class="glass p-8 rounded-3xl shadow-2xl flex flex-col h-full">
                <h3 class="text-xl font-bold uppercase tracking-tight text-slate-300 italic mb-6">Energy Analysis</h3>
                <div class="flex-grow min-h-[400px]">
                    <canvas id="quantumGraph"></canvas>
                </div>
                <div class="mt-6 p-4 bg-slate-900/80 rounded-xl border border-slate-700 space-y-2">
                    <p class="text-xs font-mono text-slate-400">
                        Equation: <span class="text-blue-400">K<sub>max</sub> = hf - <span id="eqPhi">70</span></span>
                    </p>
                    <p class="text-xs font-mono text-slate-400">
                        Threshold (f₀): <span class="text-emerald-400" id="eqThreshold">70 Hz</span>
                    </p>
                </div>
            </div>
        </section>

        <section id="quiz" class="py-12">
            <h3 class="text-2xl font-black mb-8 text-center uppercase tracking-widest text-slate-500">Observation Logs</h3>
            <div class="grid md:grid-cols-3 gap-6">
                <div class="flip-card" onclick="this.classList.toggle('is-flipped')">
                    <div class="flip-card-inner">
                        <div class="flip-card-front text-center">
                            <span class="text-blue-500 text-xs font-bold mb-2">OBSERVATION 01</span>
                            <p class="text-sm font-bold">Why does Red light (Low f) fail to eject electrons even if bright?</p>
                        </div>
                        <div class="flip-card-back">
                            <p class="font-black mb-2">QUANTIZATION.</p>
                            <p>Each individual Red photon lacks the energy to overcome the Work Function. It doesn't matter how many hit the metal!</p>
                        </div>
                    </div>
                </div>
                <div class="flip-card" onclick="this.classList.toggle('is-flipped')">
                    <div class="flip-card-inner">
                        <div class="flip-card-front text-center">
                            <span class="text-purple-500 text-xs font-bold mb-2">OBSERVATION 02</span>
                            <p class="text-sm font-bold">Why does UV light produce the fastest electrons?</p>
                        </div>
                        <div class="flip-card-back">
                            <p class="font-black mb-2">EXCESS ENERGY.</p>
                            <p>UV has the highest frequency ($E=hf$). Once the Work Function is paid, the remaining energy becomes Kinetic Energy ($1/2mv^2$).</p>
                        </div>
                    </div>
                </div>
                <div class="flip-card" onclick="this.classList.toggle('is-flipped')">
                    <div class="flip-card-inner">
                        <div class="flip-card-front text-center">
                            <span class="text-emerald-500 text-xs font-bold mb-2">OBSERVATION 03</span>
                            <p class="text-sm font-bold">What is the "Threshold Frequency" on the graph?</p>
                        </div>
                        <div class="flip-card-back">
                            <p class="font-black mb-2">X-INTERCEPT.</p>
                            <p>It is the point where Kinetic Energy is exactly ZERO. This is the minimum frequency ($f_0$) required for emission.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <script>
        const arena = document.getElementById('arena');
        const fIn = document.getElementById('fIn');
        const tIn = document.getElementById('tIn');
        const fOut = document.getElementById('fOut');
        const tOut = document.getElementById('tOut');
        const eqPhi = document.getElementById('eqPhi');
        const eqThreshold = document.getElementById('eqThreshold');
        const statusInd = document.getElementById('statusIndicator');

        let photonColor = '#fbbf24'; // Default gold

        function initElectrons() {
            for(let i=0; i<18; i++) {
                let e = document.createElement('div');
                e.className = 'electron';
                e.style.left = (55 + Math.random() * 40) + '%';
                e.style.top = (15 + Math.random() * 70) + '%';
                arena.appendChild(e);
            }
        }
        initElectrons();

        function setColor(freq, hex) {
            fIn.value = freq;
            photonColor = hex;
            updateCore();
        }

        const ctx = document.getElementById('quantumGraph').getContext('2d');
        let chart = new Chart(ctx, {
            type: 'line',
            data: {
                datasets: [{
                    label: 'Kinetic Energy',
                    data: [], borderColor: '#3b82f6', borderWidth: 4, pointRadius: 0, fill: true, backgroundColor: 'rgba(59, 130, 246, 0.05)'
                }, {
                    label: 'Current State',
                    data: [], backgroundColor: '#fbbf24', pointRadius: 10, showLine: false
                }]
            },
            options: {
                responsive: true, maintainAspectRatio: false,
                scales: {
                    y: { min: -120, max: 120, grid: { color: '#334155' }, ticks: { color: '#64748b' } },
                    x: { type: 'linear', min: 0, max: 150, grid: { color: '#334155' }, ticks: { color: '#64748b' } }
                },
                plugins: { legend: { display: false } }
            }
        });

        function updateCore() {
            const f = parseInt(fIn.value);
            const t = parseInt(tIn.value);
            fOut.innerText = f;
            tOut.innerText = t;
            eqPhi.innerText = t;
            eqThreshold.innerText = t + " Hz";

            chart.data.datasets[0].data = [{x: 0, y: -t}, {x: 150, y: 150 - t}];
            chart.data.datasets[1].data = [{x: f, y: f - t}];
            chart.data.datasets[1].backgroundColor = photonColor;
            chart.update('none');

            if (f < t) {
                statusInd.innerText = "NO EMISSION";
                statusInd.className = "text-[10px] bg-red-500/20 text-red-400 px-2 py-1 rounded border border-red-500/20 font-mono";
            } else {
                statusInd.innerText = "EMISSION ACTIVE";
                statusInd.className = "text-[10px] bg-emerald-500/20 text-emerald-400 px-2 py-1 rounded border border-emerald-500/20 font-mono";
            }
        }

        updateCore();

        function fireExperiment() {
            const f = parseInt(fIn.value);
            const t = parseInt(tIn.value);
            const electrons = document.querySelectorAll('.electron');

            for(let i=0; i<5; i++) {
                const p = document.createElement('div');
                p.className = 'photon';
                p.style.background = photonColor;
                p.style.boxShadow = `0 0 15px ${photonColor}`;
                p.style.top = (20 + i * 15) + '%';
                arena.appendChild(p);

                const duration = 1200 - (f * 5);
                const anim = p.animate([{ left: '-20px' }, { left: '110%' }], { duration: duration, easing: 'linear' });
                
                anim.onfinish = () => p.remove();

                setTimeout(() => {
                    if (f >= t) {
                        const targetE = electrons[Math.floor(Math.random() * electrons.length)];
                        if(targetE.style.opacity !== '0') {
                            const speedScale = (f - t) / 15;
                            targetE.style.transition = `all ${0.4 / (speedScale + 1)}s ease-out`;
                            targetE.style.transform = `translateX(600px)`;
                            targetE.style.opacity = '0';
                            
                            setTimeout(() => {
                                targetE.style.transition = 'none';
                                targetE.style.transform = 'none';
                                targetE.style.opacity = '1';
                            }, 2000);
                        }
                    }
                }, duration * 0.5);
            }
        }
    </script>
</body>
</html>
