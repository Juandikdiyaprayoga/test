<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🎂 Birthday Surprise</title>

    <style>
        /* ==================== STYLE DASAR ==================== */

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "Poppins", Arial, sans-serif;
        }

        body {
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            background:
                linear-gradient(
                    rgba(0, 0, 0, 0.35),
                    rgba(0, 0, 0, 0.65)
                ),
                url("https://images.unsplash.com/photo-1500534623283-312aade485b7?auto=format&fit=crop&w=1920&q=90");
            background-size: cover;
            background-position: center;
            transition: 0.5s;
        }

        .card {
            width: 90%;
            max-width: 520px;
            padding: 35px;
            text-align: center;
            color: white;
            background: rgba(255, 255, 255, 0.14);
            border: 1px solid rgba(255, 255, 255, 0.3);
            border-radius: 25px;
            backdrop-filter: blur(15px);
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.45);
            animation: muncul 1s ease;
        }

        @keyframes muncul {
            from {
                opacity: 0;
                transform: translateY(50px);
            }

            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .login-title {
            font-size: 38px;
            margin-bottom: 10px;
        }

        .subtitle {
            margin-bottom: 25px;
            line-height: 1.6;
        }

        input {
            width: 100%;
            padding: 14px;
            margin: 8px 0;
            border: none;
            outline: none;
            border-radius: 12px;
            text-align: center;
            font-size: 16px;
        }

        button {
            border: none;
            padding: 12px 17px;
            margin: 5px;
            border-radius: 12px;
            cursor: pointer;
            font-weight: bold;
            transition: 0.3s;
        }

        button:hover {
            transform: translateY(-3px) scale(1.04);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.35);
        }

        .login-button {
            width: 100%;
            margin-top: 15px;
            background: #ff4f81;
            color: white;
            font-size: 16px;
            font-weight: bold;
        }

        .login-button:hover {
            background: #ff2868;
        }

        #birthdayPage,
        #riddlePage,
        #secretPage {
            display: none;
        }

        .birthday-title {
            font-size: 42px;
            margin-bottom: 10px;
            animation: glow 2s infinite alternate;
        }

        @keyframes glow {
            from {
                text-shadow: 0 0 5px white;
            }

            to {
                text-shadow:
                    0 0 15px #ff69b4,
                    0 0 30px #ffd700,
                    0 0 50px white;
            }
        }

        #personName {
            font-size: 27px;
        }

        .message {
            margin: 20px 0;
            line-height: 1.8;
        }

        .gift {
            display: inline-block;
            font-size: 85px;
            cursor: pointer;
            transition: 0.5s;
        }

        .gift:hover {
            transform: scale(1.2) rotate(10deg);
        }

        #giftMessage {
            display: none;
            margin: 15px 0;
            font-weight: bold;
            animation: muncul 0.7s;
        }

        .buttons {
            margin-top: 15px;
        }

        #randomMessage {
            margin-top: 15px;
            font-size: 15px;
        }

        /* ==================== POPUP ==================== */

        .popup {
            position: fixed;
            inset: 0;
            display: none;
            justify-content: center;
            align-items: center;
            background: rgba(0, 0, 0, 0.75);
            z-index: 1000;
        }

        .popup-content {
            width: 85%;
            max-width: 400px;
            padding: 30px;
            background: white;
            color: #333;
            border-radius: 20px;
            text-align: center;
            animation: muncul 0.5s;
        }

        /* ==================== CONFETTI ==================== */

        .confetti {
            position: fixed;
            top: -20px;
            width: 10px;
            height: 10px;
            z-index: 999;
            animation: jatuh linear forwards;
        }

        @keyframes jatuh {
            to {
                transform: translateY(110vh) rotate(720deg);
            }
        }

        body.dark {
            filter: brightness(0.65);
        }

        /* ==================== RIDDLE ==================== */

        .riddle-card {
            background: rgba(20, 10, 20, 0.65);
        }

        .riddle-icon {
            font-size: 65px;
            margin-bottom: 10px;
        }

        .riddle-text {
            line-height: 1.8;
            margin: 20px 0;
            color: #ffe9f0;
        }

        .riddle-hint {
            font-size: 14px;
            opacity: 0.8;
            margin-top: 10px;
        }

        .riddle-error {
            color: #ffd0d8;
            min-height: 25px;
            margin-top: 10px;
        }

        .riddle-success {
            color: #baffd0;
            font-weight: bold;
        }

        /* ==================== HALAMAN SURAT ==================== */

        #secretPage {
            position: fixed;
            inset: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(
                circle at center,
                #fff7fa 0%,
                #f8dfe5 45%,
                #dca9b8 100%
            );
            overflow: hidden;
            z-index: 2000;
            align-items: center;
            justify-content: center;
            font-family: Georgia, serif;
        }

        .letter-wrapper {
            position: relative;
            width: 94%;
            max-width: 900px;
            height: 94vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        /* Amplop */

        .envelope {
            position: absolute;
            width: 430px;
            height: 280px;
            cursor: pointer;
            z-index: 20;
            transition: 1.5s ease;
        }

        .envelope-body {
            position: absolute;
            width: 100%;
            height: 100%;
            background: #fffaf5;
            border-radius: 8px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.2);
        }

        .envelope-flap {
            position: absolute;
            width: 100%;
            height: 100%;
            background: #f4d8dd;
            clip-path: polygon(0 0, 100% 0, 50% 60%);
            transform-origin: top;
            transition: 1.5s ease;
            z-index: 3;
        }

        .seal {
            position: absolute;
            z-index: 5;
            left: 50%;
            top: 55%;
            transform: translate(-50%, -50%);
            width: 60px;
            height: 60px;
            background: #b84c68;
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 25px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.25);
            transition: 0.5s;
        }

        .seal:hover {
            transform: translate(-50%, -50%) scale(1.15);
        }

        .envelope.open {
            opacity: 0;
            transform: scale(0.7) translateY(100px);
            pointer-events: none;
        }

        .envelope.open .envelope-flap {
            transform: rotateX(180deg);
        }

        /* Isi surat */

        .letter {
            position: absolute;
            width: 94%;
            max-width: 820px;
            height: 90vh;
            background: #fffdf8;
            border-radius: 8px;
            box-shadow: 0 25px 70px rgba(0, 0, 0, 0.25);
            opacity: 0;
            transform: translateY(100px) scale(0.8);
            transition:
                opacity 1.5s ease,
                transform 1.5s ease;
            overflow: auto;
        }

        .letter.show {
            opacity: 1;
            transform: translateY(0) scale(1);
        }

        .letter-content {
            padding: 45px 35px;
            text-align: center;
            color: #57333b;
        }

        .letter-title {
            font-size: 32px;
            margin-bottom: 25px;
            opacity: 0;
            animation: fadeDown 1.5s ease forwards;
            animation-delay: 1s;
        }

        /* Foto kenangan */

        .memory-container {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-bottom: 28px;
        }

        .memory {
            width: 160px;
            opacity: 0;
            transform: translateY(50px) rotate(-5deg);
            animation: memoryAppear 1s ease forwards;
        }

        .memory img {
            width: 100%;
            height: 130px;
            object-fit: cover;
            border: 8px solid white;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.18);
        }

        .memory span {
            display: block;
            margin-top: 8px;
            font-size: 13px;
            font-style: italic;
        }

        .memory1 {
            animation-delay: 2s;
        }

        .memory2 {
            transform: translateY(50px) rotate(5deg);
            animation-delay: 3s;
        }

        .memory3 {
            transform: translateY(50px) rotate(-3deg);
            animation-delay: 4s;
        }

        /* Pesan yang muncul bertahap */

        .main-message {
            margin-top: 15px;
            font-size: 18px;
            line-height: 1.8;
        }

        .line {
            display: block;
            opacity: 0;
            transform: translateY(15px);
            animation: textAppear 1.5s ease forwards;
        }

        .line1 {
            animation-delay: 5s;
        }

        .line2 {
            animation-delay: 6.2s;
        }

        .line3 {
            animation-delay: 7.4s;
        }

        .line4 {
            margin-top: 20px;
            font-size: 25px;
            font-weight: bold;
            color: #a33d5a;
            animation-delay: 8.8s;
        }

        .final-message {
            margin-top: 30px;
            font-size: 16px;
            line-height: 1.8;
            opacity: 0;
            animation: fadeIn 2s ease forwards;
            animation-delay: 10.5s;
        }

        /* Animasi surat dan teks */

        @keyframes fadeDown {
            from {
                opacity: 0;
                transform: translateY(-30px);
            }

            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes memoryAppear {
            from {
                opacity: 0;
                transform: translateY(50px) scale(0.7) rotate(-8deg);
            }

            to {
                opacity: 1;
                transform: translateY(0) scale(1) rotate(0);
            }
        }

        @keyframes textAppear {
            from {
                opacity: 0;
                transform: translateY(20px);
            }

            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }

            to {
                opacity: 1;
            }
        }

        /* Hati yang bergerak */

        .heart {
            position: absolute;
            bottom: -50px;
            font-size: 22px;
            opacity: 0.7;
            animation: heartFloat linear forwards;
            pointer-events: none;
        }

        @keyframes heartFloat {
            0% {
                transform: translateY(0) translateX(0) rotate(0);
                opacity: 0;
            }

            10% {
                opacity: 0.8;
            }

            50% {
                transform: translateY(-50vh) translateX(40px) rotate(20deg);
            }

            100% {
                transform: translateY(-110vh) translateX(-60px) rotate(-20deg);
                opacity: 0;
            }
        }

        @media (max-width: 600px) {
            .card {
                padding: 25px;
            }

            .birthday-title {
                font-size: 32px;
            }

            .login-title {
                font-size: 30px;
            }

            button {
                font-size: 13px;
            }

            .envelope {
                width: 300px;
                height: 200px;
            }

            .letter {
                width: 96%;
                height: 92vh;
            }

            .letter-content {
                padding: 30px 15px;
            }

            .letter-title {
                font-size: 25px;
            }

            .memory-container {
                gap: 7px;
            }

            .memory {
                width: 31%;
            }

            .memory img {
                height: 90px;
                border-width: 5px;
            }

            .main-message {
                font-size: 14px;
            }

            .line4 {
                font-size: 19px;
            }
        }
    </style>
</head>

<body>

    <div class="card" id="loginPage">
        <div class="login-title">🎂 Birthday Surprise 🎂</div>

        <p class="subtitle">
            Ada kejutan spesial untukmu! 💖<br><br>
            Masukkan nama dan password untuk membukanya.
        </p>

        <input
            type="text"
            id="nameInput"
            placeholder="👤 Masukkan nama..."
        >

        <input
            type="password"
            id="passwordInput"
            placeholder="🔐 Masukkan password..."
        >

        <button class="login-button" onclick="login()">
            🔓 Buka Kejutan
        </button>

        <p
            id="error"
            style="color: #ffd5d5; margin-top: 15px;"
        ></p>
    </div>

    <div class="card" id="birthdayPage">
        <div class="birthday-title">🎉 HAPPY BIRTHDAY 🎉</div>

        <h2 id="personName"></h2>

        <p class="message">
            🎂 Selamat ulang tahun!<br><br>
            Semoga hari spesial ini membawa banyak kebahagiaan,
            kesehatan, kesuksesan, dan pengalaman indah dalam hidupmu.<br><br>
            ✨ Semoga semua impianmu dapat tercapai. ✨
        </p>

        <div
            class="gift"
            onclick="openGift()"
            title="Klik hadiah"
        >
            🎁
        </div>

        <p id="giftMessage">
            ✨ SURPRISE! ✨<br>
            Semoga tahun ini menjadi tahun terbaikmu! 💖🎂
        </p>

        <div class="buttons">
            <button onclick="showMessage()">💌 special messsage</button>
            <button onclick="confetti()">🎊 Confetti</button>
            <button onclick="openRiddle()">🔐 Secret</button>
            <button onclick="changeMessage()">💖 message</button>
            <button onclick="darkMode()">🌙 Dark</button>
        </div>

        <p id="randomMessage"></p>
    </div>

    <!-- ==================== HALAMAN RIDDLE ==================== -->

    <div class="card riddle-card" id="riddlePage">
        <div class="riddle-icon">🔐🐱</div>

        <div
            class="birthday-title"
            style="font-size: 32px;"
        >
            SECRET RIDDLE
        </div>

        <p class="riddle-text">
            Ada seseorang yang sangat menyukai kucing. 🐱<br>
            Hari ulang tahunnya adalah <b>17 Maret</b>. 🎂<br><br>

            Orang ini pernah menjadi seseorang yang dekat,<br>
            namun waktu membuat semuanya berubah.<br><br>

            <strong>Siapakah nama orang tersebut?</strong>
        </p>

        <input
            type="text"
            id="riddleAnswer"
            placeholder="Tulis nama di sini..."
            onkeydown="if (event.key === 'Enter') checkRiddle()"
        >

        <button
            class="login-button"
            onclick="checkRiddle()"
        >
            💌 Buka Rahasia
        </button>

        <p
            id="riddleError"
            class="riddle-error"
        ></p>

        <div class="buttons">
            <button onclick="backToBirthday()">⬅️ Kembali</button>
        </div>
    </div>

    <!-- ==================== HALAMAN SURAT RAHASIA ==================== -->

    <div id="secretPage">
        <div class="letter-wrapper">

            <!-- Amplop -->

            <div class="envelope" id="envelope">
                <div class="envelope-flap"></div>
                <div class="envelope-body"></div>

                <div
                    class="seal"
                    onclick="openLetter()"
                >
                    ❤
                </div>
            </div>

            <!-- Isi surat -->

            <div class="letter" id="letter">
                <div class="letter-content">

                    <div class="letter-title">
                        Teruntuk Inka...
                    </div>

                    <div class="memory-container">

                        <div class="memory memory1">
                            <img
                                src="foto1.jpg"
                                alt="Kenangan 1"
                            >
                            <span>sebuah kenangan</span>
                        </div>

                        <div class="memory memory2">
                            <img
                                src="foto2.jpg"
                                alt="Kenangan 2"
                            >
                            <span>yang pernah berarti</span>
                        </div>

                        <div class="memory memory3">
                            <img
                                src="foto3.jpg"
                                alt="Kenangan 3"
                            >
                            <span>dan masih tersimpan</span>
                        </div>

                    </div>

                    <!-- Pesan yang muncul bertahap -->

                    <div class="main-message">
                        <span class="line line1">
                            Dulu kita dekat...
                        </span>

                        <span class="line line2">
                            banyak cerita yang pernah kita bagi.
                        </span>

                        <span class="line line3">
                            Waktu kemudian membawa kita ke jalan masing-masing.
                        </span>

                        <span class="line line4">
                            Dulu kita dekat, sekarang hanya saling tahu nama.
                        </span>
                    </div>

                    <!-- Pesan terakhir -->

                    <div class="final-message">
                        ✦ Beberapa orang mungkin hanya tinggal sebagai kenangan,<br>
                        tetapi kenangan itu tetap pernah menjadi bagian yang indah. ✦<br><br>
                        Selamat ulang tahun, Inka. 🎂
                    </div>

                    <div style="margin-top: 25px;">
                        <button onclick="closeSecret()">
                            ⬅️ Kembali
                        </button>
                    </div>

                </div>
            </div>

        </div>

        <div class="floating-hearts"></div>
    </div>

    <!-- ==================== POPUP PESAN SPESIAL ==================== -->

    <div class="popup" id="popup">
        <div class="popup-content">
            <h2>💌 Pesan Spesial</h2>

            <br>

            <p>
                Jangan lupa untuk selalu tersenyum dan menikmati
                setiap momen dalam hidup.<br><br>

                Teruslah mengejar impianmu dan jangan mudah menyerah.<br><br>

                🎂✨ Happy Birthday! ✨🎂
            </p>

            <br>

            <button onclick="closeMessage()">
                ❤️ Tutup
            </button>
        </div>
    </div>

    <script>
        // ==================== LOGIN ====================

        function login() {
            const name = document
                .getElementById("nameInput")
                .value
                .trim();

            const password = document
                .getElementById("passwordInput")
                .value;

            const error = document.getElementById("error");

            if (name === "") {
                error.innerHTML = "⚠️ Nama belum dimasukkan!";
                return;
            }

            if (password !== "1117") {
                error.innerHTML = "❌ Password salah!";
                return;
            }

            document.getElementById("loginPage").style.display = "none";
            document.getElementById("birthdayPage").style.display = "block";

            document.getElementById("personName").innerHTML =
                "✨ " + name + " ✨";

            confetti();
        }

        // ==================== HADIAH ====================

        function openGift() {
            document.getElementById("giftMessage").style.display = "block";
            confetti();
        }

        // ==================== POPUP PESAN ====================

        function showMessage() {
            document.getElementById("popup").style.display = "flex";
        }

        function closeMessage() {
            document.getElementById("popup").style.display = "none";
        }

        // ==================== CONFETTI ====================

        function confetti() {
            for (let i = 0; i < 100; i++) {
                const piece = document.createElement("div");

                piece.className = "confetti";
                piece.style.left = Math.random() * 100 + "vw";
                piece.style.background = randomColor();

                piece.style.animationDuration =
                    Math.random() * 3 + 2 + "s";

                piece.style.transform =
                    "rotate(" + Math.random() * 360 + "deg)";

                document.body.appendChild(piece);

                setTimeout(() => piece.remove(), 5000);
            }
        }

        function randomColor() {
            const colors = [
                "#ff4f81",
                "#ffd700",
                "#00ffff",
                "#7cff00",
                "#ff69b4",
                "#ffffff",
                "#9b59b6"
            ];

            return colors[
                Math.floor(Math.random() * colors.length)
            ];
        }

        // ==================== PESAN ACAK ====================

        function changeMessage() {
            const messages = [
                "🌟 Jangan pernah berhenti bermimpi!",
                "💖 Semoga selalu dikelilingi orang-orang baik!",
                "🎯 Terus kejar semua cita-citamu!",
                "✨ Jadilah versi terbaik dari dirimu!",
                "🎂 Semoga semakin sukses dan bahagia!",
                "🌈 Semoga tahun ini menjadi tahun terbaikmu!",
                "💫 Semoga semua harapan baikmu menjadi kenyataan!"
            ];

            document.getElementById("randomMessage").innerHTML =
                messages[
                    Math.floor(Math.random() * messages.length)
                ];
        }

        // ==================== MODE GELAP ====================

        function darkMode() {
            document.body.classList.toggle("dark");
        }

        // ==================== NAVIGASI RIDDLE ====================

        function openRiddle() {
            document.getElementById("birthdayPage").style.display = "none";
            document.getElementById("riddlePage").style.display = "block";

            document.getElementById("riddleAnswer").value = "";
            document.getElementById("riddleError").innerHTML = "";
        }

        function backToBirthday() {
            document.getElementById("riddlePage").style.display = "none";
            document.getElementById("birthdayPage").style.display = "block";
        }

        // ==================== JAWABAN RIDDLE ====================

        function checkRiddle() {
            const answer = document
                .getElementById("riddleAnswer")
                .value
                .trim()
                .toLowerCase();

            const message = document.getElementById("riddleError");

            if (answer === "inka ayu lestari") {
                message.className = "riddle-error riddle-success";
                message.innerHTML =
                    "✨ Jawaban benar... rahasianya terbuka. ✨";

                setTimeout(() => {
                    document.getElementById("riddlePage").style.display = "none";
                    document.getElementById("secretPage").style.display = "flex";

                    document.getElementById("envelope")
                        .classList.remove("open");

                    document.getElementById("letter")
                        .classList.remove("show");
                }, 1500);

            } else {
                message.className = "riddle-error";

                message.innerHTML =
                    "❌ Belum tepat. Coba ingat lagi petunjuknya...";
            }
        }

        // ==================== ANIMASI SURAT ====================

        function openLetter() {
            const envelope = document.getElementById("envelope");
            const letter = document.getElementById("letter");

            envelope.classList.add("open");

            setTimeout(() => {
                letter.classList.add("show");
                startHearts();
            }, 900);
        }

        // ==================== ANIMASI HATI ====================

        let heartTimer = null;

        function startHearts() {
            if (heartTimer) return;

            heartTimer = setInterval(() => {
                const heart = document.createElement("div");

                heart.className = "heart";

                heart.innerHTML = [
                    "❤",
                    "♡",
                    "♥",
                    "💗"
                ][Math.floor(Math.random() * 4)];

                heart.style.left = Math.random() * 100 + "%";

                heart.style.fontSize =
                    15 + Math.random() * 25 + "px";

                heart.style.animationDuration =
                    5 + Math.random() * 5 + "s";

                document
                    .querySelector(".floating-hearts")
                    .appendChild(heart);

                setTimeout(() => heart.remove(), 10000);
            }, 600);
        }

        // ==================== KEMBALI DARI SURAT ====================

        function closeSecret() {
            document.getElementById("secretPage").style.display = "none";
            document.getElementById("riddlePage").style.display = "block";

            document.getElementById("envelope")
                .classList.remove("open");

            document.getElementById("letter")
                .classList.remove("show");
        }
    </script>

</body>
</html>
