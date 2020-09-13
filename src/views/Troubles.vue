<template>
  <v-container>
    <v-row>
      <v-col class="col-4" v-for="trouble in troubles" :key="trouble.id">
        <v-hover v-slot:default="{ hover }" close-delay="100">
          <v-card :elevation="hover ? 16 : 2"  class="mx-auto">
            <v-card-title>
              <v-overflow-btn
                :id="trouble.id"
                v-model="selected"
                @change="sendUpdate(trouble.id)"
                :items="statuses"
                :label="trouble.troubleStatus"
              ></v-overflow-btn>
            </v-card-title>
            <v-card-text>
              <v-img :src="trouble.imageUrl"></v-img>
            </v-card-text>
            <v-card-actions>
              <v-chip-group
                v-for="type in trouble.troubleTypes"
                active-class="deep-purple--text text--accent-4"
                mandatory
              >
                <v-chip>{{type}}</v-chip>
              </v-chip-group>
            </v-card-actions>
          </v-card>
        </v-hover>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import { AXIOS } from "../main";

export default {
  name: "Troubles",
  selected: "",
  data: () => ({
    statuses: ["TO_DO", "IN_PROGRESS", "CHECK", "DONE"],
    troubles: [
      {
        id: 1,
        troubleStatus: "TO_DO",
        imageUrl:
          "https://sun1-86.userapi.com/cnbhkgD-wAUP5X_TrFhxKz9ApOuAGMTnwzUwyw/bNgEHlwVC7s.jpg",
        troubleTypes: ["A", "B"],
      },
      {
        id: 2,
        troubleStatus: "TO_DO",
        imageUrl:
          "https://sun1-86.userapi.com/cnbhkgD-wAUP5X_TrFhxKz9ApOuAGMTnwzUwyw/bNgEHlwVC7s.jpg",
        troubleTypes: ["A", "B"],
      },
      {
        troubleStatus: "TO_DO",
        imageUrl:
          "https://sun1-86.userapi.com/cnbhkgD-wAUP5X_TrFhxKz9ApOuAGMTnwzUwyw/bNgEHlwVC7s.jpg",
        troubleTypes: ["A", "B"],
      },
      {
        troubleStatus: "TO_DO",
        imageUrl:
          "https://sun1-86.userapi.com/cnbhkgD-wAUP5X_TrFhxKz9ApOuAGMTnwzUwyw/bNgEHlwVC7s.jpg",
        troubleTypes: ["A", "B"],
      },
    ],
  }),
  methods: {
    getTroubles() {
      let self = this;
      let options = {
        headers: {
          Authorization: this.$store.getters.getToken,
        },
      };
      AXIOS.get("/trouble", options)
        .then((res) => {})
        .catch((err) => {
          console.log(err);
        });
    },
    sendUpdate: function (id) {
      let options = {
        headers: { Authorization: this.$store.getters.getToken },
      };
      console.log(options);
      AXIOS.post("/trouble/" + id, { newStatus: this.selected }, options)
        .then(() => {
          console.log("success");
        })
        .catch((err) => console.log(err));
    },
  },
  mounted() {
    this.getTroubles();
  },
};
</script>

<style scope>
</style>