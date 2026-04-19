<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GamelWise Pro - שלום טל</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Assistant:wght@200;400;700;800&display=swap');
        body { font-family: 'Assistant', sans-serif; background: #f8fafc; color: #1e293b; }
        .glass { background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(10px); border: 1px solid #e2e8f0; border-radius: 1.5rem; }
        .card { transition: all 0.3s ease; border: 1px solid #e2e8f0; }
        .card:hover { transform: translateY(-3px); box-shadow: 0 10px 20px rgba(0,0,0,0.05); }
        .btn-primary { background: linear-gradient(135deg, #6366f1 0%, #4f46e5 100%); color: white; transition: all 0.3s; }
        .btn-primary:hover { opacity: 0.9; transform: scale(1.02); }
    </style>
</head>
<body class="p-4 md:p-8">

    <div class="max-w-6xl mx-auto">
        <header class="flex flex-col md:flex-row justify-between items-start md:items-center mb-10 gap-4">
            <div>
                <h1 class="text-4xl font-800 text-slate-900 tracking-tight">שלום, <span class="text-indigo-600">טל</span> 👋</h1>
                <p class="text-slate-500 font-medium">מרכז השליטה הפיננסי שלך - עדכון אחרון: אפריל 2026</p>
            </div>
            <div class="bg-white p-2 rounded-2xl border border-slate-200 shadow-sm flex items-center gap-4">
                <span class="px-4 py-1 bg-indigo-50 text-indigo-700 rounded-lg font-bold text-sm">חשבון פרימיום</span>
                <div class="h-8 w-px bg-slate-200"></div>
                <button onclick="location.reload()" class="p-2 hover:bg-slate-100 rounded-xl">🔄</button>
            </div>
        </header>

        <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">
            
            <div class="lg:col-span-4 space-y-6">
                <div class="glass p-6 shadow-sm">
                    <h2 class="text-xl font-bold mb-6 flex items-center gap-2">⚙️ הגדרות תיק נוכחי</h2>
                    <div class="space-y-4">
                        <div>
                            <label class="block text-xs font-bold text-slate-400 mb-2 uppercase">צבירה נוכחית (₪)</label>
                            <input type="number" id="balance" value="250000" oninput="calculateAll()" class="w-full p-3 rounded-xl border border-slate-200 font-bold focus:ring-2 focus:ring-indigo-500 outline-none">
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-slate-400 mb-2 uppercase">דמי ניהול מהצבירה (%)</label>
                            <input type="number" id="fee" value="0.7" step="0.01" oninput="calculateAll()" class="w-full p-3 rounded-xl border border-slate-200 font-bold focus:ring-2 focus:ring-indigo-500 outline-none">
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-slate-400 mb-2 uppercase">הפקדה חודשית (₪)</label>
                            <input type="number" id="monthly" value="2000" oninput="calculateAll()" class="w-full p-3 rounded-xl border border-slate-200 font-bold focus:ring-2 focus:ring-indigo-500 outline-none">
                        </div>
                    </div>
                </div>

                <div class="bg-slate-900 text-white p-8 rounded-[2rem] shadow-xl overflow-hidden relative">
                    <div class="relative z-10">
                        <h3 class="text-indigo-300 font-bold text-sm mb-2 uppercase">תחזית גיל 67</h3>
                        <p class="text-4xl font-800 mb-4" id="retirementTotal">₪0</p>
                        <p class="text-xs text-slate-400 leading-relaxed mb-6">החישוב מבוסס על תשואה שנתית ממוצעת של 7% בניכוי דמי הניהול שלך.</p>
                        <div class="bg-white/10 p-4 rounded-2xl">
                            <p class="text-xs text-indigo-200 mb-1">כמה דמי ניהול תשלם עד הפרישה?</p>
                            <p class="font-bold text-rose-400" id="totalFeesPaid">₪0</p>
                        </div>
                    </div>
                    <div class="absolute -right-10 -bottom-10 w-40 h-40 bg-indigo-500/10 rounded-full blur-3xl"></div>
                </div>
            </div>

            <div class="lg:col-span-8 space-y-8">
                
                <div class="glass p-8 shadow-sm">
                    <div class="flex justify-between items-center mb-8">
                        <h3 class="text-xl font-800">השוואת ביצועים מול השוק</h3>
                        <div class="flex gap-2">
                            <span class="flex items-center gap-1 text-xs font-bold text-indigo-600 bg-indigo-50 px-3 py-1 rounded-full border border-indigo-100">
                                <span class="w-2 h-2 bg-indigo-600 rounded-full"></span> התיק שלך
                            </span>
                        </div>
                    </div>
                    <div class="h-64">
                        <canvas id="mainChart"></canvas>
                    </div>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="card bg-white p-6 rounded-2xl flex flex-col justify-between">
                        <div>
                            <div class="w-12 h-12 bg-rose-50 rounded-xl flex items-center justify-center text-2xl mb-4">📢</div>
                            <h4 class="font-bold text-lg mb-2">דמי הניהול שלך יקרים!</h4>
                            <p class="text-sm text-slate-500 leading-relaxed mb-6">מצאנו שאתה משלם <span id="feeGapText" class="text-rose-500 font-bold"></span> יותר מהממוצע בשוק למסלול שלך.</p>
                        </div>
                        <button onclick="generateLetter()" class="btn-primary w-full py-3 rounded-xl font-bold text-sm">הפק מכתב לסוכן</button>
                    </div>

                    <div class="card bg-white p-6 rounded-2xl flex flex-col justify-between">
                        <div>
                            <div class="w-12 h-12 bg-emerald-50 rounded-xl flex items-center justify-center text-2xl mb-4">🚀</div>
                            <h4 class="font-bold text-lg mb-2">שדרוג ל-S&P 500</h4>
                            <p class="text-sm text-slate-500 leading-relaxed mb-6">מעבר למסלול מחקה מדד עשוי להגדיל את הקצבה החודשית שלך בכ-₪1,400.</p>
                        </div>
                        <button class="bg-slate-100 hover:bg-slate-200 text-slate-700 w-full py-3 rounded-xl font-bold text-sm transition">השווה מסלולים</button>
                    </div>
                </div>

                <div id="letterArea" class="hidden glass p-8 border-2 border-indigo-200 animate-fade-in">
                    <div class="flex justify-between items-center mb-4">
                        <h4 class="font-bold text-indigo-900 text-lg">טיוטה מוכנה לסוכן הביטוח</h4>
                        <button onclick="copyLetter()" class="text-indigo-600 font-bold text-sm underline">העתק טקסט</button>
                    </div>
                    <div id="letterContent" class="bg-indigo-50/50 p-6 rounded-xl text-sm leading-loose text-slate-700 whitespace-pre-wrap"></div>
                </div>

            </div>
        </div>
    </div>

    <script>
        let mainChart;

        function calculateAll() {
            const balance = parseFloat(document.getElementById('balance').value) || 0;
            const fee = parseFloat(document.getElementById('fee').value) || 0;
            const monthly = parseFloat(document.getElementById('monthly').value) || 0;
            
            // 1. Retirement Calculation (Simplified compound interest for 25 years)
            const years = 25;
            const annualReturn = 0.07; // 7% market average
            const netReturn = annualReturn - (fee / 100);
            
            // Future value of current balance
            const fvBalance = balance * Math.pow(1 + netReturn, years);
            // Future value of monthly deposits
            const fvMonthly = monthly * 12 * ((Math.pow(1 + netReturn, years) - 1) / netReturn);
            const total = fvBalance + fvMonthly;
            
            // Total fees paid (rough estimate)
            const feesPaid = (total * (fee/100)) * (years / 2);

            document.getElementById('retirementTotal').innerText = '₪' + Math.round(total).toLocaleString();
            document.getElementById('totalFeesPaid').innerText = '₪' + Math.round(feesPaid).toLocaleString();
            
            const marketAvgFee = 0.35;
            const feeGap = (fee - marketAvgFee).toFixed(2);
            document.getElementById('feeGapText').innerText = feeGap + "%";

            updateChart(fee, marketAvgFee);
        }

        function updateChart(userFee, marketFee) {
            const ctx = document.getElementById('mainChart').getContext('2d');
            
            if (mainChart) mainChart.destroy();
            
            mainChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['דמי ניהול מהצבירה (%)', 'תשואה שנתית נטו (%)'],
                    datasets: [
                        {
                            label: 'התיק שלך (טל)',
                            data: [userFee, 7 - userFee],
                            backgroundColor: '#6366f1',
                            borderRadius: 8
                        },
                        {
                            label: 'ממוצע שוק',
                            data: [marketFee, 7 - marketFee],
                            backgroundColor: '#e2e8f0',
                            borderRadius: 8
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: { y: { beginAtZero: true } }
                }
            });
        }

        function generateLetter() {
            const fee = document.getElementById('fee').value;
            const balance = document.getElementById('balance').value;
            const content = `שלום,\n\nבבדיקה שערכתי בתיק קופת הגמל שלי, ראיתי שדמי הניהול הנוכחיים עומדים על ${fee}%. \nלפי נתוני השוק העדכניים לשנת 2026, הממוצע למסלול שלי עומד על כ-0.35%.\n\nלאור הצבירה שלי שעומדת על כ-₪${parseInt(balance).toLocaleString()}, אבקש לעדכן את דמי הניהול שלי בהתאם לממוצע בשוק, או לחילופין לבחון מעבר לחברה מתחרה שמציעה תנאים אלו.\n\nאשמח לעדכונך,\nטל.`;
            
            document.getElementById('letterContent').innerText = content;
            document.getElementById('letterArea').classList.remove('hidden');
            document.getElementById('letterArea').scrollIntoView({ behavior: 'smooth' });
        }

        function copyLetter() {
            const text = document.getElementById('letterContent').innerText;
            navigator.clipboard.writeText(text);
            alert("המכתב הועתק! עכשיו אפשר להדביק ב-WhatsApp או במייל לסוכן.");
        }

        window.onload = calculateAll;
    </script>
</body>
</html>
