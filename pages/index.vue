<template>
    <div>
        <h1>AES</h1>
        <br>
        <textarea v-model="text" placeholder="give me a essay text" name="" id="" cols="30" rows="10"></textarea>
        <br>
        <button @click="gpt3()" >Generate</button>
        <br>
        <h2>Results</h2>
        <br>
        <h5>{{ results }}</h5>
    </div>
</template>

<script>
export default {
  data() {
    return {
      text: "",
      results: "",
    };
  },
  methods: {
    gpt3() {
      fetch("/api/gpt3", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          textGPT: this.text,
        }),
      })
        .then((response) => response.json())
        .then((textBACK) => {
          this.results = textBACK.result;
        });
    },
  },
};
</script>