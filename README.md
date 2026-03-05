 index.html.
 <!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lacak Lokasi HP</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f2f5;
            margin: 0;
        }
        .container {
            background: white;
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            text-align: center;
            max-width: 300px;
            width: 100%;
        }
        h2 { color: #333; }
        button {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            margin-top: 10px;
            width: 100%;
        }
        button:hover { background-color: #0056b3; }
        #result {
            margin-top: 20px;
            font-size: 14px;
            color: #555;
            word-break: break-all;
        }
        .error { color: red; }
        .success { color: green; font-weight: bold; }
    </style>
</head>
<body>

    <div class="container">
        <h2>Lacak Lokasi</h2>
        <p>Klik tombol di bawah untuk melihat koordinat GPS Anda.</p>
        <button onclick="getLocation()">Lacak Sekarang</button>
        
        <div id="result"></div>
    </div>

    <script>
        const resultDiv = document.getElementById("result");

        function getLocation() {
            resultDiv.innerHTML = "Sedang mencari lokasi...";
            
            // Cek apakah browser mendukung Geolocation
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(showPosition, showError);
            } else {
                resultDiv.innerHTML = "Browser Anda tidak mendukung Geolocation.";
            }
        }

        function showPosition(position) {
            const latitude = position.coords.latitude;
            const longitude = position.coords.longitude;
            
            // Membuat link Google Maps
            const mapLink = `https://www.google.com/maps?q=${latitude},${longitude}`;

            resultDiv.innerHTML = `
                <p class="success">Lokasi Ditemukan!</p>
                <p><strong>Latitude:</strong> ${latitude}</p>
                <p><strong>Longitude:</strong> ${longitude}</p>
                <a href="${mapLink}" target="_blank" style="color:blue; text-decoration:underline;">Lihat di Google Maps</a>
            `;
        }

        function showError(error) {
            switch(error.code) {
                case error.PERMISSION_DENIED:
                    resultDiv.innerHTML = "Pengguna menolak permintaan lokasi.";
                    break;
                case error.POSITION_UNAVAILABLE:
                    resultDiv.innerHTML = "Informasi lokasi tidak tersedia.";
                    break;
                case error.TIMEOUT:
                    resultDiv.innerHTML = "Waktu permintaan lokasi habis.";
                    break;
                case error.UNKNOWN_ERROR:
                    resultDiv.innerHTML = "Terjadi kesalahan yang tidak diketahui.";
                    break;
            }
        }
    </script>

</body>
</html>
