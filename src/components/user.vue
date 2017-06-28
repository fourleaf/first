<template>
  <div class="users">
    <h1>Users</h1>
    <form v-on:submit="addUser">
      <input type="text" v-model="newUser.name" placeholder="enter a name">
      <br/>
      <input type="text" v-model="newUser.email" placeholder="enter a email">
      <input type="submit" value="submit">
    </form>
    <ul>
      <li v-for="user in users">
        <input type="checkbox" v-model="user.contacted">
        <span :class="{contacted: user.contacted}">{{user.name}}: {{user.email}}</span>
        <button @click="delUser(user)">x</button>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'users',
    data() {
      return {
        newUser: {},
        users: []
      }
    },
    methods: {
      addUser: function (e) {
        if (this.newUser.name == null || this.newUser.email == null) {
          e.preventDefault();
          return
        };
        this.users.push({
          name: this.newUser.name,
          email: this.newUser.email,
          contacted: false
        });
        e.preventDefault();
        this.newUser = {};
      },
      delUser: function (user) {
        this.users.splice(this.users.indexOf(user), 1);
      }
    },
    created: function(){
      let self = this;
      this.$http.get("https://jsonplaceholder.typicode.com/users")
       .then(function (res) {
        self.users= res.data;
        console.log(self.users);
      })
      
    }
  }

</script>

<style>
  .contacted {
    color: grey;
    text-decoration: line-through;
  }
</style>