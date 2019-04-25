<template>
  <div class="ion-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>Hello NEM2 ionic</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <ion-item>
        <ion-input v-model="address" placeholder="アドレスを入力してください" :value="address"></ion-input>
      </ion-item>
      <ion-item-divider>
        <ion-label>
          公開鍵
        </ion-label>
      </ion-item-divider>
      <ion-item>
        {{ publicKey }}
      </ion-item>
      <ion-item-divider>
        <ion-label>
          保有モザイク一覧
        </ion-label>
      </ion-item-divider>
      <ion-list>
        <ion-item v-for="m in mosaics">
          <ion-label>{{ m.id.toHex() }}</ion-label>
          <ion-note slot="end">{{ m.amount.compact() }}</ion-note>
        </ion-item>
      </ion-list>
      <ion-button expand="block" @click="onClickButton()">アカウント情報を取得</ion-button>
    </ion-content>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Nem2Client from '../libs/Nem2Client';
import { Mosaic, MosaicId } from 'nem2-sdk';

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
      console.log(a);
      this.publicKey = a.publicKey;
      this.mosaics = a.mosaics;
    },
  },
});
</script>
