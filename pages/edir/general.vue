<template>
  <div>
    <h1>Allgemein 👋</h1>
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-switch v-model="edir" flat label="EDir freigegeben"></v-switch>
      <v-select
        v-model="ieedir"
        :items="ieedir_typs"
        :rules="[(v) => !!v || 'device is required']"
        label="Wert fur IE EDIR"
        required
      ></v-select>
      <v-text-field
        v-model="une_es"
        label="UNE> ES EDIR"
        required
      ></v-text-field>
      <v-text-field
        v-model="une_rueckfallverh"
        :rules="serialRules"
        label="UNE> Rueckfallverhalten"
        required
      ></v-text-field>
      <v-text-field
        v-model="tune_verzougerung"
        label="tUNE> Verzougerung"
        required
      ></v-text-field>
      <v-text-field
        v-model="tune_verlaungerung"
        label="tUNE> Verlaungerung"
        required
      ></v-text-field>
      <v-switch v-model="qu2_wischer" flat label="qu2 Wischer"></v-switch>
      <v-switch v-model="qu4_wischer" flat label="qu4 Wischer"></v-switch>
      <v-switch v-model="cos_phi" flat label="cos (phi)"></v-switch>
      <v-switch v-model="sin_phi" flat label="sin (phi)"></v-switch>
      <v-radio-group v-model="row" row>
        <v-radio label="unempfindlich 1x" value="radio-1"></v-radio>
        <v-radio label="unempfindlich 2x" value="radio-2"></v-radio>
        <v-radio label="unempfindlich 20x" value="radio-3"></v-radio>
      </v-radio-group>
    </v-form>
  </div>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    edir: false,
    ieedir_typs: ['gemessen', 'berechnet'],
    ieedir: null,
    une_es: '',
    une_rueckfallverh: '',
    tune_verzougerung: '',
    tune_verlaungerung: '',
    qu2_wischer: true,
    qu4_wischer: true,
    sin_phi: true,
    cos_phi: true,
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
