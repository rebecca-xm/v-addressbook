<template>
 <li>
  <!-- <h2>{{ friend.name }}</h2> -->
  <!-- <h2>{{ name }} {{ isFavorite === "1" ? "(Favorite)" : "" }}</h2> -->
  <h2>{{ name }} {{ friendIsFavorite ? "(Favorite)" : "" }}</h2>
  <button @click="toggleDetails">
   {{ detailsAreVisible ? "Hide" : "Show" }} Details
  </button>
  <button @click="toggleFavorite">Toggle Favorite</button>
  <ul v-if="detailsAreVisible">
   <!-- <li>
    <strong>Phone:</strong>
    {{ friend.phone }}
   </li>
   <li>
    <strong>Email:</strong>
    {{ friend.email }}
   </li> -->
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

<!-- 02
In order to make Vue aware of the props set in App.vue,
it'll be necessary to add a specific key in the configuration object,
the props one.
In its simplest from, it takes an array. Inside of it, we should list
the props we want to accept in this component.

Note: Vue automatically translates props written like phoneNumber in phone-number.
Here the cameCase is necessary to avoid a syntax that would not be compatible with JS
e.g. this.phone-number 
HTML: kebab-case <==> JavaScript: camelCase -->

<script>
export default {
 //  props: ["name", "phoneNumber", "emailAddress", "isFavorite"],
 props: {
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
   //  default: '0'
   default: false,
  },
 },
 // ^ to validate props and check the corrent data is being passed
 // also to set whether a prop is required or not
 data() {
  return {
   detailsAreVisible: false,
   friend: {
    id: "manuel",
    name: "Manuel Lorenz",
    phone: "0123 45678 90",
    email: "manuel@localhost.com",
   },
   friendIsFavorite: this.isFavorite,
  };
 },
 methods: {
  toggleDetails() {
   this.detailsAreVisible = !this.detailsAreVisible;
  },
  // toggleFavorite() {
  //  if (this.isFavorite === "1") {
  //   this.isFavorite = "0";
  //  } else {
  //   this.isFavorite = "1";
  //  }
  // },
  /**
   * once saved, Vue will return the following error
   *  => Unexpected mutation of "isFavorite" prop vue/no-mutating-props
   * because the data passed from App to FriendContact should only
   * be changed in App, as it violates the pattern of having a unidirectional
   * data flow.
   * Still, there are two ways of changing it.
   * First way is to let the parent component know that we'd like to change this.
   * Then the parent can go ahead and change the data in itself and pass the updated
   * data back to FriendContact.
   * The second way is that we simply take the received data as the initial data,
   * inside of FriendContact, and then we change that data inside of FriendContact,
   * being aware of the fact that we only change it there and that it won't affect
   * the data in App.vue.
   * To implement this pattern, all we need to do is to add a new data
   * property in our component, e.g. friendIsFavorite, and set it equal to
   * the received prop value. This way, we use the received prop value just
   * as an initial value for the new one.
   * This approach, though, should not be chosen as the one to go with.
   */
  toggleFavorite() {
   //  if (this.friendIsFavorite === "1") {
   //   this.friendIsFavorite = "0";
   //  } else {
   //   this.friendIsFavorite = "1";
   //  }
   this.friendIsFavorite = !this.friendIsFavorite;
  },
 },
};

// https://vuejs.org/guide/components/props.html
</script>
