<template>
  <div id="app">
    <h1 class="pb-5 text-3xl">{{ message }}</h1>
    <input type="file" @change="parseFile" ref="myFileUpload" />
    <table>
      <tr>
        <th v-for="(field, index) in visibleFields" :key="index" class="min-w-min">
          <label :for="'selectableField' + field.column">
            <br />
            {{ field.cellName }}
          </label>
        </th>
        <th>Actions</th>
      </tr>
      <tr v-for="(user, index) in userRows" :key="index">
        <td v-for="(field, index) in visibleFields" :key="index">
          {{ user[field.cellName] }}
        </td>
        <td>
          <button @click="showModal(user)">Details</button>
        </td>
      </tr>
    </table>
    <div v-if="selectedUser">
      <h2>User Details</h2>
      <div v-for="(value, key, index) in selectedUser" :key="index">
        <template v-if="index <= 3"> <!-- Show columns after the third column -->
          <strong>{{ key }}:</strong> {{ value }}
        </template>
        <template v-if="index >= 4">
          <div :id="index" class="aes">
            <h1>Pertanyaan</h1>
            <p :class="'pertanyaan-' + index" style="color: red;">{{ key }}</p>
            <!-- Show columns after the third column -->
            <p>Jawaban</p>
            <textarea :class="'jawaban-' + index">{{ value }}</textarea>
          </div>
        </template>
      </div>
      <button @click="processGpt3">Nilai</button>
    </div>

  </div>
</template>
<script>
import Papa from 'papaparse';
export default {
  data() {
    return {
      //aes
      results: "",
      result: "",
      score: "",
      correction: "",
      confidenceScore: "",

      //csv
      userRows: [],
      message: 'Papa Parse File Mapper',
      file: '',
      results: '',
      fields: [],
      config: {
        delimiter: '',
        newline: '',
        quoteChar: '"',
        escapeChar: '"',
        // preview: 11,
        header: true,
        complete: this.displayCompleteFile,
      },
      visibleFields: [], // To store the first three columns to display initially
      selectedUser: null, // To store the selected user data
    };
  },
  methods: {
    displayCompleteFile(results, file) {
      console.log('Completed File', results, file);
      this.userRows = results.data;
      let fields = results.meta.fields;
      this.fields = fields.map((x, indx) => {
        return {
          column: indx,
          cellName: x,
          assignedValue: '',
        };
      });
      this.visibleFields = this.fields.slice(0, 3); // Display the first three columns initially
    },
    parseFile(event) {
      this.results = Papa.parse(this.$refs.myFileUpload.files[0], this.config);
    },
    showModal(user) {
      this.selectedUser = user;
    },

    async processGpt3() {
      const aesDivs = document.querySelectorAll(".aes");
      for (const div of aesDivs) {
        const pertanyaan = div.querySelector(`.pertanyaan-${div.id}`).textContent;
        const jawaban = div.querySelector(`.jawaban-${div.id}`).textContent;

        try {
          await this.gpt3(pertanyaan, jawaban,); // Wait for gpt3() to finish before proceeding
        } catch (error) {
          console.error(error);
        }
      }
    },

    gpt3(pertanyaan, jawaban) {
      return new Promise((resolve, reject) => {
        fetch("/api/gpt3", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            textGPT:
              "You are a teacher for High School. I would like you to score an ANSWER written in Bahasa Indonesia. Each ANSWER is assigned a rating of 0 to 10, with 10 being the highest and 0 the lowest. The ANSWER is scored based on the following QUESTION and give me confidence score when scoring that ANSWER. Format response {score: (score) correction: (correction in bahasa) confidence score: (confidence score with percentage)} --QUESTION-- " +
              pertanyaan +
              " --QUESTION-- " +
              " \n--ANSWER-- " +
              jawaban +
              " --ANSWER-- ",
          }),
        })
          .then((response) => response.json())
          .then((data) => {
            if (!data.result) {
              reject("Invalid data received from the server.");
              return;
            }

            const result = data.result;
            // Regular expressions to extract the values
            const scoreRegex = /score: (\d+)/;
            const correctionRegex = /correction: ([^ ]+)/;
            const confidenceRegex = /confidence score: (\d+%)/;

            // Function to extract the value using regex
            const extractValue = (regex, input) => {
              const match = input.match(regex);
              return match ? match[1] : null;
            };

            // Extracting values
            const score = extractValue(scoreRegex, result);
            const correction = extractValue(correctionRegex, result);
            const confidenceScore = extractValue(confidenceRegex, result);

            // Logging the values
            console.log("Score:", score);
            console.log("Correction:", correction);
            console.log("Confidence Score:", confidenceScore);

            // You can handle the data here or store it in the component's data or state as needed.

            resolve(); // Resolve the promise once processing is done
          })
          .catch((error) => {
            reject(error);
          });
      });
    },

  },
};
</script>
