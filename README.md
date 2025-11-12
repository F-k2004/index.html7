<!-- index.html -->
<!DOCTYPE html>
<html lang="fa">
<head>
  <meta charset="UTF-8">
  <itle>🌤️ وضعیت آب‌وهوا</title>
  <style>
    body {
      font-family: sans-serif;
      background: linear-gradient(135deg, #89f7fe, #66a6ff);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      text-align: center;
      color: #333;
      margin: 0;
    }
    h1 {
      margin-bottom: 20px;
      color: #fff;
      text-shadow: 0 2px 4px rgba(0,0,0,0.3);
    }
    input {
      padding: 10px;
      border: none;
      border-radius: 8px;
      width: 220px;
      text-align: center;
      font-size: 16px;
    }
    button {
      margin-top: 10px;
      padding: 10px 20px;
      border: none;
      border-radius: 8px;
      background: #333;
      color: #fff;
      cursor: pointer;
      transition: 0.3s;
    }
    button:hover {
      background: #555;
    }
    #weather {
      margin-top: 30px;
      background: rgba(255,255,255,0.85);
      padding: 25px;
      border-radius: 15px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.2);
      width: 300px;
    }
    #weather img {
      width: 80px;
      height: 80px;
    }
  </style>
</head>
<body>
  <h1>🌤️ وضعیت آب‌وهوا</h1>
  <input id="city" type="text" placeholder="نام شهر را وارد کنید">
  <button onclick="getWeather()">جستجو</button>
  <div id="weather">در انتظار انتخاب شهر...</div>

  <script>
    const apiKey = "YOUR_API_KEY"; // 🔑 کلید API خودت رو اینجا بذار

    async function getWeather() {
      const city = document.getElementById("city").value.trim();
      if (!city) {
        alert("لطفاً نام شهر را وارد کنید!");
        return;
      }

      try {
        const response = await fetch(
          `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric&lang=fa`
        );
        const data = await response.json();

        if (data.cod === "404") {
          document.getElementById("weather").innerHTML = "❌ شهر پیدا نشد.";
        } else {
          const icon = `https://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`;

          document.getElementById("weather").innerHTML = `
            <h2>${data.name}, ${data.sys.country}</h2>
            <img src="${icon}" alt="weather icon">
            <p>🌡️ دما: ${data.main.temp} °C</p>
            <p>💧 رطوبت: ${data.main.humidity}%</p>
            <p>🌥️ وضعیت: ${data.weather[0].description}</p>
          `;
        }
      } catch (error) {
        document.getElementById("weather").innerHTML = "⚠️ خطا در دریافت اطلاعات!";
      }
    }
  </script>
</body>
</html>
