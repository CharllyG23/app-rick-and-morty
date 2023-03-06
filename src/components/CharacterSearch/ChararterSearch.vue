<template>
    <div class="characterSearch">
      <div class="characterSearch_container" >   
        <div class="characterSearch_container__input">
          <div class="svg">
            <svg aria-hidden="true" class="w-5 h-5 text-gray-500 dark:text-gray-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z" clip-rule="evenodd"></path></svg>
          </div>
          <input 
            v-model="searchText" 
            type="text" 
            id="simple-search"  
            :class="{ 'bg-red-300': error }" 
            class="input"
            placeholder="Busca pelo nome do personagem" 
            required 
            @keyup="search($event)"
          />
        </div>
        <button 
          @click="search" 
          type="submit" 
          class="characterSearch_container__button"
        >
          Busca
        </button>
      </div>
      <span class="error" v-if="error">Nome do personagem errado!</span>
    </div>
</template>
<script setup>
  import { ref, watch } from 'vue'
  import  api from '../../support/http/api.js'
  
  const emit = defineEmits(['search-character'])
  const searchText = ref('')
  const error = ref(false)
  
  const search = async () => {
      const text = formatString(searchText.value)
      if(text.length >= 3){
          await api.get(`/character/?name=${text}`).then((response)=>{
              emit('search-character', response.data.results)
          }).catch((err)=>{
              console.log(err)
              error.value = true
          })
      }
  } 
  
  const formatString = (str) => {
    let hasUppercase = false;
    let newString = "";
    for (let i = 0; i < str.length; i++) {
      if (str[i] === str[i].toUpperCase()) {
        hasUppercase = true;
        newString += str[i].toLowerCase();
      } else {
        newString += str[i];
      }
    }
    if (hasUppercase) {
      return newString;
    }
    return str;
  };
  
  watch(() => searchText.value, async () => {
      if(searchText.value.trim() === ""){
          emit('search-character', {})
      }
      error.value = false
  })
  
  </script>
  <style lang="scss" scoped>
  @import './style.scss';
  </style>