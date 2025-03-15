<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2x2 矩陣乘法計算器</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .container {
            text-align: center;
        }
        table {
            border-collapse: collapse;
            margin-bottom: 20px;
            margin-left: auto;
            margin-right: auto;
        }
        table, th, td {
            border: 1px solid black;
        }
        th, td {
            padding: 10px;
            text-align: center;
        }
        .matrix-input {
            width: 60px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>2x2 矩陣乘法計算器</h1>
        <h2>矩陣 A</h2>
        <table id="matrixA">
            <tr>
                <td><input type="text" class="matrix-input" id="a00" value="1"></td>
                <td><input type="text" class="matrix-input" id="a01" value="2"></td>
            </tr>
            <tr>
                <td><input type="text" class="matrix-input" id="a10" value="3"></td>
                <td><input type="text" class="matrix-input" id="a11" value="4"></td>
            </tr>
        </table>
        <h2>矩陣 B</h2>
        <table id="matrixB">
            <tr>
                <td><input type="text" class="matrix-input" id="b00" value="5"></td>
                <td><input type="text" class="matrix-input" id="b01" value="6"></td>
            </tr>
            <tr>
                <td><input type="text" class="matrix-input" id="b10" value="7"></td>
                <td><input type="text" class="matrix-input" id="b11" value="8"></td>
            </tr>
        </table>
        <button onclick="multiplyMatrices()">計算矩陣乘法</button>
        <h2>結果</h2>
        <table id="resultMatrix"></table>
    </div>

    <script>
        function parseMatrixInput(matrixId) {
            const matrix = [];
            for (let i = 0; i < 2; i++) {
                const row = [];
                for (let j = 0; j < 2; j++) {
                    const inputId = `${matrixId}${i}${j}`;
                    const value = document.getElementById(inputId).value;
                    row.push(value);
                }
                matrix.push(row);
            }
            return matrix;
        }

        function multiplyMatrices() {
            // Get values from input fields
            const matrixA = parseMatrixInput('a');
            const matrixB = parseMatrixInput('b');

            // Initialize the result matrix with empty strings
            const result = Array(2).fill('').map(() => Array(2).fill(''));

            // Perform multiplication
            for (let i = 0; i < 2; i++) {
                for (let j = 0; j < 2; j++) {
                    let sum = '';
                    for (let k = 0; k < 2; k++) {
                        sum += `(${matrixA[i][k]}*${matrixB[k][j]})+`;
                    }
                    result[i][j] = sum.slice(0, -1); // Remove the trailing '+'
                }
            }

            // Display the result
            const resultTable = document.getElementById('resultMatrix');
            resultTable.innerHTML = '';
            for (let i = 0; i < 2; i++) {
                const row = document.createElement('tr');
                for (let j = 0; j < 2; j++) {
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
