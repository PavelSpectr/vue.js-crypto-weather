<script>
export default {
  data() {
    return {
      users: [],
      error: '',
      userName: '',
      userPass: '',
      userEmail: ''
    }
  },
  methods: {
    sendData() {
      if(this.userName == '') {
        this.error = 'Empty name';
        return;
      } else if(this.userPass == '') {
        this.error = 'Empty pass';
        return;
      } else if(this.userEmail == '') {
        this.error = 'Empty email';
        return;
      }
      this.users.push({
        name: this.userName,
        pass: this.userPass,
        email: this.userEmail
      })
    }
  }
}
</script>

<template>
  <input type="text" v-model = userName placeholder="Name">
  <input type="password" v-model = userPass placeholder="Password">
  <input type="email" v-model = userEmail placeholder="Email">
  <p className="error">{{error}}</p>

  <button @click = sendData()>Send</button>

  <div v-if="users.length == 0" className="user">
    We have no users
  </div>
  <div v-else-if="users.length == 1" className="user">
    We have only 1 user
  </div>
  <div v-else className="user">
    We have more than 1 element
  </div>

  <div v-for="(el, index) in users" :key = index className="user">
    <h3>{{el.name}}</h3>
    <p>{{el.email}} - <b>{{el.pass}}</b></p>
  </div>

</template>

<style scoped>
input {
  display: block;
  margin-bottom: 10px;
  border-radius: 3px;
  border: 1px solid silver;
  outline: non;
  padding: 10px 15px;
  background: #fafafa;
  color: #333;
}

button {
  border: 0;
  border-radius: 5px;
  outline: none;
  padding: 10px 15px;
  background: #6cd670;
  color: #167f3d;
  font-weight: bold;
  cursor: pointer;
  transition: transform 500ms ease;
}

button:hover {
  transform: translateY(-5px);
}

.user {
  width: 500px;
  margin-top: 20px;
  border: 1px solid silver;
  background: #e3e3e3;
  color: #222;
  padding: 20px;
  border-radius: 5px;
}
</style>
