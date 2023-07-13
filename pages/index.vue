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
        <div class="h-100 p-5 bg-body-tertiary rounded-3 shadow border">
          <h2>Upload a file</h2>

          <form action="/upload" method="post" enctype="multipart/form-data">
            <input type="file" name="file" />
            <button class="btn btn-primary" type="submit" value="Upload">Check</button>
          </form>
          <p><i>Supported types: pdf, xlsx, etc</i></p>
        </div>
      </div>
      <div class="col-md-6">
        <div class="h-100 p-5 bg-body-tertiary rounded-3 shadow border">
          <h2>Results</h2>
          

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
}
</script>
