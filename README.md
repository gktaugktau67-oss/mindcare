<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MindCare - Deteksi Kesehatan Mental</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            width: 100%;
            max-width: 900px;
            padding: 40px;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .logo-header {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 30px;
        }

        .logo-text {
            font-size: 28px;
            font-weight: bold;
            background: linear-gradient(135deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .tagline {
            font-size: 14px;
            color: #666;
            font-style: italic;
        }

        h1 {
            color: #333;
            margin-bottom: 10px;
            font-size: 32px;
        }

        h2 {
            color: #555;
            margin-bottom: 30px;
            font-size: 20px;
            font-weight: normal;
        }

        .form-group {
            margin-bottom: 25px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            color: #555;
            font-weight: 600;
        }

        input[type="text"],
        input[type="password"] {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 16px;
            transition: all 0.3s;
        }

        input[type="text"]:focus,
        input[type="password"]:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .btn {
            width: 100%;
            padding: 14px;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            margin-bottom: 10px;
        }

        .btn-primary {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(102, 126, 234, 0.3);
        }

        .btn-secondary {
            background: #f0f0f0;
            color: #555;
        }

        .btn-secondary:hover {
            background: #e0e0e0;
        }

        .mascot {
            text-align: center;
            margin: 30px 0;
        }

        .mascot-img {
            font-size: 120px;
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }

        .welcome-text {
            font-size: 28px;
            color: #333;
            margin-bottom: 10px;
            font-weight: bold;
        }

        .hamburger {
            position: absolute;
            top: 30px;
            right: 30px;
            cursor: pointer;
            z-index: 100;
        }

        .hamburger div {
            width: 30px;
            height: 3px;
            background: #667eea;
            margin: 6px 0;
            border-radius: 3px;
            transition: 0.3s;
        }

        .menu-dropdown {
            position: absolute;
            top: 70px;
            right: 30px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            display: none;
            overflow: hidden;
            z-index: 99;
        }

        .menu-dropdown.active {
            display: block;
            animation: slideDown 0.3s ease;
        }

        @keyframes slideDown {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .menu-item {
            padding: 15px 25px;
            cursor: pointer;
            transition: 0.3s;
            color: #555;
            border-bottom: 1px solid #f0f0f0;
        }

        .menu-item:last-child {
            border-bottom: none;
        }

        .menu-item:hover {
            background: #f8f8f8;
            color: #667eea;
        }

        .question-container {
            margin-bottom: 30px;
            padding: 20px;
            background: #f8f9fa;
            border-radius: 10px;
            border-left: 4px solid #667eea;
        }

        .question-text {
            font-size: 18px;
            color: #333;
            margin-bottom: 15px;
            font-weight: 500;
        }

        .radio-group {
            display: flex;
            gap: 20px;
        }

        .radio-label {
            display: flex;
            align-items: center;
            cursor: pointer;
            font-size: 16px;
            color: #555;
        }

        .radio-label input[type="radio"] {
            margin-right: 8px;
            width: 20px;
            height: 20px;
            cursor: pointer;
        }

        .result-card {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 30px;
            border-radius: 15px;
            margin-bottom: 30px;
            text-align: center;
        }

        .result-title {
            font-size: 32px;
            margin-bottom: 10px;
        }

        .result-subtitle {
            font-size: 18px;
            opacity: 0.9;
        }

        .chart-container {
            background: white;
            padding: 30px;
            border-radius: 15px;
            margin-bottom: 30px;
        }

        .solution-box {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            border-left: 5px solid #667eea;
        }

        .solution-title {
            font-size: 22px;
            color: #333;
            margin-bottom: 15px;
            font-weight: bold;
        }

        .solution-text {
            color: #555;
            line-height: 1.8;
            font-size: 16px;
        }

        .solution-list {
            list-style: none;
            padding: 0;
        }

        .solution-list li {
            padding: 10px 0;
            padding-left: 30px;
            position: relative;
            color: #555;
        }

        .solution-list li:before {
            content: "✓";
            position: absolute;
            left: 0;
            color: #667eea;
            font-weight: bold;
            font-size: 18px;
        }

        .history-item {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 15px;
            border-left: 4px solid #667eea;
        }

        .history-date {
            font-size: 14px;
            color: #999;
            margin-bottom: 5px;
        }

        .history-result {
            font-size: 18px;
            color: #333;
            font-weight: 600;
        }

        .hidden {
            display: none;
        }

        .progress-bar {
            width: 100%;
            height: 10px;
            background: #e0e0e0;
            border-radius: 10px;
            overflow: hidden;
            margin-bottom: 30px;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(135deg, #667eea, #764ba2);
            transition: width 0.3s ease;
        }

        @media (max-width: 768px) {
            .container {
                padding: 25px;
            }
            
            h1 {
                font-size: 24px;
            }
            
            .mascot-img {
                font-size: 80px;
            }
        }
    </style>
</head>
<body>
    <!-- Halaman 1: Login/Register -->
    <div id="page-login" class="container">
        <div class="logo-header">
            <div class="logo-text">🧠 MindCare</div>
        </div>
        <div class="tagline">Jaga Kesehatan Mental Anda Bersama Kami</div>
        
        <div style="margin-top: 40px;">
            <h1>Selamat Datang</h1>
            <h2>Silakan login atau daftar untuk melanjutkan</h2>
            
            <div class="form-group">
                <label>Username</label>
                <input type="text" id="username" placeholder="Masukkan username">
            </div>
            
            <div class="form-group">
                <label>Password</label>
                <input type="password" id="password" placeholder="Masukkan password">
            </div>
            
            <button class="btn btn-primary" onclick="handleLogin()">Login</button>
            <button class="btn btn-secondary" onclick="handleRegister()">Daftar Akun Baru</button>
        </div>
    </div>

    <!-- Halaman 2: Dashboard -->
    <div id="page-dashboard" class="container hidden">
        <div class="hamburger" onclick="toggleMenu()">
            <div></div>
            <div></div>
            <div></div>
        </div>
        
        <div class="menu-dropdown" id="menuDropdown">
            <div class="menu-item" onclick="showHistory()">📊 Histori</div>
            <div class="menu-item" onclick="changeAccount()">🔄 Ganti Akun</div>
            <div class="menu-item" onclick="logout()">🚪 Keluar Akun</div>
        </div>
        
        <div class="logo-header">
            <div class="logo-text">🧠 MindCare</div>
        </div>
        <div class="tagline">Jaga Kesehatan Mental Anda Bersama Kami</div>
        
        <div class="mascot">
            <div class="mascot-img">🌟😊🌈</div>
        </div>
        
        <div style="text-align: center;">
            <div class="welcome-text">Halo, <span id="userName"></span>!</div>
            <p style="color: #666; margin-bottom: 30px;">Kami di sini untuk membantu Anda memahami kesehatan mental Anda</p>
            
            <button class="btn btn-primary" onclick="goToIntro()">Lakukan Pemeriksaan Mental</button>
        </div>
    </div>

    <!-- Halaman 3: Intro Pemeriksaan -->
    <div id="page-intro" class="container hidden">
        <div class="logo-header">
            <div class="logo-text">🧠 MindCare</div>
        </div>
        
        <div style="text-align: center; margin-top: 40px;">
            <div class="mascot-img" style="font-size: 100px;">🎯</div>
            
            <h1 style="margin-top: 30px;">Pemeriksaan Kesehatan Mental</h1>
            <h2>Jawab 10 pertanyaan sederhana untuk mengetahui kondisi kesehatan mental Anda</h2>
            
            <div style="background: #f8f9fa; padding: 25px; border-radius: 15px; margin: 30px 0; text-align: left;">
                <h3 style="color: #333; margin-bottom: 15px;">📋 Yang Perlu Anda Ketahui:</h3>
                <ul style="color: #555; line-height: 2;">
                    <li>Tes ini terdiri dari 10 pertanyaan</li>
                    <li>Setiap pertanyaan memiliki jawaban Ya atau Tidak</li>
                    <li>Jawablah dengan jujur sesuai kondisi Anda</li>
                    <li>Hasil akan memberikan gambaran kesehatan mental Anda</li>
                    <li>Tes ini memakan waktu sekitar 2-3 menit</li>
                </ul>
            </div>
            
            <button class="btn btn-primary" onclick="startTest()">Mulai Pemeriksaan</button>
            <button class="btn btn-secondary" onclick="backToDashboard()">Kembali</button>
        </div>
    </div>

    <!-- Halaman 4: Pertanyaan -->
    <div id="page-questions" class="container hidden">
        <div class="logo-header">
            <div class="logo-text">🧠 MindCare</div>
        </div>
        
        <h1>Pemeriksaan Kesehatan Mental</h1>
        <h2>Silakan jawab pertanyaan berikut dengan jujur</h2>
        
        <div class="progress-bar">
            <div class="progress-fill" id="progressBar" style="width: 0%"></div>
        </div>
        
        <div id="questionsContainer"></div>
        
        <button class="btn btn-primary" onclick="submitAnswers()">Lihat Hasil</button>
        <button class="btn btn-secondary" onclick="backToIntro()">Kembali</button>
    </div>

    <!-- Halaman 5: Hasil -->
    <div id="page-results" class="container hidden">
        <div class="logo-header">
            <div class="logo-text">🧠 MindCare</div>
        </div>
        
        <div class="result-card">
            <div class="result-title" id="resultTitle"></div>
            <div class="result-subtitle" id="resultSubtitle"></div>
        </div>
        
        <div class="chart-container">
            <canvas id="resultChart"></canvas>
        </div>
        
        <div class="solution-box">
            <div class="solution-title">💡 Rekomendasi untuk Anda</div>
            <div class="solution-text" id="solutionText"></div>
            <ul class="solution-list" id="solutionList"></ul>
        </div>
        
        <button class="btn btn-primary" style="margin-top: 30px;" onclick="backToDashboard()">Kembali ke Dashboard</button>
    </div>

    <!-- Halaman Histori -->
    <div id="page-history" class="container hidden">
        <div class="logo-header">
            <div class="logo-text">🧠 MindCare</div>
        </div>
        
        <h1>📊 Histori Pemeriksaan</h1>
        <h2>Riwayat hasil pemeriksaan kesehatan mental Anda</h2>
        
        <div id="historyContainer"></div>
        
        <button class="btn btn-primary" onclick="backToDashboard()">Kembali ke Dashboard</button>
    </div>

    <script>
        const questions = [
            "Apakah Anda sering merasa sedih atau murung tanpa alasan yang jelas?",
            "Apakah Anda mengalami kesulitan tidur atau tidur berlebihan?",
            "Apakah Anda kehilangan minat pada aktivitas yang dulu Anda nikmati?",
            "Apakah Anda sering merasa lelah atau kehilangan energi?",
            "Apakah Anda mengalami perubahan nafsu makan yang signifikan?",
            "Apakah Anda sering merasa cemas atau khawatir berlebihan?",
            "Apakah Anda kesulitan berkonsentrasi atau membuat keputusan?",
            "Apakah Anda merasa tidak berharga atau bersalah secara berlebihan?",
            "Apakah Anda mengalami gejala fisik seperti sakit kepala atau perut tanpa sebab medis?",
            "Apakah Anda menarik diri dari interaksi sosial atau hubungan dengan orang lain?"
        ];

        let currentUser = null;
        let answers = {};
        let users = {};
        let userHistory = {};

        function handleLogin() {
            const username = document.getElementById('username').value.trim();
            const password = document.getElementById('password').value;
            
            if (!username || !password) {
                alert('Mohon isi username dan password!');
                return;
            }
            
            if (!users[username]) {
                alert('Username tidak ditemukan! Silakan daftar terlebih dahulu.');
                return;
            }
            
            if (users[username] !== password) {
                alert('Password salah!');
                return;
            }
            
            currentUser = username;
            showDashboard();
        }

        function handleRegister() {
            const username = document.getElementById('username').value.trim();
            const password = document.getElementById('password').value;
            
            if (!username || !password) {
                alert('Mohon isi username dan password!');
                return;
            }
            
            if (users[username]) {
                alert('Username sudah terdaftar! Silakan gunakan username lain atau login.');
                return;
            }
            
            users[username] = password;
            userHistory[username] = [];
            currentUser = username;
            alert('Pendaftaran berhasil! Anda akan otomatis login.');
            showDashboard();
        }

        function showDashboard() {
            document.getElementById('page-login').classList.add('hidden');
            document.getElementById('page-dashboard').classList.remove('hidden');
            document.getElementById('userName').textContent = currentUser;
        }

        function toggleMenu() {
            document.getElementById('menuDropdown').classList.toggle('active');
        }

        function changeAccount() {
            currentUser = null;
            document.getElementById('username').value = '';
            document.getElementById('password').value = '';
            document.getElementById('page-dashboard').classList.add('hidden');
            document.getElementById('page-login').classList.remove('hidden');
            document.getElementById('menuDropdown').classList.remove('active');
        }

        function logout() {
            changeAccount();
        }

        function goToIntro() {
            document.getElementById('page-dashboard').classList.add('hidden');
            document.getElementById('page-intro').classList.remove('hidden');
        }

        function startTest() {
            document.getElementById('page-intro').classList.add('hidden');
            document.getElementById('page-questions').classList.remove('hidden');
            renderQuestions();
        }

        function renderQuestions() {
            const container = document.getElementById('questionsContainer');
            container.innerHTML = '';
            answers = {};
            
            questions.forEach((q, idx) => {
                const qDiv = document.createElement('div');
                qDiv.className = 'question-container';
                qDiv.innerHTML = `
                    <div class="question-text">${idx + 1}. ${q}</div>
                    <div class="radio-group">
                        <label class="radio-label">
                            <input type="radio" name="q${idx}" value="ya" onchange="updateProgress()"> Ya
                        </label>
                        <label class="radio-label">
                            <input type="radio" name="q${idx}" value="tidak" onchange="updateProgress()"> Tidak
                        </label>
                    </div>
                `;
                container.appendChild(qDiv);
            });
        }

        function updateProgress() {
            let answered = 0;
            questions.forEach((q, idx) => {
                const selected = document.querySelector(`input[name="q${idx}"]:checked`);
                if (selected) {
                    answers[idx] = selected.value;
                    answered++;
                }
            });
            
            const progress = (answered / questions.length) * 100;
            document.getElementById('progressBar').style.width = progress + '%';
        }

        function submitAnswers() {
            if (Object.keys(answers).length < questions.length) {
                alert('Mohon jawab semua pertanyaan!');
                return;
            }
            
            const yesCount = Object.values(answers).filter(a => a === 'ya').length;
            const noCount = questions.length - yesCount;
            const yesPercentage = (yesCount / questions.length * 100).toFixed(1);
            const noPercentage = (noCount / questions.length * 100).toFixed(1);
            
            let resultTitle, resultSubtitle, solutionText, solutionItems;
            
            if (yesCount <= 3) {
                resultTitle = "✅ Kondisi Mental Baik";
                resultSubtitle = "Kesehatan mental Anda dalam kondisi yang baik";
                solutionText = "Anda memiliki kesehatan mental yang baik! Teruslah menjaga kondisi ini dengan:";
                solutionItems = [
                    "Pertahankan pola hidup sehat dan seimbang",
                    "Lanjutkan aktivitas yang Anda nikmati",
                    "Jaga hubungan sosial yang positif",
                    "Tetap berolahraga dan istirahat yang cukup",
                    "Lakukan hobi dan aktivitas yang menyenangkan"
                ];
            } else if (yesCount <= 6) {
                resultTitle = "⚠️ Perlu Perhatian";
                resultSubtitle = "Ada beberapa aspek yang perlu Anda perhatikan";
                solutionText = "Kesehatan mental Anda memerlukan perhatian. Beberapa langkah yang dapat Anda lakukan:";
                solutionItems = [
                    "Identifikasi sumber stres dan kelola dengan baik",
                    "Tingkatkan waktu istirahat dan tidur yang berkualitas",
                    "Berbagi perasaan dengan orang terdekat",
                    "Lakukan aktivitas relaksasi seperti meditasi",
                    "Pertimbangkan konsultasi dengan profesional",
                    "Kurangi beban kerja jika memungkinkan"
                ];
            } else {
                resultTitle = "🚨 Perlu Konsultasi";
                resultSubtitle = "Kami merekomendasikan untuk berkonsultasi dengan profesional";
                solutionText = "Hasil menunjukkan Anda mungkin mengalami beberapa gejala yang perlu ditangani. Sangat disarankan untuk:";
                solutionItems = [
                    "Segera berkonsultasi dengan psikolog atau psikiater",
                    "Jangan ragu untuk meminta bantuan profesional",
                    "Ceritakan kondisi Anda pada keluarga atau teman dekat",
                    "Hindari isolasi dan tetap terhubung dengan orang lain",
                    "Prioritaskan kesehatan mental Anda",
                    "Ikuti saran dan treatment dari profesional kesehatan mental"
                ];
            }
            
            // Simpan ke histori
            if (!userHistory[currentUser]) {
                userHistory[currentUser] = [];
            }
            
            userHistory[currentUser].push({
                date: new Date().toLocaleString('id-ID'),
                result: resultTitle,
                yesCount: yesCount,
                noCount: noCount
            });
            
            // Tampilkan hasil
            document.getElementById('page-questions').classList.add('hidden');
            document.getElementById('page-results').classList.remove('hidden');
            
            document.getElementById('resultTitle').textContent = resultTitle;
            document.getElementById('resultSubtitle').textContent = resultSubtitle;
            document.getElementById('solutionText').textContent = solutionText;
            
            const solutionList = document.getElementById('solutionList');
            solutionList.innerHTML = '';
            solutionItems.forEach(item => {
                const li = document.createElement('li');
                li.textContent = item;
                solutionList.appendChild(li);
            });
            
            // Buat chart
            const ctx = document.getElementById('resultChart').getContext('2d');
            new Chart(ctx, {
                type: 'pie',
                data: {
                    labels: [`Ya (${yesPercentage}%)`, `Tidak (${noPercentage}%)`],
                    datasets: [{
                        data: [yesCount, noCount],
                        backgroundColor: [
                            'rgba(118, 75, 162, 0.8)',
                            'rgba(102, 126, 234, 0.8)'
                        ],
                        borderColor: [
                            'rgba(118, 75, 162, 1)',
                            'rgba(102, 126, 234, 1)'
                        ],
                        borderWidth: 2
                    }]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                font: {
                                    size: 14
                                },
                                padding: 20
                            }
                        },
                        title: {
                            display: true,
                            text: 'Hasil Pemeriksaan Kesehatan Mental',
                            font: {
                                size: 18
                            }
                        }
                    }
                }
            });
        }

        function showHistory() {
            document.getElementById('menuDropdown').classList.remove('active');
            
            if (!userHistory[currentUser] || userHistory[currentUser].length === 0) {
                alert('Anda belum memiliki riwayat pemeriksaan.');
                return;
            }
            
            document.getElementById('page-dashboard').classList.add('hidden');
            document.getElementById('page-history').classList.remove('hidden');
            
            const container = document.getElementById('historyContainer');
            container.innerHTML = '';
            
            userHistory[currentUser].reverse().forEach(item => {
                const histDiv = document.createElement('div');
                histDiv.className = 'history-item';
                histDiv.innerHTML = `
                    <div class="history-date">${item.date}</div>
                    <div class="history-result">${item.result}</div>
                    <div style="color: #666; margin-top: 10px;">
                        Jawaban Ya: ${item.yesCount} | Jawaban Tidak: ${item.noCount}
                    </div>
                `;
                container.appendChild(histDiv);
            });
            
            userHistory[currentUser].reverse();
        }

        function backToDashboard() {
            ['page-intro', 'page-questions', 'page-results', 'page-history'].forEach(id => {
                document.getElementById(id).classList.add('hidden');
            });
            document.getElementById('page-dashboard').classList.remove('hidden');
        }

        function backToIntro() {
            document.getElementById('page-questions').classList.add('hidden');
            document.getElementById('page-intro').classList.remove('hidden');
        }

        // Close menu when clicking outside
        document.addEventListener('click', function(event) {
            const menu = document.getElementById('menuDropdown');
            const hamburger = document.querySelector('.hamburger');
            
            if (!hamburger.contains(event.target) && !menu.contains(event.target)) {
                menu.classList.remove('active');
            }
        });
    </script>
</body>
</html>
