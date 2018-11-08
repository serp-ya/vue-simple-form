<template>
  <div class="form-group">
    <label for="fullName">Fullname</label>
    <input 
      type="text" 
      class="form-control" 
      id="fullName" 
      placeholder="Fullname"
      :value="value"
      @input="$emit('input', $event.target.value);"
    />
  </div>
</template>

<script>
  export default {
  }
</script>

<style>

</style>
