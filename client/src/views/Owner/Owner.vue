<style lang="scss" src="./style.scss"></style>
<template src="./template.html"></template>
<script>
  // Import External dependencies
  import { gql } from "apollo-boost"
  // Import Components
  import Header from "@/components/Header/Header.vue"
  import CarCard from "@/components/CarCard/CarCard.vue"
  // Create Get Owner Query
  const getOwner = gql`
    query getOwner($id: ID!) {
      owner(id: $id) {
        email
        firstName
        lastName
        cars {
          _id
          age
          brand
          price
          title
        }
      }
    }
  `;
  export default {
    name: "owner",
    data() {
      return {
        owner: {}
      };
    },
    props: ['id'],
    components: {
      Header,
      CarCard
    },
    computed: {
      fullTitle: function() {
        return this.owner.firstName + " " + this.owner.lastName
      }
    },
    apollo: {
      owner: {
        query: getOwner,
        variables() {
          return {
            id: this.id
          };
        }
      }
    },
    methods: {
      goHome() {
        this.$router.push({ name: "home" })
      }
    }
  };
</script>