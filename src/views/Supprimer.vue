<template>
  <div>
    <h2>
      Vous allez supprimer {{ userDetail.firstName }} {{ userDetail.lastName }}
    </h2>
    <button
      class="button_supprimer"
      @click="supprimer()"
    >
      Supprimer
    </button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Supprimer',
  data() {
    return {
      id: this.$route.params.id, // this is the id from the browser
      userDetail: {},
    };
  },
  created() {
    this.detailUser();
  },
  methods: {
    detailUser() {
      axios(`https://ynov-front.herokuapp.com/api/users/${this.id}`).then(
        ({ data }) => {
          this.userDetail = data.data;
        },
      );
    },
    supprimer() {
      axios.delete(`https://ynov-front.herokuapp.com/api/users/${this.id}`);
      this.$router.push({ path: '/', params: { message: 'Modification validée' } });
    },
  },
};
</script>

<style scoped>
.image {
  width: 10%;
}
.button_supprimer {
  margin-bottom: 10px;
}
</style>
