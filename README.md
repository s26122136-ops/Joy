<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>我的網頁作品集</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://fonts.googleapis.com/css2?family=Noto+Serif+TC:wght@400;600;700&family=Plus+Jakarta+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            serif: ['"Noto Serif TC"', 'serif'],
            sans: ['"Plus Jakarta Sans"', '-apple-system', 'sans-serif'],
          }
        }
      }
    }
  </script>
</head>
<body class="bg-slate-50 text-slate-800 font-sans min-h-screen selection:bg-indigo-100 selection:text-indigo-700">

  <!-- Header -->
  <header class="bg-white border-b border-slate-200 sticky top-0 z-30 shadow-sm">
    <div class="max-w-5xl mx-auto px-6 py-5 flex justify-between items-center">
      <div class="flex items-center gap-3">
        <div class="w-10 h-10 rounded-xl bg-indigo-600 text-white flex items-center justify-center font-serif font-bold text-xl shadow-md">
          W
        </div>
        <div>
          <h1 class="font-serif font-bold text-xl text-slate-900 tracking-wide">網頁設計作品集</h1>
          <p class="text-xs text-slate-500">Web Design Portfolio</p>
        </div>
      </div>
    </div>
  </header>

  <!-- Main Content -->
  <main class="max-w-5xl mx-auto px-6 py-12">
    
    <div class="mb-10 text-center">
      <h2 class="font-serif text-3xl font-bold text-slate-900 mb-3">課堂作業展示</h2>
      <p class="text-slate-500 text-sm">點擊下方各作業卡片，即可進入瀏覽對應的網頁作品。</p>
    </div>

    <!-- 作業列表 Grid -->
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
 <!-- 作業一 -->
 <a href="w1/index.html" class="group block bg-white rounded-2xl p-6 border border-slate-200 shadow-sm hover:shadow-xl hover:border-indigo-200 transition-all duration-300 hover:-translate-y-1">
        <div class="flex justify-between items-start mb-4">
          <span class="px-3 py-1 bg-slate-100 text-slate-600 text-xs font-bold rounded-lg group-hover:bg-indigo-100 group-hover:text-indigo-700 transition-colors">Week 1</span>
        </div>
        <h3 class="font-serif text-xl font-bold text-slate-900 mb-2 group-hover:text-indigo-600 transition-colors">作業一</h3>
        <p class="text-sm text-slate-500 line-clamp-2">基礎網頁建置與個人介紹頁面。</p>
      </a>
      <!-- 作業二 -->
   <a href="w2/index.html" class="group block bg-white rounded-2xl p-6 border border-slate-200 shadow-sm hover:shadow-xl hover:border-indigo-200 transition-all duration-300 hover:-translate-y-1">
        <div class="flex justify-between items-start mb-4">
          <span class="px-3 py-1 bg-slate-100 text-slate-600 text-xs font-bold rounded-lg group-hover:bg-indigo-100 group-hover:text-indigo-700 transition-colors">Week 2</span>
        </div>
        <h3 class="font-serif text-xl font-bold text-slate-900 mb-2 group-hover:text-indigo-600 transition-colors">作業二</h3>
        <p class="text-sm text-slate-500 line-clamp-2">CSS 樣式設計與排版練習。</p>
      </a>

   <!-- 作業三 -->
  <a href="w3/index.html" class="group block bg-white rounded-2xl p-6 border border-slate-200 shadow-sm hover:shadow-xl hover:border-indigo-200 transition-all duration-300 hover:-translate-y-1">
        <div class="flex justify-between items-start mb-4">
          <span class="px-3 py-1 bg-slate-100 text-slate-600 text-xs font-bold rounded-lg group-hover:bg-indigo-100 group-hover:text-indigo-700 transition-colors">Week 3</span>
        </div>
        <h3 class="font-serif text-xl font-bold text-slate-900 mb-2 group-hover:text-indigo-600 transition-colors">作業三</h3>
        <p class="text-sm text-slate-500 line-clamp-2">RWD 響應式網頁設計實作。</p>
      </a>
 <!-- 作業四 -->
      <a href="w4/index.html" class="group block bg-white rounded-2xl p-6 border border-slate-200 shadow-sm hover:shadow-xl hover:border-indigo-200 transition-all duration-300 hover:-translate-y-1">
        <div class="flex justify-between items-start mb-4">
          <span class="px-3 py-1 bg-slate-100 text-slate-600 text-xs font-bold rounded-lg group-hover:bg-indigo-100 group-hover:text-indigo-700 transition-colors">Week 4</span>
        </div>
        <h3 class="font-serif text-xl font-bold text-slate-900 mb-2 group-hover:text-indigo-600 transition-colors">作業四</h3>
        <p class="text-sm text-slate-500 line-clamp-2">JavaScript 互動功能與動態效果。</p>
      </a>
<!-- 作業五 (本次新增) -->
      <a href="w5/index.html" class="group block bg-gradient-to-br from-white to-orange-50/50 rounded-2xl p-6 border border-orange-200 shadow-md hover:shadow-xl hover:border-orange-300 transition-all duration-300 hover:-translate-y-1 relative overflow-hidden">
        <!-- 裝飾用背景光暈 -->
        <div class="absolute -right-6 -top-6 w-24 h-24 bg-orange-200 rounded-full blur-2xl opacity-50 group-hover:opacity-100 transition-opacity"></div>
        
  <div class="flex justify-between items-start mb-4 relative z-10">
          <span class="px-3 py-1 bg-orange-100 text-orange-700 text-xs font-bold rounded-lg shadow-sm">Week 5</span>
          <span class="flex h-3 w-3 relative">
            <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-orange-400 opacity-75"></span>
            <span class="relative inline-flex rounded-full h-3 w-3 bg-orange-500"></span>
          </span>
        </div>
        <h3 class="font-serif text-xl font-bold text-slate-900 mb-2 group-hover:text-orange-700 transition-colors relative z-10">作業五：雲端心電感應</h3>
        <p class="text-sm text-slate-600 line-clamp-2 relative z-10">多人同步互動遊戲，結合 3D 翻牌特效與實時狀態同步。</p>
      </a>

    </div>
  </main>

  <footer class="border-t border-slate-200 mt-auto py-6 text-center text-sm text-slate-400">
    &copy; 2026 Web Design Portfolio. All rights reserved.
  </footer>

</body>
</html>
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
