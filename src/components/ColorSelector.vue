<template>
  <v-text-field v-model="val" filled :label="title" dense hide-details :disabled="disabled">
    <v-avatar slot="prepend" :color="color" size="33" class="mt-n1 mr-n1"></v-avatar>
    <v-menu slot="append-outer" bottom offset-y :close-on-content-click="false">
      <template v-slot:activator="{ on, attrs }">
        <v-btn icon class="mt-n1 ml-n2" v-bind="attrs" v-on="on" :disabled="disabled">
          <v-icon>mdi-eyedropper-plus</v-icon>
        </v-btn>
      </template>
      <v-card>
        <v-color-picker v-model="val" :disabled="disabled" />
      </v-card>
    </v-menu>
  </v-text-field>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'color-selector',
  props: ['value', 'title', 'disabled'],
  computed: {
    val: {
      get(): string {
        const self = this as any
        return self.value
      },
      set(val) {
        const self = this as any
        self.$emit('input', val)
      },
    },
    color(): string {
      return (this.val as string) || ''
    },
  },
})
</script>
