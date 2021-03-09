<template>
  <v-menu v-model="menu" :close-on-content-click="false" :min-width="width">
    <template v-slot:activator="{ on: menu, attrs }">
      <v-tooltip bottom>
        <template v-slot:activator="{ on: tooltip }">
          <v-btn
            color="info"
            icon
            v-bind="attrs"
            v-on="{ ...tooltip, ...menu }"
          >
            <v-icon v-text="icon"></v-icon>
          </v-btn>
        </template>
        <span v-text="tooltip_text"></span>
      </v-tooltip>
    </template>
    <v-card>
      <template slot="progress">
        <v-progress-linear
          color="deep-purple"
          height="10"
          indeterminate
        ></v-progress-linear>
      </template>
      <slot name="card-title">
        <v-card-title class="headline grey lighten-2">
          {{ title_text }}
          <v-spacer></v-spacer>
          <v-btn color="white" icon @click="menu = false">
            <v-icon>mdi-close-circle-outline</v-icon>
          </v-btn>
        </v-card-title>
        <v-card-text>
          <nuxt-content :document="info" />
        </v-card-text>
      </slot>
    </v-card>
  </v-menu>
</template>

<script>
export default {
    name: 'InfoMenu',
    props: {
        width: {type: Number, required: false, default: 500},
        icon: {type: String, required: false, default: 'mdi-information-outline'},
        tooltip_text: {type: String, required: false, default: 'Click for Info'},
        title_text: {type: String, required:false, default: 'Information'},
        path: {type: String, required: false, default: 'info'},
        document: {type: String, required: true}
    },
    data() {
        return {
            loading: true,
            menu: false,
            info: {}
        }
    },
    async created() {
        const info = await this.$content(this.path, this.document).fetch()
        this.info = info
        this.loading = false
    }
};
</script>

<style>
</style>
