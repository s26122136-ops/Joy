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
            opacity: 0.
