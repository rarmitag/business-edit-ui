<template>
  <v-dialog :value="bcolDialog" width="45rem" persistent :attach="attach" content-class="bcol-error-dialog">
    <v-card v-if="bcolObject">
      <v-card-title id="dialog-title">Payment Incomplete - {{bcolObject.title}}</v-card-title>

      <v-card-text>
        <p class="genErr" id="dialog-header">
          This {{filingType}} could not be filed for the following reason:
        </p>
        <p class="genErr" id="dialog-content" v-html="bcolObject.detail"></p>

        <template v-if="!isRoleStaff">
          <p class="genErr">
            Your {{filingType}} has been saved as a draft and you
            can retry your payment from the dashboard once the issue has been resolved.
          </p>
        </template>
      </v-card-text>

      <v-divider class="my-0"></v-divider>

      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn id="dialog-exit-button" color="primary" text @click="exit()">Back to My Dashboard</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script lang="ts">
import { Component, Vue, Prop, Emit } from 'vue-property-decorator'
import { Getter } from 'vuex-class'

@Component({})
export default class BcolErrorDialog extends Vue {
  // Global getters
  @Getter isRoleStaff!: boolean

  @Prop() private filingType: string

  @Prop({ default: () => { return null as object } }) private bcolObject: object

  // Prop to provide attachment selector.
  @Prop() private attach: string

  // Pass click event to parent.
  @Emit() private exit () { }

  private get bcolDialog (): boolean {
    return !!this.bcolObject
  }
}
</script>

<style lang="scss" scoped>
// @import '@/assets/styles/theme.scss';
</style>
