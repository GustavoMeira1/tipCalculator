<template>
  <v-container class="container">
    <v-card class="calculator">
      <v-row class="ma-2">
        <v-col class="col-md-6 col-12">
          <p class="hints">Bill</p>
          <v-text-field outlined dense class="textFields" style="margin-bottom: 20px;" hide-details
          prepend-inner-icon="mdi-currency-usd" color="hsl(172, 67%, 45%)" v-model="bill" @keyup="newValues()"/>
          <p class="hints">Select Tip %</p>
          <v-row>
            <v-col class="col-md-4 col-4">
              <v-btn class="tipBtns" @click="calcTip(.05)">5%</v-btn>
            </v-col>

            <v-col class="col-md-4 col-4">
              <v-btn class="tipBtns" @click="calcTip(.10)">10%</v-btn>
            </v-col>

            <v-col class="col-md-4 col-4">
              <v-btn class="tipBtns" @click="calcTip(.15)">15%</v-btn>
            </v-col>

            <v-col class="col-md-4 col-4">
              <v-btn class="tipBtns" @click="calcTip(.25)">25%</v-btn>
            </v-col>

            <v-col class="col-md-4 col-4">
              <v-btn class="tipBtns" @click="calcTip(.50)">50%</v-btn>
            </v-col>
            
            <v-col class="col-md-4 col-4">
              <v-text-field outlined dense hide-details placeholder="Custom" @keyup="custTip(customTip)"
              v-model="customTip"
              class="textFields customTip" color="hsl(172, 67%, 45%)"/>
            </v-col>

          </v-row>
          <p class="hints" style="margin-top:30px">Number of People</p>
          <v-text-field outlined dense hide-details class="textFields" v-model="nPeople" @keyup="newValues()"
          prepend-inner-icon="mdi-account" color="hsl(172, 67%, 45%)"/>
        </v-col>

        <v-col class="col-md-6 col-12">
          <v-card class="results">
            <v-row>
              <v-col class="col-md-4 resData col-4">
                <p>Tip Amount</p>
                <p class="resPer">/person</p>
              </v-col>
              <v-col class="col-md-8 col-8">
                <p class="value ">${{tipAmount}}</p>
              </v-col>
              <v-col class="col-md-4 col-4 resData">
                <p>Total</p>
                <p class="resPer">/person</p>
              </v-col>
              <v-col class="col-md-8 col-8">
                <p class="value">${{tipTotal}}</p>
              </v-col>
            </v-row>
            <v-btn class="resBtn" color="hsl(172, 67%, 45%)"
            @click="bill=0;nPeople=0;tip=0;tipAmount=0;tipTotal=0" block>RESET</v-btn>
          </v-card>
        </v-col>
      </v-row>
    </v-card>
  </v-container>
</template>

<script>
  export default {
    name: 'Calculator',

    data(){
      return{
        bill:0,
        nPeople:0,
        tip:.1,
        tipAmount:0,
        tipTotal:0,
        customTip:'',
      }
  },
  mounted(){  
    this.fixValues();
    const btns = document.querySelectorAll(".tipBtns");
    for (var i = 0; i < btns.length; i++) {
      btns[i].addEventListener("click", function() {
        var current = document.getElementsByClassName("active");
        if (current.length > 0) {
          current[0].className = current[0].className.replace(" active", "");
        }
        this.className += " active";
      });
    }
  },
    methods:{
      calcTip(tip){
        this.tip = tip
        this.tipAmount = this.bill * tip
        this.tipTotal = this.tipAmount * this.nPeople
        
        this.tipAmount = (Math.round(this.tipAmount * 100) / 100).toFixed(2);
        this.tipTotal = (Math.round(this.tipTotal * 100) / 100).toFixed(2);
      },
      fixValues(){
        this.tipAmount = (Math.round(this.tipAmount * 100) / 100).toFixed(2);
        this.tipTotal = (Math.round(this.tipTotal * 100) / 100).toFixed(2);
      },
      newValues(){
        this.calcTip(this.tip)
      },
      custTip(cusTip){
        var customTip = cusTip/100
        this.calcTip(customTip)
      },
    }
  }
</script>

<style>
@media only screen and (max-width:450px){
.container{
  display: flex;
  align-content: center;
  justify-content: center;
  margin: auto;
}
.calculator{
  background-color: white !important;
  display: flex;
  border-radius: 20px !important;
}
.results{
  background-color: hsl(183, 100%, 15%) !important;
  height: 100%;
  border-radius: 20px !important;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 20px !important;
}
.tipBtns{
  background-color: hsl(183, 100%, 15%) !important;
  color: white !important;
  width: 80px;
}
.tipBtns:hover{
  background-color: hsl(170, 44%, 75%) !important;
  color: hsl(183, 100%, 15%) !important;
}
.active{
  background-color: hsl(170, 76%, 84%) !important;
  color: hsl(183, 100%, 15%) !important;
}
.hints{
  font-size: 12px;
  margin-bottom: 0px !important;
  color: hsl(183, 100%, 15%);
}
.textFields{
  background-color: rgba(83, 83, 83, 0.1);
}
.customTip{
  width: 85px;
}
.resData{
  color: white;
  font-size: 13px;
}
.resPer{
  color:rgba(255,255,255,.6);
  margin-top:-10px;
  text-align: left;
}
.value{
  color: hsl(172, 67%, 45%);
  font-size: 30px;
  }

}
@media only screen and (min-width:450px){
.container{
  display: flex;
  align-content: center;
  justify-content: center;
  margin: auto;
}
.calculator{
  width: 750px;
  height: 340px;
  background-color: white !important;
  display: flex;
  border-radius: 20px !important;
}
.results{
  background-color: hsl(183, 100%, 15%) !important;
  height: 100%;
  width: 550px !important;
  border-radius: 20px !important;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 20px !important;
}
.tipBtns{
  background-color: hsl(183, 100%, 15%) !important;
  color: white !important;
  width: 80px;
}
.tipBtns:hover{
  background-color: hsl(170, 44%, 75%) !important;
  color: hsl(183, 100%, 15%) !important;
}
.active{
  background-color: hsl(170, 76%, 84%) !important;
  color: hsl(183, 100%, 15%) !important;
}
.hints{
  font-size: 12px;
  margin-bottom: 0px !important;
  color: hsl(183, 100%, 15%);
}
.textFields{
  background-color: rgba(83, 83, 83, 0.1);
}
.customTip{
  width: 85px;
}
.resData{
  color: white;
  font-size: 13px;
}
.resPer{
  color:rgba(255,255,255,.6);
  margin-top:-10px;
  text-align: left;
}
.resBtn{
  height: 0px !important;
}
.value{
  color: hsl(172, 67%, 45%);
  font-size: 30px;
  }

}
</style>