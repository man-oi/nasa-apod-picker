<template>
  <div class="login">
    <form @submit.prevent="login()">
      <el-row :gutter="20">
        <el-col :span="6" :offset="6">
          <el-input placeholder="Dein Benutzername" v-model="input.username"></el-input>
        </el-col>
        <el-col :span="6">
          <el-input placeholder="Please input password" v-model="input.password" show-password></el-input>
        </el-col>
      </el-row>

      <el-row>
        <el-col :span="6" :offset="6">
          <el-button
            size="medium"
            type="success"
            native-type="submit"
          >
            Einloggen
          </el-button>
        </el-col>
      </el-row>
    </form>
  </div>
</template>


<script>
export default {
  name: 'Login',

  data() {
    return {
      input: {
        username: '',
        password: '',
      },
    };
  },

  methods: {
    login() {
      if (this.input.username.length) {
        localStorage.setItem('username', this.input.username);
        this.$router.push({ name: 'home' });
      }
    },
  },
};
</script>
