<template>

<div class="editor">
    

   <b-container>

       <b-row>

            <b-col  md="12" lg='6'>

             <div ref="download"> 
              <vue-draggable-resizable  class="img" w='1' h='1'>
                <b class="top-text"    :style="[color,size,focusedFont,focusedColor]"> {{topText}} </b>
              </vue-draggable-resizable>
              
                <img :src="imgToEdit" :alt="`Image to edit`" />
              
              <vue-draggable-resizable class="img" w='1' h='1'>
                <b class="bottom-text"  :style="[color,size,focusedFont,focusedColor]"> {{bottomText}} </b>
               </vue-draggable-resizable>
              </div>
              

            </b-col>

            <b-col md="12" lg='6'>

                <input v-model="topText" type="text" placeholder="Top text"> <br> <br>
                <input v-model="bottomText" type="text" placeholder="Bottom text"> <br> <br>
                SIZE: <input type="range" min="8" max="30" v-model="fonts"> <br>
                                




                <select v-model="focused_color">
                      <option value="" disabled selected>Color</option>
                      <option v-for="color in available_colors" :key="color" v-bind:value="color" v-bind:style="{color : color}" >{{ color }}</option>
                </select>

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
        focused_font:'',
        available_fonts: ["Pacifico", "Open Sans", "monospace", "karumbi", "Courier New","Roboto"],
        focused_color:'',
        available_colors: ["red","blue","orange","green",'white','purple']
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


      focusedFont: function() {
      return {
        fontFamily: this.focused_font
      }
    },


    focusedColor: function() {
      return {
        color: this.focused_color
      }
    }

},

methods: {


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
.img {
  border: none !important;
}

</style>