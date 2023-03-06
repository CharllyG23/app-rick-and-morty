<template>
    <div class="characterCard">
      <div class="characterCard_content"  @click="openModal">
        <div>
          <h3 class="title">{{data.name}}</h3>
          <div class="info">
            <p class="text-amber-300">Gênero: {{data.gender}}</p>
            <p>Espécies: {{data.species}}</p>
          </div>
         <div class="statu">
           <div :class="data.status" class="statu_status">
            <p>{{ data.status  }}</p>
           </div>
          </div>
        </div>
        <div class="image_container">
          <img v-if="!loading" :src="data.image " :alt="data.name" />
        </div>
      </div>
    </div>
    <character-details v-model="isActive" :info="props.data"></character-details>
  </template>
<script setup>
import { ref } from 'vue'
import CharacterDetails from '../CharacterDetails/CharacterDetails.vue';

  const props = defineProps({
    data: { type: Object, required: true},
  })
  
  const loading = ref(false)
  const isActive = ref(false)

  const openModal = () =>{
  isActive.value = true
}
</script>
<style lang="scss" scoped>
@import './style.scss';
@import '../../assets/scss/character_status.scss';

.Dead {
  background-color: $dead;
}
.Alive{
  background-color: $alive;
}
.unknown{
  background-color: $unknown;
}

</style>
  