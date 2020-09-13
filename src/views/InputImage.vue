<template>
  <v-container>
    <v-file-input
      label="File input"
      filled
      prepend-icon="mdi-camera"
      v-model="files"
      multiple
      placeholder="Внесите все файлы которые надо проверить"
      @change="handleFileUpload()"
      small-chips
      counter
      show-size
      accept="image/png, image/jpeg, image/jpg, image/bmp"
    ></v-file-input>
    <v-card-actions class="justify-center">
      <v-btn @click="sendFiles">
        <v-icon>mdi-send</v-icon>
      </v-btn>
    </v-card-actions>
    <v-divider></v-divider>
    <v-row>
      <v-col v-for="file in files" :key="file.index" class="xs-2">
        <div>
          <img :src="getUrl(file)" />
          <ul v-for="issue in issues" :key="issue" class="xs-2">
            <li>
              <p>{{issue}}</p>
            </li>
          </ul>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import { AXIOS } from "../main";

export default {
  name: "InputImage",
  data: () => ({
    files: [],
    issues: [],
    url: "",
  }),
  methods: {
    sendFiles() {
      console.log(this.files);
      var options = {
        headers: {
          Authorization: this.$store.getters.getToken,
          "Content-Type": "multipart/form-data",
        },
      };
      let formData = new FormData();
      for (var i = 0; i < this.files.length; i++) {
        let file = this.files[i];
        formData.append("files", file);
      }

      console.log(formData);
      AXIOS.post("/image", formData, options).catch((err) =>
        console.error(err)
      );
    },
    getUrl(file) {
      return URL.createObjectURL(file);
    },
    handleFileUpload() {},
  },
};
</script>

<style scope>
img {
  width: 15vw;
}
</style>