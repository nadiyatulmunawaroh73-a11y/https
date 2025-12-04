# Timer
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Timer Hitung Mundur yang Bisa Diatur</title>
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
            gap: 20px;
        }
        .timer-container {
            background: #2c3e50;
            color: white;
            padding: 20px 40px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
            text-align: center;
            min-width: 300px;
        }
        #countdown {
            font-size: 3.5em; /* Ukuran teks waktu yang lebih besar */
            font-weight: bold;
            letter-spacing: 5px;
            margin-bottom: 10px;
        }
        h1 {
            color: #333;
        }
        .controls {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            align-items: center;
        }
        .controls input {
            width: 50px;
            padding: 8px;
            text-align: center;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 1em;
        }
        .controls button {
            padding: 10px 15px;
            background-color: #27ae60;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            transition: background-color 0.3s;
        }
        .controls button:hover {
            background-color: #2ecc71;
        }
        .label {
            font-size: 0.8em;
            color: #555;
            text-align: center;
        }
    </style>
</head>
<body>

    <h1>⏱️ Atur Durasi Timer</h1>

    <div class="controls">
        <div style="display: flex; flex-direction: column;">
            <input type="number" id="inputHours" value="24" min="0" max="99">
            <span class="label">Jam</span>
        </div>
        
        <div style="display: flex; flex-direction: column;">
            <input type="number" id="inputMinutes" value="0" min="0" max="59">
            <span class="label">Menit</span>
        </div>
        
        <div style="display: flex; flex-direction: column;">
            <input type="number" id="inputSeconds" value="0" min="0" max="59">
            <span class="label">Detik</span>
        </div>
        
        <button onclick="startTimer()">Mulai Timer</button>
    </div>

    <div class="timer-container">
        <div id="countdown">00:00:00</div>
        <p id="statusMessage">Tekan "Mulai Timer" untuk memulai hitungan.</p>
    </div>

    <script>
        // --- JavaScript untuk Logika Timer ---
        let timerInterval; // Variabel untuk menyimpan interval timer
        let totalSeconds = 0; // Total waktu dalam detik
        
        const countdownElement = document.getElementById('countdown');
        const statusMessage = document.getElementById('statusMessage');

        function startTimer() {
            // 1. Hentikan timer yang sedang berjalan (jika ada)
            clearInterval(timerInterval); 

            // 2. Ambil nilai input dari pengguna
            const hours = parseInt(document.getElementById('inputHours').value) || 0;
            const minutes = parseInt(document.getElementById('inputMinutes').value) || 0;
            const seconds = parseInt(document.getElementById('inputSeconds').value) || 0;

            // 3. Hitung total detik dari input
            totalSeconds = (hours * 3600) + (minutes * 60) + seconds;

            if (totalSeconds <= 0) {
                alert("Durasi timer harus lebih dari 0 detik.");
                countdownElement.innerHTML = "00:00:00";
                statusMessage.innerHTML = "Timer tidak diatur.";
                return;
            }

            // 4. Perbarui status dan mulai hitungan
            statusMessage.innerHTML = `Timer berjalan selama ${hours}J ${minutes}M ${seconds}D.`;
            updateCountdown(); // Panggil sekali untuk tampilan awal
            
            // 5. Atur interval untuk menjalankan updateCountdown setiap 1 detik
            timerInterval = setInterval(updateCountdown, 1000);
        }

        function updateCountdown() {
            // Logika hitung mundur
            if (totalSeconds < 0) {
                clearInterval(timerInterval); // Hentikan timer
                countdownElement.innerHTML = "WAKTU HABIS!";
                statusMessage.innerHTML = "⏰ Timer Selesai!";
                return;
            }

            // Konversi totalSeconds menjadi format H:M:S
            const hours = Math.floor(totalSeconds / 3600);
            const minutes = Math.floor((totalSeconds % 3600) / 60);
            const seconds = totalSeconds % 60;

            // Format agar selalu dua digit (misal: 5 menjadi 05)
            const formattedTime = 
                String(hours).padStart(2, '0') + ":" +
                String(minutes).padStart(2, '0') + ":" +
                String(seconds).padStart(2, '0');

            // Perbarui tampilan di halaman web
            countdownElement.innerHTML = formattedTime;

            // Kurangi waktu
            totalSeconds--;
        }

        // Panggil fungsi startTimer() saat halaman dimuat untuk menampilkan nilai awal (24:00:00)
        startTimer(); 
    </script>
</body>
</html>
