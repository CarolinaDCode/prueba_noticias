<template>
    <v-card
        color="grey-lighten-3"
        class=" ma-1"
        min-height="400px"
        :title="nota.titulo"
    >
        <v-card-subtitle>
            <span>{{ chapterDate }}</span> |
            <span>Episodio {{ nota.episodio_num }}</span> |
            <span>{{ secondToMinute }}</span>
        </v-card-subtitle>
        <v-card-text>
            {{ nota.resumen }}
        </v-card-text>
        <div class="d-flex justify-center ma-1">
            <v-img
                :src="nota.img"
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
    nota : Object
});

const chapterDate = computed(() => new Date(props.nota.createdTime * 1000).toLocaleDateString("en-US"));

const secondToMinute = computed(() => {
    var hour = Math.floor(props.nota.media.duracionSec / 3600);
    hour = (hour < 10)? '0' + hour : hour;
    var minute = Math.floor((props.nota.media.duracionSec / 60) % 60);
    minute = (minute < 10)? '0' + minute : minute;
    var second = props.nota.media.duracionSec % 60;
    second = (second < 10)? '0' + second : second;
    return hour + ':' + minute + ':' + second;

});

</script>