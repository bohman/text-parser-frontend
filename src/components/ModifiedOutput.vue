<template>
  <div class="modified-output">
    <div class="modified-output--header">
      <a class="button" target="_blank" v-if="file_url" :href="file_url">Download original text</a>
      <a class="button" target="_blank" v-if="file_url" :href="file_url" >Download modified text</a>
      <button type="button" @click="toggleDisplayHighlights()">Highlight changes: {{ displayHighlights ? 'on' : 'off' }}</button>
      <button type="button" @click="clearData()">Analyze a new file</button>
    </div>
    <pre v-html="text"></pre>
  </div>
</template>

<script>
export default {
  name: 'ModifiedOutput',
  props: [
    'text',
    'file_url',
    'file_modified_url',
    'displayHighlights',
    'clearDataParent',
    'toggleDisplayHighlightsParent',
  ],
  methods: {
    clearData: function() {
      this.clearDataParent();
    },
    toggleDisplayHighlights: function() {
      this.toggleDisplayHighlightsParent();
    }
  }
}
</script>

<style lang="scss">
@import '../styles/components/modified-output';
</style>
