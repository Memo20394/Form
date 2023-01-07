<template>
  <q-page padding>
    <q-input
      v-model="textareaModel"
      filled
      type="textarea"
      color="red-12"
      label="Textarea with shadow text"
    />

    <q-btn round color="secondary" icon="send" @click="Send" />
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import { api } from "boot/axios";
import { Notify } from "quasar";
export default defineComponent({
  name: "IndexPage",
  data() {
    return { textareaModel: "" };
  },
  methods: {
    Send() {
      // console.log(this.textareaModel)
      // console.log(api)
      // const header = {
      //   "Content-Type" : "application/x-www-form-urlencoded",
      //   "Authorization" : "Bearer GqOmUoAyxaJX626osTbLCMIwBxc9UjIIDWjRCwYXBb0"

      // }
      const data = {
        message: this.textareaModel,
      };
      api
        .post("/msg", data)
        .then((respond) => {
          if (respond.status == 200) {
            console.log("Yay Complete");
            Notify.create({
              type : "positive",
              message : "Snap!"

            })
          }
        })
        .catch((error) => {
          console.log(error);
          Notify.create({
              type : "negative",
              message : "Decline"
              
            })
        });
      this.textareaModel = "";
    },
  },
});
</script>
