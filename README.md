<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GamelWise Pro Ultimate - טל</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Assistant:wght@200;400;600;700;800&display=swap');
        
        :root {
            --primary: #4f46e5;
            --primary-light: #818cf8;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
        }

        body { 
            font-family: 'Assistant', sans-serif; 
            background-color: #f8fafc; 
            color: #1e293b;
            scroll-behavior: smooth;
        }

        .glass-card { 
            background: rgba(255, 255, 255, 0.9); 
            backdrop-filter: blur(12px); 
            border: 1px solid rgba(226, 232, 240, 0.8); 
            border-radius: 2rem; 
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.03);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .glass-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 15px 30px -10px rgba(0, 0, 0, 0.08);
        }

        .gradient-bg {
            background: linear-gradient(135deg, #1e293b 0%, #334155 100%);
        }

        .btn-primary {
            background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 100%);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .btn-primary:hover {
            opacity: 0.9;
            transform: scale(1.02);
            box-shadow: 0 10px 20px -5px rgba(79, 70, 229, 0.4);
        }

        .custom-range {
            accent-color: var(--primary);
        }

        /* Animations */
        @keyframes slideIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .animate-slide { animation: slideIn 0.6s ease-out forwards; }

        .progress-ring { transition: stroke-dashoffset 0.35s; transform: rotate(-90deg); transform-origin: 50% 50%; }
    </style>
</head>
<body class="p-4 lg:p-8">

    <div class="max-w-7xl mx-auto">
        <!-- Top Navigation / Header -->
        <header class="flex flex-col md:flex-row justify-between items-start md:items-center mb-10 gap-6 animate-slide">
            <div>
                <div class="flex items-center gap-3 mb-2">
                    <div class="w-10 h-10 bg-indigo-600 rounded-xl flex items-center justify-center text-white shadow-lg">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6"></path></svg>
                    </div>
                    <h1 class="text-4xl font-[800] text-slate-900 tracking-tight">GamelWise <span class="text-indigo-600">Pro</span></h1>
                </div>
                <p class="text-slate-500 font-medium italic">שלום טל, המערכת ניתחה את התיק שלך ומצאה הזדמנויות חדשות.</p>
            </div>
            
            <div class="flex items-center gap-4">
                <div class="bg-white px-5 py-3 rounded-2xl shadow-sm border border-slate-100 text-right">
                    <p class="text-[10px] font-bold text-slate-400 uppercase">מצב שוק נוכחי</p>
                    <p class="text-sm font-bold text-emerald-500 flex items-center gap-1 justify-end">S&P 500: +1.2% 📈</p>
                </div>
                <div class="w-12 h-12 rounded-2xl bg-indigo-50 flex items-center justify-center text-xl cursor-pointer hover:bg-indigo-100 transition-colors">👤</div>
            </div>
        </header>

        <div class="grid grid-cols-1 xl:grid-cols-12 gap-8">
            
            <!-- Left Panel: Smart Inputs & Goals -->
            <div class="xl:col-span-4 space-y-6">
                <!-- Data Entry -->
                <div class="glass-card p-8 animate-slide" style="animation-delay: 0.1s">
                    <h3 class="text-lg font-bold mb-6 flex items-center gap-2 text-slate-800">
                        <span>📊</span> ניהול פרמטרים
                    </h3>
                    <div class="space-y-5">
                        <div class="group">
                            <label class="text-xs font-bold text-slate-400 mb-2 block uppercase tracking-wider group-focus-within:text-indigo-600 transition-colors">צבירה נוכחית</label>
                            <div class="relative">
                                <span class="absolute right-4 top-1/2 -translate-y-1/2 text-slate-400 font-bold">₪</span>
                                <input type="number" id="balance" value="350000" oninput="runCalculations()" class="w-full bg-slate-50 border border-slate-200 pr-10 p-4 rounded-2xl font-bold text-xl text-slate-700 focus:bg-white focus:ring-4 focus:ring-indigo-100 transition-all">
                            </div>
                        </div>

                        <div class="group">
                            <label class="text-xs font-bold text-slate-400 mb-2 block uppercase tracking-wider group-focus-within:text-indigo-600 transition-colors">הפקדה חודשית</label>
                            <div class="relative">
                                <span class="absolute right-4 top-1/2 -translate-y-1/2 text-slate-400 font-bold">₪</span>
                                <input type="number" id="monthly" value="4000" oninput="runCalculations()" class="w-full bg-slate-50 border border-slate-200 pr-10 p-4 rounded-2xl font-bold text-xl text-slate-700 focus:bg-white focus:ring-4 focus:ring-indigo-100 transition-all">
                            </div>
                        </div>

                        <div>
                            <div class="flex justify-between mb-2">
                                <label class="text-xs font-bold text-slate-400 uppercase">דמי ניהול מצבירה</label>
                                <span id="feeVal" class="text-xs font-bold text-indigo-600">0.80%</span>
                            </div>
                            <input type="range" id="fee" min="0.05" max="1.5" step="0.01" value="0.80" oninput="runCalculations()" class="w-full custom-range h-2 bg-slate-200 rounded-lg appearance-none cursor-pointer">
                        </div>
                    </div>
                </div>

                <!-- Goal Progress -->
                <div class="glass-card p-8 animate-slide" style="animation-delay: 0.2s">
                    <h3 class="text-lg font-bold mb-6 text-slate-800">🎯 יעד פרישה: 5 מיליון ₪</h3>
                    <div class="relative h-4 bg-slate-100 rounded-full overflow-hidden mb-4">
                        <div id="goalProgress" class="absolute top-0 right-0 h-full bg-emerald-500 transition-all duration-1000" style="width: 0%"></div>
                    </div>
                    <p class="text-xs text-slate-500 font-medium italic" id="goalStatus">במסלול הנוכחי תגיע ל-72% מהיעד.</p>
                </div>

                <!-- Action Insight -->
                <div class="gradient-bg p-8 rounded-[2.5rem] text-white shadow-xl animate-slide" style="animation-delay: 0.3s">
                    <p class="text-indigo-300 font-bold text-xs uppercase mb-2">חיסכון בדמי ניהול (מצטבר)</p>
                    <h3 class="text-4xl font-[800] mb-6 tracking-tight" id="lostFees">₪0</h3>
                    <div class="p-4 bg-white/10 rounded-2xl border border-white/10 backdrop-blur-md">
                        <p class="text-sm opacity-80 mb-1">טיפ מומחה:</p>
                        <p class="text-sm font-medium">הוזלת דמי הניהול ב-0.2% תוסיף לך חופשה משפחתית בכל שנה בפרישה.</p>
                    </div>
                </div>
            </div>

            <!-- Right Panel: Main Analytics -->
            <div class="xl:col-span-8 space-y-8">
                
                <!-- Summary Metrics Grid -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6 animate-slide" style="animation-delay: 0.2s">
                    <div class="glass-card p-6 border-r-4 border-indigo-500">
                        <p class="text-slate-400 text-[10px] font-bold uppercase mb-1">הון צפוי בפרישה</p>
                        <h4 class="text-2xl font-[800] text-slate-800" id="retireTotal">₪0</h4>
                    </div>
                    <div class="glass-card p-6 border-r-4 border-emerald-500">
                        <p class="text-slate-400 text-[10px] font-bold uppercase mb-1">קצבה חודשית משוערת</p>
                        <h4 class="text-2xl font-[800] text-slate-800" id="estPension">₪0</h4>
                    </div>
                    <div class="glass-card p-6 border-r-4 border-amber-500">
                        <p class="text-slate-400 text-[10px] font-bold uppercase mb-1">גיל פרישה מתוכנן</p>
                        <h4 class="text-2xl font-[800] text-slate-800">67</h4>
                    </div>
                </div>

                <!-- Comparison & Simulation -->
                <div class="glass-card p-8 animate-slide" style="animation-delay: 0.3s">
                    <div class="flex flex-col md:flex-row justify-between items-start md:items-center mb-10 gap-4">
                        <div>
                            <h3 class="text-2xl font-[800] text-slate-800">סימולציית צמיחה רב-מסלולית</h3>
                            <p class="text-slate-500 text-sm">השפעת דמי ניהול ותשואה לאורך 25 שנה</p>
                        </div>
                        <div class="flex gap-2">
                            <button onclick="changeChartType('bar')" class="p-2 hover:bg-slate-100 rounded-lg transition-colors">📊</button>
                            <button onclick="changeChartType('line')" class="p-2 hover:bg-slate-100 rounded-lg transition-colors">📈</button>
                        </div>
                    </div>
                    <div class="h-[400px] w-full">
                        <canvas id="mainChart"></canvas>
                    </div>
                </div>

                <!-- Advanced Tools -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8 animate-slide" style="animation-delay: 0.4s">
                    <!-- Smart Letter Generator -->
                    <div class="glass-card p-8 relative overflow-hidden group">
                        <div class="relative z-10">
                            <div class="w-14 h-14 bg-indigo-50 rounded-2xl flex items-center justify-center text-2xl mb-6">✉️</div>
                            <h4 class="text-xl font-bold mb-3">מחולל מכתבי מיקוח</h4>
                            <p class="text-slate-500 text-sm mb-6 leading-relaxed">המערכת יצרה עבורך מכתב מותאם אישית לסוכן המבוסס על "דמי ניהול ממוצעים" של לקוחות VIP.</p>
                            <button onclick="toggleLetter()" class="btn-primary w-full py-4 rounded-2xl text-white font-bold text-sm">הפק טקסט לסוכן</button>
                        </div>
                    </div>

                    <!-- Optimizer Tool -->
                    <div class="glass-card p-8 border-dashed border-2 border-indigo-200">
                        <div class="w-14 h-14 bg-emerald-50 rounded-2xl flex items-center justify-center text-2xl mb-6">🚀</div>
                        <h4 class="text-xl font-bold mb-3">אופטימיזציית S&P 500</h4>
                        <p class="text-slate-500 text-sm mb-6 leading-relaxed">בדיקה מראה כי מעבר למסלול חוץ-ישראלי עשוי לשפר את הקצבה שלך ב-<span class="text-emerald-600 font-bold">₪2,400</span> לחודש.</p>
                        <button class="w-full py-4 rounded-2xl bg-slate-800 text-white font-bold text-sm hover:bg-slate-900 transition-all">הורד ניתוח השוואתי PDF</button>
                    </div>
                </div>

                <!-- Letter Content Area -->
                <div id="letterBox" class="hidden glass-card p-8 border-2 border-indigo-200 animate-slide">
                    <div class="flex justify-between items-center mb-6">
                        <h5 class="font-bold text-slate-800">טיוטת פנייה לסוכן / חברת ביטוח</h5>
                        <button onclick="copyToClipboard()" class="text-indigo-600 text-xs font-bold hover:underline">📋 העתק טקסט</button>
                    </div>
                    <div id="letterBody" class="bg-indigo-50/50 p-6 rounded-2xl text-slate-700 leading-relaxed text-sm italic">
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Toast Notification -->
    <div id="toast" class="fixed bottom-10 left-1/2 -translate-x-1/2 bg-slate-900 text-white px-8 py-4 rounded-2xl shadow-2xl transition-all duration-500 translate-y-20 opacity-0 z-50">
        המכתב הועתק בהצלחה! ✅
    </div>

    <script>
        let dashboardChart;
        let chartType = 'bar';

        function runCalculations() {
            const balance = parseFloat(document.getElementById('balance').value) || 0;
            const fee = parseFloat(document.getElementById('fee').value) || 0;
            const monthly = parseFloat(document.getElementById('monthly').value) || 0;
            
            document.getElementById('feeVal').innerText = fee.toFixed(2) + "%";

            const years = 25; 
            const targetGoal = 5000000;

            // Wealth Logic
            function getFV(initial, monthlyContrib, annualRate, annualFee, yrs) {
                const netRate = annualRate - (annualFee / 100);
                const months = yrs * 12;
                const monthlyRate = netRate / 12;
                
                const fvBalance = initial * Math.pow(1 + netRate, yrs);
                const fvMonthly = monthlyContrib * ((Math.pow(1 + monthlyRate, months) - 1) / monthlyRate);
                return fvBalance + fvMonthly;
            }

            const current = getFV(balance, monthly, 0.07, fee, years);
            const optimized = getFV(balance, monthly, 0.07, 0.30, years);
            const sp500 = getFV(balance, monthly, 0.10, 0.20, years);

            // UI Updates
            document.getElementById('retireTotal').innerText = '₪' + Math.round(current).toLocaleString();
            document.getElementById('lostFees').innerText = '₪' + Math.round(optimized - current).toLocaleString();
            document.getElementById('estPension').innerText = '₪' + Math.round(current / 195).toLocaleString();

            // Progress Goal
            const progressPercent = Math.min(100, (current / targetGoal) * 100);
            document.getElementById('goalProgress').style.width = progressPercent + "%";
            document.getElementById('goalStatus').innerText = `במסלול הנוכחי תגיע ל-${Math.round(progressPercent)}% מהיעד (5 מיליון ₪).`;

            renderChart(current, optimized, sp500);
            updateLetterText(fee, balance);
        }

        function renderChart(c, o, s) {
            const ctx = document.getElementById('mainChart').getContext('2d');
            if (dashboardChart) dashboardChart.destroy();

            const data = {
                labels: ['מצב נוכחי', 'ניהול אופטימלי', 'פוטנציאל S&P 500'],
                datasets: [{
                    label: 'הון נטו (₪)',
                    data: [c, o, s],
                    backgroundColor: [
                        'rgba(99, 102, 241, 0.8)',
                        'rgba(79, 70, 229, 0.9)',
                        'rgba(16, 185, 129, 0.9)'
                    ],
                    borderColor: ['#4f46e5', '#4338ca', '#059669'],
                    borderWidth: 2,
                    borderRadius: 12,
                    fill: true,
                    tension: 0.4
                }]
            };

            dashboardChart = new Chart(ctx, {
                type: chartType,
                data: data,
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { display: false } },
                    scales: {
                        y: { 
                            beginAtZero: true, 
                            grid: { color: '#f1f5f9' },
                            ticks: { callback: (v) => '₪' + (v/1000000).toFixed(1) + 'M' }
                        },
                        x: { grid: { display: false } }
                    }
                }
            });
        }

        function changeChartType(type) {
            chartType = type;
            runCalculations();
        }

        function updateLetterText(fee, balance) {
            const text = `לכבוד חברת הביטוח / סוכן הביטוח,\n\nשמי טל ואני מחזיק אצלכם בתיק פנסיוני עם צבירה של כ-₪${parseInt(balance).toLocaleString()}.\n\nלאחרונה ביצעתי השוואת תנאים וגיליתי כי דמי הניהול שלי (${fee}%) גבוהים משמעותית מהממוצע המוצע כיום בשוק לצבירה בסדר גודל כזה (0.3%-0.4%).\n\nאבקשכם לעדכן את דמי הניהול בתיק שלי בהתאם, על מנת שאוכל להמשיך את ניהול הכספים אצלכם ולא אאלץ לבחון העברת התיק למתחרים המציעים תנאים טובים יותר.\n\nאשמח למענה בהקדם,\nטל.`;
            document.getElementById('letterBody').innerText = text;
        }

        function toggleLetter() {
            const box = document.getElementById('letterBox');
            box.classList.toggle('hidden');
            if(!box.classList.contains('hidden')) {
                box.scrollIntoView({ behavior: 'smooth' });
            }
        }

        function copyToClipboard() {
            const text = document.getElementById('letterBody').innerText;
            const el = document.createElement('textarea');
            el.value = text;
            document.body.appendChild(el);
            el.select();
            document.execCommand('copy');
            document.body.removeChild(el);

            const toast = document.getElementById('toast');
            toast.classList.remove('translate-y-20', 'opacity-0');
            setTimeout(() => {
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }

        window.onload = runCalculations;
    </script>
</body>
</html>
