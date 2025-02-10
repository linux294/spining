<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bahaya Judol</title>
    <style>
        body {
            text-align: center;
            font-family: Arial, sans-serif;
            background: linear-gradient(45deg, #1a1a2e, #16213e, #0f3460);
            color: white;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            overflow: hidden;
        }
        #slot-machine {
            font-size: 50px;
            margin-top: 20px;
            border: 5px solid white;
            padding: 20px;
            display: inline-block;
            background-color: #222;
            border-radius: 15px;
            box-shadow: 0px 0px 20px rgba(255, 255, 255, 0.2);
            transition: transform 0.3s;
        }
        #spin-button {
            margin-top: 20px;
            padding: 12px 25px;
            font-size: 22px;
            font-weight: bold;
            cursor: pointer;
            background: #ffcc00;
            border: none;
            border-radius: 10px;
            transition: 0.3s;
        }
        #spin-button:hover {
            background: #ffaa00;
            transform: scale(1.1);
        }
        #stop-message, #warning-message, #malware-message {
            display: none;
            font-size: 80px;
            color: red;
            margin-top: 20px;
            font-weight: bold;
            animation: blink 1s infinite;
        }
        @keyframes blink {
            0% { opacity: 1; }
            50% { opacity: 0; }
            100% { opacity: 1; }
        }
        .idiot-video {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 100vw;
            height: 100vh;
            object-fit: cover;
            z-index: 9999;
            display: none;
        }
        .prize-message {
            font-size: 40px;
            color: gold;
            font-weight: bold;
            margin-bottom: 10px;
        }
        .spam-message {
            font-size: 30px;
            color: red;
            font-weight: bold;
            margin-top: 10px;
            animation: blink 0.5s infinite;
        }
    </style>
</head>
<body>
    <div class="prize-message">🎁 HADIAH Rp 2.000,- 🎁</div>
    <div class="spam-message">SPAM TERUS!!!</div>
    <div id="slot-machine">🎰 🎰 🎰</div>
    <br>
    <button id="spin-button">Spin</button>
    <h2 id="stop-message">STOP JUDOL!!!</h2>
    <h2 id="malware-message">⚠️ Maaf, HP Anda terserang oleh malware! Segera hapus data dari website ini! ⚠️</h2>
    <h2 id="warning-message">⚠️⚠️⚠️</h2>
    
    <div id="video-container"></div>
    
    <audio id="spin-sound" src="pencet.mp3"></audio>
    <audio id="win-sound" src="muter.mp3"></audio>
    <audio id="lose-sound" src="kalah.mp3"></audio>
    
    <script>
        let spinCount = 0;
        document.getElementById("spin-button").addEventListener("click", function() {
            let slotMachine = document.getElementById("slot-machine");
            let spinSound = document.getElementById("spin-sound");
            let winSound = document.getElementById("win-sound");
            let loseSound = document.getElementById("lose-sound");
            let videoContainer = document.getElementById("video-container");
            let stopMessage = document.getElementById("stop-message");
            let malwareMessage = document.getElementById("malware-message");
            let warningMessage = document.getElementById("warning-message");
            let symbols = ['🍒', '🍊', '💎', '7️⃣', '🔔'];
            let result = [];
            
            spinSound.play();
            spinCount++;
            
            for (let i = 0; i < 3; i++) {
                let randomIndex = Math.floor(Math.random() * symbols.length);
                result.push(symbols[randomIndex]);
            }
            
            if (spinCount >= 30) {
                result = ['💎', '💎', '💎'];
            }
            
            slotMachine.innerText = result.join(" ");
            slotMachine.style.transform = "scale(1.2)";
            setTimeout(() => slotMachine.style.transform = "scale(1)", 300);
            
            if (result[0] === '💎' && result[1] === '💎' && result[2] === '💎') {
                stopMessage.style.display = "block";
                winSound.play();
                
                setTimeout(function() {
                    stopMessage.style.display = "none";
                    malwareMessage.style.display = "block";
                    setTimeout(function() {
                        malwareMessage.style.display = "none";
                        warningMessage.style.display = "block";
                        setTimeout(function() {
                            warningMessage.style.display = "none";
                            let video = document.createElement("video");
                            video.className = "idiot-video";
                            video.src = "idiot.mp4";
                            video.autoplay = true;
                            video.loop = true;
                            videoContainer.innerHTML = "";
                            videoContainer.appendChild(video);
                            video.style.display = "block";
                        }, 2000);
                    }, 3000);
                }, 2000);
            } else {
                loseSound.play();
            }
        });
    </script>
</body>
</html>
