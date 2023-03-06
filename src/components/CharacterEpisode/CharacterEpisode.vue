<template>
    <div class="characterEpisodes">
        <p class="name">{{  episode.name }}</p>
        <p>Episódios - <strong>{{ episode.episode  }}</strong></p>
        <div>
            <p class="id">{{ episode.id}}</p>
        </div>
    </div>
</template>
<script setup>
import { onMounted, ref } from 'vue';
import api from '../../support/http/api'

const props = defineProps({
    data: { type: String, default: null },
})

const episode = ref({})

const getCharacterEpisode = async () => {
  try{
    await api.get(props.data).then((res)=>{
        episode.value = res.data
    })
  }catch (error) {
    console.error(error);
  }
}

onMounted(() =>{
    getCharacterEpisode()
})

</script>
<style lang="scss" scoped>
@import './style.scss';
</style>