<style lang="scss" src="./style.scss"></style>
<template src="./template.html"></template>
<script>
  // Import External dependencies
  import { mapState } from "vuex";
  // Import Components
  import CarCard from "@/components/CarCard/CarCard.vue";
  import Header from "@/components/Header/Header.vue";
  export default {
    name: "home",
    components: { CarCard, Header },
    // Get data from store
    computed: mapState({
      carData: state => state.carData
    })
  };
</script>