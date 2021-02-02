<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style lang="scss">
html {
    line-height: 1.15;
    -webkit-text-size-adjust: 100%;
    box-sizing: border-box;
  }

  body {
    margin: 0;
  }

  figure {
    margin-block-start: 0;
    margin-block-end: 0;
    margin-inline-start: 0;
    margin-inline-end: 0;
  }

  h3, p {
    margin: 0;
  }

  *, ::after, ::before {
    font-smoothing: antialiased;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    box-sizing: inherit;
  }

</style>
