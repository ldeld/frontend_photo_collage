<template>
  <div id="images-holder">
    <p>Loading....</p>
  </div>
</template>

<script>
export default {
  props: {
    collageId: {
      type: Number,
      required: true
    }
  },
  created() {
    this.pollCollageStatus();
  },
  methods: {
    async pollCollageStatus() {
      console.log("polling....");
      const response = await fetch(`api/collages/${this.collageId}/status`)
      if (response.status === 200) {
        const data = await response.json();
        this.$emit('collage-finished', data.url)
      } else if (response.status === 202) {
        setTimeout(this.pollCollageStatus, 1000);
      } else {
        alert(`something unexpected, status ${response.status}`)
      }
    }
  }
}
</script>

<style>

</style>