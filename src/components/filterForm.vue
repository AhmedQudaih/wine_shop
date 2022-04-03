<template>
    <v-dialog
      v-model="dialog"
      persistent
      max-width="600px"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn   v-on="on"   v-bind="attrs"  icon>
          <v-icon color="red">mdi-filter</v-icon>
        </v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="text-h5">Filter Form: </span>
        </v-card-title>
        <v-card-text>
          <v-container>
              <SliderInput title="abv" :slider="abv" @func="handleSlider"/>
              <SliderInput title="ibu" :slider="ibu" @func="handleSlider"/>
              <SliderInput title="ebc" :slider="ebc" @func="handleSlider"/>
              <v-text-field
                v-model="date"
                type="date"
                label="brewed before"
                  color="red"
              ></v-text-field>
          </v-container>

        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="blue darken-1"
            text
            @click="dialog = false"
          >
            Close
          </v-btn>
          <v-btn
            color="blue darken-1"
            text
            @click="handleSubmet"
          >
            Filter
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
</template>
<script>
import SliderInput from "./slider"
  export default {
    name: 'FilterForm',
    props:{
      buildQuery:Function,
      submitFilter:Function
    },
    data () {
      return {
          dialog: false,
          abv:0,
          ibu:0,
          ebc:0,
          date:""
      }
    },
    components: {
      SliderInput
    },
    methods:{
      handleSubmet(){
      if(this.abv>0){
        this.$emit('buildQuery',"abv_gt",this.abv-100);
        this.$emit('buildQuery',"abv_lt",this.abv+100);
      }
      if(this.ibu>0){
        this.$emit('buildQuery',"ibu_gt",this.ibu-100);
        this.$emit('buildQuery',"ibu_lt",this.ibu+100);
      }
      if(this.ebc>0){
        this.$emit('buildQuery',"ebc_gt",this.ebc-100);
        this.$emit('buildQuery',"ebc_lt",this.ebc+100);
      }
      if(this.date.length ){
        const split = this.date.split('-');
        this.$emit('buildQuery',"brewed_before",split[1]+"-"+split[0]);
      }
      this.$emit('submitFilter');
        this.dialog = false;
      },
      handleSlider(name, val){
        this[name] = val;
      },
    }
  }
</script>
