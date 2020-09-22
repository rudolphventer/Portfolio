<template>
<!-- A blank component that allows me to pass html as a prop -->
 <div>{{html}}</div>
    
</template>

<script>
export default {
  name: 'BlankComponent',
  props: {
      html: String
  }
    
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
