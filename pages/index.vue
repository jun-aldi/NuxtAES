<template>
  <Tab />
  <div>
    <div
      v-if="loading"
      role="status"
      class="absolute -translate-x-1/2 -translate-y-1/2 top-2/4 left-1/2"
    >
      <button
        disabled
        type="button"
        class="py-2.5 px-5 mr-2 text-sm font-medium text-gray-900 bg-white rounded-lg border border-gray-200 hover:bg-gray-100 hover:text-blue-700 focus:z-10 focus:ring-2 focus:ring-blue-700 focus:text-blue-700 dark:bg-gray-800 dark:text-gray-400 dark:border-gray-600 dark:hover:text-white dark:hover:bg-gray-700 inline-flex items-center"
      >
        <svg
          aria-hidden="true"
          role="status"
          class="inline w-4 h-4 mr-3 text-gray-200 animate-spin dark:text-gray-600"
          viewBox="0 0 100 101"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z"
            fill="currentColor"
          />
          <path
            d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z"
            fill="#1C64F2"
          />
        </svg>
        Generate Scoring..
      </button>
    </div>
    <section class="bg-white dark:bg-gray-900">
      <div class="max-w-screen-xl mx-auto">
        <div
          class="p-8 mb-8 border border-gray-200 rounded-lg bg-gray-50 dark:bg-gray-800 dark:border-gray-700 md:p-12"
        >
          <a
            href="#"
            class="bg-blue-100 text-blue-800 text-xl font-medium inline-flex items-center px-2.5 py-0.5 rounded-md dark:bg-gray-700 dark:text-blue-400 mb-4"
          >
            <svg
              class="w-3 h-3 mr-1"
              fill="currentColor"
              viewBox="0 0 20 20"
              xmlns="http://www.w3.org/2000/svg"
              aria-hidden="true"
            >
              <path
                d="M2 6a2 2 0 012-2h6a2 2 0 012 2v8a2 2 0 01-2 2H4a2 2 0 01-2-2V6zM14.553 7.106A1 1 0 0014 8v4a1 1 0 00.553.894l2 1A1 1 0 0018 13V7a1 1 0 00-1.447-.894l-2 1z"
              ></path>
            </svg>
            Pertanyaan
          </a>
          <textarea
            id="message"
            v-model="questions"
            rows="4"
            class="block p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            placeholder="Tulis pertanyaan disini"
          ></textarea>
        </div>
        <div class="grid gap-8 md:grid-cols-2">
          <div
            class="p-8 border border-gray-200 rounded-lg bg-gray-50 dark:bg-gray-800 dark:border-gray-700 md:p-12"
          >
            <a
              href="#"
              class="bg-green-100 text-green-800 text-xl font-medium inline-flex items-center px-2.5 py-0.5 rounded-md dark:bg-gray-700 dark:text-green-400 mb-4"
            >
              <svg
                class="w-3 h-3 mr-1"
                fill="currentColor"
                viewBox="0 0 20 20"
                xmlns="http://www.w3.org/2000/svg"
                aria-hidden="true"
              >
                <path
                  clip-rule="evenodd"
                  fill-rule="evenodd"
                  d="M4 2a2 2 0 00-2 2v11a3 3 0 106 0V4a2 2 0 00-2-2H4zm1 14a1 1 0 100-2 1 1 0 000 2zm5-1.757l4.9-4.9a2 2 0 000-2.828L13.485 5.1a2 2 0 00-2.828 0L10 5.757v8.486zM16 18H9.071l6-6H16a2 2 0 012 2v2a2 2 0 01-2 2z"
                ></path>
              </svg>
              Jawaban
            </a>
            <textarea
              id="message"
              v-model="essays"
              rows="10"
              class="block p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
              placeholder="Tulis essays disini"
            ></textarea>
            <button
              @click="gpt3()"
              type="button"
              class="mt-4 text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800"
            >
              Nilai
            </button>
          </div>
          <div
            class="p-8 border border-gray-200 rounded-lg bg-gray-50 dark:bg-gray-800 dark:border-gray-700 md:p-12"
          >
            <a
              href="#"
              class="bg-purple-100 text-purple-800 text-xl font-medium inline-flex items-center px-2.5 py-0.5 rounded-md dark:bg-gray-700 dark:text-purple-400 mb-4"
            >
              <svg
                class="w-3 h-3 mr-1"
                fill="currentColor"
                viewBox="0 0 20 20"
                xmlns="http://www.w3.org/2000/svg"
                aria-hidden="true"
              >
                <path
                  clip-rule="evenodd"
                  fill-rule="evenodd"
                  d="M12.316 3.051a1 1 0 01.633 1.265l-4 12a1 1 0 11-1.898-.632l4-12a1 1 0 011.265-.633zM5.707 6.293a1 1 0 010 1.414L3.414 10l2.293 2.293a1 1 0 11-1.414 1.414l-3-3a1 1 0 010-1.414l3-3a1 1 0 011.414 0zm8.586 0a1 1 0 011.414 0l3 3a1 1 0 010 1.414l-3 3a1 1 0 11-1.414-1.414L16.586 10l-2.293-2.293a1 1 0 010-1.414z"
                ></path>
              </svg>
              Nilai
            </a>
            <div v-if="loading">
              <svg
                aria-hidden="true"
                class="w-8 h-8 mr-2 text-gray-200 animate-spin dark:text-gray-600 fill-blue-600"
                viewBox="0 0 100 101"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z"
                  fill="currentColor"
                />
                <path
                  d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z"
                  fill="currentFill"
                />
              </svg>
              <span class="sr-only">Loading...</span>
            </div>
            <div v-else>
              <h2
                class="mb-2 text-3xl font-extrabold text-gray-900 dark:text-white"
              >
                Nilai : {{ score }}/100
              </h2>
              <p
                class="mb-4 text-lg font-normal text-gray-500 dark:text-gray-400"
              >
                {{ correction }}
              </p>
              <p class="text-sm text-gray-400">
                Tingkat akurasi : {{ confidenceScore }}
              </p>
            </div>
          </div>
        </div>
        <div
          class="p-4 mt-4 mb-8 border border-gray-200 rounded-lg bg-gray-50 dark:bg-gray-800 dark:border-gray-700 md:p-12"
        >
          <a
            href="#"
            class="bg-blue-100 text-blue-800 text-xl font-medium inline-flex items-center px-2.5 py-0.5 rounded-md dark:bg-gray-700 dark:text-blue-400 mb-4"
          >
            <svg
              class="w-3 h-3 mr-1"
              fill="currentColor"
              viewBox="0 0 20 20"
              xmlns="http://www.w3.org/2000/svg"
              aria-hidden="true"
            >
              <path
                d="M2 6a2 2 0 012-2h6a2 2 0 012 2v8a2 2 0 01-2 2H4a2 2 0 01-2-2V6zM14.553 7.106A1 1 0 0014 8v4a1 1 0 00.553.894l2 1A1 1 0 0018 13V7a1 1 0 00-1.447-.894l-2 1z"
              ></path>
            </svg>
            Raw Response
          </a>
          <div v-if="loading">
            <svg
              aria-hidden="true"
              class="w-8 h-8 mr-2 text-gray-200 animate-spin dark:text-gray-600 fill-blue-600"
              viewBox="0 0 100 101"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z"
                fill="currentColor"
              />
              <path
                d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z"
                fill="currentFill"
              />
            </svg>
            <span class="sr-only">Loading...</span>
          </div>
          <div v-else>
            <p
              class="mb-4 text-sm font-normal text-gray-500 dark:text-gray-400"
            >
              {{ result }}
            </p>
            <p v-if="error" class="mb-4 text-sm font-normal text-red-500">
              {{ error_message }}
            </p>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
<script>
import { initFlowbite } from "flowbite";
definePageMeta({
  layout: "nav",
  title: "My App",
  meta: [{ name: "description", content: "My amazing site." }],
  bodyAttrs: {
    class: "test",
  },
  script: [{ innerHTML: "console.log('Hello world')" }],
});
export default {
  data() {
    return {
      textAreaEssay: null,
      textAreaQuestion: null,
      error_message: "",
      error: false,
      loading: false,
      questions: "",
      // text: "",
      essays: "",
      results: "",
      result: "",
      score: "",
      correction: "",
      confidenceScore: "",
    };
  },
  methods: {
    gpt3() {
      if (this.essays === "" && this.questions === "") {
        // Code to execute if both conditions are true
        this.error_message = "Harap isi jawaban dan pertanyaan !!";
        this.result = "";
        this.score = "";
        this.correction = "";
        this.confidenceScore = "";
        this.error = true;
      } else if (this.questions === "") {
        // Code to execute if both conditions are true
        this.error_message = "Harap isi pertanyaan !";
        this.result = "";
        this.score = "";
        this.correction = "";
        this.confidenceScore = "";
        this.error = true;
      } else if (this.essays === "") {
        // Code to execute if both conditions are true
        this.error_message = "Harap isi jawaban !";
        this.result = "";
        this.score = "";
        this.correction = "";
        this.confidenceScore = "";
        this.error = true;
      } else {
        this.loading = true; // Set loading to true
        this.error = false; // Set loading to true
        fetch("/api/gpt3", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },

          // body: JSON.stringify({
          //   textGPT: "pertanyaan :" + this.questions + "jawaban :" + this.answers,
          // }),
          body: JSON.stringify({
            textGPT:
              "You is teacher for High School. i would like you to score an ANSWER written by Bahasa Indonesia. Each ANSWER is assigned a rating of 0 to 100, with 100 being the highest and 0 the lowest. The ANSWER is scored based on the following QUESTION. and give me confidence score when scoring that ANSWER. Format response {score: (score) correction: (correction in bahasa) confidence score: (confidence score with percentage)} --QEUSTION-- " +
              this.questions +
              " --QEUSTION-- " +
              " \n--ANSWER-- " +
              this.essays +
              " --ANSWER-- ",
          }),
        })
          .then((response) => {
            if (!response.ok) {
              throw new Error(response.status);
            }
            return response.json();
          })
          .then((data) => {
            this.result = data.result;
            if (this.result !== "") {
            // Regular expressions to extract the values

            const scoreRegex = /score:\s+(\d+)/;
            const correctionRegex = /correction:\s+(.*)\s+confidence score:/;
            const confidenceRegex = /confidence score:\s+(\d+%)/;

            // Function to extract the value using regex
            const extractValue = (regex, input) => {
              const match = input.match(regex);
              return match ? match[1] : null;
            };

            // Extracting values
            this.score = extractValue(scoreRegex, this.result);
            this.correction = extractValue(correctionRegex, this.result);
            this.confidenceScore = extractValue(confidenceRegex, this.result);
              console.log(this.score);
              console.log(this.correction);
              console.log(this.confidenceScore);
            }
            this.loading = false;
          })
          .catch((error) => {
            this.error_message = "Error: " + error.message;
            console.error(error);
            this.loading = false; // Set loading back to false
            this.error = true; // Set loading back to false
          });
      }
    },
  },
};
onMounted(() => {
  initFlowbite();
});
</script>
