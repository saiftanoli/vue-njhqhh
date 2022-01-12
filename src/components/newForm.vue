<template>
  <form @submit.prevent="handelSubmit">
    <label>Email :</label>
    <input type="email" required v-model="email" />

    <label>Password :</label>
    <input type="password" required v-model="password" />
    <div v-if="PasswordError" class="error">{{PasswordError}}</div>

    <label>Role : </label>
    <select v-model="role">
      <option value="developer">web developer</option>
      <option value="designer">web designer</option>
    </select>

    <div>
      <input type="checkbox" value="HTML" v-model="names" />
      <label>HTML</label>
    </div>

    <div>
      <input type="checkbox" value="CSS" v-model="names" />
      <label>CSS</label>
    </div>

    <div>
      <input type="checkbox" value="JavaScript" v-model="names" />
      <label>JavaScript</label>
    </div>

    <label>Hobbies :</label>
    <input type="text" v-model="myHobbies" @keyup="addSkills"  />
    <div v-for="hobby in Hobbies" :key="hobby" class="pill">
      <span @click="deleteSkills(hobby)">{{ hobby }}</span>
    </div>

    <div>
      <input type="checkbox" required v-model="terms" />
      <label>Accept terms and conditions</label>
    </div>
    <button>Create Account</button>
  </form>

  
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      role: '',
      terms: 'false',
      names: [],
      myHobbies: '',
      Hobbies: [],
      PasswordError:''
    };
  },
  methods: {
    addSkills(e) {
      if (e.key === 'Enter' && this.myHobbies) {
        if (!this.Hobbies.includes(this.myHobbies)) {
          this.Hobbies.push(this.myHobbies);
        }
        this.myHobbies = '';
      }
    },
    deleteSkills(hobby){
      this.Hobbies = this.Hobbies.filter((item) => {
        return hobby !== item
      })
    },
    handelSubmit(){
      this.PasswordError = this.PasswordError.length > 5 ? ''
      : "Password must be atleast 6 characters"
      if(this.PasswordError){
      console.log('email:',this.email)
      console.log('password:',this.password)
      console.log('role:',this.role)
      console.log('names:',this.names)
      console.log('Hobbies:',this.Hobbies)
      console.log('terms:',this.terms)
      }
    }
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: center;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  display: block;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type='checkbox'] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.pill {
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
.submit {
    text-align: center;
}
.error{
    color: brown;
    margin-top: 10px;
    font-size: 0.8rem;
    font-weight: bold;
}
</style>