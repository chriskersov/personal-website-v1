---
title: Home
---

<style>
.profile-container {
  max-width: 30%;
  min-width: 120px;
  float: right;
  margin-top: 0.7em;
  position: relative;
  aspect-ratio: 1;
  cursor: pointer;
}

#depthCanvas {
  display: block;
  width: 100%;
  height: 100%;
  /* border-radius: 50%; */
}
</style>

<br>

<div class="profile-container" id="profileContainer">
  <canvas id="depthCanvas"></canvas>
</div>

<h1 style="font-size:3.5rem; margin:0 0 -0.2em;">Chris Kersov</h1>

<div style="margin-bottom:2.05em; color: #000000">
  /kr<span style="font-size: 0.95em; font-weight:100; font-variation-settings: 'wght' 50; -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;">ɪ</span>s ˈk<span style="font-size: 0.95em; font-weight:100; font-variation-settings: 'wght' 50; -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;">ɛə</span>rs<span style="font-size: 0.95em; font-weight:100; font-variation-settings: 'wght' 50; -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;">ɒ</span>v/

  <button class="pronounce-btn" id="pronounce-button" aria-label="Play pronunciation of Chris Kersov" title="Play pronunciation of Chris Kersov" onclick="pronounceName()">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true" focusable="false">
      <path d="M11 5L6 9H2v6h4l5 4V5z"/>
      <path d="M15.54 8.46a5 5 0 0 1 0 7.07"/>
    </svg>
  </button>

<audio id="pronounce-audio" src="Chris Kersov pronunciation.MP3" preload="none"></audio>

</div>

<script>
function pronounceName() {
  speechSynthesis.cancel();
  const utterance = new SpeechSynthesisUtterance('Chris Kairsov');
  utterance.lang = 'en-GB';
  utterance.rate = 0.5;    
  utterance.pitch = 1.0;
  utterance.volume = 1;
  utterance.onend = () => speechSynthesis.cancel();
  utterance.onerror = () => speechSynthesis.cancel();
  speechSynthesis.speak(utterance);
}

// Depth map effect
const canvas = document.getElementById('depthCanvas');
const ctx = canvas.getContext('2d');
const container = document.getElementById('profileContainer');

let originalImg, depthImg;
let targetMouseX = 0.5, targetMouseY = 0.5;
let currentMouseX = 0.5, currentMouseY = 0.5;
let animationFrame;

// REPLACE THESE WITH YOUR ACTUAL IMAGE PATHS
const originalSrc = 'Chris Kersov pfp.jpeg';
const depthSrc = 'Chris Kersov depth.png';

Promise.all([loadImage(originalSrc), loadImage(depthSrc)])
  .then(([orig, depth]) => {
    originalImg = orig;
    depthImg = depth;
    canvas.width = originalImg.width;
    canvas.height = originalImg.height;
    animate();
  });

function loadImage(src) {
  return new Promise((resolve, reject) => {
    const img = new Image();
    img.onload = () => resolve(img);
    img.onerror = reject;
    img.src = src;
  });
}

container.addEventListener('mousemove', (e) => {
  const rect = container.getBoundingClientRect();
  targetMouseX = (e.clientX - rect.left) / rect.width;
  targetMouseY = (e.clientY - rect.top) / rect.height;
});

container.addEventListener('mouseleave', () => {
  targetMouseX = 0.5;
  targetMouseY = 0.5;
});

function animate() {
  // Smooth interpolation (easing)
  const ease = 0.1;
  currentMouseX += (targetMouseX - currentMouseX) * ease;
  currentMouseY += (targetMouseY - currentMouseY) * ease;
  
  render();
  animationFrame = requestAnimationFrame(animate);
}

function render() {
  if (!originalImg || !depthImg) return;
  
  const width = canvas.width;
  const height = canvas.height;
  
  ctx.clearRect(0, 0, width, height);
  ctx.drawImage(originalImg, 0, 0, width, height);
  
  const imageData = ctx.getImageData(0, 0, width, height);
  const pixels = imageData.data;
  
  ctx.drawImage(depthImg, 0, 0, width, height);
  const depthData = ctx.getImageData(0, 0, width, height);
  const depthPixels = depthData.data;
  
  const maxDisplacement = 20;
  const offsetX = (currentMouseX - 0.5) * maxDisplacement;
  const offsetY = (currentMouseY - 0.5) * maxDisplacement;
  
  const newImageData = ctx.createImageData(width, height);
  const newPixels = newImageData.data;
  
  for (let y = 0; y < height; y++) {
    for (let x = 0; x < width; x++) {
      const i = (y * width + x) * 4;
      const depth = depthPixels[i] / 255;
      const displaceX = Math.round(offsetX * depth);
      const displaceY = Math.round(offsetY * depth);
      const srcX = Math.max(0, Math.min(width - 1, x - displaceX));
      const srcY = Math.max(0, Math.min(height - 1, y - displaceY));
      const srcI = (srcY * width + srcX) * 4;
      
      newPixels[i] = pixels[srcI];
      newPixels[i + 1] = pixels[srcI + 1];
      newPixels[i + 2] = pixels[srcI + 2];
      newPixels[i + 3] = pixels[srcI + 3];
    }
  }
  
  ctx.putImageData(newImageData, 0, 0);
}
</script>

<br>

### Data Science in E-Mobility at Shell <img src="Shell Recharge logo.png" alt="Shell Recharge logo" style="max-height:2.3em; display:inline-block; vertical-align:text-bottom; margin-left:-0.1em; margin-bottom: -0.4em" />

BSc (Hons) Computer Science and Artificial Intelligence at <a href="https://www.bath.ac.uk/" target="blank" style="color:#00478f; text-decoration:underline;">University of Bath</a>

<br>

I am in my third year of university studying CS + AI, maintaining a first-class honours, and currently on a placement year at Shell in Central London. I'm gaining invaluable industry experience in data science while pursuing my passion for leveraging technology to solve complex business problems.
