<template >
  <div>
    <h2> Add your recent incomes and expenses </h2>
    
    <div class="d-flex justify-content-around mb-3 p-2 border border-secondary" >
      <div> 
        <button type="button" 
          class="btn btn-success" 
          v-if="incomeArray.length > 0"   
          data-bs-toggle="modal" 
          data-bs-target="#exampleModal">

          Check all income
        </button>
      </div>

      <div>
        <span class="input-group-text">How much money do you have?</span>
        <input type="number" 
          aria-label="moneyStart" 
          required 
          class="form-control" 
          v-model="moneyStart"
          placeholder="ex: 1000 euros">            
      </div>

      <div> 
        <button type="button" 
          class="btn btn-danger" 
          v-if="expenseArray.length > 0" 
          data-bs-toggle="modal" 
          data-bs-target="#exampleModalExpenses">

          Check all expenses
        </button>  
      </div>     
    </div>

    <!-- Select with income and expenses -->
    <div class="d-flex justify-content-center border border-primary">
      <div class="card centered" style="width: 22rem;">
        <div class="card-body">
          <h5 class="card-title badge bg-secondary p-2">Where did my Money go</h5>
          
          <div class="card-text mt-2">
            <div class="form-floating">
              <select class="form-select" id="floatingSelect" aria-label="Floating label select example" v-model="category">
                
                <option value="expenses">Expenses</option>
                <option value="income">Income</option>        
              </select>

              <label for="floatingSelect">Choose the Category</label>
            </div>

            <div v-if="category" class="form-floating">
              <select class="form-select" id="floatingSelect" aria-label="Floating label select example" v-model="type">
                <option value="fixed">Fixed</option>
                <option value="variable">Variable</option>
                <option value="others">Others</option>        
              </select>

              <label for="floatingSelect">Choose the Type</label>
            </div>

            <div v-if="category && type" class="mt-4">  
              <div class="input-group p-1">
                <span class="input-group-text">Description</span>
                <input type="text" 
                  aria-label="Description" 
                  required 
                  class="form-control" 
                  v-model="description"
                  :placeholder="'What kind of' + ' ' + category">        
              </div>

              <div class="input-group p-1">
                <span class="input-group-text" style="min-width: 106px;">Amount</span>
                <input type="number" aria-label="Amount" required class="form-control" v-model.number="amount">
                
              </div>

              <div class="input-group p-1">
                <span class="input-group-text" style="min-width: 106px;">Date</span>
                <input type="date" aria-label="Amount" required class="form-control" v-model="date">
                
              </div>

              <div>
                <button type="button" @click="addToAllTransactions" class="btn btn-outline-secondary  p-2 mt-2" style="cursor: pointer; background-color: grey; color: white; font-weigth: bold;">Add {{category}}</button>
              </div>

            </div>
          </div>            
        </div>
      </div>
    </div>
    
    

    <!-- Modal income-->
    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog" >
        
        <div class="modal-content">
          
          <div class="modal-header">
            <div> 
              <p> 
              </p>
            </div>
            <div> 
              <h5 class="modal-title badge bg-success" id="exampleModalLabel" style="font-size: 20px;">Report of all Incomes </h5>
            </div>
            <div> 
              <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>            
          </div>
          <div class="modal-body" v-for="(income,index) in incomeArray" :key="index">
            <div class="border d-flex align-items-center  justify-content-center" style="padding: 1px;" > 

              <div class="col-lg-12">
                  <ul class="list-group  flex-row justify-content-between align-items-center">                
                      <li  class="list-group-item btn btn-danger text-muted" style="font-size: 20px">   {{income.date}} </li>                
                      <li  class="list-group-item badge bg-success" style="font-size: 20px">   {{income.description}} </li>
                      <li  class="list-group-item disabled" style="color: red">   {{income.amount}} Euros </li>                                 
                  </ul>
              </div>
            </div>
            <div>
              <div style="border: 2px solid blue"> 
                
              </div>
            </div>
          </div>
        </div>
      
      </div>
       
    </div>

    <!-- Modal expenses -->
    <div class="modal fade" id="exampleModalExpenses" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog" >
        
        <div class="modal-content">
          
          <div class="modal-header">
            <div> 
              <p> 
              </p>
            </div>
            <div> 
              <h5 class="modal-title badge bg-danger" id="exampleModalLabel" style="font-size: 20px;">Report of all Expenses </h5>
            </div>
            <div> 
              <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>            
          </div>
          <div class="modal-body" v-for="(expense,index) in expenseArray" :key="index">
            <div class="border d-flex align-items-center  justify-content-center align-items-center"  style="padding: 1px;" > 

              <div class="col-lg-12 ">
                  <ul class="list-group  flex-row justify-content-between align-items-center"> 
                      <li  class="list-group-item btn btn-danger text-muted" style="font-size: 20px">   {{expense.date}} </li>                
                      <li  class="list-group-item badge bg-danger" style="font-size: 20px">   {{expense.description}} </li>
                      <li  class="list-group-item disabled" style="color: red">   {{expense.amount}} Euros </li>                     
                  </ul>
              </div>
            </div>
            <div>
              <div style="border: 2px solid blue"> 
                
              </div>
            </div>
          </div>
        </div>
      
      </div>
    </div>

    <!-- modal report -->

    <div class="modal fade" id="exampleModalReport" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Report</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <h1 v-if="sumIncomes > sumExpenses"> Well done! <span style="color:blue;"> your bank account is increasing </span> </h1>
        <h1 v-if="sumIncomes <= sumExpenses"> Tip: <span style="color:red;">Change your job! you are getting poor everyday</span>  </h1>
        
      </div>
      <div class="modal-footer">
        
      </div>
    </div>
  </div>
</div>
    

    <!-- <div>
      <p> % in expenses</p>
      <div class="progress">
        <div class="progress-bar" role="progressbar" style="width: 45%" aria-valuenow="15" aria-valuemin="0" aria-valuemax="100"></div>
        <div class="progress-bar bg-success" role="progressbar" style="width: 30%" aria-valuenow="30" aria-valuemin="0" aria-valuemax="100"></div>
        <div class="progress-bar bg-info" role="progressbar" style="width: 20%" aria-valuenow="20" aria-valuemin="0" aria-valuemax="100"></div>
      </div>

      <p class="mt-3"> % in income</p>
      <div class="progress">
        <div class="progress-bar" role="progressbar" style="width: 45%" aria-valuenow="15" aria-valuemin="0" aria-valuemax="100"></div>
        <div class="progress-bar bg-success" role="progressbar" style="width: 30%" aria-valuenow="30" aria-valuemin="0" aria-valuemax="100"></div>
        <div class="progress-bar bg-info" role="progressbar" style="width: 20%" aria-valuenow="20" aria-valuemin="0" aria-valuemax="100"></div>
      </div>
    </div> -->

    <!-- <div class="form-floating">
      <select class="form-select" id="floatingSelect" aria-label="Floating label select example" v-model="category">
        
        <option value="expenses">Expenses</option>
        <option value="income">Income</option>        
      </select>

      <label for="floatingSelect">Choose the Category</label>
    </div>

    <div v-if="category" class="form-floating">
      <select class="form-select" id="floatingSelect" aria-label="Floating label select example" v-model="type">
        <option value="fixed">Fixed</option>
        <option value="variable">Variable</option>
        <option value="others">Others</option>        
      </select>

      <label for="floatingSelect">Choose the Type</label>
    </div> -->

    <div class="mt-3 d-flex flex-column justify-content-start" style="">
      <div> 
        <h6 class="badge bg-primary"> Saldo Inicial: <span v-if="moneyStart"> {{moneyStart}} Euros</span> </h6>
      </div>

      <div> 
        <h6 class="badge bg-success"> Total Income: <span v-if="sumIncomes"> {{sumIncomes}} Euros</span> </h6>
      </div>

      <div> 
        <h6 class="badge bg-danger"> Total Expenses: <span v-if="sumExpenses"> {{sumExpenses}} Euros</span> </h6>
      </div>
      
      <button type="button" 
        class="btn btn-success"  
        data-bs-toggle="modal" 
        data-bs-target="#exampleModalReport"> 

        Report 
      </button>

    
    </div>

    

    
    
  </div>
</template>

<script>



export default {
  data () {
    return {
      allTransactions: [],
      
      category: "",
      type: "",
      description:  "",
      amount: 0,
      date: "",
        
      
      moneyStart: ""
      
    }
  },


  computed: {
    
    incomeArray: function () {
      return this.allTransactions.filter((income) => income.category == "income")      
    },

    expenseArray: function () {
      return this.allTransactions.filter((expense) => expense.category == "expenses")      
    },

    

    sumExpenses: function () {
      
      let a = this.expenseArray.map(a => a.amount);
      let acumuladorExpense = 0
      for(let i = 0; i< a.length; i++) {
        acumuladorExpense += a[i]
      }
      return acumuladorExpense
    },
    
    sumIncomes: function () {
      

      let a = this.incomeArray.map(a => a.amount);
      let acumuladorIncome = 0
      for(let i = 0; i< a.length; i++) {
        acumuladorIncome += a[i]
      }
      return acumuladorIncome
    },
  },
    
  methods: {
    addToAllTransactions () {

      if (!this.category || !this.type || !this.description || !this.amount || !this.date ) {
        this.$swal(
          'Tem de preencher todos os campos!!'         
        )
        return
      }

      let length = this.allTransactions.length + 1    
      this.allTransactions.push({ id: length, category: this.category, type: this.type, description: this.description, amount: this.amount, date: this.date})
      this.category = "",
      this.type = "",
      this.description = "",
      this.amount = 0,
      this.date = ""

      this.$swal(
          'Adicionado com sucesso',                    
        )
    }
  },

  created() {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>