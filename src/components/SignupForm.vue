<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email" />

    <label>Hasło</label>
    <input type="password" required v-model="password" />
    <div class="error">{{ passwordError }}</div>

    <label>Praca:</label>
    <select v-model="select">
      <option value="barman">Barman</option>
      <option value="striper">Striper</option>
    </select>

    <label>Umiejętności:</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill" />
    <div v-for="skill in skils" :key="skill" class="pill">
      <span @click="deleteskill(skill)"> {{ skill }}</span>
    </div>

    <div class="term">
      <input type="checkbox" required v-model="term" />
      <label>Akcepuje warunki kozystania</label>
    </div>

    <div class="submit">
      <button>załóź konto</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      select: "",
      term: false,
      tempSkill: "",
      skils: [],
      passwordError: ''
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        if (!this.skils.includes(this.tempSkill)) {
          this.skils.push(this.tempSkill);
        }
        this.tempSkill = "";
      }
    },
    deleteskill(skill) {
      this.skils = this.skils.filter((item, index) => item !== skill);
    },
    handleSubmit(){
      this.passwordError = this.password.length > 5 ? '' : "hasło musi zawierać min. 5 znaków"
      if(!this.passwordError){
        console.log(this.email)
        console.log(this.password)
        console.log(this.select)
        console.log(this.skils)
      }
    }
  },
};
</script>

<style scoped>
form {
  text-align: left;
  max-width: 420px;
  margin: 30px auto;
  background: #fff;
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
  width: 100%;
  display: block;
  padding: 10px 6px;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"] {
  position: relative;
  display: inline-block;
  width: 16px;
  top: 2px;
  margin: 0 10px 0 0;
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
  transition: all 0.3s ease-in-out;
}
.pill:hover {
  background: tomato;
  color: #fff;
}
button {
  background: #0b6dff;
  margin-top: 20px;
  border: none;
  padding: 10px 20px;
  color: #fff;
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.3s ease-in-out;
}
button:hover {
  background: #eee;
  color: #0b6dff;
}
.submit {
  text-align: center;
}
.error{
  color: tomato;
  margin-top: 10px;
  font-size: 0.8rem;
  font-weight: bold;
}
</style>