<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Property Yield Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            align-items: flex-start;
            justify-content: center;
            padding: 20px;
        }

        .main-wrapper {
            max-width: 1200px;
            width: 100%;
        }

        .content-layout {
            display: grid;
            grid-template-columns: 1fr;
            gap: 20px;
            align-items: start;
        }

        .container {
            background: white;
            border-radius: 10px;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
            max-width: 100%;
            width: 100%;
            padding: 40px;
            margin-bottom: 20px;
        }

        h1 {
            color: #333;
            margin-bottom: 30px;
            text-align: center;
            font-size: 28px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            color: #555;
            font-weight: 500;
            font-size: 14px;
        }

        input[type="text"],
        input[type="number"] {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 5px;
            font-size: 14px;
            transition: border-color 0.3s;
        }

        input[type="text"]:focus,
        input[type="number"]:focus {
            outline: none;
            border-color: #667eea;
        }

        button {
            width: 100%;
            padding: 12px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.2s;
        }

        button:hover {
            transform: translateY(-2px);
        }

        button:active {
            transform: translateY(0);
        }

        .results {
            margin-top: 30px;
            padding: 20px;
            background: #f5f5f5;
            border-radius: 5px;
            display: none;
        }

        .results.show {
            display: block;
            animation: slideIn 0.3s ease-in;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(-10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .result-item {
            margin-bottom: 15px;
        }

        .result-label {
            color: #666;
            font-size: 13px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .result-value {
            color: #333;
            font-size: 20px;
            font-weight: 600;
            margin-top: 4px;
        }

        .yield-highlight {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 15px;
            border-radius: 5px;
            margin-top: 10px;
        }

        .yield-highlight .result-label {
            color: rgba(255, 255, 255, 0.8);
        }

        .yield-highlight .result-value {
            color: white;
            font-size: 28px;
        }

        .error {
            background: #fee;
            color: #c33;
            padding: 12px;
            border-radius: 5px;
            margin-top: 10px;
            display: none;
        }

        .error.show {
            display: block;
        }

        .input-hint {
            font-size: 12px;
            color: #999;
            margin-top: 4px;
        }

        .save-button {
            margin-top: 15px;
            padding: 10px;
            background: #28a745;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.2s;
        }

        .save-button:hover {
            background: #218838;
            transform: translateY(-2px);
        }

        .comparison-section {
            margin-top: 40px;
            padding-top: 30px;
            border-top: 2px solid #e0e0e0;
        }

        .comparison-section h2 {
            color: #333;
            font-size: 20px;
            margin-bottom: 20px;
        }

        .table-container {
            overflow-x: auto;
            background: #f9f9f9;
            border-radius: 5px;
            border: 1px solid #e0e0e0;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 13px;
        }

        th {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 12px;
            text-align: left;
            font-weight: 600;
        }

        td {
            padding: 12px;
            border-bottom: 1px solid #e0e0e0;
        }

        tr:hover {
            background: #f0f0f0;
        }

        .delete-btn {
            background: #dc3545;
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 3px;
            cursor: pointer;
            font-size: 12px;
        }

        .delete-btn:hover {
            background: #c82333;
        }

        .no-data {
            text-align: center;
            padding: 20px;
            color: #999;
            font-size: 14px;
        }

        .clear-all-btn {
            background: #dc3545;
            color: white;
            border: none;
            padding: 8px 16px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 14px;
            margin-top: 10px;
        }

        .clear-all-btn:hover {
            background: #c82333;
        }

        .export-btn {
            background: #007bff;
            color: white;
            border: none;
            padding: 8px 16px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 14px;
            margin-top: 10px;
            margin-right: 10px;
        }

        .export-btn:hover {
            background: #0056b3;
        }

        .highlight-row {
            background: #fff3cd;
        }

        .sensitivity-section {
            margin-top: 40px;
            padding-top: 30px;
            border-top: 2px solid #e0e0e0;
        }

        .sensitivity-section h2 {
            color: #333;
            font-size: 20px;
            margin-bottom: 20px;
        }

        .slider-group {
            margin-bottom: 25px;
            padding: 15px;
            background: #f9f9f9;
            border-radius: 5px;
        }

        .slider-label {
            display: flex;
            justify-content: space-between;
            margin-bottom: 8px;
            font-size: 14px;
        }

        .slider-label-name {
            color: #555;
            font-weight: 500;
        }

        .slider-value {
            color: #667eea;
            font-weight: 600;
        }

        input[type="range"] {
            width: 100%;
            height: 6px;
            border-radius: 3px;
            background: #ddd;
            outline: none;
            -webkit-appearance: none;
            appearance: none;
        }

        input[type="range"]::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            cursor: pointer;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        }

        input[type="range"]::-moz-range-thumb {
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            cursor: pointer;
            border: none;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        }

        .sensitivity-results {
            margin-top: 25px;
            padding: 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border-radius: 5px;
        }

        .sensitivity-results h3 {
            font-size: 16px;
            margin-bottom: 15px;
        }

        .sensitivity-yield {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 15px;
        }

        .sensitivity-yield-item {
            background: rgba(255, 255, 255, 0.1);
            padding: 12px;
            border-radius: 5px;
            text-align: center;
        }

        .sensitivity-yield-label {
            font-size: 12px;
            opacity: 0.9;
            margin-bottom: 5px;
        }

        .sensitivity-yield-value {
            font-size: 24px;
            font-weight: 600;
        }

        .sensitivity-buttons {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .reset-sensitivity-btn {
            background: rgba(255, 255, 255, 0.2);
            color: white;
            border: 2px solid white;
            padding: 8px 16px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 14px;
            flex: 1;
            min-width: 150px;
        }

        .reset-sensitivity-btn:hover {
            background: rgba(255, 255, 255, 0.3);
        }

        .save-sensitivity-btn {
            background: rgba(255, 255, 255, 0.2);
            color: white;
            border: 2px solid white;
            padding: 8px 16px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 14px;
            flex: 1;
            min-width: 150px;
        }

        .save-sensitivity-btn:hover {
            background: rgba(255, 255, 255, 0.3);
        }

        .reload-btn {
            background: #17a2b8;
            color: white;
            border: none;
            padding: 4px 8px;
            border-radius: 3px;
            cursor: pointer;
            font-size: 11px;
            margin-right: 5px;
        }

        .reload-btn:hover {
            background: #117a8b;
        }
    </style>
</head>
<body>
    <div class="main-wrapper">
        <div class="content-layout">
            <div class="container">
                <h1>🏠 Property Yield Calculator</h1>
        
        <form id="propertyForm">
            <div class="form-group">
                <label for="name">Property Name/Address</label>
                <input type="text" id="name" name="name" required placeholder="e.g., 221B Baker Street">
            </div>

            <div class="form-group">
                <label for="price">Price (in $1000s)</label>
                <input type="number" id="price" name="price" required placeholder="e.g., 500">
                <div class="input-hint">Enter 500 for $500,000</div>
            </div>

            <div class="form-group">
                <label for="rent">Weekly Rent ($)</label>
                <input type="number" id="rent" name="rent" required placeholder="e.g., 600">
                <div class="input-hint">Enter amount in dollars per week</div>
            </div>

            <div class="form-group">
                <label for="owners_corp">Owners Corp Fee (Quarterly $)</label>
                <input type="number" id="owners_corp" name="owners_corp" required placeholder="e.g., 1200">
                <div class="input-hint">Quarterly maintenance/strata fee</div>
            </div>

            <div class="form-group">
                <label for="council_rate">Council Rate (Quarterly $)</label>
                <input type="number" id="council_rate" name="council_rate" required placeholder="e.g., 300">
                <div class="input-hint">Quarterly council rate</div>
            </div>

            <div class="form-group">
                <label for="water_rate">Water Rate (Quarterly $)</label>
                <input type="number" id="water_rate" name="water_rate" required placeholder="e.g., 200">
                <div class="input-hint">Quarterly water rate</div>
            </div>

            <button type="submit">Calculate Yield</button>
        </form>

        <div class="error" id="error"></div>

        <div class="results" id="results">
            <div class="result-item">
                <div class="result-label">Property</div>
                <div class="result-value" id="resultName"></div>
            </div>

            <div class="result-item">
                <div class="result-label">Purchase Price</div>
                <div class="result-value" id="resultPrice"></div>
            </div>

            <div class="result-item yield-highlight">
                <div class="result-label">Gross Yield</div>
                <div class="result-value" id="resultGrossYield"></div>
            </div>

            <div class="result-item yield-highlight">
                <div class="result-label">Net Yield</div>
                <div class="result-value" id="resultNetYield"></div>
            </div>

            <div style="margin-top: 15px; font-size: 12px; color: #999;">
                <strong>Details:</strong><br>
                Weekly Rent: $<span id="resultRent"></span> | 
                Owners Corp: $<span id="resultOwnersCorp"></span>/qtr | 
                Council: $<span id="resultCouncil"></span>/qtr | 
                Water: $<span id="resultWater"></span>/qtr
            </div>
            <button class="save-button" id="saveBtn">💾 Save This Property</button>
        </div>

        <div class="sensitivity-section" id="sensitivitySection" style="display: none;">
            <h2>🔍 Sensitivity Tester</h2>
            <p style="color: #666; font-size: 14px; margin-bottom: 20px;">Adjust values with sliders to see how yields change:</p>
            
            <div class="slider-group">
                <div class="slider-label">
                    <span class="slider-label-name">Weekly Rent</span>
                    <span class="slider-value">$<span id="rentSliderValue">0</span></span>
                </div>
                <input type="range" id="rentSlider" min="-50" max="50" value="0" step="1">
                <div style="font-size: 11px; color: #999; margin-top: 5px; text-align: center;">-50% to +50%</div>
            </div>

            <div class="slider-group">
                <div class="slider-label">
                    <span class="slider-label-name">Property Price</span>
                    <span class="slider-value">$<span id="priceSliderValue">0</span>k</span>
                </div>
                <input type="range" id="priceSlider" min="-50" max="50" value="0" step="1">
                <div style="font-size: 11px; color: #999; margin-top: 5px; text-align: center;">-50% to +50%</div>
            </div>

            <div class="slider-group">
                <div class="slider-label">
                    <span class="slider-label-name">Owners Corp Fee (Quarterly)</span>
                    <span class="slider-value">$<span id="corpSliderValue">0</span></span>
                </div>
                <input type="range" id="corpSlider" min="-50" max="50" value="0" step="1">
                <div style="font-size: 11px; color: #999; margin-top: 5px; text-align: center;">-50% to +50%</div>
            </div>

            <div class="slider-group">
                <div class="slider-label">
                    <span class="slider-label-name">Council Rate (Quarterly)</span>
                    <span class="slider-value">$<span id="councilSliderValue">0</span></span>
                </div>
                <input type="range" id="councilSlider" min="-50" max="50" value="0" step="1">
                <div style="font-size: 11px; color: #999; margin-top: 5px; text-align: center;">-50% to +50%</div>
            </div>

            <div class="slider-group">
                <div class="slider-label">
                    <span class="slider-label-name">Water Rate (Quarterly)</span>
                    <span class="slider-value">$<span id="waterSliderValue">0</span></span>
                </div>
                <input type="range" id="waterSlider" min="-50" max="50" value="0" step="1">
                <div style="font-size: 11px; color: #999; margin-top: 5px; text-align: center;">-50% to +50%</div>
            </div>

            <div class="sensitivity-results">
                <h3>Updated Yields</h3>
                <div class="sensitivity-yield">
                    <div class="sensitivity-yield-item">
                        <div class="sensitivity-yield-label">Gross Yield</div>
                        <div class="sensitivity-yield-value" id="sensitivityGrossYield">0%</div>
                    </div>
                    <div class="sensitivity-yield-item">
                        <div class="sensitivity-yield-label">Net Yield</div>
                        <div class="sensitivity-yield-value" id="sensitivityNetYield">0%</div>
                    </div>
                </div>
                <div class="sensitivity-buttons">
                    <button class="reset-sensitivity-btn" id="resetSensitivityBtn">Reset Sliders</button>
                    <button class="save-sensitivity-btn" id="saveSensitivityBtn">💾 Save Sensitivity Result</button>
                </div>
            </div>
        </div>
            </div>
            <div class="container comparison-section" id="comparisonSection" style="display: none;">
                <h2>📊 Saved Properties</h2>
        <div style="margin-bottom: 15px;">
            <button class="export-btn" id="exportBtn">📥 Export to CSV</button>
            <button class="clear-all-btn" id="clearAllBtn">Clear All</button>
        </div>
        <div class="table-container">
            <table id="comparisonTable">
                <thead>
                    <tr>
                        <th>Property</th>
                        <th>Price</th>
                        <th>Weekly Rent</th>
                        <th>Owners Corp/qtr</th>
                        <th>Council/qtr</th>
                        <th>Water/qtr</th>
                        <th>Gross Yield</th>
                        <th>Net Yield</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody id="tableBody">
                    <tr class="no-data"><td colspan="10">No saved properties yet. Calculate and save one!</td></tr>
                </tbody>
            </table>
        </div>
            </div>
        </div>
    </div>

    <script>
        let currentResult = null;

        function calculateYield(price, rent, owners_corp, council_rate, water_rate) {
            const gross_yield = (rent * 52) / (price * 1000) * 100;
            const net_yield = (rent * 52 - owners_corp * 4 - council_rate * 4 - water_rate * 4) / (price * 1000) * 100;
            
            return {
                gross_yield: gross_yield.toFixed(2),
                net_yield: net_yield.toFixed(2)
            };
        }

        function loadSavedProperties() {
            const saved = localStorage.getItem('savedProperties');
            return saved ? JSON.parse(saved) : [];
        }

        function saveTolocalStorage(properties) {
            localStorage.setItem('savedProperties', JSON.stringify(properties));
        }

        function updateComparisonTable() {
            const properties = loadSavedProperties();
            const tbody = document.getElementById('tableBody');
            const comparisonSection = document.getElementById('comparisonSection');

            if (properties.length === 0) {
                tbody.innerHTML = '<tr class="no-data"><td colspan="10">No saved properties yet. Calculate and save one!</td></tr>';
                comparisonSection.style.display = 'none';
                return;
            }

            comparisonSection.style.display = 'block';
            tbody.innerHTML = properties.map((prop, index) => `
                <tr>
                    <td><strong>${prop.name}</strong></td>
                    <td>$${prop.price}k</td>
                    <td>$${prop.rent}</td>
                    <td>$${prop.owners_corp}</td>
                    <td>$${prop.council_rate}</td>
                    <td>$${prop.water_rate}</td>
                    <td><strong>${prop.gross_yield}%</strong></td>
                    <td><strong style="color: #667eea;">${prop.net_yield}%</strong></td>
                    <td>
                       <button class="reload-btn" onclick="reloadProperty(${index})">Reload</button>
                       <button class="delete-btn" onclick="deleteProperty(${index})">Delete</button>
                    </td>
                </tr>
            `).join('');
        }

        function deleteProperty(index) {
            const properties = loadSavedProperties();
            properties.splice(index, 1);
            saveTolocalStorage(properties);
            updateComparisonTable();
        }

        function reloadProperty(index) {
            const properties = loadSavedProperties();
            const prop = properties[index];
            
            // Fill the form with the property data
            document.getElementById('name').value = prop.name;
            document.getElementById('price').value = prop.price;
            document.getElementById('rent').value = prop.rent;
            document.getElementById('owners_corp').value = prop.owners_corp;
            document.getElementById('council_rate').value = prop.council_rate;
            document.getElementById('water_rate').value = prop.water_rate;
            
            // Trigger calculation
            const submitEvent = new Event('submit');
            document.getElementById('propertyForm').dispatchEvent(submitEvent);
            
            // Scroll to top
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function saveCurrentResult() {
            if (!currentResult) {
                alert('Please calculate a yield first!');
                return;
            }

            const properties = loadSavedProperties();
            properties.push(currentResult);
            saveTolocalStorage(properties);
            
            alert('✅ Property saved!');
            updateComparisonTable();
        }

        function exportToCSV() {
            const properties = loadSavedProperties();
            if (properties.length === 0) {
                alert('No properties to export!');
                return;
            }

            let csv = 'Property,Price ($k),Weekly Rent,Owners Corp (quarterly),Council (quarterly),Water (quarterly),Gross Yield (%),Net Yield (%)\n';
            
            properties.forEach(prop => {
                csv += `"${prop.name}",${prop.price},${prop.rent},${prop.owners_corp},${prop.council_rate},${prop.water_rate},${prop.gross_yield},${prop.net_yield}\n`;
            });

            const blob = new Blob([csv], { type: 'text/csv' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'PropertyYieldComparison.csv';
            a.click();
            window.URL.revokeObjectURL(url);
        }

        function clearAllProperties() {
            if (confirm('Are you sure you want to delete all saved properties?')) {
                localStorage.removeItem('savedProperties');
                updateComparisonTable();
                alert('All properties cleared!');
            }
        }

        document.getElementById('propertyForm').addEventListener('submit', (e) => {
            e.preventDefault();
            
            const errorDiv = document.getElementById('error');
            errorDiv.classList.remove('show');

            try {
                const name = document.getElementById('name').value;
                const price = parseFloat(document.getElementById('price').value);
                const rent = parseFloat(document.getElementById('rent').value);
                const owners_corp = parseFloat(document.getElementById('owners_corp').value);
                const council_rate = parseFloat(document.getElementById('council_rate').value);
                const water_rate = parseFloat(document.getElementById('water_rate').value);

                if (!name || !price || !rent || owners_corp === '' || council_rate === '' || water_rate === '') {
                    throw new Error('Please fill in all fields');
                }

                const result = calculateYield(price, rent, owners_corp, council_rate, water_rate);

                currentResult = {
                    name,
                    price,
                    rent,
                    owners_corp,
                    council_rate,
                    water_rate,
                    gross_yield: result.gross_yield,
                    net_yield: result.net_yield
                };

                document.getElementById('resultName').textContent = name;
                document.getElementById('resultPrice').textContent = `$${price}k`;
                document.getElementById('resultRent').textContent = rent;
                document.getElementById('resultOwnersCorp').textContent = owners_corp;
                document.getElementById('resultCouncil').textContent = council_rate;
                document.getElementById('resultWater').textContent = water_rate;
                document.getElementById('resultGrossYield').textContent = `${result.gross_yield}%`;
                document.getElementById('resultNetYield').textContent = `${result.net_yield}%`;
                document.getElementById('results').classList.add('show');
            } catch (error) {
                errorDiv.textContent = `Error: ${error.message}`;
                errorDiv.classList.add('show');
            }
        });

        document.getElementById('saveBtn').addEventListener('click', saveCurrentResult);
        document.getElementById('exportBtn').addEventListener('click', exportToCSV);
        document.getElementById('clearAllBtn').addEventListener('click', clearAllProperties);

        function updateSensitivityDisplay() {
            if (!currentResult) return;

            const rentPercent = parseFloat(document.getElementById('rentSlider').value);
            const pricePercent = parseFloat(document.getElementById('priceSlider').value);
            const corpPercent = parseFloat(document.getElementById('corpSlider').value);
            const councilPercent = parseFloat(document.getElementById('councilSlider').value);
            const waterPercent = parseFloat(document.getElementById('waterSlider').value);

            // Calculate adjusted values
            const adjustedPrice = currentResult.price * (1 + pricePercent / 100);
            const adjustedRent = currentResult.rent * (1 + rentPercent / 100);
            const adjustedCorp = currentResult.owners_corp * (1 + corpPercent / 100);
            const adjustedCouncil = currentResult.council_rate * (1 + councilPercent / 100);
            const adjustedWater = currentResult.water_rate * (1 + waterPercent / 100);

            // Display adjusted values
            document.getElementById('priceSliderValue').textContent = adjustedPrice.toFixed(2);
            document.getElementById('rentSliderValue').textContent = adjustedRent.toFixed(2);
            document.getElementById('corpSliderValue').textContent = adjustedCorp.toFixed(2);
            document.getElementById('councilSliderValue').textContent = adjustedCouncil.toFixed(2);
            document.getElementById('waterSliderValue').textContent = adjustedWater.toFixed(2);

            // Calculate new yields
            const result = calculateYield(adjustedPrice, adjustedRent, adjustedCorp, adjustedCouncil, adjustedWater);
            
            document.getElementById('sensitivityGrossYield').textContent = `${result.gross_yield}%`;
            document.getElementById('sensitivityNetYield').textContent = `${result.net_yield}%`;
        }

        function resetSensitivity() {
            document.getElementById('priceSlider').value = 0;
            document.getElementById('rentSlider').value = 0;
            document.getElementById('corpSlider').value = 0;
            document.getElementById('councilSlider').value = 0;
            document.getElementById('waterSlider').value = 0;
            updateSensitivityDisplay();
        }

        // Slider event listeners
        document.getElementById('priceSlider').addEventListener('input', updateSensitivityDisplay);
        document.getElementById('rentSlider').addEventListener('input', updateSensitivityDisplay);
        document.getElementById('corpSlider').addEventListener('input', updateSensitivityDisplay);
        document.getElementById('councilSlider').addEventListener('input', updateSensitivityDisplay);
        document.getElementById('waterSlider').addEventListener('input', updateSensitivityDisplay);
        document.getElementById('resetSensitivityBtn').addEventListener('click', resetSensitivity);

        function saveSensitivityAnalysis() {
            if (!currentResult) {
                alert('Please calculate a yield first!');
                return;
            }

            const rentPercent = parseFloat(document.getElementById('rentSlider').value);
            const pricePercent = parseFloat(document.getElementById('priceSlider').value);
            const corpPercent = parseFloat(document.getElementById('corpSlider').value);
            const councilPercent = parseFloat(document.getElementById('councilSlider').value);
            const waterPercent = parseFloat(document.getElementById('waterSlider').value);

            // Calculate adjusted values
            const adjustedPrice = currentResult.price * (1 + pricePercent / 100);
            const adjustedRent = currentResult.rent * (1 + rentPercent / 100);
            const adjustedCorp = currentResult.owners_corp * (1 + corpPercent / 100);
            const adjustedCouncil = currentResult.council_rate * (1 + councilPercent / 100);
            const adjustedWater = currentResult.water_rate * (1 + waterPercent / 100);

            const result = calculateYield(adjustedPrice, adjustedRent, adjustedCorp, adjustedCouncil, adjustedWater);

            const scenarioName = `${currentResult.name} (Scenario: P${pricePercent>0?'+':' '}${pricePercent}%, R${rentPercent>0?'+':' '}${rentPercent}%)`;

            const sensitivity = {
                name: scenarioName,
                price: adjustedPrice,
                rent: adjustedRent,
                owners_corp: adjustedCorp,
                council_rate: adjustedCouncil,
                water_rate: adjustedWater,
                gross_yield: result.gross_yield,
                net_yield: result.net_yield
            };

            const properties = loadSavedProperties();
            properties.push(sensitivity);
            saveTolocalStorage(properties);
            
            alert('✅ Sensitivity scenario saved!');
            updateComparisonTable();
        }

        document.getElementById('saveSensitivityBtn').addEventListener('click', saveSensitivityAnalysis);

        // Modify the form submit to show sensitivity section
        const originalFormSubmit = document.getElementById('propertyForm').onsubmit;
        document.getElementById('propertyForm').addEventListener('submit', (e) => {
            // After results are shown, also show sensitivity section
            setTimeout(() => {
                const sensitivitySection = document.getElementById('sensitivitySection');
                if (currentResult) {
                    sensitivitySection.style.display = 'block';
                    resetSensitivity();
                }
            }, 100);
        });

        // Load saved properties on page load
        updateComparisonTable();
    </script>
</body>
</html>
