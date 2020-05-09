<template class="body">
  <div class="container">
    <b-row class="mt-5" v-if="!images.length">
      <b-col>
        <b-spinner label="Loading images" variant="primary"></b-spinner>
      </b-col>
    </b-row>
    <div class="gallery">
      <template v-for="image in images">
        <img
          :src="image.url"
          :key="image.id"
          :alt="`Image of ${image.name} meme`"
          class="meme-thumb"
          v-b-modal.modal-1
          @click="imgToEdit = image.url"
        />
      </template>
    </div>
    <b-modal size='xl' id="modal-1" title="Editor" hide-footer="true">

      <Editor :imgToEdit="imgToEdit" />

    </b-modal>
  </div>
</template>
<script>
import Editor from '@/components/Editor.vue'

export default {
  name: 'Gallery',
  components: { Editor },
  data() {
    return {
      images: [],
      imgToEdit: ''
    }
  },
  created() {
    fetch('https://api.imgflip.com/get_memes')
      .then((response) => response.json())
      .then((response) => (this.images = response.data.memes))
      .catch((err) => console.log(err))
  },
}




</script>
<style scoped>

.default {
    width: 600px;
}

.gallery {
    display: flex;
    flex-wrap: wrap;
}


.gallery img {
    height: 200px;
    flex: 1 0 auto;
}


</style>