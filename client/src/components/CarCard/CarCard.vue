<style lang="scss" src="./style.scss"></style>
<template src="./template.html"></template>
<script>
  export default {
    name: "CarListing",
    data() {
      return {
        // Check if the card is used for an owner or car page
        ownerpage: this.$route.name === "owner" ? true : false
      };
    },
    props: {
      car: Object
    },
    methods: {
      // View the car page
      viewCar(id) {
        this.$router.push({ name: "car", params: { id: id } });
      },
      // View the owner page
      viewOwner(id) {
        this.$router.push({ name: "owner", params: { id: id } });
      }
    }
  };
</script>