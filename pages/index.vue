<template>
  <v-layout
    column
    justify-center
    align-center
  >
    <v-flex
      xs12
      sm8
      md6
    >
      <v-form ref="form">
        <v-file-input 
          accept="image/*"
          label="画像を選択してください"
          show-size
          prepend-icon="mdi-image"
          outlined
          dense
        @change="onImageSelect"
        ></v-file-input>
        <img v-if="imageUrl" :src="imageUrl" />
      </v-form>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  data() {
    return {
      imageUrl: "",
    }
  },
  methods: {
    onImageSelect(file) {
      if (file !== undefined && file !== null) {
        if (file.name.lastIndexOf('.') <= 0) {
          return
        }
        const fr = new FileReader()
        fr.readAsDataURL(file)
        fr.addEventListener('load', () => {
          this.imageUrl = fr.result
        })
      } else {
        this.imageUrl = ''
      }
    }
  }
}
</script>
