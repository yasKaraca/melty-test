<template>
  <article class='article' :class="{ mcq: isMcq }">
      <a :href='urlArticle' target='_blank' class='article-link'>
        <figure class='article-link-thumb'>
          <img :src='thumbnail' :alt='altImage' class='article-link-thumb-img'>
          <figcaption class='article-link-thumb-caption'>
                <a :href='folderUrl' target='_blank' class='article-link-thumb-caption-link'>{{folderName}}</a>
                <time :datetime='dateTime' class='article-link-thumb-caption-date'>{{sincePublished}}</time>
            </figcaption>
        </figure>
        <h3 class='article-link-title'>{{title}}</h3>
        <div v-if="isMcq" class='article-link-quizz'>
            <p class='article-link-quizz-cta'>participer</p>
        </div>
        <p v-else class='article-link-lead'>{{lead}}</p>
      </a>
  </article>
</template>

<script>
import moment from 'moment';
moment.locale('fr');

export default {
    name: 'Card',
    data: () => {
        return {
            mcqKey: 'Article<MultipleChoice>'
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
        },
        isMcq: {
            get: function () {
                return ( this.data.kind === this.mcqKey ? true : false );
            }
        }
    },
}
</script>

<style lang='scss' scoped>
    $black: #323232;
    $green: #14f032;
    $white: #ffffff;

    .article {
        grid-column: 1 / span 12;
        width: 100%;
        font-family: Quicksand,sans-serif;
    
        &-link {
            display: flex;
            flex-direction: column;
            text-decoration: none;
            color: $black;

            &-thumb {
                position: relative;
                width: 100%;
                padding-top: 56.25%;
                overflow: hidden;
                border-radius: 1.875rem 1.875rem 1.875rem 0;
                -webkit-border-radius: 1.875rem 1.875rem 1.875rem 0;

                &-img {
                    position: absolute;
                    left: 0;
                    top: 0;
                    width: 100%;
                    height: auto;
                    border-radius: inherit;
                    transition: transform .25s,opacity .2s,-webkit-transform .25s;
                    -o-object-fit: cover;
                    object-fit: cover;
                    transform: translateZ(0);
                    -webkit-transform: translateZ(0)
                }

                &-caption {
                    font-size: .75rem;
                    position: absolute;
                    bottom: 0;
                    left: 0;
                    right: 0;
                    background: rgba(50,50,50,.7);
                    backdrop-filter: blur(10px) saturate(300%);
                    -webkit-backdrop-filter: blur(10px) saturate(300%);
                    border-bottom-right-radius: 1.875rem;
                    color: $white;
                    display: flex;
                    justify-content: space-between;
                    font-size: .6875rem;
                    font-weight: 300;

                    &-link {
                        color: $white;
                        text-decoration: none;
                        display: block;
                        position: relative;
                        padding: .5rem 0 .5rem 1rem;

                        &::after {
                            position: absolute;
                            bottom: 0;
                            left: 0;
                            display: block;
                            content: "";
                            width: 30px;
                            height: 1px;
                            background: $green;
                            -webkit-transition: width .25s;
                            transition: width .25s;
                            pointer-events: none;
                        }
                    }

                    &-link:hover {
                        &::after {
                            width: calc(100% + 30px);
                        }
                    }

                    &-date {
                        padding: .5rem 1.5rem .5rem 0;
                    }
                }
            }

            &-title {
                padding: .625rem .9375rem;
                font-size: 1.375rem;
                line-height: 1.25;
                font-family: 'Source Sans Pro', sans-serif;
                font-weight: 700;
                transition: color .25s;
            }

            &-quizz {
                display: flex;
                justify-content: center;
                margin-bottom: .9375rem;

                &-cta {
                    text-transform: uppercase;
                    line-height: 1.15;
                    -webkit-box-shadow: inset 0 -6px $green;
                    box-shadow: inset 0 -6px #14f032;
                    font-size: .9375rem;
                    font-weight: 700;
                }
            }

            &-lead {
                padding: 0 .9375rem;
                font-size: 1.0625rem;
                display: -webkit-box;
                text-overflow: ellipsis;
                overflow: hidden;
                -webkit-box-orient: vertical;
                -webkit-line-clamp: 3;
            }
        }

        &:hover {
            .article-link-title {
                color: $green;
            }

            .article-link-thumb-img {
                -webkit-transform: scale3d(1.1,1.1,1);
                transform: scale3d(1.1,1.1,1);
            }
        }

        &.mcq {
            .article-link-title {
                padding: 1.25rem .9375rem;
            }
        }
    }
</style>