<template>
  <div class="about">
    <transition
      appear
      @before-enter="beforeEnter"
      @enter="enter"
      :css="false"
    >
      <h1 v-if="showTitle">About</h1>
    </transition>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
  </div>
</template>

<script>
import { ref } from 'vue'
import gsap from 'gsap'

export default {
  setup() {
    const showTitle = ref(true)

    const beforeEnter = (el) => {
      console.log('before enter - set intial state')
      el.style.transform = 'translateY(-60px)'
      el.style.opacity = 0
    }
    const enter = (el, done) => {
      console.log('starting to enter - make transition')
      gsap.to(el, {
        duration: 1,
        y: 0,
        opacity: 1,
        ease: 'bounce.out',
        onComplete: done
      })
    }

    return { beforeEnter, enter, showTitle }
  }
}
</script>

<style>
  .about {
    max-width: 600px;
    margin: 20px auto;
  }
</style>