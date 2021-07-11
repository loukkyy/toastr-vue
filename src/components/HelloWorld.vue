<template>
  <button @click="toastMe">Click me</button>
</template>

<script>
import NotificationDownload from "./NotificationDownload.vue"
import { createToast } from "mosha-vue-toastify"
import "mosha-vue-toastify/dist/style.css"
export default {
  name: "HelloWorld",
  components: {
    NotificationDownload,
  },
  setup() {
    const toastMe = () => {
      console.log("it works")
      createToast(
        withProps(NotificationDownload, { title: "this is a test" }),
        {
          transition: "slide",
          position: "top-left",
          type: "info",
          showIcon: true,
          swipeClose: true,
          hideProgressBar: false,
          timeout: -1,
          onClose: () => {
            console.log("log")
          },
        }
      )
    }
    return { toastMe }
  },
}
</script>

<style scoped>
a {
  color: #42b983;
}
</style>
