```html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Seleksi Kepala Sekolah - Fadli Omi Raharjo</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; }
        .custom-scrollbar::-webkit-scrollbar { width: 6px; }
        .custom-scrollbar::-webkit-scrollbar-track { background: #f1f1f1; }
        .custom-scrollbar::-webkit-scrollbar-thumb { background: #10b981; border-radius: 10px; }
    </style>
</head>
<body class="bg-slate-100 min-h-screen p-2 md:p-6">

    <div id="app" class="max-w-6xl mx-auto bg-white rounded-3xl shadow-2xl overflow-hidden border border-slate-200">
        <!-- Konten akan dimuat oleh JavaScript -->
    </div>

    <script>
        // Konfigurasi Dasar
        const ADMIN_USER = 'admin';
        const ADMIN_PASS = 'muaraman123';
        const CREATOR_NAME = "Fadli Omi Raharjo";
        const TOTAL_TIME = 100 * 60; // 100 menit

        // State Global
        let view = 'welcome';
        let currentQuestionIdx = 0;
        let examData = { name: '', answers: Array(100).fill(null) };
        let timeLeft = TOTAL_TIME;
        let timerInterval = null;
        let submissions = [];
        let selectedSubmission = null;

        // Generate Soal
        const categories = ["AIK", "Manajerial", "Pedagogik", "Supervisi", "Sosial"];
        const questions = Array.from({ length: 100 }, (_, i) => {
            if (i === 0) return { id: 1, category: "AIK", q: "KH Ahmad Dahlan mendirikan Muhammadiyah pada tanggal 8 Dzulhijjah 1330 H, yang bertepatan dengan tanggal?", options: ["18 November 1912", "18 Desember 1912", "18 Oktober 1912", "18 Januari 1912"], correct: 0 };
            if (i === 1) return { id: 2, category: "Manajerial", q: "Dalam manajemen berbasis sekolah, keterlibatan masyarakat direpresentasikan melalui lembaga?", options: ["Komite Sekolah", "Majelis Dikdasmen", "Dewan Guru", "Pimpinan Cabang"], correct: 0 };
            
            return {
                id: i + 1,
                category: categories[i % categories.length],
                q: `[Soal ${i + 1}] Bagaimana implementasi strategi kepemimpinan yang paling tepat dalam mengelola sumber daya sekolah di lingkungan Muhammadiyah untuk mencapai visi unggul dan berkemajuan?`,
                options: [
                    "Melakukan penghematan anggaran tanpa memperhatikan kualitas program",
                    "Menerapkan transparansi dan akuntabilitas berbasis nilai-nilai Al-Ikhlas",
                    "Mendelegasikan semua urusan keuangan kepada bendahara tanpa kontrol",
                    "Menunggu bantuan dari Pimpinan Cabang tanpa ada inisiatif mandiri"
                ],
                correct: 1
            };
        });

        // Utils
        function formatTime(seconds) {
            const h = Math.floor(seconds / 3600);
            const m = Math.floor((seconds % 3600) / 60);
            const s = seconds % 60;
            return `${h > 0 ? h + ':' : ''}${m.toString().padStart(2, '0')}:${s.toString().padStart(2, '0')}`;
        }

        // Core Functions
        function render() {
            const container = document.getElementById('app');
            let content = '';

            // Header
            content += `
                <div class="bg-emerald-900 p-4 md:p-6 text-white flex flex-col md:flex-row justify-between items-center gap-4">
                    <div class="flex items-center gap-4">
                        <div class="bg-white p-2 rounded-xl">
                            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c5/Muhammadiyah_Logo.svg/1200px-Muhammadiyah_Logo.svg.png" class="w-8 h-8 object-contain" alt="Logo">
                        </div>
                        <div>
                            <h1 class="text-lg md:text-xl font-bold leading-tight uppercase tracking-tight text-white">Seleksi Kepala Sekolah</h1>
                            <p class="text-emerald-300 text-[10px] tracking-widest font-semibold uppercase italic">Buatan ${CREATOR_NAME}</p>
                        </div>
                    </div>
                    ${view === 'exam' ? `
                        <div class="flex items-center gap-3">
                            <div class="flex items-center gap-2 px-4 py-2 rounded-2xl border ${timeLeft < 600 ? 'bg-red-500 border-red-400 animate-pulse' : 'bg-emerald-800 border-emerald-700'}">
                                <i class="fas fa-clock"></i>
                                <span class="text-xl font-mono font-bold">${formatTime(timeLeft)}</span>
                            </div>
                        </div>
                    ` : ''}
                </div>
                <div class="p-4 md:p-10">
            `;

            if (view === 'welcome') {
                content += `
                    <div class="py-12 text-center max-w-lg mx-auto">
                        <div class="bg-emerald-50 w-24 h-24 rounded-3xl flex items-center justify-center mx-auto mb-6 shadow-lg border border-emerald-100">
                            <i class="fas fa-book-open text-emerald-600 text-4xl"></i>
                        </div>
                        <h2 class="text-3xl font-black text-slate-800 mb-2">Selamat Datang</h2>
                        <p class="text-emerald-600 text-sm font-bold uppercase tracking-widest mb-6">Sistem Seleksi Terpadu</p>
                        <div class="bg-slate-50 p-6 rounded-2xl border-2 border-dashed border-slate-200 mb-8">
                            <div class="grid grid-cols-2 gap-4">
                                <div class="text-center">
                                    <p class="text-[10px] font-black text-slate-400 uppercase">Durasi</p>
                                    <p class="font-bold text-slate-700">100 Menit</p>
                                </div>
                                <div class="text-center">
                                    <p class="text-[10px] font-black text-slate-400 uppercase">Jumlah Soal</p>
                                    <p class="font-bold text-slate-700">100 Butir</p>
                                </div>
                            </div>
                        </div>
                        <div class="space-y-4">
                            <input type="text" id="nameInput" class="w-full p-5 bg-white border-2 border-slate-100 rounded-2xl focus:border-emerald-500 outline-none text-center text-xl font-bold uppercase" placeholder="INPUT NAMA LENGKAP" value="${examData.name}">
                            <button onclick="startExam()" class="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-black py-5 rounded-2xl shadow-xl transition-all text-lg uppercase">MULAI UJIAN</button>
                            <div class="pt-4 space-y-2">
                                <p class="text-[10px] text-slate-400 font-bold uppercase tracking-tighter">Dikembangkan Oleh <span class="text-slate-600">${CREATOR_NAME}</span></p>
                                <button onclick="switchView('admin_login')" class="text-emerald-600 text-xs font-bold hover:underline">Panel Kontrol Majelis</button>
                            </div>
                        </div>
                    </div>
                `;
            } else if (view === 'exam') {
                const q = questions[currentQuestionIdx];
                content += `
                    <div class="grid grid-cols-1 lg:grid-cols-4 gap-8">
                        <div class="lg:col-span-1 order-2 lg:order-1">
                            <div class="bg-slate-50 p-4 rounded-2xl border border-slate-200 sticky top-6">
                                <h4 class="text-[10px] font-black text-slate-400 mb-4 uppercase tracking-widest flex justify-between">
                                    <span>Navigasi Soal</span>
                                    <span>${examData.answers.filter(a => a !== null).length}/100</span>
                                </h4>
                                <div class="grid grid-cols-5 gap-1.5 max-h-[450px] overflow-y-auto pr-1 custom-scrollbar">
                                    ${questions.map((_, i) => `
                                        <button onclick="jumpToQuestion(${i})" class="aspect-square text-[10px] font-bold rounded-lg flex items-center justify-center transition-all border ${currentQuestionIdx === i ? 'bg-emerald-600 text-white border-emerald-600' : examData.answers[i] !== null ? 'bg-emerald-100 text-emerald-700 border-emerald-200' : 'bg-white text-slate-400 border-slate-200'}">
                                            ${i + 1}
                                        </button>
                                    `).join('')}
                                </div>
                            </div>
                        </div>
                        <div class="lg:col-span-3 order-1 lg:order-2 space-y-6">
                            <div class="flex justify-between items-center">
                                <span class="bg-amber-100 text-amber-700 px-3 py-1 rounded-lg text-[10px] font-black uppercase tracking-wider">BIDANG: ${q.category}</span>
                                <button onclick="showModal()" class="text-[10px] font-black text-red-500 hover:bg-red-50 px-3 py-1 rounded-lg border border-red-100 uppercase">Selesai</button>
                            </div>
                            <div class="mb-10">
                                <h3 class="text-xl md:text-2xl font-bold text-slate-800 leading-snug">
                                    <span class="text-emerald-600 font-black mr-2">Soal ${q.id}.</span> ${q.q}
                                </h3>
                            </div>
                            <div class="grid gap-3">
                                ${q.options.map((opt, i) => `
                                    <button onclick="selectAnswer(${i})" class="group text-left p-5 rounded-2xl border-2 transition-all flex items-center gap-4 ${examData.answers[currentQuestionIdx] === i ? 'border-emerald-500 bg-emerald-50 text-emerald-900 shadow-sm ring-1 ring-emerald-500' : 'border-slate-100 bg-white hover:border-emerald-200'}">
                                        <div class="w-9 h-9 rounded-xl flex items-center justify-center font-black ${examData.answers[currentQuestionIdx] === i ? 'bg-emerald-500 text-white' : 'bg-slate-100 text-slate-400'}">
                                            ${String.fromCharCode(65 + i)}
                                        </div>
                                        <span class="text-base font-semibold">${opt}</span>
                                    </button>
                                `).join('')}
                            </div>
                            <div class="flex justify-between items-center pt-10 border-t border-slate-100">
                                <button onclick="prevQ()" ${currentQuestionIdx === 0 ? 'disabled' : ''} class="flex items-center gap-2 font-black text-sm text-slate-400 hover:text-emerald-600 disabled:opacity-20 uppercase">
                                    <i class="fas fa-chevron-left"></i> Sebelumnya
                                </button>
                                ${currentQuestionIdx === 99 ? 
                                    `<button onclick="showModal()" class="bg-emerald-600 text-white px-12 py-4 rounded-2xl font-black shadow-xl uppercase animate-pulse">Kirim <i class="fas fa-paper-plane ml-2"></i></button>` :
                                    `<button onclick="nextQ()" class="flex items-center gap-2 px-10 py-4 bg-emerald-600 text-white rounded-2xl font-black shadow-lg uppercase">Lanjut <i class="fas fa-chevron-right ml-2"></i></button>`
                                }
                            </div>
                        </div>
                    </div>
                `;
            } else if (view === 'result_sent') {
                content += `
                    <div class="py-24 text-center max-w-md mx-auto">
                        <div class="bg-emerald-500 w-24 h-24 rounded-full flex items-center justify-center mx-auto mb-8 shadow-2xl">
                            <i class="fas fa-check text-white text-4xl"></i>
                        </div>
                        <h2 class="text-3xl font-black text-slate-800 mb-2 uppercase">Jawaban Tersimpan</h2>
                        <p class="text-slate-500 font-medium">Data Anda telah masuk ke sistem audit Majelis Dikdasmen PNF.</p>
                        <div class="mt-12 p-6 bg-slate-50 rounded-2xl border border-slate-100">
                            <p class="text-[10px] font-black text-slate-400 uppercase mb-4 tracking-widest">Digital Signature</p>
                            <p class="text-sm font-bold text-slate-600 italic">"Mencerdaskan kehidupan bangsa melalui kejujuran akademik."</p>
                            <p class="text-[10px] mt-4 font-black text-emerald-600">— ${CREATOR_NAME}</p>
                        </div>
                        <button onclick="location.reload()" class="mt-10 px-10 py-4 bg-slate-900 text-white font-black rounded-2xl shadow-xl uppercase">Keluar</button>
                    </div>
                `;
            } else if (view === 'admin_login') {
                content += `
                    <div class="max-w-xs mx-auto py-12 space-y-8">
                        <div class="text-center">
                            <div class="bg-slate-900 w-20 h-20 rounded-3xl flex items-center justify-center mx-auto mb-6">
                                <i class="fas fa-shield-alt text-white text-3xl"></i>
                            </div>
                            <h2 class="text-2xl font-black text-slate-800 uppercase">Login Admin</h2>
                        </div>
                        <div class="space-y-4">
                            <input type="text" id="adminUser" class="w-full p-4 border-2 border-slate-100 rounded-2xl font-bold outline-none" placeholder="Username">
                            <input type="password" id="adminPass" class="w-full p-4 border-2 border-slate-100 rounded-2xl font-bold outline-none" placeholder="Password">
                            <button onclick="handleAdminLogin()" class="w-full bg-slate-900 text-white font-black py-4 rounded-2xl shadow-xl uppercase">Masuk</button>
                            <button onclick="switchView('welcome')" class="w-full text-slate-400 text-xs font-bold uppercase tracking-widest">Kembali</button>
                        </div>
                    </div>
                `;
            } else if (view === 'admin_dashboard') {
                content += `
                    <div class="space-y-8">
                        <div class="flex justify-between items-center">
                            <div>
                                <h2 class="text-3xl font-black text-slate-800 tracking-tighter uppercase">Panel Rekapitulasi</h2>
                                <p class="text-slate-400 text-xs font-bold uppercase tracking-widest">Otoritas Majelis Dikdasmen</p>
                            </div>
                            <button onclick="switchView('welcome')" class="bg-red-50 text-red-600 px-6 py-3 rounded-2xl font-black text-xs uppercase hover:bg-red-100 transition-all">Logout</button>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                            <div class="bg-emerald-50 p-6 rounded-3xl border border-emerald-100">
                                <p class="text-emerald-600 text-[10px] font-black uppercase tracking-widest">Total Peserta</p>
                                <p class="text-4xl font-black text-emerald-900">${submissions.length}</p>
                            </div>
                            <div class="bg-slate-900 p-6 rounded-3xl shadow-xl">
                                <p class="text-emerald-400 text-[10px] font-black uppercase tracking-widest">Sistem Pengembang</p>
                                <p class="text-lg font-black text-white">${CREATOR_NAME}</p>
                            </div>
                        </div>
                        <div class="bg-white rounded-3xl border border-slate-200 overflow-x-auto shadow-md">
                            <table class="w-full text-left">
                                <thead class="bg-slate-50 text-[10px] font-black text-slate-400 uppercase tracking-widest">
                                    <tr>
                                        <th class="p-6">Peserta</th>
                                        <th class="p-6 text-center">Betul</th>
                                        <th class="p-6 text-center">Durasi</th>
                                        <th class="p-6 text-center">Skor</th>
                                        <th class="p-6 text-center">Detail</th>
                                    </tr>
                                </thead>
                                <tbody class="divide-y divide-slate-50">
                                    ${submissions.map((s, idx) => `
                                        <tr class="hover:bg-slate-50 transition-colors">
                                            <td class="p-6">
                                                <p class="font-black text-slate-800 uppercase text-sm">${s.name}</p>
                                                <p class="text-[9px] text-slate-400">${s.time}</p>
                                            </td>
                                            <td class="p-6 text-center font-bold text-emerald-600">${s.score}</td>
                                            <td class="p-6 text-center font-bold text-blue-600 text-xs">${s.durationSpent}</td>
                                            <td class="p-6 text-center"><span class="bg-slate-900 text-white px-4 py-2 rounded-xl font-black">${s.score}</span></td>
                                            <td class="p-6 text-center">
                                                <button onclick="viewAudit(${idx})" class="p-3 text-emerald-600 bg-emerald-50 rounded-2xl"><i class="fas fa-eye"></i></button>
                                            </td>
                                        </tr>
                                    `).join('')}
                                </tbody>
                            </table>
                        </div>
                    </div>
                `;
            }

            content += `
                </div>
                <!-- Modal -->
                <div id="modal" class="fixed inset-0 bg-slate-900/80 backdrop-blur-md z-50 hidden items-center justify-center p-4">
                    <div class="bg-white rounded-[2rem] max-w-sm w-full p-10 shadow-2xl">
                        <div class="bg-red-50 w-20 h-20 rounded-3xl flex items-center justify-center mx-auto mb-6">
                            <i class="fas fa-exclamation-triangle text-red-500 text-4xl"></i>
                        </div>
                        <h3 class="text-2xl font-black text-center mb-4 text-slate-800 uppercase">Akhiri Ujian?</h3>
                        <p class="text-slate-500 text-center text-sm mb-8 font-medium">Pastikan semua jawaban telah terisi dengan benar.</p>
                        <div class="space-y-3">
                            <button onclick="submitExam()" class="w-full bg-red-500 text-white font-black py-4 rounded-2xl uppercase tracking-widest text-xs">Ya, Selesai</button>
                            <button onclick="hideModal()" class="w-full bg-slate-100 text-slate-600 font-black py-4 rounded-2xl uppercase tracking-widest text-xs">Batal</button>
                        </div>
                    </div>
                </div>
                <!-- Audit Detail Modal -->
                <div id="auditModal" class="fixed inset-0 bg-slate-900/90 z-50 hidden overflow-y-auto p-4 md:p-10">
                    <div id="auditContent" class="max-w-4xl mx-auto"></div>
                </div>
                <!-- Footer -->
                <div class="bg-slate-50 p-4 border-t border-slate-100 flex flex-col md:flex-row justify-between items-center gap-2">
                    <div class="flex items-center gap-2">
                        <div class="w-2 h-2 bg-emerald-500 rounded-full animate-pulse"></div>
                        <span class="text-[10px] font-black text-slate-400 uppercase tracking-[0.2em]">Sistem Seleksi Majelis Dikdasmen PNF</span>
                    </div>
                    <div class="flex items-center gap-1 text-[10px] font-black text-slate-400 uppercase">
                        Dikembangkan oleh <span class="text-emerald-700 ml-1 font-black">${CREATOR_NAME}</span>
                    </div>
                </div>
            `;

            container.innerHTML = content;
        }

        // Logic Handlers
        function switchView(newView) {
            view = newView;
            render();
        }

        function startExam() {
            const name = document.getElementById('nameInput').value.trim();
            if (!name) return alert("Silakan masukkan nama lengkap.");
            examData.name = name;
            view = 'exam';
            timeLeft = TOTAL_TIME;
            timerInterval = setInterval(() => {
                timeLeft--;
                if (timeLeft <= 0) {
                    clearInterval(timerInterval);
                    submitExam("Waktu Habis");
                }
                render();
            }, 1000);
            render();
        }

        function selectAnswer(optIdx) {
            examData.answers[currentQuestionIdx] = optIdx;
            render();
        }

        function nextQ() { if(currentQuestionIdx < 99) { currentQuestionIdx++; render(); } }
        function prevQ() { if(currentQuestionIdx > 0) { currentQuestionIdx--; render(); } }
        function jumpToQuestion(idx) { currentQuestionIdx = idx; render(); }

        function showModal() { document.getElementById('modal').style.display = 'flex'; }
        function hideModal() { document.getElementById('modal').style.display = 'none'; }

        function submitExam(reason = "Selesai Normal") {
            clearInterval(timerInterval);
            let score = 0;
            examData.answers.forEach((ans, idx) => {
                if (ans === questions[idx].correct) score++;
            });

            submissions.push({
                ...examData,
                id: Date.now(),
                score: score,
                time: new Date().toLocaleString(),
                durationSpent: formatTime(TOTAL_TIME - timeLeft),
                status: reason,
                answeredCount: examData.answers.filter(a => a !== null).length
            });

            view = 'result_sent';
            render();
        }

        function handleAdminLogin() {
            const u = document.getElementById('adminUser').value;
            const p = document.getElementById('adminPass').value;
            if (u === ADMIN_USER && p === ADMIN_PASS) {
                view = 'admin_dashboard';
                render();
            } else {
                alert("Username atau Password salah!");
            }
        }

        function viewAudit(idx) {
            const s = submissions[idx];
            const modal = document.getElementById('auditModal');
            const content = document.getElementById('auditContent');
            
            let html = `
                <div class="bg-white rounded-3xl overflow-hidden shadow-2xl border-2 border-slate-900 animate-in zoom-in-95 duration-300">
                    <div class="p-6 bg-slate-900 text-white flex justify-between items-center">
                        <div>
                            <h3 class="text-xl font-black uppercase">${s.name}</h3>
                            <p class="text-emerald-400 text-[10px] font-black uppercase tracking-widest">Audit Keputusan Sistem</p>
                        </div>
                        <button onclick="document.getElementById('auditModal').style.display='none'" class="bg-white/10 px-6 py-2 rounded-xl font-black text-xs uppercase">Tutup</button>
                    </div>
                    <div class="p-8 grid grid-cols-2 md:grid-cols-4 gap-4 bg-slate-50 border-b border-slate-200">
                        <div class="text-center bg-white p-4 rounded-2xl shadow-sm border border-slate-200">
                            <p class="text-[10px] font-black text-slate-400 uppercase">Benar</p>
                            <p class="text-2xl font-black text-emerald-600">${s.score}</p>
                        </div>
                        <div class="text-center bg-white p-4 rounded-2xl shadow-sm border border-slate-200">
                            <p class="text-[10px] font-black text-slate-400 uppercase">Salah</p>
                            <p class="text-2xl font-black text-red-500">${100 - s.score}</p>
                        </div>
                        <div class="text-center bg-white p-4 rounded-2xl shadow-sm border border-slate-200">
                            <p class="text-[10px] font-black text-slate-400 uppercase">Terjawab</p>
                            <p class="text-2xl font-black text-blue-600">${s.answeredCount}</p>
                        </div>
                        <div class="text-center bg-white p-4 rounded-2xl shadow-sm border border-slate-200">
                            <p class="text-[10px] font-black text-slate-400 uppercase">Durasi</p>
                            <p class="text-2xl font-black text-slate-800">${s.durationSpent}</p>
                        </div>
                    </div>
                    <div class="p-6 max-h-[60vh] overflow-y-auto space-y-4 bg-white custom-scrollbar">
                        ${questions.map((q, qIdx) => {
                            const userAns = s.answers[qIdx];
                            const correct = userAns === q.correct;
                            return `
                                <div class="p-4 rounded-xl border-2 ${userAns === null ? 'bg-slate-50 border-slate-100' : correct ? 'bg-emerald-50 border-emerald-100' : 'bg-red-50 border-red-100'}">
                                    <div class="flex justify-between gap-4 mb-2">
                                        <p class="text-sm font-bold text-slate-800"><span class="text-slate-400 font-black">#${q.id}</span> ${q.q}</p>
                                        <div class="shrink-0">
                                            ${userAns === null ? '<span class="text-[8px] font-black px-2 py-1 bg-slate-200 text-slate-500 rounded uppercase">Kosong</span>' : 
                                              correct ? '<span class="text-[8px] font-black px-2 py-1 bg-emerald-500 text-white rounded uppercase">Betul</span>' : 
                                              '<span class="text-[8px] font-black px-2 py-1 bg-red-500 text-white rounded uppercase">Salah</span>'}
                                        </div>
                                    </div>
                                    <div class="grid grid-cols-1 md:grid-cols-2 gap-2 text-[11px]">
                                        <div class="p-2 bg-white/50 rounded-lg">
                                            <p class="text-slate-400 font-black uppercase text-[8px]">Jawaban Peserta</p>
                                            <p class="font-bold ${correct ? 'text-emerald-700' : 'text-red-700'}">
                                                ${userAns === null ? '-' : String.fromCharCode(65 + userAns) + '. ' + q.options[userAns]}
                                            </p>
                                        </div>
                                        ${!correct ? `
                                            <div class="p-2 bg-white/50 rounded-lg border border-blue-50">
                                                <p class="text-blue-400 font-black uppercase text-[8px]">Kunci</p>
                                                <p class="font-bold text-blue-700">${String.fromCharCode(65 + q.correct)}. ${q.options[q.correct]}</p>
                                            </div>
                                        ` : ''}
                                    </div>
                                </div>
                            `;
                        }).join('')}
                    </div>
                </div>
            `;
            content.innerHTML = html;
            modal.style.display = 'block';
        }

        // Init
        render();
    </script>
</body>
</html>

```
