<template>
    <v-container grid-list-md>
  <v-tabs icons-and-text fixed-tabs>
    <v-tab href="#tab-1">
      App config
      <v-icon>info</v-icon>
    </v-tab>
    <v-tab href="#tab-2">
      Email config
      <v-icon>code</v-icon>
    </v-tab>
    <v-tab href="#tab-3">
      Price config
      <v-icon>settings</v-icon>
    </v-tab>
    <v-tab href="#tab-4">
      Storage config
      <v-icon>photo_camera</v-icon>
    </v-tab>
    <v-tab-item
      v-for="i in 4"
      :key="i"
      :value="'tab-' + i"
    >
      <v-card v-if="i === 1" flat>
         <app-config></app-config>
      </v-card>
      <v-card v-if="i === 2" flat>
        <email-config></email-config>
      </v-card>
      <v-card v-if="i === 3" flat>
        <price-config></price-config>
      </v-card>
      <v-card v-if="i === 4" flat>
        <storage-config></storage-config>
      </v-card>
    </v-tab-item>
  </v-tabs>
    </v-container>
</template>

<script>
  import AppConfig from './AppConfig';
  import EmailConfig from './EmailConfig';
  import PriceConfig from './PriceConfig';
  import StorageConfig from './StorageConfig';

  export default {
    name: 'tabs',
    data() {
      return {
      };
    },
    components: {
      'app-config': AppConfig,
      'email-config': EmailConfig,
      'price-config': PriceConfig,
      'storage-config': StorageConfig
    },
    mounted() {
      // this.$store.dispatch('fetchContainers');
      // console.log(this.$store.getters.containersTableData);
    }
  };
</script>
