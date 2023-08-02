<script>
import Calculations from './Calculations.vue'
export default {
  name: 'App',
  data() {
    return {
      day: '',
      month: '',
      year: '',
      errorCount: 0,
    }
  },
  components: {
    "age-result": Calculations,
  },
  methods: {
    checkDate() {
      var errorTxt = document.querySelectorAll(".error");
      var inputs = document.querySelectorAll("input");
      var dateTitle = document.querySelectorAll(".date");
      var date = new Date();
      if(this.day &&
         this.month &&
         this.year &&
         this.year < date.getFullYear() &&
         this.month <= 12 &&
         this.day <= (new Date(this.year, this.month, 0)).getDate()
        ) {
        this.$refs.ageCal.calculateAge(this.day,this.month,this.year)
      }

      

      if(!this.day) {
        errorTxt[0].innerText = "This field is required";
        dateTitle[0].style.setProperty('--smokey-grey', 'hsl(0, 100%, 67%)');
        inputs[0].style.setProperty('--light-grey', 'hsl(0, 100%, 67%)');
        this.errorCount++;
      } else {
        errorTxt[0].innerText = "";
        dateTitle[0].style.setProperty('--smokey-grey', 'hsl(0, 1%, 44%)');
        inputs[0].style.setProperty('--light-grey', 'hsl(0, 0%, 86%)');
      }
      if(!this.month) {
        errorTxt[1].innerText = "This field is required";
        dateTitle[1].style.setProperty('--smokey-grey', 'hsl(0, 100%, 67%)');
        inputs[1].style.setProperty('--light-grey', 'hsl(0, 100%, 67%)');
        this.errorCount++;
      } else {
        errorTxt[1].innerText = ""
        dateTitle[1].style.setProperty('--smokey-grey', 'hsl(0, 1%, 44%)');
        inputs[1].style.setProperty('--light-grey', 'hsl(0, 0%, 86%)');
      }
      if(!this.year) {
        errorTxt[2].innerText = "This field is required";
        dateTitle[2].style.setProperty('--smokey-grey', 'hsl(0, 100%, 67%)');
        inputs[2].style.setProperty('--light-grey', 'hsl(0, 100%, 67%)');
        this.errorCount++;
      } else {
        errorTxt[2].innerText = ""
        dateTitle[2].style.setProperty('--smokey-grey', 'hsl(0, 1%, 44%)');
        inputs[2].style.setProperty('--light-grey', 'hsl(0, 0%, 86%)');
      }
      //------------------------------------------
      if(this.year >= date.getFullYear()) {
        errorTxt[2].innerText = "Must be in the past";
        dateTitle[2].style.setProperty('--smokey-grey', 'hsl(0, 100%, 67%)');
        inputs[2].style.setProperty('--light-grey', 'hsl(0, 100%, 67%)');
        this.errorCount++;
      } 
      if(this.month > 12) {
        errorTxt[1].innerText = "Must be a valid month";
        dateTitle[1].style.setProperty('--smokey-grey', 'hsl(0, 100%, 67%)');
        inputs[1].style.setProperty('--light-grey', 'hsl(0, 100%, 67%)');
        this.errorCount++;
      } 
      if(this.day > (new Date(this.year, this.month, 0)).getDate()) {
        errorTxt[0].innerText = "Must be a valid day";
        dateTitle[0].style.setProperty('--smokey-grey', 'hsl(0, 100%, 67%)');
        inputs[0].style.setProperty('--light-grey', 'hsl(0, 100%, 67%)');
        this.errorCount++;
      } 

      if(this.errorCount >= 3) {
        errorTxt[0].innerText = "Must be a valid date";
        errorTxt[1].innerText = "";
        errorTxt[2].innerText = "";     
      }
      this.errorCount = 0;
    }
  }
}
</script>

<template v-cloak>
  <main class="container">
    <div class="mobile-container">
      <div class="date-container">
        <p class="date">DAY</p>
        <input v-model="day" placeholder="DD" type="number">
        <p class="error"></p>
      </div>
      <div class="date-container">
        <p class="date">MONTH</p>
        <input v-model="month" placeholder="MM" type="number">
        <p class="error"></p>
      </div>
      <div class="date-container">
        <p class="date">YEAR</p>
        <input v-model="year" placeholder="YYYY" type="number">
        <p class="error"></p>
      </div>
    </div>
    
    <div class="divider">
      <div class="line"></div>
      <button @click="checkDate()" class="enter"></button>
    </div>
    
    <age-result ref="ageCal"/>
  </main>

</template>

<style scoped>
@import '../style.css';
[v-cloak] {
  display: none;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

.container {
  width: 45vw;
  height: 80vh;
  padding: 50px 50px 0px;
  border-radius: 20px 20px 200px 20px;
  background-color: var(--white);
  
}

.date-container {
  display: inline-block;
  margin-right: 20px;
  margin-top: 10px;
}

.date {
  color: var(--smokey-grey);
  font-size: 20px;
}

input {
  font-size: 32px;
  width: 120px;
  height: 70px;
  border-radius: 10px;
  border: 1px solid var(--light-grey);
  padding: 0 20px 0;
  margin-top: 5px;
}

input:focus{
  outline: 1px solid var(--purple);
}

.error {
  font-weight: 400;
  color: var(--light-red);
  font-size: 15px;
  position: absolute;
  margin-top: 10px;
  font-style: italic;
}

.divider {
  height: 80px;
  display: flex;
  flex-direction: row;
  align-items: center;
}
.line {
  height: 1px;
  width: 85%;
  background-color: var(--light-grey);
}

.enter {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  outline: none;
  border: none;
  background: url('../assets/images/icon-arrow.svg') center no-repeat;
  background-color: var(--purple);
}

.enter:hover {
  background-color: var(--off-black);
}

@media only screen and (max-width: 500px) {
  .container {
    width: 80vw;
    height: 55vh;
    padding: 15px;
    padding-top: 30px;
    border-radius: 20px 20px 100px 20px;
  }

  .mobile-container {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }
  .date-container {
    margin-right: 0px;
  }

  .date {
    color: var(--smokey-grey);
    font-size: 14px;
  }

  input {
    font-size: 22px;
    width: 65px;
    height: 40px;
    padding: 0 10px 0;
  }

  .divider {
    height: 50px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    margin-top: 30px;
  }
  .line {
    width: 100%;
  }

  .enter {
    position: absolute;
    width: 55px;
    height: 55px;
    background-size: 25px;
  }
  .error {
    font-size: 8px;
    margin-top: 10px;
  }
}
</style>
