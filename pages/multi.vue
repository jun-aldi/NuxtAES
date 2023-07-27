<template>
    <div>
        <section class="bg-white dark:bg-gray-900">
            <div class="max-w-screen-xl px-4 py-8 mx-auto lg:py-16">
                <div
                    class="p-8 mb-8 border border-gray-200 rounded-lg bg-gray-50 dark:bg-gray-800 dark:border-gray-700 md:p-12">
                    <h1 class="mb-2 text-3xl font-extrabold text-gray-900 dark:text-white md:text-5xl">How to quickly deploy
                        a static website</h1>
                    <p class="mb-6 text-lg font-normal text-gray-500 dark:text-gray-400">Static websites are now used to
                        bootstrap lots of websites and are becoming the basis for a variety of tools that even influence
                        both web designers and developers.</p>
                    <input
                        class="inline-flex justify-center items-center py-2.5 px-5 text-base font-medium text-center text-white rounded-lg bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 dark:focus:ring-blue-900"
                        type="file" @change="parseFile" ref="myFileUpload" />
                </div>
                <div class="relative overflow-x-auto shadow-md sm:rounded-lg">
                    <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
                        <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                            <tr>
                                <th v-for="(field, index) in visibleFields" :key="index" scope="col"
                                    class="px-6 py-3 min-w-min">
                                    <label :for="'selectableField' + field.column">
                                        <br />
                                        {{ field.cellName }}
                                    </label>
                                </th>
                                <th>Actions</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(user, index) in userRows" :key="index"
                                class="bg-white border-b dark:bg-gray-900 dark:border-gray-700">
                                <td class="px-6 py-4" v-for="(field, index) in visibleFields" :key="index">
                                    {{ user[field.cellName] }}
                                </td>
                                <td class="px-6 py-4">
                                    <button class="font-medium text-blue-600 dark:text-blue-500 hover:underline"
                                        @click="showModal(user)">Details</button>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </section>
    </div>
    <!-- Modal -->
    <!-- Vertically Centered Scrollable Extra Large Modal -->
    <div v-if="selectedUser"
        class="fixed inset-0 z-10 flex items-center justify-center w-screen h-screen bg-black bg-opacity-50">
        <div
            class="w-full max-w-4xl p-8 mb-8 overflow-hidden bg-white border border-gray-200 rounded-lg dark:bg-gray-800 dark:border-gray-700 md:p-12">
            <!-- Display user details in the modal -->
            <h2 class="mb-4 text-xl font-semibold">Student Details</h2>
            <div class="p-4 overflow-y-auto border bg-gray-50 max-h-96 border-grey-500">
                <div v-for="(value, key, index) in selectedUser" :key="index">
                    <div class="border-b border-grey-200">
                        <template v-if="index <= 3">
                            <!-- Show columns up to the third column -->
                            <div class="flex justify-between mb-2 ">
                                <strong class="text-gray-600">{{ key }}:</strong>
                                <span>{{ value }}</span>
                            </div>
                        </template>
                    </div>

                    <template v-if="index >= 4">
                        <div :id="index" class="mb-4 aes">
                            <a
                                class="mt-4 mb-4 bg-blue-100 text-blue-800 text-xl font-medium inline-flex items-center px-2.5 py-0.5 rounded-md dark:bg-gray-700 dark:text-blue-400 ">
                                <svg class="w-3 h-3 mr-1" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"
              aria-hidden="true">
              <path
                d="M2 6a2 2 0 012-2h6a2 2 0 012 2v8a2 2 0 01-2 2H4a2 2 0 01-2-2V6zM14.553 7.106A1 1 0 0014 8v4a1 1 0 00.553.894l2 1A1 1 0 0018 13V7a1 1 0 00-1.447-.894l-2 1z">
              </path>
            </svg> Pertanyaan
                            </a>
                            <p :class="'pertanyaan-' + index + ''">{{ key }}</p>
                            <!-- Show columns after the third column -->
                            <a
                                class="mt-4 mb-4 bg-green-100 text-green-800 text-xl font-medium inline-flex items-center px-2.5 py-0.5 rounded-md dark:bg-gray-700 dark:text-green-400">
                                <svg class="w-3 h-3 mr-1" fill="currentColor" viewBox="0 0 20 20"
                                    xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                                    <path clip-rule="evenodd" fill-rule="evenodd"
                                        d="M4 2a2 2 0 00-2 2v11a3 3 0 106 0V4a2 2 0 00-2-2H4zm1 14a1 1 0 100-2 1 1 0 000 2zm5-1.757l4.9-4.9a2 2 0 000-2.828L13.485 5.1a2 2 0 00-2.828 0L10 5.757v8.486zM16 18H9.071l6-6H16a2 2 0 012 2v2a2 2 0 01-2 2z">
                                    </path>
                                </svg> Jawaban</a>
                            <textarea :class="'jawaban-' + index + ' w-full p-2 rounded-md border border-gray-300'"
                                rows="4">{{ value }}</textarea>
                        </div>
                    </template>
                </div>
            </div>
            <button @click="processGpt3"
                class="px-4 py-2 mt-4 mr-2 text-sm font-medium text-white bg-blue-600 rounded-md hover:bg-blue-700 focus:outline-none focus:ring focus:ring-blue-300">Nilai</button>
            <!-- Close button -->
            <button @click="selectedUser = null"
                class="px-4 py-2 mt-4 text-sm font-medium text-white bg-red-600 rounded-md hover:bg-red-700 focus:outline-none focus:ring focus:ring-red-300">Close</button>
        </div>
    </div>
</template>
<script>
import Papa from 'papaparse';
definePageMeta({
    layout: "nav",
});
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
            message: 'Multiple AES with CSV',
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
            this.removeDetailClasses();
        },

        async processGpt3() {
            this.removeDetailClasses();
            const aesDivs = document.querySelectorAll(".aes");
            for (const div of aesDivs) {
                const divId = div.id;
                const pertanyaan = div.querySelector(`.pertanyaan-${div.id}`).textContent;
                const jawaban = div.querySelector(`.jawaban-${div.id}`).textContent;

                try {
                    await this.gpt3(pertanyaan, jawaban, divId); // Wait for gpt3() to finish before proceeding
                } catch (error) {
                    console.error(error);
                }
            }
        },

        gpt3(pertanyaan, jawaban, divId) {
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


                        const scoreRegex = /score:\s+(\d+)/;
                        const correctionRegex = /correction:\s+(.*)\s+confidence score:/;
                        const confidenceRegex = /confidence score:\s+(\d+%)/;

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
                        console.log("Index:", divId);
                        console.log("Score:", score);
                        console.log("Correction:", correction);
                        console.log("Confidence Score:", confidenceScore);

                        // shows it
                        // Step 1: Find the element with class "jawaban"
                        const jawabanElement = document.querySelector('.jawaban-' + divId);

                        if (jawabanElement) {
                            const h1ScoreElement = document.createElement('h1');
                            h1ScoreElement.textContent = 'Score: ' + score + '/10';
                            h1ScoreElement.style.color = 'Red';
                            h1ScoreElement.classList.add('score-class'); // Add class name 'score-class'

                            const h1CorrectionElement = document.createElement('h1');
                            h1CorrectionElement.textContent = 'Correction: ' + correction;
                            h1CorrectionElement.style.color = 'Green';
                            h1CorrectionElement.classList.add('correction-class'); // Add class name 'correction-class'

                            const h2ConfidenceScoreElement = document.createElement('h2');
                            h2ConfidenceScoreElement.textContent = 'Accurate: ' + confidenceScore;
                            h2ConfidenceScoreElement.style.color = 'blue';
                            h2ConfidenceScoreElement.classList.add('confidence-class'); // Add class name 'confidence-class'

                            jawabanElement.insertAdjacentElement('afterend', h2ConfidenceScoreElement);
                            jawabanElement.insertAdjacentElement('afterend', h1CorrectionElement);
                            jawabanElement.insertAdjacentElement('afterend', h1ScoreElement);



                        }


                        // You can handle the data here or store it in the component's data or state as needed.

                        resolve(); // Resolve the promise once processing is done
                    })
                    .catch((error) => {
                        reject(error);
                    });
            });
        },

        removeDetailClasses() {
            // Access the DOM elements using querySelectorAll and remove the classes
            const scoreElements = document.querySelectorAll('.score-class');
            const correctionElements = document.querySelectorAll('.correction-class');
            const confidenceElements = document.querySelectorAll('.confidence-class');

            scoreElements.forEach((element) => element.remove());
            correctionElements.forEach((element) => element.remove());
            confidenceElements.forEach((element) => element.remove());
        },

    },
};
</script>