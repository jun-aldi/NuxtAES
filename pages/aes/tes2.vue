<template>
    <div id="app">
      <h1 class="pb-5 text-3xl">{{ message }}</h1>
      <input type="file" @change="parseFile" ref="myFileUpload" />
      <table class="">
        <tr>
          <th v-for="field in fields" :key="field.column" class="min-w-min">
            <label :for="'selectableField'+field.column">
              <br />
              {{ field.cellName }}
            </label>
          </th>
          <th class="min-w-min">Detail</th>
        </tr>
        <tr v-for="(user, index) in userRows" :key="index">
          <td v-for="(key, value) in user" :key="key">
            {{ key }}
          </td>
          <td class="min-w-min">
            <button @click="toggleDetail(index)">
              {{ showDetail[index] ? 'Hide' : 'Detail' }}
            </button>
            <div v-if="showDetail[index]">
              <!-- Add your hidden columns here -->
              <span>Hidden Column 1: {{ user.hiddenColumn1 }}</span>
              <span>Hidden Column 2: {{ user.hiddenColumn2 }}</span>
            </div>
          </td>
        </tr>
      </table>
    </div>
  </template>
<script>
import Papa from 'papaparse';
export default {
  data() {
    return {
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
        preview: 11,
        header: true,
        complete: this.displayCompleteFile,
      },
      showDetail: [], // New data property to track the visibility of hidden columns
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
      this.showDetail = Array(this.userRows.length).fill(false); // Initialize showDetail with false for each row
    },
    parseFile(event) {
      this.results = Papa.parse(this.$refs.myFileUpload.files[0], this.config);
    },
    toggleDetail(index) {
      this.$set(this.showDetail, index, !this.showDetail[index]);
    },
  },
};
</script>
  