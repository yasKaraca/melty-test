<template>
  <div class="home">
    <Card v-for="( item, index ) in cards" :key="index" :data="item"
    />
  </div>
</template>

<script>
import axios from 'axios';
import Card from '@/components/Card.vue';

export default {
  name: 'Home',
  components: {
    Card
  },
  data: () => {
    return {
      apiUrl: 'https://api.melty.fr/v1/fr/feeds/2',
      errorData: false,
      articles: [],
      numberOfCards: 6
    }
  },
  created: function() {
    axios.get(this.apiUrl)
      .then((response) => {
        this.cards = response.data.feed_elements.items.slice(0, this.numberOfCards);
      })
      .catch((error) => {
        this.errorData = true;
        console.error(error);
      })
  },
  computed: {
    cards: {
      get: function () {
        return this.articles;
      },
      set: function (v) {
        this.articles = v;
      }
    }
  }
}
</script>
