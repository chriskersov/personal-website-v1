---
Title: Projects
---

<br>

<h1 style="font-size:3.5rem; margin:0 0 -0.2em;">Projects</h1>

This page showcases the personal projects I've built in my spare time. I always have so many ideas and I love being able to bring them to life. I'm always thinking about what to build next, or how to make something I've already built better.

<br>
 
<div style="display:grid; grid-template-columns:0.5fr 0.5fr; gap:3rem; align-items:start;">
    <div style="display:flex; flex-direction:column; gap:1rem;">
        <table style="width:100%; border: 2px solid #ccc; border-collapse: collapse; table-layout: fixed; box-sizing: border-box;">
            <tr>
                <td style="border: 1px solid #ccc; padding: 0.5rem 0.75rem; background: #f4f4f4; text-align: center;">
                    <strong>Contents</strong>
                </td>
            </tr>
            <tr>
                <td style="border: 1px solid #ccc; padding: 1rem 1.25rem; vertical-align: top; background: white;">
                  <ul style="margin: 0; padding-left: 0; list-style: none; text-align: center;">
                    <li><a href="#3ds-mpo-wobble-tool" style="color: black; text-decoration: none; display: inline-block;">3DS MPO Wobble Tool</a></li>
                    <li><a href="#" style="color: black; text-decoration: none; display: inline-block;">MPO Parser NPM Package</a></li>
                    <li><a href="#personal-finances-ai" style="color: black; text-decoration: none; display: inline-block;">Personal Finances AI</a></li>
                    <li><a href="#" style="color: black; text-decoration: none; display: inline-block;">Australian Open Predictor</a></li>
                    <li><a href="#" style="color: black; text-decoration: none; display: inline-block;">Roland Garros Predictor</a></li>
                    <li><a href="#" style="color: black; text-decoration: none; display: inline-block;">LLM Typing Test</a></li>
                    </ul>
                </td>
            </tr>
        </table>
    </div>
    <div style="display:flex; flex-direction:column; justify-content: flex-start;"> 
        <table style="width:100%; border: 2px solid #ccc; border-collapse: collapse; table-layout: fixed; box-sizing: border-box;">
            <tr>
                <td style="border: 1px solid #ccc; padding: 0.5rem 0.75rem; background: #f4f4f4; text-align: center;">
                    <strong>Github Contribution Graph</strong>
                </td>
            </tr>
            <tr>
                <td style="border: 1px solid #ccc; padding: 1rem; vertical-align: top; text-align: center; background: white;">
                    <div id="contrib-graph" style="width:100%;"></div>
                </td>
            </tr>
        </table>
    </div>
</div>

<script>
const USERNAME = "chriskersov";
const CONTRIBUTION_WEEKS = {{< github_contrib_weeks username="chriskersov" >}};

function getColor(count) {
  if (count === 0) return "#e8e8e8";
  if (count <= 2)  return "#aaaaaa";
  if (count <= 5)  return "#777777";
  if (count <= 9)  return "#444444";
  return "#111111";
}

function getColor(count) {
  if (count === 0) return "#ebedf0"; // GitHub empty cell
  if (count <= 2)  return "#9be9a8"; // GitHub Light Green
  if (count <= 5)  return "#40c463"; // GitHub Medium Green
  if (count <= 9)  return "#30a14e"; // GitHub Dark Green
  return "#216e39";                // GitHub Deepest Green
}

function renderGraph() {
  const allWeeks = CONTRIBUTION_WEEKS;
  const weeks = allWeeks.slice(-16);

  const container = document.getElementById("contrib-graph");
  
  // FIX: Clear the container before appending the new graph
  container.innerHTML = ""; 

  const cellSize = 10;
  const gap = 2;
  const cols = weeks.length;
  const rows = 7;
  const totalW = cols * (cellSize + gap) - gap;
  const totalH = rows * (cellSize + gap) - gap;

  const svg = document.createElementNS("http://www.w3.org/2000/svg", "svg");
  svg.setAttribute("viewBox", `0 0 ${totalW} ${totalH}`);
  svg.setAttribute("width", "100%"); 
  svg.style.display = "block";

  weeks.forEach((week, col) => {
    week.contributionDays.forEach((d, row) => {
      const rect = document.createElementNS("http://www.w3.org/2000/svg", "rect");
      rect.setAttribute("x", col * (cellSize + gap));
      rect.setAttribute("y", row * (cellSize + gap));
      rect.setAttribute("width", cellSize);
      rect.setAttribute("height", cellSize);
      rect.setAttribute("rx", 2);
      rect.setAttribute("fill", getColor(d.contributionCount));
      
      const title = document.createElementNS("http://www.w3.org/2000/svg", "title");
      title.textContent = `${d.date}: ${d.contributionCount} contribution${d.contributionCount !== 1 ? "s" : ""}`;
      rect.appendChild(title);
      svg.appendChild(rect);
    });
  });

  container.appendChild(svg);
}

renderGraph();
</script>

<br>

<!-- <hr style="border:none; border-top:1px solid #e0e0e0; margin:0 0 3.5rem;"> -->

<!-- ─── PROJECT 01 ─────────────────────────────────────────── -->

## 3DS MPO Wobble Tool

### <a href="https://3ds-wobble-gif.streamlit.app" target="_blank" style="color:black; text-decoration:underline;">Link</a>&nbsp;-----&nbsp;<a href="https://github.com/chriskersov/3DS-wobble-gif" target="_blank" style="color:black; text-decoration:underline;">GitHub</a>

<div style="display:flex; flex-wrap:wrap; gap:0.4rem; margin-bottom:1rem;">
  <span style="border:2px solid #ccc; padding:0.1rem 0.5rem; color: #888;">Streamlit</span>
  <span style="border:2px solid #ccc; padding:0.1rem 0.5rem; color: #888;">Pillow</span>
  <span style="border:2px solid #ccc; padding:0.1rem 0.5rem; color: #888;">NumPy</span>
  <span style="border:2px solid #ccc; padding:0.1rem 0.5rem; color: #888;">Streamlit Community Cloud</span>
</div>

<div style="display:grid; grid-template-columns:0.6fr 0.4fr; gap:3rem; align-items:start; margin-bottom:1.75rem;">

  <div>
 A web tool that converts Nintendo 3DS .mpo stereo image files into animated wobble GIFs. The 3DS captured true stereoscopic photos - two slightly offset images stored in a single file - but the format is almost universally unsupported outside the handheld itself. This tool extracts the stereo pair, aligns the frames using a pixel-difference score, and encodes them into a smoothly crossfaded, looping GIF that conveys the original depth and parallax allowing it to be viewable on any device with no special hardware required.
  </div>

<div style="width:100%; border: 2px solid #ccc; table-layout: fixed; box-sizing: border-box;">
  <div onclick="openLightbox(0)" style="position:relative; cursor:pointer; overflow:hidden; background: #000000; line-height:0;">
    <img src="/projects/screenshot1.png" alt="Project screenshot" style="width:100%; display:block; opacity:0.35;">
    <div style="position:absolute; inset:0; display:flex; flex-direction:column; align-items:center; justify-content:center; gap:8px; line-height:1.5;">
      <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="1.5" stroke-linecap="round">
        <rect x="3" y="3" width="7" height="7" rx="1"/><rect x="14" y="3" width="7" height="7" rx="1"/>
        <rect x="3" y="14" width="7" height="7" rx="1"/><rect x="14" y="14" width="7" height="7" rx="1"/>
      </svg>
      <span style="color:white;">7 photos</span>
    </div>
  </div>
  <div onclick="openLightbox(0)" style="cursor:pointer; text-align:center; padding:0.4rem 0; color:black; background:#f4f4f4; border-top:1px solid #ccc;"><strong>View Gallery</strong></div>
</div>
</div>

</div>

<table style="width:100%; border: 2px solid #ccc; border-collapse: collapse; table-layout: fixed; box-sizing: border-box;">
    <tr>
        <td style="width:33%; border: 1px solid #ccc; padding: 0.5rem 0.75rem; vertical-align: top; text-align: center; background: #f4f4f4;">
            <strong>README.md</strong>
        </td>
    </tr>
    <tr>
        <td style="border: 1px solid #ccc; padding: 0.5rem 0.75rem; vertical-align: top; background: white;">
            <a href="https://github.com/chriskersov/3DS-wobble-gif" target="_blank"  style="color:black; text-decoration:none;">
              <div id="readme-container" style="max-height:500px; overflow-y:scroll; scrollbar-width:none; -ms-overflow-style:none; padding:1rem 1.25rem; margin-top:0.5rem; box-sizing:border-box; width:100%;">
                <div id="readme-content" style="font-family:monospace; color:black; margin:0; word-break:break-word;">Loading README...</div>
              </div>
            </a>
        </td>
    </tr>
</table>

<!-- <hr style="border:none; border-top:1px solid #e0e0e0; margin:3.5rem 0;"> -->

<div id="lightbox" style="display:none; position:fixed; inset:0; background:rgba(0,0,0,0.85); z-index:1000; align-items:center; justify-content:center;">
  <button onclick="closeLightbox()" style="position:absolute; top:1.5rem; right:1.5rem; background:none; border:none; color:white; font-size:1.5rem; cursor:pointer;">✕</button>
  <button onclick="lightboxPrev()" style="position:absolute; left:1.5rem; background:none; border:none; color:white; font-size:2rem; cursor:pointer;">&#8592;</button>
  <img id="lightbox-img" src="" style="max-width:90vw; max-height:85vh; display:block; object-fit:contain;">
  <span id="lightbox-counter" style="position:absolute; bottom:1.5rem; left:50%; transform:translateX(-50%); color:white; font-size:0.8rem;"></span>
  <button onclick="lightboxNext()" style="position:absolute; right:1.5rem; background:none; border:none; color:white; font-size:2rem; cursor:pointer;">&#8594;</button>
</div>

<style>
  details[open] summary .arrow { display: none; }
  details:not([open]) summary .open-arrow { display: none; }
  /* details[open] #readme-container { max-height:none; } */

  #readme-container::-webkit-scrollbar {
    display: none;
  }
</style>

<script>
let lightboxIndex = 0;

function openLightbox(index) {
  lightboxIndex = index;
  const lb = document.getElementById("lightbox");
  lb.style.display = "flex";
  updateLightbox();
}

function closeLightbox() {
  document.getElementById("lightbox").style.display = "none";
}

function updateLightbox() {
  document.getElementById("lightbox-img").src = slides[lightboxIndex];
  document.getElementById("lightbox-counter").textContent = (lightboxIndex + 1) + " / " + slides.length;
}

function lightboxNext() { lightboxIndex = (lightboxIndex + 1) % slides.length; updateLightbox(); }
function lightboxPrev() { lightboxIndex = (lightboxIndex - 1 + slides.length) % slides.length; updateLightbox(); }

document.getElementById("lightbox").addEventListener("click", function(e) {
  if (e.target === this) closeLightbox();
});

document.addEventListener("keydown", function(e) {
  if (e.key === "Escape") {
    closeLightbox();
    closeLightbox2();
  }
});
</script>

<script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>

<script>
const slides = [
  "/projects/screenshot1.png",
  "/projects/screenshot2.png",
  "/projects/screenshot3.png",
  "/projects/screenshot4.png",
  "/projects/screenshot5.png",
  "/projects/screenshot6.png",
  "/projects/wobble.gif"
];
let current = 0;

function updateCarousel() {
  document.getElementById("carousel-img").src = slides[current];
  document.getElementById("carousel-counter").textContent = (current + 1) + " / " + slides.length;
}
function nextSlide() { current = (current + 1) % slides.length; updateCarousel(); }
function prevSlide() { current = (current - 1 + slides.length) % slides.length; updateCarousel(); }

const REPO_RAW_BASE = "https://raw.githubusercontent.com/chriskersov/3DS-wobble-gif/main/";

fetch(REPO_RAW_BASE + "README.md")
  .then(r => r.text())
  .then(text => {
    // Rewrite relative markdown image paths
    let rewritten = text.replace(
      /!\[([^\]]*)\]\((?!https?:\/\/)([^)]+)\)/g,
      (match, alt, src) => `![${alt}](${REPO_RAW_BASE}${src})`
    );
    // Rewrite relative src="" attributes in HTML tags
    rewritten = rewritten.replace(
      /src="(?!https?:\/\/)([^"]+)"/g,
      (match, src) => `src="${REPO_RAW_BASE}${src}"`
    );
    document.getElementById("readme-content").innerHTML = marked.parse(rewritten);
  })
  .catch(() => { document.getElementById("readme-content").textContent = "Could not load README."; });
</script>

<!-- ─── PROJECT 02 ─────────────────────────────────────────── -->

<br>
<br>
 
## Personal Finances AI
 
### <a href="https://github.com/chriskersov/personal-finances-ai" target="_blank" style="color:black; text-decoration:underline;">GitHub</a>
 
<div style="display:flex; flex-wrap:wrap; gap:0.4rem; margin-bottom:1rem;">
  <span style="border:2px solid #ccc; padding:0.1rem 0.5rem; color: #888;">Streamlit</span>
  <span style="border:2px solid #ccc; padding:0.1rem 0.5rem; color: #888;">openpyxl</span>
  <span style="border:2px solid #ccc; padding:0.1rem 0.5rem; color: #888;">Ollama</span>
  <span style="border:2px solid #ccc; padding:0.1rem 0.5rem; color: #888;">qwen2.5:7b</span>
</div>
 
<div style="display:grid; grid-template-columns:0.6fr 0.4fr; gap:3rem; align-items:start; margin-bottom:1.75rem;">
 
  <div>
    A Streamlit app that reads a personal Excel finance workbook — one sheet per month, tracking needs, wants, savings, income, and spending by category — and uses a locally running LLM to generate a plain-English summary of the current month. It produces a monthly digest covering cash flow, budget goal tracking, top spending categories, and a forward-looking observation. Everything runs fully offline on the machine; the Excel file is never committed to the repo.
  </div>
 
<div style="width:100%; border: 2px solid #ccc; table-layout: fixed; box-sizing: border-box;">
  <div onclick="openLightbox2(0)" style="position:relative; cursor:pointer; overflow:hidden; background: #000000; line-height:0;">
    <img src="/projects/screenshot7.png" alt="Project screenshot" style="width:100%; display:block; opacity:0.35;">
    <div style="position:absolute; inset:0; display:flex; flex-direction:column; align-items:center; justify-content:center; gap:8px; line-height:1.5;">
      <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="1.5" stroke-linecap="round">
        <rect x="3" y="3" width="7" height="7" rx="1"/><rect x="14" y="3" width="7" height="7" rx="1"/>
        <rect x="3" y="14" width="7" height="7" rx="1"/><rect x="14" y="14" width="7" height="7" rx="1"/>
      </svg>
      <span style="color:white;">1 photo</span>
    </div>
  </div>
  <div onclick="openLightbox2(0)" style="cursor:pointer; text-align:center; padding:0.4rem 0; color:black; background:#f4f4f4; border-top:1px solid #ccc;"><strong>View Gallery</strong></div>
</div>
 
</div>
 
<table style="width:100%; border: 2px solid #ccc; border-collapse: collapse; table-layout: fixed; box-sizing: border-box;">
    <tr>
        <td style="width:33%; border: 1px solid #ccc; padding: 0.5rem 0.75rem; vertical-align: top; text-align: center; background: #f4f4f4;">
            <strong>README.md</strong>
        </td>
    </tr>
    <tr>
        <td style="border: 1px solid #ccc; padding: 0.5rem 0.75rem; vertical-align: top; background: white;">
            <a href="https://github.com/chriskersov/personal-finances-ai" target="_blank" style="color:black; text-decoration:none;">
              <div id="readme-container-2" style="max-height:500px; overflow-y:scroll; scrollbar-width:none; -ms-overflow-style:none; padding:1rem 1.25rem; margin-top:0.5rem; box-sizing:border-box; width:100%;">
                <div id="readme-content-2" style="font-family:monospace; color:black; margin:0; word-break:break-word;">Loading README...</div>
              </div>
            </a>
        </td>
    </tr>
</table>
 
<div id="lightbox2" style="display:none; position:fixed; inset:0; background:rgba(0,0,0,0.85); z-index:1000; align-items:center; justify-content:center;">
  <button onclick="closeLightbox2()" style="position:absolute; top:1.5rem; right:1.5rem; background:none; border:none; color:white; font-size:1.5rem; cursor:pointer;">✕</button>
  <img id="lightbox2-img" src="" style="max-width:90vw; max-height:85vh; display:block; object-fit:contain;">
  <span id="lightbox2-counter" style="position:absolute; bottom:1.5rem; left:50%; transform:translateX(-50%); color:white; font-size:0.8rem;"></span>
</div>
 
<script>
const slides2 = ["/projects/screenshot7.png"];
let lightboxIndex2 = 0;
 
function openLightbox2(index) {
  lightboxIndex2 = index;
  const lb = document.getElementById("lightbox2");
  lb.style.display = "flex";
  document.getElementById("lightbox2-img").src = slides2[lightboxIndex2];
  document.getElementById("lightbox2-counter").textContent = (lightboxIndex2 + 1) + " / " + slides2.length;
}
function closeLightbox2() {
  document.getElementById("lightbox2").style.display = "none";
}
document.getElementById("lightbox2").addEventListener("click", function(e) {
  if (e.target === this) closeLightbox2();
});
</script>
 
<script>
const REPO_RAW_BASE_2 = "https://raw.githubusercontent.com/chriskersov/personal-finances-ai/main/";
 
fetch(REPO_RAW_BASE_2 + "README.md")
  .then(r => r.text())
  .then(text => {
    let rewritten = text.replace(
      /!\[([^\]]*)\]\((?!https?:\/\/)([^)]+)\)/g,
      (match, alt, src) => `![${alt}](${REPO_RAW_BASE_2}${src})`
    );
    rewritten = rewritten.replace(
      /src="(?!https?:\/\/)([^"]+)"/g,
      (match, src) => `src="${REPO_RAW_BASE_2}${src}"`
    );
    document.getElementById("readme-content-2").innerHTML = marked.parse(rewritten);
  })
  .catch(() => { document.getElementById("readme-content-2").textContent = "Could not load README."; });
</script>
