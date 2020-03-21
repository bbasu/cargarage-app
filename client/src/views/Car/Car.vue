<style lang="scss" src="./style.scss"></style>
<template src="./template.html"></template>
<script>
  // Import Vue dependencies
  import { gql } from "apollo-boost";
  import { mapState } from "vuex";
  // Import Components
  import Header from "@/components/Header/Header.vue";
  import EditCar from "@/components/EditCar/EditCar.vue";
  // Create Get Car Query
  const getCar = gql`
    query getCar($id: ID!) {
      car(id: $id) {
        title
        brand
        _id
        age
        services {
          date
          name
        }
        price
      }
    }
  `;
  // Create the Delete Car Query
  const deleteCar = gql`
    mutation deleteCar($id: ID!) {
      deleteCar(id: $id) {
        _id
      }
    }
  `;
  export default {
    name: "car",
    data() {
      return {
        loaded: false
      }
    },
    // Retrieved from Route params
    props: ['id'],
    computed: mapState({
      car: state => state.car,
      fullTitle: state => state.car.title + " - " + state.car.brand
    }),
    components: { Header, EditCar },
    beforeMount() {
      this.getCarDetails()
    },
    methods: {
      goHome() {
        this.$router.go(-1);
      },
      async getCarDetails() {
        try {
          // Use the ID parameter to get a single cars details
          const id = this.$route.params.id
          const response = await this.$apollo.query({
            query: getCar,
            variables: {
              id: id
            }
          });
          // Commit the response to the store
          this.$store.commit("car", response.data.car)
          this.loaded = true;
        } catch (error) {
          console.log(error);
        }
      },
      deleteCar() {
        // Use the ID parameter to delete a single car
        this.$apollo.mutate({
          mutation: deleteCar,
          variables: {
            id: this.id
          }
        })
        // Use the ID parameter to set the new state
        this.$store.commit("deleteCar", this.id)
        this.$router.push({ name: "home" })
      }
    }
  };
</script>