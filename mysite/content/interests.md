---
title: Interests
# author: Chris Kersov
---

<br>

<h1 style="font-size:3.5rem; margin:0 0 -0.2em;">Interests</h1>

<br>

<div>
This page is a snapshot of who I am outside of work and computer science - the sports I play, the places I have travelled, the things I am learning, and the hobbies that keep me curious and grounded day to day.
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
    { id: "Travelling", label: "Travelling", size: 18, color: "#c4c4c4", textColor: "#333", target: "#travel-photo" },
    { id: "Photography", label: "Photography", size: 18, color: "#c4c4c4", textColor: "#333", target: "#travel-photo" },
    { id: "Philosophy", label: "Philosophy", size: 18, color: "#c4c4c4", textColor: "#333", target: "#philosophy" },
    { id: "Mandarin", label: "Mandarin", size: 18, color: "#c4c4c4", textColor: "#333", target: "#learning" },
    { id: "ProjectIdeas", label: "Project Ideas", size: 18, color: "#c4c4c4", textColor: "#333", target: "#projects-ideas" },
    { id: "Reading", label: "Reading", size: 18, color: "#c4c4c4", textColor: "#333", target: "#learning" },
    { id: "Technology", label: "Technology", size: 18, color: "#c4c4c4", textColor: "#333", target: "#tech-life" }
  ],
  links: [
    { source: "Chris", target: "Tennis" },
    { source: "Chris", target: "TableTennis" },
    { source: "Chris", target: "Badminton" },
    { source: "Chris", target: "Travelling" },
    { source: "Chris", target: "Photography" },
    { source: "Chris", target: "Philosophy" },
    { source: "Chris", target: "Mandarin" },
    { source: "Chris", target: "ProjectIdeas" },
    { source: "Chris", target: "Reading" },
    { source: "Chris", target: "Technology" },
    { source: "Tennis", target: "TableTennis" },
    { source: "TableTennis", target: "Badminton" },
    { source: "Badminton", target: "Tennis" },
    { source: "Travelling", target: "Photography" },
    { source: "Reading", target: "Philosophy" }
  ]
};

const svg = d3.select("#brain-graph");
const container = document.getElementById('graph-container');
let width = container.clientWidth;
let height = container.clientHeight;

// Optimized Forces for a balanced "Galaxy" look
function getTargetX(d) {
  if (d.id === "Chris") return width / 2;
  if (["Tennis", "TableTennis", "Badminton"].includes(d.id)) return width * 0.22;
  if (d.id === "Travelling") return width * 0.33;
  if (d.id === "Photography") return width * 0.38;
  if (["Philosophy", "Mandarin", "Reading"].includes(d.id)) return width * 0.68;
  if (["ProjectIdeas", "Technology"].includes(d.id)) return width * 0.84;
  return width * 0.6;
}

function getTargetY(d) {
  if (d.id === "Travelling") return height * 0.22;
  return height / 2;
}

const simulation = d3.forceSimulation(data.nodes)
  .force("link", d3.forceLink(data.links).id(d => d.id).distance(140))
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
    link.attr("x1", d => d.source.x)
        .attr("y1", d => d.source.y)
        .attr("x2", d => d.target.x)
        .attr("y2", d => d.target.y);
    node.attr("transform", d => `translate(${d.x},${d.y})`);
});

function dragstarted(event) {
  if (!event.active) simulation.alphaTarget(0.3).restart();
  event.subject.fx = event.subject.x;
  event.subject.fy = event.subject.y;
}
function dragged(event) {
  event.subject.fx = event.x;
  event.subject.fy = event.y;
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
    <div style="color: #888; margin-bottom: 1rem;">The sports I follow and play are the ones that reward repetition, technique, and small improvements over time.</div>
    <div style="display: grid; grid-template-columns: 1fr; gap: 1rem;">
      <div style="border: 1px solid #ccc; background: #f9f9f9; padding: 1rem 1.1rem;">
        <div style="font-size: 1.05rem; font-weight: 700; margin-bottom: 0.4rem;">Tennis</div>
        <div style="line-height: 1.7; color: #444;">
          Tennis is probably the sport I care about most. I want to write about how long I’ve played, the equipment I use, what I like about the game, and the prediction ideas I keep coming back to.
        </div>
        <div style="margin-top: 0.8rem; border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">
          Image placeholder: me playing tennis
        </div>
      </div>
      <div style="border: 1px solid #ccc; background: #f9f9f9; padding: 1rem 1.1rem;">
        <div style="font-size: 1.05rem; font-weight: 700; margin-bottom: 0.4rem;">Table tennis</div>
        <div style="line-height: 1.7; color: #444;">
          Fast, technical, and addictive. This section can cover how I got into it, favourite players, equipment, and the moments I’ve played at work or elsewhere.
        </div>
        <div style="margin-top: 0.8rem; border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">
          Image placeholder: table tennis photo
        </div>
      </div>
      <div style="border: 1px solid #ccc; background: #f9f9f9; padding: 1rem 1.1rem;">
        <div style="font-size: 1.05rem; font-weight: 700; margin-bottom: 0.4rem;">Badminton / Padel</div>
        <div style="line-height: 1.7; color: #444;">
          A smaller space for racket sports I want to keep playing more of. This is where I can talk about what I enjoy, where I play, and what I want to improve.
        </div>
        <div style="margin-top: 0.8rem; border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">
          Image placeholder: badminton / padel
        </div>
      </div>
    </div>

  </div>

  <div id="projects-ideas" style="border: 2px solid #ccc; background: white; padding: 1.25rem 1.5rem; margin-bottom: 1.25rem;">
    <div style="font-size: 1.5rem; font-weight: 700; margin-bottom: 0.35rem;">Projects ideas</div>
    <div style="color: #888; margin-bottom: 1rem;">A vertical section for the ideas I keep returning to — these will eventually become fuller case studies with screenshots and demos.</div>
    <div style="display: grid; grid-template-columns: 1fr; gap: 1rem;">
      <div style="border: 1px solid #ccc; padding: 1rem 1.1rem; background: #f9f9f9;">
        <strong>Prediction / ML projects</strong>
        <div style="margin-top: 0.45rem; line-height: 1.7; color: #444;">
          Grand slam predictors, football-style live match predictions, F1 ideas, weather analysis, and anything else where patterns, uncertainty, and data meet.
        </div>
      </div>
      <div style="border: 1px solid #ccc; padding: 1rem 1.1rem; background: #f9f9f9;">
        <strong>Useful tools</strong>
        <div style="margin-top: 0.45rem; line-height: 1.7; color: #444;">
          An MPO-to-image package, a typing test, a chat context mover, a pronunciation fix for my name, and other small things that solve a real annoyance.
        </div>
      </div>
      <div style="border: 1px solid #ccc; padding: 1rem 1.1rem; background: #f9f9f9;">
        <strong>Presentation / online presence</strong>
        <div style="margin-top: 0.45rem; line-height: 1.7; color: #444;">
          Improving my GitHub profile, writing better READMEs, exploring marketing for projects, and maybe rebuilding my CV in LaTeX or Typst.
        </div>
      </div>
    </div>
  </div>

  <div id="learning" style="border: 2px solid #ccc; background: white; padding: 1.25rem 1.5rem; margin-bottom: 1.25rem;">
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
  </div>

  <div id="travel-photo" style="border: 2px solid #ccc; background: white; padding: 1.25rem 1.5rem; margin-bottom: 1.25rem;">
    <div style="font-size: 1.5rem; font-weight: 700; margin-bottom: 0.35rem;">Travel and photography</div>
    <div style="color: #888; margin-bottom: 1rem;">A place for photos, destinations, and the kind of moments I want to remember.</div>
    <div style="display: grid; grid-template-columns: 1fr; gap: 1rem;">
      <div style="border: 1px solid #ccc; background: #f9f9f9; padding: 1rem 1.1rem;">
        <div style="line-height: 1.7; color: #444;">
          Recently I’ve started travelling more and I want this section to become a photo-led diary of places I’ve been and places I want to go.
        </div>
        <div style="margin-top: 0.8rem; border: 2px dashed #ccc; background: white; padding: 1rem; color: #888; text-align: center;">
          Image placeholder: travel / scenery photo
        </div>
      </div>
    </div>
  </div>

  <div id="tech-life" style="border: 2px solid #ccc; background: white; padding: 1.25rem 1.5rem; margin-bottom: 1.25rem;">
    <div style="font-size: 1.5rem; font-weight: 700; margin-bottom: 0.35rem;">Tech and life</div>
    <div style="color: #888; margin-bottom: 1rem;">The everyday stuff: devices, finances, productivity, and the systems I like keeping tidy.</div>
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 1rem;">
      <div style="border: 1px solid #ccc; background: #f9f9f9; padding: 1rem 1.1rem;">
        <strong>Tech</strong>
        <div style="margin-top: 0.45rem; line-height: 1.7; color: #444;">
          Keyboards, laptops, headphones, Linux ideas, and the little design details that make tools nicer to use.
        </div>
      </div>
      <div style="border: 1px solid #ccc; background: #f9f9f9; padding: 1rem 1.1rem;">
        <strong>Personal finances</strong>
        <div style="margin-top: 0.45rem; line-height: 1.7; color: #444;">
          Keeping track of my finances and building a better system for staying on top of everything.
        </div>
      </div>
    </div>

  </div>

  <div id="philosophy" style="border: 2px solid #ccc; background: #f4f4f4; padding: 1.25rem 1.5rem; margin-bottom: 1.25rem;">
    <div style="font-size: 1.5rem; font-weight: 700; margin-bottom: 0.35rem;">Philosophy</div>
    <div style="line-height: 1.7; color: #444;">
      I like the idea of building a life around curiosity, consistency, and useful output — learning a lot, making things that help people, and leaving room to enjoy the process too.
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
  - haha what if you make a parlay for some likely combinations

- need to fix the pronounciation of chris kersov to be able to work on all browsers
- just make it play a stored audio

- have a cv download on the first page

### Sports:

#### Tennis

Talk about tennis history.
How much I love it.
How long I have been playing.
My equipment, shoes etc.
Predictions for next grand slam.
ML predictor for next grand slam github link maybe.
(I could do this for each year and then see how evolves etc).
Racket stringing as sort of a mini business.
IMAGE OF ME PLAYING TENNIS - NEEDS TO BE COLD.

#### Table tennis

Talk about how much I love table tennis.
My equipment.
How I got into table tennis.
Watching table tennis and fav players etc: ma long, truls, anders, fan.
My fav ma long photo and maybe truls celebration photo.
IMAGE OF ME PLAYING TABLE TENNIS AT WORK.

#### Badminton

Talk about my badminton interests.
How I got into it.
Want to play more, will play more at uni.
My equipment.
IMAGE OF ME PLAYING BADMINTON WITH YU SUM.

#### Padel

### Interests:

#### Rubik's Cubes:

Solving Rubik's cubes of various shapes and sizes:
2x2, 3x3, 4x4, 5x5, pyraminx, megaminx.

#### Learning Mandarin:

Give some explanation as to why I am learning Mandarin.
How much I have learnt so far.
My learning goals: HSK 1 etc.

#### Travelling:

Recently started travelling more.
Absolutely love it.
Places I have been to: list them.
Places I plan and want to go.

#### Photography:

Some cool photos I have taken.
I wish to learn more about photography.
I love taking photos of pretty scenery.

#### Eating:

I love eating.

#### Learning:

Learning in my spare time.
What stuff am I interested in learning.
Books I am reading for personal learning. HOML.
Any courses I am taking.

#### Anime:

Anime I am watching currently.
Animes I have enjoyed.
Could include some manga panels or cool photos.

#### Gaming:

Minecraft.
Nintendo 3DS jailbroken.

#### Personal Finances:

Interested in staying on top of my finances.
Created Excel spreadsheet to track.
Could link the sheet.

#### Tech:

Logitech MX master 3.
M4 Macbook Air.
iPad air something (i want to look into e ink tablets).
Sony xm5s (cant live without them).
Nintendo 3ds.
logitech mx master keyboard
or my own keyboard I created (show photos - blank keycaps)

Want to purchase and upgrade a thinkpad
and use linux

also rewrite cv in latex or typst. can also have it previewed in one of the pages. with some annotations or something maybe idk.

it could be cool to have my timezone and current time for me as well. also have the hk timezone on there.

i want something about my philosophy towards life as well.

also i want to enable google analytics.

when you tab and then it higlights the surrounding of links i want that to be customised. i want the scroll bar to be customised as well.

I managed to make code blocks with syntax highlighting. I could make something cool where like it shows a block of code or like a function of sorts and then an animted output of like a cool graph or something. my github profile hahahhaha

perhaps on my projects page i could have a heatmap of my leetcode
and also a heatmap of my github

```python
print("hello world")
```

```
 > hello world
```

i can also render latex equations qhich is cool. maybe i might find a use for this somewhere. maybe when talking about what i am learning idk.

$$
{\sqrt {n}}\left(\left({\frac {1}{n}}\sum _{i=1}^{n}X_{i}\right)-\mu \right)\ {\xrightarrow {d}}\ N\left(0,\sigma ^{2}\right)
$$

looks like i can link to other parts just by doing this [posts](/post/) [notes](/note/). but idk what these pages are. in the template yihui mentions these 'pages not under the root directory' and shows these. so this must be something to do with the footer.

i also want to improve the footer.

i have realised that what i mean by footer and header are the things above and below the dotted lines. but these arent header.html and footer.html. i need to improve my understanding
-->
