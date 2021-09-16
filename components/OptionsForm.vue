<template>
  <div id="options-form-container" class="content-container">
    <form ref="optionsForm" @submit.prevent="submitForm">
      <div class="form-section">
        <h2>Orientation</h2>
        <div class="form-control-radioboxes">
          <div class="radio-input">
            <input id="orientation-horizontal" v-model="orientation" type="radio" name="collage[orientation]" value ="horizontal">
            <label for="orientation-horizontal">Horizontal</label>
          </div>
          <div class="radio-input">
            <input id="orientation-vertical"  v-model="orientation" type="radio" name="collage[orientation]" value="vertical">
            <label for="orientation-vertical">Vertical</label>
          </div>
        </div>
      </div>
      <div class="form-section">
        <h2>Border</h2>
        <div class="text-input">
          <label for="border-size">Border size</label>
          <input id="border-size" v-model="borderSize" type="text" name="collage[border_size]">
          <p class="input-units">px</p>
        </div>
        <div class="text-input">
          <label for="border-color">Border Color</label>
          <p class="input-units">#</p>
          <input id="border-color" v-model="borderColor" type="text" name="collage[border_color]">
        </div>
      </div>
      <div class="form-section">
        <input type="submit" value="Generate collage">
      </div>
    </form>
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
      orientation: "horizontal", // default orientation
      borderSize: 0,
      borderColor: "FFFFFF"
    }
  },
  methods: {
    async submitForm() {
      // Handle form submission
      // add images to form data
      const data = new FormData(this.$refs.optionsForm);
      this.images.forEach((image) => { data.append("collage[collage_elements_attributes][][image]", image, image.name) });
      // todo: change url to env var
      const raw = await fetch('api/collages', { method: 'POST', body: data })
      const response = await raw.json();
      console.log(response);
    },
  },
}
</script>

<style scoped>
  #options-form-container {
    flex: 0 1 30%;
  }

  .form-section {
    margin-bottom: 1.5em;
  }

  input {
    border: 1px solid var(--light-grey);
    border-radius: 4px;
  }

  .text-input {
    margin-bottom: 1em;
  }

  .input-units {
    display: inline;
    opacity: 0.8;
  }
</style>