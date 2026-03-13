<template>
  <div id="app">
    <div class="card">
      <h1>🚀 CI/CD DevOps Project</h1>
      <h2>Vue + Docker + Kubernetes</h2>

      <p>
        Hello <strong>Parthiv</strong> 👋<br>
        This application is running inside a Docker container.
      </p>

      <button @click="changeMessage">Click Me</button>

      <p class="message">{{ message }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      message: ""
    };
  },
  methods: {
    changeMessage() {
      this.message = "🎉 Congratulations! Your DevOps pipeline will work perfectly.";
    }
  }
};
</script>

<style>
#app {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: linear-gradient(135deg, #42b883, #35495e);
  font-family: Arial, sans-serif;
}

.card {
  background: white;
  padding: 40px;
  border-radius: 12px;
  text-align: center;
  width: 400px;
  box-shadow: 0px 10px 25px rgba(0,0,0,0.2);
}

h1 {
  color: #42b883;
}

h2 {
  color: #35495e;
}

button {
  margin-top: 20px;
  padding: 10px 20px;
  border: none;
  background: #42b883;
  color: white;
  font-size: 16px;
  border-radius: 6px;
  cursor: pointer;
}

button:hover {
  background: #2e8b6c;
}

.message {
  margin-top: 20px;
  font-weight: bold;
  color: #35495e;
}
</style>