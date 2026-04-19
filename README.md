<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GamelWise Pro - טל</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Assistant:wght@200;400;700;800&display=swap');
        body { 
            font-family: 'Assistant', sans-serif; 
            background-color: #f1f5f9; 
            color: #1e293b;
            scroll-behavior: smooth;
        }
        .glass-card { 
            background: rgba(255, 255, 255, 0.95); 
            backdrop-filter: blur(10px); 
            border: 1px solid #e2e8f0; 
            border-radius: 2rem; 
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.05);
        }
        .action-button {
            background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 100%);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .action-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px -5px rgba(79, 70, 229, 0.4);
        }
        .retirement-gradient {
            background: linear-gradient(225deg, #1e293b 0%, #0f172a 100%);
        }
        input:focus {
            outline: none;
            border-color: #6366f1;
            box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.2);
        }
        .animate-fade-in {
            animation: fadeIn 0.8s ease-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body class="p-4 md:p-10 animate-fade-in">

    <div class="max-w-7xl mx-auto">
        <!-- Header -->
        <header class="flex flex-col md:flex-row justify-between items-start md:items-center mb-12 gap-6">
            <div>
                <h1 class="text-5xl font-[800] text-slate-900 tracking-tight mb-2">שלום, <span class="text-indigo-600">טל</span> 👋</h1>
                <p class="text-slate-500 text-lg font-medium italic">מרכז השליטה הפיננסי האישי שלך - גרסת מומחה</p>
            </div>
            <div class="flex items-center gap-4 bg-white p-3 rounded-3xl shadow-sm border border-slate-200">
                <div class="text-right">
                    <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest leading-none mb-1">עדכון אחרון</p>
                    <p id="currentDate" class="text-sm font-bold text-slate-700 leading-none"></p>
                </div>
                <div class="w-12 h-12 rounded-2xl bg-indigo-50 flex items-center justify-center text-2xl">🏆</div>
            </div>
        </header>

        <div class="grid grid-cols-1 xl:grid-cols-12 gap-8">
            
            <!-- Left Panel: Input Section -->
            <div class="xl:col-span-4 space-y-8">
                <div class="glass-card p-8">
                    <h2 class="text-xl font-[800] mb-8 flex items-center gap-3">
                        <span class="w-8 h-8 rounded-xl bg-indigo-100 flex items-center justify-center text-sm">⚙️</span>
                        נתוני התיק שלך
                    </h2>
                    <div class="space-y-6">
                        <div>
                            <label class="text-xs font-bold text-slate-400 mb-2 block uppercase tracking-wider">צבירה נוכחית (₪)</label>
                            <input type="number" id="balance" value="350000" oninput="runCalculations()" class="w-full bg-slate-50 border border-slate-200 p-4 rounded-2xl font-[800] text-xl text-slate-700 transition-all focus:bg-white">
                        </div>
                        <div>
                            <label class="text-xs font-bold text-slate-400 mb-2 block uppercase tracking-wider">דמי ניהול מצבירה (%)</label>
                            <input type="number" id="fee" value="0.80" step="0.01" oninput="runCalculations()" class="w-full bg-slate-50 border border-slate-200 p-4 rounded-2xl font-[800] text-xl text-slate-700 transition-all focus:bg-white">
                        </div>
                        <div>
                            <label class="text-xs font-bold text-slate-400 mb-2 block uppercase tracking-wider">הפקדה חודשית (₪)</label>
                            <input type="number" id="monthly" value="4000" oninput="runCalculations()" class="w-full bg-slate-50 border border-slate-200 p-4 rounded-2xl font-[800] text-xl text-slate-700 transition-all focus:bg-white">
                        </div>
                    </div>
                </div>

                <!-- Retirement Card -->
                <div class="retirement-gradient p-10 rounded-[2.5rem] text-white shadow-2xl relative overflow-hidden">
                    <div class="relative z-10">
                        <p class="text-indigo-400 font-bold text-xs uppercase tracking-widest mb-3">צפי הון נטו בגיל 67</p>
                        <h3 class="text-5xl font-[800] mb-8 tracking-tight" id="retireTotal">₪0</h3>
                        
                        <div class="space-y-4">
                            <div class="flex justify-between items-center p-4 bg-white/5 rounded-2xl border border-white/10">
                                <span class="text-slate-400 text-sm italic">מתוכם דמי ניהול שיאבדו:</span>
                                <span class="text-rose-400 font-bold" id="lostFees">₪0</span>
                            </div>
                            <div class="flex justify-between items-center p-4 bg-white/5 rounded-2xl border border-white/10">
                                <span class="text-slate-400 text-sm italic">קצבה חודשית משוערת:</span>
                                <span class="text-emerald-400 font-bold" id="estPension">₪0</span>
                            </div>
                        </div>
                    </div>
                    <div class="absolute -right-20 -top-20 w-64 h-64 bg-indigo-500/10 rounded-full blur-3xl"></div>
                </div>
            </div>

            <!-- Right Panel: Charts and Tools -->
            <div class="xl:col-span-8 space-y-8">
                
                <!-- Main Comparison Chart -->
                <div class="glass-card p-8">
                    <div class="flex flex-col md:flex-row justify-between items-start md:items-center mb-8 gap-4">
                        <div>
                            <h3 class="text-2xl font-[800] text-slate-800 tracking-tight">השוואת מסלולי תשואה</h3>
                            <p class="text-slate-500 font-medium">הקופה שלך מול מדד ה-S&P 500 וממוצע השוק</p>
                        </div>
                    </div>
                    <div class="h-80">
                        <canvas id="mainChart"></canvas>
                    </div>
                </div>

                <!-- Tools Grid -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                    <!-- Letter Tool -->
                    <div class="glass-card p-8 flex flex-col justify-between hover:border-indigo-400 transition-all cursor-pointer group">
                        <div>
                            <div class="w-16 h-16 bg-rose-50 rounded-2xl flex items-center justify-center text-3xl mb-6 group-hover:scale-110 transition-transform">📧</div>
                            <h4 class="text-xl font-[800] mb-3">מכתב להוזלת עמלות</h4>
                            <p class="text-slate-500 text-sm leading-relaxed mb-8">
                                נמצא פער של <span id="gapIndicator" class="text-rose-500 font-bold">0%</span> מהממוצע. הפק מכתב מוכן לסוכן כדי לחסוך עשרות אלפי שקלים.
                            </p>
                        </div>
                        <button onclick="generateLetter()" class="action-button w-full py-5 rounded-2xl text-white font-[800] text-sm shadow-xl">הפק מכתב לסוכן</button>
                    </div>

                    <!-- Market Comparison -->
                    <div class="glass-card p-8 border-dashed border-2 flex flex-col justify-between group">
                        <div>
                            <div class="w-16 h-16 bg-emerald-50 rounded-2xl flex items-center justify-center text-3xl mb-6 group-hover:scale-110 transition-transform">🚀</div>
                            <h4 class="text-xl font-[800] mb-3">פוטנציאל S&P 500</h4>
                            <p class="text-slate-500 text-sm leading-relaxed mb-8">
                                מעבר למסלול מחקה מדד יכול להוסיף לך כ-<span class="text-emerald-500 font-bold">₪150,000</span> להון הסופי בגלל דמי ניהול נמוכים ותשואה היסטורית עודפת.
                            </p>
                        </div>
                        <button class="w-full py-5 rounded-2xl bg-white border-2 border-slate-100 text-slate-600 font-[800] text-sm hover:bg-slate-50 transition-all">השווה למדד S&P 500</button>
                    </div>
                </div>

                <!-- Hidden Letter Content -->
                <div id="letterBox" class="hidden glass-card p-10 border-2 border-indigo-200 animate-fade-in relative overflow-hidden">
                    <div class="absolute top-0 right-0 p-3 bg-indigo-600 text-white text-[10px] font-bold uppercase tracking-widest">טיוטה מוכנה</div>
                    <div class="flex justify-between items-center mb-8">
                        <h4 class="text-2xl font-[800] text-slate-900">טקסט להעתקה</h4>
                        <button onclick="copyLetter()" class="text-indigo-600 font-[800] text-sm flex items-center gap-2 hover:bg-indigo-50 p-2 rounded-lg transition-colors">
                            <span>📋</span> העתק טקסט
                        </button>
                    </div>
                    <div id="letterContent" class="bg-indigo-50/30 p-8 rounded-3xl text-lg leading-relaxed text-slate-700 italic border border-indigo-100 shadow-inner"></div>
                </div>

            </div>
        </div>
    </div>

    <script>
        let dashboardChart;

        function runCalculations() {
            const balance = parseFloat(document.getElementById('balance').value) || 0;
            const fee = parseFloat(document.getElementById('fee').value) || 0;
            const monthly = parseFloat(document.getElementById('monthly').value) || 0;
            
            const years = 25; // Estimate until retirement
            const marketReturn = 0.08; // 8% avg return
            const marketFee = 0.35; // Target fee

            // Calculate Final Wealth
            function calculateWealth(r, f) {
                const netRate = r - (f / 100);
                const months = years * 12;
                const monthlyRate = netRate / 12;
                
                const fvBalance = balance * Math.pow(1 + netRate, years);
                const fvMonthly = monthly * ((Math.pow(1 + monthlyRate, months) - 1) / monthlyRate);
                return fvBalance + fvMonthly;
            }

            const currentTotal = calculateWealth(marketReturn, fee);
            const optimizedTotal = calculateWealth(marketReturn, marketFee);
            const spTotal = calculateWealth(0.10, 0.25); // S&P 500 estimation

            const lostFees = optimizedTotal - currentTotal;

            // UI Updates
            document.getElementById('retireTotal').innerText = '₪' + Math.round(currentTotal).toLocaleString();
            document.getElementById('lostFees').innerText = '₪' + Math.round(lostFees).toLocaleString();
            document.getElementById('estPension').innerText = '₪' + Math.round(currentTotal / 200).toLocaleString(); 
            
            const gap = (fee - marketFee).toFixed(2);
            document.getElementById('gapIndicator').innerText = gap + "%";

            updateChart(currentTotal, optimizedTotal, spTotal);
        }

        function updateChart(c, o, s) {
            const ctx = document.getElementById('mainChart').getContext('2d');
            if (dashboardChart) dashboardChart.destroy();

            dashboardChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['המצב הנוכחי', 'דמי ניהול אופטימליים', 'מסלול S&P 500'],
                    datasets: [{
                        label: 'הון נטו בפרישה (₪)',
                        data: [c, o, s],
                        backgroundColor: ['#6366f1', '#4f46e5', '#10b981'],
                        borderRadius: 15,
                        barThickness: 60
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { display: false }
                    },
                    scales: {
                        y: { beginAtZero: true, grid: { display: false }, ticks: { callback: (v) => '₪' + v.toLocaleString() } },
                        x: { grid: { display: false } }
                    }
                }
            });
        }

        function generateLetter() {
            const fee = document.getElementById('fee').value;
            const balance = document.getElementById('balance').value;
            const text = `שלום רב,\n\nאני פונה אליך לגבי תיק הגמל/פנסיה שלי. בבדיקה שערכתי, ראיתי שדמי הניהול שלי עומדים על ${fee}%, בזמן שדמי הניהול הממוצעים בשוק לצבירה של ₪${parseInt(balance).toLocaleString()} עומדים על כ-0.35% בלבד.\n\nלאור זאת, אבקש להשוות את תנאי דמי הניהול שלי למקובל בשוק. אשמח לקבל הצעה מעודכנת בהקדם לפני שאבחן חלופות בחברות אחרות.\n\nבברכה,\nטל.`;
            
            document.getElementById('letterContent').innerText = text;
            document.getElementById('letterBox').classList.remove('hidden');
            document.getElementById('letterBox').scrollIntoView({ behavior: 'smooth' });
        }

        function copyLetter() {
            const text = document.getElementById('letterContent').innerText;
            const el = document.createElement('textarea');
            el.value = text;
            document.body.appendChild(el);
            el.select();
            document.execCommand('copy');
            document.body.removeChild(el);
            alert("המכתב הועתק! עכשיו אפשר להדביק בווטסאפ או במייל לסוכן.");
        }

        window.onload = function() {
            document.getElementById('currentDate').innerText = new Date().toLocaleDateString('he-IL');
            runCalculations();
        };
    </script>
</body>
</html>
