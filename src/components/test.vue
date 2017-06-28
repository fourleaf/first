<template>
  <div class="test">
    <input type="text" v-model="title">
    <input type="text" @keyup.enter="press">
    <br/>
    <h1>{{title}}</h1>
    <h2 v-if="showName">{{user.first_name}}</h2>
    <button @click='greet("hello"),cook()'>click</button>
    <ul>
      <li v-for="item in items">{{item.title}}</li>
    </ul>
    <label for="">First name</label><input type="text" v-model='user.firstName'>
    <label for="">Last name</label><input type="text" v-model='user.lastName'>
    <h2>{{fullName}}</h2>
    <h2>{{msg}}</h2>
  </div>
</template>

<script>
  export default {
    name: 'test',
    props: {
      msg: {
        type: String,
        default: 'foobar',
      }
    },
    data() {
      return {
        title: 'helllo world',
        user: {
          firstName: 'john',
          lastName: 'doe'
        },
        showName: true,
        items: [
          { title: 'item one' },
          { title: 'item two' },
          { title: 'item three' }
        ]
      }
    },
    methods: {
      greet: function (a) {
        alert(a);
      },
      press: function (e) {
        console.log(e.target.value);
      }
    },
    computed: {
      fullName: function () {
        return this.user.firstName + '' + this.user.lastName
      }
    }
  }

</script>