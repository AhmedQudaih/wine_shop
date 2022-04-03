<template>
  <div>
    <v-app-bar
      app
      color="#FFFFFF"
      dark
    >

        <v-icon  color="red" x-large>
           mdi-bottle-wine
        </v-icon>

      <v-toolbar-title class="red--text">Wine Shop</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn @click="handleSearch" icon>
        <v-icon color="red">mdi-magnify</v-icon>
      </v-btn>
      <v-row

             no-gutters
             style="flex: 0.5 ;height: 1.9rem;"
              align-self-end
           >
              <v-text-field
               class="custom-placeholer-color"
              v-model="searchData"
            error
          ></v-text-field>
          </v-row
     >

     <FilterForm @buildQuery="buildQuery" @submitFilter="submitFilter"/>
      </v-app-bar>
  </div>
</template>

<script>
import FilterForm from "./filterForm"
  export default {
    name: 'NavBar',
    data(){
      return{
        searchData:'Search'
      }
    },
    props:{
      buildQuery:Function,
      submitFilter:Function
    },
    methods:{
      handleSearch(){
        if(this.searchData != "Search" && this.searchData.length>0){
          this.buildQuery("beer_name",this.searchData);
          this.submitFilter();
          this.searchData="Search";
        }
      }
    },
    components: {
      FilterForm
    },
  }
</script>

<style >

.custom-placeholer-color input,
.custom-label-color input{
  color: red!important;
}


</style>
