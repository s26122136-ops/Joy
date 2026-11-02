<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>網頁程式設計作品集 | Web Course Portfolio</title>
  <!-- 引入 Google Fonts 襯線字體 -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Noto+Serif+TC:wght@400;600;700&display=swap" rel="stylesheet">
  
  <style>
    /* CSS 全域變數設定（莫蘭迪文青風格配色） */
    :root {
      --bg-color: #f7f5f0;
      --card-unlocked-bg: #ffffff;
      --card-locked-bg: #eae8e1;
      --primary-text: #3c3c3c;
      --secondary-text: #7c7c7c;
      --accent-color: #8c977d; /* 莫蘭迪鼠尾草綠 */
      --accent-hover: #707b62;
      --locked-text: #9e9e9e;
      --shadow-sm: 0 4px 12px rgba(0, 0, 0, 0.04);
      --shadow-lg: 0 12px 24px rgba(0, 0, 0, 0.08);
      --transition: all 0.35s cubic-bezier(0.25, 0.8, 0.25, 1);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Noto Serif TC', serif, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto;
      background-color: var(--bg-color);
      color: var(--primary-text);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      padding: 3rem 1.5rem;
      line-height: 1.6;
    }

    /* 個人大頭貼與標題區塊 */
    .profile-header {
      text-align: center;
      margin-bottom: 2.5rem;
      animation: fadeIn 1s ease-in-out;
    }

    .avatar-wrapper {
      position: relative;
      width: 140px;
      height: 140px;
      margin: 0 auto 1.2rem;
      border-radius: 50%;
      padding: 5px;
      background: linear-gradient(135deg, var(--accent-color), #c2b9a7);
      box-shadow: var(--shadow-sm);
      transition: var(--transition);
    }

    .avatar-wrapper:hover {
      transform: scale(1.05) rotate(2deg);
      box-shadow: var(--shadow-lg);
    }

    .avatar-img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      object-position: top center;
      border-radius: 50%;
      background-color: #e0e0e0;
      display: block;
    }

    .profile-name {
      font-size: 1.8rem;
      font-weight: 700;
      color: var(--primary-text);
      letter-spacing: 2px;
      margin-bottom: 0.3rem;
    }

    .profile-subtitle {
      font-size: 0.95rem;
      color: var(--secondary-text);
      letter-spacing: 1px;
    }

    /* 網格作品集中樞容器 */
    .portfolio-grid {
      width: 100%;
      max-width: 900px;
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 1.25rem;
      margin-top: 1rem;
    }

    /* 作品卡片基本樣式 */
    .card {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 110px;
      border-radius: 14px;
      text-decoration: none;
      position: relative;
      overflow: hidden;
      padding: 1rem;
      transition: var(--transition);
      user-select: none;
    }

    /* 1. 已解鎖狀態 (Week 1 & Week 2) */
    .card.unlocked {
      background-color: var(--card-unlocked-bg);
      color: var(--primary-text);
      box-shadow: var(--shadow-sm);
      border: 1px solid rgba(0, 0, 0, 0.05);
      cursor: pointer;
    }

    .card.unlocked .week-tag {
      font-size: 0.75rem;
      font-weight: 600;
      color: var(--accent-color);
      letter-spacing: 1px;
      margin-bottom: 0.3rem;
      text-transform: uppercase;
    }

    .card.unlocked .title {
      font-size: 1rem;
      font-weight: 600;
      text-align: center;
      color: var(--primary-text);
      transition: var(--transition);
    }

    /* 已解鎖懸停效果 (Hover Animation) */
    .card.unlocked:hover {
      transform: translateY(-6px);
      box-shadow: var(--shadow-lg);
      border-color: var(--accent-color);
      background-color: #faf9f6;
    }

    .card.unlocked:hover .title {
      color: var(--accent-color);
    }

    .card.unlocked::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 4px;
      background-color: var(--accent-color);
      transform: scaleX(0);
      transition: var(--transition);
    }

    .card.unlocked:hover::after {
      transform: scaleX(1);
    }

    /* 2. 未解鎖狀態 (Week 3 ~ 16) */
    .card.locked {
      background-color: var(--card-locked-bg);
      color: var(--locked-text);
      cursor: not-allowed;
      border: 1px dashed #d0cdb8;
    }

    .card.locked .lock-icon {
      font-size: 1.4rem;
      margin-bottom: 0.3rem;
      opacity: 0.7;
      transition: transform 0.3s ease;
    }

    .card.locked .title {
      font-size: 0.9rem;
      font-weight: 400;
      color: var(--locked-text);
    }

    /* 未解鎖懸停效果：鎖頭晃動微動畫 */
    .card.locked:hover {
      background-color: #e4e1d7;
    }

    .card.locked:hover .lock-icon {
      animation: shake 0.5s ease-in-out;
    }

    /* 動畫定義 */
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(-10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    @keyframes shake {
      0%, 100% { transform: rotate(0deg); }
      20% { transform: rotate(-12deg); }
      40% { transform: rotate(12deg); }
      60% { transform: rotate(-8deg); }
      80% { transform: rotate(8deg); }
    }

    /* 響應式佈局設定 (RWD) */
    @media (max-width: 768px) {
      .portfolio-grid {
        grid-template-columns: repeat(2, 1fr); /* 平板/大手機顯示兩欄 */
        gap: 1rem;
      }
    }

    @media (max-width: 480px) {
      body {
        padding: 2rem 1rem;
      }
      .portfolio-grid {
        grid-template-columns: repeat(2, 1fr); /* 小型手機維持雙欄，提高精緻感 */
        gap: 0.8rem;
      }
      .card {
        height: 100px;
        padding: 0.8rem;
      }
      .card.unlocked .title {
        font-size: 0.9rem;
      }
    }

    /* 頁尾聲明 */
    footer {
      margin-top: 3.5rem;
      font-size: 0.8rem;
      color: var(--secondary-text);
      letter-spacing: 1px;
    }
  </style>
</head>
<body>

  <!-- 個人資料與頭像區塊 -->
  <header class="profile-header">
    <div class="avatar-wrapper">
      <!-- 這裡預設載入您的照片 IMG_5180.PNG，若找不到圖片則有預設文字備援 -->
      <img src="IMG_5180.PNG" alt="個人大頭貼" class="avatar-img" onerror="this.src='https://via.placeholder.com/150/d2c9b1/ffffff?text=Avatar'">
    </div>
    <h1 class="profile-name">網頁程式設計作品集</h1>
    <p class="profile-subtitle">Web Design & Development Portfolio</p>
  </header>

  <!-- 16 個任務關卡按鈕網格 -->
  <main class="portfolio-grid">
    <!-- 已解鎖項目 1 -->
    <a href="w1/index.html" class="card unlocked">
      <span class="week-tag">Week 01</span>
      <span class="title">數位名片</span>
    </a>

    <!-- 已解鎖項目 2 -->
    <a href="w2/index.html" class="card unlocked">
      <span class="week-tag">Week 02</span>
      <span class="title">今天吃甚麼?</span>
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
