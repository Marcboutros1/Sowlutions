


<template>
    <div class="app">
      <h1>Search and Highlight</h1>
      <input
        type="text"
        v-model="searchQuery"
        placeholder="Search..."
        @input="filterResults"
      />
      <ul>
        <li v-for="item in filteredResults" :key="item">
          <span v-html="highlight(item, searchQuery)"></span>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue'
  
  export default {
    data() {
      return {
        searchQuery: "",
        items: [
          "Vue.js is a progressive JavaScript framework",
          "React is a popular library for building user interfaces",
          "Angular is a platform for building mobile and desktop web applications",
          "Svelte is a compiler that generates minimal and fast JavaScript",
          "Ember.js is a framework for ambitious web developers",
        ],
        filteredResults: [],
      };
    },
    mounted() {
      this.filteredResults = this.items;
    },
    methods: {
      filterResults() {
        if (this.searchQuery) {
          this.filteredResults = this.items.filter((item) =>
            item.toLowerCase().includes(this.searchQuery.toLowerCase())
          );
        } else {
          this.filteredResults = this.items;
        }
      },
      highlight(text, search) {
        if (!search) return text;
        const regex = new RegExp(`(${search})`, "gi");
        return text.replace(regex, "<mark>$1</mark>");
      },
    },
  };
  </script>
  
  <style>
  .app {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
  }
  
  input {
    width: 100%;
    padding: 10px;
    margin-bottom: 20px;
    font-size: 16px;
  }
  
  mark {
    background-color: yellow;
  }
  </style>