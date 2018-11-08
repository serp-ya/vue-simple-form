<template>
  <div class="container">
    <template v-if="!isSubmit">
      <form>
        <div class="row">
          <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
            <!-- Exercise 1 -->
              <!-- Create a Signup Form where you retrieve the following Information -->
              <!-- Full Name (First Name + Last Name) -->
              <!-- Mail -->
              <!-- Password -->
              <!-- Store Data? Yes/No -->
            <!-- /Exercise 1 -->
    
            <!-- Exercise 2 -->
              <!-- Only display the Form if it has NOT been submitted -->
              <!-- Display the Data Summary ONCE the Form HAS been submitted -->
            <!-- /Exercise 2 -->
    
            <!-- Exercise 3 -->
              <!-- Edit the Example from above and create a custom "Full Name" Control -->
              <!-- which still holds the First Name and Last Name Input Field -->
            <!-- /Exercise 3 -->

            <FullNameField 
              v-model="userData.fullName"
            />
            
            <div class="form-group">
              <label for="email">Email</label>
              <input 
                type="email" 
                class="form-control" 
                id="email" 
                placeholder="Email"
                v-model="userData.email"
              />
            </div>
            
            <div class="form-group">
              <label for="password">Password</label>
              <input 
                type="password" 
                class="form-control" 
                id="password" 
                placeholder="Password"
                v-model="userData.password"
              />
            </div>
            
            <div class="form-group">
              <label>Store Data</label>
              <div>
                <input 
                  type="radio" 
                  name="store-data" 
                  value="Yes"
                  v-model="storeData"
                />
                <span>Yes</span>

                <input 
                  type="radio" 
                  name="store-data" 
                  value="No"
                  v-model="storeData"
                />
                <span>No</span>
              </div>
            </div>

            <p 
              class="bg-danger" 
              style="padding: 15px;"
              v-for="error in errors"
            >{{ error }}</p>

            <button type="submit" class="btn btn-primary" @click.prevent="submit">
              Submit
            </button>
          </div>
        </div>
      </form>
      <hr>
    </template>

    <div class="row" v-else>
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <div class="panel panel-default">
          <div class="panel-heading">
            <h4>Your Data</h4>
          </div>
          <div class="panel-body">
            <p>Full Name: {{ userData.fullName }}</p>
            <p>Mail: {{ userData.email }}</p>
            <p>Password: {{ userData.password }}</p>
            <p>Store in Database?: {{ storeData }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import FullNameField from './components/FullNameField.vue';

export default {
  components: {
    FullNameField,
  },
  data() {
    return {
      userData: {
        fullName: '',
        email: '',
        password: '',
      },
      storeData: 'Yes',
      isSubmit: false,
      errors: [],
      fname: '',
    };
  },
  methods: {
    submit() {
      const errors = this.validateForm(this.userData);

      if (errors.length) {
        return this.errors = errors;
      }
      this.isSubmit = true;
    },
    validateForm(formData) {
      return Object.keys(formData).reduce((res, key) => {
        if (!formData[key]) {
          res = [...res, `Field ${key} can\'t be empty`];
        }
        return res;
      }, []);
    },
  }
};
</script>

<style>
</style>
