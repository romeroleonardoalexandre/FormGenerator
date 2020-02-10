<template lang="html">
  <section class="dashboard">
    <div class="row">
      <div class="col-md-6 grid-margin stretch-card">
        <div class="card">
          <div class="card-body">
            <h4 class="card-title">Basic Tab</h4>
            <b-tabs>
              <b-tab title="Form" active>
                Aqui o formulario
              </b-tab>
              <b-tab title="JSON">
                Aqui vai o Json
              </b-tab>
            </b-tabs>
          </div>
        </div>
      </div>
      <div class="col-md-6 grid-margin stretch-card">
        <div class="card">
          <div class="card-body">
            <h4 class="card-title">Componentes</h4>
            <form class="forms-sample">
                <b-form-group label="Name"  label-for="input5">
                  <b-form-input type="text" id="input5" placeholder="Name"></b-form-input>
                </b-form-group>
                <b-form-group label="Text Area"  label-for="input10">
                  <b-form-textarea id="input10" v-model="text" placeholder="Message" :rows="3" :max-rows="6"></b-form-textarea>
                </b-form-group>
                <b-form-group label="Arquivo" label-for="input8">
                  <b-form-file v-model="file" id="inpu8" :state="Boolean(file)" placeholder="Choose a file..."></b-form-file>
                </b-form-group>
                <b-form-group horizontal label="Radio button">
                  <b-form-radio-group id="radios2" v-model="selected" name="radioSubComponent">
                    <b-form-radio value="Free">Free</b-form-radio>
                    <b-form-radio value="Professional">Professional</b-form-radio>
                  </b-form-radio-group>
                </b-form-group>
            </form>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script lang="js">
export default {
  name: 'playground'
}
</script>

<style scoped lang="scss">
</style>
