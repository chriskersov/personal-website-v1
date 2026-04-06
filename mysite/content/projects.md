---
Title: Projects
---

<br>

<h1 style="font-size:3.5rem; margin:0 0 -0.2em;">Projects</h1>

This page showcases the personal projects I've built in my spare time. I always have so many ideas and I love being able to bring them to life. I'm always thinking about what to build next, or how to make something I've already built better.

<br>

<!-- <hr style="border:none; border-top:1px solid #e0e0e0; margin:0 0 3.5rem;"> -->

<!-- ─── PROJECT 01 ─────────────────────────────────────────── -->

## 3DS MPO Wobble Tool

### <a href="https://3ds-wobble-gif.streamlit.app" target="_blank" style="color:black; text-decoration:underline;">Link</a>&nbsp;-----&nbsp;<a href="https://github.com/chriskersov/3DS-wobble-gif" target="_blank" style="color:black; text-decoration:underline;">GitHub</a>

Streamlit, Pillow, NumPy, Streamlit Community Clouds

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
  <div onclick="openLightbox(0)" style="cursor:pointer; text-align:center; padding:0.4rem 0; color:black; border-top:1px solid #ccc;"><strong>View Gallery</strong></div>
</div>
</div>

</div>

<table style="width:100%; border: 2px solid #ccc; border-collapse: collapse; table-layout: fixed; box-sizing: border-box;">
    <tr>
        <td style="width:33%; border: 1px solid #ccc; padding: 0.5rem 0.75rem; vertical-align: top; text-align: center;">
            <strong>README.md</strong>
        </td>
    </tr>
    <tr>
        <td style="border: 1px solid #ccc; padding: 0.5rem 0.75rem; vertical-align: top;">
            <a href="https://github.com/chriskersov/3DS-wobble-gif" target="_blank"  style="color:black; text-decoration:none;">
              <div id="readme-container" style="max-height:500px; overflow-y:scroll; scrollbar-width:none; -ms-overflow-style:none; background:#ededed; padding:1rem 1.25rem; margin-top:0.5rem; box-sizing:border-box; width:100%;">
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

// Close on backdrop click
document.getElementById("lightbox").addEventListener("click", function(e) {
  if (e.target === this) closeLightbox();
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
