<template>
  <i :class="'ti ti-'+icon"></i>
</template>

<script>
export default {
  name: "Icon",
  props: {
    icon: String
  }
}
</script>

<style scoped>

</style>
