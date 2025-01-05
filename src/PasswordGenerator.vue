<template>
  <div class="password-generator">
    <h1>Password Generator</h1>
    <button @click="generatePassword">CLICK GENERATE</button>
    <div class="slider-container">
      <label>LENGTH: {{ passwordLength }}</label>
      <input
        type="range"
        min="4"
        max="32"
        v-model="passwordLength"
        @input="updateLength"
      />
    </div>
    <div class="settings">
      <div v-for="(setting, index) in settings" :key="index" class="setting">
        <label>{{ setting.label }}</label>
        <input
          type="checkbox"
          v-model="setting.value"
        />
      </div>
    </div>
    <button @click="generatePassword">GENERATE PASSWORD</button>
    <div v-if="generatedPassword" class="output">
      <p>Your Password: <strong>{{ generatedPassword }}</strong></p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      passwordLength: 16,
      generatedPassword: "",
      settings: [
        { label: "Include Uppercase", value: true, chars: "ABCDEFGHIJKLMNOPQRSTUVWXYZ" },
        { label: "Include Lowercase", value: true, chars: "abcdefghijklmnopqrstuvwxyz" },
        { label: "Include Numbers", value: true, chars: "0123456789" },
        { label: "Include Symbols", value: false, chars: "!@#$%^&*()_+-=[]{}|;:'\",.<>?/`~" },
      ],
    };
  },
  methods: {
    updateLength() {
      this.generatedPassword = "";
    },
    generatePassword() {
      let charPool = "";
      this.settings.forEach((setting) => {
        if (setting.value) {
          charPool += setting.chars;
        }
      });

      if (charPool.length === 0) {
        alert("Please select at least one option.");
        return;
      }

      let password = "";
      for (let i = 0; i < this.passwordLength; i++) {
        const randomIndex = Math.floor(Math.random() * charPool.length);
        password += charPool[randomIndex];
      }

      this.generatedPassword = password;
    },
  },
};
</script>

<style scoped>
.password-generator {
  max-width: 400px;
  margin: 20px auto;
  background: #1e1e2f;
  padding: 20px;
  border-radius: 10px;
  text-align: center;
  color: white;
}

h1 {
  font-size: 1.5rem;
  margin-bottom: 20px;
}

button {
  background: #6a5acd;
  color: white;
  border: none;
  padding: 10px 15px;
  margin: 10px 0;
  cursor: pointer;
  border-radius: 5px;
  font-size: 1rem;
}

button:hover {
  background: #836fff;
}

.slider-container {
  margin: 15px 0;
}

label {
  display: block;
  font-size: 1rem;
  margin-bottom: 5px;
}

input[type="range"] {
  width: 100%;
}

.settings {
  text-align: left;
  margin: 20px 0;
}

.setting {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}

.output {
  margin-top: 20px;
  font-size: 1.2rem;
  background: #27293d;
  padding: 10px;
  border-radius: 5px;
}
</style>