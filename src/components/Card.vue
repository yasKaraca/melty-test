<template>
  <article>
      <a :href='urlArticle' target='_blank'>
        <figure>
          <img :src='thumbnail' :alt='altImage'>
          <figcaption>{{data.folder.name}}</figcaption>
        </figure>
      </a>
  </article>
</template>

<script>
export default {
    data: () => {
        return {

        }
    },
    props: {
        data: Object
    },
    computed: {
        thumbnail: {
            get: function () {
                return this.data.thumbnail.URL.replace('{size}', 'thumb');
            }
        },
        altImage: {
            get: function () {
                return this.data.thumbnail.title;
            }
        },
        urlArticle: {
            get: function () {
                return this.data.URL;
            }
        }
    }
}
</script>

<style>

</style>