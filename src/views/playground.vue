<template lang="html">
  <section class="dashboard">
    <div class="row">
      <div class="col-md-8 grid-margin stretch-card">
        <div class="card">
          <div class="card-body">
            <h4 class="card-title">Criar</h4>
            <b-tabs>
              <b-tab title="Form" active>
                <div class="drags row">

                  <div class="dropzone col-md-12">
                    
                  </div>
                </div>
              </b-tab>
              <b-tab title="JSON">
                Aqui vai o Json
              </b-tab>
            </b-tabs>
          </div>
        </div>
      </div>
      <div class="col-md-4 grid-margin stretch-card">
        <div class="card">
          <div class="card-body">
            <h4 class="card-title">Componentes</h4>
            
              <b-form-group label="Name"  label-for="input5">
                <b-form-input type="text" placeholder="Name"></b-form-input>
              </b-form-group>
              <b-form-group label="Text Area"  label-for="input10">
                <b-form-textarea v-model="text" placeholder="Message" :rows="3" :max-rows="6"></b-form-textarea>
              </b-form-group>
              <b-form-group label="Arquivo" label-for="input8">
                <b-form-file v-model="file" :state="Boolean(file)" placeholder="Choose a file..."></b-form-file>
              </b-form-group>
              <b-form-group horizontal label="Radio button">
                <b-form-radio-group v-model="selected" name="radioSubComponent">
                  <b-form-radio value="Free">Free</b-form-radio>
                  <b-form-radio value="Professional">Professional</b-form-radio>
                </b-form-radio-group>
              </b-form-group>
              <div class="dropzone col-md-12">
              </div>
            
            
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script lang="js">

import interact from 'interactjs'

export default {
  name: 'playground',
  data(){
    return {
      file: null,
      selected: true,
      options: [
        { value: null, text: 'Please select an option' },
        { value: 'a', text: 'This is First option' },
        { value: 'b', text: 'Selected Option' },
        { value: {'C': '3PO'}, text: 'This is an option with object value' },
        { value: 'd', text: 'This one is disabled', disabled: true }
      ],
      GenderSelect: [
        { value: 'Male', text: 'Male' },
        { value: 'Female', text: 'Female' }
      ],
      Category: [
        { value: 'a', text: 'Category 1' },
        { value: 'b', text: 'Category 2' },
        { value: 'c', text: 'Category 3' },
        { value: 'd', text: 'Category 4' },
        { value: 'e', text: 'Category 5' }
      ],
      countries: [
        { value: 'America', text: 'America' },
        { value: 'Italy', text: 'Italy' },
        { value: 'Russia', text: 'Russia' },
        { value: 'China', text: 'China' },
        { value: 'Britain', text: 'Britain' }
      ],
      text: '',
      x:0,
      y:0
      
    }

  },
  mounted () {
    interact('.form-group').draggable({
      inertia: true,
      modifiers: [
        interact.modifiers.restrictRect({
          restriction: 'parent',
          endOnly: true
        })
      ],
      autoScroll: true,
      // dragMoveListener from the dragging demo above
      listeners: { move: this.dragMoveListener }
      
    })

    // enable draggables to be dropped into this
    interact('.dropzone').dropzone({
      // only accept elements matching this CSS selector
      accept: '.form-group',
      // Require a 75% element overlap for a drop to be possible
      overlap: 'pointer',

      // listen for drop related events:

      ondropactivate: function (event) {
        // add active dropzone feedback
        event.target.classList.add('drop-active')
      },
      ondragenter: function (event) {
        var draggableElement = event.relatedTarget
        var dropzoneElement = event.target

        // feedback the possibility of a drop
        dropzoneElement.classList.add('drop-target')
        draggableElement.classList.add('can-drop')
      },
      ondragleave: function (event) {
        // remove the drop feedback style
        event.target.classList.remove('drop-target')
        event.relatedTarget.classList.remove('can-drop')
      },
      ondrop: function (event) {
        console.log('caiu essa porra')
      },
      ondropdeactivate: function (event) {
        // remove active dropzone feedback
        event.target.classList.remove('drop-active')
        event.target.classList.remove('drop-target')
      }
    })
      
  },
  methods: {
    dragMoveListener: (event) => {
      var target = event.target
      // keep the dragged position in the data-x/data-y attributes
      var x = (parseFloat(target.getAttribute('data-x')) || 0) + event.dx
      var y = (parseFloat(target.getAttribute('data-y')) || 0) + event.dy

      // translate the element
      target.style.webkitTransform =
        target.style.transform =
          'translate(' + x + 'px, ' + y + 'px)'

      // update the posiion attributes
      target.setAttribute('data-x', x)
      target.setAttribute('data-y', y)

      let interaction = event.interaction;
      if (interaction.pointerIsDown && !interaction.interacting()) {
        let original = target;
        let clone = target.cloneNode(true);
        let x = clone.offsetLeft;
        let y = clone.offsetTop;
        clone.style.position = "absolute";
        clone.style.left = original.offsetLeft+"px";
        clone.style.top = original.offsetTop+"px";
        original.parentElement.appendChild(clone);
        interaction.start({ name: 'drag' },event.interactable,clone);
      }
    }
  }
}
</script>

<style scoped lang="scss">
.drags:hover {
  border:2px solid;
  border-color: rgb(230, 233, 233);
}
.drags {
  border:2px solid;
  border-color:white;
  border-radius: 5px;
}

.dropzone {
  background-color: aliceblue;
  width:100px;  
  height: 30px;
}
#outer-dropzone {
  height: 140px;
}

#inner-dropzone {
  height: 80px;
}

.dropzone {
  background-color: #ccc;
  border: dashed 4px transparent;
  border-radius: 4px;
  margin: 10px auto 30px;
  padding: 10px;
  width: 80%;
  transition: background-color 0.3s;
}

.drop-active {
  border-color: #aaa;
}

.drop-target {
  background-color: #29e;
  border-color: #fff;
  border-style: solid;
}

.drag-drop {
  display: inline-block;
  min-width: 40px;
  padding: 2em 0.5em;

  color: #fff;
  background-color: #29e;
  border: solid 2px #fff;

  touch-action: none;
  -webkit-transform: translate(0px, 0px);
          transform: translate(0px, 0px);

  transition: background-color 0.3s;
}

.drag-drop.can-drop {
  color: #000;
  background-color: #4e4;
}


</style>
