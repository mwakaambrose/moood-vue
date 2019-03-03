<template>
  <div class="hello">
    <h1>{{ title }}</h1>
    <p>
      So fucking <strong>relatable</strong>, The one place to complain or be happy anonymously
    </p>
    <router-link to="/moods">
      <sui-button primary content="View Moods" icon="right arrow" label-position="right" />
    </router-link>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    title: String
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  margin: 40px 0 0;
  font-size: 48px;
}
p {
  font-size: 26px;
}
</style>
