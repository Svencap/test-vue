<template>
  <v-container>
    <PhotoFormVue @addPhoto="addPhoto"/>
    <v-row>
      <Photo v-for="photo in photos" :key="photo.id" :photo="photo" @openPhoto="openPhoto"/>
    </v-row>
    <PhotoDialog :photo="currentPhoto" v-model="dialogVisible"/>
  </v-container>
</template>

<script>
import Photo from "@/components/photo/Photo.vue";
import PhotoFormVue from "@/components/photo/PhotoForm.vue";
import PhotoDialog from '@/components/photo/PhotoDialog.vue';

export default {
  name: "PhotosPage",
  data: () => ({
    photos: [],
    currentPhoto: {},
    dialogVisible: false,
  }),
  components: { Photo, PhotoFormVue, PhotoDialog },
  mounted() {
    this.fetchTodo();
  },
  methods: {
    fetchTodo() {
      this.axios
        .get("https://jsonplaceholder.typicode.com/photos?_limit=10")
        .then((res) => (this.photos = res.data));
    },
    addPhoto(photo) {
      this.photos.push(photo);
    },
    openPhoto(photo) {
      this.currentPhoto = photo;
      this.dialogVisible = true;
    }
  },
};
</script>

<style>
</style>