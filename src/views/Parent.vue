<template>
  <div id="parent">
    <p>ここからがParentです</p>
    <ChildInput
      @updateFirstname="updateFirstname"
      @updateLastname="updateLastname"
    />
    <ChildOutput
      :firstname=firstname
      :lastname=lastname
    />
    <p>ここまでがParentです</p>
  </div>
</template>

<script>
import ChildInput from '@/components/ChildInput.vue'
import ChildOutput from '@/components/ChildOutput.vue'

export default {
  name: 'Parent',
  components: {
    ChildInput,
    ChildOutput
  },
  data () {
    return {
      firstname: '',
      lastname: ''
    }
  },
  methods: {
    updateFirstname (firstname) {
      this.firstname = firstname
    },
    updateLastname (lastname) {
      this.lastname = lastname
    }
  }
}
</script>