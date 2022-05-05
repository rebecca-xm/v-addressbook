<template>
 <li>
  <h2>{{ name }} {{ isFavorite ? "(Favorite)" : "" }}</h2>
  <button @click="toggleDetails">
   {{ detailsAreVisible ? "Hide" : "Show" }} Details
  </button>
  <button @click="toggleFavorite">Toggle Favorite</button>
  <ul v-if="detailsAreVisible">
   <li>
    <strong>Phone:</strong>
    {{ phoneNumber }}
   </li>
   <li>
    <strong>Email:</strong>
    {{ emailAddress }}
   </li>
  </ul>
  <button @click="removeFriend">Remove</button>
 </li>
</template>

<script>
export default {
 props: {
  id: {
   type: String,
   required: true,
  },
  name: {
   type: String,
   required: true,
  },
  phoneNumber: {
   type: String,
   required: true,
  },
  emailAddress: {
   type: String,
   required: true,
  },
  isFavorite: {
   type: Boolean,
   required: false,
   default: false,
  },
 },
 emits: ["toggle-favorite", "remove-friend"],
 //  emits: {
 //   "toggle-favorite": function (id) {
 //    return id ? true : console.warn("Id is missing");
 //   }
 //  },
 data() {
  return {
   detailsAreVisible: false,
   friend: [],
  };
 },
 methods: {
  toggleDetails() {
   this.detailsAreVisible = !this.detailsAreVisible;
  },
  toggleFavorite() {
   this.$emit("toggle-favorite", this.id);
  },
  removeFriend() {
   this.$emit("remove-friend", this.id);
  },
 },
};

// https://vuejs.org/guide/components/props.html
</script>
