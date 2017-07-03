<template>
  <div id="app">
      <div class="menu">
          <button @click="toggleLoginForm" class="button LoginToggle">Login</button>
          <button @click="toggleRegistrationForm" class="button RegistrationToggle">Register</button>
      </div>
      <registration-form v-show="registrationActive" :active="registrationActive"></registration-form>
      <login-form v-show="loginActive" :active="loginActive"></login-form>
  </div>
</template>

<script>
import LoginForm from './components/loginForm'
import RegistrationForm from './components/RegistrationForm'

export default {
    components: {
        LoginForm,
        RegistrationForm
    },
    data () {
        return {
            loginActive: false,
            registrationActive: false
        }
    },
    methods: {
        toggleLoginForm() {
            if (!this.loginActive) {
                this.loginActive = true;
          
                // Close registration form if needed.
                if (this.registrationActive) {
                    this.registrationActive = false;
                }
            } else {
                this.loginActive = false;
            }
        },
        toggleRegistrationForm() {
            if (!this.registrationActive) {
                this.registrationActive = true;
          
                // Close login form if needed.
                if (this.loginActive) {
                    this.loginActive = false;
                }
            } else {
                this.registrationActive = false;
            }
        }
    }
}
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }

    * {
        box-sizing: border-box;
    }

    .menu {
        background-color: #444;
        padding: 1em;
        width: 200px;
        float: left;
    }

    .button {
        padding: .5em 2em;
        border: 0;
        cursor: pointer;
        width: 100%;
    }

        .button:hover {
            opacity: .9;
        }

    .LoginToggle {
        background-color: #fff041;
    }

    .RegistrationToggle {
        background-color: #6fd4c6;
    }

    .form {
        padding: 1em;
        border: 2px solid #444;
        width: 30%;
    }

    .form-field {
        display: block;
        margin: 1em 0;
    }

    /* Login Form */
    .loginForm {
        background-color: #fff041;
        margin-left: 50%;
    }
    /* Login Form */


    /* Registration Form */
    .registration-form {
        background-color: #6fd4c6;
        margin-left: 15%;
    }
    /* Registration Form */


    .msg-validation {
        display: block;
        font-size: .7em;
        color: red;
    }
</style>
