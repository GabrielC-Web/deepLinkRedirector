<script setup>
import { ref } from 'vue';
import { PhCopy } from '@phosphor-icons/vue';

const text = ref('')

let finalURL = ref('')

let validURL = null

/**
 * Obtiene el valor de la URL tipeada
 * @param e 
 */
function getCurrentURL(e) {

    //* Veo si es paste
    if(e && e.type != 'click') {
        text.value = e.target.value
    }

    //* Valido el input
    checkURLValidity()

    //* Creo la url de redirección
    urlConverter()

}

function checkURLValidity() {

    //* Regex
    let regex = /(https:\/\/www\.|http:\/\/www\.|https:\/\/|http:\/\/)?[a-zA-Z]{2,}(\.[a-zA-Z]{2,})(\.[a-zA-Z]{2,})?\/[a-zA-Z0-9]{2,}|((https:\/\/www\.|http:\/\/www\.|https:\/\/|http:\/\/)?[a-zA-Z]{2,}(\.[a-zA-Z]{2,})(\.[a-zA-Z]{2,})?)|(https:\/\/www\.|http:\/\/www\.|https:\/\/|http:\/\/)?[a-zA-Z0-9]{2,}\.[a-zA-Z0-9]{2,}\.[a-zA-Z0-9]{2,}(\.[a-zA-Z0-9]{2,})?/g;

    //* Veo si la URL es válida
    if(text.value) {
        validURL = regex.test(text.value)
    } else {
        validURL = null
    }

}

/**
 * Crea el link de redirección
 */
function urlConverter() {

    finalURL.value = ''

    if(!text.value) {
        return
    }

    let url = text.value

    let origin = window.location.href.split('?')[0]

    finalURL.value = origin + '/?redirect=' + url

}

/**
 * Copia la URL
 */
function copyURL() {

    navigator.clipboard.writeText(finalURL.value)
    
}

</script>

<template class="url_converter">

    <div class="items_container">

        <!-- Input -->
        <section class="url_converter">
    
            <!-- /* From Uiverse.io by LightAndy1 */  -->
            
    
            <div class="group">
                <svg viewBox="0 0 24 24" aria-hidden="true" class="search-icon">
                    <g>
                    <path
                        d="M21.53 20.47l-3.66-3.66C19.195 15.24 20 13.214 20 11c0-4.97-4.03-9-9-9s-9 4.03-9 9 4.03 9 9 9c2.215 0 4.24-.804 5.808-2.13l3.66 3.66c.147.146.34.22.53.22s.385-.073.53-.22c.295-.293.295-.767.002-1.06zM3.5 11c0-4.135 3.365-7.5 7.5-7.5s7.5 3.365 7.5 7.5-3.365 7.5-7.5 7.5-7.5-3.365-7.5-7.5z"
                    ></path>
                    </g>
                </svg>
    
        
                <input
                    id="query"
                    class="input"
                    type="search"
                    placeholder="Search..."
                    name="searchbar"
                    v-model="text"
                    @input="getCurrentURL"
                    @paste="getCurrentURL"
                />
            </div>
    
            <button @click="getCurrentURL">
                Convertir
            </button>
    
        </section>
    
        <!-- Resultado -->
        <section v-if="finalURL && validURL" class="result">

            <div class="result_items" @click="copyURL()">
                <span>{{ finalURL }} </span>
                <PhCopy :size="32" /> 
            </div>
            
        </section>

        <!-- Error -->

        <p v-if="validURL == false" class="error_text">Debe escribir una URL válida</p>

    </div>


</template>

<style scoped>

* {
    font-family: "Montserrat", sans-serif;
    line-height: 28px;
}

.items_container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    gap: 2rem;
    width: 100%;
    height: 100%;
    overflow: hidden;
}

.url_converter {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    gap: 2rem;
    width: 100%;
    overflow: hidden;
    padding: 0.5rem;
}

/* From Uiverse.io by LightAndy1 */ 
.group {
  display: flex;
  line-height: 28px;
  align-items: center;
  position: relative;
  max-width: 400px;
  width: 100%;
}

.input {
  font-family: "Montserrat", sans-serif;
  width: 100%;
  height: 45px;
  padding-left: 2.5rem;
  box-shadow: 0 0 0 1.5px #2b2c37, 0 0 25px -17px #000;
  border: 0;
  border-radius: 12px;
  background-color: #16171d;
  outline: none;
  color: #bdbecb;
  transition: all 0.25s cubic-bezier(0.19, 1, 0.22, 1);
  cursor: text;
  z-index: 0;
}

.input::placeholder {
  color: #bdbecb;
}

.input:hover {
  box-shadow: 0 0 0 2.5px #2f303d, 0px 0px 25px -15px #000;
}

.input:active {
  transform: scale(0.95);
}

.input:focus {
  box-shadow: 0 0 0 2.5px #2f303d;
}

.search-icon {
  position: absolute;
  left: 1rem;
  fill: #bdbecb;
  width: 1rem;
  height: 1rem;
  pointer-events: none;
  z-index: 1;
}

/* Resultado */

.result {
    display: flex;
    justify-content: center;
    width: 100%;
}

.result_items {
    overflow-wrap: break-word;
    text-align: center;
    inline-size: 45px;
    width: 100%;
    max-width: 400px;
    height: 45px;
    padding: 0 2rem;
    line-height: 45px;
    box-shadow: 0 0 0 1.5px #2b2c37, 0 0 25px -17px #000;
    border: 0;
    border-radius: 12px;
    background-color: #16171d;
    outline: none;
    color: #bdbecb;
    transition: all 0.25s cubic-bezier(0.19, 1, 0.22, 1);
    cursor: pointer;
    display: flex;
    align-items: center
}

.result_items:active {
    scale: 0.9;
}

span {
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    width: 100%;
    display: block;
}

/* Botón */

/* From Uiverse.io by niat786 */ 
button {
  font-family: PlusJakartaSans, -apple-system, BlinkMacSystemFont, Segoe UI,
    Roboto, Oxygen, Cantarell, Helvetica Neue, Ubuntu, sans-serif;
  font-size: 1rem;
  align-items: center;
  height: 48px;
  border-radius: 0.4rem;
  font-weight: 600;
  padding: 0 1.2rem;
  color: #ddd;
  border: none;
  cursor: pointer;
  box-shadow: 0 0.5rem 1rem rgba(143, 142, 142, 0.15) !important;
  background: #000000;
}

.followers {
  font-size: 0.8rem;
  color: #7f7f7f;
}

button:hover {
  background: #2b2a2a;
}

/* Error */

.error_text {
    animation: scale linear infinite;
    animation-duration: 2s;
    animation-iteration-count: infinite;

}

@keyframes scale {
    from {
        scale: 1
    }
    to {
        scale: 1.05
    }
} 

</style>