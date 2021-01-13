<template>
  <div class="home">
    <transition name="toast">
      <Toast v-if="showToast" />
    </transition>
    <Todos @badValue="triggerToast" />
    <button @click="showP = !showP">toggle</button>
  </div>
</template>

<script>
import { ref } from 'vue'
import Toast from '../components/Toast'
import Todos from '../components/Todos'

export default {
  components: { Toast, Todos },
  setup() {
    const showToast = ref(false)

    const triggerToast = () => {
      showToast.value = true;
      setTimeout(() => showToast.value = false, 3000)
    }

    return { showToast, triggerToast }
  }
}
</script>

<style>
  /* enter transitions */
  .toast-enter-from {
    opacity: 0;
    transform: translateY(-60px);
  }
  /* .toast-enter-to {
    opacity: 1;
    transform: translateY(0);
  } */
  .toast-enter-active {
    transition: all 0.3s ease;
  }
  /* leave transitions */
  /* .toast-leave-from {
    opacity: 1;
    transform: translateY(0);
  } */
  .toast-leave-to {
    opacity: 0;
    transform: translateY(-60px);
  }
  .toast-leave-active {
    transition: all 0.3s ease;
  }
</style>