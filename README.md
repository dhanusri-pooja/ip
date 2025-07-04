# IP Location Viewer

A simple  web app that lets users enter any IP address to find out its city and country using a public geolocation API.

## Live Demo

https://dhanusri-pooja.github.io/ip/


## Features

- Look up city and country by IP address
- Real-time fetch using the ipapi.co API
- Animated background with smooth gradients
- Floating glowing shapes using CSS animations
- Clean, minimal, and responsive design

## Technologies Used

- HTML5
- CSS3 (animations, layout, visual effects)
- JavaScript (async/await, Fetch API)



## API Reference

- [ipapi.co](https://ipapi.co/) - Public API for IP geolocation

## Code Used:

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>🌍 IP Location Viewer</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Comic Sans MS', cursive, sans-serif;
      min-height: 100vh;
      overflow: hidden;
      background: linear-gradient(120deg, #ffe1f0, #d1f3ff);
      background-size: 400% 400%;
      animation: gradient 25s ease infinite;
      display: flex;
      justify-content: center;
      align-items: center;
      position: relative;
    }

    @keyframes gradient {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    /* Floating, glowing animated shapes */
    .floating-shape {
      position: absolute;
      width: 50px;
      height: 50px;
      border-radius: 50%;
      background: rgba(255, 200, 255, 0.4);
      box-shadow: 0 0 20px rgba(255, 200, 255, 0.5);
      animation: floatXY 10s ease-in-out infinite;
    }

    .floating-shape.alt {
      background: rgba(200, 255, 255, 0.4);
      box-shadow: 0 0 20px rgba(200, 255, 255, 0.5);
      animation-duration: 12s;
    }

    @keyframes floatXY {
      0% { transform: translate(0, 0) scale(1); }
      50% { transform: translate(30px, -40px) scale(1.2); }
      100% { transform: translate(0, 0) scale(1); }
    }

    .card {
      position: relative;
      background: #ffffffee;
      border-radius: 20px;
      padding: 30px;
      box-shadow: 0 12px 24px rgba(0, 0, 0, 0.1);
      text-align: center;
      width: 90%;
      max-width: 400px;
      z-index: 10;
    }

    h1 {
      color: #000;
      font-size: 2em;
      margin-bottom: 20px;
    }

    input {
      padding: 12px;
      width: 80%;
      border: 2px solid #d1c4e9;
      border-radius: 10px;
      font-size: 1em;
      margin-bottom: 20px;
      color: #000;
    }

    button {
      padding: 12px 24px;
      border: none;
      border-radius: 20px;
      background: linear-gradient(90deg, #ff99cc, #99ccff);
      color: white;
      font-size: 1em;
      cursor: pointer;
      transition: all 0.3s ease;
    }

    button:hover {
      transform: scale(1.05);
      background: linear-gradient(90deg, #ff77aa, #77bbff);
    }

    .result {
      margin-top: 20px;
      font-size: 1.1em;
      background: #fafafa;
      padding: 15px;
      border-radius: 12px;
      box-shadow: 0 0 10px #f0eaff;
    }
  </style>
</head>
<body>

  <!-- Visible floating glowing shapes in px positions -->
  <div class="floating-shape" style="top: 40px; left: 60px;"></div>
  <div class="floating-shape alt" style="top: 150px; left: 90%;"></div>
  <div class="floating-shape" style="top: 500px; left: 30px;"></div>
  <div class="floating-shape alt" style="top: 400px; left: 70%;"></div>
  <div class="floating-shape" style="top: 300px; left: 150px;"></div>
  <div class="floating-shape alt" style="top: 80px; left: 250px;"></div>

  <div class="card">
    <h1>🌸 IP Location Lookup</h1>
    <input type="text" id="ipInput" placeholder="Enter an IP address..." />
    <br>
    <button id="lookupBtn">Find Location</button>
    <div id="result" class="result"></div>
  </div>

  <script>
    document.getElementById("lookupBtn").addEventListener("click", async function () {
      const ip = document.getElementById("ipInput").value.trim();
      const resultDiv = document.getElementById("result");

      if (!ip) {
        resultDiv.innerHTML = "⚠️ Please enter a valid IP address.";
        return;
      }

      resultDiv.innerHTML = "⏳ Fetching location...";

      try {
        const response = await fetch(`https://ipapi.co/${ip}/json/`);
        const data = await response.json();

        if (data.error || !data.city || !data.country_name) {
          resultDiv.innerHTML = "🚫 Could not fetch location. Try another IP.";
        } else {
          resultDiv.innerHTML = `
            📍 <b>City:</b> ${data.city}<br>
            🌐 <b>Country:</b> ${data.country_name}
          `;
        }
      } catch (error) {
        resultDiv.innerHTML = "❌ Something went wrong. Please try again.";
      }
    });
  </script>

</body>
</html>

```
