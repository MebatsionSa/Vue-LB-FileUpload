<template>
  <div class="container">
        <label>File
            <input type="file" 
            :headers="multipart/form-data"
            accept="image/*"
            ref="file" v-on:change="handleFileUpload"/>
        </label>
        <button v-on:click="submitFile">Submit</button>
    </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data() {
    return {
      selectedFile: null
    }
  },
  methods: {
    submitFile() {
      console.log('imin')
      const fileObj = new FormData();
      fileObj.append('image', this.selectedFile, this.selectedFile.name)
      console.log('formdata',fileObj)
      axios.post('http://localhost:3000/api/StorageFiles/upload', fileObj)
      .then(res => {
        console.log(res);
      })
      .catch(function() {
        console.log('Failed............');
      });
    },
    handleFileUpload(event) { 
      this.selectedFile = this.$refs.file.files[0];
      // this.selectedFile = event.target.files[0];
      console.log(event)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
