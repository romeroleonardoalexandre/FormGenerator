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
