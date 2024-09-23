<template>
    <div>
      <img v-if="imageUrl" :src="imageUrl" alt="Fetched Image" />
      <p v-else>Loading image...</p>
    </div>
</template>
  
  <script>
  export default {
    props: {
      selectedObject: {
        required: true,
      },
    },
    data() {
      return {
        imageUrl: '',
      };
    },
    watch: {
        selectedObject: 'fetchImage', // Watch for changes to objectId
    },
    async created() {
      await this.fetchImage(); // Fetch image on component creation
    },
    methods: {

        // selectRandomImage() {
        // const randomIndex = Math.floor(Math.random() * this.objectIds.length);
        // const randomObjectId = this.objectIds[randomIndex];
        // this.fetchImage(randomObjectId);
        // },

        async fetchImage() {    
            try {
            // const response = await fetch(`https://collectionapi.metmuseum.org/public/collection/v1/objects/${this.selectedObjectId}`);
            // const data = await response.json();
            this.imageUrl = this.selectedObject.primaryImageSmall;
            // if (data.primaryImageSmall) {
            //     this.imageUrl = data.primaryImageSmall;
            // } else {
            //     //sometime the imageurl is blank even though I filtered it, so just call the method again
            //     this.fetchImage();
            // }
            } catch (error) {
            console.error('Error fetching the image:', error);
            }
        },
        },
  };
  </script>
  