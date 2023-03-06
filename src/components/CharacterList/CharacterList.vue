<template>
    <div class="characterList">
      <div class="characterList_container">
       <div class="characterList_content">
          <character-card v-for="(item, index) in character.results" :key="index" :data="item"/>
       </div>
      </div>
    </div>
  </template>
<script setup>
import { onMounted, ref } from 'vue';
import CharacterCard from '../CharacterCard/CharacterCard.vue';
import api from '../../support/http/api'

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