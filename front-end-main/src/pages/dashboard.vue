<template>
    <div>
      <input type="file" @change="handleFileUpload" accept="image/*">
      <button @click="uploadImage">Upload</button>
      <span v-if="isUploaded" class="text-green-500 ml-2">File Uploaded!</span>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        selectedFile: null,
        isUploaded: false
      };
    },
    methods: {
      handleFileUpload(event) {
        this.selectedFile = event.target.files[0];
      },
      uploadImage() {
        const formData = new FormData();
        formData.append('image', this.selectedFile);
  
        axios.post('http://localhost:3001/api/upload', formData)
          .then(response => {
            console.log(response.data);
            console.log(response.data.imageUrl);
            // Handle the response as needed
            this.isUploaded = true; // Set isUploaded to true when upload is successful
          })
          .catch(error => {
            console.error(error);
            // Handle the error as needed
          });
      }
    }
  };
  </script>
  