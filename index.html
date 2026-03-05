<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quantum Chronology | MRSM Gerik Physics</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;900&family=JetBrains+Mono&display=swap');
        body { font-family: 'Inter', sans-serif; background: #020617; color: #f8fafc; scroll-behavior: smooth; }
        .mono { font-family: 'JetBrains Mono', monospace; }
        .timeline-line { position: absolute; left: 50%; width: 4px; height: 100%; background: linear-gradient(to bottom, #1e293b, #3b82f6, #ec4899, #1e293b); transform: translateX(-50%); z-index: 0; }
        .glass-card { background: rgba(15, 23, 42, 0.8); backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,0.1); }
        .portrait { width: 100%; height: 220px; object-fit: cover; border-radius: 12px; border: 1px solid #334155; }
        .sim-box { width: 100%; height: 320px; background: #000; border-radius: 12px; border: 2px solid #1e293b; position: relative; overflow: hidden; }
        canvas { width: 100%; height: 100%; display: block; }
        
        [data-lang="bm"] .lang-en { display: none; }
        [data-lang="en"] .lang-bm { display: none; }

        .btn-start { background: #059669; }
        .btn-stop { background: #dc2626; }
    </style>
</head>
<body class="pb-20" data-lang="en">

    <nav class="sticky top-0 z-50 bg-slate-950/95 border-b border-slate-800 py-4 px-8 flex justify-between items-center">
        <div class="flex flex-col">
            <span class="text-xs mono text-blue-500 font-bold tracking-widest uppercase">Saturation Searching Lab</span>
            <h1 class="text-2xl font-black tracking-tighter uppercase">Quantum Evolution</h1>
        </div>
        <div class="flex bg-slate-900 p-1 rounded-xl border border-slate-700">
            <button onclick="setLang('en')" id="btn-en" class="px-4 py-1 rounded-lg text-xs font-bold transition-all bg-blue-600 text-white">EN</button>
            <button onclick="setLang('bm')" id="btn-bm" class="px-4 py-1 rounded-lg text-xs font-bold transition-all text-slate-400">BM</button>
        </div>
    </nav>

    <div class="max-w-6xl mx-auto px-6 py-16 relative">
        <div class="timeline-line"></div>
        <div id="segments-container"></div>
    </div>

    <script>
        const activeSims = {};
        const data = [
            { id: 'newton', name: 'Isaac Newton', year: '1704', img: 'https://upload.wikimedia.org/wikipedia/commons/thumb/3/39/GodfreyKneller-IsaacNewton-1689.jpg/300px-GodfreyKneller-IsaacNewton-1689.jpg', theoryEn: 'Light is made of tiny, hard particles called "corpuscles" that travel in straight lines.', theoryBm: 'Cahaya terdiri daripada zarah kecil dan keras dipanggil "korpuskel" yang bergerak lurus.' },
            { id: 'young', name: 'Thomas Young', year: '1801', img: 'https://upload.wikimedia.org/wikipedia/commons/thumb/1/1a/Thomas_Young_%28physician%29.jpg/300px-Thomas_Young_%28physician%29.jpg', theoryEn: 'Light is a wave. Overlapping waves from two slits create Bright (constructive) and Dark (destructive) fringes.', theoryBm: 'Cahaya ialah gelombang. Gelombang bertindih dari dua celah menghasilkan pinggir Terang (membina) dan Gelap (memusnah).' },
            { id: 'dalton', name: 'John Dalton', year: '1803', img: 'https://upload.wikimedia.org/wikipedia/commons/thumb/d/d4/John_Dalton_by_Charles_Turner.jpg/300px-John_Dalton_by_Charles_Turner.jpg', theoryEn: 'The atom is an indivisible, solid sphere. All matter is made of these building blocks.', theoryBm: 'Atom ialah sfera pepejal yang tidak boleh dibahagi. Semua jirim terdiri daripada blok binaan ini.' },
            { id: 'thomson', name: 'J.J. Thomson', year: '1897', img: 'https://upload.wikimedia.org/wikipedia/commons/thumb/c/c1/J.J_Thomson.jpg/300px-J.J_Thomson.jpg', theoryEn: 'Discovered the electron. The atom is a positive sphere with embedded negative electrons.', theoryBm: 'Menemui elektron. Atom ialah sfera positif dengan elektron negatif terbenam di dalamnya.' },
            { id: 'planck', name: 'Max Planck', year: '1900', img: 'https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/Max_Planck_1933.jpg/300px-Max_Planck_1933.jpg', theoryEn: 'Energy is not continuous but emitted in discrete packets called Quanta (E=hf).', theoryBm: 'Tenaga tidak berterusan tetapi dipancarkan dalam paket diskrit dipanggil Kuantum.' },
            { id: 'einstein', name: 'Albert Einstein', year: '1905', img: 'https://upload.wikimedia.org/wikipedia/commons/thumb/d/d3/Albert_Einstein_Head.jpg/300px-Albert_Einstein_Head.jpg', theoryEn: 'Explained the Photoelectric Effect. Light acts as photons that can knock electrons off metal.', theoryBm: 'Menerangkan Kesan Fotoelektrik. Cahaya bertindak sebagai foton yang boleh mengeluarkan elektron.' },
            { id: 'bohr', name: 'Niels Bohr', year: '1913', img: 'https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Niels_Bohr.jpg/300px-Niels_Bohr.jpg', theoryEn: 'Electrons travel in fixed, circular orbits (energy levels) around the nucleus.', theoryBm: 'Elektron bergerak dalam orbit bulat yang tetap (tahap tenaga) di sekeliling nukleus.' },
            { id: 'debroglie', name: 'Louis De Broglie', year: '1924', img: 'https://upload.wikimedia.org/wikipedia/commons/thumb/d/d2/Louis_de_Broglie_Portrait.jpg/300px-Louis_de_Broglie_Portrait.jpg', theoryEn: 'Proposed matter waves. Electrons passing through a gap show a diffraction pattern on a detector.', theoryBm: 'Mencadangkan gelombang jirim. Elektron melalui celah sempit menunjukkan corak belauan pada pengesan.' }
        ];

        const container = document.getElementById('segments-container');
        data.forEach((item, index) => {
            const isEven = index % 2 === 0;
            container.innerHTML += `
                <div class="relative z-10 grid md:grid-cols-12 gap-8 mb-40 items-start">
                    <div class="md:col-span-3 text-center ${isEven ? '' : 'md:order-3'}">
                        <h3 class="text-3xl font-black mb-2">${item.name}</h3>
                        <img src="${item.img}" class="portrait mb-2" alt="${item.name}">
                        <div class="mono text-blue-500 font-black text-xl">${item.year}</div>
                    </div>
                    <div class="md:col-span-4 glass-card p-6 rounded-3xl ${isEven ? '' : 'md:order-2'}">
                        <div class="mb-6">
                            <h4 class="font-black text-blue-400 uppercase text-xs tracking-widest lang-en">Theory Proposal</h4>
                            <h4 class="font-black text-blue-400 uppercase text-xs tracking-widest lang-bm">Cadangan Teori</h4>
                            <p class="text-sm mt-3 leading-relaxed lang-en">${item.theoryEn}</p>
                            <p class="text-sm mt-3 leading-relaxed lang-bm">${item.theoryBm}</p>
                        </div>
                        <button onclick="toggleSim('${item.id}')" id="btn-${item.id}" class="btn-start px-6 py-3 rounded-xl text-[10px] font-black uppercase tracking-widest w-full transition-all">Start Simulation</button>
                    </div>
                    <div class="md:col-span-5 ${isEven ? '' : 'md:order-1'}">
                        <div class="sim-box"><canvas id="canvas-${item.id}"></canvas></div>
                    </div>
                </div>`;
        });

        function setLang(lang) {
            document.body.setAttribute('data-lang', lang);
            document.getElementById('btn-en').className = lang === 'en' ? "px-4 py-1 rounded-lg text-xs font-bold transition-all bg-blue-600 text-white" : "px-4 py-1 rounded-lg text-xs font-bold transition-all text-slate-400";
            document.getElementById('btn-bm').className = lang === 'bm' ? "px-4 py-1 rounded-lg text-xs font-bold transition-all bg-blue-600 text-white" : "px-4 py-1 rounded-lg text-xs font-bold transition-all text-slate-400";
        }

        function toggleSim(id) {
            const btn = document.getElementById(`btn-${id}`);
            if (activeSims[id]) {
                activeSims[id] = false;
                btn.innerText = "Start Simulation";
                btn.className = btn.className.replace('btn-stop', 'btn-start');
            } else {
                activeSims[id] = true;
                btn.innerText = "Stop Simulation";
                btn.className = btn.className.replace('btn-start', 'btn-stop');
                runSim(id);
            }
        }

        function runSim(id) {
            const canvas = document.getElementById(`canvas-${id}`);
            const ctx = canvas.getContext('2d');
            canvas.width = canvas.offsetWidth;
            canvas.height = canvas.offsetHeight;
            let frame = 0;
            let dbParticles = [];

            const draw = () => {
                if (!activeSims[id]) return;
                ctx.fillStyle = 'black'; ctx.fillRect(0,0, canvas.width, canvas.height);
                
                if(id === 'newton') {
                    ctx.fillStyle = '#3b82f6';
                    for(let i=0; i<8; i++) {
                        let x = (frame*4 + i*60) % canvas.width;
                        ctx.beginPath(); ctx.arc(x, canvas.height/2, 3, 0, Math.PI*2); ctx.fill();
                    }
                }
                
                if(id === 'young') {
                    const s1y = canvas.height/2 - 25, s2y = canvas.height/2 + 25;
                    // Waves
                    ctx.globalCompositeOperation = 'lighter';
                    for(let r=0; r<canvas.width-50; r+=25) {
                        ctx.strokeStyle = `rgba(34, 211, 238, ${0.4 - r/canvas.width})`;
                        ctx.beginPath(); ctx.arc(30, s1y, (r + frame)%canvas.width, -Math.PI/2, Math.PI/2); ctx.stroke();
                        ctx.beginPath(); ctx.arc(30, s2y, (r + frame)%canvas.width, -Math.PI/2, Math.PI/2); ctx.stroke();
                    }
                    // Interference Fringe Screen (Right side)
                    ctx.globalCompositeOperation = 'source-over';
                    for(let y=0; y<canvas.height; y++) {
                        let d1 = Math.sqrt(Math.pow(canvas.width-40, 2) + Math.pow(y-s1y, 2));
                        let d2 = Math.sqrt(Math.pow(canvas.width-40, 2) + Math.pow(y-s2y, 2));
                        let diff = Math.abs(d1 - d2);
                        let intensity = Math.pow(Math.cos(diff * 0.15), 2);
                        ctx.fillStyle = `rgba(34, 211, 238, ${intensity})`;
                        ctx.fillRect(canvas.width-30, y, 20, 1);
                    }
                    ctx.fillStyle = 'white'; ctx.fillRect(25, 0, 5, canvas.height);
                    ctx.clearRect(25, s1y-2, 5, 4); ctx.clearRect(25, s2y-2, 5, 4);
                }

                if(id === 'dalton') {
                    ctx.fillStyle = '#10b981'; ctx.beginPath(); ctx.arc(canvas.width/2, canvas.height/2, 50, 0, Math.PI*2); ctx.fill();
                }

                if(id === 'thomson') {
                    ctx.fillStyle = 'rgba(245, 158, 11, 0.4)'; ctx.beginPath(); ctx.arc(canvas.width/2, canvas.height/2, 60, 0, Math.PI*2); ctx.fill();
                    ctx.fillStyle = 'blue';
                    for(let i=0; i<6; i++) {
                        let ang = (frame*0.02) + (i * Math.PI/3);
                        ctx.beginPath(); ctx.arc(canvas.width/2 + Math.cos(ang)*35, canvas.height/2 + Math.sin(ang)*35, 6, 0, Math.PI*2); ctx.fill();
                    }
                }

                if(id === 'planck') {
                    ctx.fillStyle = '#a855f7'; let pos = (frame*3) % canvas.width;
                    ctx.fillRect(pos, canvas.height/2 - 10 + Math.sin(frame*0.1)*20, 15, 15);
                }

                if(id === 'einstein') {
                    ctx.fillStyle = 'yellow'; ctx.fillRect((frame*5)% (canvas.width/2), canvas.height/2, 8, 2);
                    ctx.fillStyle = '#475569'; ctx.fillRect(canvas.width/2, 20, 15, canvas.height-40);
                    if((frame*5)%canvas.width > canvas.width/2) {
                        ctx.fillStyle = '#3b82f6'; ctx.beginPath(); ctx.arc(canvas.width/2 + 20 + (frame%50), canvas.height/2 - (frame%30), 4, 0, Math.PI*2); ctx.fill();
                    }
                }

                if(id === 'bohr') {
                    ctx.strokeStyle = '#4f46e5'; ctx.beginPath(); ctx.arc(canvas.width/2, canvas.height/2, 50, 0, Math.PI*2); ctx.stroke();
                    ctx.fillStyle = 'cyan'; ctx.beginPath(); ctx.arc(canvas.width/2 + Math.cos(frame*0.05)*50, canvas.height/2 + Math.sin(frame*0.05)*50, 6, 0, Math.PI*2); ctx.fill();
                    ctx.fillStyle = 'red'; ctx.beginPath(); ctx.arc(canvas.width/2, canvas.height/2, 12, 0, Math.PI*2); ctx.fill();
                }

                if(id === 'debroglie') {
                    // Diffraction Simulation
                    if(frame % 2 === 0) dbParticles.push({x: 0, y: canvas.height/2 + (Math.random()-0.5)*10, angle: (Math.random()-0.5)*0.1});
                    dbParticles.forEach((p, i) => {
                        p.x += 4;
                        if(p.x > 60) { // Gap logic: electron "waves" through the gap
                            let diff = (Math.tan(Math.asin(Math.sin(p.angle) || 0.01))) * (p.x - 60);
                            // Apply a probability distribution (Gaussian-like)
                            if(!p.fixedAngle) p.fixedAngle = (Math.tan((Math.random()-0.5) * 1.5));
                            p.y += p.fixedAngle * 2;
                        }
                        ctx.fillStyle = 'rgba(236, 72, 153, 0.8)';
                        ctx.beginPath(); ctx.arc(p.x, p.y, 2, 0, Math.PI*2); ctx.fill();
                        if(p.x > canvas.width - 40) { // Hit detector
                            ctx.fillStyle = 'rgba(236, 72, 153, 0.2)';
                            ctx.fillRect(canvas.width-30, p.y-5, 15, 10);
                            dbParticles.splice(i, 1);
                        }
                    });
                    ctx.fillStyle = 'white'; ctx.fillRect(60, 0, 5, canvas.height/2 - 10); ctx.fillRect(60, canvas.height/2 + 10, 5, canvas.height/2);
                }

                frame++;
                requestAnimationFrame(draw);
            };
            draw();
        }
    </script>
</body>
</html>
