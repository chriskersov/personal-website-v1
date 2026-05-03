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
    { id: "Chris", label: "Chris", size: 22, color: "#2f2f2f", textColor: "#fff", target: null },
    { id: "Tennis", label: "Tennis", size: 18, color: "#c4c4c4", textColor: "#333", target: "#sports" },
    { id: "TableTennis", label: "Table Tennis", size: 18, color: "#c4c4c4", textColor: "#333", target: "#sports" },
    { id: "Badminton", label: "Badminton", size: 18, color: "#c4c4c4", textColor: "#333", target: "#sports" },
    { id: "Travel", label: "Travel", size: 18, color: "#c4c4c4", textColor: "#333", target: "#travel-photo" },
    { id: "Photography", label: "Photography", size: 18, color: "#c4c4c4", textColor: "#333", target: "#travel-photo" },
    { id: "Philosophy", label: "Philosophy", size: 18, color: "#c4c4c4", textColor: "#333", target: "#philosophy" },
    { id: "RubiksCubes", label: "Rubik's Cubes", size: 18, color: "#c4c4c4", textColor: "#333", target: "#rubiks-cubes" },
    { id: "Food", label: "Food", size: 18, color: "#c4c4c4", textColor: "#333", target: "#food" },
    { id: "ProjectIdeas", label: "Project Ideas", size: 18, color: "#c4c4c4", textColor: "#333", target: "#projects-ideas" },
    { id: "Tech", label: "Tech", size: 18, color: "#c4c4c4", textColor: "#333", target: "#tech-life" }
  ],
  links: [
    { source: "Chris", target: "Tennis" },
    { source: "Chris", target: "TableTennis" },
    { source: "Chris", target: "Badminton" },
    { source: "Chris", target: "Travel" },
    { source: "Chris", target: "Photography" },
    { source: "Chris", target: "Philosophy" },
    { source: "Chris", target: "ProjectIdeas" },
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
const graphPadding = 28;

// Optimized Forces for a balanced "Galaxy" look
function getTargetX(d) {
  if (d.id === "Chris") return width / 2;
  if (["Tennis", "TableTennis", "Badminton"].includes(d.id)) return width * 0.22;
  // Evenly space the travel/food/photography trio across the top
  // Move the travel/food/photography trio to the right side (slightly left-shifted)
  if (d.id === "Travel") return width * 0.68;
  if (d.id === "Food") return width * 0.72;
  if (d.id === "Photography") return width * 0.76;
  if (["Tech"].includes(d.id)) return width * 0.5;
  // Place Rubik's Cubes directly below the central node
  if (d.id === "RubiksCubes") return width * 0.60;
  // Place Philosophy centered above the central node
  if (d.id === "Philosophy") return width / 2;
  if (["ProjectIdeas"].includes(d.id)) return width * 0.45;
  return width * 0.6;
}

function getTargetY(d) {
  if (d.id === "Chris") return height * 0.41;
  // Keep travel/food/photography at center like tennis trio
  if (["Travel", "Food", "Photography"].includes(d.id)) return height / 2;
  // Place Philosophy above and isolated
  if (d.id === "Philosophy") return height * 0.15;
  // Place Tech at bottom-right corner
  if (d.id === "Tech") return height * 0.9;
  // Place Project Ideas near the bottom
  if (d.id === "ProjectIdeas") return height * 0.85;
  // Rubik's Cubes below centre
  if (d.id === "RubiksCubes") return height * 0.75;
  return height / 2;
}

function clampNodePosition(node) {
  const padding = Math.max(graphPadding, node.size + 18);
  node.x = Math.max(padding, Math.min(width - padding, node.x));
  node.y = Math.max(padding, Math.min(height - padding, node.y));
}

const simulation = d3.forceSimulation(data.nodes)
  .alpha(0.55) // Start with less energy so initial motion is calmer
  .velocityDecay(0.58) // More damping slows node movement between ticks
  .force("link", d3.forceLink(data.links).id(d => d.id).distance(d => {
    if (d.source.id === "Chris" && d.target.id === "ProjectIdeas" || d.source.id === "ProjectIdeas" && d.target.id === "Chris") {
      return 100;
    }
    if (d.source.id === "Chris" && d.target.id === "Philosophy" || d.source.id === "Philosophy" && d.target.id === "Chris") {
      return 130;
    }
    return 140;
  }))
  .force("charge", d3.forceManyBody().strength(-420)) // Stronger repulsion for even spread
  .force("x", d3.forceX(d => getTargetX(d)).strength(0.14))
  .force("y", d3.forceY(d => getTargetY(d)).strength(0.22))
    .force("center", d3.forceCenter(width / 2, height / 2))
  .force("collide", d3.forceCollide().radius(40)); // Keeps nodes from overlapping

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
    .attr("cursor", "pointer")
    .on("click", (event, d) => {
        if (d.target) {
            const el = document.querySelector(d.target);
            if(el) el.scrollIntoView({ behavior: 'smooth' });
        }
    })
    .call(d3.drag()
        .on("start", dragstarted)
        .on("drag", dragged)
        .on("end", dragended));

node.append("circle")
    .attr("r", d => d.size)
    .attr("fill", d => d.color)
    .attr("stroke", "#fff")
    .attr("stroke-width", 2)
    .style("filter", "drop-shadow(0 1px 2px rgba(0,0,0,0.05))");

node.append("text")
    .attr("text-anchor", "middle")
  .attr("y", d => d.size + 12)
  .attr("dy", "0")
    .style("font-family", "Arial, sans-serif")
  .style("font-size", "11px") // Smaller, cleaner text
    .style("font-weight", "500")
    .style("fill", d => d.textColor)
    .style("pointer-events", "none")
  .style("dominant-baseline", "hanging")
    .text(d => d.label);

simulation.on("tick", () => {
  data.nodes.forEach(clampNodePosition);
    link.attr("x1", d => d.source.x)
        .attr("y1", d => d.source.y)
        .attr("x2", d => d.target.x)
        .attr("y2", d => d.target.y);
    node.attr("transform", d => `translate(${d.x},${d.y})`);
});

function dragstarted(event) {
  if (!event.active) simulation.alphaTarget(0.16).restart();
  event.subject.fx = event.subject.x;
  event.subject.fy = event.subject.y;
}
function dragged(event) {
  event.subject.fx = event.x;
  event.subject.fy = event.y;
  clampNodePosition(event.subject);
  event.subject.fx = event.subject.x;
  event.subject.fy = event.subject.y;
}
function dragended(event) {
  if (!event.active) simulation.alphaTarget(0);
  event.subject.fx = null;
  event.subject.fy = null;
}

window.addEventListener('resize', () => {
    width = container.clientWidth;
    height = container.clientHeight;

    simulation.force("center", d3.forceCenter(width / 2, height / 2));
    data.nodes.forEach(clampNodePosition);
  simulation.alpha(0.16).restart();
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
          I've been to Spain once; I went to Barcelona and Blanes. I was completely mesmerised by La Sagrada Familia.
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

  <!-- <div id="learning" style="border: 2px solid #ccc; background: white; padding: 1.25rem 1.5rem; margin-bottom: 1.25rem;">
    <div style="font-size: 1.5rem; font-weight: 700; margin-bottom: 0.35rem;">Learning</div>
    <div style="color: #888; margin-bottom: 1rem;">Things I’m actively learning or want to learn more deeply over time.</div>
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 1rem;">
      <div style="border: 1px solid #ccc; background: #f9f9f9; padding: 1rem 1.1rem;">
        <strong>Mandarin</strong>
        <div style="margin-top: 0.45rem; line-height: 1.7; color: #444;">
          Why I started, how far I’ve got, and what I want to reach next.
        </div>
      </div>
      <div style="border: 1px solid #ccc; background: #f9f9f9; padding: 1rem 1.1rem;">
        <strong>Reading and courses</strong>
        <div style="margin-top: 0.45rem; line-height: 1.7; color: #444;">
          Books, papers, courses, and whatever I’m currently learning in my spare time.
        </div>
      </div>
    </div>
  </div> -->

  <div id="projects-ideas" style="border: 2px solid #ccc; background: white; padding: 1.25rem 1.5rem; margin-bottom: 1.25rem;">
    <div style="font-size: 1.5rem; font-weight: 700; margin-bottom: 0.35rem;">Project Ideas</div>
    <br>
    <!-- <div style="color: #888; margin-bottom: 1rem;"></div> -->
    <div style="border: 1px solid #ccc; padding: 1rem 1.1rem; background: #f9f9f9; line-height: 1.8; color: #444; display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 0.8rem 1.5rem;">
      <div>
        Tennis Grand Slam Predictors<br>
        Football-Style Live Match Predictions<br>
        F1 Ideas<br>
        Weather Analysis<br>
        An MPO-to-Image Package<br>
        A Typing Test
      </div>
      <div>
        A Chat Context Mover<br>
        Improving My GitHub Profile<br>
        Exploring Marketing for Projects<br>
        Rebuilding My CV in LaTeX or Typst<br>
        Quant-Related Projects
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

<!--
Archived original notes for later expansion:

ideas for future projects

- UK weather analysis

- create an npm package that converts mpo file to two jpegs

- aus open predictor
- roland garros predictor (so many further things that can be built on top of this)
- world cup predictor
- premier league predictor

- an f1 related project

- llm free tier memory mover

- terminal typing test with basic customisability that dies when you make a mistake
- but has better versions as well
- and also gives in depth analsis as to waht you did while typing

- quant finance related projects
- something that could be useful for my final year project
- with some machine learning could be cool

- make my github profile look pretty

- make a readme for my github main page

- look into how best to market projects to get users. like for the 3ds one for example.

- a project that takes your current chat lets say you reached your limit then converts it to some format. then you take that to a new free ai tier then upload it there and boom its caught up and dont need to worry about the context window. what format to convert it to and how i am not sure. binary, tokens, idk. also how can you export a whole chat. im sure thats possible. but yeah this should be a useable tool maybe even a chrome extension or something.

- just had an idea to evolve the ML grand slam predictor further
- i want to have live match prediction kinda like google and football
- use this video to learn how to do this ml stuff by looking a match:
  - https://www.youtube.com/watch?v=L23oIHZE14w
- just cool to be able to learn and play with this stuff anyways
- but perhaps the ml predictor could make a prediction
  - then after the match is over watch the match back and improve its prediction or something
- idk im not exactly sure yet but there is something cool that can be done here i know there is

- i want to do the ml predictor for mens and woman
- perhaps for aus open i can do for mens only
- then for roland garros i can do for woman as well
- i also want to have money involved
- what about sentiment analysis
- also what bookies

also rewrite cv in latex or typst. can also have it previewed in one of the pages. with some annotations or something maybe idk.

it could be cool to have my timezone and current time for me as well. also have the hk timezone on there.

also i want to enable google analytics.

when you tab and then it higlights the surrounding of links i want that to be customised. i want the scroll bar to be customised as well.

perhaps on my projects page i could have a heatmap of my leetcode
and also a heatmap of my github





#### Padel

### Interests:

#### Rubik's Cubes:

Solving Rubik's cubes of various shapes and sizes:
2x2, 3x3, 4x4, 5x5, pyraminx, megaminx.
