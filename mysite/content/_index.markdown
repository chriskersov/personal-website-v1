---
title: Home
---

<style>
/* Pronunciation button */
.pronounce-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;                 
  background: transparent;
  border: none;
  padding: 0rem 0.25rem 0.10rem; 
  cursor: pointer;
  color: inherit;
  vertical-align: middle;
  font: inherit;
  line-height: 1;
}

.pronounce-btn svg {
  width: 1.05em;
  height: 1.05em;
  flex: none;
  stroke-width: 1.5; 
}

.pronounce-btn svg {
  width: 1.2em;
  height: 1.2em;
  flex: none;
}

.profile-img {
  max-width: 30%;
  min-width: 120px;
  float: right;
}

</style>

<br>

<img src="1760907231592.jpeg" class="profile-img" alt="Picture of Chris Kersov" />

<h1 style="font-size:3.5rem; margin:0 0 -0.2em;">Chris Kersov</h1>

<div style="margin-bottom: 1.45em; color: black">
  /kr<span style="font-size: 0.95em; font-weight:100; font-variation-settings: 'wght' 50; -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;">ɪ</span>s ˈk<span style="font-size: 0.95em; font-weight:100; font-variation-settings: 'wght' 50; -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;">ɛə</span>rs<span style="font-size: 0.95em; font-weight:100; font-variation-settings: 'wght' 50; -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;">ɒ</span>v/

  <button class="pronounce-btn" id="pronounce-button" aria-label="Play pronunciation of Chris Kersov" title="Play pronunciation of Chris Kersov" onclick="pronounceName()">

<!-- Icon: speaker with sound waves -->
<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true" focusable="false">
  <path d="M11 5L6 9H2v6h4l5 4V5z"/>
  <path d="M15.54 8.46a5 5 0 0 1 0 7.07"/>
</svg>

  </button>

  <!-- Audio element (use a short, hyphenated filename and place the file under your static or assets folder) -->

<audio id="pronounce-audio" src="chris kersov pronunciation.MP3" preload="none"></audio>

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
</script>

<br>

### Data Science in E-Mobility at Shell <img src="https://s3-eu-west-1.amazonaws.com/tpd/logos/6230badf6b83103f8dafcc43/0x0.png" alt="Shell logo" style="max-height:2.3em; display:inline-block; vertical-align:text-bottom; margin-left:-0.1em; margin-bottom: -0.4em" />

BSc (Hons) Computer Science and Artificial Intelligence at <a href="https://www.bath.ac.uk/" target="blank" style="color:#000000; text-decoration:underline;">University of Bath</a>

<br>

Currently on placement year doing data science within E-Mobility at Shell.
Studying Computer Science and Artificial Intelligence at the Univeristy of Bath.
Playing tennis, table tennis, badminton, padel. Solving Rubik's cubes of all various shapes and sizes: 2x2, 3x3, 4x4, 5x5, pyraminx, megaminx. Doing my best to learn mandarin. Travelling when I can. trying Trying hard to take cool photos. Eating a lot. I've always wanted to document my life. Maybe I can start with blogs, perhaps one day I will start posting vids on youtube. also talk aboutu how i string rackets as kind of a mini business.

I also want to talk very briefly about my work and what i am currently doing at work. what am i learning at work. what do i want to learn at work. goals at work. life at work. also want to talk about learning in my spare time. what stuff am i interested in learning. then maybe on the topic of leanring i can talk about uni. like books i am reading and stuff for personal learning. maybe homl. and also any courses i am taking.

it could be cool to have my timezone and current time for me as well. also have the hk timezone on there.

i want something about my philosophy towards life as well.

i want to improve the header as well. header.html

also i want to enable google analytics.

hobbies and interests. watching anime. listening to music. 3ds on the commute to work haha. learning mandarin. drawing sometimes. i just find life so interesting and i love to do lots of things. i built a keyboard i could put that as well. can talk about my current setup. and what i am interested to get into.

also interested in keeping tabs on my personal finances so i made this excel spreadsheet. then link the sheet.

mahjong, chess

nintendo 3ds

want to do thinkpad + linux (can i dual boot my m4 air and play around with linux)

add the name pronounciation thing

<!-- can have a page about speedsolving along with my best time and maybe a solve as well -->
<!-- Include a page about travel with photos I am proud of.  -->

<!-- ```bash
find . -not -path '*/exampleSite/*' \( -name '*.html' -o -name '*.css' \) | xargs wc -l
``` -->

I managed to make code blocks with syntax highlighting. I could make something cool where like it shows a block of code or like a function of sorts and then an animted output of like a cool graph or something. my github profile hahahhaha

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
