<template>
  <div>
    <section>
      <h3>Arrays</h3>
      <div class="col-12 space">
        <h3>Items</h3>
        <span class="items" v-for="(search, index) in items" :key="index">
          [{{search}}]
      </span>
      <div class="row">
        <div class="col-12 space">
          <input type="decimal" v-model="newItem" style="max-width:100px">        
        </div>
        <div class="col-4 space">
          <button class="btn-ux" @click="add()"> Add element</button>
          <button class="btn-ux" @click="reset()"> Reset</button>      
          <button class="btn-ux" @click="cleanItems()"> Clean items</button>
        </div>      
      </div>      
      </div>
      <v-row>
        <div class="col-12 space">
        <button class="btn-ux" @click="fill()"> Get combinations</button>
        <button class="btn-ux" @click="findTripplets()"> Get triplets</button>
      </div>
      </v-row>
      
      <div class="col-12 space">
        <h3>Tripplets combinations</h3>       
        <span class="items" v-for="(trip, index) in combinations " :key="index">
          [{{trip.first}}, {{trip.second}}]
        </span>
      </div>
      <div class="col-12 space">
        <h3>Triplets</h3>       
        <span>Exists {{tripplets}} triplets</span>
        <span v-for="(comb, index) in trippletsArray" :key="index">
          [{{comb.first}}, {{comb.second}}]
        </span>
      </div>
    </section>
  </div>
</template>
<style scoped>
 .space {
  margin:2%;
  padding:1%;
 }
 .btn-ux {
  height: 50px;
  width: 160px;
  border-radius: 5px;
  background-color: rgb(25, 68, 27);
  color: white;
  font-size: 16px;
 }
 .btn-ux:hover{
  background-color: rgb(58, 131, 62);
  color: white;
  font-size: 18px;
 }
 .items {
  color: black;
  font-size: 18px;
 }
</style>
<script>
export default {
  data() {
    return {
      newItem: 0,
      items: [1,2,3,5,4,9,10],
      tripplets: 0,
      trippletsArray:[],
      combinations: []
    }
  },
  name: 'QuizComponent',  
  methods: {
    add() {
      let exist = false
      this.items.forEach(item => {
        if(item == this.newItem) {
          exist = true
        }
      })
      if(!exist) {
        this.items.push(parseInt(this.newItem))
      }
      this.newItem = 0
    },
    cleanItems() {
      this.items = []
    },
    reset() {
      this.combinations = []
      this.trippletsArray = []
      this.tripplets = 0 
      this.items = [1,2,3,5,4,9,10]
    },
    fill(){
      this.combinations = []
      console.log(this.items)
			this.items.forEach( first => {
      this.items.forEach( second => {        
      if(first != second) {
        this.combinations.push({"first": first, "second": second })
        }
       })      	
      })      
    },
    findTripplets() {
      this.trippletsArray = []
      this.tripplets = 0
      console.log(this.combinations)
      this.combinations.forEach(item=> {
        let sum = item.first + item.second
        if(this.exist(sum)) {
          console.log('00>', sum,item)
          this.trippletsArray.push(item)
          this.tripplets++
        }
      })
    },
    exist(findNumber) {
      let exist = false
      this.items.forEach(item => {
        if(item == findNumber)
          exist = true
      })
      return exist
    }
  }
 
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
