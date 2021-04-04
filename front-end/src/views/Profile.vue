<template>
  <div class="profile">
    <Menu :user="user" />
    <div v-if="user">
      <h3>{{user.firstName}} {{user.lastName}}</h3>
      <p class="bio">Bio: {{user.bio}}</p>
      <form class="pure-form">
        <fieldset>
          <legend>Update account details:</legend>
          <input placeholder="First Name" v-model="firstName">
          <input placeholder="Last Name" v-model="lastName">
        </fieldset>
        <fieldset>
          <textarea placeholder="Biography" v-model="bio" />
          <button type="submit" class="pure-button pure-button-primary" @click.prevent="updateUser">Update Info</button>
        </fieldset>
      </form>
    </div>
    <Login v-else />
  </div>
</template>

<script>
import axios from 'axios';
import Login from '@/components/Login.vue'
import Menu from '@/components/Menu.vue'

export default {
  name: 'Profile',
  components: {
    Login,
    Menu,
  },
  data() {
    return {
      firstName: '',
      lastName: '',
      bio: '',
    }
  },
  async created() {
    try {
      let response = await axios.get('/api/users');
      this.$root.$data.user = response.data.user;
    } catch (error) {
      this.$root.$data.user = null;
    }
  },
  methods: {
    async updateUser() {
      try {
        let response = await axios.put('/api/users', {
          firstName: this.firstName,
          lastName: this.lastName,
          bio: this.bio,
        });
        console.log(response.data.user);
        this.$root.$data.user = response.data;
      } catch (error) {
        console.log(error)
      }
    }
  },
  computed: {
    user() {
      return this.$root.$data.user;
    }
  }
}
</script>
