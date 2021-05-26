<template >
  <div>

    <div class="d-flex justify-content-around mb-3 p-2 border border-secondary" >
      <div> 
        <button type="button" class="btn btn-success">Check all income</button>
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
        <button type="button" class="btn btn-danger">Check all expenses</button>  
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
                <input type="number" aria-label="Amount" required class="form-control" v-model="amount">
                
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
    
    <button v-if="allTransactions.length > 0" type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal6">
  Launch demo modal
    </button>

<!-- Modal -->
    <div class="modal fade" id="exampleModal6" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog" v-if="allTransactions.length > 0">
        
        <div class="modal-content">
          
          <div class="modal-header">
            <div> 
              <p> 
              </p>
            </div>
            <div> 
              <!-- <h5 class="modal-title badge bg-danger" id="exampleModalLabel" style="font-size: 20px;">Report of {{allTransactions[0].category}} </h5> -->
            </div>
            <div> 
              <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>            
          </div>
          <div class="modal-body">
             
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
            <button type="button" class="btn btn-primary">Save changes</button>
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
      amount: "",
      date: "",
        
      
      moneyStart: ""
      
    }
  },

  methods: {
    addToAllTransactions () {

      let length = this.allTransactions.length + 1    
      this.allTransactions.push({ id: length, category: this.category, type: this.type, description: this.description, amount: this.amount, date: this.date})
      this.category = "",
      this.type = "",
      this.description = "",
      this.amount = "",
      this.date = ""
    }
  },

  created() {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>