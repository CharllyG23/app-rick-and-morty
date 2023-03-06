<template>
  <div class="bg-black">
    <section class="banner">
      <div class="banner_container">
        <div class="_image">
            <img :src="card" alt="rick and morty"/>
        </div>
      </div>
    </section>
    <section class="pt-10">
      <character-search @search-character="setSearchCharacter"/>
    </section>
    <main>
      <character-list :search="searchCharacter"></character-list>
    </main>
  </div>
</template>
<script setup>
import CharacterList from '../../components/CharacterList/CharacterList.vue';
import CharacterSearch from '../../components/CharacterSearch/ChararterSearch.vue';
import card from '../../assets/img/rick-card.png'
import { ref } from 'vue';

const searchCharacter = ref({})

const setSearchCharacter = (data) =>{
  searchCharacter.value = data
}
</script>
<style lang="scss" scoped>
@import './style.scss';
</style>