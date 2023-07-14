<template>
  <div class="container py-4">
    <header class="pb-3 mb-4 border-bottom">
      <a href="/" class="d-flex align-items-center text-body-emphasis text-decoration-none">
        <span class="fs-3 ml-2">IDEA 1.0</span>
      </a>
    </header>

    <div class="p-5 mb-4 bg-body-tertiary rounded-3 shadow border">
      <div class="container-fluid py-5">
        <h1 class="display-5 fw-bold">Check financial documents.</h1>
        <p class="col-md-8 fs-4">Scan your financial documents for *buzzword* in *special phrase*. Lorem ipsum, lorem ipsum dolor sit amet.</p>
      </div>
    </div>

    <div class="row align-items-md-stretch">
      <div class="col-md-6">
        <div class="h-100 p-5 bg-body-tertiary rounded-3 shadow border" v-if="stage==0">
          <h2 class="text-center">Upload a file</h2>

          <form action="/upload" method="post" enctype="multipart/form-data" @submit.prevent="uploadFile()">
            <input type="file" name="file" ref="file" v-on:change="handleFileUpload()"/>
            <button class="btn btn-primary" type="submit" value="Upload">Check</button>
          </form>
          <p><i>Supported types: pdf, xlsx, etc</i></p>
        </div>
        <div class="h-100 p-5 bg-body-tertiary rounded-3 shadow border" v-if="stage==1">
          <h2 class="text-center">Uploading file</h2>
          <div class="d-flex justify-content-center">
            <div class="spinner-border" role="status">
              <span class="visually-hidden">Loading...</span>
            </div>
          </div>
        </div>
         <div class="h-100 p-5 bg-body-tertiary rounded-3 shadow border" v-if="stage==2">
          <h2 class="text-center">Processing through model</h2>
          <div class="d-flex justify-content-center">
            <div class="spinner-border" role="status">
              <span class="visually-hidden">Loading...</span>
            </div>
          </div>
        </div>
        <div class="h-100 p-5 bg-body-tertiary rounded-3 shadow border" v-if="stage==3">
          <h2 class="text-center">Your results are ready</h2>
          <p class="text-center">See the panel on the right.</p>
        </div>
      </div>
      <div class="col-md-6">
      <div class="h-100 p-5 bg-body-tertiary rounded-3 shadow border" v-if="stage==3">
          <h2 class="text-center">Results </h2>
          <table class="table rounded">
            <thead>
              <tr>
                <th scope="col">India</th>
                <th scope="col">Status</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>China</td>
                <td>✅Passed</td>
              </tr>
              <tr>
                <td>India</td>
                <td>✅Passed</td>
              </tr>
              <tr>
                <td>EU</td>
                <td>❌Failed</td>
              </tr>

            </tbody>
          </table>

      </div>
      <div class="h-100 p-5 bg-body-tertiary rounded-3 shadow border" v-if="stage<3">
          <h2 class="text-center">Results </h2>
          
          
          <p class="text-center">Results will be displayed here</p>

        </div>
      </div>
    </div>

    <footer class="pt-3 mt-4 text-body-secondary border-top">
      © 2023
    </footer>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',

  data(){
    return {
      file: '',
      stage : 0,
    }
  },

  methods: {
    handleFileUpload() {
      this.file = this.$refs.file.files[0];
    },
    getRandomArbitrary(min, max) {
      return Math.random() * (max - min) + min;
    },
    uploadFile() {
      console.log('uploading file');

      // get name of file
      const fileName = this.file.name;      

      // detect content type of file uploaded
      var contentType = this.file.type || 'application/octet-stream';

      const file = this.file;

      this.stage = 1;

      // (2) Let's upload the file
      fetch('https://storage.googleapis.com/upload/storage/v1/b/gravity-data/o?uploadType=media&name=' + fileName, {
        method: 'POST',
        headers: {
          'Authorization': 'Bearer ya29.a0AbVbY6OE4dsbMfYdItzXvSIzwaSCmxH3AqlfN0Fp6OdnpCmz8gLmAw0Rz0AbK4FA-BfgzMM0LUdfcr_3TXlCUM0aRFDCDN9m-mFIwdxMsl2fgZPz0_8rBXQ-Cf_2xzLuxdzgMOQExKZLsbotlvOnset4z_VtuocaCgYKAUkSARASFQFWKvPlEh3iVPtDwhg1_9pLp8cx7w0166',
          'Content-Type':  contentType,
        },
        body: file
      });
      // we really really shouldn't be dropping this token around so casually, but it's a hackathon, so who cares?

      // wait for 5 seconds
      setTimeout(() => {
        this.stage = 2;
      }, this.getRandomArbitrary(3000, 5000));

      // wait for 5 seconds
      setTimeout(() => {
        this.stage = 3;
      }, this.getRandomArbitrary(7000, 9000));


    }
  }
}
</script>
