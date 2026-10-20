---
title: Cleaning Estimate HTML
updated: 2025-11-08 14:54:26Z
created: 2025-11-08 14:52:50Z
---

```html


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cleaning Estimate Generator</title>
    <style>
        body {
            font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif, sans-serif;
            margin: 20px;
            padding: 20px;
            background-color: hsl(0, 2%, 8%);
            border: 1px solid #000000;
            border-radius: 10px;
        }
        h1 {
            text-align: center;
            color: #8d8d8d;

          }
        h2 {
            background-color: #a02f1b;
            color: rgb(252, 255, 94);
            text-align: center;
            padding: 10px;
            border-radius: 10px;
            margin-top: 20px;
            margin-bottom: 20px;
            font: 400 1.5em 'Open Sans', sans-serif;
        }  
        h3 {
            text-align: left;
            color: rgb(114, 114, 114);
        }
        label {
            display: block;
            margin-top: 10px;
            color:rgb(131, 131, 131);
        }
        input, textarea, select {
            width: 80%;
            padding: 8px;
            margin-top: 5px;
            border-radius: 5px;
        }
        button {
            margin-top: 20px;
            padding: 10px 15px;
            background-color: #a02f1b;
            color: rgb(252, 255, 94);
            border: solid 2px;
            border-radius: 15px;
            cursor: pointer;
            border-radius: 30px;
        }
        button:hover {
          background-color: rgb(252, 255, 94);
          color:#a02f1b;
        }
        .supply-item {
            margin-bottom: 10px;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Commercial Cleaning Invoice Generator</h1>
    <h3>by Daniel Moore</h3>
    <form id="invoice-form">
        <label for="job-date">Job Date:</label>
        <input type="date" id="job-date" required>

        <h3>Supplies Needed:</h3>
        <div id="supplies-container">
            <div class="supply-item">
                <label for="supply-name-1">Item:</label>
                <input type="text" id="supply-name-1" placeholder="Enter supply name" required>
                <label for="supply-cost-1">Cost per item:</label>
                <input type="number" id="supply-cost-1" placeholder="Enter cost in USD, omit $" required>
                <label for="supply-qty-1">Quantity of same items:</label>
                <input type="number" id="supply-qty-1" placeholder="Enter quantity" required>
            </div>
        </div>
        <button type="button" onclick="addSupply()">Add Another Item</button>

        <h3>Hours Worked and Surface Area:</h3>
        <label for="total-hours">Total Hours Estimated:</label>
        <input type="number" id="total-hours" placeholder="Enter number of hours it will take to complete all tasks." required>

        <label for="surface-area">Surface Area (sqft):</label>
        <input type="number" id="surface-area" placeholder="Enter square footage total of all surfaces." required>

        <label for="client-signature">Client Signature:</label>
        <input type="text" id="client-signature" placeholder="Enter client's name and I will calculate a rough estimate.">

        <button type="button" onclick="generateInvoice()">Generate Estimate</button>
    </form>

    <h2>Estimated Cost Summary</h2>
    <div id="invoice-summary" style="display:none; margin-top: 20px;"></div>

    <script>
        let supplyIndex = 1;

        function addSupply() {
            supplyIndex++;
            const supplyContainer = document.getElementById('supplies-container');
            const newSupply = document.createElement('div');
            newSupply.className = 'supply-item';
            newSupply.innerHTML = `
                <label for="supply-name-${supplyIndex}">Supply Name:</label>
                <input type="text" id="supply-name-${supplyIndex}" placeholder="Enter supply name" required>
                <label for="supply-cost-${supplyIndex}">Cost:</label>
                <input type="number" id="supply-cost-${supplyIndex}" placeholder="Enter cost" required>
                <label for="supply-qty-${supplyIndex}">Quantity:</label>
                <input type="number" id="supply-qty-${supplyIndex}" placeholder="Enter quantity" required>
            `;
            supplyContainer.appendChild(newSupply);
        }

        function generateInvoice() {
            const jobDate = document.getElementById('job-date').value;
            const totalHours = document.getElementById('total-hours').value;
            const surfaceArea = document.getElementById('surface-area').value;
            const clientSignature = document.getElementById('client-signature').value;

            // Cost calculations
            const setupCost = 100; // First hour includes setup cost and materials purchased
            const hourlyCost = 25; // Per hour rate,after setup
            const totalCost = setupCost + (Math.max(0, totalHours - 1) * hourlyCost);

            // Calculate supplies total cost
            let suppliesTotal = 0;
            for (let i = 1; i <= supplyIndex; i++) {
                const cost = parseFloat(document.getElementById(`supply-cost-${i}`).value) || 0;
                const qty = parseInt(document.getElementById(`supply-qty-${i}`).value) || 0;
                suppliesTotal += cost * qty;
            }

            const grandTotal = totalCost + suppliesTotal;

            // Displaying the invoice summary
            const invoiceSummary = `
                <strong>Job Date:</strong> ${jobDate}<br>
                <strong>Supplies Needed:</strong><br>
                ${Array.from({ length: supplyIndex }, (_, i) => {
                    const name = document.getElementById(`supply-name-${i + 1}`).value || 'N/A';
                    const cost = document.getElementById(`supply-cost-${i + 1}`).value || 0;
                    const qty = document.getElementById(`supply-qty-${i + 1}`).value || 0;
                    return `${name} - $${cost} x ${qty} = $${(cost * qty).toFixed(2)}<br>`;
                }).join('')}
                <strong>Estiimate of labor time:</strong> ${totalHours}<br>
                <strong>Surface Area:</strong> ${surfaceArea} sqft<br>
                <strong>Client:</strong> ${clientSignature}<br>
                <strong>Supplies Total Cost:</strong> $${suppliesTotal.toFixed(2)}<br>
                <strong>Total Cost including Labor:</strong> $${grandTotal.toFixed(2)}<br>
                <strong>Hours of labor accounted for in Estimate:</strong> ${totalHours}<br>
            `;
            document.getElementById('invoice-summary').innerHTML = invoiceSummary;
            document.getElementById('invoice-summary').style.display = 'block';
        }
    </script>
</body>
</html>


'''