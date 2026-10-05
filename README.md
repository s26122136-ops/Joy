<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>作品集入口 ‧ Portfolio Gateway</title>
    
    <!-- 引入 Google Fonts: Noto Serif TC (襯線文青風) 與 Inter (現代數字與英文) -->
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
            --text-main: #3d405b;         /* 深莫蘭迪藍灰 (主文字) */
            --text-sub: #8d99ae;          /* 靜謐灰藍 (次要文字) */
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
            justify-content: center;
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

        /* RWD 響應式調整 */
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
        
        /* --- [ 已解鎖卡片 樣式 & Hover] --- */
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

        /* 已解鎖懸停效果 */
        .card.unlocked:hover {
            transform: translateY(-6px);
            box-shadow: var(--shadow-hover);
            border-color: var(--accent-color);
        }

        .card.unlocked:hover::before {
            left: 100%; /* 光澤微閃過效果 */
        }

        .card.unlocked .card-arrow {
            font-size: 0.9rem;
            color: var(--accent-color);
            transition: transform 0.3s ease;
        }

        .card.unlocked:hover .card-arrow {
            transform: translateX(4px);
        }

        /* --- [ 未解鎖卡片 樣式 & Hover] --- */
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

        /* 未解鎖懸停：鎖頭搖晃 (Shake) 動畫 */
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

        /* 鎖定提示 Tooltip */
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
         * 7. 頁尾 Footer 資訊
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

            <!-- Week 3 ~ 16 (未解鎖) -->
            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 03</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 3 - 尚未解鎖</div>
            </div>

            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 04</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 4 - 尚未解鎖</div>
            </div>

            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 05</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 5 - 尚未解鎖</div>
            </div>

            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 06</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 6 - 尚未解鎖</div>
            </div>

            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 07</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 7 - 尚未解鎖</div>
            </div>

            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 08</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 8 - 尚未解鎖</div>
            </div>

            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 09</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 9 - 尚未解鎖</div>
            </div>

            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 10</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 10 - 尚未解鎖</div>
            </div>

            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 11</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 11 - 尚未解鎖</div>
            </div>

            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 12</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 12 - 尚未解鎖</div>
            </div>

            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 13</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 13 - 尚未解鎖</div>
            </div>

            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 14</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 14 - 尚未解鎖</div>
            </div>

            <div class="card locked">
                <div class="card-header">
                    <span class="week-tag">Week 15</span>
                    <span class="status-badge lock-icon">🔒</span>
                </div>
                <div class="card-title">Week 15 - 尚未解鎖</div>
            </div>

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

</body>
</html>
