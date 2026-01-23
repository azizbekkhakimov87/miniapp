<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Telegram Web App</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        :root {
            --primary: #0088cc;
            --secondary: #6c757d;
            --success: #28a745;
            --warning: #ffc107;
            --danger: #dc3545;
            --light: #f8f9fa;
            --dark: #343a40;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
            padding: 15px;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .container {
            width: 100%;
            max-width: 420px;
            background: white;
            border-radius: 25px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.2);
            overflow: hidden;
            animation: fadeIn 0.5s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .header {
            background: linear-gradient(135deg, var(--primary) 0%, #0099cc 100%);
            color: white;
            padding: 30px 25px;
            text-align: center;
            position: relative;
            overflow: hidden;
        }
        
        .header::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.1) 1px, transparent 1px);
            background-size: 30px 30px;
            animation: float 20s linear infinite;
        }
        
        @keyframes float {
            0% { transform: translate(0, 0) rotate(0deg); }
            100% { transform: translate(-30px, -30px) rotate(360deg); }
        }
        
        .header-content {
            position: relative;
            z-index: 2;
        }
        
        .header h1 {
            font-size: 28px;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            font-weight: 700;
        }
        
        .header p {
            font-size: 15px;
            opacity: 0.95;
            line-height: 1.5;
        }
        
        .badge {
            display: inline-block;
            background: rgba(255,255,255,0.2);
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 12px;
            margin-top: 10px;
            font-weight: 500;
        }
        
        .user-card {
            background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
            margin: 20px;
            padding: 20px;
            border-radius: 18px;
            border-left: 5px solid var(--primary);
            box-shadow: 0 5px 15px rgba(0,0,0,0.05);
        }
        
        .user-card h3 {
            color: var(--primary);
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 18px;
        }
        
        .user-info {
            display: grid;
            gap: 8px;
        }
        
        .info-row {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid rgba(0,0,0,0.05);
        }
        
        .info-label {
            color: var(--secondary);
            font-weight: 500;
        }
        
        .info-value {
            color: var(--dark);
            font-weight: 600;
        }
        
        .content {
            padding: 25px;
        }
        
        .section {
            margin-bottom: 25px;
            animation: slideUp 0.5s ease;
        }
        
        @keyframes slideUp {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .section-title {
            color: var(--primary);
            margin-bottom: 15px;
            font-size: 18px;
            display: flex;
            align-items: center;
            gap: 10px;
            font-weight: 600;
        }
        
        .message-box {
            position: relative;
        }
        
        .message-box textarea {
            width: 100%;
            padding: 18px;
            border: 2px solid #e0e0e0;
            border-radius: 15px;
            font-size: 16px;
            resize: vertical;
            min-height: 130px;
            transition: all 0.3s;
            background: var(--light);
            color: var(--dark);
        }
        
        .message-box textarea:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(0, 136, 204, 0.1);
        }
        
        .char-count {
            text-align: right;
            font-size: 12px;
            color: var(--secondary);
            margin-top: 5px;
        }
        
        .btn {
            padding: 18px;
            border: none;
            border-radius: 15px;
            font-size: 17px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            width: 100%;
            margin-top: 10px;
            position: relative;
            overflow: hidden;
        }
        
        .btn::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 5px;
            height: 5px;
            background: rgba(255, 255, 255, 0.5);
            opacity: 0;
            border-radius: 100%;
            transform: scale(1, 1) translate(-50%);
            transform-origin: 50% 50%;
        }
        
        .btn:focus:not(:active)::after {
            animation: ripple 1s ease-out;
        }
        
        @keyframes ripple {
            0% { transform: scale(0, 0); opacity: 0.5; }
            100% { transform: scale(50, 50); opacity: 0; }
        }
        
        .btn-primary {
            background: linear-gradient(135deg, var(--primary) 0%, #0077b3 100%);
            color: white;
            box-shadow: 0 6px 20px rgba(0, 136, 204, 0.3);
        }
        
        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(0, 136, 204, 0.4);
        }
        
        .btn-primary:active {
            transform: translateY(0);
        }
        
        .btn-success {
            background: linear-gradient(135deg, var(--success) 0%, #218838 100%);
            color: white;
            box-shadow: 0 6px 20px rgba(40, 167, 69, 0.3);
        }
        
        .btn-warning {
            background: linear-gradient(135deg, var(--warning) 0%, #e0a800 100%);
            color: var(--dark);
            box-shadow: 0 6px 20px rgba(255, 193, 7, 0.3);
        }
        
        .quick-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 12px;
            margin-top: 10px;
        }
        
        .quick-btn {
            padding: 14px;
            background: linear-gradient(135deg, #f0f8ff 0%, #e6f7ff 100%);
            border: 2px solid var(--primary);
            border-radius: 12px;
            color: var(--primary);
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            text-align: center;
        }
        
        .quick-btn:hover {
            background: var(--primary);
            color: white;
            transform: translateY(-2px);
        }
        
        .status {
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            font-weight: 600;
            margin-top: 20px;
            display: none;
            animation: fadeIn 0.5s ease;
        }
        
        .status.success {
            background: linear-gradient(135deg, #d4edda 0%, #c3e6cb 100%);
            color: #155724;
            border: 2px solid #c3e6cb;
            display: block;
        }
        
        .status.error {
            background: linear-gradient(135deg, #f8d7da 0%, #f5c6cb 100%);
            color: #721c24;
            border: 2px solid #f5c6cb;
            display: block;
        }
        
        .status.info {
            background: linear-gradient(135deg, #d1ecf1 0%, #bee5eb 100%);
            color: #0c5460;
            border: 2px solid #bee5eb;
            display: block;
        }
        
        .footer {
            text-align: center;
            padding: 20px;
            font-size: 13px;
            color: var(--secondary);
            border-top: 1px solid #eee;
            background: var(--light);
        }
        
        .footer p {
            margin: 5px 0;
        }
        
        @media (max-width: 480px) {
            .container {
                border-radius: 20px;
                margin: 10px;
            }
            
            .header {
                padding: 25px 20px;
            }
            
            .content {
                padding: 20px;
            }
            
            .quick-grid {
                grid-template-columns: 1fr;
            }
            
            .btn {
                padding: 16px;
            }
        }
        
        .loader {
            display: none;
            text-align: center;
            padding: 15px;
        }
        
        .loader-dots {
            display: inline-flex;
            gap: 6px;
        }
        
        .loader-dot {
            width: 10px;
            height: 10px;
            background: var(--primary);
            border-radius: 50%;
            animation: bounce 1.4s infinite ease-in-out both;
        }
        
        .loader-dot:nth-child(1) { animation-delay: -0.32s; }
        .loader-dot:nth-child(2) { animation-delay: -0.16s; }
        
        @keyframes bounce {
            0%, 80%, 100% { transform: scale(0); }
            40% { transform: scale(1); }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <div class="header-content">
                <h1>🤖 Telegram Web App</h1>
                <p>Bot bilan muloqot qilish uchun interfeys</p>
                <div class="badge">GitHub Pages | Telegram Bot API</div>
            </div>
        </div>
        
        <div class="user-card">
            <h3>👤 Foydalanuvchi ma'lumotlari</h3>
            <div class="user-info">
                <div class="info-row">
                    <span class="info-label">Ism:</span>
                    <span class="info-value" id="userName">Yuklanmoqda...</span>
                </div>
                <div class="info-row">
                    <span class="info-label">ID:</span>
                    <span class="info-value" id="userId">-</span>
                </div>
                <div class="info-row">
                    <span class="info-label">Platforma:</span>
                    <span class="info-value" id="platform">-</span>
                </div>
                <div class="info-row">
                    <span class="info-label">Holat:</span>
                    <span class="info-value" id="statusText">Faol ✅</span>
                </div>
            </div>
        </div>
        
        <div class="content">
            <div class="section">
                <div class="section-title">📝 Xabar yuborish</div>
                <div class="message-box">
                    <textarea id="messageInput" placeholder="Bu yerda xabaringizni yozing..." maxlength="500">Salom! Men Telegram Web App orqali xabar yuboryapman 🚀</textarea>
                    <div class="char-count"><span id="charCount">0</span>/500</div>
                </div>
                
                <button class="btn btn-primary" id="sendBtn" onclick="sendMessage()">
                    📤 Xabarni yuborish
                </button>
            </div>
            
            <div class="section">
                <div class="section-title">⚡ Tezkor xabarlar</div>
                <div class="quick-grid">
                    <button class="quick-btn" onclick="sendQuick('👋 Salom! Qandaysiz?')">Salom</button>
                    <button class="quick-btn" onclick="sendQuick('❓ Savolim bor')">Savol</button>
                    <button class="quick-btn" onclick="sendQuick('✅ Tushundim, rahmat')">Tushundim</button>
                    <button class="quick-btn" onclick="sendQuick('🆘 Yordam kerak')">Yordam</button>
                    <button class="quick-btn" onclick="sendQuick('📅 Bugungi kun qanday?')">Kun</button>
                    <button class="quick-btn" onclick="sendQuick('❤️ Juda yaxshi!')">Yaxshi</button>
                </div>
            </div>
            
            <div class="section">
                <div class="section-title">🛠️ Test va sozlamalar</div>
                <button class="btn btn-success" onclick="sendTest()">
                    ✅ Test xabarini yuborish
                </button>
                <button class="btn btn-warning" onclick="getUserInfo()">
                    👁️ Ma'lumotlarni ko'rish
                </button>
                <button class="btn btn-primary" onclick="checkConnection()">
                    📡 Ulanishni tekshirish
                </button>
            </div>
            
            <div class="loader" id="loader">
                <div class="loader-dots">
                    <div class="loader-dot"></div>
                    <div class="loader-dot"></div>
                    <div class="loader-dot"></div>
                </div>
                <p>Xabar yuborilmoqda...</p>
            </div>
            
            <div class="status" id="statusMessage"></div>
        </div>
        
        <div class="footer">
            <p>© 2024 Telegram Web App | GitHub Pages hosting</p>
            <p>Bot API: telebot | Version: 1.0.0</p>
            <p id="timestamp">Yuklangan: -</p>
        </div>
    </div>
    
    <script>
        // Telegram Web App obyekti
        const tg = window.Telegram.WebApp;
        
        // DOM elementlari
        const messageInput = document.getElementById('messageInput');
        const sendBtn = document.getElementById('sendBtn');
        const statusMessage = document.getElementById('statusMessage');
        const loader = document.getElementById('loader');
        const charCount = document.getElementById('charCount');
        
        // App'ni ishga tushirish
        function initApp() {
            // App'ni to'liq ekran qilish
            tg.expand();
            
            // Foydalanuvchi ma'lumotlarini ko'rsatish
            updateUserInfo();
            
            // Tayyor ekanligini bildirish
            tg.ready();
            
            // Vaqtni ko'rsatish
            document.getElementById('timestamp').textContent = 
                'Yuklangan: ' + new Date().toLocaleString('uz-UZ');
            
            // Belgilarni hisoblash
            updateCharCount();
            
            // Konsolga ma'lumot
            console.log('🚀 Web App ishga tushdi:', {
                platform: tg.platform,
                version: tg.version,
                user: tg.initDataUnsafe.user,
                theme: tg.themeParams
            });
            
            // Agar test rejimida bo'lsa
            if (!tg.initData) {
                showStatus("ℹ️ Test rejimida ishlamoqdasiz", "info");
            }
        }
        
        // Foydalanuvchi ma'lumotlarini yangilash
        function updateUserInfo() {
            const user = tg.initDataUnsafe.user;
            
            if (user) {
                document.getElementById('userName').textContent = 
                    user.first_name + (user.last_name ? ' ' + user.last_name : '');
                document.getElementById('userId').textContent = user.id;
                document.getElementById('platform').textContent = tg.platform;
                document.getElementById('statusText').textContent = 'Faol ✅';
            } else {
                document.getElementById('userName').textContent = "Test foydalanuvchi";
                document.getElementById('userId').textContent = "000000";
                document.getElementById('platform').textContent = "Brauzer";
                document.getElementById('statusText').textContent = 'Test rejimi ⚠️';
            }
        }
        
        // Belgilar sonini yangilash
        function updateCharCount() {
            charCount.textContent = messageInput.value.length;
        }
        
        // Asosiy xabar yuborish
        function sendMessage() {
            const text = messageInput.value.trim();
            
            if (!text) {
                showStatus("❌ Iltimos, xabar matnini kiriting!", "error");
                messageInput.focus();
                return;
            }
            
            if (text.length > 500) {
                showStatus("❌ Xabar 500 belgidan oshmasligi kerak!", "error");
                return;
            }
            
            // Yuklash ko'rsatkichini ko'rsatish
            showLoader();
            
            // Bot'ga yuborish
            tg.sendData(text);
            
            // Status ko'rsatish
            showStatus("✅ Xabar muvaffaqiyatli yuborildi!", "success");
            
            // 2 soniyadan so'ng app'ni yopish
            setTimeout(() => {
                hideLoader();
                tg.close();
            }, 2000);
        }
        
        // Test xabarini yuborish
        function sendTest() {
            const testData = {
                type: "test",
                platform: tg.platform,
                user_id: tg.initDataUnsafe.user?.id || "test",
                timestamp: new Date().toISOString(),
                message: "✅ Web App test xabari"
            };
            
            showLoader();
            tg.sendData(JSON.stringify(testData));
            showStatus("✅ Test xabari yuborildi!", "success");
            
            setTimeout(() => {
                hideLoader();
                tg.close();
            }, 1500);
        }
        
        // Tezkor xabar yuborish
        function sendQuick(text) {
            showLoader();
            tg.sendData(text);
            showStatus(`✅ "${text}" xabari yuborildi!`, "success");
            
            setTimeout(() => {
                hideLoader();
                tg.close();
            }, 1000);
        }
        
        // Foydalanuvchi ma'lumotlarini olish
        function getUserInfo() {
            const user = tg.initDataUnsafe.user;
            let info = "📋 FOYDALANUVCHI MA'LUMOTLARI\n\n";
            
            if (user) {
                info += `👤 Ism: ${user.first_name}\n`;
                if (user.last_name) info += `👤 Familiya: ${user.last_name}\n`;
                if (user.username) info += `@ Username: @${user.username}\n`;
                info += `🆔 ID: ${user.id}\n`;
                info += `🌐 Tili: ${user.language_code || 'Noma\'lum'}\n`;
            } else {
                info += "Test rejimida ishlamoqdasiz\n";
            }
            
            info += `📱 Platforma: ${tg.platform}\n`;
            info += `🎨 Tema: ${tg.themeParams?.bg_color ? 'qorong\'i' : 'och'}\n`;
            info += `🕐 Vaqt: ${new Date().toLocaleString('uz-UZ')}`;
            
            showLoader();
            tg.sendData(info);
            showStatus("👤 Ma'lumotlar yuborildi!", "success");
            
            setTimeout(() => {
                hideLoader();
                tg.close();
            }, 1500);
        }
        
        // Ulanishni tekshirish
        function checkConnection() {
            const testResult = {
                type: "connection_test",
                status: "success",
                platform: tg.platform,
                app_ready: true,
                has_user: !!tg.initDataUnsafe.user,
                timestamp: new Date().toISOString()
            };
            
            showLoader();
            tg.sendData(JSON.stringify(testResult));
            showStatus("✅ Ulanish muvaffaqiyatli!", "success");
            
            setTimeout(() => {
                hideLoader();
            }, 1000);
        }
        
        // Status xabarini ko'rsatish
        function showStatus(text, type = "success") {
            statusMessage.textContent = text;
            statusMessage.className = "status " + type;
            
            // 4 soniyadan so'ng yashirish
            setTimeout(() => {
                statusMessage.style.display = 'none';
            }, 4000);
        }
        
        // Yuklash ko'rsatkichini ko'rsatish
        function showLoader() {
            loader.style.display = 'block';
            sendBtn.disabled = true;
            sendBtn.innerHTML = '⏳ Yuborilmoqda...';
        }
        
        // Yuklash ko'rsatkichini yashirish
        function hideLoader() {
            loader.style.display = 'none';
            sendBtn.disabled = false;
            sendBtn.innerHTML = '📤 Xabarni yuborish';
        }
        
        // Hodisalar
        messageInput.addEventListener('input', updateCharCount);
        messageInput.addEventListener('keypress', function(e) {
            if (e.key === 'Enter' && e.ctrlKey) {
                sendMessage();
            }
        });
        
        // App'ni ishga tushirish
        document.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>
