<template>
  <div class="home">
    <Menu :user="user" />
    <p v-if="user">Feed goes here later. </p>
    <Login v-else />
  </div>
</template>

<script>
import axios from 'axios';
import Login from '@/components/Login.vue'
import Menu from '@/components/Menu.vue'

export default {
  name: 'home',
  components: {
    Login,
    Menu,
  },
  data() {
    return {
      posts: [],
    }
  },
  async created() {
    try {
      let response = await axios.get('/api/users');
      this.$root.$data.user = response.data.user;
      //this.posts = await axios.get('/api/posts/following/:id')
    } catch (error) {
      this.$root.$data.user = null;
    }
  },
  computed: {
    user() {
      return this.$root.$data.user;
    }
  }
}
</script>
