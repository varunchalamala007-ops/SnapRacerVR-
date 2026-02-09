<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>👻 Snap Racer VR | Snapchat Game</title>
  <style>
    :root {
      --snap-yellow: #FFFC00;
      --snap-black: #000000;
      --snap-white: #FFFFFF;
      --neon-pink: #FF006E;
      --neon-blue: #00F5FF;
      --neon-purple: #8338EC;
      --neon-green: #3FFF00;
      --neon-orange: #FF9E00;
    }
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
      background: var(--snap-black);
      color: var(--snap-white);
      overflow: hidden;
      width: 100vw;
      height: 100vh;
      position: relative;
      -webkit-touch-callout: none;
      -webkit-user-select: none;
      user-select: none;
    }
    body::before {
      content: '';
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: radial-gradient(circle at 20% 50%, rgba(255, 0, 110, 0.15) 0%, transparent 50%), radial-gradient(circle at 80% 50%, rgba(131, 56, 236, 0.15) 0%, transparent 50%);
      animation: bgPulse 8s ease-in-out infinite;
      pointer-events: none;
    }
    @keyframes bgPulse {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.7; }
    }
    .screen {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      display: none;
      align-items: center;
      justify-content: center;
      opacity: 0;
      transition: opacity 0.5s;
      z-index: 1;
    }
    .screen.active {
      display: flex;
      opacity: 1;
    }
    .content {
      text-align: center;
      padding: 2rem;
      max-width: 600px;
      width: 100%;
      position: relative;
      z-index: 2;
    }
    .ghost-icon {
      font-size: 5rem;
      margin-bottom: 1rem;
      filter: drop-shadow(0 0 20px var(--snap-yellow));
      animation: float 3s ease-in-out infinite;
    }
    @keyframes float {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-10px); }
    }
    .title {
      font-size: 4rem;
      font-weight: 900;
      letter-spacing: 0.1em;
      background: linear-gradient(135deg, var(--neon-pink), var(--neon-purple), var(--neon-blue));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      margin-bottom: 0.5rem;
      animation: glow 2s ease-in-out infinite;
    }
    @keyframes glow {
      0%, 100% { filter: brightness(1); }
      50% { filter: brightness(1.3); }
    }
    .subtitle {
      font-size: 1.2rem;
      color: var(--neon-blue);
      text-transform: uppercase;
      letter-spacing: 0.3em;
      margin-bottom: 2rem;
    }
    .btn {
      padding: 1rem 3rem;
      font-size: 1.2rem;
      font-weight: 700;
      letter-spacing: 0.15em;
      border: none;
      border-radius: 50px;
      background: linear-gradient(135deg, var(--neon-pink), var(--neon-purple));
      color: var(--snap-white);
      cursor: pointer;
      box-shadow: 0 0 20px rgba(255, 0, 110, 0.6);
      transition: all 0.3s;
      margin: 1rem;
      text-transform: uppercase;
    }
    .btn:hover {
      transform: scale(1.05);
      box-shadow: 0 0 30px rgba(255, 0, 110, 0.8);
    }
    .btn:active {
      transform: scale(0.98);
    }
    .btn.secondary {
      background: rgba(255, 255, 255, 0.1);
      border: 2px solid var(--neon-purple);
      box-shadow: none;
    }
    #game-canvas {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: linear-gradient(180deg, #000428 0%, #004e92 100%);
    }
    .hud {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      padding: 1rem;
      pointer-events: none;
      z-index: 10;
      display: flex;
      justify-content: space-between;
    }
    .hud-item {
      background: rgba(0, 0, 0, 0.7);
      backdrop-filter: blur(10px);
      padding: 0.5rem 1.5rem;
      border-radius: 15px;
      border: 2px solid var(--neon-pink);
      box-shadow: 0 0 15px rgba(255, 0, 110, 0.3);
    }
    .hud-label {
      font-size: 0.7rem;
      color: var(--neon-blue);
      display: block;
      font-weight: 600;
      letter-spacing: 0.1em;
    }
    .hud-value {
      font-size: 2rem;
      font-weight: 900;
      color: var(--snap-white);
      background: linear-gradient(90deg, var(--neon-orange), var(--neon-pink));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }
    .mobile-controls {
      position: absolute;
      bottom: 2rem;
      left: 0;
      right: 0;
      display: flex;
      justify-content: space-between;
      padding: 0 2rem;
      z-index: 100;
      pointer-events: none;
    }
    .control-btn {
      width: 70px;
      height: 70px;
      border-radius: 50%;
      border: 3px solid var(--neon-blue);
      background: rgba(0, 245, 255, 0.2);
      backdrop-filter: blur(10px);
      color: var(--snap-white);
      font-size: 2rem;
      cursor: pointer;
      box-shadow: 0 0 20px rgba(0, 245, 255, 0.4);
      pointer-events: auto;
      transition: all 0.2s;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .control-btn:active {
      transform: scale(0.9);
      background: rgba(0, 245, 255, 0.4);
      box-shadow: 0 0 30px rgba(0, 245, 255, 0.6);
    }
    .stats {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 1rem;
      margin: 2rem 0;
    }
    .stat-card {
      background: rgba(255, 255, 255, 0.05);
      padding: 1.5rem;
      border-radius: 15px;
      border: 2px solid rgba(131, 56, 236, 0.3);
      backdrop-filter: blur(10px);
      transition: all 0.3s;
    }
    .stat-card:hover {
      transform: translateY(-5px);
      border-color: var(--neon-purple);
      box-shadow: 0 0 20px rgba(131, 56, 236, 0.5);
    }
    .stat-icon {
      font-size: 2rem;
      display: block;
      margin-bottom: 0.5rem;
    }
    .stat-name {
      font-size: 0.8rem;
      color: rgba(255, 255, 255, 0.6);
      display: block;
      margin: 0.5rem 0;
      text-transform: uppercase;
      letter-spacing: 0.1em;
    }
    .stat-num {
      font-size: 1.8rem;
      font-weight: 900;
      color: var(--neon-green);
    }
    .instructions {
      margin-top: 2rem;
      font-size: 0.9rem;
      color: rgba(255, 255, 255, 0.5);
    }
    .instructions p {
      margin: 0.3rem 0;
    }
    @media (max-width: 768px) {
      .title { font-size: 3rem; }
      .ghost-icon { font-size: 4rem; }
      .hud { flex-direction: column; gap: 0.5rem; }
      .stats { grid-template-columns: 1fr; }
    }
    @media (min-width: 769px) {
      .mobile-controls { display: none; }
    }
  </style>
</head>
<body>
  <div id="start-screen" class="screen active">
    <div class="content">
      <div class="ghost-icon">👻</div>
      <h1 class="title">SNAP RACER</h1>
      <p class="subtitle">VR Edition</p>
      <button id="start-btn" class="btn">Start Racing</button>
      <div class="instructions">
        <p>🎮 Desktop: Arrow Keys or A/D</p>
        <p>📱 Mobile: Tap Left/Right</p>
      </div>
    </div>
  </div>

  <div id="game-screen" class="screen">
    <canvas id="game-canvas"></canvas>
    <div class="hud">
      <div class="hud-item">
        <span class="hud-label">SCORE</span>
        <span class="hud-value" id="score">0</span>
      </div>
      <div class="hud-item">
        <span class="hud-label">SPEED</span>
        <span class="hud-value" id="speed">0</span>
      </div>
    </div>
    <div class="mobile-controls">
      <button class="control-btn" id="left-btn">◀</button>
      <button class="control-btn" id="right-btn">▶</button>
    </div>
  </div>

  <div id="gameover-screen" class="screen">
    <div class="content">
      <h2 class="title">RACE OVER!</h2>
      <p class="subtitle">Final Score: <span id="final-score">0</span></p>
      <div class="stats">
        <div class="stat-card">
          <span class="stat-icon">🏆</span>
          <span class="stat-name">High Score</span>
          <span class="stat-num" id="high-score">0</span>
        </div>
        <div class="stat-card">
          <span class="stat-icon">📏</span>
          <span class="stat-name">Distance</span>
          <span class="stat-num" id="distance">0m</span>
        </div>
        <div class="stat-card">
          <span class="stat-icon">⚡</span>
          <span class="stat-name">Max Speed</span>
          <span class="stat-num" id="max-speed">0</span>
        </div>
        <div class="stat-card">
          <span class="stat-icon">🎯</span>
          <span class="stat-name">Total Runs</span>
          <span class="stat-num" id="total-runs">0</span>
        </div>
      </div>
      <button id="restart-btn" class="btn">Play Again</button>
      <button id="menu-btn" class="btn secondary">Main Menu</button>
    </div>
  </div>

  <script type="importmap">
  {
    "imports": {
      "three": "https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js"
    }
  }
  </script>

  <script type="module">
    import * as THREE from 'three';

    class SnapRacerGame {
      constructor() {
        this.canvas = document.getElementById('game-canvas');
        this.isPlaying = false;
        this.score = 0;
        this.distance = 0;
        this.speed = 0.05;
        this.baseSpeed = 0.05;
        this.maxSpeed = 0.3;
        this.speedIncrement = 0.0005;
        this.currentLane = 1;
        this.playerX = 0;
        this.targetX = 0;
        this.obstacles = [];
        this.roadSegments = [];
        this.barriers = [];
        this.laneWidth = 2.67;
        this.init();
      }

      init() {
        this.scene = new THREE.Scene();
        this.scene.fog = new THREE.FogExp2(0x000428, 0.015);
        
        this.camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        this.camera.position.set(0, 2.5, 5);
        this.camera.lookAt(0, 0, -10);
        
        this.renderer = new THREE.WebGLRenderer({ canvas: this.canvas, antialias: true });
        this.renderer.setSize(window.innerWidth, window.innerHeight);
        this.renderer.setPixelRatio(window.devicePixelRatio);
        
        const ambient = new THREE.AmbientLight(0xffffff, 0.4);
        this.scene.add(ambient);
        
        const dirLight = new THREE.DirectionalLight(0xffffff, 0.6);
        dirLight.position.set(0, 10, 5);
        this.scene.add(dirLight);
        
        const pinkLight = new THREE.PointLight(0xFF006E, 1.5, 15);
        pinkLight.position.set(-4, 1.5, 0);
        this.scene.add(pinkLight);
        
        const blueLight = new THREE.PointLight(0x00F5FF, 1.5, 15);
        blueLight.position.set(4, 1.5, 0);
        this.scene.add(blueLight);
        
        this.createPlayer();
        this.createRoad();
        this.createStars();
        this.createParticles();
        this.setupControls();
        
        window.addEventListener('resize', () => this.onResize());
        this.animate();
      }

      createPlayer() {
        const group = new THREE.Group();
        
        const body = new THREE.Mesh(
          new THREE.BoxGeometry(0.8, 0.4, 1.2),
          new THREE.MeshPhongMaterial({
            color: 0xFF006E,
            emissive: 0xFF006E,
            emissiveIntensity: 0.3,
            shininess: 100
          })
        );
        group.add(body);
        
        const cockpit = new THREE.Mesh(
          new THREE.SphereGeometry(0.35, 16, 16),
          new THREE.MeshPhongMaterial({
            color: 0x00F5FF,
            emissive: 0x00F5FF,
            emissiveIntensity: 0.5,
            transparent: true,
            opacity: 0.8
          })
        );
        cockpit.position.y = 0.25;
        cockpit.scale.set(1, 0.7, 1);
        group.add(cockpit);
        
        const engine = new THREE.Mesh(
          new THREE.CylinderGeometry(0.2, 0.3, 0.5, 8),
          new THREE.MeshPhongMaterial({
            color: 0x8338EC,
            emissive: 0x8338EC,
            emissiveIntensity: 1
          })
        );
        engine.position.set(0, -0.2, -0.7);
        engine.rotation.x = Math.PI / 2;
        group.add(engine);
        
        group.position.set(0, 0.4, 0);
        this.player = group;
        this.scene.add(group);
      }

      createRoad() {
        for (let i = 0; i < 30; i++) {
          const road = new THREE.Mesh(
            new THREE.PlaneGeometry(8, 10),
            new THREE.MeshPhongMaterial({ color: 0x1a1a1a, side: THREE.DoubleSide })
          );
          road.rotation.x = -Math.PI / 2;
          road.position.z = -i * 10;
          this.scene.add(road);
          this.roadSegments.push(road);
          
          const leftBarrier = new THREE.Mesh(
            new THREE.BoxGeometry(0.2, 0.8, 10),
            new THREE.MeshPhongMaterial({
              color: 0xFF006E,
              emissive: 0xFF006E,
              emissiveIntensity: 0.4
            })
          );
          leftBarrier.position.set(-4.1, 0.4, -i * 10);
          this.scene.add(leftBarrier);
          this.barriers.push(leftBarrier);
          
          const rightBarrier = new THREE.Mesh(
            new THREE.BoxGeometry(0.2, 0.8, 10),
            new THREE.MeshPhongMaterial({
              color: 0x00F5FF,
              emissive: 0x00F5FF,
              emissiveIntensity: 0.4
            })
          );
          rightBarrier.position.set(4.1, 0.4, -i * 10);
          this.scene.add(rightBarrier);
          this.barriers.push(rightBarrier);
        }
        
        const laneMarkers = [];
        for (let i = 0; i < 60; i++) {
          for (let lane = 1; lane < 3; lane++) {
            const marker = new THREE.Mesh(
              new THREE.BoxGeometry(0.1, 0.01, 1.5),
              new THREE.MeshBasicMaterial({ color: 0xFFFC00 })
            );
            marker.position.set(-4 + (lane * this.laneWidth), 0.02, -i * 5);
            this.scene.add(marker);
            laneMarkers.push(marker);
          }
        }
        this.laneMarkers = laneMarkers;
      }

      createStars() {
        const geometry = new THREE.BufferGeometry();
        const positions = new Float32Array(500 * 3);
        
        for (let i = 0; i < 500 * 3; i += 3) {
          positions[i] = (Math.random() - 0.5) * 100;
          positions[i + 1] = (Math.random() - 0.5) * 100;
          positions[i + 2] = -Math.random() * 300;
        }
        
        geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
        const material = new THREE.PointsMaterial({
          color: 0xffffff,
          size: 0.4,
          transparent: true,
          opacity: 0.8
        });
        
        this.stars = new THREE.Points(geometry, material);
        this.scene.add(this.stars);
      }

      createParticles() {
        const geometry = new THREE.BufferGeometry();
        const positions = new Float32Array(100 * 3);
        
        for (let i = 0; i < 100 * 3; i += 3) {
          positions[i] = (Math.random() - 0.5) * 10;
          positions[i + 1] = Math.random() * 2;
          positions[i + 2] = -Math.random() * 30;
        }
        
        geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
        const material = new THREE.PointsMaterial({
          color: 0x8338EC,
          size: 0.2,
          transparent: true,
          opacity: 0.6,
          blending: THREE.AdditiveBlending
        });
        
        this.particles = new THREE.Points(geometry, material);
        this.scene.add(this.particles);
      }

      spawnObstacle() {
        if (Math.random() < 0.015) {
          const lane = Math.floor(Math.random() * 3);
          const xPos = -4 + (lane * this.laneWidth) + this.laneWidth / 2;
          
          const colors = [0xFF006E, 0x8338EC, 0x00F5FF, 0x3FFF00];
          const color = colors[Math.floor(Math.random() * colors.length)];
          
          const obstacle = new THREE.Mesh(
            new THREE.BoxGeometry(1.2, 1.2, 1.2),
            new THREE.MeshPhongMaterial({
              color: color,
              emissive: color,
              emissiveIntensity: 0.5,
              shininess: 100
            })
          );
          
          obstacle.position.set(xPos, 0.6, -50);
          this.scene.add(obstacle);
          this.obstacles.push({ mesh: obstacle, lane: lane });
        }
      }

      setupControls() {
        document.addEventListener('keydown', (e) => {
          if (!this.isPlaying) return;
          if (e.key === 'ArrowLeft' || e.key === 'a' || e.key === 'A') this.changeLane(-1);
          else if (e.key === 'ArrowRight' || e.key === 'd' || e.key === 'D') this.changeLane(1);
        });
        
        document.getElementById('left-btn').addEventListener('click', () => {
          if (this.isPlaying) this.changeLane(-1);
        });
        document.getElementById('left-btn').addEventListener('touchstart', (e) => {
          e.preventDefault();
          if (this.isPlaying) this.changeLane(-1);
        });
        
        document.getElementById('right-btn').addEventListener('click', () => {
          if (this.isPlaying) this.changeLane(1);
        });
        document.getElementById('right-btn').addEventListener('touchstart', (e) => {
          e.preventDefault();
          if (this.isPlaying) this.changeLane(1);
        });
      }

      changeLane(dir) {
        const newLane = Math.max(0, Math.min(2, this.currentLane + dir));
        if (newLane !== this.currentLane) {
          this.currentLane = newLane;
          this.targetX = -4 + (this.currentLane * this.laneWidth) + this.laneWidth / 2;
        }
      }

      start() {
        this.isPlaying = true;
        this.score = 0;
        this.distance = 0;
        this.speed = this.baseSpeed;
        this.currentLane = 1;
        this.targetX = -4 + (this.currentLane * this.laneWidth) + this.laneWidth / 2;
        this.playerX = this.targetX;
        
        this.obstacles.forEach(obs => this.scene.remove(obs.mesh));
        this.obstacles = [];
        
        this.updateHUD();
      }

      stop() {
        this.isPlaying = false;
        
        const saveData = JSON.parse(localStorage.getItem('snapRacerData') || '{}');
        const highScore = saveData.highScore || 0;
        const totalRuns = (saveData.totalRuns || 0) + 1;
        
        const newHighScore = Math.max(highScore, Math.floor(this.score));
        
        localStorage.setItem('snapRacerData', JSON.stringify({
          highScore: newHighScore,
          totalRuns: totalRuns
        }));
        
        document.getElementById('final-score').textContent = Math.floor(this.score);
        document.getElementById('high-score').textContent = newHighScore;
        document.getElementById('distance').textContent = Math.floor(this.distance) + 'm';
        document.getElementById('max-speed').textContent = Math.floor(this.speed * 1000);
        document.getElementById('total-runs').textContent = totalRuns;
        
        showScreen('gameover');
      }

      updateHUD() {
        document.getElementById('score').textContent = Math.floor(this.score);
        document.getElementById('speed').textContent = Math.floor(this.speed * 1000);
      }

      checkCollisions() {
        for (const obs of this.obstacles) {
          const dx = Math.abs(obs.mesh.position.x - this.playerX);
          const dz = Math.abs(obs.mesh.position.z);
          if (dz < 1.5 && dx < 1.2) return true;
        }
        return false;
      }

      update() {
        if (!this.isPlaying) return;
        
        this.speed = Math.min(this.maxSpeed, this.speed + this.speedIncrement);
        this.score += this.speed * 10;
        this.distance += this.speed;
        
        this.playerX += (this.targetX - this.playerX) * 0.12;
        this.player.position.x = this.playerX;
        this.player.rotation.z = (this.targetX - this.playerX) * 0.4;
        this.player.rotation.x = Math.sin(Date.now() * 0.003) * 0.05;
        
        this.roadSegments.forEach(seg => {
          seg.position.z += this.speed;
          if (seg.position.z > 10) seg.position.z -= 300;
        });
        
        this.barriers.forEach(bar => {
          bar.position.z += this.speed;
          if (bar.position.z > 10) bar.position.z -= 300;
        });
        
        this.laneMarkers.forEach(marker => {
          marker.position.z += this.speed;
          if (marker.position.z > 10) marker.position.z -= 300;
        });
        
        const starPos = this.stars.geometry.attributes.position.array;
        for (let i = 0; i < starPos.length; i += 3) {
          starPos[i + 2] += this.speed * 2;
          if (starPos[i + 2] > 5) starPos[i + 2] -= 300;
        }
        this.stars.geometry.attributes.position.needsUpdate = true;
        
        const particlePos = this.particles.geometry.attributes.position.array;
        for (let i = 0; i < particlePos.length; i += 3) {
          particlePos[i + 2] += this.speed * 1.5;
          if (particlePos[i + 2] > 5) {
            particlePos[i] = (Math.random() - 0.5) * 10;
            particlePos[i + 1] = Math.random() * 2;
            particlePos[i + 2] = -30;
          }
        }
        this.particles.geometry.attributes.position.needsUpdate = true;
        
        this.spawnObstacle();
        
        for (let i = this.obstacles.length - 1; i >= 0; i--) {
          const obs = this.obstacles[i];
          obs.mesh.position.z += this.speed;
          obs.mesh.rotation.y += 0.03;
          obs.mesh.rotation.x += 0.02;
          
          if (obs.mesh.position.z > 5) {
            this.scene.remove(obs.mesh);
            this.obstacles.splice(i, 1);
          }
        }
        
        if (this.checkCollisions()) this.stop();
        this.updateHUD();
      }

      onResize() {
        this.camera.aspect = window.innerWidth / window.innerHeight;
        this.camera.updateProjectionMatrix();
        this.renderer.setSize(window.innerWidth, window.innerHeight);
      }

      animate() {
        requestAnimationFrame(() => this.animate());
        this.update();
        this.renderer.render(this.scene, this.camera);
      }
    }

    function showScreen(name) {
      document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
      document.getElementById(name + '-screen').classList.add('active');
    }

    const game = new SnapRacerGame();

    document.getElementById('start-btn').addEventListener('click', () => {
      showScreen('game');
      setTimeout(() => game.start(), 100);
    });

    document.getElementById('restart-btn').addEventListener('click', () => {
      showScreen('game');
      setTimeout(() => game.start(), 100);
    });

    document.getElementById('menu-btn').addEventListener('click', () => {
      showScreen('start');
    });
  </script>
</body>
</html>
