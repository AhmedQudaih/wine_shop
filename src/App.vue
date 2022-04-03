<template>
  <v-app>
    <NavBar :buildQuery="buildQuery" :submitFilter="filteredData" />
      <v-main>
        <MainBanner />
        <ListWine :data="data" />
      </v-main>
  </v-app>
</template>

<script>
import ListWine from './components/listWine';
import NavBar from './components/navBar';
import MainBanner from './components/mainBanner';
export default {
  name: 'App',

    data: () => ({
      data:[],
      query:""
    }),
  mounted:function(){
    fetch("https://api.punkapi.com/v2/beers", {method:"get"})
    .then((res) => {return res.json()})
    .then(data => this.data = data)
  },
  components: {
    ListWine,
    NavBar,
    MainBanner
  },
  methods:{
    buildQuery(name , val){
      this.query = this.query +`&${name}=${val}`;
    },
    filteredData(){
      fetch("https://api.punkapi.com/v2/beers?"+this.query, {method:"get"})
      .then((res) => {return res.json()})
      .then(data => this.data = data)
      this.query =" ";
    },
  }

};
</script>
