<template>

<div class="editor">
    

   <b-container>

       <b-row>

            <b-col cols="6">

             <div ref="download"> 
              <vue-draggable-resizable w="0" h="0" @dragging="onDrag">
                <b class="top-text"    :style="[color,size,focused]"> {{topText}} </b>
              </vue-draggable-resizable>
              
                <img :src="imgToEdit" :alt="`Image to edit`" />
              
              <vue-draggable-resizable w="0" h="0" @dragging="onDrag">
                <b class="bottom-text"  :style="[color,size,focused]"> {{bottomText}} </b>
               </vue-draggable-resizable>
              </div>
              

            </b-col>

            <b-col cols="6">

                <input v-model="topText" type="text" placeholder="Top text"> <br> <br>
                <input v-model="bottomText" type="text" placeholder="Bottom text"> <br> <br>
                SIZE: <input type="range" min="8" max="30" v-model="fonts"> <br>
                COLOR: <input type="range" min="0" max="999999" v-model="colors"> <br>
                 <br> 


                 <select v-model="focused_font">
                      <option value="" disabled selected>Font</option>
                      <option v-for="font in available_fonts" :key="font" v-bind:value="font" v-bind:style="{fontFamily : font}" >{{ font }}</option>
                </select>
                <br>
                <b-button variant="success" @click="download()" class="mt-5">Download</b-button>
                

            </b-col>

       </b-row>

   </b-container>

    

</div>

</template>
<script>
import { saveAsPng } from 'save-html-as-image'

export default {
  name: 'Editor',
  
  

  props: {
    imgToEdit: {
      type: String
    },


  },
  data() {
    return {
        topText: '',
        bottomText:'',
        fonts: 16,
        colors:'',
        // famlys: ['Elvis', 'Arturs', 'TOms'],
        x: 0,
        y: 0,
        focused_font:'',
        available_fonts: ["Pacifico", "Open Sans", "monospace", "karumbi", "Courier New","Roboto"]
    }
  },

computed: {
    size() {
        return {
            fontSize: this.fonts + 'px',
        }
    },
    color() {
      return {
            color: '#' + this.colors,
      }
    },


      focused: function() {
      return {
        fontFamily: this.focused_font
      }
    }

},

methods: {
    onDrag: function (x, y) {
      this.x = x
      this.y = y
    },

    download: function () {
      const node = this.$refs.download
      saveAsPng(node, { filename: 'generated-mem', printDate: false })
    },



}
 


  

}
</script>
<style scoped>

@import url('https://fonts.googleapis.com/css2?family=Pacifico&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');

  .editor img {
        
        height: 100%;
        width: 100%; 
        
    }


</style>