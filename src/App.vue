<template>
  <div id="app" class="center spacing--large" v-bind:class="{ loading }">

    <h1 class="site-name">Text Parser</h1>

    <div class="legible">
      <p>This is a small app built to demonstrate web technologies. It accepts a file upload (that ought to be text), finds the most commonly used word, and surrounds all of the instances with <em>foo</em> and <em>bar</em>. The app has a decoupled <a href="https://github.com/bohman/text-parser-frontend">frontend</a> and <a href="https://github.com/bohman/text-parser-backend">backend</a>. Built with ❤ in Malmö by <a href="https://linusbohman.se">Linus Bohman</a>.</p>
    </div>

    <form v-if="!analysis.analysis" class="parse-form" method="post" :action="backendPostUrl" enctype="multipart/form-data" @submit.prevent="submit()" ref="form">
      <div class="form-item form-item--file-upload">
        <label for="upload">Text file</label>
        <input type="file" id="upload" name="upload" accept=".txt, .rtf, .md, .file" required>
        <button type="submit">Analyze</button>
      </div>
      <p class="description">A few things to note: your file should be one of the following formats: .txt, .rtf, .md, .file. This analysis is case insensitive. If there's a tie we consider the first match the most common word. Larger files take a longer time to process - be patient.</p>
    </form>

    <Error v-if="error" :text="error"></Error>

    <template v-if="analysis.analysis">
      <div class="pushes">
        <Push :large="analysis.analysis.word_count" small="total words"></Push>
        <Push :large="analysis.analysis.unique_word_count" small="unique words"></Push>
        <Push :large="analysis.analysis.most_common_word" small="most common word"></Push>
      </div>

      <ModifiedOutput
        :text="modifiedText"
        :file_url="analysis.file.file_url"
        :file_modified_url="analysis.file.file_modified_url"
        :displayHighlights="displayHighlights"
        :clearDataParent="clearData"
        :toggleDisplayHighlightsParent="toggleDisplayHighlights"></ModifiedOutput>
    </template>

  </div>
</template>

<script>
import Axios from 'axios'

import Push from './components/Push.vue'
import ModifiedOutput from './components/ModifiedOutput.vue'
import Error from './components/Error.vue'

let methods = {};
let computed = {};

methods.submit = async function() {
  this.loading = true;
  let formData = new FormData(this.$refs.form);
  const response = await Axios.post(this.backendPostUrl, formData);
  if(!response.data.analysis.word_count) {
    this.error = "You uploaded an empty file. That's no fun! Upload one with words! :)";
  } else {
    this.error = '';
    this.analysis = response.data;
  } 
  this.loading = false;
}

methods.clearData = function() {
  this.analysis = {};
  this.error = '';
}

methods.toggleDisplayHighlights = function() {
  this.displayHighlights = !this.displayHighlights;
}

computed.modifiedText = function() {
  if(this.analysis && !this.displayHighlights) {
    return this.analysis.modified_text;
  } else if(this.analysis && this.displayHighlights) {
    const original = this.analysis.modified_changes;
    const withHighlight = '<span class="highlight">$1</span>';
    const regexp = new RegExp('('+original+')', "gi");
    return this.analysis.modified_text.replace(regexp, withHighlight);
  } else {
    return '';
  }
}

export default {
  name: 'text-parser-frontend',
  methods: methods,
  computed: computed,
  data: function() {
    return {
      backendUrl: process.env.VUE_APP_BACKEND_URL,
      backendPostUrl: process.env.VUE_APP_BACKEND_POST_URL,
      analysis: {},
      error: '',
      displayHighlights: false,
      loading: false,
    }
  },
  components: {
    Push,
    ModifiedOutput,
    Error
  }
}
</script>

<style lang="scss">
@import 'styles/global.scss';
</style>
