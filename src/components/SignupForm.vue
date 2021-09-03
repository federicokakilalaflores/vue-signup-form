<template>
  <form @submit.prevent="handleRegister" autocomplete="off">
    <h2>Create Account</h2>
    <small>Please fill up all the fields below.</small> 
     <label>*Name:</label>
    <input type="text" name="name" v-model="name" required>
    <label>*Email:</label>
    <input type="text" name="email" v-model="email" required>
     <label>*Password:</label>
    <input type="password" name="password" v-model="password" required>
    <small class="alert-danger" v-if="passwordErr"> {{ passwordErr }} </small>
    <label>*Job Role:</label> 
    <select name="job_role" v-model="job_role" required>
        <option value="">--Select Role--</option>
        <option value="web designer">Web Designer</option>
        <option value="frontend developer">Frontend Developer</option>
        <option value="backend developer">Backend Developer</option>
        <option value="fullstack developer">Fullstack Developer</option>       
    </select>
    <label>Skills (Press Alt + Enter):</label>
    <input type="text" name="tempSkill" v-model="tempSkill" @keyup.alt="addSkill">
    <span v-for="skill in skills" :key="skill" class="pill" >
         <span @click="removeSkill(skill)">{{ skill }}</span>
    </span>
    <div class="terms">
      <input type="checkbox" name="terms" v-model="terms" required>
      <label>Accept Terms and conditions</label> 
    </div>
    <div class="submit">
      <button type="submit">Create Account</button>
    </div>
  </form>
</template>

<script>
  export default {
    name: 'SignupForm',
    data() {
      return {
        name: '',
        email: '',
        password: '',
        job_role: '',
        terms: '',
        tempSkill: '',
        skills: [],
        passwordErr: ''
      }
    },
    methods: {
      addSkill(e){
        if(e.key === "Enter" && this.tempSkill){
          if(!this.skills.includes(this.tempSkill)){
            this.skills.push(this.tempSkill)
          }
          this.tempSkill = ''
        }
      },
      removeSkill(skill){
        this.skills = this.skills.filter((item) => {
          return item !== skill
        })
      },
      handleRegister(){
        this.passwordErr = this.password.length > 5 ? '' 
            : 'Password must be atleast 6 characters long.'

        if(!this.passwordErr){
          console.log(this.name)
          console.log(this.email)
          console.log(this.password)
          console.log(this.job_role)
          console.log(this.skills) 
        }
      
      }
    }
  }
</script>

<style scoped>
  form{
    text-align: left;
    padding: 40px;
    border-radius: 8px;
    background-color: #fff;
    max-width: 420px;
    margin: 2rem auto;
    box-shadow: 2px 4px 12px rgba(0, 0, 0, 0.19);
  }

  form h2{
    margin: 0;
  }

  form small{
    margin: 5px 0;
    color: #aaa;
    margin-bottom: 2rem;
    display: block;
  }

  label{
    color: #aaa;
    text-transform: uppercase;
    letter-spacing: 1px;
    display: inline-block;
    margin-bottom: 8px;
    font-size: 0.8rem;
    font-weight: 600;
  }

  input, select{
    width: 100%;
    padding: 6px;
    border:0;
    border-bottom: 2px solid #ddd;
    color: #555;
    margin-bottom: 1.5rem;
  }

  input:active{
    border: 0;
  }

  .terms{
    display: flex;
    margin-top: 1rem;
  }

  .terms input[type=checkbox]{
    width: 15px;
    height: 20px;
    margin: 0 6px 0 0;
  }

  .terms label{
    font-size: 0.7rem;
    margin-top: 3px;
  }

  .submit{
    text-align: center;
  }

  button[type=submit]{
    margin-top: 1rem;
    border: 0;
    padding: 12px 18px;
    background-color: teal;
    color: white;
    border-radius: 20px;
  }

  input[name=tempSkill], input[name=password]{
    margin-bottom: 0.7rem;
  }

  .pill{
    background-color: #eee;
    border: 1px solid #ccc;
    padding: 5px 8px;
    border-radius: 12px; 
    margin: 0 3px;
    font-size: 0.9rem;
  }

  .pill:hover{
    cursor: pointer;
  }

  .alert-danger{
    color: red;
  }

</style>