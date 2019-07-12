<template>
  <div class="child-output">
    <p>ここからが Child Output です</p>
    <p>{{ firstname }}</p>
    <p>{{ lastname }}<p>
    <p>ここまでが Child Output です</p>
  </div>
</template>

<script>
export default {
  name: 'ChildOutput',
  props: {
    firstname: String,
    lastname: String
  }
}
</script>
