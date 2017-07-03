<template>
    <div :class="classlist">
        <h2>Login Form</h2>
        <form action="#" @submit.prevent="login">

            <!-- Email Field -->
            <div class="form-field">
                <span class="msg-validation" v-show="invalidEmail">{{fields[0].validationText}}</span>
                <input type="email" :placeholder="fields[0].placeholderText" v-model="model.Email" @blur="validateEmail(this)" />
            </div>

            <!-- Password Field -->
            <div class="form-field">
                <span class="msg-validation" v-show="invalidPassword">{{fields[1].validationText}}</span>
                <input type="password" :placeholder="fields[1].placeholderText" v-model="model.Password" @blur="validatePassword()" />
            </div>

            <!-- Submit Form -->
            <input type="submit" value="Log In" />
        </form>
    </div>
</template>

<script>
export default {
    props: [
        'active',
    ],
      data() {
          return {
              model: {
                  Email: '',
                  Password: ''
              },
              invalidEmail: false,
              invalidPassword: false,
              classlist: [
                'form',
                'loginForm'
              ],
              fields: [{  // Form fields
                  label: 'Email',
                  placeholderText: 'Enter Email Address',
                  type: 'email',
                  validationText: 'Please enter a valid Email addresss.'
              }, {
                  label: 'Password',
                  placeholderText: 'Enter Your Password',
                  type: 'password',
                  validationText: 'Incorrect Password'
              }]
          }
      },
    watch: {
        // Clear data when we leave Registration Form
        'active': function (val, oldVal) {
            console.log("loginchanged: " + val);
            if (val) {
                this.clearForm();
            }
        }
    },
    methods: {
        login() {
            //  Validate
            this.validateEmail();
            this.validatePassword();

            let valid = true;
            if (this.invalidEmail || this.invalidPassword) {
                valid = false
            }

            if (valid) {
                console.log(this.model);
                alert('Logging In! See console for object details.');
            } else {
                console.log('Invalid Information');
            }
        },
        validateEmail() {
            // Validation Checks
            let regex = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
            if (regex.test(this.model.Email)) {
                this.invalidEmail = false;
            } else {
                this.invalidEmail = true;
            }
        },
        validatePassword() {
            // Validation Checks
            let regex = /^(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{6,20}$/;
            if (regex.test(this.model.Password)) {
                this.invalidPassword = false;
            } else {
                this.invalidPassword = true;
            }
        },
        clearForm() {
            this.model.Email = '';
            this.model.Password = '';
        }
    }
}
</script>
