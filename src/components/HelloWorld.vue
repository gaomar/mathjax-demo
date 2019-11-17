<template>
  <v-container>
    <v-layout
      text-center
      wrap
    >
      <v-flex xs12 class="py-12">
        <h1></h1>
      </v-flex>
      <v-flex xs12 class="py-12">
        <h1>数式結果</h1>
      </v-flex>

      <v-flex mb-4>
        <h1 class="display-2 font-weight-bold mb-3">
          <vue-mathjax :formula="formula" :safe="false"></vue-mathjax>
        </h1>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import {VueMathjax} from 'vue-mathjax'
export default {
  components: {
    'vue-mathjax': VueMathjax
  },  
  name: 'HelloWorld',
  data () {
    return {
      formula: '$$x = {-b \\pm \\sqrt{b^2-4ac} \\over 2a}.$$',
      msg: 'Welcome to Your Vue.js App',
      shiki: '',
      area: [],
      type: ''
    }
  },
  created () {
    var me = this
    const callbacks = {
      onUpdate(data) {
        if ('sekibun' in data) {
          me.type = data.sekibun.type
          me.shiki = data.sekibun.shiki
          me.area = data.sekibun.area.split('から')

          me.formula = `$$${me.type}${me.area[0]}^${me.area[1]} ${me.shiki}.$$`
        }
      },
    }
    interactiveCanvas.ready(callbacks)
  }
};
</script>
