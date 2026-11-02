<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>作品集入口 ‧ Portfolio Gateway</title>
    
    <!-- 引入 Google Fonts: Noto Serif TC, Inter, 黑體, 與搞笑風炸裂字體 Black Han Sans -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Black+Han+Sans&family=Inter:wght@300;400;500;600;800&family=Noto+Sans+TC:wght@500;700;900&family=Noto+Serif+TC:wght@300;400;600&display=swap" rel="stylesheet">
    
    <!-- 引入 html2canvas 截圖下載 CDN -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    
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
         * 2. 主要容器與淡入動畫
         * -------------------------------------------------- */
        .container {
            max-width: 1080px;
            width: 100%;
            margin: 0 auto;
            opacity: 0;
            transform: translateY(20px);
            animation: fadeInUp 1.2s cubic-bezier(0.16, 1, 0.3, 1) forwards;
        }

        @keyframes fadeInUp {
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* --------------------------------------------------
         * 3. 個人資訊 Header 區塊
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

        /* 頭像外圍細線飾環 */
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
            grid-template-columns: repeat(4, 1fr); /* 預設 4x4 */
            gap: 1.5rem;
        }

        @media (max-width: 960px) {
            .card-grid {
                grid-template-columns: repeat(3, 1fr);
            }
        }

        @media (max-width: 680px) {
            .card-grid {
                grid-template-columns: repeat(2, 1fr); /* 手機版雙欄 */
                gap: 1rem;
            }
        }

        @media (max-width: 420px) {
            .card-grid {
                grid-template-columns: 1fr; /* 極小螢幕單欄 */
            }
        }

        /* --------------------------------------------------
         * 5. 作品卡片基礎樣式
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

        /* --------------------------------------------------
         * 6. 卡片動態與互動效果 (Unlocked vs Locked)
         * -------------------------------------------------- */
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
            background: linear-gradient(
                90deg,
                transparent,
                rgba(255, 255, 255, 0.6),
                transparent
            );
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
         * 7. 搞笑風格迷因產生器 (Modal 彈窗樣式)
         * -------------------------------------------------- */
        .modal-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.75);
            z-index: 1000;
            overflow-y: auto;
            padding: 1rem;
            align-items: center;
            justify-content: center;
        }

        .modal-overlay.active {
            display: flex;
        }

        .meme-app-wrapper {
            background: #fffae6;
            border: 4px solid #000;
            border-radius: 20px;
            box-shadow: 10px 10px 0px #000;
            width: 100%;
            max-width: 950px;
            max-height: 90vh;
            overflow-y: auto;
            position: relative;
            padding: 2rem;
            color: #000;
            font-family: 'Noto Sans TC', sans-serif;
        }

        .close-btn {
            position: absolute;
            top: 15px;
            right: 15px;
            background: #ff595e;
            color: #fff;
            border: 3px solid #000;
            font-size: 1.2rem;
            font-weight: 900;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            cursor: pointer;
            box-shadow: 3px 3px 0px #000;
            transition: transform 0.1s;
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 10;
        }

        .close-btn:active {
            transform: translate(2px, 2px);
            box-shadow: 1px 1px 0px #000;
        }

        .meme-title {
            text-align: center;
            font-size: 2.2rem;
            font-weight: 900;
            text-transform: uppercase;
            background: #ffca3a;
            display: inline-block;
            padding: 0.3rem 1.2rem;
            border: 3px solid #000;
            box-shadow: 5px 5px 0px #000;
            transform: rotate(-2deg);
            margin-bottom: 1.5rem;
        }

        .meme-header-container {
            text-align: center;
        }

        /* 產生器雙欄配置 */
        .meme-generator-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 2rem;
            align-items: start;
        }

        @media (max-width: 768px) {
            .meme-generator-grid {
                grid-template-columns: 1fr;
            }
        }

        /* 控制區 */
        .controls-panel {
            background: #ffffff;
            border: 3px solid #000;
            border-radius: 12px;
            padding: 1.5rem;
            box-shadow: 5px 5px 0px #000;
        }

        .control-group {
            margin-bottom: 1.2rem;
        }

        .control-group label {
            display: block;
            font-weight: 900;
            margin-bottom: 0.4rem;
            font-size: 1rem;
        }

        .funny-input {
            width: 100%;
            padding: 0.8rem;
            border: 3px solid #000;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 700;
            background: #f0f3f4;
            outline: none;
            transition: 0.2s;
        }

        .funny-input:focus {
            background: #fff;
            box-shadow: 3px 3px 0px #8ac926;
        }

        .funny-range {
            width: 100%;
            accent-color: #ff595e;
            cursor: pointer;
        }

        .file-upload-btn {
            display: inline-block;
            width: 100%;
            text-align: center;
            background: #8ac926;
            color: #000;
            font-weight: 900;
            padding: 0.8rem;
            border: 3px solid #000;
            border-radius: 8px;
            cursor: pointer;
            box-shadow: 4px 4px 0px #000;
            transition: all 0.1s ease;
        }

        .file-upload-btn:hover {
            background: #9ef01a;
        }

        .file-upload-btn:active {
            transform: translate(2px, 2px);
            box-shadow: 2px 2px 0px #000;
        }

        #image-input {
            display: none;
        }

        .download-btn {
            width: 100%;
            background: #ff595e;
            color: #fff;
            font-size: 1.3rem;
            font-weight: 900;
            padding: 1rem;
            border: 3px solid #000;
            border-radius: 12px;
            cursor: pointer;
            box-shadow: 5px 5px 0px #000;
            margin-top: 1rem;
            transition: all 0.1s ease;
        }

        .download-btn:hover {
            background: #ff6b6b;
        }

        .download-btn:active {
            transform: translate(3px, 3px);
            box-shadow: 2px 2px 0px #000;
        }

        /* 預覽區 */
        .preview-panel {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .meme-canvas-box {
            position: relative;
            width: 100%;
            max-width: 420px;
            background: #111;
            border: 4px solid #000;
            border-radius: 10px;
            box-shadow: 8px 8px 0px #000;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 300px;
        }

        .meme-canvas-box img {
            width: 100%;
            height: auto;
            display: block;
            object-fit: contain;
        }

        /* 迷因文字樣式 (粗黑描邊) */
        .meme-text {
            position: absolute;
            width: 90%;
            left: 5%;
            text-align: center;
            color: #ffffff;
            font-family: 'Black Han Sans', 'Noto Sans TC', sans-serif;
            font-weight: 900;
            text-transform: uppercase;
            line-height: 1.2;
            word-wrap: break-word;
            pointer-events: none;
            text-shadow: 
                3px 3px 0 #000, -3px 3px 0 #000, 3px -3px 0 #000, -3px -3px 0 #000,
                0px 3px 0 #000,  0px -3px 0 #000, 3px  0px 0 #000, -3px  0px 0 #000;
        }

        .meme-text-top {
            top: 10px;
        }

        .meme-text-bottom {
            bottom: 10px;
        }

        /* --------------------------------------------------
         * 8. 頁尾 Footer 資訊
         * -------------------------------------------------- */
        .footer {
            margin-top: 4rem;
            text-align: center;
            font-size: 0.8rem;
            color: var(--text-sub);
            letter-spacing: 1px;
        }

        .footer p {
            font-family: 'Inter', sans-serif;
            font-weight: 300;
        }
    </style>
</head>
<body>

    <main class="container">
        
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

            <!-- Week 3 (已解鎖 - 迷因產生器 點擊開啟彈窗) -->
            <div class="card unlocked" id="open-meme-btn">
                <div class="card-header">
                    <span class="week-tag">Week 03</span>
                    <span class="card-arrow">→</span>
                </div>
                <div class="card-title">Week 3 - 迷因產生器</div>
            </div>

            <!-- Week 4 (已解鎖 - 講八卦) -->
            <a href="https://docs.google.com/spreadsheets/d/e/2PACX-1vSzQ9hxlz17-FjU9oXi-Qn-yKLyeRWVxbOGNXeZQhU3YX3LpUmH_ITjQKOLgyALuj-OQgpvoEEKJd7-/pub?output=csv" target="_blank" class="card unlocked">
                <div class="card-header">
                    <span class="week-tag">Week 04</span>
                    <span class="card-arrow">→</span>
                </div>
                <div class="card-title">Week 4 - 講八卦</div>
            </a>

            <!-- Week 5 至 16 (未解鎖) -->
            <div class="card locked"><div class="card-header"><span class="week-tag">Week 05</span><span class="status-badge lock-icon">🔒</span></div><div class="card-title">Week 5 - 尚未解鎖</div></div>
            <div class="card locked"><div class="card-header"><span class="week-tag">Week 06</span><span class="status-badge lock-icon">🔒</span></div><div class="card-title">Week 6 - 尚未解鎖</div></div>
            <div class="card locked"><div class="card-header"><span class="week-tag">Week 07</span><span class="status-badge lock-icon">🔒</span></div><div class="card-title">Week 7 - 尚未解鎖</div></div>
            <div class="card locked"><div class="card-header"><span class="week-tag">Week 08</span><span class="status-badge lock-icon">🔒</span></div><div class="card-title">Week 8 - 尚未解鎖</div></div>
            <div class="card locked"><div class="card-header"><span class="week-tag">Week 09</span><span class="status-badge lock-icon">🔒</span></div><div class="card-title">Week 9 - 尚未解鎖</div></div>
            <div class="card locked"><div class="card-header"><span class="week-tag">Week 10</span><span class="status-badge lock-icon">🔒</span></div><div class="card-title">Week 10 - 尚未解鎖</div></div>
            <div class="card locked"><div class="card-header"><span class="week-tag">Week 11</span><span class="status-badge lock-icon">🔒</span></div><div class="card-title">Week 11 - 尚未解鎖</div></div>
            <div class="card locked"><div class="card-header"><span class="week-tag">Week 12</span><span class="status-badge lock-icon">🔒</span></div><div class="card-title">Week 12 - 尚未解鎖</div></div>
            <div class="card locked"><div class="card-header"><span class="week-tag">Week 13</span><span class="status-badge lock-icon">🔒</span></div><div class="card-title">Week 13 - 尚未解鎖</div></div>
            <div class="card locked"><div class="card-header"><span class="week-tag">Week 14</span><span class="status-badge lock-icon">🔒</span></div><div class="card-title">Week 14 - 尚未解鎖</div></div>
            <div class="card locked"><div class="card-header"><span class="week-tag">Week 15</span><span class="status-badge lock-icon">🔒</span></div><div class="card-title">Week 15 - 尚未解鎖</div></div>
            <div class="card locked"><div class="card-header"><span class="week-tag">Week 16</span><span class="status-badge lock-icon">🔒</span></div><div class="card-title">Week 16 - 尚未解鎖</div></div>

        </section>

        <!-- 頁尾 -->
        <footer class="footer">
            <p>© Web Programming Portfolio Gateway. All Rights Reserved.</p>
        </footer>

    </main>

    <!-- --------------------------------------------------
     * 9. 迷因產生器 Modal 彈窗區塊
     * -------------------------------------------------- -->
    <div class="modal-overlay" id="meme-modal">
        <div class="meme-app-wrapper">
            <button class="close-btn" id="close-modal-btn">✕</button>
            
            <div class="meme-header-container">
                <h2 class="meme-title">🤪 超吉迷因產生器</h2>
            </div>

            <div class="meme-generator-grid">
                <!-- 左側控制面板 -->
                <div class="controls-panel">
                    <div class="control-group">
                        <label>📁 上傳底圖 (本機圖片)</label>
                        <label for="image-input" class="file-upload-btn">選擇檔案...</label>
                        <input type="file" id="image-input" accept="image/*">
                    </div>

                    <div class="control-group">
                        <label for="top-text-input">✍️ 上方文字</label>
                        <input type="text" id="top-text-input" class="funny-input" placeholder="寫點搞笑的..." value="當你終於解鎖 WEEK 3">
                    </div>

                    <div class="control-group">
                        <label for="bottom-text-input">✍️ 下方文字</label>
                        <input type="text" id="bottom-text-input" class="funny-input" placeholder="再寫點更爆笑的..." value="扣子直接爆炸 💥">
                    </div>

                    <div class="control-group">
                        <label for="font-size-range">📏 字體大小</label>
                        <input type="range" id="font-size-range" class="funny-range" min="16" max="64" value="32">
                    </div>

                    <div class="control-group">
                        <label for="top-pos-range">↕️ 上方文字位置</label>
                        <input type="range" id="top-pos-range" class="funny-range" min="5" max="40" value="10">
                    </div>

                    <div class="control-group">
                        <label for="bottom-pos-range">↕️ 下方文字位置</label>
                        <input type="range" id="bottom-pos-range" class="funny-range" min="5" max="40" value="10">
                    </div>

                    <button class="download-btn" id="download-btn">🚀 一鍵下載 my-meme.png</button>
                </div>

                <!-- 右側即時預覽區 -->
                <div class="preview-panel">
                    <div class="meme-canvas-box" id="meme-preview-area">
                        <img id="meme-image" src="https://images.unsplash.com/photo-1537151608828-ea2b11777ee8?q=80&w=600&auto=format&fit=crop" alt="迷因底圖">
                        <div id="meme-top-text" class="meme-text meme-text-top">當你終於解鎖 WEEK 3</div>
                        <div id="meme-bottom-text" class="meme-text meme-text-bottom">扣子直接爆炸 💥</div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- --------------------------------------------------
     * 10. JavaScript 邏輯控制
     * -------------------------------------------------- -->
    <script>
        // 取得 DOM 元素
        const openMemeBtn = document.getElementById('open-meme-btn');
        const closeMemeBtn = document.getElementById('close-modal-btn');
        const memeModal = document.getElementById('meme-modal');

        const imageInput = document.getElementById('image-input');
        const memeImage = document.getElementById('meme-image');

        const topTextInput = document.getElementById('top-text-input');
        const bottomTextInput = document.getElementById('bottom-text-input');
        const memeTopText = document.getElementById('meme-top-text');
        const memeBottomText = document.getElementById('meme-bottom-text');

        const fontSizeRange = document.getElementById('font-size-range');
        const topPosRange = document.getElementById('top-pos-range');
        const bottomPosRange = document.getElementById('bottom-pos-range');

        const downloadBtn = document.getElementById('download-btn');
        const memePreviewArea = document.getElementById('meme-preview-area');

        // 開啟 / 關閉 彈窗
        openMemeBtn.addEventListener('click', () => {
            memeModal.classList.add('active');
        });

        closeMemeBtn.addEventListener('click', () => {
            memeModal.classList.remove('active');
        });

        memeModal.addEventListener('click', (e) => {
            if (e.target === memeModal) {
                memeModal.classList.remove('active');
            }
        });

        // 1. 本機圖片讀取 (使用 FileReader 避開 CORS)
        imageInput.addEventListener('change', (e) => {
            const file = e.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(event) {
                    memeImage.src = event.target.result;
                };
                reader.readAsDataURL(file);
            }
        });

        // 2. 即時文字同步輸入
        topTextInput.addEventListener('input', () => {
            memeTopText.textContent = topTextInput.value;
        });

        bottomTextInput.addEventListener('input', () => {
            memeBottomText.textContent = bottomTextInput.value;
        });

        // 3. 滑桿控制 (字體大小與垂直位置)
        fontSizeRange.addEventListener('input', () => {
            const size = fontSizeRange.value + 'px';
            memeTopText.style.fontSize = size;
            memeBottomText.style.fontSize = size;
        });

        topPosRange.addEventListener('input', () => {
            memeTopText.style.top = topPosRange.value + 'px';
        });

        bottomPosRange.addEventListener('input', () => {
            memeBottomText.style.bottom = bottomPosRange.value + 'px';
        });

        // 4. 一鍵截圖下載 (使用 html2canvas)
        downloadBtn.addEventListener('click', () => {
            downloadBtn.innerText = "⏳ 正在生成截圖...";
            
            html2canvas(memePreviewArea, {
                useCORS: true,
                allowTaint: true,
                scale: 2 // 高畫質渲染
            }).then(canvas => {
                const link = document.createElement('a');
                link.download = 'my-meme.png';
                link.href = canvas.toDataURL('image/png');
                link.click();

                downloadBtn.innerText = "🚀 一鍵下載 my-meme.png";
            }).catch(err => {
                console.error(err);
                alert("下載失敗，請嘗試自行上傳本地圖片後再試一次！");
                downloadBtn.innerText = "🚀 一鍵下載 my-meme.png";
            });
        });
    </script>
</body>
</html>
