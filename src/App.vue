<template>
  <div class="container">
    <div class="block" :class="{ animate: animatedBlock }"></div>
    <button @click="animateBlock">Animate</button>
  </div>
  <div class="container">
    <transition name="para">
      <!-- The transition component can only have one child. It is a component provided by vue to help create animations and can be useful for creating animation on elements that disappear. If you have multiple transition components, you can use the name prop to differentiate them. So instead of .v-enter-from , it will be para-enter-from. Also if for some reason you need to use custom class names for v-enter-from, v-enter-to, etc. you can do so by using the prop = enter-to-class="your-class-name" and same with the rest -->
      <p v-if="paraIsVisible">This is only sometimes visible...</p>
    </transition>
    <button @click="toggleParagraph">Toggle Paragraph</button>
  </div>
  <base-modal @close="hideDialog" v-if="dialogIsVisible">
    <p>This is a test dialog!</p>
    <button @click="hideDialog">Close it!</button>
  </base-modal>
  <div class="container">
    <button @click="showDialog">Show Dialog</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dialogIsVisible: false,
      animatedBlock: false,
      paraIsVisible: false,
    };
  },
  methods: {
    animateBlock() {
      this.animatedBlock = true;
    },
    showDialog() {
      this.dialogIsVisible = true;
    },
    hideDialog() {
      this.dialogIsVisible = false;
    },
    toggleParagraph() {
      this.paraIsVisible = !this.paraIsVisible;
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  font-family: sans-serif;
}
body {
  margin: 0;
}
button {
  font: inherit;
  padding: 0.5rem 2rem;
  border: 1px solid #810032;
  border-radius: 30px;
  background-color: #810032;
  color: white;
  cursor: pointer;
}
button:hover,
button:active {
  background-color: #a80b48;
  border-color: #a80b48;
}
.block {
  width: 8rem;
  height: 8rem;
  background-color: #290033;
  margin-bottom: 2rem;
}
.container {
  max-width: 40rem;
  margin: 2rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 2rem;
  border: 2px solid #ccc;
  border-radius: 12px;
}

.animate {
  transform: translateX(
    -150px
  ); /* Moves the element to the left, the higher the negative number - the higher the increase in space the element moves to the left. If the number is a positive, then vice versa */
  /* transition: transform 0.3s ease-out;  A css property that creates a smoother transition, choose transform since that is the animation*/
  animation: slide-fade 0.3s ease-out forwards; /* forwards means to make sure that after the animation, the element should stay in the position created by the animation*/
}

/* These are all classes provided by the transition tag */
/* Animation for when the element appears */
.para-enter-from {
  /* opacity: 0;
  transform: translateY(-30px); */
}

.para-enter-active {
  /* For the active classes add the transition property to watch for all  css properties that might be animated */
  /* transition: all 0.3s ease-out; */
  animation: slide-scale 0.3s ease-out; /* animation css property chooses which animation to execute. So you can use css animation with the transition component*/
}

.para-enter-to {
  /* opacity: 1;
  transform: translateY(0); */
}
/* Animation for when the element disappears */
.para-leave-from {
  /* opacity: 1;
  transform: translateY(0); */
}

.para-leave-active {
  /* transition: all 0.3s ease-out; */
  animation: slide-scale 0.3s ease-out;
}

.v-leave-to {
  /* opacity: 0;
  transform: translateY(-30px); */
}
/* keyframes is a more configurable way of addidng animations */
@keyframes slide-scale {
  0% {
    transform: translateX(0) scale(1); /* scale means to increase the size, the percentages refer to the moments in the animation*/
  }
  70% {
    transform: translateX(-120px) scale(1.1);
  }
  100% {
    transform: translateX(-150px) scale(1);
  }
}
</style>
