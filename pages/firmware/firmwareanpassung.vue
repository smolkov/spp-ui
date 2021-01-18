<template>
  <div>
    <h1>Firmwareanpassung👋</h1>
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-text-field
        v-model="serial"
        :counter="10"
        :rules="serialRules"
        label="Serrial"
        required
      ></v-text-field>
      <v-select
        v-model="select"
        :items="device_typs"
        :rules="[(v) => !!v || 'device is required']"
        label="Geraetetyp"
        required
      ></v-select>
      <v-radio-group v-model="row" row>
        <v-radio label="unempfindlich 1x" value="radio-1"></v-radio>
        <v-radio label="unempfindlich 2x" value="radio-2"></v-radio>
        <v-radio label="unempfindlich 20x" value="radio-3"></v-radio>
      </v-radio-group>

      <v-btn :disabled="!valid" color="success" class="mr-4" @click="validate">
        Send
      </v-btn>
      <v-btn color="error" class="mr-4" @click="reset"> Reset </v-btn>
      <v-btn color="warning" @click="resetValidation"> Reset Validation </v-btn>
    </v-form>
  </div>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    serial: '',
    serialRules: [
      (v) => !!v || 'Name is required',
      (v) => (v && v.length <= 10) || 'Name must be less than 10 characters',
    ],
    email: '',
    emailRules: [
      (v) => !!v || 'E-mail is required',
      (v) => /.+@.+\..+/.test(v) || 'E-mail must be valid',
    ],
    device: null,
    device_typs: [
      'DS6 PR20 4I',
      'DSE6 PR21 4I+1U',
      'DSR6 PR22 3I+3U',
      'DSRE PR23 4I+3U',
      'DSRY6 PR24 4I+4U',
      'DS6-0 PR20 Basis',
      'DS6-0 PR20 FE1',
      'DSREY6-0 PR24 Basis',
      'DSREY6-0 PR24 FE1',
    ],
    items: ['Item 1', 'Item 2', 'Item 3', 'Item 4'],
    checkbox: false,
    row: null,
  }),
  methods: {
    validate() {
      this.$refs.form.validate()
    },
    reset() {
      this.$refs.form.reset()
    },
    resetValidation() {
      this.$refs.form.resetValidation()
    },
  },
}
</script>
