<template>
  <ion-toolbar color="primary">
    <ion-buttons>
      <ion-button>
        <ion-icon slot="start" :icon="logoWhatsapp"></ion-icon>
        <ion-title class="ion-text-capitalize">{{ title }}</ion-title>
      </ion-button>
    </ion-buttons>
  </ion-toolbar>

  <div class="ion-padding">
    <ion-card>
      <ion-card-header class="ion-text-center">
        <ion-card-title>{{ title }}</ion-card-title>
        <ion-card-subtitle>
          write the phone number bellow to start the conversation without save
          it as contact
        </ion-card-subtitle>
      </ion-card-header>
      <ion-card-content>
        <ion-item>
          <ion-label position="stacked">{{ label1 }} (require)</ion-label>
          <ion-input :placeholder="label1" v-model="number"></ion-input>
        </ion-item>
        <ion-item>
          <ion-label position="stacked">{{ label2 }} (optional)</ion-label>
          <ion-textarea
            :placeholder="label2"
            v-model="msg"
            rows="3"
          ></ion-textarea>
        </ion-item>
      </ion-card-content>
      <ion-card-content class="ion-text-center">
        <ion-button :disabled="!number" @click="sendMessage()">
          send message
        </ion-button>
      </ion-card-content>
    </ion-card>
  </div>
</template>

<script>
import {
  IonTitle,
  IonToolbar,
  IonIcon,
  IonButton,
  IonButtons,
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardSubtitle,
  IonCardContent,
  IonInput,
  IonTextarea,
  IonLabel,
  IonItem,
} from "@ionic/vue"
import { defineComponent } from "vue"
import { logoWhatsapp } from "ionicons/icons"

export default defineComponent({
  components: {
    IonTitle,
    IonToolbar,
    IonIcon,
    IonButton,
    IonButtons,
    IonCard,
    IonCardHeader,
    IonCardTitle,
    IonCardSubtitle,
    IonCardContent,
    IonInput,
    IonTextarea,
    IonLabel,
    IonItem,
  },
  data: () => ({
    // icons
    logoWhatsapp,
    // api
    whatsappAPI: "https://api.whatsapp.com/send?phone=",
    // data
    title: "Whatsapp unsaved contacts",
    label1: "Phone Number",
    label2: "Your Message",
    msg: "",
    number: "",
  }),
  methods: {
    sendMessage() {
      if (this.number) {
        let url = this.whatsappAPI + this.number
        if (this.msg) {
          url += "&text=" + this.msg
        }
        window.open(url)
      }
    },
  },
})
</script>

<style scoped>
ion-card {
  max-width: 500px;
  margin: 30px auto;
  box-shadow: 2px 2px 10px;
}
</style>
