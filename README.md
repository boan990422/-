<!DOCTYPE html>
<html lang="zh-TW" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>考前錯題集自動分類演練系統 | 學習歷程作品展示</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#eef2ff',
                            100: '#e0e7ff',
                            500: '#6366f1',
                            600: '#4f46e5',
                            700: '#4338ca',
                        }
                    }
                }
            }
        }
    </script>
    <!-- Chart.js CDN -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- QRCode.js CDN -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <!-- FontAwesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@300;400;500;700;900&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Noto Sans TC', sans-serif; }
        .glass-card {
            background: rgba(255, 255, 255, 0.7);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.3);
        }
        .dark .glass-card {
            background: rgba(30, 41, 59, 0.7);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }
        @media print {
            body * { visibility: hidden; }
            #print-section, #print-section * { visibility: visible; }
            #print-section { position: absolute; left: 0; top: 0; width: 100%; }
        }
    </style>
</head>
<body class="bg-slate-50 dark:bg-slate-950 text-slate-800 dark:text-slate-100 min-h-screen transition-colors duration-300">

    <!-- Top Navigation Bar -->
    <header class="sticky top-0 z-50 glass-card border-b border-slate-200 dark:border-slate-800 px-4 lg:px-12 py-4 flex items-center justify-between">
        <div class="flex items-center space-x-3">
            <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-indigo-600 to-violet-500 flex items-center justify-center text-white shadow-lg shadow-indigo-500/30">
                <i class="fa-solid fa-brain text-lg"></i>
            </div>
            <div>
                <h1 class="font-bold text-lg leading-tight">Smart Error-Notebook</h1>
                <p class="text-xs text-slate-500 dark:text-slate-400">高中自主學習成果展示系統 v1.0</p>
            </div>
        </div>
        
        <div class="flex items-center space-x-3">
            <button onclick="openSystemModal()" class="px-4 py-2 bg-indigo-600 hover:bg-indigo-700 text-white rounded-xl font-medium text-sm shadow-lg shadow-indigo-600/20 transition flex items-center space-x-2">
                <i class="fa-solid fa-play"></i>
                <span>進入系統展示</span>
            </button>
            <button onclick="toggleDarkMode()" class="w-10 h-10 rounded-xl bg-slate-200 dark:bg-slate-800 flex items-center justify-center text-slate-700 dark:text-slate-300 transition hover:bg-slate-300 dark:hover:bg-slate-700">
                <i class="fa-solid fa-moon dark:hidden"></i>
                <i class="fa-solid fa-sun hidden dark:inline"></i>
            </button>
        </div>
    </header>

    <!-- Main Container -->
    <main class="max-w-7xl mx-auto px-4 lg:px-8 py-8 space-y-12">

        <!-- Hero Section with Cover Image & QR Code -->
        <section class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-center">
            <!-- Left Intro -->
            <div class="lg:col-span-7 space-y-6">
                <div class="inline-flex items-center space-x-2 px-3 py-1 rounded-full bg-indigo-500/10 text-indigo-600 dark:text-indigo-400 text-xs font-semibold">
                    <i class="fa-solid fa-graduation-cap"></i>
                    <span>理工科系自主學習精選專案</span>
                </div>
                <h2 class="text-4xl lg:text-5xl font-black tracking-tight leading-tight">
                    考前錯題集自動分類與演練系統
                </h2>
                <p class="text-slate-600 dark:text-slate-300 text-base leading-relaxed">
                    結合 <strong class="text-indigo-600 dark:text-indigo-400">Python、OCR 影像辨識、jieba 關鍵字斷詞與 Streamlit/Web 架構</strong>，解決高中生手寫錯題整理費時、分類混亂的痛點。拍照上傳即可自動歸納章節、錯因分析並一鍵生成專屬複習卷！
                </p>
                <div class="flex flex-wrap gap-4 pt-2">
                    <button onclick="openSystemModal()" class="px-6 py-3.5 bg-gradient-to-r from-indigo-600 to-violet-600 hover:from-indigo-700 hover:to-violet-700 text-white font-semibold rounded-2xl shadow-xl shadow-indigo-600/30 transition transform hover:-translate-y-0.5 flex items-center space-x-3">
                        <i class="fa-solid fa-laptop-code text-lg"></i>
                        <span>立即體驗互動軟體</span>
                    </button>
                </div>
            </div>

            <!-- Right Cover & QR Code Card -->
            <div class="lg:col-span-5">
                <div class="glass-card rounded-3xl p-6 shadow-2xl space-y-6 border border-slate-200/80 dark:border-slate-800">
                    <div class="relative rounded-2xl overflow-hidden shadow-md group">
                        <img src="watermarked_img_7034365759675648951.jpg" alt="系統專案封面" class="w-full h-64 object-cover">
                        <div class="absolute inset-0 bg-gradient-to-t from-slate-950/80 via-transparent to-transparent flex items-end p-4">
                            <span class="text-white text-xs font-medium px-2.5 py-1 rounded-lg bg-indigo-600/80 backdrop-blur-md">
                                <i class="fa-solid fa-image mr-1"></i> 專案代表封面圖
                            </span>
                        </div>
                    </div>

                    <!-- QR Code Box -->
                    <div class="bg-white dark:bg-slate-900 p-4 rounded-2xl border border-slate-200 dark:border-slate-800 flex items-center space-x-4">
                        <div id="qrcode-container" class="bg-white p-2 rounded-xl shadow-inner flex items-center justify-center shrink-0"></div>
                        <div class="space-y-1 overflow-hidden">
                            <h4 class="font-bold text-sm">掃描體驗與檔案下載</h4>
                            <p class="text-xs text-slate-500 dark:text-slate-400 truncate">使用手機掃描 QR Code 隨時查閱本專案成果</p>
                            <button onclick="downloadQRCode()" class="text-xs text-indigo-600 dark:text-indigo-400 font-semibold hover:underline flex items-center space-x-1 pt-1">
                                <i class="fa-solid fa-download"></i>
                                <span>下載 QR Code 圖片</span>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <!-- FULL INTERACTIVE SYSTEM MODAL -->
    <div id="system-modal" class="fixed inset-0 z-50 bg-slate-950/80 backdrop-blur-md hidden flex items-center justify-center p-2 lg:p-6 overflow-y-auto">
        <div class="bg-slate-900 border border-slate-800 w-full max-w-6xl rounded-3xl shadow-2xl overflow-hidden flex flex-col max-h-[92vh]">
            
            <!-- Modal Header -->
            <div class="px-6 py-4 bg-slate-950 border-b border-slate-800 flex items-center justify-between shrink-0">
                <div class="flex items-center space-x-3">
                    <div class="w-3 h-3 rounded-full bg-red-500"></div>
                    <div class="w-3 h-3 rounded-full bg-amber-500"></div>
                    <div class="w-3 h-3 rounded-full bg-emerald-500"></div>
                    <span class="text-sm font-bold text-slate-300 ml-2">考前錯題集自動分類演練系統 - 互動展示環境</span>
                </div>
                <button onclick="closeSystemModal()" class="text-slate-400 hover:text-white text-lg w-8 h-8 rounded-full flex items-center justify-center hover:bg-slate-800 transition">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <!-- Modal Nav Tabs -->
            <div class="flex border-b border-slate-800 bg-slate-900 px-6 shrink-0 overflow-x-auto">
                <button onclick="switchTab('tab-ocr')" id="btn-tab-ocr" class="py-3 px-4 font-semibold text-sm border-b-2 border-indigo-500 text-indigo-400 flex items-center space-x-2 whitespace-nowrap">
                    <i class="fa-solid fa-cloud-arrow-up"></i>
                    <span>1. 拍照上傳與 AI 辨識</span>
                </button>
                <button onclick="switchTab('tab-bank')" id="btn-tab-bank" class="py-3 px-4 font-semibold text-sm border-b-2 border-transparent text-slate-400 hover:text-slate-200 flex items-center space-x-2 whitespace-nowrap">
                    <i class="fa-solid fa-database"></i>
                    <span>2. 錯題庫與標籤管理</span>
                </button>
                <button onclick="switchTab('tab-generator')" id="btn-tab-generator" class="py-3 px-4 font-semibold text-sm border-b-2 border-transparent text-slate-400 hover:text-slate-200 flex items-center space-x-2 whitespace-nowrap">
                    <i class="fa-solid fa-file-lines"></i>
                    <span>3. 動態演練試卷產生</span>
                </button>
                <button onclick="switchTab('tab-analytics')" id="btn-tab-analytics" class="py-3 px-4 font-semibold text-sm border-b-2 border-transparent text-slate-400 hover:text-slate-200 flex items-center space-x-2 whitespace-nowrap">
                    <i class="fa-solid fa-chart-simple"></i>
                    <span>4. 數據分析看板</span>
                </button>
            </div>

            <!-- Modal Body Content -->
            <div class="p-6 overflow-y-auto space-y-6 flex-1 bg-slate-900/50">

                <!-- TAB 1: OCR Upload -->
                <div id="tab-ocr" class="space-y-6">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <!-- Left Upload Box -->
                        <div class="bg-slate-950 border border-slate-800 rounded-2xl p-6 space-y-4">
                            <h4 class="font-bold text-base flex items-center space-x-2">
                                <i class="fa-solid fa-image text-indigo-400"></i>
                                <span>上傳或選擇錯題照片</span>
                            </h4>
                            
                            <!--真實檔案上傳 input-->
                            <input type="file" id="real-file-input" accept="image/*" class="hidden" onchange="handleRealImageUpload(event)">
                            
                            <div class="border-2 border-dashed border-slate-700 rounded-2xl p-6 text-center space-y-3 hover:border-indigo-500 transition cursor-pointer" onclick="document.getElementById('real-file-input').click()">
                                <i class="fa-solid fa-cloud-arrow-up text-3xl text-indigo-400"></i>
                                <div>
                                    <p class="font-medium text-sm">點此上傳你手機或電腦裡的圖片</p>
                                    <p class="text-xs text-slate-500">支援 JPG, PNG 格式</p>
                                </div>
                            </div>

                            <!-- 預覽上傳的圖片顯示區 -->
                            <div id="uploaded-preview-container" class="hidden space-y-2">
                                <p class="text-xs text-slate-400">已上傳的圖片預覽：</p>
                                <img id="uploaded-img-tag" src="" alt="上傳預覽" class="w-full h-32 object-cover rounded-xl border border-slate-800">
                            </div>

                            <!-- Preset options -->
                            <div class="space-y-2 pt-2">
                                <p class="text-xs text-slate-400 font-medium">或快速載入內建範例題目：</p>
                                <div class="grid grid-cols-3 gap-2">
                                    <button onclick="loadPreset(0)" class="px-3 py-2 bg-slate-800 hover:bg-slate-700 rounded-xl text-xs font-medium text-left truncate">
                                        📐 三角函數證明
                                    </button>
                                    <button onclick="loadPreset(1)" class="px-3 py-2 bg-slate-800 hover:bg-slate-700 rounded-xl text-xs font-medium text-left truncate">
                                        ⚡ 物理力學與施力
                                    </button>
                                    <button onclick="loadPreset(2)" class="px-3 py-2 bg-slate-800 hover:bg-slate-700 rounded-xl text-xs font-medium text-left truncate">
                                        📈 多項式與根式
                                    </button>
                                </div>
                            </div>
                        </div>

                        <!-- Right OCR Result Box -->
                        <div class="bg-slate-950 border border-slate-800 rounded-2xl p-6 space-y-4 flex flex-col justify-between">
                            <div class="space-y-4">
                                <h4 class="font-bold text-base flex items-center space-x-2">
                                    <i class="fa-solid fa-wand-magic-sparkles text-violet-400"></i>
                                    <span>OCR 辨識與自動分類結果</span>
                                </h4>
                                <div id="ocr-result-box" class="bg-slate-900 border border-slate-800 rounded-xl p-4 text-sm font-mono text-slate-300 min-h-[120px] flex items-center justify-center text-center text-slate-500">
                                    請上傳照片或點擊內建範例以啟動 OCR 分析...
                                </div>
                                <div id="ocr-tags-box" class="flex flex-wrap gap-2"></div>
                            </div>
                            <button id="save-to-bank-btn" onclick="saveCurrentQuestion()" disabled class="w-full py-3 bg-indigo-600/50 text-slate-400 font-semibold rounded-xl text-sm transition cursor-not-allowed">
                                <i class="fa-solid fa-plus mr-1"></i> 儲存至個人錯題庫
                            </button>
                        </div>
                    </div>
                </div>

                <!-- TAB 2: Question Bank -->
                <div id="tab-bank" class="space-y-4 hidden">
                    <div class="flex flex-wrap items-center justify-between gap-4">
                        <div class="flex items-center space-x-3">
                            <h4 class="font-bold text-base">個人錯題資料庫</h4>
                            <span id="bank-count" class="px-2.5 py-0.5 rounded-full bg-indigo-500/20 text-indigo-400 text-xs font-bold">共 3 題</span>
                        </div>
                    </div>

                    <div class="bg-slate-950 border border-slate-800 rounded-2xl overflow-hidden">
                        <table class="w-full text-left border-collapse text-xs">
                            <thead>
                                <tr class="bg-slate-900/80 border-b border-slate-800 text-slate-400">
                                    <th class="p-3">#ID</th>
                                    <th class="p-3">科目與題目摘要</th>
                                    <th class="p-3">章節標籤</th>
                                    <th class="p-3">錯因標籤</th>
                                    <th class="p-3 text-center">複習次數</th>
                                    <th class="p-3 text-right">操作</th>
                                </tr>
                            </thead>
                            <tbody id="bank-table-body" class="divide-y divide-slate-800">
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- TAB 3: Generator -->
                <div id="tab-generator" class="space-y-6 hidden">
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                        <div class="bg-slate-950 border border-slate-800 rounded-2xl p-6 space-y-4">
                            <h4 class="font-bold text-sm text-indigo-400">試卷產生設定</h4>
                            <div class="space-y-3 text-xs">
                                <div>
                                    <label class="block text-slate-400 mb-1">試卷標題：</label>
                                    <input type="text" id="exam-title-input" value="期末複習：錯題精選演練卷" class="w-full bg-slate-900 border border-slate-800 rounded-xl p-2 text-slate-200">
                                </div>
                                <button onclick="generateExamPreview()" class="w-full py-2.5 bg-indigo-600 hover:bg-indigo-700 text-white font-semibold rounded-xl transition">
                                    重新整理試卷排版
                                </button>
                                <button onclick="window.print()" class="w-full py-2.5 bg-emerald-600 hover:bg-emerald-700 text-white font-semibold rounded-xl transition">
                                    列印 / 儲存 PDF 試卷
                                </button>
                            </div>
                        </div>

                        <div class="md:col-span-2 bg-white text-slate-900 p-8 rounded-2xl shadow-xl space-y-6 font-serif" id="print-section">
                            <div class="text-center border-b-2 border-slate-900 pb-4 space-y-1">
                                <h2 id="preview-exam-title" class="text-xl font-bold">期末複習：錯題精選演練卷</h2>
                                <p class="text-xs text-slate-600">班級：_______ 座號：_______ 姓名：___________ 得分：_______</p>
                            </div>
                            <div id="exam-questions-list" class="space-y-6 text-sm">
                            </div>
                        </div>
                    </div>
                </div>

                <!-- TAB 4: Analytics -->
                <div id="tab-analytics" class="space-y-6 hidden">
                    <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                        <div class="bg-slate-950 border border-slate-800 rounded-2xl p-6 space-y-4">
                            <h4 class="font-bold text-sm text-indigo-400">各單元錯題分佈比例</h4>
                            <div class="h-64 flex items-center justify-center">
                                <canvas id="chartTopic"></canvas>
                            </div>
                        </div>
                        <div class="bg-slate-950 border border-slate-800 rounded-2xl p-6 space-y-4">
                            <h4 class="font-bold text-sm text-violet-400">手動整理 vs 系統自動化省時對比 (分鐘)</h4>
                            <div class="h-64 flex items-center justify-center">
                                <canvas id="chartTime"></canvas>
                            </div>
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </div>

    <!-- JavaScript Application Logic -->
    <script>
        const currentUrl = window.location.href;
        new QRCode(document.getElementById("qrcode-container"), {
            text: currentUrl,
            width: 100,
            height: 100,
            colorDark: "#0f172a",
            colorLight: "#ffffff",
            correctLevel: QRCode.CorrectLevel.H
        });

        function downloadQRCode() {
            const img = document.querySelector('#qrcode-container img');
            if (img) {
                const link = document.createElement('a');
                link.download = 'smart-error-notebook-qr.png';
                link.href = img.src;
                link.click();
            }
        }

        function toggleDarkMode() {
            document.documentElement.classList.toggle('dark');
        }

        function openSystemModal() {
            document.getElementById('system-modal').classList.remove('hidden');
            initCharts();
            renderBankTable();
            generateExamPreview();
        }

        function closeSystemModal() {
            document.getElementById('system-modal').classList.add('hidden');
        }

        function switchTab(tabId) {
            ['tab-ocr', 'tab-bank', 'tab-generator', 'tab-analytics'].forEach(id => {
                document.getElementById(id).classList.add('hidden');
            });
            ['btn-tab-ocr', 'btn-tab-bank', 'btn-tab-generator', 'btn-tab-analytics'].forEach(id => {
                const btn = document.getElementById(id);
                btn.classList.remove('border-indigo-500', 'text-indigo-400');
                btn.classList.add('border-transparent', 'text-slate-400');
            });

            document.getElementById(tabId).classList.remove('hidden');
            const activeBtn = document.getElementById('btn-' + tabId);
            activeBtn.classList.remove('border-transparent', 'text-slate-400');
            activeBtn.classList.add('border-indigo-500', 'text-indigo-400');

            if(tabId === 'tab-analytics') {
                updateCharts();
            }
        }

        let questionBank = [
            { id: 1, subject: '高中數學', text: '設 sin(θ) + cos(θ) = 1/5，求 sin³(θ) + cos³(θ) 之值。', tagChapter: '三角函數', tagError: '觀念混淆', count: 3 },
            { id: 2, subject: '物理力學', text: '質量 m 之物體置於傾角 θ 之光滑斜面上，求其下滑加速度。', tagChapter: '牛頓運動定律', tagError: '計算粗心', count: 2 },
            { id: 3, subject: '多項式', text: '已知多項式 f(x) 除以 x²-3x+2 餘 2x+1，求除以 x-1 之餘式。', tagChapter: '多項式函數', tagError: '審題不清', count: 1 }
        ];

        let currentScannedData = null;

        const presets = [
            {
                text: "設 sin(θ) + cos(θ) = 1/5，求 sin³(θ) + cos³(θ) 之值。",
                chapters: ["三角函數", "代數恆等式"],
                errors: ["觀念混淆", "公式代錯"]
            },
            {
                text: "質量 m 之物體置於傾角 θ 之光滑斜面上，求其下滑加速度與正向力。",
                chapters: ["牛頓運動定律", "力學分析"],
                errors: ["計算粗心", "力圖畫錯"]
            },
            {
                text: "已知多項式 f(x) 除以 x²-3x+2 餘 2x+1，求除以 x-1 之餘式。",
                chapters: ["多項式函數", "餘式定理"],
                errors: ["審題不清", "代數化簡失誤"]
            }
        ];

        // 真實檔案上傳處理函式
        function handleRealImageUpload(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    // 顯示圖片預覽
                    document.getElementById('uploaded-preview-container').classList.remove('hidden');
                    document.getElementById('uploaded-img-tag').src = e.target.result;
                    
                    // 模擬 OCR 解析剛上傳的檔案
                    document.getElementById('ocr-result-box').innerHTML = `<p class="text-emerald-400 font-semibold">[OCR 成功載入自訂圖片]</p><p class="mt-2 text-slate-200">已成功讀取檔案：${file.name}</p><p class="text-xs text-slate-400 mt-1">AI 辨識文字：[自定義上傳題目內容辨識中...]</p>`;
                    
                    let tagsHtml = `<span class="px-2.5 py-1 rounded-lg bg-indigo-500/20 text-indigo-300 text-xs font-semibold">章節: 綜合演練</span><span class="px-2.5 py-1 rounded-lg bg-rose-500/20 text-rose-300 text-xs font-semibold">錯因: 自訂錯題</span>`;
                    document.getElementById('ocr-tags-box').innerHTML = tagsHtml;

                    currentScannedData = {
                        text: `[自定義圖片] 檔案名稱：${file.name}`,
                        chapters: ["綜合演練"],
                        errors: ["自訂錯題"]
                    };

                    const btn = document.getElementById('save-to-bank-btn');
                    btn.disabled = false;
                    btn.classList.remove('bg-indigo-600/50', 'text-slate-400', 'cursor-not-allowed');
                    btn.classList.add('bg-indigo-600', 'hover:bg-indigo-700', 'text-white');
                }
                reader.readAsDataURL(file);
            }
        }

        function loadPreset(index) {
            const p = presets[index];
            currentScannedData = p;
            
            document.getElementById('uploaded-preview-container').classList.add('hidden');
            document.getElementById('ocr-result-box').innerHTML = `<p class="text-indigo-300 font-semibold">[OCR 辨識成功 98.4%]</p><p class="mt-2 text-slate-200">${p.text}</p>`;
            
            let tagsHtml = '';
            p.chapters.forEach(c => tagsHtml += `<span class="px-2.5 py-1 rounded-lg bg-indigo-500/20 text-indigo-300 text-xs font-semibold">章節: ${c}</span>`);
            p.errors.forEach(e => tagsHtml += `<span class="px-2.5 py-1 rounded-lg bg-rose-500/20 text-rose-300 text-xs font-semibold">錯因: ${e}</span>`);
            
            document.getElementById('ocr-tags-box').innerHTML = tagsHtml;
            
            const btn = document.getElementById('save-to-bank-btn');
            btn.disabled = false;
            btn.classList.remove('bg-indigo-600/50', 'text-slate-400', 'cursor-not-allowed');
            btn.classList.add('bg-indigo-600', 'hover:bg-indigo-700', 'text-white');
        }

        function saveCurrentQuestion() {
            if(!currentScannedData) return;
            questionBank.push({
                id: questionBank.length + 1,
                subject: '高中數學',
                text: currentScannedData.text,
                tagChapter: currentScannedData.chapters[0],
                tagError: currentScannedData.errors[0],
                count: 1
            });
            alert('成功存入錯題庫！');
            renderBankTable();
            switchTab('tab-bank');
        }

        function renderBankTable() {
            const tbody = document.getElementById('bank-table-body');
            document.getElementById('bank-count').innerText = `共 ${questionBank.length} 題`;
            let html = '';
            questionBank.forEach(q => {
                html += `
                    <tr class="hover:bg-slate-900 transition">
                        <td class="p-3 font-bold text-indigo-400">#${q.id}</td>
                        <td class="p-3 max-w-xs truncate text-slate-300">${q.text}</td>
                        <td class="p-3"><span class="px-2 py-0.5 rounded bg-indigo-500/10 text-indigo-400 text-[10px]">${q.tagChapter}</span></td>
                        <td class="p-3"><span class="px-2 py-0.5 rounded bg-rose-500/10 text-rose-400 text-[10px]">${q.tagError}</span></td>
                        <td class="p-3 text-center font-bold">${q.count}</td>
                        <td class="p-3 text-right">
                            <button onclick="incrementReview(${q.id})" class="px-2 py-1 bg-slate-800 hover:bg-slate-700 text-slate-300 rounded text-[10px] mr-1">+1 複習</button>
                            <button onclick="deleteQuestion(${q.id})" class="px-2 py-1 bg-rose-500/20 hover:bg-rose-500/30 text-rose-400 rounded text-[10px]">刪除</button>
                        </td>
                    </tr>
                `;
            });
            tbody.innerHTML = html;
        }

        function incrementReview(id) {
            const q = questionBank.find(item => item.id === id);
            if(q) q.count++;
            renderBankTable();
        }

        function deleteQuestion(id) {
            questionBank = questionBank.filter(item => item.id !== id);
            renderBankTable();
        }

        function generateExamPreview() {
            const title = document.getElementById('exam-title-input').value;
            document.getElementById('preview-exam-title').innerText = title;
            
            const listContainer = document.getElementById('exam-questions-list');
            let html = '';
            questionBank.forEach((q, idx) => {
                html += `
                    <div class="space-y-2 border-b border-slate-200 pb-4">
                        <p class="font-bold">第 ${idx+1} 題 [${q.tagChapter}]</p>
                        <p>${q.text}</p>
                        <div class="h-16 border border-dashed border-slate-300 rounded-lg p-2 text-xs text-slate-400">【學生計算與訂正區】</div>
                    </div>
                `;
            });
            listContainer.innerHTML = html;
        }

        let chartTopicInstance = null;
        let chartTimeInstance = null;

        function initCharts() {
            if(chartTopicInstance) chartTopicInstance.destroy();
            if(chartTimeInstance) chartTimeInstance.destroy();

            const ctxTopic = document.getElementById('chartTopic').getContext('2d');
            chartTopicInstance = new Chart(ctxTopic, {
                type: 'doughnut',
                data: {
                    labels: ['三角函數', '牛頓力學', '多項式函數', '向量與幾何'],
                    datasets: [{
                        data: [40, 25, 20, 15],
                        backgroundColor: ['#6366f1', '#8b5cf6', '#ec4899', '#3b82f6']
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { position: 'bottom', labels: { color: '#cbd5e1', font: { size: 10 } } } }
                }
            });

            const ctxTime = document.getElementById('chartTime').getContext('2d');
            chartTimeInstance = new Chart(ctxTime, {
                type: 'bar',
                data: {
                    labels: ['收集題目', '分類建檔', '製作試卷', '總耗時 (分鐘)'],
                    datasets: [
                        { label: '傳統人工方式', data: [30, 45, 60, 135], backgroundColor: '#64748b' },
                        { label: '本系統自動化', data: [5, 2, 3, 10], backgroundColor: '#6366f1' }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        x: { ticks: { color: '#cbd5e1', font: { size: 10 } } },
                        y: { ticks: { color: '#cbd5e1', font: { size: 10 } } }
                    },
                    plugins: { legend: { position: 'bottom', labels: { color: '#cbd5e1', font: { size: 10 } } } }
                }
            });
        }

        function updateCharts() {
            if(chartTopicInstance) chartTopicInstance.update();
            if(chartTimeInstance) chartTimeInstance.update();
        }
    </script>
</body>
</html>
