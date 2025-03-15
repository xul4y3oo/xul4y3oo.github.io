<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>矩陣乘法計算器</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        table {
            border-collapse: collapse;
            margin-bottom: 20px;
        }
        table, th, td {
            border: 1px solid black;
        }
        th, td {
            padding: 10px;
            text-align: center;
        }
        .matrix-input {
            width: 40px;
        }
    </style>
</head>
<body>
    <h1>矩陣乘法計算器</h1>
    <h2>矩陣 A</h2>
    <table id="matrixA">
        <tr>
            <td><input type="number" class="matrix-input" id="a00" value="1"></td>
            <td><input type="number" class="matrix-input" id="a01" value="2"></td>
            <td><input type="number" class="matrix-input" id="a02" value="3"></td>
        </tr>
        <tr>
            <td><input type="number" class="matrix-input" id="a10" value="4"></td>
            <td><input type="number" class="matrix-input" id="a11" value="5"></td>
            <td><input type="number" class="matrix-input" id="a12" value="6"></td>
        </tr>
    </table>
    <h2>矩陣 B</h2>
    <table id="matrixB">
        <tr>
            <td><input type="number" class="matrix-input" id="b00" value="7"></td>
            <td><input type="number" class="matrix-input" id="b01" value="8"></td>
        </tr>
        <tr>
            <td><input type="number" class="matrix-input" id="b10" value="9"></td>
            <td><input type="number" class="matrix-input" id="b11" value="10"></td>
        </tr>
        <tr>
            <td><input type="number" class="matrix-input" id="b20" value="11"></td>
            <td><input type="number" class="matrix-input" id="b21" value="12"></td>
        </tr>
    </table>
    <button onclick="multiplyMatrices()">計算矩陣乘法</button>
    <h2>結果</h2>
    <table id="resultMatrix"></table>

    <script>
        function multiplyMatrices() {
            // Get values from input fields
            const matrixA = [
                [parseFloat(document.getElementById('a00').value), parseFloat(document.getElementById('a01').value), parseFloat(document.getElementById('a02').value)],
                [parseFloat(document.getElementById('a10').value), parseFloat(document.getElementById('a11').value), parseFloat(document.getElementById('a12').value)]
            ];

            const matrixB = [
                [parseFloat(document.getElementById('b00').value), parseFloat(document.getElementById('b01').value)],
                [parseFloat(document.getElementById('b10').value), parseFloat(document.getElementById('b11').value)],
                [parseFloat(document.getElementById('b20').value), parseFloat(document.getElementById('b21').value)]
            ];

            // Check if matrices can be multiplied
            const colsA = matrixA[0].length;
            const rowsB = matrixB.length;

            if (colsA !== rowsB) {
                alert('矩陣無法相乘');
                return;
            }

            // Initialize the result matrix with zeros
            const rowsA = matrixA.length;
            const colsB = matrixB[0].length;
            const result = Array(rowsA).fill(0).map(() => Array(colsB).fill(0));

            // Perform multiplication
            for (let i = 0; i < rowsA; i++) {
                for (let j = 0; j < colsB; j++) {
                    for (let k = 0; k < colsA; k++) {
                        result[i][j] += matrixA[i][k] * matrixB[k][j];
                    }
                }
            }

            // Display the result
            const resultTable = document.getElementById('resultMatrix');
            resultTable.innerHTML = '';
            for (let i = 0; i < rowsA; i++) {
                const row = document.createElement('tr');
                for (let j = 0; j < colsB; j++) {
                    const cell = document.createElement('td');
                    cell.innerText = result[i][j];
                    row.appendChild(cell);
                }
                resultTable.appendChild(row);
            }
        }
    </script>
</body>
</html>
