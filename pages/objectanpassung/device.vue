<template>
  <div>
    <h1>Gerauteanpassung👋</h1>
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-select
        v-model="schutz"
        :items="schutz_typ"
        :rules="[(v) => !!v || 'device is required']"
        label="Schutzobject"
        required
      ></v-select>
      <v-text-field
        v-model="ur_spannung"
        :counter="10"
        label="Ur Bemessungsspannung"
        required
      ></v-text-field>
    </v-form>
  </div>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    ur_spannung: '',
    schutz: null,
    schutz_typ: ['Sternpunkt', 'Standard', 'Motor'],
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
