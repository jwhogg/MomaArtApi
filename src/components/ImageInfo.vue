<template>
<p> {{ this.selectedObject.artistDisplayName || "Unidentified artist" }}</p>
<p> {{ this.selectedObject.title }}</p>
<p> {{ this.selectedObject.accessionYear }}</p>
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
    };
  },
}
</script>