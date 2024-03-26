<script setup>
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
  IonItem,
  alertController,
} from "@ionic/vue"
import {
  logoWhatsapp,
  helpCircle,
  callOutline,
  chatboxOutline,
} from "ionicons/icons"
import { Capacitor } from "@capacitor/core"
import { ref } from "vue"

// data
/// static
const title = "Whatsapp unsaved"
/// dynamic
const number = ref("")
const msg = ref("")

// methods
/// get whatsapp api url
function getWhatsappAPIurl() {
  const isWeb = Capacitor.getPlatform() === "web"

  return `https://${isWeb ? "web" : "api"}.whatsapp.com/send?phone=`
}
/// send the message
function sendMessage() {
  let url = getWhatsappAPIurl() + number.value
  if (msg.value) {
    url += "&text=" + msg.value
  }
  window.open(url)
}

async function showInfo() {
  const alert = await alertController.create({
    header: "About App",
    message:
      "This app is a simple tool to send a message to a phone number in whatsapp without saving it as a contact",
    buttons: ["Nice"],
  })
  await alert.present()
}
</script>

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
      <ion-card-header class="ion-text-center" v-if="false">
        <ion-card-title class="ion-margin-bottom">
          {{ title }}
        </ion-card-title>
        <ion-card-subtitle>
          write the phone number bellow to start the conversation without save
          it as contact
        </ion-card-subtitle>
      </ion-card-header>
      <ion-card-header>
        <h4><b>NOTE:</b></h4>
        <p class="ion-text-capitalize">
          phone number should include the international code (eg: +212545454)
        </p>
      </ion-card-header>
      <ion-card-content>
        <ion-item class="ion-margin-vertical">
          <ion-input
            v-model="number"
            label-placement="stacked"
            required
            label="Phone Number (required)"
            placeholder="Phone Number"
          >
            <ion-icon
              slot="start"
              :icon="callOutline"
              aria-hidden="true"
            ></ion-icon>
          </ion-input>
        </ion-item>
        <ion-item class="ion-margin-vertical">
          <ion-textarea
            v-model="msg"
            label-placement="stacked"
            label="Message (optional)"
            placeholder="Message"
          >
            <ion-icon
              slot="start"
              :icon="chatboxOutline"
              aria-hidden="true"
            ></ion-icon>
          </ion-textarea>
        </ion-item>
      </ion-card-content>
      <ion-card-content class="ion-text-center">
        <ion-button @click="sendMessage()"> send message </ion-button>
      </ion-card-content>
    </ion-card>
  </div>
</template>

<style scoped>
ion-card {
  max-width: 500px;
  margin: 10px auto;
}
</style>
