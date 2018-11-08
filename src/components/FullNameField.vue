<template>
  <div>
    <div class="form-group">
      <label for="firstName">First Name</label>
      <input 
        type="text" 
        class="form-control" 
        id="firstName" 
        placeholder="First Name"
        :value="firstName"
        @input="input($event, 'firstName')"
      />
    </div>
    
    <div class="form-group">
      <label for="lastName">Last Name</label>
      <input 
        type="text" 
        class="form-control" 
        id="lastName" 
        placeholder="Last Name"
        :value="lastName"
        @input="input($event, 'lastName')"
      />
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      value: {
        type: String,
        default: '',
      },
    },
    methods: {
      splitValues() {
        return this.value.split(' ');
      },
      input(event, fieldName) {
        const { value } = event.target;
        const result = [
          fieldName === 'firstName' ? value : this.firstName,
          fieldName === 'lastName' ? value : this.lastName,
        ].join(' ');
        this.$emit('input', result);
      }
    },
    computed: {
      firstName() {
        return this.splitValues()[0] || '';
      },
      lastName() {
        return this.splitValues()[1] || '';
      }
    }
  }
</script>

<style>

</style>
