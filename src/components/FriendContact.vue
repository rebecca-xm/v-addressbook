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
 //*  in props we decide which props this component receives,
 //*  while in emits we define which custom events the component
 //*  will at some point emit
 //  emits: ['toggle-favorite'], <= basic form
 emits: {
  "toggle-favorite": function (id) {
   return id ? true : console.warn("Id is missing");
  },
 },
 data() {
  return {
   detailsAreVisible: false,
   friend: {
    id: "manuel",
    name: "Manuel Lorenz",
    phone: "0123 45678 90",
    email: "manuel@localhost.com",
   },
  };
 },
 methods: {
  toggleDetails() {
   this.detailsAreVisible = !this.detailsAreVisible;
  },
  toggleFavorite() {
   this.$emit("toggle-favorite", this.id);
  },
 },
};

// https://vuejs.org/guide/components/props.html
</script>
