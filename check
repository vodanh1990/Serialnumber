<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Tra Cứu Code</title>
  <script src="https://unpkg.com/html5-qrcode"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 20px;
    }
    input, button {
      font-size: 16px;
      padding: 8px;
      margin: 5px;
    }
    #result {
      margin-top: 15px;
      font-size: 18px;
      white-space: pre-line;
    }
    #reader {
      width: 320px;
      margin: 0 auto;
      display: none;
    }
    #micToggleBtn {
      font-size: 20px;
      padding: 10px;
    }
  </style>
</head>
<body>
  <h1>TRA CỨU SERIAL</h1>
  <input type="text" id="searchBox" placeholder="Nhập mã serial hoặc model...">
  <button onclick="searchSerial()">🔍 Tra cứu</button>
  <button id="micToggleBtn">🎤</button>
  <button onclick="toggleScanner()">📷 Quét mã</button>
  <div id="reader"></div>
  <div id="result"></div>

  <script>
    const data = {
      "2/KRJ90130/1": "WE37-A0 R0",
      "KRC161881/3": "4478 B12A(Pegasus)",
      "KRC161917/2": "4422 B41H(Shogun)",
      "KRC161970/2": "4417 B1 (Pammukale)",
      "KRC161971/1": "2212 B28F B68 (Baltic)",
      "KRE105299": "AIR 6449 B41K",
      "KRE105353": "AIR 3239 B40",
      "KRE105400": "AIR 3228 B38A B78R",
      "KRE105436": "AIR 6419 B42",
      "KRE10802": "AIR 3239 B78C",
      "KRE10809": "AIR 3227 B43",
      "KRE10810": "AIR 3227 B42",
      "KRE10812": "AIR 4435 B41",
      "KRE10813": "AIR 4435 B77D",
      "KRE10814": "AIR 6419 B40",
      "KRE10821": "AIR 6419 B77D",
      "KRF102456/1": "XE08-B1 R0",
      "KRF901143": "ME08-B1 R2",
      "KRF901330": "ME18-B7 R1",
      "KRF901331": "ME08-B3 R0",
      "KRF901350": "ME19-B2 R0",
      "KRF901354": "ME09-A0 R0",
      "KRF901366": "ME26-A1 R0",
      "KRF901376": "ME26-A4 R0",
      "KRF901377": "ME23-A1 R0",
      "KRF901409/1": "ME21-D2 R1",
      "KRF901414/3": "ME21-BG R0",
      "KRF901421": "ME21-A1 R1",
      "KRF901430/1": "ME21-B6 R0",
      "KRF901434/1": "ME37-A1 R0",
      "KRF901438": "ME08-B5 R1",
      "KRF901439": "ME07-B2 R1",
      "KRF901448": "ME08-B6 R0",
      "KRF901469/1": "ME09-D0 R0",
      "KRF901496": "XE38-A0 R1",
      "KRF901516/1": "ME35-A0 R0",
      "KRF901537": "ME21-BD R0",
      "KRF901543": "ME21-BB R0",
      "KRF901573": "XE36-A2 R1",
      "KRF901585": "ME39-A3 R1",
      "KRF901591": "ME22-B0 R0",
      "KRF901595": "ME07-A2 R0",
      "KRF901600": "ME26-B7 R0",
      "KRF901601": "ME26-B8 R0",
      "KRF901610": "ME07-B5 R0",
      "KRF901616": "XE35-A4 R0",
      "KRF901617": "ME07-A3 R0",
      "KRF901621": "ME21-BM R0",
      "KRF901651": "ME04-B3 R0",
      "KRF901655": "ME09-D2 R1",
      "KRF901660": "ME21-D6 R0",
      "KRF901663": "ME26-D4 R0",
      "KRF901668": "ME26-AB R0",
      "KRF901682": "ME35-B3 R0",
      "KRF901684": "ME07-C0 R0",
      "KRF901685": "ME08-C0 R0",
      "KRF901686": "ME21-BN R0",
      "KRF901689": "ME18-BF R0",
      "KRF901692": "ME18-BG R0",
      "KRF901693": "ME21-BP R0",
      "KRF901694": "ME21-BR R0",
      "KRF901699": "ME09-BB R0",
      "KRF901700": "ME21-BL R0",
      "KRF901702": "ME08-BE R0",
      "KRF901703": "XE26-A0/A1 R0",
      "KRF901712": "ME23-A6 R0",
      "KRF901715": "ME09-D3 R0",
      "KRF901722": "ME07-B7 R0",
      "KRF901725": "ME07-B8 R0",
      "KRF901828": "ME21-BA R0",
      "EP96-06540A": "FS08 AQR0",
      "EP96-06155A": "FS08 B9 R0",
      "EP96-04906A": "FS08-AH R2",
      "EP96-05228A": "FS08-AL R0",
      "EP96-06373A": "FS08-AP R0",
      "EP96-05023A": "FS08-B5 R3",
      "EP96-06394A": "FS09-A8 R0",
      "EP96-06394B": "FS09-A9 R0",
      "EP96-06542A": "FS09-AA R0",
      "EP96-04825A": "FS18-AN R0",
      "EP96-05924A": "FS18-B1 R0",
      "EP96-05565A": "FS21-AL R0",
      "EP96-06215A": "FS21-AQ R0",
      "EP96-06215C": "FS21-AQ R2",
      "EP96-05038A": "FS21-B3 R0",
      "EP96-06563A": "FS21-C6 R0",
      "EP96-06563B": "FS21-C7 R0",
      "EP96-05482A": "FS21-AK R1",
      "EP96-05302A": "FS23-A9 R1",
      "EP96-05735A": "FS23-A9 R2",
      "EP96-05735B": "FS23-A9 R3",
      "EP96-05735C": "FS23-A9 R4",
      "EP96-06601A": "FS23-AB R0",
      "EP96-06601B": "FS23-AC R0",
      "EP96-05770A": "FS25-D3 R0",
      "EP96-05521A": "MS23-B1 R1",
      "EP96-05528A": "FS26-AF R0",
      "EP96-05543A": "FS26-AG R0",
      "EP96-05509A": "FS26-B1 R1",
      "EP96-06015A": "FS26-D0 R0",
      "EP96-05281A": "FS34-D0 R0",
      "EP96-05282A": "FS35-D0 R0",
      "EP96-06439A": "FS35-D6 R0",
      "EP96-05419A": "FS37-A0 R1",
      "EP96-05244A": "FS21 AJ R0",
      "EP96-06421A": "FS07-B2R0",
      "EP96-05958A": "FS34-A0R0",
      "EP96-05797A": "FS36 D3R0"


    };

    function searchSerial() {
      const query = document.getElementById("searchBox").value.trim().toUpperCase();
      const resultDiv = document.getElementById("result");

      if (!query) {
        resultDiv.textContent = "Vui lòng nhập thông tin để tra cứu.";
        resultDiv.style.color = 'red';
        return;
      }

      if (query in data) {
        resultDiv.textContent = `🔸 ${query} → ${data[query]}`;
        resultDiv.style.color = 'black';
        return;
      }

      const foundSerials = Object.entries(data)
        .filter(([serial, model]) => serial.includes(query))
        .map(([serial, model]) => `🔸 ${serial} → ${model}`);

      const foundModels = Object.entries(data)
        .filter(([serial, model]) => model.includes(query))
        .map(([serial, model]) => `🔸 ${serial} → ${model}`);

      const results = [...foundSerials, ...foundModels];

      if (results.length > 0) {
        resultDiv.textContent = results.join('\n');
        resultDiv.style.color = 'black';
      } else {
        resultDiv.textContent = "Không tìm thấy kết quả phù hợp!";
        resultDiv.style.color = 'red';
      }
    }

    document.getElementById("searchBox").addEventListener("keypress", function(e) {
      if (e.key === "Enter") {
        searchSerial();
      }
    });

    // Giọng nói
    let recognition;
    let isListening = false;
    let finalTranscript = "";

    const micBtn = document.getElementById("micToggleBtn");
    const searchBox = document.getElementById("searchBox");
    const resultDiv = document.getElementById("result");

    function initRecognition() {
      const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
      if (!SpeechRecognition) {
        alert("Trình duyệt không hỗ trợ nhận diện giọng nói.");
        return null;
      }
      const recog = new SpeechRecognition();
      recog.lang = 'vi-VN';
      recog.continuous = true;
      recog.interimResults = true;
      return recog;
    }

    micBtn.addEventListener("click", () => {
      if (!isListening) {
        recognition = initRecognition();
        if (!recognition) return;

        finalTranscript = "";
        recognition.onstart = () => {
          resultDiv.textContent = "🎤 Đang lắng nghe...";
          resultDiv.style.color = "green";
        };

        recognition.onresult = (event) => {
          let interim = "";
          for (let i = event.resultIndex; i < event.results.length; i++) {
            const transcript = event.results[i][0].transcript;
            if (event.results[i].isFinal) {
              finalTranscript += transcript;
            } else {
              interim += transcript;
            }
          }
          const combined = (finalTranscript + interim).toUpperCase().replace(/\s/g, '');
          searchBox.value = combined;
          resultDiv.textContent = `🗣️ Nhận: ${combined}`;
          resultDiv.style.color = "blue";
        };

        recognition.onerror = (event) => {
          resultDiv.textContent = "Lỗi: " + event.error;
          resultDiv.style.color = "red";
        };

        recognition.onend = () => {
          if (isListening) {
            micBtn.textContent = "🎤";
            isListening = false;
            searchSerial();
          }
        };

        recognition.start();
        isListening = true;
        micBtn.textContent = "⏹️";
      } else {
        recognition.stop();
      }
    });

    // Quét mã QR
    let scannerOn = false;
    let html5Qrcode;

    function toggleScanner() {
      const reader = document.getElementById("reader");
      if (!scannerOn) {
        reader.style.display = "block";
        html5Qrcode = new Html5Qrcode("reader");

        Html5Qrcode.getCameras().then(cameras => {
          if (cameras && cameras.length) {
            const backCamera = cameras.find(cam => cam.label.toLowerCase().includes('back')) || cameras[0];
            html5Qrcode.start(
              { deviceId: { exact: backCamera.id } },
              {
                fps: 15,
                qrbox: { width: 250, height: 250 },
                aspectRatio: 1.333,
                disableFlip: true
              },
              qrCodeMessage => {
                html5Qrcode.stop();
                reader.style.display = "none";
                scannerOn = false;

                const result = qrCodeMessage.toUpperCase();
                document.getElementById("searchBox").value = result;
                resultDiv.textContent = `📦 Mã quét: ${result}`;
                resultDiv.style.color = "blue";
                searchSerial();
              },
              error => {
                // console.log("Lỗi quét: ", error);
              }
            );
            scannerOn = true;
          }
        }).catch(err => {
          alert("Không thể mở camera: " + err);
        });
      } else {
        html5Qrcode.stop();
        reader.style.display = "none";
        scannerOn = false;
      }
    }
  </script>
</body>
</html>
