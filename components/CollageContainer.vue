<template>
  <div id="images-container">
    <img :src="collageUrl" class="collage" alt="">
    <button>Download</button>
  </div>
</template>

<script>
export default {
  props: {
    collageUrl: {
      type: String, 
      required: true
    }
  }
}
</script>

<style>
  .collage {
    width: 400px;
  }
</style>