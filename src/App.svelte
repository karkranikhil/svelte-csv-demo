<script>
  import { onMount } from "svelte";
  import { csvGenerator } from "./csvGenerator";

  let tableData = [];
  /** default Headers name **/
  let tableHeader = ["User Id", "ID", "Title", "Description"];
  /**Lifecycle hook to load JSON from service**/
  onMount(async () => {
    const res = await fetch(`https://jsonplaceholder.typicode.com/posts`);
    tableData = await res.json();
    console.log(tableData);
  });
  /** Download handler **/
    function downloadHandler() {
  		let tableKeys = Object.keys(tableData[0]); // Extracting the key names from Object
		csvGenerator(tableData, tableKeys, tableHeader, "svelte_csv_demo.csv");

    }
</script>

<style>
  .container {
    max-width: 1140px;
    margin: auto;
  }
  .header {
    display: flex;
    justify-content: space-between;
    display: flex;
    justify-content: space-between;
    background: orange;
    padding: 10px;
  }
  table {
    font-family: arial, sans-serif;
    border-collapse: collapse;
    width: 100%;
  }

  td,
  th {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 8px;
  }

  tr:nth-child(even) {
    background-color: #dddddd;
  }
  button {
    border: none; /* Remove borders */
    color: white; /* Add a text color */
    padding: 14px 28px; /* Add some padding */
    cursor: pointer; /* Add a pointer cursor on mouse-over */
    background-color: #4caf50;
    height: fit-content;
  }
  h1 {
    margin: 0px;
  }
</style>

<div class="container">
  <div class="header">
    <h1>CSV generation using svelte</h1>
    <button on:click={downloadHandler}>Download</button>

  </div>

  <div class="main">
    <table>
      <thead>
        <tr>
          {#each tableHeader as header}
            <th>{header}</th>
          {/each}
        </tr>
      </thead>
      <tbody>
        {#each tableData as item}
          <tr>
            <td>{item.userId}</td>
            <td>{item.id}</td>
            <td>{item.title}</td>
            <td>{item.body}</td>
          </tr>
        {/each}
      </tbody>
    </table>

  </div>
</div>
