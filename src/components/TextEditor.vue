<template>
  <div class="container">

  </div>
</template>

<script>
export default {
  name: 'TextEditor',
  props: {},
  data() {
    return {
      textArray: [
        {
          content: "",
          x: "",
          y: "",
          font: "",
          size: "",
          lineHeight: "",
        },
      ],
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
