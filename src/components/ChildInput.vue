<template>
  <div class="child-input">
    <p>ここからが Child Input です</p>
    <form>
      <div class="form-group">
        <label for="input-fitstname" class="bmd-label-floating">Firstname</label>
        <input type="name" class="form-control" id="input-fitstname" v-model="firstname">
      </div>
      <div class="form-group">
        <label for="input-lastname" class="bmd-label-floating">Lastname</label>
        <input type="name" class="form-control" id="input-lastname" v-model="lastname">
      </div>
      <button type="button" class="btn btn-primary" @click="handleClick">Submit</button>
    </form>
    <p>ここまでが Child Input です</p>
  </div>
</template>

<script>
export default {
  name: 'ChildInput',
  data () {
    return {
      firstname: '',
      lastname: ''
    }
  },
  methods: {
    handleClick: function () {
      this.$emit('updateFirstname', this.firstname)
      this.$emit('updateLastname', this.lastname)
    }
  }
}
</script>