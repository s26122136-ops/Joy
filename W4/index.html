<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>網頁作品集 - 學習闖關地圖</title>
    <!-- Google Fonts: Noto Sans TC & Poppins -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;700;900&family=Poppins:wght@600;700;800&display=swap" rel="stylesheet">
    
    <style>
        /* ==================== 基礎與變數設定 ==================== */
        :root {
            --bg-color: #0d0614;
            --card-bg: rgba(29, 15, 48, 0.7);
            --primary-purple: #9d4edd;
            --accent-glow: #c77dff;
            --neon-pink: #f72585;
            --text-light: #f8f9fa;
            --text-muted: #a092b7;
            --locked-bg: rgba(20, 15, 30, 0.6);
            --locked-border: #2d1e40;
            --locked-text: #605075;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Poppins', 'Noto Sans TC', sans-serif;
            background-color: var(--bg-color);
            color: var(--text-light);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
            padding: 40px 20px;
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(157, 78, 221, 0.15) 0%, transparent 40%),
                radial-gradient(circle at 90% 80%, rgba(247, 37, 133, 0.12) 0%, transparent 40%),
                radial-gradient(circle at 50% 50%, rgba(60, 9, 108, 0.2) 0%, transparent 60%);
            background-attachment: fixed;
            overflow-x: hidden;
        }

        .container {
            width: 100%;
            max-width: 1100px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        /* ==================== 個人資訊區塊 (Header) ==================== */
        .profile-card {
            text-align: center;
            margin-bottom: 40px;
            display: flex;
            flex-direction: column;
            align-items: center;
            animation: fadeInDown 0.8s ease-out;
        }

        .avatar-wrapper {
            position: relative;
            width: 130px;
            height: 130px;
            margin-bottom: 20px;
        }

        .avatar-glow {
            position: absolute;
            top: -5px;
            left: -5px;
            right: -5px;
            bottom: -5px;
            border-radius: 50%;
            background: linear-gradient(45deg, var(--neon-pink), var(--primary-purple), var(--accent-glow));
            background-size: 300% 300%;
            animation: neonGlow 4s ease infinite;
            filter: blur(8px);
            z-index: 1;
        }

        .avatar-img {
            position: relative;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            object-fit: cover;
            border: 3px solid rgba(255, 255, 255, 0.8);
            z-index: 2;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.5);
        }

        .user-name {
            font-size: 2.2rem;
            font-weight: 900;
            background: linear-gradient(135deg, #ffffff 0%, var(--accent-glow) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 8px;
            letter-spacing: 1px;
        }

        .user-title {
            font-size: 1rem;
            color: var(--text-muted);
            letter-spacing: 2px;
            text-transform: uppercase;
            font-weight: 500;
            background: rgba(157, 78, 221, 0.15);
            padding: 6px 18px;
            border-radius: 20px;
            border: 1px solid rgba(157, 78, 221, 0.3);
        }

        /* ==================== 作品集網格 (Grid) ==================== */
        .grid-title {
            align-self: flex-start;
            font-size: 1.2rem;
            color: var(--accent-glow);
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
            font-weight: 700;
        }

        .grid-title::before {
            content: '';
            display: inline-block;
            width: 8px;
            height: 20px;
            background: var(--neon-pink);
            border-radius: 4px;
        }

        .portfolio-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 20px;
            width: 100%;
        }

        /* ==================== 卡片與按鈕樣式 ==================== */
        .card {
            text-decoration: none;
            border-radius: 16px;
            padding: 22px 18px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            min-height: 130px;
            position: relative;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            backdrop-filter: blur(10px);
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
            overflow: hidden;
        }

        /* 已解鎖卡片 (Unlocked) */
        .card.unlocked {
            background: var(--card-bg);
            border: 1px solid rgba(157, 78, 221, 0.4);
            cursor: pointer;
        }

        .card.unlocked::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.15), transparent);
            transition: 0.6s;
        }

        .card.unlocked:hover::before {
            left: 100%;
        }

        .card.unlocked:hover {
            transform: translateY(-8px) scale(1.02);
            border-color: var(--accent-glow);
            box-shadow: 0 12px 30px rgba(157, 78, 221, 0.4), 
                        0 0 15px rgba(199, 125, 255, 0.2);
            background: rgba(45, 20, 75, 0.85);
        }

        .card.unlocked .badge {
            background: linear-gradient(135deg, var(--neon-pink), var(--primary-purple));
            color: #fff;
            box-shadow: 0 2px 8px rgba(247, 37, 133, 0.4);
        }

        .card.unlocked .card-title {
            color: var(--text-light);
        }

        .card.unlocked .action-text {
            color: var(--accent-glow);
            font-weight: 700;
        }

        /* 未解鎖卡片 (Locked) */
        .card.locked {
            background: var(--locked-bg);
            border: 1px solid var(--locked-border);
            cursor: not-allowed;
            opacity: 0.75;
        }

        .card.locked:hover {
            transform: translateY(-2px);
            border-color: rgba(157, 78, 221, 0.2);
        }

        .card.locked .badge {
            background: rgba(255, 255, 255, 0.05);
            color: var(--locked-text);
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        .card.locked .card-title {
            color: var(--locked-text);
        }

        .card.locked .action-text {
            color: var(--locked-text);
            font-size: 0.8rem;
        }

        /* 卡片內部元素 */
        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
        }

        .badge {
            font-size: 0.75rem;
            font-weight: 700;
            padding: 4px 10px;
            border-radius: 12px;
            letter-spacing: 0.5px;
        }

        .icon {
            font-size: 1.2rem;
        }

        .card-title {
            font-size: 1.05rem;
            font-weight: 700;
            line-height: 1.4;
            margin-bottom: 12px;
        }

        .card-footer {
            display: flex;
            align-items: center;
            justify-content: space-between;
            font-size: 0.85rem;
        }

        .action-text {
            display: flex;
            align-items: center;
            gap: 4px;
            transition: gap 0.2s ease;
        }

        .card.unlocked:hover .action-text {
            gap: 8px;
        }

        /* 點擊鎖定卡片的搖晃動畫 */
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            20%, 60% { transform: translateX(-6px); }
            40%, 80% { transform: translateX(6px); }
        }

        .shake-anim {
            animation: shake 0.4s ease-in-out;
        }

        /* ==================== 頁尾 (Footer) ==================== */
        footer {
            margin-top: 50px;
            color: var(--text-muted);
            font-size: 0.85rem;
            text-align: center;
        }

        /* ==================== 動畫效果 ==================== */
        @keyframes neonGlow {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        @keyframes fadeInDown {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* ==================== 響應式設計 (RWD) ==================== */
        @media (max-width: 992px) {
            .portfolio-grid {
                grid-template-columns: repeat(3, 1fr);
            }
        }

        @media (max-width: 768px) {
            .portfolio-grid {
                grid-template-columns: repeat(2, 1fr);
                gap: 15px;
            }
            .user-name {
                font-size: 1.8rem;
            }
            .avatar-wrapper {
                width: 110px;
                height: 110px;
            }
        }

        @media (max-width: 480px) {
            .portfolio-grid {
                grid-template-columns: 1fr;
            }
            body {
                padding: 25px 15px;
            }
            .card {
                padding: 18px 16px;
                min-height: auto;
            }
        }
    </style>
</head>
<body>

    <div class="container">
        <!-- 個人資訊區塊 -->
        <header class="profile-card">
            <div class="avatar-wrapper">
                <div class="avatar-glow"></div>
                <img class="avatar-img" src="https://i.postimg.cc/28jGM5CR/temp-image-30F7BB40-034E-42DC-8F49-14F02BDB66C1.jpg" alt="大頭貼">
            </div>
            <h1 class="user-name"></h1>
            <div class="user-title"></div>
        </header>

        <!-- 關卡選單標題 -->
        <div class="grid-title">闖關地圖 (16 個任務關卡)</div>

        <!-- 16 個按鈕網格區塊 -->
        <main class="portfolio-grid">
            
            <!-- Week 1 (已解鎖) -->
            <a href="w1/index.html" class="card unlocked">
                <div class="card-header">
                    <span class="badge">WEEK 01</span>
                    <span class="icon">🚀</span>
                </div>
                <div class="card-title">Week 1 - 數位名片</div>
                <div class="card-footer">
                    <span class="action-text">前往關卡 ➔</span>
                </div>
            </a>

            <!-- Week 2 (已解鎖) -->
            <a href="w2/index.html" class="card unlocked">
                <div class="card-header">
                    <span class="badge">WEEK 02</span>
                    <span class="icon">🍔</span>
                </div>
                <div class="card-title">Week 2 - 今天吃甚麼?</div>
                <div class="card-footer">
                    <span class="action-text">前往關卡 ➔</span>
                </div>
            </a>

            <!-- Week 3 (已解鎖) -->
            <a href="w3/index.html" class="card unlocked">
                <div class="card-header">
                    <span class="badge">WEEK 03</span>
                    <span class="icon">🎭</span>
                </div>
                <div class="card-title">Week 3 - 迷因產生器</div>
                <div class="card-footer">
                    <span class="action-text">前往關卡 ➔</span>
                </div>
            </a>

            <!-- Week 4 (已解鎖) -->
            <a href="w4/index.html" class="card unlocked">
                <div class="card-header">
                    <span class="badge">WEEK 04</span>
                    <span class="icon">💬</span>
                </div>
                <div class="card-title">Week 4 - 悄悄話</div>
                <div class="card-footer">
                    <span class="action-text">前往關卡 ➔</span>
                </div>
            </a>

            <!-- Week 5 (未解鎖) -->
            <div class="card locked" onclick="playLockedEffect(this)">
                <div class="card-header">
                    <span class="badge">WEEK 05</span>
                    <span class="icon">🔒</span>
                </div>
                <div class="card-title">未解鎖關卡</div>
                <div class="card-footer">
                    <span class="action-text">敬請期待...</span>
                </div>
            </div>

            <!-- Week 6 (未解鎖) -->
            <div class="card locked" onclick="playLockedEffect(this)">
                <div class="card-header">
                    <span class="badge">WEEK 06</span>
                    <span class="icon">🔒</span>
                </div>
                <div class="card-title">未解鎖關卡</div>
                <div class="card-footer">
                    <span class="action-text">敬請期待...</span>
                </div>
            </div>

            <!-- Week 7 (未解鎖) -->
            <div class="card locked" onclick="playLockedEffect(this)">
                <div class="card-header">
                    <span class="badge">WEEK 07</span>
                    <span class="icon">🔒</span>
                </div>
                <div class="card-title">未解鎖關卡</div>
                <div class="card-footer">
                    <span class="action-text">敬請期待...</span>
                </div>
            </div>

            <!-- Week 8 (未解鎖) -->
            <div class="card locked" onclick="playLockedEffect(this)">
                <div class="card-header">
                    <span class="badge">WEEK 08</span>
                    <span class="icon">🔒</span>
                </div>
                <div class="card-title">未解鎖關卡</div>
                <div class="card-footer">
                    <span class="action-text">敬請期待...</span>
                </div>
            </div>

            <!-- Week 9 (未解鎖) -->
            <div class="card locked" onclick="playLockedEffect(this)">
                <div class="card-header">
                    <span class="badge">WEEK 09</span>
                    <span class="icon">🔒</span>
                </div>
                <div class="card-title">未解鎖關卡</div>
                <div class="card-footer">
                    <span class="action-text">敬請期待...</span>
                </div>
            </div>

            <!-- Week 10 (未解鎖) -->
            <div class="card locked" onclick="playLockedEffect(this)">
                <div class="card-header">
                    <span class="badge">WEEK 10</span>
                    <span class="icon">🔒</span>
                </div>
                <div class="card-title">未解鎖關卡</div>
                <div class="card-footer">
                    <span class="action-text">敬請期待...</span>
                </div>
            </div>

            <!-- Week 11 (未解鎖) -->
            <div class="card locked" onclick="playLockedEffect(this)">
                <div class="card-header">
                    <span class="badge">WEEK 11</span>
                    <span class="icon">🔒</span>
                </div>
                <div class="card-title">未解鎖關卡</div>
                <div class="card-footer">
                    <span class="action-text">敬請期待...</span>
                </div>
            </div>

            <!-- Week 12 (未解鎖) -->
            <div class="card locked" onclick="playLockedEffect(this)">
                <div class="card-header">
                    <span class="badge">WEEK 12</span>
                    <span class="icon">🔒</span>
                </div>
                <div class="card-title">未解鎖關卡</div>
                <div class="card-footer">
                    <span class="action-text">敬請期待...</span>
                </div>
            </div>

            <!-- Week 13 (未解鎖) -->
            <div class="card locked" onclick="playLockedEffect(this)">
                <div class="card-header">
                    <span class="badge">WEEK 13</span>
                    <span class="icon">🔒</span>
                </div>
                <div class="card-title">未解鎖關卡</div>
                <div class="card-footer">
                    <span class="action-text">敬請期待...</span>
                </div>
            </div>

            <!-- Week 14 (未解鎖) -->
            <div class="card locked" onclick="playLockedEffect(this)">
                <div class="card-header">
                    <span class="badge">WEEK 14</span>
                    <span class="icon">🔒</span>
                </div>
                <div class="card-title">未解鎖關卡</div>
                <div class="card-footer">
                    <span class="action-text">敬請期待...</span>
                </div>
            </div>

            <!-- Week 15 (未解鎖) -->
            <div class="card locked" onclick="playLockedEffect(this)">
                <div class="card-header">
                    <span class="badge">WEEK 15</span>
                    <span class="icon">🔒</span>
                </div>
                <div class="card-title">未解鎖關卡</div>
                <div class="card-footer">
                    <span class="action-text">敬請期待...</span>
                </div>
            </div>

            <!-- Week 16 (未解鎖) -->
            <div class="card locked" onclick="playLockedEffect(this)">
                <div class="card-header">
                    <span class="badge">WEEK 16</span>
                    <span class="icon">👑</span>
                </div>
                <div class="card-title">期末展示 / 未解鎖</div>
                <div class="card-footer">
                    <span class="action-text">敬請期待...</span>
                </div>
            </div>

        </main>

        <!-- 頁尾 -->
        <footer>
            <p>© 2026 網頁程式設計作品集入口 | All Rights Reserved.</p>
        </footer>
    </div>

    <!-- 點擊未解鎖卡片時的小互動腳本 -->
    <script>
        function playLockedEffect(element) {
            element.classList.remove('shake-anim');
            void element.offsetWidth;
            element.classList.add('shake-anim');
        }
    </script>
</body>
</html>
