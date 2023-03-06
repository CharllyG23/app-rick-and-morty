<template>
    <section class="banner">
      <div class="banner_container">
        <div class="_image">
            <img :src="rick" alt="rick and morty"/>
        </div>
      </div>
    </section>
    <section class="sectionList">
      <character-list></character-list>
    </section>
</template>
<script setup>
import CharacterList from '../../components/CharacterList/CharacterList.vue';
import rick from '../../assets/img/rick.png'
</script>
<style lang="scss" scoped>
@import './style.scss';
</style>