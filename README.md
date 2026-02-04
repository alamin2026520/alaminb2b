# alaminb2b
https://alamin2026520.github.io/alaminb2b/
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Lead Generator</title>
<style>
body { font-family: Arial; margin: 20px; }
input, button { padding: 5px; margin: 5px 0; }
table { border-collapse: collapse; width: 100%; margin-top: 20px; }
table, th, td { border: 1px solid #333; }
th, td { padding: 8px; text-align: left; }
#status { margin-top: 10px; font-weight: bold; }
</style>
</head>
<body>

<h2>Lead Generator (Frontend Only)</h2>

<form id="leadForm">
  <label>Company Name:</label><br>
  <input type="text" id="companyName" required><br>
  <label>Target Position (optional):</label><br>
  <input type="text" id="targetPosition"><br><br>
  <button type="submit">Submit</button>
</form>

<div id="status"></div>

<table id="outputTable">
  <thead>
    <tr>
      <th>Company Name</th>
      <th>Company Website</th>
      <th>Company Email</th>
      <th>Company Address</th>
      <th>Person Name</th>
      <th>Position</th>
      <th>LinkedIn URL</th>
    </tr>
  </thead>
  <tbody></tbody>
</table>

<button id="downloadCSV">Download CSV</button>

<script>
const form = document.getElementById('leadForm');
const statusDiv = document.getElementById('status');
const outputTable = document.getElementById('outputTable').querySelector('tbody');
const downloadBtn = document.getElementById('downloadCSV');

form.addEventListener('submit', function(e){
    e.preventDefault();
    const companyName = document.getElementById('companyName').value;
    const targetPosition = document.getElementById('targetPosition').value || "Position Placeholder";

    statusDiv.innerText = "Processing...";

    // Simulated data for frontend-only version
    setTimeout(() => {
        const companyWebsite = `https://www.${companyName.replace(/\s+/g, '').toLowerCase()}.com`;
        const companyEmail = `info@${companyName.replace(/\s+/g, '').toLowerCase()}.com`;
        const companyAddress = `123 Main Street, City, Country`;

        const personName = "John Doe";
        const position = targetPosition;
        const linkedinURL = "https://linkedin.com/in/example";

        // Fill table
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td>${companyName}</td>
          <td>${companyWebsite}</td>
          <td>${companyEmail}</td>
          <td>${companyAddress}</td>
          <td>${personName}</td>
          <td>${position}</td>
          <td>${linkedinURL}</td>
        `;
        outputTable.appendChild(tr);

        statusDiv.innerText = "Done";
    }, 1000); // simulate processing delay
});

// CSV Download
downloadBtn.addEventListener('click', function(){
    let csv = 'Company Name,Company Website,Company Email,Company Address,Person Name,Position,LinkedIn URL\n';
    outputTable.querySelectorAll('tr').forEach(tr => {
        const row = Array.from(tr.querySelectorAll('td')).map(td => td.innerText);
        csv += row.join(',') + '\n';
    });
    const blob = new Blob([csv], { type: 'text/csv' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = 'leads.csv';
    a.click();
});
</script>

</body>
</html>
