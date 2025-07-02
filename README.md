<html>
<head>
  <title>Corn Basis Improvement if You Stop Selling Cash</title>
  <style>
    body {
      font-family: Arial;
      padding: 20px;
      max-width: 700px;
      margin: auto;
      text-align: center;
      font-size: 20px;
    }
    input[type=range] {
      width: 100%;
      -webkit-appearance: none;
      appearance: none;
      height: 8px;
      background: #ddd;
      border-radius: 4px;
      outline: none;
      cursor: pointer;
    }
    input[type=range]::-webkit-slider-thumb {
      -webkit-appearance: none;
      appearance: none;
      width: 20px;
      height: 20px;
      background: #4CAF50;
      border-radius: 50%;
      cursor: pointer;
      margin-top: -6px;
    }
    input[type=range]::-moz-range-thumb {
      width: 20px;
      height: 20px;
      background: #4CAF50;
      border-radius: 50%;
      cursor: pointer;
    }
    .section {
      margin-bottom: 20px;
      border: 2px solid #4CAF50;
      border-radius: 10px;
      padding: 15px;
      background-color: #f9f9f9;
    }
    .output {
      font-weight: bold;
      margin-top: 10px;
      border: 2px solid #2196F3;
      border-radius: 10px;
      padding: 15px;
      background-color: #eef6fd;
    }
    h2 {
      font-size: 28px;
    }
  </style>
</head>
<body>
  <h2>🌽 Corn Basis Improvement if You Stop Selling Cash</h2>

  <div class="section">
    <label>Basis Improvement ($/bushel): <span id="basisValue">0.80</span></label>
    <input type="range" id="basis" min="0.10" max="0.80" step="0.01" value="0.80">
  </div>

  <div class="section">
    <label>Yield per Acre (fixed): 200 bu/acre</label>
  </div>

  <div class="section">
    <label>Acres: <span id="acresValue">2,000</span></label>
    <input type="range" id="acres" min="250" max="2000" step="50" value="2000">
  </div>

  <div class="section output" id="perAcreValue"></div>
  <div class="section output" id="annualValue"></div>
  <div class="section output" id="fortyYearTotal"></div>
  <div class="section output" id="investedValue"></div>

  <script>
    const basisSlider = document.getElementById("basis");
    const acresSlider = document.getElementById("acres");
    const basisLabel = document.getElementById("basisValue");
    const acresLabel = document.getElementById("acresValue");
    const perAcreValueEl = document.getElementById("perAcreValue");
    const annualValueEl = document.getElementById("annualValue");
    const fortyYearEl = document.getElementById("fortyYearTotal");
    const investedEl = document.getElementById("investedValue");

    function formatCurrency(value) {
      return "$" + value.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 2 });
    }

    function updateValues() {
      const basis = parseFloat(basisSlider.value);
      const acres = parseInt(acresSlider.value);
      const yieldPerAcre = 200;
      const perAcreValue = basis * yieldPerAcre;
      const annualImprovement = perAcreValue * acres;

      // 40 year static total
      const fortyYearTotal = annualImprovement * 40;

      // Compound growth at 8% over 40 years with yearly contributions
      const rate = 0.08;
      const n = 40;
      const compoundFutureValue = annualImprovement * ((Math.pow(1 + rate, n) - 1) / rate);

      // Update display
      basisLabel.textContent = basis.toFixed(2);
      acresLabel.textContent = acres.toLocaleString();
      perAcreValueEl.innerHTML = `💡 Per Acre Basis Improvement Value: <span style="color:#9C27B0">${formatCurrency(perAcreValue)}</span>`;
      annualValueEl.innerHTML = `📈 Annual Basis Improvement Value: <span style="color:green">${formatCurrency(annualImprovement)}</span>`;
      fortyYearEl.innerHTML = `📅 40-Year Total (No Investing): <span style="color:blue">${formatCurrency(fortyYearTotal)}</span>`;
      investedEl.innerHTML = `💰 40-Year Compounded Investment (8%): <span style="color:darkgreen">${formatCurrency(compoundFutureValue)}</span>`;
    }

    basisSlider.addEventListener("input", updateValues);
    acresSlider.addEventListener("input", updateValues);

    // Initial calculation
    updateValues();
  </script>
</body>
</html>
