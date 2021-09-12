<template>
<div class="w-full flex flex-col justify-center">
  <div class="switch flex items-center justify-center my-4">
    <p v-if="show">show table input field</p>
    <p v-else>Do not show table input field</p>
      <div class="switch-container">
        <input id="show-switch" v-model="show" type="checkbox">
        <label for="show-switch"></label>
      </div>
  </div>
  <div v-if="show" class="shadow flex flex-col justify-center items-center">

  <div class="w-full flex flex-wrap justify-center gap-3">
  <input id="y" v-model="row" required type="number" placeholder="Enter Number of row"
  class="form__input"
  />
  <input id="x" v-model="column" required type="number" placeholder="Enter Number of column"
  class="form__input"
  />
  </div>
  <button class="btn btn__primary my-2"  @click="create(row, column)">Create</button>

  </div>
   <div id="container" v-html="tableData"></div>

</div>
</template>

<script>
export default {
  name:"Home",
  data(){
    return{
      show:true,
      row:'',
      column:'',
      tableData:''
    }
  },
  head () {
    return {
        link: [
        { rel: 'stylesheet', href: './main.css' }
      ]
    }
  },
  created(){
    // on create display a table of 10 prime number, check the readme for an alternate method
this.create(30,30)
  },
  methods:{
    // this function checks a number to see if it is a prime number
    isPrime(num) {
  for(let i = 2; i < num; i++)
    if(num % i === 0) return false;
  return num > 1;
},

// This is the function that generates the prime array used in create
generatePrimeArray(num){
const PrimeArray = []
let counter = 0
while(counter <= num){
  if(this.isPrime(counter)){
    PrimeArray.push(counter)
  }
  counter ++
}
return PrimeArray
},

// This creates the table by accepting a X and Y parameter, which is the start and end value of the table
    create(x, y){

     const row =[1, ...this.generatePrimeArray(x)];
    const  column =[1, ...this.generatePrimeArray(y)];

      let tableBuilder = `<table class="neumorphic">`;


      for(let i=1; i<=row.length-1; i++) {
           if(i===1){
              tableBuilder = tableBuilder + "<tr class='side'>";
         }else{
            tableBuilder = tableBuilder + "<tr>";
         }

       for (let j=1; j<=column.length-1; j++){
         if(j===1 && i ===1){
            tableBuilder = tableBuilder + ("<td  class='side'>" + '*' + "</td>");
         }else if(j===1){
           tableBuilder = tableBuilder + ("<td  class='side'>" + (column[j-1]*row[i-1]) + "</td>");
         }else{
           tableBuilder = tableBuilder + ("<td >" + (column[j-1]*row[i-1]) + "</td>");
         }

       }
       tableBuilder = tableBuilder + "</tr>";
    }
      tableBuilder = tableBuilder + "</table>";

    //  document.getElementById("container").innerHTML = tableBuilder;
     this.tableData = tableBuilder;


}
  }

}
</script>


