<template src="./template.html"></template>
<script>
  // Import External dependencies
  import { gql } from "apollo-boost";
  // Create Edit Car Query
  const editCar = gql`
    mutation editCar(
      $id: ID!
      $title: String!
      $brand: String!
      $age: Int!
      $price: String!
    ) {
      editCar(id: $id, title: $title, brand: $brand, age: $age, price: $price) {
        _id
        title
        brand
        age
        price
        services {
          date
          name
        }
      }
    }
  `;
  export default {
    name: "EditCar",
    props: {
      car: Object
    },
    data() {
      let car = this.car
      return {
        form: {
          id: car._id,
          title: car.title,
          brand: car.brand,
          age: car.age,
          price: car.price
        }
      };
    },
    methods: {
      async onSubmit(evt) {
        evt.preventDefault()
        const data = this.form
        const updatedCar = await this.$apollo.mutate({
          mutation: editCar,
          variables: { ...data }
        })
        this.$store.commit("car", updatedCar.data.editCar)
        this.$refs["my-modal"].hide()
      }
    }
  };
</script>