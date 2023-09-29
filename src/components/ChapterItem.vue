<template>
    <v-card
        color="grey-lighten-3"
        class=" ma-1"
        min-height="400px"
        :title="chapter.titulo"
    >
        <v-card-subtitle>
            <span>{{ chapterDate }}</span> |
            <span>Episodio {{ chapter.episodio_num }}</span> |
            <span>{{ secondToMinute }}</span>
        </v-card-subtitle>
        <v-card-text>
            {{ chapter.resumen }}
        </v-card-text>
        <div class="d-flex justify-center ma-1">
            <v-img
                :src="chapter.img"
                width="150"
                height="150"
            >
            </v-img>
        </div>
    </v-card>
</template>
<script setup>
import { defineProps, computed } from 'vue'; 

const props = defineProps({ 
    chapter : Object
});

const chapterDate = computed(() => new Date(props.chapter.createdTime * 1000).toLocaleDateString("en-US"));

const secondToMinute = computed(() => {
    var hour = Math.floor(props.chapter.media.duracionSec / 3600);
    hour = (hour < 10)? '0' + hour : hour;
    var minute = Math.floor((props.chapter.media.duracionSec / 60) % 60);
    minute = (minute < 10)? '0' + minute : minute;
    var second = props.chapter.media.duracionSec % 60;
    second = (second < 10)? '0' + second : second;
    return hour + ':' + minute + ':' + second;

});

</script>