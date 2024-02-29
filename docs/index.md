# My Census Data Dashboard

<div id="my-table-container"></div>

```js

// const data = await FileAttachment("US-AK-census-naics4-2020.csv").csv();

class DataLoader {

  constructor(apiKey) {
    this.apiKey = apiKey; 
  }
  
  async loadDataCommons(dcid, property) {

    const url = `https://api.datacommons.org/v2/node?key=${this.apiKey}&nodes=${dcid}&property=${property}`;

    const response = await fetch(url);
    return await response.json();

  }

}

const API_KEY = 'AIzaSyCTI4Xz-UW_G2Q2RfknhcfdAnTHq5X5XuI'; 

const loader = new DataLoader(API_KEY);

// Fetch population of Los Angeles County
const data = await loader.loadDataCommons(
  'geoId/06', 
  '<-'
);
console.log(data)

function displayTableCSV(data) {
  const table = document.createElement("table");
  const thead = document.createElement("thead");
  const tbody = document.createElement("tbody");

  const headerRow = data[0];
  for (const key in headerRow) {
    const th = document.createElement("th");
    th.textContent = key;
    thead.appendChild(th);
  }

  for (const row of data) {
    const tr = document.createElement("tr");
    for (const key in row) {
      const td = document.createElement("td");
      td.textContent = row[key];
      tr.appendChild(td);
    }
    tbody.appendChild(tr);
  }

  const container = document.getElementById("my-table-container"); 
  container.appendChild(table);
  table.appendChild(thead);
  table.appendChild(tbody);
}

// Display function
function displayTableJSON(data) {

  // Handle data as object
  const records = data; 

  // Get keys  
  const keys = Object.keys(records);

  // Create table    
  const table = document.createElement('table');

  // Add headers
  const headerRow = document.createElement('tr');
  headerRow.innerHTML = `
    <th>Place</th>
    <th>Count</th> 
  `;
  table.appendChild(headerRow);  

  // Add data rows 
  for(const key of keys) {
    const row = document.createElement('tr');
    const nameCell = document.createElement('td'); 
    const countCell = document.createElement('td');

    nameCell.textContent = key; 
    countCell.textContent = records[key];

    row.appendChild(nameCell);
    row.appendChild(countCell);

    table.appendChild(row); 
  }

  // Display table
  document.body.appendChild(table);

}

// displayTableCSV(data);
displayTableJSON(data);