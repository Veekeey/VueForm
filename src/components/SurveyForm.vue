<template>
<div class="subform">
<h1>TorieM Events Survey Form!</h1>
<p v-if="success" class="success">{{success}}</p>
  <form @submit.prevent="handleSubmit">
    <div class="Fname">
      <label>First Name:</label>
      <input class="F-input" type="text" v-model="formData.firstName" required/>
    </div>
    <div class="Lname">
      <label>Last Name:</label>
      <input class="L-input" type="text" v-model="formData.lastName" required/>
    </div>
    <div class="contact">
      <label>Contact:</label>
      <input class="P-input" type="tel" v-model="formData.phone" required>
      <p v-if="phoneError" class="perror">{{ phoneError }}</p>
    </div>
    <div class="email">
      <label>Email:</label>
      <input class="E-input" type="email" v-model="formData.email" required>
    </div>   
    <div class="gender">
      <label>Gender:</label>
      <input id="male" class="check" type="radio" v-model="formData.gender" value="Male">
      <label for="male">Male</label>
      <input id="female" class="check" type="radio" v-model="formData.gender" value="Female">
      <label for="female">Female</label>         
    </div>
    <div class="rating">
        <label>Rate us:</label>
        <select class="R-input" v-model="formData.rating" required>
          <option value="5">5</option>
          <option value="4">4</option> 
          <option value="3">3</option> 
          <option value="2">2</option> 
          <option value="1">1</option>     
        </select>
    </div>
    <div class="comment">
      <label for="comment">Comments:</label>
      <textarea id="comment" v-model="formData.comment"></textarea>
    </div>
    <div class="button">
      <button>Submit</button>
    </div>
  </form>
</div>
  
<div class="form-review">
  <h2>Review your response</h2>
  <p>{{formData.firstName}} {{formData.lastName}}</p>
  <p>{{formData.phone}}</p>
  <p>{{formData.email}}</p>
  <p>{{formData.gender}}</p>
  <p>{{formData.rating}}</p>
  <p>{{formData.comment}}</p>
</div>

</template>

<script>
export default {
  data(){
    return {
      formData: {
        firstName: '',
        lastName: '',
        email: '',
        phone: '',
        rating: '',
        gender: '',
        comment: ''
      },
      
      phoneError: ' ',
      success: ''
    }
  },

  methods: {
    handleSubmit(){
      // console.log("submited");
      //validations
      if (this.formData.phone.length !== 11){
        this.phoneError = "phone number should be 11 digits"
      }else {
        this.phoneError = '';
        localStorage.setItem(`${this.formData.email}`, JSON.stringify(this.formData))

          this.success = "Response submitted successfully!"
          

        this.formData.firstName = ''
        this.formData.lastName = ''
        this.formData.email = ''
        this.formData.phone = ''
        this.formData.comment = ''
        this.formData.rating = ''
        this.formData.gender = ''

        setTimeout(()=>{
          this.success = ''
          }, 10000)
      }
      


    }
  }
}
</script>
  
  
<style>

body {
  background-color: #eee;
}
 
.F-input, .L-input {
  margin-left: 1rem;
}

.P-input {
  margin-left: 2.2rem;
}

.E-input{
  margin-left: 3rem;
}

.R-input, .check {
  margin-left: 2.5rem;
}

button {
  margin-left: 5.8rem;
  background-color: #fff;
}

.fname, .Lname, .email, .contact, .gender, .rating, .button, #comment {
    margin-top: 1.5rem;
}

button, .E-input, .F-input, .L-input, .P-input, .R-input, #comment {
  width: 30%;
  height: 30px;
  border: 0;
  border-radius: 5px;
}

#comment {
  margin-left: 1rem;
}

.check {
  border: 0;
  border-radius: 5px;
}

.perror {
  margin-left: 6rem;
  font-size: 12px;
  color: red;
}

.success {
  color: green;
  font-style: italic;
  font-size: 20px;
}
</style>