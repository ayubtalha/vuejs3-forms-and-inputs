<template>
  <form @submit.prevent="handleSubmit">
    <!-- TWO DATA BINDING (v-model) -->
    <label>Email:</label>
    <input type="email" required v-model="email" />

    <label>Password:</label>
    <input type="password" required v-model="password" />
    <div class="error" v-if="passwordError">{{ passwordError }}</div>

    <!-- SELECT BOXES -->
    <label>Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <!-- CHECK BOXES -->
    <div class="terms">
      <input type="checkbox" required v-model="terms" />
      <label>Accept Terms and Conditions</label>
    </div>

    <!-- INPUT WHILE STORING IN ARRAY -->
    <label>Skills:</label>
    <!-- @keyup keeps track of each key -->
    <!-- @keyup.alt the key you press while holding it won't appear on input while it is there -->
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill" />
    <div v-for="skill in skills" :key="skill" class="pill">
      <!-- DELETING SKILL with @click and passing a function with argument -->
      <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>

    <!-- MULTIPLE CHECK BOXES -->
    <div>
      <input type="checkbox" value="talha" v-model="names" />
      <label>Talha</label>
    </div>
    <div>
      <input type="checkbox" value="ayub" v-model="names" />
      <label>Ayub</label>
    </div>
    <div>
      <input type="checkbox" value="khan" v-model="names" />
      <label>Khan</label>
    </div>

    <div class="submit">
      <button>Create an Account (Submit Button)</button>
    </div>
  </form>

  {{ email }}
  {{ password }}
  {{ role }}
  {{ terms }}
  {{ names }}
  {{ skills }}
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: false,
      names: [],
      tempSkill: "",
      skills: [],
      passwordError: "",
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
        }
        this.tempSkill = "";
      }
      console.log("addSkill", e);
    },
    deleteSkill(skillToDelete) {
      console.log("deleteSkill", skillToDelete);
      this.skills = this.skills.filter((skill) => skill !== skillToDelete);
    },
    handleSubmit() {
      console.log("Form Submitted");
      this.passwordError =
        this.password.length < 5
          ? "The password must be alteast 6 chars long"
          : "";

      if (!this.passwordError) {
        console.log("email", this.email);
        console.log("password", this.password);
        console.log("role", this.role);
        console.log("skills", this.skills);
        console.log("terms", this.terms);
        console.log("names", this.names);
      }
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
.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>
