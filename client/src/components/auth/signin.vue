<template>
  <div id="signin">
    <div class="signin-form">
      <form @submit.prevent="onSubmit">
        <div class="input">
          <label for="email">Mail</label>
          <input
                  type="email"
                  id="email"
                  v-model="email">
        </div>
        <div class="input">
          <label for="password">Password</label>
          <input
                  type="password"
                  id="password"
                  v-model="password">
        </div>
        <p class="submit">
          <button type="submit">Submit</button>
        </p>
        <div class="callout alert" v-if="message">{{ message }}</div>
      </form>
    </div>
  </div>
</template>

<script>
  import { AUTH_REQUEST } from '../../store/actions/auth'

  export default {
    data () {
      return {
        email: '',
        password: '',
        message: '',
      }
    },
    methods: {
      login: function () {
        const { email, password } = this
        this.$store.dispatch(AUTH_REQUEST, { email, password }).then((res) => {
          if(res.data.status!=true)
          {
            this.message = res.data.message
            return
          }

          this.$router.push({ name: 'categoryList' });
        })
      },
      onSubmit () {
        this.login()
      }
    }
  }
</script>

<style scoped>
  .signin-form {
    width: 400px;
    margin: 30px auto;
    border: 1px solid #eee;
    padding: 20px;
    box-shadow: 0 2px 3px #ccc;
  }

  .input {
    margin: 10px auto;
  }

  .input label {
    display: block;
    color: #4e4e4e;
    margin-bottom: 6px;
  }

  .input input {
    font: inherit;
    width: 100%;
    padding: 6px 12px;
    box-sizing: border-box;
    border: 1px solid #ccc;
  }

  .input input:focus {
    outline: none;
    border: 1px solid #521751;
    background-color: #eee;
  }

  .submit button {
    border: 1px solid #521751;
    color: #521751;
    padding: 10px 20px;
    font: inherit;
    cursor: pointer;
  }

  .submit button:hover,
  .submit button:active {
    background-color: #521751;
    color: white;
  }

  .submit button[disabled],
  .submit button[disabled]:hover,
  .submit button[disabled]:active {
    border: 1px solid #ccc;
    background-color: transparent;
    color: #ccc;
    cursor: not-allowed;
  }
</style>