<template>
    <button @click="reloadPage" class="button">New Artwork</button>
</template>
  
  <script>
  export default {
    methods: {
      reloadPage() {
        window.location.reload(); // Reload the current page
      },
    },
  };
  </script>

    <style>
        .button {
        margin-bottom: 20px; /* Adjust the spacing as needed */
        }
    </style>
  