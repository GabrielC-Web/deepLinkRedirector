<script setup>
import { onMounted } from 'vue';
import UrlConverter from './components/UrlConverter.vue';

let query = ''

onMounted(() => {

  if(window.location.search) {
    query = window.location.search.split('?')[1].split('&&')[0].split('=')[1]

    redirect()
  }

})

function redirect() {

  window.location.href = 'intent:' + query + '#Intent;scheme=http;package=com.android.chrome;S.browser_fallback_url='+ query + ';end'

}

</script>

<template>

  <header class="title">
    <h1>Deep Link Redirector!</h1>

    <p>Esta aplicación te permite crear links directos de una aplicación a otra, de manera sencilla</p>

  </header>

  <main>
    <!-- <TheWelcome /> -->
     <UrlConverter></UrlConverter>
  </main>

</template>

<style scoped>

.title {
  text-align: center;
  gap: 2rem;
  width: 100%;
  display: flex;
  flex-direction: column;
}

template {
  display: flex;
  flex-direction: column;
}

main {
  flex-grow: 1;
  height: calc(80dvh);
  display: flex;
  justify-content: center;
  align-items: center;
}

</style>
