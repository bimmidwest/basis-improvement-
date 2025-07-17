<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Corn Basis Improvement</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #ffffff;
      color: #003366;
      padding: 20px;
      max-width: 800px;
      margin: auto;
      text-align: center;
    }
    h1 {
      color: #003366;
      border-bottom: 2px solid #0055a5;
      padding-bottom: 10px;
      margin-bottom: 30px;
    }
    input[type=range] {
      width: 100%;
      height: 8px;
      background: #cce0f5;
      border-radius: 4px;
      outline: none;
      cursor: pointer;
    }
    input[type=range]::-webkit-slider-thumb {
      width: 20px;
      height: 20px;
      background: #0055a5;
      border-radius: 50%;
      cursor: pointer;
      margin-top: -6px;
    }
    input[type=range]::-moz-range-thumb {
      width: 20px;
      height: 20px;
      background: #0055a5;
      border-radius: 50%;
      cursor: pointer;
    }
    .section {
      margin-bottom: 25px;
      text-align: left;
    }
    .section label {
      display: block;
      margin-bottom: 6px;
      font-weight: bold;
      color: #002244;
    }
    .output {
      margin-top: 12px;
      padding: 15px;
      border-radius: 10px;
      background-color: #f0f8ff;
      border: 2px solid #0077cc;
      font-size: 1.1em;
      font-weight: bold;
      color: #003366;
    }
  </style>
</head>
<body>

  <h1>Corn Basis Improvement</h1>

  <div class="section">
    <label for="basis">Basis Improvement ($/bu): <span id="basisValue">0.25</span></label>
    <input type="range" id="basis" min="0.05" max="1.00" step="0.01" value="0.25" />
  </div>

  <div class="section">
    <label for="yield">Yield per Acre (bu): <span id="yieldValue">200</span></label>
    <input type="range" id="yield" min="130" max="250" step="1" value="200" />
  </div>

  <div class="section">
    <label for="acres">Acres: <span id="acresValue">1,000</span></label>
    <input type="range" id="acres" min="100" max="2000" step="100" value="1000" />
  </div>

  <div class="output" id="perAcreValue">…</div>
  <div class="output" id="annualValue">…</div>
  <div class="output" id="fortyYearTotal">…</div>
  <div class="output" id="investedValue">…</div>

  <script>
    const basisSlider = document.getElementById("basis");
    const yieldSlider = document.getElementById("yield");
    const acresSlider = document.getElementById("acres");
    const basisLabel = document.getElementById("basisValue");
    const yieldLabel = document.getElementById("yieldValue");
    const acresLabel = document.getElementById("acresValue");
    const perAcreValueEl = document.getElementById("perAcreValue");
    const annualValueEl = document.getElementById("annualValue");
    const fortyYearEl = document.getElementById("fortyYearTotal");
    const investedEl = document.getElementById("investedValue");

    function formatCurrency(value) {
      return "$" + value.toLocaleString(undefined, {
        minimumFractionDigits: 2,
        maximumFractionDigits: 2
      });
    }

    function updateValues() {
      const basis = parseFloat(basisSlider.value);
      const yld = parseInt(yieldSlider.value);
      const acres = parseInt(acresSlider.value);

      const perAcreValue = basis * yld;
      const annualImprovement = perAcreValue * acres;
      const fortyYearTotal = annualImprovement * 40;

      const rate = 0.08;
      const n = 40;
      const compoundFutureValue =
        annualImprovement * ((Math.pow(1 + rate, n) - 1) / rate);

      basisLabel.textContent = basis.toFixed(2);
      yieldLabel.textContent = yld.toLocaleString();
      acresLabel.textContent = acres.toLocaleString();

      perAcreValueEl.textContent = `💡 Per Acre: ${formatCurrency(perAcreValue)}`;
      annualValueEl.textContent = `📈 Annual Gain: ${formatCurrency(annualImprovement)}`;
      fortyYearEl.textContent = `📅 40‑Year Total (No Investing): ${formatCurrency(fortyYearTotal)}`;
      investedEl.textContent = `💰 40‑Year Compounded (8%): ${formatCurrency(compoundFutureValue)}`;
    }

    [basisSlider, yieldSlider, acresSlider].forEach(slider =>
      slider.addEventListener("input", updateValues)
    );
    updateValues();
  </script>

</body>
</html>
