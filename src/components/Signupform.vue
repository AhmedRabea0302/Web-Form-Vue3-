<template>
  <form @submit.prevent="handleSubmit">
      <label>Email</label>
      <input type="email" required v-model="email">

      <label>Password</label>
      <input type="password" required v-model="password">
      <div class="error" v-if="passwordError">{{ passwordError }}</div>

      <label>Role:</label>
      <select v-model="role">
          <option value="developer">Web Developer</option>
          <option value="designer">Web Designer</option>
      </select>

      <label>Skills:</label>
      <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
      <div class="pill" v-for="skill in skills" :key="skill" @click="deleteSkill(skill)">{{skill}}</div>

      <div class="terms">
          <input type="checkbox" v-model="terms">
          <label>Accept Terms and condtions</label>
      </div>

      <div class="submit">
          <button type="" >Create Account</button>
      </div>

     
  </form>

  <p>The Email: {{email}} - Password: {{password}} - Role: {{role}}</p>
  <p>{{names}}</p>
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: 'developer',
            terms: false,
            tempSkill: '',
            skills: [],
            passwordError: '',
        }
    },

    methods: {
        addSkill(event) {
            if(event.key === ',' && this.tempSkill) {
                if(!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill);
                }
                this.tempSkill = '';
                console.log(this.skills)
            }
        },

        deleteSkill(skill) {
            this.skills = this.skills.filter(s => {
                return s != skill;
            })
        },

        handleSubmit() {
            // Validate Password
            this.passwordError = this.password.length < 6 ? 'Password Must be al least 6 chars long' : '';
            

            if(!this.passwordError) {
                console.log('Email', this.email);
                console.log('Password', this.password);
                console.log('Role', this.role);
                console.log('Terms', this.terms);
                console.log('Skills', this.skills);
            }
        }
    }

}
</script>

<style>

form {
    max-width: 420px;
    margin: 30px auto;
    background-color:white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}

label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}


input, select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555555;
}

input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}

.pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    color: #777;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: border;
    cursor: pointer;
}

button {
    background: #0b6dff;
    border: 0;
    padding:10px 20px;
    margin-top: 20px;
    border-radius: 20px;
    color: white;
}

.submit {
    text-align: center;
}

.error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}

</style>