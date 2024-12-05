<template>
    <div class="info">
      <h1>TranDucTin</h1>
      <section>
        <h2>Author Information</h2>
        <p><strong>Name:</strong> Tran Duc Tin GCS220477</p>
       
    
        <p>
          This is webpage build by Tran Duc TIn.
        </p>
      </section>
 
    </div>
  </template>
  
  <script>
  export default {
    name: 'Info'
  };
  </script>
  
  <style scoped>
  .info {
    max-width: 800px;
    margin: auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 8px;
    background-color: #f9f9f9;
  }
  
  h1, h2 {
    text-align: center;
    color: #333;
  }
  
  p, ul {
    font-size: 16px;
    line-height: 1.6;
    color: #555;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  ul li {
    margin-bottom: 10px;
  }
  
  ul li strong {
    color: #000;
  }
  </style>
  