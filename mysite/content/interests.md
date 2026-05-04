---
title: Interests
# author: Chris Kersov
---

<br>

<h1 style="font-size:3.5rem; margin:0 0 -0.2em;">Interests</h1>

<br>

<div>
This page is a snapshot of who I am outside of work and computer science - the sports I play, the places I have travelled, the things I am learning, and the hobbies I have that bring me so much joy in life.
</div>

<br>

<script src="https://d3js.org/d3.v7.min.js"></script>

<div style="max-width: 70rem; margin: 0 auto 1.1rem auto; border: 2px solid #ccc; background: white; padding: 0.7rem 0.9rem; box-sizing: border-box;">
  <div id="graph-container" style="position: relative; width: 100%; height: 340px; overflow: hidden; cursor: grab;">
    <svg id="brain-graph" style="width: 100%; height: 100%;"></svg>
  </div>
</div>

<script>
const data = {
    nodes: [
    { id: "Chris", label: "", size: 22, color: "#2f2f2f", textColor: "#fff", target: null },
    { id: "Tennis", label: "Tennis", size: 18, color: "#c4c4c4", textColor: "#333", target: "#sports" },
    { id: "TableTennis", label: "Table Tennis", size: 18, color: "#c4c4c4", textColor: "#333", target: "#sports" },
    { id: "Badminton", label: "Badminton", size: 18, color: "#c4c4c4", textColor: "#333", target: "#sports" },
    { id: "Travel", label: "Travel", size: 18, color: "#c4c4c4", textColor: "#333", target: "#travel-photo" },
    { id: "Photography", label: "Photography", size: 18, color: "#c4c4c4", textColor: "#333", target: "#travel-photo" },
    { id: "Philosophy", label: "Philosophy", size: 18, color: "#c4c4c4", textColor: "#333", target: "#philosophy" },
    { id: "RubiksCubes", label: "Rubik's Cubes", size: 18, color: "#c4c4c4", textColor: "#333", target: "#rubiks-cubes" },
    { id: "Food", label: "Food", size: 18, color: "#c4c4c4", textColor: "#333", target: "#food" },
    { id: "Tech", label: "Tech", size: 18, color: "#c4c4c4", textColor: "#333", target: "#tech-life" }
  ],
  links: [
    { source: "Chris", target: "Tennis" },
    { source: "Chris", target: "TableTennis" },
    { source: "Chris", target: "Badminton" },
    { source: "Chris", target: "Travel" },
    { source: "Chris", target: "Photography" },
    { source: "Chris", target: "Philosophy" },
    { source: "Chris", target: "Tech" },
    { source: "Chris", target: "RubiksCubes" },
    { source: "Chris", target: "Food" },
    { source: "Food", target: "Travel" },
    { source: "Food", target: "Photography" },
    { source: "Tennis", target: "TableTennis" },
    { source: "TableTennis", target: "Badminton" },
    { source: "Badminton", target: "Tennis" },
    { source: "Travel", target: "Photography" }
  ]
};

const svg = d3.select("#brain-graph");
const container = document.getElementById('graph-container');
let width = container.clientWidth;
let height = container.clientHeight;

function cx() { return width / 2; }
function cy() { return height / 2; }

data.nodes.forEach((d, i) => {
  const angle = (i / data.nodes.length) * Math.PI * 2;
  const radius = 10;
  d.x = cx() + Math.cos(angle) * radius;
  d.y = cy() + Math.sin(angle) * radius;
});

function targetX(d) {
  if (d.id === "Chris") return cx();
  if (["Tennis", "TableTennis", "Badminton"].includes(d.id)) return cx() - 180;
  if (["Travel", "Food", "Photography"].includes(d.id)) return cx() + 180;
  if (["Philosophy", "RubiksCubes"].includes(d.id)) return cx();
  if (d.id === "Tech") return cx();
  return cx();
}

function targetY(d) {
  if (d.id === "Chris") return cy();
  if (d.id === "Tennis") return cy() - 80;
  if (d.id === "TableTennis") return cy();
  if (d.id === "Badminton") return cy() + 80;
  if (d.id === "Travel") return cy() - 80;
  if (d.id === "Food") return cy();
  if (d.id === "Photography") return cy() + 80;
  if (d.id === "Philosophy") return cy() - 50;
  if (d.id === "RubiksCubes") return cy() + 130;
  if (d.id === "Tech") return cy() + 210;
  return cy();
}

const simulation = d3.forceSimulation(data.nodes)
  .force("link", d3.forceLink(data.links).id(d => d.id).distance(120))
  .force("charge", d3.forceManyBody().strength(-300))
  .force("x", d3.forceX(d => targetX(d)).strength(0.08))
  .force("y", d3.forceY(d => targetY(d)).strength(0.08))
  .force("collide", d3.forceCollide().radius(d => d.size + 18))
  .alphaDecay(0.02)
  .velocityDecay(0.5);

const link = svg.append("g")
  .selectAll("line")
  .data(data.links)
  .join("line")
  .attr("stroke", "#eee")
  .attr("stroke-width", 1.5);

const node = svg.append("g")
  .selectAll("g")
  .data(data.nodes)
  .join("g")
  .attr("cursor", "grab")
  .on("click", (event, d) => {
    if (d.target) {
      const el = document.querySelector(d.target);
      if (el) el.scrollIntoView({ behavior: 'smooth' });
    }
  })
  .call(d3.drag()
    .on("start", function(event, d) {
      if (!event.active) simulation.alphaTarget(0.3).restart();
      d.fx = d.x;
      d.fy = d.y;
      d3.select(this).attr("cursor", "grabbing");
    })
    .on("drag", function(event, d) {
      d.fx = Math.max(d.size + 4, Math.min(width - d.size - 4, event.x));
      d.fy = Math.max(d.size + 4, Math.min(height - d.size - 30, event.y));
    })
    .on("end", function(event, d) {
      if (!event.active) simulation.alphaTarget(0);
      d.fx = null;
      d.fy = null;
      d3.select(this).attr("cursor", "grab");
    })
  );

node.append("circle")
  .attr("r", d => d.size)
  .attr("fill", d => d.color)
  .attr("stroke", "#fff")
  .attr("stroke-width", 2);

node.append("text")
  .attr("text-anchor", "middle")
  .attr("dominant-baseline", d => d.id === "Chris" ? "central" : "hanging")
  .attr("y", d => d.id === "Chris" ? 0 : d.size + 12)
  .style("font-family", "Arial, sans-serif")
  .style("font-size", "11px")
  .style("font-weight", "500")
  .style("fill", d => d.textColor)
  .style("pointer-events", "none")
  .text(d => d.label);

simulation.on("tick", () => {
  data.nodes.forEach(d => {
    if (d.fx == null) {
      d.x = Math.max(d.size + 4, Math.min(width - d.size - 4, d.x));
      d.y = Math.max(d.size + 4, Math.min(height - d.size - 30, d.y));
    }
  });
  link
    .attr("x1", d => d.source.x).attr("y1", d => d.source.y)
    .attr("x2", d => d.target.x).attr("y2", d => d.target.y);
  node.attr("transform", d => `translate(${d.x},${d.y})`);
});

window.addEventListener('resize', () => {
  width = container.clientWidth;
  height = container.clientHeight;
  simulation.alpha(0.3).restart();
});
</script>

<br>

<!-- <div style="max-width: 70rem; margin: 0 auto;">
  <div style="border: 2px solid #ccc; background: white; padding: 1.25rem 1.5rem; margin-bottom: 1.5rem;">
<script src="https://d3js.org/d3.v7.min.js"></script> -->

</div>

  <div id="sports" style="border: 2px solid #ccc; background: white; padding: 1.25rem 1.5rem; margin-bottom: 1.25rem;">
    <div style="font-size: 1.5rem; font-weight: 700; margin-bottom: 0.35rem;">Sports</div>
    <br>
    <!-- <div style="color: #888; margin-bottom: 1rem;">The sports I follow and play are the ones that reward repetition, technique, and small improvements over time.</div> -->
    <div style="display: grid; grid-template-columns: 1fr; gap: 1rem;">
      <div style="border: 1px solid #ccc; background: #f9f9f9; padding: 1rem 1.1rem;">
        <div style="font-size: 1.05rem; font-weight: 700; margin-bottom: 0.4rem;">Tennis</div>
        <div style="line-height: 1.7; color: #444;">
          I have played tennis since I was 5 years old. I have always loved playing tennis. I competed regularly as a junior and have played first team for David Lloyd Northwood, Eastcote Lawn Tennis Club, and Lowlands Lawn Tennis Club. Over the past few years, I have battled through wrist and back injuries. I am still incredibly driven and motivated to keep improving in tennis, I just love it so much. I use a Head Extreme Pro with Head Lynx Tour at 54 / 52 lbs. I also have a stringing machine and string rackets for clients as a mini business.
        </div>
        <div style="margin-top: 0.8rem; display:grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap:0.6rem; background: #f9f9f9; padding: 0.6rem;">
          <img src="tennis_image_1.jpg" alt="Tennis 1" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
          <img src="tennis_image_4.jpg" alt="Tennis 4" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
          <img src="tennis_image_2.jpg" alt="Tennis 2" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
        </div>
      </div>
      <div style="border: 1px solid #ccc; background: #f9f9f9; padding: 1rem 1.1rem;">
        <div style="font-size: 1.05rem; font-weight: 700; margin-bottom: 0.4rem;">Table Tennis</div>
        <div style="line-height: 1.7; color: #444;">
         I love playing table tennis with my colleagues during lunch at work. It's a great way to take a break, reset my mind, and come back focused. Table tennis is very fast paced and requires super fast reaction times, which is one of the reasons I enjoy it so much. I quite enjoy watching table tennis as well, my favourite player is Truls Moregard.
        </div>
        <div style="margin-top: 0.8rem; display:grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap:0.6rem; background: #f9f9f9; padding: 0.6rem;">
          <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Table tennis 1</div>
          <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Table tennis 2</div>
          <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Table tennis 3</div>
        </div>
      </div>
      <div style="border: 1px solid #ccc; background: #f9f9f9; padding: 1rem 1.1rem;">
        <div style="font-size: 1.05rem; font-weight: 700; margin-bottom: 0.4rem;">Badminton</div>
        <div style="line-height: 1.7; color: #444;">
        I really enjoy playing badminton because it offers a unique dynamic compared to both tennis and table tennis. The game is incredibly high-intensity with explosive bursts, extreme speed, and technical skill involved. Playing doubles with my friends is so much fun and provides an excellent workout.
        </div>
        <div style="margin-top: 0.8rem; display:grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap:0.6rem; background: #f9f9f9; padding: 0.6rem;">
          <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Badminton 1</div>
          <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Badminton 2</div>
          <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Badminton 3</div>
        </div>
      </div>
    </div>
  </div>

  <div id="travel-photo" style="border: 2px solid #ccc; background: white; padding: 1.25rem 1.5rem; margin-bottom: 1.25rem;">
    <div style="font-size: 1.5rem; font-weight: 700; margin-bottom: 0.35rem;">Travel and Photography</div>
    <br>
    <!-- <div style="color: #888; margin-bottom: 1rem;"></div> -->
    <div style="display: grid; grid-template-columns: 1fr; gap: 1rem;">
      <div style="border: 1px solid #ccc; padding: 1rem 1.1rem; background: #f9f9f9;">
        <strong>Hong Kong</strong>
        <div style="margin-top: 0.45rem; line-height: 1.7; color: #444;">
          I've been to Hong Kong once and it was my first ever trip to Asia. It was the greatest trip of my life.
        </div>
        <div style="margin-top: 0.8rem; display:grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap:0.6rem; background: #f9f9f9; padding: 0.6rem;">
          <img src="hong_kong_image_1.jpg" alt="Hong Kong 1" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
          <img src="hong_kong_image_2.jpg" alt="Hong Kong 2" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
          <img src="hong_kong_image_3.jpg" alt="Hong Kong 3" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
        </div>
      </div>
      <div style="border: 1px solid #ccc; padding: 1rem 1.1rem; background: #f9f9f9;">
        <strong>Macau</strong>
        <div style="margin-top: 0.45rem; line-height: 1.7; color: #444;">
          During my first trip to Hong Kong I also went to Macau, exploring both the Macau Peninsula and Cotai. 
        </div>
        <div style="margin-top: 0.8rem; display:grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap:0.6rem; background: #f9f9f9; padding: 0.6rem;">
          <img src="macau_image_1.jpg" alt="Macau 1" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
          <img src="macau_image_3.jpg" alt="Macau 2" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
          <img src="macau_image_2.jpg" alt="Macau 3" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
        </div>
      </div>
      <div style="border: 1px solid #ccc; padding: 1rem 1.1rem; background: #f9f9f9;">
        <strong>Spain</strong>
        <div style="margin-top: 0.45rem; line-height: 1.7; color: #444;">
          I've been to Spain once; I went to Barcelona. I was completely mesmerised by La Sagrada Familia.
        </div>
        <div style="margin-top: 0.8rem; display:grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap:0.6rem; background: #f9f9f9; padding: 0.6rem;">
          <img src="spain_image_1.jpg" alt="Spain 1" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
          <img src="spain_image_2.jpg" alt="Spain 2" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
          <img src="spain_image_3.jpg" alt="Spain 3" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
        </div>
      </div>
      <div style="border: 1px solid #ccc; padding: 1rem 1.1rem; background: #f9f9f9;">
        <strong>Lithuania</strong>
        <div style="margin-top: 0.45rem; line-height: 1.7; color: #444;">
          Lithuania is very tranquil. I enjoy spending time in nature, especially in its forests and by its lakes.
        </div>
        <div style="margin-top: 0.8rem; display:grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap:0.6rem; background: #f9f9f9; padding: 0.6rem;">
          <img src="lithuania_image_1.jpg" alt="Lithuania 1" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
          <img src="lithuania_image_2.jpg" alt="Lithuania 2" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
          <img src="lithuania_image_3.jpg" alt="Lithuania 3" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
        </div>
      </div>
      <div style="border: 1px solid #ccc; padding: 1rem 1.1rem; background: #f9f9f9;">
        <strong>Egypt</strong>
        <div style="margin-top: 0.45rem; line-height: 1.7; color: #444;">
          I stayed in Sharm El Sheikh on my trip to Egypt, where I relaxed on the beach and tried activities like diving on coral reefs and quad‑biking in the desert.
        </div>
        <div style="margin-top: 0.8rem; display:grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap:0.6rem; background: #f9f9f9; padding: 0.6rem;">
          <img src="egypt_image_1.jpg" alt="Egypt 1" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
          <img src="egypt_image_2.jpg" alt="Egypt 2" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
          <img src="egypt_image_3.jpg" alt="Egypt 3" style="width:100%; height:auto; border:1px solid #e6e6e6; box-sizing:border-box; display:block;" />
        </div>
      </div>
    </div>
    <div style="margin-top: 1.5rem; padding-top: 1.5rem;">
      <div style="font-size: 1.25rem; font-weight: 700; margin-bottom: 0.8rem; color: #666;">Upcoming</div>
      <div style="display: grid; grid-template-columns: 1fr; gap: 1rem;">
        <div style="border: 1px solid #ccc; padding: 1rem 1.1rem; background: #f9f9f9;">
          <strong>China</strong>
            <div style="margin-top: 0.45rem; line-height: 1.7; color: #444;">
              I will be visiting China and I'm excited to explore its rich culture, natural beauty, and delicious food.
            </div>
            <div style="margin-top: 0.8rem; display:grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap:0.6rem; background: #f9f9f9; padding: 0.6rem;">
              <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: China 1</div>
              <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: China 2</div>
              <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: China 3</div>
            </div>
        </div>
        <div style="border: 1px solid #ccc; padding: 1rem 1.1rem; background: #f9f9f9;">
          <strong>Japan</strong>
          <div style="margin-top: 0.45rem; line-height: 1.7; color: #444;">
            I will be visiting Japan soon. I've always wanted to go to Japan so this will be a dream come true.
          </div>
          <div style="margin-top: 0.8rem; display:grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap:0.6rem; background: #f9f9f9; padding: 0.6rem;">
            <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Japan 1</div>
            <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Japan 2</div>
            <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Japan 3</div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div id="food" style="border: 2px solid #ccc; background: white; padding: 1.25rem 1.5rem; margin-bottom: 1.25rem;">
    <div style="font-size: 1.5rem; font-weight: 700; margin-bottom: 0.35rem;">Food</div>
    <br>
    <div style="border: 1px solid #ccc; padding: 1rem 1.1rem; background: #f9f9f9; line-height: 1.7; color: #444;">
      I love food so much. I enjoy trying new dishes in different countries and cultures - I get so much enjoyment from eating. I have so many images of food I've tried that I can't choose just a few to put here. I also love cooking and baking.
    </div>
  </div>

  <div id="tech-life" style="border: 2px solid #ccc; background: white; padding: 1.25rem 1.5rem; margin-bottom: 1.25rem;">
    <div style="font-size: 1.5rem; font-weight: 700; margin-bottom: 0.35rem;">Tech and Life</div>
    <br>
    <!-- Tech Section -->
    <div style="margin-bottom: 1.5rem;">
      <div style="display: grid; grid-template-columns: 1fr; gap: 1rem;">
        <div style="border: 1px solid #ccc; padding: 1rem 1.1rem; background: #f9f9f9;">
          <strong>Tech</strong>
                <div style="margin-top: 0.9rem; display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 1rem; color: #444; line-height: 1.7; margin: 0; padding: 0;">
            <div>
              <u>Laptop</u>: M4 Macbook Air<br>
              <u>Mouse</u>: Logitech MX Master 3<br>
              <u>Keyboard</u>: Custom built keyboard<br>
              <u>Keyboard</u>: Logitech MX Keys<br>
            </div>
            <div>
              <u>Notetaking</u>: iPad Air 4th Gen<br>
              <u>Headphones</u>: Sony WH-1000XM5<br>
              <u>Gaming</u>: Nintendo 3DS<br>
            </div>
          </div>
          <br>
          <div style="display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 0.6rem;">
            <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Tech 1</div>
            <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Tech 2</div>
            <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Tech 3</div>
            <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Tech 4</div>
            <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Tech 5</div>
            <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Tech 6</div>
            <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Tech 7</div>
            <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Tech 8</div>
          </div>
        </div>
      </div>
    </div>
    <!-- Rubik's Cubes Section -->
    <div id="rubiks-cubes" style="margin-bottom: 1.5rem;">
      <div style="display: grid; grid-template-columns: 1fr; gap: 1rem;">
        <div style="border: 1px solid #ccc; padding: 1rem 1.1rem; background: #f9f9f9;">
          <strong>Rubik's Cubes</strong>
          <div style="margin-top: 0.45rem; line-height: 1.7; color: #444;">
            I enjoy solving Rubik's Cubes of different shapes and sizes, including the 2x2, 3x3, 4x4, 5x5, Pyraminx, and Megaminx. It is a fun mix of pattern recognition, memory, and problem-solving.
          </div>
          <div style="margin-top: 0.9rem; display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 0.6rem; background: #f9f9f9; padding: 0.6rem;">
            <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Rubik's Cube 1</div>
            <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Rubik's Cube 2</div>
            <div style="border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">Image placeholder: Rubik's Cube 3</div>
          </div>
        </div>
      </div>
    </div>
    <!-- Anime Section -->
    <!-- <div style="margin-bottom: 1.5rem;">
      <div style="display: grid; grid-template-columns: 1fr; gap: 1rem;">
        <div style="border: 1px solid #ccc; padding: 1rem 1.1rem; background: #f9f9f9;">
          <strong>Shows & Anime</strong>
          <div style="margin-top: 0.45rem; line-height: 1.7; color: #444;">
            Anime shows I'm watching currently. Series I have enjoyed. Could include some manga panels or cool photos.
          </div>
        </div>
      </div>
    </div> -->
    <!-- Personal Finances Section -->
    <div style="margin-bottom: 0;">
      <div style="display: grid; grid-template-columns: 1fr; gap: 1rem;">
        <div style="border: 1px solid #ccc; padding: 1rem 1.1rem; background: #f9f9f9;">
          <strong>Personal Finances</strong>
          <div style="margin-top: 0.45rem; line-height: 1.7; color: #444;">
            I'm interested in staying on top of my finances. I've created an <a href="https://github.com/chriskersov/personal-finances-spreadsheet" style="color: black; text-decoration: underline;">Excel spreadsheet</a> that tracks my monthly expenses, income, and savings. It helps me visualise spending patterns and maintain awareness of my financial health. Beyond tracking, I'm interested in investing and algorithmic trading strategies. I love exploring how data science and quantitative methods can unlock better financial decision-making.
          </div>
        </div>
      </div>
    </div>
  </div>

  <div id="philosophy" style="border: 2px solid #ccc; background: white; padding: 1.25rem 1.5rem; margin-bottom: 1.25rem;">
    <div style="font-size: 1.5rem; font-weight: 700; margin-bottom: 0.35rem;">Philosophy</div>
    <div style="margin-top: 0.6rem;">
      <div style="border: 1px solid #ccc; background: #f9f9f9; padding: 1rem; line-height: 1.7; color: #444;">
        My everyday actions are what make me who I am. Results are just the side effects of what I do. You do it right. And do it every day. Doing stuff right just feels good. Repetition. Consistency. Care.
      </div>
    </div>
  </div>
</div>
