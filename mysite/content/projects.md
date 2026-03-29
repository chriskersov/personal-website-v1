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

### <a href="https://github.com/chriskersov/3DS-wobble-gif" target="_blank" style="color:black; text-decoration:underline;">Link</a>&nbsp;-----&nbsp;<a href="https://github.com/chriskersov/3DS-wobble-gif" target="_blank" style="color:black; text-decoration:underline;">GitHub</a>

Streamlit, Pillow, NumPy, Streamlit Community Cloud

A web tool that converts Nintendo 3DS .mpo stereo image files into animated wobble GIFs. The 3DS captured true stereoscopic photos - two slightly offset images stored in a single file - but the format is almost universally unsupported outside the handheld itself. This tool extracts the stereo pair, aligns the frames using a pixel-difference score, and encodes them into a smoothly crossfaded, looping GIF that conveys the original depth and parallax allowing it to be viewable on any device with no special hardware required.

<!-- <div style="display:grid; grid-template-columns:1.5fr 0.5fr; gap:3rem; align-items:start; margin-bottom:1.75rem;">
å
  <div>
  A web tool for converting Nintendo 3DS MPO stereo images into animated wobble GIFs. Upload an MPO file, adjust the wobble speed and frame count, and download the result — all in the browser with no installation required. Built and deployed on Streamlit Community Cloud.
  </div>

  <div>
    <div id="carousel" style="position:relative; width:100%;">
      <img id="carousel-img" src="/projects/screenshot1.png" alt="Project screenshot" style="width:100%; display:block; border:1px solid #e8e8e8;">
      <div style="display:flex; justify-content:center; align-items:center; gap:1rem; margin-top:0.5rem;">
        <button onclick="prevSlide()" style="background:none; border:none; cursor:pointer; font-size:1rem; color:#999;">&#8592;</button>
        <span id="carousel-counter" style="font-size:0.75rem; color:#999;">1 / 3</span>
        <button onclick="nextSlide()" style="background:none; border:none; cursor:pointer; font-size:1rem; color:#999;">&#8594;</button>
      </div>
    </div>
  </div>

</div> -->

<table style="width:100%; border: 2px solid #ccc; border-collapse: collapse;">
    <tr>
        <td style="width:33%; border: 1px solid #ccc; padding: 0.5rem 0.75rem; vertical-align: top; text-align: center;">
            <strong>README.md</strong>
        </td>
    </tr>
    <tr>
        <td style="border: 1px solid #ccc; padding: 0.5rem 0.75rem; vertical-align: top;">
            <a href="https://github.com/chriskersov/3DS-wobble-gif" target="_blank"  style="color:black; text-decoration:none;">
              <div id="readme-container" style="max-height:500px; overflow-y:auto; background:#ededed; padding:1rem 1.25rem; margin-top:0.5rem;">
                <div id="readme-content" style="font-family:monospace; color:black; margin:0; word-break:break-word;">Loading README...</div>
              </div>
            </a>
        </td>
    </tr>
</table>

<!-- <hr style="border:none; border-top:1px solid #e0e0e0; margin:3.5rem 0;"> -->

<style>
  details[open] summary .arrow { display: none; }
  details:not([open]) summary .open-arrow { display: none; }
  details[open] #readme-container { max-height:none; }
</style>

<script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>

<script>
const slides = [
  "/projects/screenshot1.png",
  "/projects/screenshot2.png",
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
