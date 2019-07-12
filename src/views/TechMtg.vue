<template>
  <div id="tech-mtg">
    <h1>コミット状況</h1>
    <template v-for="branch in branches">
      <input type="radio"
        :id="branch"
        :value="branch"
        name="branch"
        v-model="currentBranch">
      <label>{{ branch }}</label>
    </template>
    <p>vuejs/vue/{{ currentBranch }}</p>
    <ul>
      <li v-for="(record, index) in commits" :key="index">
        <a :href="record.html_url" target="_blank" class="commit">{{ record.sha.slice(0, 7) }}</a>
        - <span class="message">{{ record.commit.message | truncate }}</span><br>
        by <span class="author"><a :href="record.author.html_url" target="_blank">{{ record.commit.author.name }}</a></span>
        at <span class="date">{{ record.commit.author.date | formatDate }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
var baseUrl = 'https://api.github.com' 
var repo = '/repos/vuejs/vue/commits'
var token = 'access_token=' // private repo の場合は必須
var preBranch = 'sha='

export default {
  name: 'TechMtg',

  data () {
    return {
      branches: ['master', 'dev'],
      currentBranch: 'master',
      commits: null
    }
  },
  created: function () {
    this.fetchData()
  },
  watch: {
    currentBranch: 'fetchData'
  },
  filters: {
    truncate: function (v) {
      var newline = v.indexOf('\n')
      return newline > 0 ? v.slice(0, newline) : v
    },
    formatDate: function (v) {
      return v.replace(/T|Z/g, ' ')
    }
  },
  methods: {
    fetchData: function () {
      axios
        .get(baseUrl + repo + '?' + token + '&' + preBranch + this.currentBranch)
        .then(response => (this.commits = response.data))
    }
  }
}
</script>

<style>
a {
  text-decoration: none;
  color: #42b983;
}
li {
  list-style-type: none;
  line-height: 1.5em;
  margin-bottom: 20px;
}
.author, .date {
  font-weight: bold;
}
</style>
