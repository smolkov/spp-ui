<template>
  <div>
    <h1>LS-Anpassung 👋</h1>
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-switch v-model="lsHandEin" flat label="Signal LS-Hand-Ein"></v-switch>
      <v-switch v-model="lsBereit" flat label="Signal LS Bereit"></v-switch>
      <v-switch
        v-model="lsFallMeldung"
        flat
        label="Unterbrechen LC-FallMeldung"
      ></v-switch>
      <v-select
        v-model="auskreis1"
        :items="auskreis_typ"
        :rules="[(v) => !!v || 'parameter is required']"
        label="Auskreisuberw. 1"
        required
      ></v-select>
      <v-switch v-model="blockAusKr1" flat label="Block. AusKrUbw.1"></v-switch>
      <v-text-field
        v-model="tauskteis1"
        :counter="10"
        label="tAuskreisunberw.1"
      ></v-text-field>
      <v-select
        v-model="auskreis2"
        :items="auskreis_typ"
        :rules="[(v) => !!v || 'parameter is required']"
        label="Auskreisuberw. 2"
        required
      ></v-select>
      <v-switch v-model="blockAusKr2" flat label="Block. AusKrUbw.2"></v-switch>
      <v-text-field
        v-model="tauskteis2"
        :counter="10"
        label="tAuskreisunberw.2"
      ></v-text-field>
      <v-select
        v-model="auskreis3"
        :items="auskreis_typ"
        :rules="[(v) => !!v || 'parameter is required']"
        label="Auskreisuberw. 3"
        required
      ></v-select>
      <v-switch v-model="blockAusKr3" flat label="Block. AusKrUbw.3"></v-switch>
      <v-text-field
        v-model="tauskteis3"
        :counter="10"
        label="tAuskreisunberw.3"
      ></v-text-field>
      <v-text-field
        v-model="tEinDauerLsEin"
        :counter="10"
        label="tEin Dauer LS-Ein"
      ></v-text-field>
    </v-form>
  </div>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    lsHandEin: false,
    lsBereit: true,
    lsFallMeldung: true,
    auskreis1: null,
    tauskteis1: '2.0',
    blockAusKr1: false,
    auskreis2: null,
    blockAusKr2: false,
    tauskteis2: '2.0',
    auskreis3: null,
    blockAusKr3: false,
    tauskteis3: '2.0',
    tEinDauerLsEin: '0.10',
    auskreis_typ: ['gesperrt', 'mit 1 BE', 'mit 2 BE'],
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
