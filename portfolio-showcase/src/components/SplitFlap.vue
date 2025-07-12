<template>
    <div id="display" class="flex justify-center items-center">
      <div
        v-for="(letter, index) in displayLetters"
        :key="index"
        class="split-flap relative inline-block"
      >
        <!-- Top half of the flap -->
        <div class="flap-top">
          <span :class="['letter', { 'flip-top': flipState[index].top }]">
            {{ letter }}
          </span>
        </div>
  
        <!-- Bottom half of the flap -->
        <div class="flap-bottom">
          <span :class="['letter', { 'flip-bottom': flipState[index].bottom }]">
            {{ letter }}
          </span>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue'
  
  const props = defineProps({
    text: {
      type: String,
      default: 'HELLO'
    }
  })
  
  // Reactive array for the currently displayed letters
  const displayLetters = ref(Array.from(props.text, () => ' '))
  
  // Each letter’s flip state (top/bottom) for animation
  const flipState = ref(
    Array.from(props.text, () => ({
      top: false,
      bottom: false
    }))
  )
  
  // Returns a random character (A–Z or space)
  function getRandomChar() {
    const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ '
    return chars[Math.floor(Math.random() * chars.length)]
  }
  
  onMounted(() => {
    props.text.split('').forEach((targetLetter, index) => {
      animateFlap(index, targetLetter)
    })
  })
  
  function animateFlap(index, targetLetter) {
    let iterations = 0
    const delay = 100 + index * 20
    const interval = setInterval(() => {
      iterations++
      displayLetters.value[index] = getRandomChar()
  
      // Trigger flip animations on both halves
      flipState.value[index].top = true
      flipState.value[index].bottom = true
  
      // Remove flip classes after the animation ends
      setTimeout(() => {
        flipState.value[index].top = false
        flipState.value[index].bottom = false
      }, 300)
  
      // After enough random flips, show the final letter
      if (iterations > 10) {
        clearInterval(interval)
        displayLetters.value[index] = targetLetter
      }
    }, delay)
  }
  </script>
  
  <style scoped>
  /* Container for each letter (total height = 70px) */
  .split-flap {
    position: relative;
    width: 50px;
    height: 70px;
    margin: 0 5px;
    font-family: 'Courier New', Courier, monospace;
    perspective: 600px;
  }
  
  /* TOP HALF */
  .flap-top {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 35px; /* half of total 70px */
    background: #333; /* black-ish */
    color: #fff;
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
    border-bottom: 1px solid #fff;
    overflow: hidden; /* Only show top half of the letter */
  }
  
  /* BOTTOM HALF */
  .flap-bottom {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 35px; /* half of total 70px */
    background: #333;
    color: #fff;
    border-bottom-left-radius: 5px;
    border-bottom-right-radius: 5px;
    border-top: 1px solid #f9f9f9;
    overflow: hidden; /* Only show bottom half of the letter */
  }
  
  /* The letter itself is 70px tall but we only show half in each container. */
  .letter {
    display: inline-block;
    width: 100%;
    height: 70px; 
    line-height: 70px;
    font-size: 48px;
    text-align: center;
    backface-visibility: hidden;
  }
  
  /* 
    By default, the top container sees the top half of the letter (no shift).
    The bottom container sees the bottom half by shifting the letter up 35px.
  */
  .flap-top .letter {
    transform: translateY(0);
  }
  .flap-bottom .letter {
    transform: translateY(-35px);
  }
  
  /* Flip Animations */
  .flip-top {
    animation: flipTop 0.6s ease-out forwards;
    transform-origin: bottom center; /* hinge at bottom edge */
  }
  .flip-bottom {
    animation: flipBottom 0.6s ease-out forwards;
    transform-origin: top center; /* hinge at top edge */
  }
  
  /* Keyframes for top half flipping down */
  @keyframes flipTop {
    0% {
      transform: translateY(0) rotateX(0deg);
    }
    50% {
      transform: translateY(0) rotateX(-90deg);
    }
    100% {
      transform: translateY(0) rotateX(0deg);
    }
  }
  
  /* Keyframes for bottom half flipping up */
  @keyframes flipBottom {
    0% {
      transform: translateY(-35px) rotateX(0deg);
    }
    50% {
      transform: translateY(-35px) rotateX(90deg);
    }
    100% {
      transform: translateY(-35px) rotateX(0deg);
    }
  }
  </style>
  