<template>
  <div class="search" fill-width>
    <div class="searchContainer">
      <div class="srch">
        <v-responsive max-width="260" class="searchBtn">
          <v-text-field
            dense
            flat
            hide-details
            rounded
            solo-inverted
            placeholder="Search..."
            v-model="searchValue"
          ></v-text-field>
        </v-responsive>

        <v-btn @click="getData" class="searchBtn">Search meals</v-btn>
      </div>

      <v-autocomplete
        v-model="dvalue"
        :items="items"
        dense
        filled
        label="Category"
      ></v-autocomplete>
      <v-btn @click="getDataByCategory" class="searchBtn">Search by category</v-btn>
    </div>

    <h1 class="nemaRezultata" v-if="nemaRezultata">
      No results :( Try again !
    </h1>

    <v-row no-gutters dense>
      <v-col
        class="ma-4"
        cols="4"
        v-for="meal in meals"
        :key="meal.id"
        lg="2"
        md="3"
        sm="4"
      >
        <v-card>
          <v-img
            :src="meal.strMealThumb"
            height="125"
            class="grey darken-4"
          ></v-img>
          <v-card-title class="text-h6">
            Name : {{ meal.strMeal }}
            <div class="text-center">
    <v-dialog
      v-model="dialog"
      width="500"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          color="gray lighten-2"
          dark
          v-bind="attrs"
          v-on="on"
        >
          Instructions
        </v-btn>
      </template>

      <v-card>
        <v-card-title class="text-h5 grey lighten-2">
          Name : {{ meal.strMeal }}
        </v-card-title>

        <v-card-text>
          Instructions : {{meal.strInstructions}}
        </v-card-text>

        <v-divider></v-divider>

        
      </v-card>
    </v-dialog>
  </div>
          </v-card-title>
        </v-card>
      </v-col>
    </v-row>
  
 

  </div>
</template>

<script>
export default {
  data() {
    return {
      dialog: false,
      meals: null,
      searchValue: "",
      nemaRezultata: false,
      items: ["Beef", "Chicken", "Dessert", "Lamb", "Seafood", "Pasta", "Vegetarian", "Vegan"],
      dvalue: null,
      
      page: 1,
      //total:0,
      //perPage:10
    };
  },
  methods: {
    getData() {
      //params:{
     //       'offset';Math.round(this.perPage*(this.page-1))
       //   }
      this.axios
        .get(
          `https://www.themealdb.com/api/json/v1/1/search.php?s=${this.searchValue}`
        ) 
        .then((response) => {
          if (this.searchValue === "") {
            this.nemaRezultata = true;
          } else {
            this.nemaRezultata = false;
            console.log(response);
            this.meals = response.data.meals;
          }
        });
    },
    getDataByCategory() {
      this.axios
        .get(
          `https://www.themealdb.com/api/json/v1/1/filter.php?c=${this.dvalue}`
        )
        .then((response) => {
          this.meals = response.data.meals;
        });
    }
  },
};
</script>

<style scoped>
.search {
  width: 100vw;
  height: 100%;
  margin: 0 auto;  
  background-color: rgb(148, 155, 145);
}

.searchContainer {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  width: 30%;
  margin: 0 auto;
}

.srch {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  flex-direction: column;
  margin: 1rem 0;
}

.searchBtn {
  margin: 1rem 0;
  border: 1px solid white;
  border-radius: 50px;
}

.nemaRezultata {
  text-align: center;
  color: rgb(255, 255, 255);
}
</style>

