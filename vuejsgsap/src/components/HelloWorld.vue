<template>

  <!-- <div ref="box" class="box"></div> -->

  <div class="container">
    <div class="wrapper">


      <!-- <div class="bubble-wrapper">
      <div ref="bubble" class="bubble">
      <img class="bubble-image" src="https://s3.ap-southeast-2.amazonaws.com/daily-fire-assets/slack-white.svg" />
    </div>
    <div ref="bubblePulse" class="bubble-pulse"></div>
  </div> -->

  <div class="bubble-wrapper">
    <div ref="slackBubble" class="bubble">
      <img class="bubble-image" :src="currentLogo" />
    </div>
    <div ref="slackBubblePulse" class="bubble-pulse"></div>
  </div>


</div>


<button @click="randomiseLogo">Random Logo</button>
</div>



</template>

<script>
import { TimelineLite, Back, Elastic, Expo } from 'gsap'


export default {
  name: 'HelloWorld',
  data () {
    return {
      timeline: null,
      logos: [
        'https://s3.ap-southeast-2.amazonaws.com/daily-fire-assets/slack-white.svg',
        'https://s3.ap-southeast-2.amazonaws.com/daily-fire-assets/discord-white.svg',
        'https://s3.ap-southeast-2.amazonaws.com/daily-fire-assets/messenger-white.png',
      ],
      currentLogo: '',
    }
  },
  methods: {
    randomiseLogo() {
      const logosToSample = this.logos.filter(logo => logo !== this.currentLogo);

      this.currentLogo = logosToSample[Math.floor(Math.random() * logosToSample.length)];
    }
  },
  mounted() {

    // // For box animation.
    // const { box } = this.$refs;
    // const timeline = new TimelineLite();
    //
    // timeline.to(box, 1, {
    //   x: 200,
    //   rotation: 90,
    //   ease: Back.easeInOut,
    // })
    // timeline.to(box, 0.5, {
    //   background: 'salmon'
    // }, '-=0.5'); // Run change color animation 0.5s early




    // // For logo animation.
    // const { bubble, bubblePulse } = this.$refs;
    // const timeline = new TimelineLite();
    //
    // this.timeline = new TimelineLite({
    //   // onComplete: () => this.timeline.restart()
    // });
    //
    // timeline.to(bubble, 0.4, {
    //   scale: 0.8,
    //   rotation: 16,
    //   ease: Back.easeOut.config(1.7),
    // });
    //
    // timeline.to(bubblePulse, 0.5, {
    //   scale: 0.9,
    //   opacity: 1,
    // }, '-=0.6');
    //
    // this.timeline.to(bubble, 1.2, {
    //   scale: 1,
    //   rotation: '-=16',
    //   ease: Elastic.easeOut.config(2.5, 0.5),
    // });
    //
    // this.timeline.to(bubblePulse, 1.1, {
    //   scale: 3,
    //   opacity: 0,
    //   ease: Expo.easeOut,
    // }, '-=1.2')



    // Call the random logo method.
    this.randomiseLogo();

    const { slackBubble, slackBubblePulse } = this.$refs;

    this.timeline = new TimelineLite({
      onComplete: () => {
        this.timeline.restart(),
        this.randomiseLogo()
      }
    });

    // Zoom in.
    this.timeline.to(slackBubble, 0.4, {
      scale: 0.8,
      rotation: 16,
      ease: Back.easeOut.config(1.7)
    });

    this.timeline.to(slackBubblePulse, 0.8, {
      scale: 0.8,
      opacity: 1
    }, '-=0.6');

    // Zoom out.
    this.timeline.to(slackBubble, 1.2, {
      scale: 1,
      rotation: '-=16',
      ease: Elastic.easeOut.config(2.5, 0.5)
    });

    this.timeline.to(slackBubblePulse, 1.1, {
      scale: 3,
      opacity: 0,
      ease: Expo.easeOut
    }, "-=1.2");



  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bubble-wrapper {
  position: relative;
}

.bubble {
  position: relative;
  z-index: 2;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid white;
  background: #272727;
  border-radius: 50%;
  height: 100px;
  width: 100px;
}

.bubble-pulse {
  position: absolute;
  z-index: 1;
  height: 120px;
  width: 120px;
  top: 50%;
  left: 50%;
  margin-top: -60px;
  margin-left: -60px;
  background: #272727;
  border-radius: 50%;
  opacity: 0;
  transform: scale(0);
}

.bubble-image {
  height: 50%;
}

.wrapper {
  padding-top: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
}

button {
  position: relative;
  z-index: 50;
  background-color: #fff;
  padding: 1em;
  left: 50%;
  transform: translate(-50%);
  margin: 40px auto;
  font-size: 1em;
  border: none;
}

.container {
  background: #1a1a1a;
  max-width: 600px;
}



</style>
