<template>
  <v-container>
    <HEADER></HEADER>
    <v-file-input label="File input" filled prepend-icon="mdi-camera" v-model="files" multiple></v-file-input>
    <v-btn @click="sendFiles">
      <v-icon>mdi-send</v-icon>
    </v-btn>
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
import HEADER from "./header.vue";

export default {
  name: "InputImage",
  components: {
    HEADER,
  },
  data: () => ({
    files: [],
    issues: [],
    url: "",
  }),
  methods: {
    sendFiles() {
      console.log(this.files);
      console.log(AXIOS);

      var options = {
        Authorization: this.$store.getters.getToken,
        "Content-Type": "multipart/form-data",
      };
      let formData = new FormData();
      for (let i = 0; i < this.files.length; i++) {
        formData.append("file" + i, this.files[i]);
      }
      AXIOS.post("/image", formData, options).then(function (response) {
        var issue = response.data.info;
        files = response.data.image;
        if (issue.includes(0)) {
          issues.push("issue1");
        }
        if (issue.includes(1)) {
          issues.push("issue1");
        }
        if (issue.includes(2)) {
          issues.push("issue2");
        }
      });
    },
    getUrl(file) {
      return URL.createObjectURL(file);
    },
  },
};
</script>

<style scope>
img {
  width: 15vw;
}
</style>