<template>
  <div class="container">
    <h1>My News App</h1>

    <table class="table table-bordered">
          <thead>
            <tr>
              <th> תיאור</th>
              <th> עורך</th>
              <th> כותרת</th>
            </tr>
          </thead>
          <tr v-for="a in news" :key="a.id">
            <td>{{a.description}}</td>
            <td>{{a.author}}</td>
            <td>{{a.title}}</td>
          </tr>


        </table>
      </div>
</template>

<script>
import axios from 'axios'
  export default {
    name: 'course-list-row',
    mounted: function () {
      this.getNews()
      console.log('mounted: got here')
    },
    data: function () {
      return {
        news: []
      }
    },
    methods: {
      getNews: function () {
          var self = this
          const url = 'http://newsapi.org/v2/top-headlines?country=il&apiKey=2edaea495526406dbdd56a0a72913756'
          axios.get(url, {
            dataType: 'json',
            headers: {
              'Accept': 'application/json',
              'Content-Type': 'application/json'
            },
            mode: 'no-cors',
            credentials: 'include'
          })
          .then(function (response) {
            console.log(JSON.stringify(response.data))
            self.news = response.data.articles
          })
          .catch(function (error) {
            console.log(error)
          })
      }
    }
  }
</script>
