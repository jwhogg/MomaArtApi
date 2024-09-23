<template>
    <h2>Image from API</h2>
  <div>
    <ReloadPageButton/>
  </div>
  <div>
    <DisplayImage v-if="selectedObject" :selectedObject="selectedObject" />
    <p v-else>Loading image...</p>
  </div>
  <div>
    <ImageInfo v-if="selectedObject" :selectedObject="selectedObject" />
    <p v-else></p>
  </div>
</template>

<script>
import DisplayImage from './DisplayImage.vue';
import ImageInfo from './ImageInfo.vue';
import ReloadPageButton from './ReloadPageButton.vue';

export default {
  components: {
    DisplayImage,
    ImageInfo,
    ReloadPageButton
  },
  data() {
    return {
        selectedObject: '',
        objectIds: [],
    };
  },
  async created() {
    await this.loadObjectIds();
    this.selectRandomObject();
  },
  methods: {

    async selectRandomObject() {
      const randomIndex = Math.floor(Math.random() * this.objectIds.length);
      const tempSelectedObjectId = this.objectIds[randomIndex];

      //check the image url isnt blank
      const response = await fetch(`https://collectionapi.metmuseum.org/public/collection/v1/objects/${tempSelectedObjectId}`);
      const data = await response.json();
      if (! data.primaryImageSmall) {
        this.selectRandomObject();
      }
      this.selectedObject = data;

    },

    loadObjectIds() {
      const cachedObjectIds = localStorage.getItem('objectIds');

      if (cachedObjectIds) {
        this.objectIds = JSON.parse(cachedObjectIds);
      } else {
        this.fetchObjectIds();
      }
    },
    async fetchObjectIds() {
      try {
        const response = await fetch('https://collectionapi.metmuseum.org/public/collection/v1/objects');

        if (!response.ok) {
          throw new Error('Network response was not ok');
        }

        const data = await response.json();
        this.objectIds = data.objectIDs || [];
        
        localStorage.setItem('objectIds', JSON.stringify(this.objectIds)); // Cache in localStorage
      } catch (error) {
        console.error('Error fetching image IDs:', error);
      }
    },
  },
};
</script>
