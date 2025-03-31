<template>
  <div>
    <h1>Vue.js Asynchronous Examples</h1>
    <button @click="fetchDataWithCallback">Fetch with Callback</button>
    <button @click="fetchDataWithPromise">Fetch with Promise</button>
    <button @click="fetchDataWithAsyncAwait">Fetch with Async/Await</button>
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: "Click a button to fetch data!"
    };
  },
  methods: {
    // Using Callback
    fetchDataWithCallback() {
      this.fetchDataCallback((error, data) => {
        if (error) {
          this.message = "Error fetching data!";
        } else {
          this.message = `Callback: ${data}`;
        }
      });
    },
    
    fetchDataCallback(callback) {
      setTimeout(() => {
        const success = Math.random() > 0.3; // Simulate success rate
        if (success) {
          callback(null, "Data received via Callback");
        } else {
          callback("Error", null);
        }
      }, 1000);
    },
    
    // Using Promise
    fetchDataWithPromise() {
      this.fetchDataPromise()
        .then(data => {
          this.message = `Promise: ${data}`;
        })
        .catch(() => {
          this.message = "Error fetching data!";
        });
    },
    
    fetchDataPromise() {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          const success = Math.random() > 0.3;
          if (success) {
            resolve("Data received via Promise");
          } else {
            reject("Error");
          }
        }, 1000);
      });
    },
    
    // Using Async/Await
    async fetchDataWithAsyncAwait() {
      try {
        this.message = `Async/Await: ${await this.fetchDataPromise()}`;
      } catch (error) {
        this.message = "Error fetching data!";
      }
    }
  }
};
</script>
