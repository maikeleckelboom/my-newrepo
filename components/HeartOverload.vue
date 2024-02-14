<script lang="ts" setup>
const colors = ["#e03776", "#8f3e98", "#4687bf", "#3bab6f", "#f9c25e", "#f47274"];
const SVG_NS = 'http://www.w3.org/2000/svg';
const SVG_XLINK = "http://www.w3.org/1999/xlink";


onMounted(() => {

  const hearts = document.getElementById('hearts');
  let heartsRy: any[] = []

  function useTheHeart(n: number) {
    let use = document.createElementNS(SVG_NS, 'use');
    use.n = n;
    use.setAttributeNS(SVG_XLINK, 'xlink:href', '#heart');
    use.setAttributeNS(null, 'transform', `scale(${use.n})`);
    use.setAttributeNS(null, 'fill', colors[n % colors.length]);
    use.setAttributeNS(null, 'x', String(-69));
    use.setAttributeNS(null, 'y', String(-16));
    use.setAttributeNS(null, 'width', String(138));
    use.setAttributeNS(null, 'height', String(138));

    heartsRy.push(use)
    hearts?.appendChild(use)
  }

  for (let n = 18; n >= 0; n--) {
    useTheHeart(n)
  }

  function Frame() {
    window.requestAnimationFrame(Frame);
    for (let i = 0; i < heartsRy.length; i++) {
      if (heartsRy[i].n < 18) {
        heartsRy[i].n += .01
      } else {
        heartsRy[i].n = 0;
        hearts?.appendChild(heartsRy[i])
      }
      heartsRy[i].setAttributeNS(null, 'transform', `scale(${heartsRy[i].n})`);
    }
  }

  Frame()
})
</script>
<template>
  <svg id="hearts" ref="heartsRef" preserveAspectRatio="xMidYMid slice" viewBox="-600 -400 1200 800">
    <defs>
      <symbol class="heart" id="heart" viewBox="-69 -16 138 138">
        <path d="M0,12
             C 50,-30 110,50  0,120
             C-110,50 -50,-30 0,12z"/>
      </symbol>
    </defs>
  </svg>
</template>

<style>
#__nuxt {
  display: flex;
  align-items: center;
  height: 100%;
  justify-content: center;
}

body {

  margin: 0;
  padding: 0;
  overflow: hidden;
}

#heart {
  height: 100svh;

}

#hearts {
  width: 100svw;
  position: fixed;
  background-color: #fae1dd;
  top: 0;
}
</style>
