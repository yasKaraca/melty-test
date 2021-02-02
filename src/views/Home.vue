<template>
  <section class="home">
    <Card v-for="( item, index ) in cards" :key="index" :data="item"
    />
  </section>
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

<style lang="scss" scoped>
  .home {
    display: grid;
    grid-template-columns: repeat(12, 1fr);
    grid-gap: 1.875rem;
    padding: 2rem .625rem;
  }

  @media (min-width: 720px) and (max-width: 1160px) {
    @for $i from 1 to 6+1 {
      .home article:nth-child(#{$i}) {
        @if $i % 2 == 0 {
          grid-column: 7 / span 6;
        } @else {
          grid-column: 1 / span 6;
        }
      }
    }
  }

  @media (min-width: 1160px) {
    @for $i from 1 to 6+1 {
      .home article:nth-child(#{$i}) {
        @if $i % 3 == 1 {
          grid-column: 1 / span 4;
        } @else if $i % 3 == 2 {
          grid-column: 5 / span 4;
        } @else if $i % 3 == 0 {
          grid-column: 9 / span 4;
        }
      }
    }
  }
</style>
