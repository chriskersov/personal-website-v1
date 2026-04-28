---
title: CV
---

<br>

<div style="position: relative; width: 100%; max-width: 900px; margin: 0 auto; border: 2px solid #ccc; background: white; box-sizing: border-box;">
  <a href="/images/ChristopherKersovCV_UpReach%20(1).pdf" download aria-label="Download CV" title="Download CV" style="position: absolute; top: 0.65rem; right: 0.65rem; z-index: 2; display: inline-flex; align-items: center; justify-content: center; width: 2.25rem; height: 2.25rem; border: 2px solid #ccc; border-radius: 0; background: #fff; color: #ccc; text-decoration: none; box-shadow: none; box-sizing: border-box;">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true" focusable="false" style="width: 1.1rem; height: 1.1rem; color: #000;">
      <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/>
      <path d="M7 10l5 5 5-5"/>
      <path d="M12 15V3"/>
    </svg>
  </a>
  <div id="pdf-container" style="width: 100%; box-sizing: border-box;"></div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<script>
pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';
const container = document.getElementById('pdf-container');
const PDF_URL = '/images/ChristopherKersovCV_UpReach (1).pdf';
const PAGE_GAP = 0; // px between pages — set to e.g. 12 if you want spacing
async function renderPDF(url) {
  const pdf = await pdfjsLib.getDocument(url).promise;
  for (let pageNum = 1; pageNum <= pdf.numPages; pageNum++) {
    const page = await pdf.getPage(pageNum);
    const scale = (container.clientWidth / page.getViewport({ scale: 1 }).width) * window.devicePixelRatio;
    const viewport = page.getViewport({ scale });
    const canvas = document.createElement('canvas');
    canvas.width = viewport.width;
    canvas.height = viewport.height;
    canvas.style.width = '100%';
    canvas.style.display = 'block';
    if (pageNum < pdf.numPages && PAGE_GAP > 0) {
      canvas.style.marginBottom = PAGE_GAP + 'px';
    }
    container.appendChild(canvas);
    await page.render({
      canvasContext: canvas.getContext('2d'),
      viewport
    }).promise;
  }
}
renderPDF(PDF_URL);
</script>
