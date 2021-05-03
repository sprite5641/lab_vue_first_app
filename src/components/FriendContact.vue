<template>
  <div>
    <li>
      <h2>{{ name }} {{ isFavorite ? '(Favorite)' : ''}}</h2>
      <button @click="toggleFavorite">Toggle Favorite</button>
      <button @click="toggleDetails">{{ detailAreVisible ? 'Hide' : 'Show'}}Show Details</button>
      <ul v-if="detailAreVisible">
        <li>
          <strong>Phone:</strong>
          {{ phoneNumber }}
        </li>
        <li>
          <strong>Email:</strong>
          {{ emailAddress }}
        </li>
      </ul>
      <button @click="deleteFriend">Delete</button>
    </li>
  </div>
</template>

<script>
export default {
  // props: ["name", "phoneNumber", "emailAddress", "is-favorite"],
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
      type: String,
      required: false,
      default: "false",
      // validator: function(value) {
      //   return value === '1' || value === '0';
      // }
    },
  },
  emits: ["toggle-favorite", "delete"],
  // emits: {
  //   "toggle-favorite": function(id) {
  //     if(id) {
  //       return true;
  //     }else {
  //       console.log('id is missing!');
  //       return false;
  //     }
  //   },
  // },
  data() {
    return {
      detailAreVisible: false,
    };
  },
  methods: {
    toggleDetails() {
      this.detailAreVisible = !this.detailAreVisible;
    },
    toggleFavorite() {
      this.$emit("toggle-favorite", this.id);
    },
    deleteFriend() {
      this.$emit("delete", this.id);
    },
  },
};
</script>