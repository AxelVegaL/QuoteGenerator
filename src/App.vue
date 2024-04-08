<script>

import Header from './components/Header.vue';
import Quote from './components/Quote.vue';
import translate from "translate";

translate.engine = 'deepl';
translate.key = 'a11d21a1-adec-455e-ab19-9bc16dcaf748:fx';

export default {
  name: 'App',
  components: {
    Header,
    Quote,
  },
  data() {
    return {
      quote: {
        //content: 'Content goes here...',
        content: 'Frase',
        anime: 'Serie',
        character: 'Personaje',
      },
      quotes: []
    }
  },
  methods: {
    async getQuote() {
      //const data = await fetch('https://animechan.vercel.app/api/random'). //API ya no disponible :c
      const data = await fetch('https://animechan.xyz/api/random').then(res => res.json()); //Cargar como json una API pública
      const translatedQuote = await translate(data.quote,'es');

      this.quote = {
        content: translatedQuote,
        anime: data.anime,
        character: data.character
      };
    }
  },
  created() {
    //this.getQuote();
  }
}


</script>

<template>

  <div class="app">
    <Header title="Generador de Frases"/> <!-- Se añade un valor del title dentro de Header.vue -->
    <Quote :quote="quote" />
    <div class="grid place-items-center mt-12">
      <button @click="getQuote"
      class="w-40 py-2 bg-red-600 text-white rounded-3xl hover:bg-red-500
      font-bold text-lg mt-4"
      >Generar</button>
    </div>
  </div>

</template>

<style lang="scss">

:root {
  --primary: #D81E5B;
  --secondary: #8A4FFF;
  --tertiary: #32CBFF;
  --dark: #131A26;
  --light: #EEE;
  --grey: #848484;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans, sans-serif';
}
</style>