<template>
  <h3>{{ title }}</h3>
  <a v-if="type === 'image/jpeg'" :href="data" :download="outputName" class="btn btn-primary">Download</a>
  <button v-else @click="downloadFile" class="btn btn-primary">Download</button>
</template>

<script>
import { saveAs } from "file-saver"
export default {
  props: {
    title: {
      type: String,
      default: "Download",
    },
    data: {
      type: [Object, String],
      required: true,
    },
    type: {
      type: String,
      required: true,
    },
    outputName: {
      type: String,
      default: "output",
    },
  },
  methods: {
    downloadFile() {
        const blob = new Blob([this.data], { type: this.type })
        saveAs(blob, this.outputName)
    },
  },
}
</script>

<style></style>
