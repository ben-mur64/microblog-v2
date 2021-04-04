<template>
  <div class="discover">
    <Menu :user="user" />
    <div v-if="user">
      <div class="container" v-for="a in foundUsers" v-bind:key="a._id">
        <input v-model="find" placeholder="Search" class="form-control">
        <hr />
        <div class="row">
          <div class="col"><p>Name: {{a.firstName}} {{a.lastName}}</p></div>
          <div class="col"><p>Bio: {{a.bio}}</p></div>
          <div class="col"><button class="pure-button pure-button-primary" @click="follow(a)">Follow</button></div>
        </div>
      </div>
    </div>
    <Login v-else />
  </div>
</template>

<script>
import axios from 'axios';
import Login from '@/components/Login.vue'
import Menu from '@/components/Menu.vue'

export default {
  name: 'Discover',
  components: {
    Login,
    Menu,
  },
  data() {
    return {
      users: [],
      find: '',
    }
  },
  async created() {
    this.getUsers();
  },
  computed: {
    user() {
      return this.$root.$data.user;
    },
    foundUsers() {
      let us1 = this.users.filter(u => u.firstName.toLowerCase().startsWith(this.find.toLowerCase()));
      return us1;
    }
  },
   methods: {
    async getUsers() {
      try {
        let response = await axios.get('/api/users');
        this.$root.$data.user = response.data.user;

        let r2 = await axios.get('/api/users/all');
        console.log(r2);
        this.users = r2.data;
      } catch (error) {
        this.$root.$data.user = null;
      }
    },
    async follow(a) {
      try {
        await axios.post('/api/users/follow/' + a._id);
        this.getUsers();
      } catch (error) {
        console.log(error);
      }
    }
  }
}
</script>
