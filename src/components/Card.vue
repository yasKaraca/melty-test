<template>
  <article class='article'>
      <a :href='urlArticle' target='_blank' class='article-link'>
        <figure class='article-link-thumb'>
          <img :src='thumbnail' :alt='altImage' class='article-link-thumb-img'>
          <figcaption class='article-link-thumb-caption'>
                <a :href='folderUrl' target='_blank' class='article-link-thumb-caption-link'>{{folderName}}</a>
                <time :datetime='dateTime' class='article-link-thumb-caption-date'>{{sincePublished}}</time>
            </figcaption>
        </figure>
        <h3 class='article-link-title'>{{title}}</h3>
        <p class='article-link-lead'>{{lead}}</p>
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
        },
        title: {
            get: function () {
                return this.data.title;
            }
        },
        lead: {
            get: function () {
                return this.data.lead;
            }
        }
    },
}
</script>

<style lang='scss' scoped>
    .article {
        grid-column: 1 / span 12;
        width: 100%;
        font-family: Quicksand,sans-serif;
    
        &-link {
            display: flex;
            flex-direction: column;
            text-decoration: none;
            color: #323232;

            &-thumb {
                position: relative;
                width: 100%;
                padding-top: 56.25%;

                &-img {
                    position: absolute;
                    left: 0;
                    top: 0;
                    width: 100%;
                    height: auto;
                    border-radius: 1.875rem 1.875rem 1.875rem 0;
                }

                &-caption {
                    font-size: .75rem;
                    position: absolute;
                    bottom: 0;
                    left: 0;
                    right: 0;
                    background: rgba(50,50,50,.7);
                    backdrop-filter: blur(10px) saturate(300%);
                    border-bottom-right-radius: 1.875rem;
                    color: white;
                    display: flex;
                    justify-content: space-between;
                    padding: .5rem 1rem;
                    font-size: .6875rem;
                    font-weight: 300;

                    &-link {
                        color: white;
                        text-decoration: none;
                    }

                    &-date {
                        padding-right: .5rem;
                    }
                }
            }

            &-title {
                padding: .625rem .9375rem;
                font-size: 1.375rem;
                line-height: 1.25;
                font-family: 'Source Sans Pro', sans-serif;
                font-weight: 700;
            }

            &-lead {
                padding: 0 .9375rem;
                font-size: 1.0625rem;
            }
        }
    }
</style>