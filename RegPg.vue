<template>

        <div class ="container-fluid">
            <form class="form-group" @submit.prevent="validateBeforeSubmit" novalidate>
                <h2 style="font-weight: bold; font-size: 45px">
                    Register
                </h2>

                <div class="row">
                <div :class="{'col-md-6':true, 'has-error':errors.has('name')}">
                <label for="fname"><strong>FirstName :</strong></label>
                <input
                type="text"
                v-validate="'required'"
                :class="{'form-control':true}"
                name="fname"
                placeholder="Enter First Name"
                v-model="fname"
                />
                <span class="text-danger" v-if="errors.has('fname')">{{ errors.first('fname') }}</span>
                  <!-- <span>{{v.errors[0]}}</span> -->
                </div>

            <div :class="{'col-md-6':true,'has-errors':errors.has('lname')}">
                <label for="lname"><strong>LastName : </strong></label>
                <input
                type="text"
                v-validate="'required'"
                :class="{'form-control':true}"
                name="lname"
                class="form-control"
                placeholder="Enter Last Name"
                v-model="lname"
                />
                <span class="text-danger" v-if="errors.has('lname')">{{ errors.first('lname') }}</span>            </div>

            <div :class="{'col-md-6':true,'has-errors':errors.has('email')}">
            <label for="email"><strong> Email : </strong></label>
            <input
            type="text"
            v-validate="'required'"
            :class="{'form-control':true}"
            name="email"
            class="form-control"
            placeholder="Enter Email"
            v-model="email"
            />
            <span class="text-danger" v-if="errors.has('email')">{{ errors.first('email') }}</span>
            </div>

            <div :class="{'col-md-6':true,'has-errors':errors.has('mobile')}" >
            <label for="mobile"><strong>Mobile No. : </strong></label>
            <input
            type="text"
            v-validate="'required'"
            :class="{'form-control':true}"
            name="mobile"
            class="form-control"
            placeholder="Enter Mobile No."
            v-model="mobile"
            />
            <span class="text-danger" v-if="errors.has('mobile')">{{ errors.first('mobile') }}</span>
            </div>

            <div :class="{'col-md-6':true,'has-errors':errors.has('username')}">
            <label for="username"><strong> Username: </strong></label>
            <input
            type="text"
            v-validate="'required'"
            :class="{'form-control':true}"
            name="username"
            class="form-control"
            placeholder="Enter Username"
            v-model="username"
            />
            <span class="text-danger" v-if="errors.has('username')">{{ errors.first('username') }}</span>
           </div>

            <div :class="{'col-md-6':true,'has-errors':errors.has('password')}">
            <label for="password"><strong>Password : </strong></label>
            <input
            type="password"
            v-validate="'required'"
            :class="{'form-control':true}"
            name="password"
            class="form-control"
            placeholder="Enter Password"
            v-model="password"
            />
            <span class="text-danger" v-if="errors.has('password')">{{ errors.first('password') }}</span>
            </div>

            <div class="col-md-12" style="text-align: center; margin-top: 20px">
            <button
              type="submit"
              :disabled="errors.any()"
              class="btn btn-primary"
              v-on:click="submit()">Submit
            </button>
          </div>

        <div class="col-md-12" style="text-align: center">
            Already have an account?<br /><router-link to="/LoginPage"
              >Login here</router-link>
        </div>

        </div>
        </form>
        </div>

</template>

<script>
import axios from 'axios'
// import VeeValidate from 'vee-validate'
// import Vue from 'vue'
// Vue.use(VeeValidate)

export default {
  name: 'RegistrationPage',
  data () {
    return {
      error: [],
      fname: '',
      lname: '',
      email: '',
      mobile: '',
      username: '',
      password: ''
    }
  },

  computed: {
    isComplete () {
      return this.fname && this.lname && this.email && this.mobile && this.username && this.password
    }
  },
  methods: {
    validateBeforeSubmit () {
      this.$validator.validateAll().then((result) => {
        if (result) {
          alert('Form Submitted!')
        }
      })
    },
    // onChange(e) {
    //           console.log(e.target.value);
    //       },

    submit () {
      const url = 'http://localhost:4887/o/setStudentData'
      axios
        .post(url, {
          fname: this.fname,
          lname: this.lname,
          // gender: this.gender,
          email: this.email,
          mobile: this.mobile,
          username: this.username,
          password: this.password
        })
        .then((response) => {
          console.log(response.data)
          this.value = response.data
          if (response.data === true) {
            alert('Registration Successful')
            this.$router.push({ name: 'login' })
          } else {
            alert('Please enter data')
          }
        })
        .catch(function (err) {
          console.error(err)
        })
      console.log(this.fname)
    }
  }
  //  gender(newValue) {
  //   this.validations.gender = this.genders.includes(newValue);
  // }
}
</script>
