<template>
  <div id="images-holder" class="content-container">
    <h2>Images</h2>
    <div v-for="image in images" :key="image.name" class="image-preview">
      <p>{{image.name}}</p>
    </div>
    <input id="new-image" 
      type="file" 
      name="collage[collage_elements_attributes][][image]" 
      accept="image/*"
      @change="handleNewImage">
    <label id="add-image-button" for="new-image" >Add image</label>
  </div>
</template>

<script>
export default {
  props: {
    images: {
      type: Array,
      required: true
    }
  },
  data() {
    return { 
      // images: [],
    }
  },
  methods: {
    handleNewImage(event) {
      this.$emit("new-image-added", event.target.files[0])
    }
  }
}
</script>

<style scoped>
  #images-holder {
    flex: 0 1 65%;
  }

  #new-image {
    display: none;
  }

  #add-image-button {
    padding: 1em;
    border: 1px solid var(--light-grey);
    border-radius: 4px;
    cursor: pointer;
  }
</style>