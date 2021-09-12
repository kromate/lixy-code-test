<template>
<div class="w-full flex justify-center">
  <div v-if="show" class="shadow">
  <input id="y" v-model="row" type="number" placeholder="row: "
  class="relative outline-none rounded py-1 px-2 w-full bg-white shadow text-sm text-gray-700 placeholder-gray-400 focus:outline-none focus:shadow-outline"
  />
  <input id="x" v-model="column" type="number" placeholder="column: "
  class="relative outline-none rounded py-1 px-2 w-full bg-white shadow text-sm text-gray-700 placeholder-gray-400 focus:outline-none focus:shadow-outline"
  />
  <button class="bg-black text-white"  @click="create(row, column)">multiply</button>

  </div>
   <div id="container" v-html="tableData"></div>

</div>
</template>

<script>
export default {
  name:"Home",
  data(){
    return{
      show:false,
      row:'',
      column:'',
      tableData:''
    }
  },
  created(){
    // on create display a table of 10 prime number, check the readme for an alternate method
this.create(300,300)
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


<style >


#container {
  /* position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%); */
  width: 95vw;
  overflow-x: auto;
}

table.neumorphic{
  width: 50vw;
  border-spacing: 0;
  color: #212121;
  text-align: center;
  margin-top:2rem;
  overflow: hidden;
  box-shadow: 9px 9px 16px rgba(163, 177, 198, 0.6),
  -9px -9px 16px rgba(255, 255, 255, 0.6);
}

table.neumorphic th{
  padding: 7px;
}

table.neumorphic>tbody>tr>td {
  padding: 10px;
  font-size: 14px;
  position: relative;
}


table.neumorphic>tbody>tr:hover {
  padding: 20px;
  box-shadow: 9px 9px 16px rgba(163, 177, 198, 0.6),
  -9px -9px 16px rgba(255, 255, 255, 0.6);
}

table.neumorphic tr td:first-child::before {
  content: "";
  position: absolute;
  padding: 7px;
  top: 0;
  left: -5000px;
  width: 10000px;
  height: 100%;
  z-index: -10;
}

table.neumorphic td:hover::after {
  content: "";
  position: absolute;
  box-shadow: 9px 9px 16px rgba(163, 177, 198, 0.6),
  -9px -9px 16px rgba(255, 255, 255, 0.6);
  left: 0;
  top: -5000px;
  height: 10000px;
  width: 100%;
  z-index: -1;
}
.side{
  background: #bdc4cd8f;
  box-shadow:  9px 9px 16px rgba(163, 177, 198, 0.6);

}
</style>