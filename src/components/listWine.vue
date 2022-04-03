<template>
  <v-container class="my-5">
    <v-layout row wrap>
      <v-flex xs12 sm6 md4 lg3 v-for="element in data" :key="element.id">
      <v-card
        class=" ma-3 my-12"
        max-width="max-content"
        height="50rem"
      >
        <template slot="progress">
          <v-progress-linear
            color="deep-purple"
            height="10"
            indeterminate
          ></v-progress-linear>
        </template>
        <v-img
          contain
          max-height="250"
          :src="element.image_url"
        ></v-img>

        <v-card-title>{{element.name}}</v-card-title>
        <v-card-text>
          <v-row
            align="center"
            class="mx-0"
          >

            <v-progress-circular
                  :value="element.attenuation_level"
                  color="amber"
                />

            <div class="grey--text ms-4">
               %{{element.attenuation_level}} (attenuation level)
            </div>
          </v-row>

          <div class="my-4 text-subtitle-1">
            $ • {{element.tagline}}

          </div>

          <div class="desc">{{element.description}}</div>


          <div class="grey--text ms-4">
            $ • first brewed: {{element.first_brewed }}

          </div>
        </v-card-text>

        <v-divider class="mx-4"></v-divider>

        <v-card-title>Contains</v-card-title>

        <v-card-text>
          <v-chip-group
            active-class="deep-purple accent-4 white--text"
            column
          >
            <v-chip>abv:{{element.abv}}</v-chip>
            <v-chip>ibu:{{element.ibu}}</v-chip>
            <v-chip>fg:{{element.target_fg}}</v-chip>
            <v-chip>og:{{element.target_og}}</v-chip>
            <v-chip>ebc:{{element.ebc}}</v-chip>
            <v-chip>srm:{{element.srm}}</v-chip>
            <v-chip>ph:{{element.ph}}</v-chip>
          </v-chip-group>
        </v-card-text>
  </v-card>

          </v-flex>
        </v-layout>

      </v-container>
</template>

<script>
  export default {
    name: 'ListWine',
    props:{
      data:[]
    }

  }
</script>
<style>
.desc {
  height: 7rem;
  overflow-y: scroll;
}
.desc::-webkit-scrollbar {
  display: none;
  -ms-overflow-style: none;
  scrollbar-width: none;
}

</style>
