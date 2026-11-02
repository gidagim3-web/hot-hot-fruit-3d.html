<!DOCTYPE html>
<html lang="am">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hot Hot Fruit 3D Slot - MelaBet</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            background-color: #0b141d;
            font-family: Arial, sans-serif;
            color: #fff;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            overflow: hidden;
        }

        h1 {
            color: #ff3366;
            text-shadow: 0 0 10px #ff3366, 0 0 20px #ff0044;
            margin-bottom: 10px;
        }

        #canvas-container {
            width: 340px;
            height: 380px;
            position: relative;
            box-shadow: 0 0 25px rgba(255, 51, 102, 0.4);
            border-radius: 15px;
            border: 3px solid #00ffcc;
            background: #050b11;
        }

        .controls {
            margin-top: 20px;
            display: flex;
            gap: 15px;
        }

        button {
            background: linear-gradient(135deg, #00ffcc, #0099ff);
            border: none;
            padding: 12px 30px;
            font-size: 18px;
            font-weight: bold;
            color: #000;
            border-radius: 25px;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(0, 255, 204, 0.4);
            transition: 0.2s;
        }

        button:active {
            transform: scale(0.95);
        }

        #result {
            margin-top: 15px;
            font-size: 18px;
            font-weight: bold;
            color: #00ffcc;
            height: 25px;
        }
    </style>
    <!-- Three.js 3D Library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
</head>
<body>

    <h1>🔥 Hot Hot Fruit 3D</h1>

    <div id="canvas-container"></div>
    <div id="result"></div>

    <div class="controls">
        <button id="spinBtn" onclick="spinReels()">SPIN 🎰</button>
    </div>

    <script>
        // Three.js 3D Scene Setup
        const container = document.getElementById('canvas-container');
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(45, container.clientWidth / container.clientHeight, 0.1, 1000);
        camera.position.z = 7;

        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(container.clientWidth, container.clientHeight);
        container.appendChild(renderer.domElement);

        // Lighting
        const ambientLight = new THREE.AmbientLight(0xffffff, 0.8);
        scene.add(ambientLight);

        const pointLight = new THREE.PointLight(0xff3366, 2, 10);
        pointLight.position.set(0, 0, 5);
        scene.add(pointLight);

        // Create 3D Cylinders for 3 Reels
        const reels = [];
        const reelCount = 3;
        const geometry = new THREE.CylinderGeometry(1.5, 1.5, 1.2, 16);

        // Colors representing Fruits (🍉, 🍋, 🍒, 7️⃣)
        const colors = [0xff0055, 0xffcc00, 0x00ffcc, 0xff9900, 0xcc00ff];

        for (let i = 0; i < reelCount; i++) {
            const material = new THREE.MeshPhongMaterial({
                color: colors[i % colors.length],
                wireframe: false,
                shininess: 100
            });
            const cylinder = new THREE.Mesh(geometry, material);
            cylinder.position.x = (i - 1) * 1.8;
            scene.add(cylinder);
            reels.push(cylinder);
        }

        // Animation Loop
        function animate() {
            requestAnimationFrame(animate);
            renderer.render(scene, camera);
        }
        animate();

        // Spin Logic
        let isSpinning = false;
        function spinReels() {
            if (isSpinning) return;
            isSpinning = true;
            document.getElementById('result').innerText = "እየተሽከረከረ ነው...";

            let spinsLeft = 30;
            const interval = setInterval(() => {
                reels.forEach(reel => {
                    reel.rotation.x += 0.4;
                    // Randomize color during spin for 3D flash effect
                    reel.material.color.setHex(colors[Math.floor(Math.random() * colors.length)]);
                });
                spinsLeft--;

                if (spinsLeft <= 0) {
                    clearInterval(interval);
                    isSpinning = false;
                    checkWin();
                }
            }, 50);
        }

        function checkWin() {
            const isWin = Math.random() > 0.4; // Win chance
            if (isWin) {
                document.getElementById('result').innerText = "🎉 አሸንፈዋል! 🎉";
            } else {
                document.getElementById('result').innerText = "❌ አልወጣም! እንደገና ይሞክሩ።";
            }
        }
    </script>
</body>
</html>
