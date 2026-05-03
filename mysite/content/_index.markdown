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

<div style="margin:0 0 0em;">
  <h1 style="font-size:3.5rem; margin:0;">Chris Kersov</h1>
    <a href="/images/ChristopherKersovCV_UpReach%20(1).pdf" download aria-label="Download CV" title="Download CV" style="display:inline-flex; align-items:center; gap:0.55rem; margin-top:0.6rem; padding:0.45rem 0.75rem; border:2px solid #ccc; border-radius:0; background:#f4f4f4; color:#000; text-decoration:none; box-sizing:border-box; width:fit-content;">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.6" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true" focusable="false" style="width:1.05rem; height:1.05rem; color:#000; flex:none;">
      <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/>
      <path d="M7 10l5 5 5-5"/>
      <path d="M12 15V3"/>
    </svg>
    <span style="font-size:0.95rem; line-height:1; font-weight:bold;">Download CV</span>
  </a>
</div>

<!-- <div style="margin-bottom:2.05em; color: #000000">
  /kr<span style="font-size: 0.95em; font-weight:100; font-variation-settings: 'wght' 50; -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;">ɪ</span>s ˈk<span style="font-size: 0.95em; font-weight:100; font-variation-settings: 'wght' 50; -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;">ɛə</span>rs<span style="font-size: 0.95em; font-weight:100; font-variation-settings: 'wght' 50; -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;">ɒ</span>v/ -->

  <!-- <button class="pronounce-btn" id="pronounce-button" aria-label="Play pronunciation of Chris Kersov" title="Play pronunciation of Chris Kersov" onclick="pronounceName()">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true" focusable="false">
      <path d="M11 5L6 9H2v6h4l5 4V5z"/>
      <path d="M15.54 8.46a5 5 0 0 1 0 7.07"/>
    </svg>
  </button> -->

<!-- <audio id="pronounce-audio" src="Chris Kersov pronunciation.MP3" preload="none"></audio> -->

</div>

<script>
function updateLondonTime() {
  const now = new Date();
  const londonTime = new Date(now.toLocaleString('en-US', { timeZone: 'Europe/London' }));
  const timeString = londonTime.toLocaleTimeString('en-GB', { 
    hour: '2-digit', 
    minute: '2-digit',
    second: '2-digit'
  });
  const timeElement = document.getElementById('london-time');
  if (timeElement) {
    timeElement.textContent = timeString;
  }
}

// Update time immediately and then every second
updateLondonTime();
setInterval(updateLondonTime, 1000);

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

const originalSrc = '/images/Chris Kersov pfp.jpeg';
const depthSrc = '/images/Chris Kersov depth.png';

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

### Data Science in E-Mobility at Shell <img src="/images/Shell Recharge logo.png" alt="Shell Recharge logo" style="max-height:2.3em; display:inline-block; vertical-align:text-bottom; margin-left:-0.1em; margin-bottom: -0.4em" />

Final Year BSc (Hons) Computer Science and AI at the <a href="https://www.bath.ac.uk/" target="_blank" style="color:#00478f; text-decoration:underline;">University of Bath</a>

<br>

<div style="text-align:justify; text-justify:inter-word;">
I am in my third year studying Computer Science and Artificial Intelligence, maintaining a first‑class honours, and currently on a placement year at Shell in Central London. I am gaining invaluable industry experience in data science while pursuing my passion for leveraging technology to solve complex business problems.

Following my placement, I look forward to applying these industry insights to my final year and my dissertation. I am excited to return to an academic environment where I can continue tackling challenging, high-level topics. Looking further ahead, I am eager to pursue graduate opportunities for 2027, where I can continue delivering impact through data-driven innovation.

I'm passionate about building personal projects that combine my interests with technical skills. One project I'm currently working on is my <a href="/projects/#3ds-mpo-wobble-tool" style="color:black; text-decoration:underline;">3DS MPO Wobble Tool</a>, which converts Nintendo 3DS stereo MPO files into animated GIFs that preserve the depth effect in a web-friendly format. Check out my <a href="/projects/" style="color:black; text-decoration:underline;">projects page</a> for more.

<!-- This website explores various aspects of my life, from professional work and education to personal hobbies and interests, such as tennis, table tennis, speedsolving Rubik’s cubes, and travelling. -->

<br>

<div style="display: flex; justify-content: space-between; align-items: center; gap: 2rem;">
  <div style="line-height: 1.7; display: grid; gap: 0.45rem; color: #000;">
    <div>
      <strong>LinkedIn:</strong> <a href="https://www.linkedin.com/in/chriskersov/" target="_blank" rel="noreferrer" style="color:#000; text-decoration:underline;">linkedin.com/in/chriskersov</a>
    </div>
    <div>
      <strong>Email:</strong> <button id="copyEmailBtn" type="button" aria-label="Copy email address" title="Copy email address" style="background:none; border:0; padding:0; color:#000; text-decoration:underline; cursor:pointer; font:inherit;">chris@kersov.com</button> <span id="copyEmailFeedback" aria-hidden="true" style="margin-left:0.25em; color:#00A000; font-weight:bold;"></span>
    </div>
  </div>
  <div style="border: 2px solid #ccc; padding: 0.5rem 0.75rem; border-radius: 0; flex-shrink: 0; display: flex; align-items: center; gap: 0.35rem; background:#f4f4f4;">
    <div style="font-size: 1rem; color: #000; white-space: nowrap;">LDN</div>
    <div style="font-size: 1rem; font-weight: bold; font-variant-numeric: tabular-nums;" id="london-time"></div>
  </div>
</div>

<script>
(function(){
  const btn = document.getElementById('copyEmailBtn');
  const fb = document.getElementById('copyEmailFeedback');
  if (!btn) return;

  btn.addEventListener('click', async () => {
    const email = 'chris@kersov.com';
    try {
      await navigator.clipboard.writeText(email);
      fb.textContent = 'Copied!';
      setTimeout(() => fb.textContent = '', 3000);
    } catch (e) {
      window.prompt('Copy this email address', email);
    }
  });
})();

function updateLondonTime() {
  const now = new Date();
  const londonTime = new Date(now.toLocaleString('en-US', { timeZone: 'Europe/London' }));
  const timeString = londonTime.toLocaleTimeString('en-GB', {
    hour: '2-digit',
    minute: '2-digit',
    second: '2-digit'
  });
  const timeElement = document.getElementById('london-time');
  if (timeElement) {
    timeElement.textContent = timeString;
  }
}

updateLondonTime();
setInterval(updateLondonTime, 1000);
</script>

</div>
