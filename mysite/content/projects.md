---
Title: Projects
---

<br>

<h1 style="font-size:3.5rem; margin:0 0 -0.2em;">Projects</h1>

This is a summary / intro paragraph about the projects I have made. I really enjoy doing personal projects in my spare time. I always have so many ideas and I find it so fun to be able to implement them into real life. I'm always thinking about new ideas or ways to improve my projects / solving problems.

<br>

<!-- <hr style="border:none; border-top:1px solid #e0e0e0; margin:0 0 3.5rem;"> -->

<!-- ─── PROJECT 01 ─────────────────────────────────────────── -->

## 3DS MPO Wobble Tool

### <a href="https://github.com/chriskersov/3DS-wobble-gif" target="_blank" style="color:black; text-decoration:underline;">Link</a>&nbsp;-----&nbsp;<a href="https://github.com/chriskersov/3DS-wobble-gif" target="_blank" style="color:black; text-decoration:underline;">GitHub</a>

Streamlit, Pillow, NumPy, Streamlit Community Cloud

<div style="display:grid; grid-template-columns:1.5fr 0.5fr; gap:3rem; align-items:start; margin-bottom:1.75rem;">

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

</div>

<table style="width:100%; border: 2px solid #ccc; border-collapse: collapse;">
    <tr>
        <td style="width:33%; border: 1px solid #ccc; padding: 0.5rem 0.75rem; vertical-align: top; text-align: center;">
            <strong>README.md</strong>
        </td>
    </tr>
    <tr>
        <td style="border: 1px solid #ccc; padding: 0.5rem 0.75rem; vertical-align: top;">
            <a href="../experience/" style="color:black; text-decoration:underline;">
              <div id="readme-container" style="max-height:500px; overflow-y:auto; border:1px solid #e8e8e8; background:#ededed; padding:1rem 1.25rem; margin-top:0.5rem;">
                <div id="readme-content" style="font-family:monospace; font-size:0.72rem; line-height:1.7; color:black; margin:0; white-space:pre-wrap; word-break:break-word;">Loading README...</div>
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

fetch("https://raw.githubusercontent.com/chriskersov/3DS-wobble-gif/main/README.md")
  .then(r => r.text())
  .then(text => { document.getElementById("readme-content").innerHTML = marked.parse(text); })
  .catch(() => { document.getElementById("readme-content").textContent = "Could not load README."; });
</script>

<!-- ─── PROJECT 02 ─────────────────────────────────────────── -->
