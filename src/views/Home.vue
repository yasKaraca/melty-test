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
  $desktop: 1160px;
  $tablet: 720px;
  $cards: 6;

  //  GRID LAYOUT FOR MOBILE

  .home {
    display: grid;
    grid-template-columns: repeat(12, 1fr);
    grid-gap: 1.875rem;
    padding: 2rem .625rem;
  }

  //  GRID LAYOUT FOR TABLET
  
  @media (min-width: $tablet) and (max-width: $desktop) {
    @for $i from 1 to $cards+1 {
      .home article:nth-child(#{$i}) {
        @if $i % 2 == 0 {
          grid-column: 7 / span 6;  // ALIGN RIGHT
        } @else {
          grid-column: 1 / span 6;  // ALIGN LEFT
        }
      }
    }
  }

  // GRID LAYOUT FOR DESKTOP

  @media (min-width: 1160px) {
    .home {
      max-width: 1140px;
      padding: 2rem 0;
      margin: 0 auto;
    }

    @for $i from 1 to 6+1 {
      .home article:nth-child(#{$i}) {
        @if $i % 3 == 1 {
          grid-column: 1 / span 4;  // ALIGN LEFT
        } @else if $i % 3 == 2 {
          grid-column: 5 / span 4;  // ALIGN CENTER
        } @else if $i % 3 == 0 {
          grid-column: 9 / span 4;  // ALIGN RIGHT
        }
      }
    }
  }
</style>
