<template>
    <div id="app">
        <Header />
        <Content />
    </div>
</template>

<script>
  import Header from './components/Header';
  import Content from './components/Content';

  export default {
    name: 'app',
    components: {
      Header,
      Content,
    }
  }
</script>
