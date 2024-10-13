<script setup>
import { onMounted } from 'vue';
import UrlConverter from './components/UrlConverter.vue';

let query = ''

onMounted(() => {

  if(window.location.search) {
    query = window.location.search.split('?redirect=')[1]

    redirect()
  }

})

function redirect() {

  window.open(query, '_system');

  // window.location.href = 'intent:' + query + '#Intent;scheme=http;package=com.android.chrome;S.browser_fallback_url='+ query + ';end'

}

</script>

<template>

  <div class="main">
    <header class="title">
      <h1>Deep Link Redirector!</h1>
  
      <p>Esta aplicación te permite crear links directos de una aplicación a otra, de manera sencilla</p>
  
    </header>
  
    <main style="width: 100%;">
      <!-- <TheWelcome /> -->
       <UrlConverter></UrlConverter>
    </main>
  </div>


</template>

<style scoped>

.main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100vw;
}

.title {
  text-align: center;
  gap: 2rem;
  padding: 0 2rem;
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
  padding: 0 2rem;
  height: calc(80dvh);
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

</style>
