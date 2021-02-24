<template>
  <button class="skittish-button">
    <svg
        class="skittish-button__background"
        viewBox="0 0 300 200"
        preserveAspectRatio="none"
        height="100%"
        width="100%"
    >
      <path
          d="M50,50 L250,50 L250,150 L50,150 Z"
          class="skittish-button__background-layer"
          fill="rgb(120, 235, 237)"
          ref="path1"
      ></path>
      <path
          d="M50,50 L250,50 L250,150 L50,150 Z"
          class="skittish-button__background-layer"
          fill="rgb(219, 51, 65)"
          ref="path2"
      ></path>
    </svg>
    <span class="skittish-button__label">A cool label for the button</span>
  </button>
</template>

<script>
import anime from 'animejs';

export default {
  name: 'SkittishButton',
  data() {
    return {
      bounds: {
        topLeft: {
          x: { min: 0, max: 50 },
          y: { min: 0, max: 50 },
        },
        topRight: {
          x: { min: 250, max: 300 },
          y: { min: 0, max: 50 },
        },
        bottomRight: {
          x: { min: 250, max: 300 },
          y: { min: 150, max: 200 },
        },
        bottomLeft: {
          x: { min: 0, max: 50 },
          y: { min: 150, max: 200 },
        },
      },
      speed: 150,
    };
  },
  methods: {
    updateSkit() {
      [this.$refs.path1, this.$refs.path2].map(path => {
        let state = {};
        Object.keys(this.bounds).map(corner => {
          state[corner] = {
            x: anime.random(this.bounds[corner].x.min, this.bounds[corner].x.max),
            y: anime.random(this.bounds[corner].y.min, this.bounds[corner].y.max),
          };
        });

        anime({
          targets: path,
          d: `M${state.topLeft.x},${state.topLeft.y} L${state.topRight.x},${state.topRight.y} L${state.bottomRight.x},${state.bottomRight.y} L${state.bottomLeft.x},${state.bottomLeft.y} Z`,
          duration: this.speed,
          easing: 'linear'
        });
      });
    }
  },
  mounted() {
    // prefers-reduced-motion indicates that we should not animate the button
    if (!window.matchMedia('(prefers-reduced-motion)').matches) {
      setInterval(this.updateSkit, this.speed)
    }
  }
}
</script>

<style scoped>
.skittish-button {
  background: none;
  border: none;
  display: grid;
  height: 100px;
  grid-template-columns: max-content;
  align-items: center;
}

.skittish-button > * {
  grid-column: 1;
  grid-row: 1;
}

.skittish-button__label {
  padding: 50px 100px;
}

.skittish-button__background-layer {
  mix-blend-mode: lighten;
}
</style>
