<template>
<div class="error col-12 d-flex align-items-center justify-content-center mt-3">
 <div class="alert alert-danger d-flex align-items-center justify-content-center" role="alert">
  <svg class="bi flex-shrink-0 me-2" width="24" height="24" role="img" aria-label="Danger:"><use xlink:href="#exclamation-triangle-fill"/></svg>
  <div>
   {{text}}
  </div>
</div>
</div>
</template>

<script>
export default {
    props: ["text"]
  
}
</script>

<style scoped>


</style>