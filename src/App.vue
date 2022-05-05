<template>
 <section>
  <add-friend @new-friend="addNewFriend"></add-friend>
  <ul>
   <friend-contact
    v-for="friend of friends"
    :key="friend.id"
    :name="friend.name"
    :phone-number="friend.phone"
    :email-address="friend.email"
    :is-favorite="friend.isFavorite"
    :id="friend.id"
    @toggle-favorite="toggleFavoriteStatus"
    @remove-friend="removeFriend"
   ></friend-contact>
  </ul>
 </section>
</template>

<script>
export default {
 data() {
  return {
   friends: [],
  };
 },
 methods: {
  toggleFavoriteStatus(friendId) {
   const identifiedFriend = this.friends.find(
    (friend) => friend.id === friendId
   );
   identifiedFriend.isFavorite = !identifiedFriend.isFavorite;
  },
  addNewFriend(name, phone, email) {
   const newFriendContact = {
    id: Math.random().toString(),
    name: name,
    phone: phone,
    email: email,
    isFavorite: false,
   };
   this.friends.push(newFriendContact);
  },
  removeFriend(friendId) {
   this.friends = this.friends.filter((friend) => friend.id !== friendId);
  },
 },
};
</script>

<style>
* {
 box-sizing: border-box;
}
html {
 font-family: "Jost", sans-serif;
}

body {
 margin: 0;
}

#app ul {
 margin: 0;
 padding: 0;
 list-style: none;
}

#app li,
#app form {
 box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
 margin: 1rem auto;
 padding: 1rem;
 text-align: center;
 width: 90%;
 max-width: 40rem;
}

#app h2 {
 font-size: 2rem;
 border-bottom: 2px solid #ccc;
 color: #003558;
 margin: 0 0 1rem 0;
}

#app button {
 font: inherit;
 cursor: pointer;
 border: 1px solid #008cff;
 background-color: #008cff;
 color: white;
 padding: 0.05rem 1rem;
 margin: 0.05rem 0.5rem;
 box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.26);
}

#app button:hover,
#app button:active {
 background-color: #31a1ec;
 border-color: #31a1ec;
 box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
}

#app input {
 font: inherit;
 padding: 0.15rem;
}

#app label {
 display: inline-block;
 font-weight: bold;
 margin-right: 1rem;
 width: 7rem;
}

#app form div {
 margin: 1rem 0;
}
</style>
