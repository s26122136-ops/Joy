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

    /* --------------------------------------------------
     * 6. Week 4 悄悄話動態留言牆樣式
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
      animation: spin 1s infinite linear;
    }

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

    .msg-card.is-highlighted {
      transform: scale(1.05);
      border-color: var(--highlight-border);
      box-shadow: 0 10px 30px var(--highlight-glow);
      background-color: var(--highlight-bg);
      z-index: 10;
    }

    .masonry-container.has-active .msg-card:not(.is-highlighted) {
      opacity: 0.4;
      filter: blur(1px);
      transform: scale(0.98);
    }

    /* --------------------------------------------------
     * 7. Week 3 迷因產生器 Modal 彈窗專屬樣式
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
      background: #fef08a;
      background-image: radial-gradient(#facc15 2px, transparent 2px);
      background-size: 24px 24px;
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
      font-family: 'Fredoka', 'Noto Sans TC', sans-serif;
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

    .meme-text {
      font-family: 'Impact', 'Bungee', 'Noto Sans TC', sans-serif;
      text-transform: uppercase;
      letter-spacing: 1px;
      line-height: 1.1;
      text-shadow: 
        3px 3px 0 #000, -3px -3px 0 #000, 
        3px -3px 0 #000, -3px 3px 0 #000,
        0 4px 0 #000, 0 -4px 0 #000, 
        4px 0 0 #000, -4px 0 0 #000,
        0 0 10px rgba(0,0,0,0.8);
      word-break: break-word;
      user-select: none;
    }

    .funky-card {
      background: #ffffff;
      border: 4px solid #000000;
      box-shadow: 8px 8px 0px #000000;
      border-radius: 16px;
    }

    .funky-btn {
      border: 3px solid #000000;
      box-shadow: 4px 4px 0px #000000;
      transition: all 0.15s ease-in-out;
      font-weight: 700;
    }

    .funky-btn:hover {
      transform: translate(-2px, -2px);
      box-shadow: 6px 6px 0px #000000;
    }

    .funky-btn:active {
      transform: translate(2px, 2px);
      box-shadow: 2px 2px 0px #000000;
    }

    @keyframes wiggle {
      0%, 100% { transform: rotate(-2deg); }
      50% { transform: rotate(2deg); }
    }
    .hover-wiggle:hover {
      animation: wiggle 0.3s infinite ease-in-out;
    }

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
      <!-- Week 1: 鎖定 -->
      <div class="card locked">
        <div class="card-header">
          <span class="week-tag">Week 01</span>
          <span class="status-badge lock-icon">🔒</span>
        </div>
        <h3 class="card-title">HTML / CSS 基礎體驗</h3>
      </div>

      <!-- Week 2: 鎖定 -->
      <div class="card locked">
        <div class="card-header">
          <span class="week-tag">Week 02</span>
          <span class="status-badge lock-icon">🔒</span>
        </div>
        <h3 class="card-title">JavaScript 基礎語法</h3>
      </div>

      <!-- Week 3: 已解鎖 (點擊打開 Modal 迷因產生器) -->
      <div class="card unlocked" onclick="openMemeModal()">
        <div class="card-header">
          <span class="week-tag">Week 03</span>
          <span class="status-badge card-arrow">➔</span>
        </div>
        <h3 class="card-title">🤪 搞怪迷因產生器</h3>
      </div>

      <!-- Week 4: 已解鎖 (點擊切換至留言牆頁面) -->
      <div class="card unlocked" onclick="switchPage('board-page')">
        <div class="card-header">
          <span class="week-tag">Week 04</span>
          <span class="status-badge card-arrow">➔</span>
        </div>
        <h3 class="card-title">悄悄話動態留言牆</h3>
      </div>
    </main>
  </div>

  <!-- ==========================================
       Week 4 頁面：悄悄話動態留言牆
       ========================================== -->
  <div id="board-page" class="page-container hidden">
    <header class="board-header">
      <button class="back-btn" onclick="switchPage('home-page')">← 返回作品集列表</button>
      <h1 class="board-title">悄悄話動態留言牆</h1>
      <p class="board-subtitle">傾聽大家留下的心聲與悄悄話</p>
    </header>

    <div id="loading">
      <div class="whisper-spinner"></div>
      <p>正在拉取悄悄話...</p>
    </div>

    <main id="masonry-board" class="masonry-container"></main>
  </div>

  <!-- ==========================================
       Week 3 Modal 彈窗：搞怪迷因產生器
       ========================================== -->
  <div id="meme-modal" class="modal-overlay">
    <div class="meme-app-wrapper">
      <button class="close-btn" onclick="closeMemeModal()">✕</button>
      
      <!-- 標題區 -->
      <div class="text-center mb-6">
        <div class="inline-block bg-pink-500 text-white px-6 py-2 border-4 border-black rounded-2xl shadow-[6px_6px_0px_0px_rgba(0,0,0,1)] -rotate-1 hover-wiggle">
          <h2 class="text-2xl md:text-4xl font-extrabold tracking-wider flex items-center gap-2">
            <span>🤪</span> 迷因發射器 Meme Studio <span>🔥</span>
          </h2>
        </div>
      </div>

      <!-- 控制面板與預覽畫布 -->
      <div class="meme-generator-grid">
        <!-- 左側：控制台 -->
        <div class="funky-card p-4 space-y-4 text-left">
          <h3 class="text-xl font-black border-b-4 border-black pb-2">🛠️ 迷因控制台</h3>

          <!-- 上傳與預設底圖 -->
          <div>
            <label class="block font-black text-slate-800 mb-1">1. 選擇底圖 (本機上傳)</label>
            <input type="file" id="imageInput" accept="image/*" style="display: none;" />
            <button onclick="document.getElementById('imageInput').click()" class="w-full py-2 px-3 bg-cyan-300 hover:bg-cyan-400 text-black funky-btn rounded-xl text-sm mb-2">
              📁 上傳你的梗圖照片
            </button>
            <div class="flex gap-1 flex-wrap">
              <span class="text-xs font-bold text-slate-600 w-full mb-1">預設底圖：</span>
              <button onclick="loadPresetImage('doge')" class="text-xs bg-amber-200 hover:bg-amber-300 px-2 py-1 rounded border-2 border-black font-bold">🐕 柴犬</button>
              <button onclick="loadPresetImage('cat')" class="text-xs bg-orange-200 hover:bg-orange-300 px-2 py-1 rounded border-2 border-black font-bold">🙀 震驚貓</button>
              <button onclick="loadPresetImage('success')" class="text-xs bg-emerald-200 hover:bg-emerald-300 px-2 py-1 rounded border-2 border-black font-bold">👶 成功男孩</button>
            </div>
          </div>

          <!-- 文字輸入 -->
          <div class="space-y-2 pt-2 border-t-2 border-slate-200">
            <label class="block font-black text-slate-800">2. 輸入經典迷因文字</label>
            <div>
              <span class="text-xs font-bold text-slate-500">上方文字 (Top Text)</span>
              <input type="text" id="topTextInput" value="當你寫的 Code" class="w-full p-2 border-2 border-black rounded-lg font-bold">
            </div>
            <div>
              <span class="text-xs font-bold text-slate-500">下方文字 (Bottom Text)</span>
              <input type="text" id="bottomTextInput" value="一次就通過測試時" class="w-full p-2 border-2 border-black rounded-lg font-bold">
            </div>
          </div>

          <!-- 微調控制 -->
          <div class="space-y-2 pt-2 border-t-2 border-slate-200 text-xs">
            <label class="block font-black text-slate-800 text-sm">3. 樣式微調</label>
            <div>
              <div class="flex justify-between font-bold">
                <span>🔤 字體大小</span>
                <span id="fontSizeVal">36px</span>
              </div>
              <input type="range" id="fontSizeSlider" min="20" max="80" value="36" class="w-full">
            </div>
            <div>
              <div class="flex justify-between font-bold">
                <span>⬆️ 上方文字高度</span>
                <span id="topPosVal">5%</span>
              </div>
              <input type="range" id="topPosSlider" min="0" max="40" value="5" class="w-full">
            </div>
            <div>
              <div class="flex justify-between font-bold">
                <span>⬇️ 下方文字高度</span>
                <span id="bottomPosVal">5%</span>
              </div>
              <input type="range" id="bottomPosSlider" min="0" max="40" value="5" class="w-full">
            </div>
            <div class="flex items-center gap-2 pt-1">
              <label for="textColorPicker" class="font-bold">🎨 文字顏色：</label>
              <input type="color" id="textColorPicker" value="#ffffff" class="w-8 h-8 border border-black rounded cursor-pointer">
            </div>
          </div>

          <!-- 按鈕 -->
          <div class="pt-2 border-t-2 border-black space-y-2">
            <button id="downloadBtn" class="w-full py-3 bg-emerald-400 hover:bg-emerald-300 text-black text-lg funky-btn rounded-xl flex items-center justify-center gap-2 hover-wiggle">
              🚀 一鍵打包下載迷因
            </button>
            <button id="resetBtn" class="w-full py-1.5 bg-slate-200 hover:bg-slate-300 text-slate-800 text-xs font-bold rounded border-2 border-black">
              🔄 重置為預設設定
            </button>
          </div>
        </div>

        <!-- 右側：即時預覽區 -->
        <div class="funky-card p-4 bg-slate-900 text-white flex flex-col items-center justify-center">
          <div class="w-full flex justify-between items-center mb-2">
            <h3 class="text-lg font-black text-yellow-400">👁️ 即時預覽畫布</h3>
          </div>
          <div id="memeContainer" class="relative inline-block max-w-full overflow-hidden select-none bg-slate-800 rounded-lg border-4 border-black">
            <img id="memeImage" src="https://images.unsplash.com/photo-1533738363-b7f9aef128ce?w=800&auto=format&fit=crop&q=80" alt="Meme Canvas" style="max-height: 400px;" class="block w-auto object-contain mx-auto pointer-events-none" crossorigin="anonymous">
            <div id="topTextDisplay" class="meme-text absolute left-0 right-0 text-center px-4 leading-tight text-white pointer-events-none uppercase">
              當你寫的 CODE
            </div>
            <div id="bottomTextDisplay" class="meme-text absolute left-0 right-0 text-center px-4 leading-tight text-white pointer-events-none uppercase">
              一次就通過測試時
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <script>
    /* ==========================================
     * 1. 頁面切換邏輯
     * ========================================== */
    function switchPage(pageId) {
      document.querySelectorAll('.page-container').forEach(page => {
        page.classList.add('hidden');
      });
      document.getElementById(pageId).classList.remove('hidden');

      if (pageId === 'board-page') {
        loadBoardData();
      }
    }

    /* ==========================================
     * 2. Modal 彈窗開關控制 (Week 3 迷因產生器)
     * ========================================== */
    function openMemeModal() {
      document.getElementById('meme-modal').classList.add('active');
    }

    function closeMemeModal() {
      document.getElementById('meme-modal').classList.remove('active');
    }

    /* ==========================================
     * 3. Week 4 留言牆數據載入邏輯
     * ========================================== */
    function loadBoardData() {
      const board = document.getElementById('masonry-board');
      const loading = document.getElementById('loading');

      // 避免重複發送請求
      if (board.children.length > 0) return;

      fetch('https://jsonplaceholder.typicode.com/comments?_limit=15')
        .then(response => response.json())
        .then(data => {
          loading.style.display = 'none';
          board.style.display = 'block';

          data.forEach(item => {
            const card = document.createElement('div');
            card.className = 'msg-card';
            card.innerHTML = `
              <div class="msg-header">
                <span class="msg-author">${item.name.split(' ')[0]}</span>
                <span class="msg-time">熱門留言</span>
              </div>
              <p class="msg-content">${item.body}</p>
            `;

            card.addEventListener('click', () => {
              document.querySelectorAll('.msg-card').forEach(c => c.classList.remove('is-highlighted'));
              card.classList.add('is-highlighted');
              board.classList.add('has-active');
            });

            board.appendChild(card);
          });
        })
        .catch(err => {
          loading.innerHTML = '<p style="color:red;">載入失敗，請稍後再試。</p>';
        });
    }

    // 點擊空白處取消留言卡片高亮
    document.addEventListener('click', (e) => {
      const board = document.getElementById('masonry-board');
      if (board && !e.target.closest('.msg-card')) {
        document.querySelectorAll('.msg-card').forEach(c => c.classList.remove('is-highlighted'));
        board.classList.remove('has-active');
      }
    });

    /* ==========================================
     * 4. Week 3 迷因產生器核心 Logic
     * ========================================== */
    const imageInput = document.getElementById('imageInput');
    const memeImage = document.getElementById('memeImage');
    const memeContainer = document.getElementById('memeContainer');

    const topTextInput = document.getElementById('topTextInput');
    const bottomTextInput = document.getElementById('bottomTextInput');
    const topTextDisplay = document.getElementById('topTextDisplay');
    const bottomTextDisplay = document.getElementById('bottomTextDisplay');

    const fontSizeSlider = document.getElementById('fontSizeSlider');
    const topPosSlider = document.getElementById('topPosSlider');
    const bottomPosSlider = document.getElementById('bottomPosSlider');
    const textColorPicker = document.getElementById('textColorPicker');

    const fontSizeVal = document.getElementById('fontSizeVal');
    const topPosVal = document.getElementById('topPosVal');
    const bottomPosVal = document.getElementById('bottomPosVal');

    const downloadBtn = document.getElementById('downloadBtn');
    const resetBtn = document.getElementById('resetBtn');

    imageInput.addEventListener('change', function(e) {
      const file = e.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = function(event) {
          memeImage.src = event.target.result;
        };
        reader.readAsDataURL(file);
      }
    });

    function loadPresetImage(type) {
      const presets = {
        'doge': 'https://images.unsplash.com/photo-1583511655857-d19b40a7a54e?w=800&auto=format&fit=crop&q=80',
        'cat': 'https://images.unsplash.com/photo-1533738363-b7f9aef128ce?w=800&auto=format&fit=crop&q=80',
        'success': 'https://images.unsplash.com/photo-1543466835-00a7907e9de1?w=800&auto=format&fit=crop&q=80'
      };
      if (presets[type]) {
        memeImage.src = presets[type];
      }
    }

    function updateMemeText() {
      topTextDisplay.textContent = topTextInput.value || '';
      bottomTextDisplay.textContent = bottomTextInput.value || '';

      const fontSize = fontSizeSlider.value;
      topTextDisplay.style.fontSize = `${fontSize}px`;
      bottomTextDisplay.style.fontSize = `${fontSize}px`;
      fontSizeVal.textContent = `${fontSize}px`;

      const topPos = topPosSlider.value;
      topTextDisplay.style.top = `${topPos}%`;
      topPosVal.textContent = `${topPos}%`;

      const bottomPos = bottomPosSlider.value;
      bottomTextDisplay.style.bottom = `${bottomPos}%`;
      bottomPosVal.textContent = `${bottomPos}%`;

      const color = textColorPicker.value;
      topTextDisplay.style.color = color;
      bottomTextDisplay.style.color = color;
    }

    topTextInput.addEventListener('input', updateMemeText);
    bottomTextInput.addEventListener('input', updateMemeText);
    fontSizeSlider.addEventListener('input', updateMemeText);
    topPosSlider.addEventListener('input', updateMemeText);
    bottomPosSlider.addEventListener('input', updateMemeText);
    textColorPicker.addEventListener('input', updateMemeText);

    downloadBtn.addEventListener('click', function() {
      const originalText = downloadBtn.innerHTML;
      downloadBtn.innerHTML = '⏳ 生成中...';
      downloadBtn.disabled = true;

      html2canvas(memeContainer, {
        useCORS: true,
        scale: 2,
        backgroundColor: null
      }).then(canvas => {
        const imageUrl = canvas.toDataURL('image/png');
        const downloadLink = document.createElement('a');
        downloadLink.href = imageUrl;
        downloadLink.download = 'my-meme.png';

        document.body.appendChild(downloadLink);
        downloadLink.click();
        document.body.removeChild(downloadLink);

        downloadBtn.innerHTML = '✅ 下載成功！';
        setTimeout(() => {
          downloadBtn.innerHTML = originalText;
          downloadBtn.disabled = false;
        }, 2000);
      }).catch(err => {
        console.error('截圖失敗：', err);
        alert('生成失敗，請確認圖片已順利載入！');
        downloadBtn.innerHTML = originalText;
        downloadBtn.disabled = false;
      });
    });

    resetBtn.addEventListener('click', function() {
      topTextInput.value = '當你寫的 CODE';
      bottomTextInput.value = '一次就通過測試時';
      fontSizeSlider.value = 36;
      topPosSlider.value = 5;
      bottomPosSlider.value = 5;
      textColorPicker.value = '#ffffff';
      updateMemeText();
    });

    window.onload = function() {
      updateMemeText();
    };
  </script>
</body>
</html>
