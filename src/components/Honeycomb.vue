<template>
  <div class="honeycomb">
      <div
        v-for="project in projects"
        :key="project.id"
        :class="'hexagon ' + (project.is_challenge ? 'challenge' : 'project')"
        :challenge="project.is_challenge"
        :style="project.logo_color ? ('border-width: 3px; border-color:' + project.logo_color) : ''"
        :title="project.summary"
        @click="$emit('preview', project)"
      >
        <div class="hexagontent">
          <span>{{ project.name }}</span>
          <div v-if="project.hashtag" class="hashtag">{{ project.hashtag }}</div>
          <div class="hexaicon"
              v-if="project.image_url"
              :style="'background-image:url(' + project.image_url + ')'"></div>
              <div class="progress"
                v-if="!project.is_challenge && project.score && project.score > 0">
                <div class="progress-bar" role="progressbar"
                  :style="'width:' + project.score + '%'">
                </div>
              </div>
          </div>
      </div>
    </div>
</template>
<script>
export default {
  name: "Honeycomb",
  props: {
    projects: Array
  }
}
</script>

<style scoped>

/* ---- Hexagonal hawtness ---- */

.honeycomb {
  width: 760px;
  min-height: 700px;
  text-align: left;
  margin: 0 auto;
}
@media (max-width: 980px) {
  .honeycomb {
    width: auto;
    /* left: inherit; */
  }
}
@media (max-width: 420px) {
  .honeycomb .hexagon {
    margin-bottom: auto;
    top: auto;
  }
  .honeycomb {
    clear: both;
  }
}

@media (min-width: 452px) and (max-width: 595px) {
  .honeycomb {
    width:360px;
  }
}
@media (min-width: 707px) and (max-width: 847px) {
  .honeycomb {
    width:600px;
  }
}

.challenge.hexagon {
  background-color: white;
  border-top: 1px dashed rgba(0,0,200,0.4);
  border-bottom: 1px dashed rgba(0,0,200,0.4);
}
.challenge.hexagon::before {
  border-top: 1px dashed rgba(0,0,200,0.4);
  border-bottom: 1px dashed rgba(0,0,200,0.4);
}
.challenge.hexagon::after {
  border-top: 1px dashed rgba(0,0,200,0.4);
  border-bottom: 1px dashed rgba(0,0,200,0.4);
}

.project.hexagon  .hexagontent {
  overflow: hidden;
  color: black;
}
.project .hexagontent.with-icon div {
  font-size: 90%;
}
.project .hexagontent div {
  max-height: 5.4em;
}
.project .hexagontent .fa {
  font-size: 240%;
}
.project .hexagontent .progress {
  margin-top: 1em;
  margin-bottom: 0px;
  height: 3px;
  position: relative;
  width: 72px;
  margin-left: -36px;
  left: 50%;
  opacity: 1;
  border: 1px solid white;
}
.project .hexagontent .progress-bar {
  background-color: #aaa;
}
.project.hexagon {
  border-top: 1px solid rgba(0,0,0,0.2);
  border-bottom: 1px solid rgba(0,0,0,0.2);
}
.project.hexagon::before {
  border-top: 1px solid rgba(0,0,0,0.2);
  border-bottom: 1px solid rgba(0,0,0,0.2);
}
.project.hexagon::after {
  border-top: 1px solid rgba(0,0,0,0.2);
  border-bottom: 1px solid rgba(0,0,0,0.2);
}

/* --- Hexagon default palette --- */
.project.hexagon  { background-color: #f5d1e4; } /* primary color */
.hexagon.stage-5  { background-color: #f5d1e4; }
.hexagon.stage-10 { background-color: #e3d0e3; }
.hexagon.stage-20 { background-color: #e0c9ca; }
.hexagon.stage-30 { background-color: #e8b6a6; }
.hexagon.stage-40 { background-color: #f1cfad; }
.hexagon.stage-50 { background-color: #f6e8c0; }
/* https://colorkit.co/palette/f5d1e4-e3d0e3-e0c9ca-e8b6a6-f1cfad-f6e8c0/ */

@font-face{
  font-family: M3Regular;
  src: url(../assets/m3regular-webfont.woff2) format("woff2"),
       url(../assets/m3regular-webfont.woff) format("woff");
  font-weight: 400; font-style: normal;
}

.hexagon .hexagontent {
  color: #139;
  font-weight: normal;
  padding: 4px 0px;
  max-height: 120px;
  font-size: 12pt;
  line-height: 13pt;
  font-family: M3Regular,-apple-system,system-ui,BlinkMacSystemFont,Helvetica Neue,Arial,sans-serif;
}
.hexagontent .hashtag {
  font-weight: bold;
  font-size: 120%;
  color: red;
  text-shadow: 1px 1px 1px white;
  font-family: monospace;
  line-height: 0em;
  margin: 0.8em 0 0; 
  padding: 0px;
}
.hexagon .hexaicon {
  width: 2em;
  height: 2em;
  background-color: white;
  background-size: cover;
  position: relative;
  left: 50%;
  margin: 1em 0 0 -1em;
  box-shadow: -2px -2px 1px rgb(0 0 0 / 20%);
  border-radius: 1em;
}

.hexagon {
  position: relative;
  display: inline-block;
  /* left/right margin approx. 25% of .hexagon width + spacing */
  margin: -1px 22px;
  background-color: white;
  text-align: center;
  padding: 0px;
}
.hexagon, .hexagon::before, .hexagon::after {
  /* easy way: height is width * 1.732
  actual formula is 2*(width/(2*Math.tan(Math.PI/6)))
  remove border-radius for straight edges on hexagons */
  width: 82px;
  height: 142px;
  border-radius: 20%/5%;
}
.hexagon::before {
  background-color: inherit;
  content: "";
  position: absolute;
  left: 0;
  transform: rotate(-60deg);
}
.hexagon::after {
  background-color: inherit;
  content: "";
  position: absolute;
  left: 0;
  transform: rotate(60deg);
}
.hexagon:nth-child(even) {
  /* top approx. 50% of .hexagon height + spacing */
  top: 73px;
}
.hexagon:hover {
  background-color: hsla(60, 75%, 75%, 1.0) !important;
  box-shadow: 5px 5px 25px rgba(0,0,0,0.2);
  cursor: pointer;
  z-index: 105;
}
.hexagon:active {
  background-color: hsla(60, 75%, 50%, 1.0);
  z-index: 110;
}
.hexagontent {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 140%;
  font-size: 1.0rem;
  line-height: 1.2;
  z-index: 100;
}
.ibws-fix {
  /* inline-block whitespace fix */
  font-size: 0;
}
.hexagon .project { display: none; }
</style>