# Timer
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Timer Hitung Mundur 24 Jam</title>
    <style>
        /* CSS untuk Tampilan */
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: #f0f0f0;
            margin: 0;
            flex-direction: column;
        }
        .timer-container {
            background: #2c3e50;
            color: white;
            padding: 20px 40px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
            text-align: center;
        }
        #countdown {
            font-size: 3em;
            font-weight: bold;
            letter-spacing: 5px;
        }
        h1 {
            color: #333;
        }
    </style>
</head>
<body>

    <h1>⌛ Timer 24 Jam</h1>

    <div class="timer-container">
        <div id="countdown">24:00:00</div>
        <p>Jam:Menit:Detik</p>
    </div>

    <script>
        // --- JavaScript untuk Logika Hitung Mundur ---

        // 1. Definisikan total durasi dalam detik (24 jam * 60 menit * 60 detik)
        let totalSeconds = 24 * 60 * 60; 
        
        // Dapatkan elemen HTML tempat waktu akan ditampilkan
        const countdownElement = document.getElementById('countdown');

        function updateCountdown() {
            // Jika waktu habis, hentikan timer
            if (totalSeconds < 0) {
                clearInterval(timerInterval); // Hentikan fungsi berulang
                countdownElement.innerHTML = "WAKTU HABIS!";
                return; // Keluar dari fungsi
            }

            // Hitung Jam, Menit, dan Detik
            // Math.floor digunakan untuk mendapatkan bilangan bulat
            const hours = Math.floor(totalSeconds / 3600);
            const minutes = Math.floor((totalSeconds % 3600) / 60);
            const seconds = totalSeconds % 60;

            // Format waktu (pastikan selalu dua digit: 01, 05, 10, dll.)
            const formattedTime = 
                String(hours).padStart(2, '0') + ":" +
                String(minutes).padStart(2, '0') + ":" +
                String(seconds).padStart(2, '0');

            // Tampilkan waktu yang sudah diformat ke dalam elemen HTML
            countdownElement.innerHTML = formattedTime;

            // Kurangi total waktu tersisa sebanyak 1 detik
            totalSeconds--;
        }

        // Jalankan fungsi updateCountdown sekali agar tampilan awal benar
        updateCountdown();

        // Panggil fungsi updateCountdown setiap 1000 milidetik (1 detik)
        const timerInterval = setInterval(updateCountdown, 1000);

    </script>
</body>
</html>
