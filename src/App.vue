<template>
  <ion-toolbar color="primary">
    <ion-buttons slot="start">
      <ion-button>
        <ion-icon :icon="logoWhatsapp"></ion-icon>
      </ion-button>
    </ion-buttons>
    <ion-buttons slot="end">
      <ion-button @click="showInfo">
        <ion-icon :icon="helpCircle"></ion-icon>
      </ion-button>
    </ion-buttons>

    <ion-title class="ion-text-center ion-text-capitalize">
      {{ title }}
    </ion-title>
  </ion-toolbar>

  <div class="ion-margin">
    <ion-card>
      <ion-card-header class="ion-text-center">
        <ion-card-title class="ion-margin-bottom">
          {{ title }}
        </ion-card-title>
        <ion-card-subtitle>
          write the phone number bellow to start the conversation without save
          it as contact
        </ion-card-subtitle>
      </ion-card-header>
      <ion-card-content>
        <h4>NOTE:</h4>
        <p class="ion-text-capitalize">
          phone number should include the international code (eg: +212545454)
        </p>
      </ion-card-content>
      <ion-card-content>
        <ion-item>
          <ion-label position="stacked">{{ label1 }} (require)</ion-label>
          <ion-input
            :placeholder="label1 + ` (eg: +212545454)`"
            v-model="number"
          ></ion-input>
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
  alertController,
} from "@ionic/vue"
import { defineComponent } from "vue"
import { logoWhatsapp, helpCircle } from "ionicons/icons"

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
    helpCircle,
    // api
    whatsappAPI: "https://api.whatsapp.com/send?phone=",
    // data
    title: "Whatsapp unsaved contacts",
    label1: "Phone Number",
    label2: "Your Message",
    number: "",
    msg: "",
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
    async showInfo() {
      const alert = await alertController.create({
        header: "About App",
        message:
          "A very basic ionc/vue app that let you chating with any whatsapp user without save his/her phone number in your device",
        buttons: ["Nice"],
      })
      await alert.present()
    },
  },
})
</script>

<style scoped>
ion-card {
  max-width: 500px;
  margin: 50px auto;
  box-shadow: 2px 2px 10px;
}
</style>
