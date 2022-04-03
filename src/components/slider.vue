
<template>
  <v-row>
   <v-subheader>{{title}}:{{slider}}</v-subheader>
         <v-slider
           :v-model="slider"
           class="align-center"
           max="500"
           color="red"
           @change="handleSlider($event)"
           hide-details
         >
      
         </v-slider>
  </v-row>
</template>
<script>
  export default {
    name: 'SliderInput',
    props:{
      title:String,
      slider:Number,
      func:Function
    },
    methods:{
      handleSlider(e){
        this.$emit('func',this.title,e)
      }
    }
  }
</script>
