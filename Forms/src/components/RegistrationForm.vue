<template>
    <div :class="classlist">
        <h2>Registration Form</h2>
        <form action="#" @submit.prevent="register">

            <!-- Name Field -->
            <div class="form-field">
                <span class="msg-validation" v-show="invalidName">{{fields[0].validationText}}</span>
                <input type="textbox" :placeholder="fields[0].placeholderText" v-model="model.Name" @blur="validateName()" />
            </div>

            <!-- Email Field -->
            <div class="form-field">
                <span class="msg-validation" v-show="invalidEmail">{{fields[1].validationText}}</span>
                <input type="email" :placeholder="fields[1].placeholderText" v-model="model.Email" @blur="validateEmail()" />
            </div>

            <!-- Password Field -->
            <div class="form-field">
                <span class="msg-validation" v-show="invalidPassword">{{fields[2].validationText}}</span>
                <input type="password" :placeholder="fields[2].placeholderText" v-model="model.Password" @blur="validatePassword()" />
            </div>

            <!-- Industry Field -->
            <div class="form-field">
                <span class="msg-validation" v-show="invalidIndustry">{{fields[3].validationText}}</span>
                <select v-model="model.Industry" @blur="validateIndustry()">
                    <option value="" disabled="disabled" selected="selected">Please select an Industry</option>
                    <option v-for="(industry, index) in industryList" :value="industry.label">{{industry.label}}</option>
                </select>
            </div>

            <!-- Submit Form -->
            <input type="submit" value="Register" />
        </form>
    </div>
</template>

<script>
export default {
    props: [
        'active'
    ],
      data() {
          return {
              model: {
                  Name: '',
                  Email: '',
                  Password: '',
                  Industry: ''
              },
              invalidName: false,
              invalidEmail: false,
              invalidPassword: false,
              invalidIndustry: false,
              classlist: [
                'form',
                'registration-form'
              ],
              fields: [{
                  label: 'Name',
                  placeholderText: 'Enter Name',
                  type: 'textbox',
                  validationText: 'Please enter a valid name.'
              }, {
                  label: 'Email',
                  placeholderText: 'Enter email address',
                  type: 'email',
                  validationText: 'Please enter a valid Email addresss.'
              }, {
                  label: 'Password',
                  placeholderText: 'Enter Your Password',
                  type: 'password',
                  validationText: 'Password must be 6-20 characters long and include 1 Uppercase letter, 1 lowercase letter, and 1 numeric digit.'
              }, {
                  // Industry
                  validationText: 'Please select an Industry.'
              }],
              industryList: [{
                  label: 'Advertising',
                  value: 0
              }, {
                  label: 'Communications',
                  value: 1
              }, {
                  label: 'Marketing',
                  value: 2
              }, {
                  label: 'Real Estate',
                  value: 3
              }, {
                  label: 'Web Services',
                  value: 4
              }]
          }
      },
    watch: {
        // Clear data when we leave Registration Form
        'active': function (val, oldVal) {
            console.log("registrationChanged: " + val);
            if (val) {
                this.clearForm();
            }
        }
    },
    methods: {
        register(e) {
            this.validateName();
            this.validateEmail();
            this.validatePassword();
            this.validateIndustry();

            let valid = true;
            if (this.invalidName || this.invalidEmail || this.invalidPassword || this.invalidIndustry) {
                valid = false
            }

            if (valid) {
                console.log(this.model);
                alert('Validated. Hooray! See console for object details.');
            } else {
                console.log('Invalid Information');
            }
        },
        validateName() {
            // Validation Checks
            let regex = /^[A-Za-z\s]+$/;
            if (regex.test(this.model.Name)) {
                this.invalidName = false;
            } else {
                this.invalidName = true;
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
        validateIndustry() {
            // Validation Checks
            if (this.model.Industry) {
                this.invalidIndustry = false;
            } else {
                this.invalidIndustry = true;
            }
        },
        clearForm() {
            this.model.Name = '';
            this.model.Email = '';
            this.model.Password = '';
            this.model.Industry = '';
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
