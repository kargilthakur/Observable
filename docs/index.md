# My Census Data Dashboard

<div id="my-table-container"></div>

```js

const data = await FileAttachment("US-AK-census-naics4-2020.csv").csv();
function displayTable(data) {
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

displayTable(data);
