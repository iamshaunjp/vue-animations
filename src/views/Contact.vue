<template>
  <div class="contact">
    <h1>Contact</h1>
    <ul>
      <li v-for="icon in icons" :key="icon.name">
        <span class="material-icons">{{ icon.name }}</span>
        <div>{{ icon.text }}</div>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    const icons = ref([
      { name: 'alternate_email', text: 'by email'},
      { name: 'local_phone', text: 'by phone'},
      { name: 'local_post_office', text: 'by post'},
      { name: 'local_fire_department', text: 'by smoke signal'},
    ])

    return { icons }
  }
}
</script>

<style>
  .contact ul {
    padding: 0;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
    max-width: 400px;
    margin: 60px auto;
  }
  .contact li {
    list-style-type: none;
    background: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 1px 3px 5px rgba(0,0,0,0.1);
    cursor: pointer;
    line-height: 1.5em;
  }
</style>