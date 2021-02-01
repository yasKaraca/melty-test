<template>
  <article class='article'>
      <a :href='urlArticle' target='_blank'>
        <figure>
          <img :src='thumbnail' :alt='altImage'>
          <figcaption>
                <a :href='folderUrl' target='_blank'>{{folderName}}</a>
                <time :datetime='dateTime'>{{sincePublished}}</time>
            </figcaption>
        </figure>
      </a>
  </article>
</template>

<script>
import moment from 'moment';
moment.locale('fr');


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
        },
        sincePublished: {
            get: function () {
                return moment(this.data.date.published).fromNow();
            }
        },
        dateTime: {
            get: function () {
                return this.data.date.published;
            }
        },
        folderUrl: {
            get: function () {
                return this.data.folder.URL;
            }
        },
        folderName: {
            get: function () {
                return this.data.folder.name;
            }
        }
    },
}
</script>

<style lang='scss' scoped>
    .article {
        grid-column: 1 / span 12;
        width: 100%;
    }

    .article > a {
        display: flex;
        flex-direction: column;

        figure {
            position: relative;
            width: 100%;
            padding-top: 56.25%;

            img {
                position: absolute;
                left: 0;
                top: 0;
                width: 100%;
                height: auto;
            }

            figcaption {
                font-size: .75rem;
            }
        } 
    }
</style>