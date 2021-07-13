<template>
  <div class="container">
    <textarea
      name="text"
      id="text-area"
      cols="30"
      rows="10"
      v-model="text"
      placeholder="Enter text..."
      class="form-control"
    ></textarea>
    <button
      @click="toastMe(text, 'text/plain', 'my-text.txt')"
      class="btn btn-primary"
      :disabled="text.length == 0"
    >
      Save text
    </button>
    <div class="image">
      <img
        src="https://picsum.photos/500/500"
        alt="dummy photo"
        crossorigin="anonymous"
        srcset=""
        @load="getDataUrl"
      />
    </div>
    <button
      @click="toastMe(img, 'image/jpeg', 'my-image.jpeg')"
      class="btn btn-primary"
    >
      Save picture
    </button>
  </div>
</template>

<script>
import { ref } from "vue"
import NotificationDownload from "./NotificationDownload.vue"
import { createToast, withProps } from "mosha-vue-toastify"
import "mosha-vue-toastify/dist/style.css"
export default {
  name: "HelloWorld",
  components: {
    NotificationDownload,
  },
  setup() {
    const text = ref("")
    const img = ""

    const toastMe = (data, type, outputName) => {
      createToast(
        withProps(NotificationDownload, {
          title: "Your download is ready!",
          data,
          type,
          outputName,
        }),
        {
          transition: "slide",
          position: "top-right",
          type: "success",
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
    return { toastMe, text, img }
  },
  methods: {
    getDataUrl(e) {
      const img = e.currentTarget
      const canvas = document.createElement("canvas")
      const ctx = canvas.getContext("2d")
      canvas.width = img.width
      canvas.height = img.height
      ctx.drawImage(img, 0, 0)
      this.img = canvas.toDataURL("image/jpeg")
    },
  },
}
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  gap: 5px;
}
a {
  color: #42b983;
}
img {
  border-radius: 8px;
  box-shadow: 0 13px 27px -5px hsla(240, 30.1%, 28%, 0.25),
    0 8px 16px -8px hsla(0, 0%, 0%, 0.3), 0 -6px 16px -6px hsla(0, 0%, 0%, 0.03);
}
</style>
