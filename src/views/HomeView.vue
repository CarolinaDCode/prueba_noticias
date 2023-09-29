<template>
  <v-container>
    <v-row>
      <v-col
        cols="12"
      >
        <v-text-field
          v-model="inputChapter" 
          @keyup.enter="getList">
        </v-text-field>
      </v-col>
      <v-col
        cols="12"
        v-if="resultFound"
      >
        <v-card>
          <v-card-title>
            Hemos encontrado {{ resultFound }} resultados para: {{ inputChapter }}
          </v-card-title>
        </v-card>
      </v-col>
    </v-row>
    <v-row>
      <v-col
          v-for="chapter of chapterList"
          :key="chapter.id"
          md="6"
          cols="12"
      >
        <ChapterItem
          :nota="chapter"
        />
      </v-col>
    </v-row>
  </v-container>
</template>
<script setup>
import { ref, watch } from 'vue';

import ChapterItem from '@/components/ChapterItem';

import axios from 'axios';

const inputChapter = ref('');

const resultFound = ref(0);

const chapterList = ref(null);

const getList = async() =>{
  try{

    let inputBox = inputChapter.value != '' ? inputChapter.value : ''

    const { data } = await axios.get(`https://opzz0lreh2.execute-api.us-east-1.amazonaws.com/prod/audioplayer/buscador?texto=${inputBox}`)
    chapterList.value = data.resultado.documentos;
    resultFound.value = data.resultado.numero_documentos;

  }catch(err){
    console.log(err);
  }

}

/**
 * Revisa los cambios del ingresados
 * en el buscador
 */
watch(inputChapter, () =>{
  if(inputChapter.value == ''){
    getList();
  }
})

</script>
