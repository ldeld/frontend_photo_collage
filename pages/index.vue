<template>
  <div id="app">
    <OptionsForm :images="images" @collage-submitted="updateStatusToPending"/>
    <ImagesHolder v-if="status === 'creating'" :images="images" @new-image-added="addImage"/>
    <Loader v-else-if="status === 'pending'" :collage-id="collageId" @collage-finished="updateStatusToDone"/>
    <CollageContainer v-else-if="status === 'done'" :collage-url="collageUrl"/>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        images: [],
        status: 'creating',
        collageId: null,
        collageUrl: null
      }
    },
    methods: {
      addImage(image) {
        this.images.push(image);
      },
      updateStatusToPending(collageId) {
        this.collageId = collageId;
        this.status = 'pending';
      },
      updateStatusToDone(collageUrl) {
        console.log("updating to done", collageUrl)
        this.collageUrl = collageUrl;
        this.status = 'done';
      }
    }
  }
</script>

<style>
  * {
    margin: 0;
    box-sizing: border-box;
  }

  :root {
    --light-grey: rgb(221, 221, 221);
    --primary: #5F5EAD;
}

  #app {
    background-color: #F4F7FF;
    padding: 4rem 6rem;
    height: 100vh;
    width: 100vw;
    display: flex;
    justify-content: space-between;
  }

  h1, h2, h3, h4 {
    color: var(--primary);
  }

  h2 {
    font-size: 1.5rem;
    margin-bottom: 1rem;
  }

  .content-container {
    height: 80%;
    background-color: white;
    border-radius: 15px;
    box-shadow: var(--light-grey) 2px 2px 4px;
    padding: 1rem;
  }
</style>