<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" v-model="email" required />
    <label>Password:</label>
    <input type="text" v-model="password" />
    <label>Role:</label>
    <select v-model="role">
      <option value="Designer">Web Designer</option>
      <option value="Developer">Web Developer</option>
    </select>

    <div class="terms">
      <input type="checkbox" required v-model="conditions" />
      <label>Terms and Conditions</label>
    </div>

    <label>Users</label>
    <br />
    <input type="checkbox" v-model="users" value="user1" />
    <label>User1</label>
    <input type="checkbox" v-model="users" value="user2" />
    <label>User2</label>
    <input type="checkbox" v-model="users" value="user3" />
    <label>User3</label>
    <br />
    <label>Skills</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill" />
    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="deleteSkill(skill)">
        {{ skill }}
      </span>
    </div>
    <br />
    <div class="submit">
      <button>Create an Account</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      conditions: false,
      users: [],
      tempSkill: "",
      skills: [],
      passwordError: "",
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill.split(",")[0])) {
          this.skills.push(this.tempSkill.split(",")[0]);
          this.tempSkill = "";
        }
      }
    },
    deleteSkill(skill) {
      //can use filter too
      this.skills.splice(this.skills.indexOf(skill), 1);
    },
    handleSubmit() {
      this.passwordError =
        this.password.length > 5
          ? ""
          : "Password needs to be at least 6 chars long";
      console.log(this.passwordError);
    },
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
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
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
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
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
button {
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
</style>
