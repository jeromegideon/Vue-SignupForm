
<script> /* setup, two way data binding to store inputs */
export default {
 data() {
    return {
        email: '',
        password: '',
        role: 'developer',
        terms: false,
        //sex: [],
        tempSkill: '',
        skills: [],
        passwordError: ''
    }
 },
 methods: {
    addSkill(e){
        if (e.key === ',' && this.tempSkill){
            if(!this.skills.includes(this.tempSkill)){
                this.skills.push(this.tempSkill)
            }
             this.tempSkill = ''
        }
    },
    deleteSkill(skill){
      this.skills = this.skills.filter((item) => {
        return skill !== item
      })
    },
    validatePassword(){
       // validate password
       console.log('password:', this.password);
       console.log('email:', this.email);
       console.log('skills:', this.skills);
       console.log('role:', this.role);
       console.log('terms:', this.terms);

       if(this.password.length < 8) {
        this.passwordError = 'password must be at least 8 characters long.';
       }
       else {
        this.passwordError = '';
       }
           
    }
 }
};
</script>

<template>
    <form>
        <label>Email:</label>
        <input type="email" required v-model="email">

        <label for="password">Password:</label>
        <input type="password" id="password" required :model="password" @input="validatePassword" />
        <div class="error" v-if="passwordError">{{ passwordError }}</div>

      <!--creating role options-->  
        <label>Role:</label>
        <select v-model="role">
            <option value="developer">Web Developer</option>
            <option value="draphics designer">Grapghis Designer</option>
            <option value="email marketer">Email Marketer</option>
            <option value="product designer">Product Designer</option>
            <option value="it engineer">IT Engineer</option>
        </select>

        <!--creating a skill input-->
        <label>Skills:</label>
        <input type="text" v-model="tempSkill" @keyup.ctrl="addSkill">
        <div v-for="skill in skills" :key="skill" class="pill">
            <span @click="deleteSkill(skill)">{{ skill }}</span>
        </div>
  
        <div class ="terms">
            <input type="checkbox" v-model="terms" required>
            <label>Accept terms and conditions</label>
        </div>

          <!--creating a skill input-->
        <div class="submit">
            <button>Create Account</button>
        </div>

       <!--  <div>
            <input type="checkbox" value="male" v-model="sex">
            <label>Male</label>
        </div>
        <div>
            <input type="checkbox" value="female" v-model="sex">
            <label>Female</label>
        </div> -->

    </form>

     <!-- to display the inputs.
      <p>Email: {{ email }}</p>
    <p>Password: {{ password }}</p>
    <p>Role: {{ role }}</p>
    <p>Terms Accepted: {{ terms }}</p>
    -->
    

</template>

<style scoped>
form{
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label{
    color: #595959;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
    

}
input, select{
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
    opacity: 60%;
}
input[type="checkbox"]{
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 3px;
}
.pill{
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}
button{
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}
.submit{
    text-align: center;
}
.error{
    color: red;
    margin-top: 10px;
    font-size: 0.7em;
    font-weight: bold;
}
</style>