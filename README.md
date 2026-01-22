<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mening Web App'im</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        :root {
            --primary: #0088cc;
            --secondary: #6c757d;
            --success: #28a745;
            --danger: #dc3545;
            --light: #f8f9fa;
            --dark: #343a40;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: var(--dark);
            padding: 20px;
        }
        
        .container {
            max-width: 500px;
            margin: 0 auto;
        }
        
        .header {
            background: white;
            border-radius: 20px 20px 0 0;
            padding: 25px;
            text-align: center;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            margin-bottom: 15px;
        }
        
        .header h1 {
            color: var(--primary);
            margin-bottom: 10px;
            font-size: 24px;
        }
        
        .header p {
            color: var(--secondary);
            font-size: 14px;
        }
        
        .card {
            background: white;
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 15px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .card h2 {
            color: var(--primary);
            margin-bottom: 15px;
            font-size: 18px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .card h2 i {
            font-size: 20px;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: var(--dark);
        }
        
        .form-control {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #e9ecef;
            border-radius: 10px;
            font-size: 16px;
            transition: border-color 0.3s;
        }
        
        .form-control:focus {
            outline: none;
            border-color: var(--primary);
        }
        
        textarea.form-control {
            min-height: 100px;
            resize: vertical;
        }
        
        .radio-group {
            display: flex;
            gap: 15px;
            margin-top: 10px;
        }
        
        .radio-item {
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .btn {
            display: block;
            width: 100%;
            padding: 15px;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            text-align: center;
            margin-top: 10px;
        }
        
        .btn-primary {
            background: var(--primary);
            color: white;
        }
        
        .btn-primary:hover {
            background: #0077b3;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 136, 204, 0.3);
        }
        
        .btn-success {
            background: var(--success);
            color: white;
        }
        
        .btn-success:hover {
            background: #218838;
        }
        
        .user-info {
            background: var(--light);
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            font-size: 14px;
        }
        
        .user-info p {
            margin: 5px 0;
        }
        
        .status {
            padding: 15px;
            border-radius: 10px;
            margin-top: 20px;
            display: none;
            text-align: center;
            font-weight: 500;
        }
        
        .status.success {
            background: rgba(40, 167, 69, 0.1);
            color: var(--success);
            border: 1px solid var(--success);
            display: block;
        }
        
        .status.error {
            background: rgba(220, 53, 69, 0.1);
            color: var(--danger);
            border: 1px solid var(--danger);
            display: block;
        }
        
        .footer {
            text-align: center;
            margin-top: 30px;
            color: white;
            font-size: 12px;
            opacity: 0.8;
        }
        
        @media (max-width: 480px) {
            .container {
                padding: 10px;
            }
            
            .card, .header {
                padding: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>📱 Mening Web App'im</h1>
            <p>Bot'ga turli xabar va ma'lumotlarni yuborish</p>
        </div>
        
        <div class="user-info" id="userInfo">
            <p><strong>👤 Foydalanuvchi:</strong> Yuklanmoqda...</p>
            <p><strong>🆔 ID:</strong> Yuklanmoqda...</p>
            <p><strong>📱 Platforma:</strong> Yuklanmoqda...</p>
        </div>
        
        <div class="card">
            <h2>📨 Xabar yuborish</h2>
            <div class="form-group">
                <label for="message">Xabar matni:</label>
                <textarea 
                    id="message" 
                    class="form-control" 
                    placeholder="Bu yerda xabar yozing..."
                    rows="3">Salom! Men Web App'dan yuboryapman 🚀</textarea>
            </div>
            
            <div class="form-group">
                <label>Xabar turi:</label>
                <div class="radio-group">
                    <div class="radio-item">
                        <input type="radio" id="type1" name="messageType" value="oddiy" checked>
                        <label for="type1">Oddiy xabar</label>
                    </div>
                    <div class="radio-item">
                        <input type="radio" id="type2" name="messageType" value="shikoyat">
                        <label for="type2">Shikoyat</label>
                    </div>
                    <div class="radio-item">
                        <input type="radio" id="type3" name="messageType" value="taklif">
                        <label for="type3">Taklif</label>
                    </div>
                </div>
            </div>
            
            <div class="form-group">
                <label for="category">Kategoriya:</label>
                <select id="category" class="form-control">
                    <option value="umumiy">Umumiy</option>
                    <option value="texnik">Texnik masala</option>
                    <option value="fikr">Fikr-mulohaza</option>
                    <option value="boshqa">Boshqa</option>
                </select>
            </div>
            
            <button class="btn btn-primary" onclick="sendMessage()">
                📤 Xabarni yuborish
            </button>
        </div>
        
        <div class="card">
            <h2>⚡ Tezkor xabarlar</h2>
            <div class="quick-buttons">
                <button class="btn btn-primary" onclick="sendQuickMessage('👋 Salom! Hozir mavjudman')">
                    Salom
                </button>
                <button class="btn btn-primary" onclick="sendQuickMessage('❓ Savolim bor')">
                    Savol
                </button>
                <button class="btn btn-primary" onclick="sendQuickMessage('🆘 Yordam kerak')">
                    Yordam
                </button>
                <button class="btn btn-primary" onclick="sendQuickMessage('✅ Tushunarli, rahmat')">
                    Tushunarli
                </button>
            </div>
        </div>
        
        <div class="card">
            <h2>📊 Test natijalari</h2>
            <p>Web App'ning ishlashini tekshirish:</p>
            <button class="btn btn-success" onclick="runTests()">
                🧪 Testlarni ishga tushirish
            </button>
        </div>
        
        <div class="status" id="status"></div>
        
        <div class="footer">
            <p>© 2024 Mening Web App'im | Telegram Mini App</p>
            <p>GitHub Pages | Telegram Bot API</p>
        </div>
    </div>
    
    <script>
        // Telegram Web App obyekti
        const tg = window.Telegram.WebApp;
        
        // App'ni to'liq ekran qilish
        tg.expand();
        
        // Foydalanuvchi ma'lumotlarini ko'rsatish
        function updateUserInfo() {
            const user = tg.initDataUnsafe.user;
            const userInfo = document.getElementById('userInfo');
            
            if (user) {
                userInfo.innerHTML = `
                    <p><strong>👤 Foydalanuvchi:</strong> ${user.first_name || 'Noma\'lum'} ${user.last_name || ''}</p>
                    <p><strong>🆔 ID:</strong> ${user.id}</p>
                    <p><strong>📱 Platforma:</strong> ${tg.platform}</p>
                    <p><strong>👤 Username:</strong> @${user.username || 'yo\'q'}</p>
                `;
            } else {
                userInfo.innerHTML = '<p>Test rejimida ishlamoqdasiz</p>';
            }
        }
        
        // Asosiy xabar yuborish funksiyasi
        function sendMessage() {
            const message = document.getElementById('message').value;
            const messageType = document.querySelector('input[name="messageType"]:checked').value;
            const category = document.getElementById('category').value;
            
            if (!message.trim()) {
                showStatus('Xabar matni bo\'sh bo\'lishi mumkin emas!', 'error');
                return;
            }
            
            // JSON formatida ma'lumot tayyorlaymiz
            const data = {
                type: 'message',
                content: message,
                messageType: messageType,
                category: category,
                timestamp: new Date().toISOString(),
                platform: tg.platform,
                user: tg.initDataUnsafe.user ? {
                    id: tg.initDataUnsafe.user.id,
                    name: tg.initDataUnsafe.user.first_name
                } : null
            };
            
            // Bot'ga yuboramiz
            tg.sendData(JSON.stringify(data));
            
            // Status ko'rsatamiz
            showStatus('✅ Xabar muvaffaqiyatli yuborildi!', 'success');
            
            // 2 soniyadan so'ng app'ni yopamiz
            setTimeout(() => {
                tg.close();
            }, 2000);
        }
        
        // Tezkor xabar yuborish
        function sendQuickMessage(text) {
            const data = {
                type: 'quick_message',
                content: text,
                timestamp: new Date().toISOString()
            };
            
            tg.sendData(JSON.stringify(data));
            showStatus(`✅ "${text}" xabari yuborildi!`, 'success');
            
            setTimeout(() => {
                tg.close();
            }, 1500);
        }
        
        // Testlarni ishga tushirish
        function runTests() {
            const tests = [
                {name: "Web App obyekti", result: !!tg},
                {name: "Telegram API", result: !!window.Telegram},
                {name: "Foydalanuvchi ma'lumoti", result: !!tg.initDataUnsafe.user},
                {name: "Platforma", result: !!tg.platform}
            ];
            
            const passed = tests.filter(t => t.result).length;
            const total = tests.length;
            
            const testResults = tests.map(t => 
                `${t.result ? '✅' : '❌'} ${t.name}`
            ).join('\n');
            
            const summary = `🧪 Test natijalari: ${passed}/${total} o'tdi\n\n${testResults}`;
            
            const data = {
                type: 'test_results',
                results: tests,
                summary: summary,
                passed: passed,
                total: total
            };
            
            tg.sendData(JSON.stringify(summary));
            showStatus(summary, passed === total ? 'success' : 'error');
        }
        
        // Status ko'rsatish
        function showStatus(text, type = 'success') {
            const status = document.getElementById('status');
            status.textContent = text;
            status.className = `status ${type}`;
            
            // 5 soniyadan so'ng yashirish
            setTimeout(() => {
                status.style.display = 'none';
            }, 5000);
        }
        
        // Tayyor ekanligini bildirish
        tg.ready();
        
        // Foydalanuvchi ma'lumotlarini yangilash
        updateUserInfo();
        
        // Konsolga debug ma'lumotlari
        console.log('Telegram Web App ishga tushdi:', {
            platform: tg.platform,
            user: tg.initDataUnsafe.user,
            initData: tg.initData
        });
    </script>
</body>
</html># miniapp
