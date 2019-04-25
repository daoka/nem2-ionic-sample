<template>
  <div class="ion-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>Hello NEM2 ionic</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <ion-item>
        <ion-input
         v-bind:value="address"
         v-on:input="address = $event.target.value"
        placeholder="input your address"></ion-input>
      </ion-item>
      <ion-item-divider>
        <ion-label>
          Public Key
        </ion-label>
      </ion-item-divider>
      <ion-item>
        {{ publicKey }}
      </ion-item>
      <ion-item-divider>
        <ion-label>
          Owned mosaics
        </ion-label>
      </ion-item-divider>
      <ion-list>
        <ion-item v-for="m in mosaics">
          <ion-label>{{ m.id.toHex() }}</ion-label>
          <ion-note slot="end">{{ m.amount.compact() }}</ion-note>
        </ion-item>
      </ion-list>
      <ion-button expand="block" @click="onClickButton()">Get Account Info</ion-button>
    </ion-content>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { Mosaic } from 'nem2-sdk';
import Nem2Client from '../libs/Nem2Client';

export default Vue.extend({
  name: 'home',
  data() {
    return {
      address: 'SA7OY4-IHRUZJ-LSM2IP-VDTZBO-OOFRLY-WKSKGC-TVGL',
      mosaics: new Array<Mosaic>(),
      publicKey: '',
    };
  },
  methods: {
    async onClickButton() {
      const a = await Nem2Client.getAccountInfo(this.address);
      this.publicKey = a.publicKey;
      this.mosaics = a.mosaics;
    },
  },
});
</script>
