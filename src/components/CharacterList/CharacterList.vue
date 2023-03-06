<template>
    <div class="characterList">
      <div class="characterList_container">
       <div class="characterList_content">
        <template v-if="Object.keys(search).length">
          <character-card v-for="(item, index) in search" :key="index" :data="item"/>
        </template>
         <template v-else>
            <character-card v-for="(item, index) in character.results" :key="index" :data="item"/>
         </template>
       </div>
      </div>
    </div>
  </template>
<script setup>
import { onMounted, ref } from 'vue';
import CharacterCard from '../CharacterCard/CharacterCard.vue';
import api from '../../support/http/api'

const props = defineProps({
  search: { type: Object, default: {} }
})

  const character = ref({})

  const getCharacterList = async () => {
    try{
      const response = await api.get('/character')
      character.value = response.data
    }catch (error) {
      console.error(error);
    }
  }

  onMounted(() =>{
    getCharacterList()
  })
</script>
<style lang="scss" scoped>
@import './style.scss';
</style>