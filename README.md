<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>作品集展示與迷因產生器</title>

  <!-- 引入 Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Bungee&family=Fredoka:wght@600;700&family=Inter:wght@300;400;500;600;800&family=Noto+Sans+TC:wght@500;700;900&family=Noto+Serif+TC:wght@300;400;600&display=swap" rel="stylesheet">

  <!-- 引入 html2canvas 截圖下載 CDN -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>

  <style>
    /* --------------------------------------------------
     * 1. 全局樣式與變數定義 (莫蘭迪文青色調)
     * -------------------------------------------------- */
    :root {
      --bg-color: #f7f5f0;           /* 柔和米白紙張背景 */
      --card-bg: #ffffff;            /* 卡片純白背景 */
      --text-main: #3d405b;          /* 深莫蘭迪藍灰 (主文字) */
      --text-sub: #8d99ae;           /* 靜謐灰藍 (次要文字) */
      --accent-color: #e07a5f;       /* 溫暖暖橙 (點綴色) */
      --accent-hover: #d1684e;       /* 懸停點綴色 */
      --locked-bg: #eceae4;          /* 鎖定狀態卡片背景 */
      --locked-text: #a0a5aa;        /* 鎖定狀態文字 */
      --border-color: #e2dfd7;       /* 柔和邊框 */
      --shadow-soft: 0 10px 30px rgba(61, 64, 91, 0.05);
      --shadow-hover: 0 15px 35px rgba(61, 64, 91, 0.12);

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
     * 5. 作品卡片樣式
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

    .badge {
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

    .card-footer {
      margin-top: 0.8rem;
      font-size: 0.85rem;
    }

    .card.unlocked {
      border-left: 4px solid var(--accent-color);
      cursor: pointer;
    }

    .card.unlocked .badge {
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

    .card.unlocked .action-text {
      color: var(--accent-color);
      font-weight: 500;
    }

    .card.locked {
      background-color: var(--locked-bg);
      border-color: var(--border-color);
      cursor: not-allowed;
      opacity: 0.75;
    }

    .card.locked .card-title,
    .card.locked .action-text {
      color: var(--locked-text);
      font-weight: 400;
    }

    .card.locked .badge {
      color: var(--locked-text);
      opacity: 0.7;
    }

    .card.locked:hover {
      transform: translateY(-2px);
      opacity: 0.9;
    }

    .shake-anim {
      animation: lockShake 0.35s ease-in-out;
    }

    @keyframes lockShake {
      0%, 100% { transform: translateX(0); }
      25% { transform: translateX(-5px); }
      75% { transform: translateX(5px); }
    }

    footer {
      text-align: center;
      margin-top: 3.5rem;
      font-size: 0.85rem;
      color: var(--text-sub);
    }
  </style>
</head>
<body>

  <!-- ==========================================
       主入口頁面 (Week 作品選單)
       ========================================== -->
  <div id="home-page" class="page-container">
    <header class="profile-section">
      <div class="avatar-wrapper">
        <img src="https://images.unsplash.com/photo-1534528741775-53994a69daeb?auto=format&fit=crop&w=300&q=80" alt="個人頭像" class="avatar">
      </div>
      <h1 class="profile-name">我的前端作品集</h1>
      <p class="profile-bio">探索每週學習成果與互動網頁實作專案</p>
      <div class="divider"></div>
    </header>

  <main class="card-grid">
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
      <!-- Week 5 (已解鎖) -->
      <a href="w5/index.html" class="card unlocked">
        <div class="card-header">
          <span class="badge">WEEK 05</span>
          <span class="icon">🔮</span>
        </div>
        <div class="card-title">Week 5 - 雲端心電感應</div>
        <div class="card-footer">
          <span class="action-text">前往關卡 ➔</span>
        </div>
      </a>
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
