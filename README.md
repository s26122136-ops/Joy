<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>作品集入口 ‧ Portfolio Gateway</title>
    
    <!-- 引入 Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&family=Noto+Serif+TC:wght@300;400;600&display=swap" rel="stylesheet">
    
    <style>
        /* --------------------------------------------------
         * 1. 全局樣式與變數定義 (莫蘭迪文青色調)
         * -------------------------------------------------- */
        :root {
            --bg-color: #f7f5f0;           /* 柔和米白紙張背景 */
            --card-bg: #ffffff;           /* 卡片純白背景 */
            --text-main: #3d405b;          /* 深莫蘭迪藍灰 (主文字) */
            --text-sub: #8d99ae;           /* 靜謐灰藍 (次要文字) */
            --accent-color: #e07a5f;      /* 溫暖暖橙 (點綴色) */
            --accent-hover: #d1684e;      /* 懸停點綴色 */
            --locked-bg: #eceae4;        /* 鎖定狀態卡片背景 */
            --locked-text: #a0a5aa;      /* 鎖定狀態文字 */
            --border-color: #e2dfd7;      /* 柔和邊框 */
            --shadow-soft: 0 10px 30px rgba(61, 64, 91, 0.05);
            --shadow-hover: 0 15px 35px rgba(61, 64, 91, 0.12);

            /* 悄悄話留言板專用高亮顏色 (【顏色設定】) */
            --highlight-glow: rgba(224, 122, 95, 0.4); 
            --highlight-border: #e07a5f;
            --highlight-bg: #fffbf7;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Noto Serif TC', 'Inter', serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
            padding: 3rem 1.5rem;
            position: relative;
            overflow-x: hidden;
        }

        /* 背景微細紙質紋理與優雅幾何裝飾 */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: radial-gradient(var(--border-color) 1px, transparent 0);
            background-size: 28px 28px;
            opacity: 0.4;
            z-index: -1;
            pointer-events: none;
        }

        /* --------------------------------------------------
         * 2. 主要頁面容器與切換動畫
         * -------------------------------------------------- */
        .page-container {
            max-width: 1080px;
            width: 100%;
            margin: 0 auto;
            opacity: 0;
            transform: translateY(20px);
            animation: fadeInUp 0.8s cubic-bezier(0.16, 1, 0.3, 1) forwards;
        }

        /* 隱藏未活化的頁面 */
        .page-container.hidden {
            display: none;
        }

        @keyframes fadeInUp {
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* --------------------------------------------------
         * 3. 個人資訊 Header 區塊 (入口頁)
         * -------------------------------------------------- */
        .profile-section {
            text-align: center;
            margin-bottom: 3.5rem;
        }

        .avatar-wrapper {
            position: relative;
            display: inline-block;
            margin-bottom: 1.2rem;
        }

        .avatar {
            width: 110px;
            height: 110px;
            border-radius: 50%;
            object-fit: cover;
            border: 3px solid var(--card-bg);
            box-shadow: var(--shadow-soft);
            transition: transform 0.5s ease, box-shadow 0.5s ease;
        }

        .avatar-wrapper:hover .avatar {
            transform: scale(1.05) rotate(2deg);
            box-shadow: var(--shadow-hover);
        }

        .avatar-wrapper::after {
            content: '';
            position: absolute;
            inset: -6px;
            border-radius: 50%;
            border: 1px dashed var(--accent-color);
            opacity: 0.6;
            animation: spin 25s linear infinite;
        }

        @keyframes spin {
            100% { transform: rotate(360deg); }
        }

        .profile-name {
            font-size: 1.8rem;
            font-weight: 600;
            letter-spacing: 2px;
            color: var(--text-main);
            margin-bottom: 0.5rem;
        }

        .profile-bio {
            font-size: 0.95rem;
            color: var(--text-sub);
            font-weight: 300;
            letter-spacing: 1px;
            max-width: 480px;
            margin: 0 auto;
            line-height: 1.6;
        }

        .divider {
            width: 40px;
            height: 2px;
            background-color: var(--accent-color);
            margin: 1.2rem auto 0;
            border-radius: 2px;
            opacity: 0.7;
        }

        /* --------------------------------------------------
         * 4. 作品卡片網格系統 (RWD)
         * -------------------------------------------------- */
        .card-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 1.5rem;
        }

        @media (max-width: 960px) {
            .card-grid { grid-template-columns: repeat(3, 1fr); }
        }

        @media (max-width: 680px) {
            .card-grid { grid-template-columns: repeat(2, 1fr); gap: 1rem; }
        }

        @media (max-width: 420px) {
            .card-grid { grid-template-columns: 1fr; }
        }

        /* --------------------------------------------------
         * 5. 作品卡片基礎樣式與互動效果
         * -------------------------------------------------- */
        .card {
            position: relative;
            background-color: var(--card-bg);
            border-radius: 16px;
            padding: 1.5rem 1.2rem;
            text-decoration: none;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            min-height: 130px;
            border: 1px solid var(--border-color);
            box-shadow: var(--shadow-soft);
            transition: all 0.4s cubic-bezier(0.25, 0.8, 0.25, 1);
            overflow: hidden;
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 0.8rem;
        }

        .week-tag {
            font-family: 'Inter', sans-serif;
            font-size: 0.75rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1.5px;
            color: var(--text-sub);
        }

        .card-title {
            font-size: 1.05rem;
            font-weight: 600;
            color: var(--text-main);
            line-height: 1.4;
        }

        .status-badge {
            font-size: 0.8rem;
            display: inline-flex;
            align-items: center;
            justify-content: center;
        }

        /* 已解鎖卡片 樣式 & Hover */
        .card.unlocked {
            border-left: 4px solid var(--accent-color);
            cursor: pointer;
        }

        .card.unlocked .week-tag {
            color: var(--accent-color);
        }

        .card.unlocked::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.6), transparent);
            transition: 0.6s;
        }

        .card.unlocked:hover {
            transform: translateY(-6px);
            box-shadow: var(--shadow-hover);
            border-color: var(--accent-color);
        }

        .card.unlocked:hover::before {
            left: 100%;
        }

        .card.unlocked .card-arrow {
            font-size: 0.9rem;
            color: var(--accent-color);
            transition: transform 0.3s ease;
        }

        .card.unlocked:hover .card-arrow {
            transform: translateX(4px);
        }

        /* 未解鎖卡片 樣式 & Hover */
        .card.locked {
            background-color: var(--locked-bg);
            border-color: var(--border-color);
            cursor: not-allowed;
            opacity: 0.75;
        }

        .card.locked .card-title {
            color: var(--locked-text);
            font-weight: 400;
        }

        .card.locked .week-tag {
            color: var(--locked-text);
            opacity: 0.7;
        }

        .card.locked:hover {
            transform: translateY(-2px);
            opacity: 0.9;
        }

        .card.locked:hover .lock-icon {
            animation: lockShake 0.4s ease-in-out infinite alternate;
        }

        @keyframes lockShake {
            0% { transform: rotate(-10deg); }
            100% { transform: rotate(10deg); }
        }

        .card.locked::after {
            content: '任務未解鎖';
            position: absolute;
            bottom: 10px;
            right: 12px;
            font-size: 0.7rem;
            color: #888;
            opacity: 0;
            transform: translateY(4px);
            transition: all 0.3s ease;
            font-family: 'Inter', sans-serif;
            letter-spacing: 0.5px;
        }

        .card.locked:hover::after {
            opacity: 0.8;
            transform: translateY(0);
        }

        /* --------------------------------------------------
         * 6. Week 4 悄悄話動態留言牆專屬樣式
         * -------------------------------------------------- */
        .board-header {
            text-align: center;
            margin-bottom: 2.5rem;
            position: relative;
        }

        .back-btn {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            background: var(--card-bg);
            color: var(--accent-color);
            border: 1px solid var(--border-color);
            padding: 0.5rem 1.2rem;
            border-radius: 20px;
            cursor: pointer;
            font-size: 0.9rem;
            font-family: 'Noto Serif TC', serif;
            transition: all 0.3s ease;
            box-shadow: var(--shadow-soft);
            margin-bottom: 1.5rem;
        }

        .back-btn:hover {
            background: var(--accent-color);
            color: #ffffff;
            transform: translateX(-3px);
        }

        .board-title {
            font-size: 2rem;
            font-weight: 600;
            color: var(--text-main);
            letter-spacing: 2px;
            margin-bottom: 0.5rem;
        }

        .board-subtitle {
            font-size: 0.95rem;
            color: var(--text-sub);
            letter-spacing: 1px;
        }

        /* 讀取中酷炫動畫 */
        #loading {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            margin: 4rem 0;
            gap: 1rem;
        }

        .whisper-spinner {
            width: 45px;
            height: 45px;
            border: 3px solid var(--border-color);
            border-radius: 50%;
            border-top-color: var(--accent-color);
            animation: spin 1s infinite linear, pulse 2s infinite ease-in-out;
        }

        #loading p {
            letter-spacing: 2px;
            color: var(--accent-color);
            font-size: 1rem;
            animation: blink 1.5s infinite ease-in-out;
        }

        @keyframes blink {
            0%, 100% { opacity: 0.4; }
            50% { opacity: 1; }
        }

        /* 瀑布流排版 (Masonry Layout) */
        .masonry-container {
            width: 100%;
            column-count: 3;
            column-gap: 1.5rem;
            display: none;
        }

        @media (max-width: 900px) {
            .masonry-container { column-count: 2; }
        }
        @media (max-width: 600px) {
            .masonry-container { column-count: 1; }
        }

        /* 留言卡片樣式 */
        .msg-card {
            background: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 16px;
            padding: 1.5rem;
            margin-bottom: 1.5rem;
            break-inside: avoid;
            transition: all 0.6s cubic-bezier(0.25, 1, 0.5, 1);
            position: relative;
            box-shadow: var(--shadow-soft);
            cursor: pointer;
        }

        .msg-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 0.8rem;
            border-bottom: 1px dashed var(--border-color);
            padding-bottom: 0.5rem;
        }

        .msg-author {
            font-weight: 600;
            color: var(--accent-color);
            font-size: 1rem;
        }

        .msg-time {
            font-size: 0.75rem;
            color: var(--text-sub);
            font-family: 'Inter', sans-serif;
        }

        .msg-content {
            line-height: 1.6;
            font-size: 0.95rem;
            color: var(--text-main);
            white-space: pre-wrap;
            word-break: break-word;
        }

        /* 【重點特效】輪播高亮放大亮起 (Highlight) */
        .msg-card.is-highlighted {
            transform: scale(1.05);
            border-color: var(--highlight-border);
            box-shadow: 0 10px 30px var(--highlight-glow);
            background-color: var(--highlight-bg);
            z-index: 10;
        }

        /* 【重點特效】未選中變暗模糊 (Dimmed) */
        .masonry-container.has-active .msg-card:not(.is-highlighted) {
            opacity: 0.4;
            filter: blur(1px);
            transform: scale(0.98);
        }

        /* --------------------------------------------------
         * 7. 頁尾 Footer 資訊
         * -------------------------------------------------- */
        .footer {
            margin-top: 4rem;
            text-align: center;
            font-size: 0.8rem;
            color: var(--text-sub);
            letter-spacing: 1px;
            width: 100%;
        }

        .footer p {
            font-family: 'Inter', sans-serif;
            font-weight: 300;
        }
    </style>
</head>
<body>

    <!-- =========================================================
         【頁面 A】作品集入口主頁面
         ========================================================= -->
    <main id="portal-page" class="page-container">
        
        <!-- 核心個人資訊 Header -->
        <header class="profile-section">
            <div class="avatar-wrapper">
                <img 
                    src="https://images.unsplash.com/photo-1534528741775-53994a69daeb?q=80&w=400&auto=format&fit=crop" 
                    alt="個人大頭貼" 
                    class="avatar"
                    onerror="this.src='https://placehold.co/150x150/e07a5f/ffffff?text=Me';"
                >
            </div>
            <h1 class="profile-name">作品集入口 ‧ Portfolio</h1>
            <p class="profile-bio">記錄網頁程式設計的探索旅程，一步步解鎖屬於我的數位足跡。</p>
            <div class="divider"></div>
        </header>

        <!-- 16 個關卡按鈕網格區塊 -->
        <section class="card-grid">
            
            <!-- Week 1 (已解鎖) -->
            <a href="w1/index.html" class="card unlocked">
                <div class="card-header">
                    <span class="week-tag">Week 01</span>
                    <span class="card-arrow">→</span>
                </div>
                <div class="card-title">Week 1 - 數位名片</div>
            </a>

            <!-- Week 2 (已解鎖) -->
            <a href="w2/index.html" class="card unlocked">
                <div class="card-header">
                    <span class="week-tag">Week 02</span>
                    <span class="card-arrow">→</span>
                </div>
                <div class="card-title">Week 2 - 今天吃甚麼?</div>
            </a>

            <!-- Week 3 (已解鎖) -->
            <a href="w3/index.html" class="card unlocked">
                <div class="card-header">
                    <span class="week-tag">Week 03</span>
                    <span class="card-arrow">→</span>
                </div>
                <div class="card-title">Week 3 - 迷因產生器?</div>
            </a>

            <!-- Week 4 (解鎖：悄悄話動態留言板) -->
            <div onclick="openWhisperBoard()" class="card unlocked">
                <div class="card-header">
                    <span class="week-tag">Week 04</span>
                    <span class="card-arrow">→</span>
                </div>
                <div class="card-title">Week 4 - 悄悄話</div>
            </div>

            <!-- Week 5 (未解鎖) -->
            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 05</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 5 - 尚未解鎖</div>
            </div>

            <!-- Week 6 (未解鎖) -->
            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 06</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 6 - 尚未解鎖</div>
            </div>

            <!-- Week 7 (未解鎖) -->
            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 07</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 7 - 尚未解鎖</div>
            </div>

            <!-- Week 8 (未解鎖) -->
            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 08</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 8 - 尚未解鎖</div>
            </div>

            <!-- Week 9 (未解鎖) -->
            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 09</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 9 - 尚未解鎖</div>
            </div>

            <!-- Week 10 (未解鎖) -->
            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 10</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 10 - 尚未解鎖</div>
            </div>

            <!-- Week 11 (未解鎖) -->
            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 11</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 11 - 尚未解鎖</div>
            </div>

            <!-- Week 12 (未解鎖) -->
            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 12</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 12 - 尚未解鎖</div>
            </div>

            <!-- Week 13 (未解鎖) -->
            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 13</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 13 - 尚未解鎖</div>
            </div>

            <!-- Week 14 (未解鎖) -->
            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 14</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 14 - 尚未解鎖</div>
            </div>

            <!-- Week 15 (未解鎖) -->
            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 15</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 15 - 尚未解鎖</div>
            </div>

            <!-- Week 16 (未解鎖) -->
            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 16</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 16 - 尚未解鎖</div>
            </div>

        </section>

        <!-- 頁尾 -->
        <footer class="footer">
            <p>© Web Programming Portfolio Gateway. All Rights Reserved.</p>
        </footer>

    </main>

    <!-- =========================================================
         【頁面 B】Week 4 - 悄悄話留言板頁面
         ========================================================= -->
    <main id="whisper-page" class="page-container hidden">
        
        <header class="board-header">
            <button class="back-btn" onclick="openPortal()">← 返回作品集</button>
            <h1 class="board-title">🤫 悄悄話留言牆</h1>
            <p class="board-subtitle">靜靜地聆聽，那些朋友們留給我的秘密與祝福...</p>
            <div class="divider"></div>
        </header>

        <!-- 載入中動畫 -->
        <div id="loading">
            <div class="whisper-spinner"></div>
            <p>讀取留言中...</p>
        </div>

        <!-- 瀑布流卡片牆 -->
        <div id="masonry-wall" class="masonry-container"></div>

        <footer class="footer">
            <p>© Web Programming Portfolio Gateway. All Rights Reserved.</p>
        </footer>

    </main>

    <script>
        /* =========================================================
         * JavaScript 控制邏輯與 Google 試算表 CSV 解析
         * ========================================================= */

        // 【資料網址設定】指定 Google 試算表 CSV 發佈網址
        const CSV_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vSzQ9hxlz17-FjU9oXi-Qn-yKLyeRWVxbOGNXeZQhU3YX3LpUmH_ITjQKOLgyALuj-OQgpvoEEKJd7-/pub?output=csv';

        // 【輪播秒數設定 Zone】控制高亮輪播切換間隔時間 (3000ms = 3 秒)
        const ROTATE_INTERVAL = 3000;

        let cardsData = [];
        let currentIndex = -1;
        let carouselTimer = null;
        let isLoaded = false;

        // 頁面 DOM 元素參考
        const portalPage = document.getElementById('portal-page');
        const whisperPage = document.getElementById('whisper-page');
        const loadingEl = document.getElementById('loading');
        const wallEl = document.getElementById('masonry-wall');

        /**
         * 開啟悄悄話留言板頁面
         */
        function openWhisperBoard() {
            portalPage.classList.add('hidden');
            whisperPage.classList.remove('hidden');
            window.scrollTo(0, 0);

            // 若尚未讀取過資料則發起 Fetch 請求
            if (!isLoaded) {
                loadWhisperData();
            } else if (cardsData.length > 0) {
                startCarousel();
            }
        }

        /**
         * 返回作品集入口主頁
         */
        function openPortal() {
            whisperPage.classList.add('hidden');
            portalPage.classList.remove('hidden');
            window.scrollTo(0, 0);
            
            // 暫停輪播計時器節省資源
            clearInterval(carouselTimer);
        }

        /**
         * 使用 Fetch API 讀取 CSV 資料
         */
        async function loadWhisperData() {
            try {
                const response = await fetch(CSV_URL);
                const csvText = await response.text();

                // 解析 CSV 資料
                cardsData = parseCSV(csvText);
                isLoaded = true;

                // 隱藏載入中，顯示留言牆
                loadingEl.style.display = 'none';
                wallEl.style.display = 'block';

                // 動態生成卡片
                renderCards(cardsData);

                // 啟動 3 秒輪播高亮
                if (cardsData.length > 0) {
                    wallEl.classList.add('has-active');
                    startCarousel();
                }
            } catch (error) {
                console.error('讀取 CSV 資料失敗:', error);
                loadingEl.innerHTML = '<p style="color:#e07a5f;">讀取留言失敗，請確認網路連線或連結是否正確。</p>';
            }
        }

        /**
         * 【CSV 解析器】
         * 正確處理留言內容中含有逗號與雙引號的情形
         */
        function parseCSV(text) {
            const result = [];
            let row = [];
            let entry = '';
            let insideQuotes = false;

            for (let i = 0; i < text.length; i++) {
                const char = text[i];
                const nextChar = text[i + 1];

                if (char === '"') {
                    if (insideQuotes && nextChar === '"') {
                        entry += '"';
                        i++;
                    } else {
                        insideQuotes = !insideQuotes;
                    }
                } else if (char === ',' && !insideQuotes) {
                    row.push(entry.trim());
                    entry = '';
                } else if ((char === '\n' || char === '\r') && !insideQuotes) {
                    if (char === '\r' && nextChar === '\n') {
                        i++;
                    }
                    row.push(entry.trim());
                    if (row.length > 1 || row[0] !== '') {
                        result.push(row);
                    }
                    row = [];
                    entry = '';
                } else {
                    entry += char;
                }
            }

            if (entry || row.length > 0) {
                row.push(entry.trim());
                result.push(row);
            }

            // 過濾跳過第 0 行欄位標題 (時間戳記, 名字, 悄悄話)
            return result.slice(1).map(r => ({
                timestamp: r[0] || '',
                name: r[1] || '無名氏',
                message: r[2] || '這封悄悄話是空的...'
            }));
        }

        /**
         * 動態產生留言卡片
         */
        function renderCards(data) {
            wallEl.innerHTML = '';
            data.forEach((item, index) => {
                const card = document.createElement('div');
                card.className = 'msg-card';
                card.dataset.index = index;

                // 格式化日期
                const timeText = item.timestamp ? item.timestamp.split(' ')[0] : '';

                card.innerHTML = `
                    <div class="msg-header">
                        <span class="msg-author">${escapeHTML(item.name)}</span>
                        <span class="msg-time">${escapeHTML(timeText)}</span>
                    </div>
                    <div class="msg-content">${escapeHTML(item.message)}</div>
                `;

                // 點擊手動高亮並重新計時
                card.addEventListener('click', () => {
                    currentIndex = index;
                    updateHighlight();
                    resetCarousel();
                });

                wallEl.appendChild(card);
            });
        }

        /**
         * 啟動 3 秒輪播高亮特效
         */
        function startCarousel() {
            if (currentIndex === -1) currentIndex = 0;
            updateHighlight();

            clearInterval(carouselTimer);
            carouselTimer = setInterval(() => {
                currentIndex = (currentIndex + 1) % cardsData.length;
                updateHighlight();
            }, ROTATE_INTERVAL);
        }

        /**
         * 更新高亮狀態 (加上明顯邊框、發光與放大)
         */
        function updateHighlight() {
            const cards = wallEl.querySelectorAll('.msg-card');
            cards.forEach((card, idx) => {
                if (idx === currentIndex) {
                    card.classList.add('is-highlighted');
                } else {
                    card.classList.remove('is-highlighted');
                }
            });
        }

        /**
         * 重置輪播計時器
         */
        function resetCarousel() {
            clearInterval(carouselTimer);
            carouselTimer = setInterval(() => {
                currentIndex = (currentIndex + 1) % cardsData.length;
                updateHighlight();
            }, ROTATE_INTERVAL);
        }

        /**
         * XSS 文字轉義防護
         */
        function escapeHTML(str) {
            return str
                .replace(/&/g, '&amp;')
                .replace(/</g, '&lt;')
                .replace(/>/g, '&gt;')
                .replace(/"/g, '&quot;')
                .replace(/'/g, '&#039;');
        }
    </script>
</body>
</html>
