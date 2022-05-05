<template>
 <form @submit.prevent="submitInfo">
  <div>
   <label>Name</label>
   <input type="text" v-model="inputName" />
  </div>
  <div>
   <label>Phone</label>
   <input type="tel" v-model="inputPhone" />
  </div>
  <div>
   <label>Email</label>
   <input type="email" v-model="inputEmail" />
  </div>
  <div>
   <button>Add Friend</button>
  </div>
 </form>
</template>

<script>
export default {
 emits: ["new-friend"],
 data() {
  return {
   inputName: "",
   inputPhone: "",
   inputEmail: "",
  };
 },
 methods: {
  submitInfo() {
   this.$emit("new-friend", this.inputName, this.inputPhone, this.inputEmail);
  },
 },
};
</script>
