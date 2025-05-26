# Nec_risk_by_FM
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Калькулятор риска НЭК</title>
    <style>
        body { font-family: Arial, sans-serif; background-color: #f0f4f7; padding: 20px; }
        h2 { color: #333; text-align: center; }
        .container { background: white; padding: 20px; border-radius: 10px; max-width: 400px; margin: auto; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
        label { display: block; margin-top: 12px; }
        input { width: 100%; padding: 10px; margin-top: 5px; border-radius: 5px; border: 1px solid #ccc; }
        button { margin-top: 20px; padding: 12px; width: 100%; background-color: #0066cc; color: white; border: none; border-radius: 5px; font-size: 16px; }
        .result { margin-top: 20px; font-size: 18px; font-weight: bold; text-align: center; }
    </style>
</head>
<body>
    <div class="container">
        <h2>Калькулятор риска НЭК</h2>
        
        <label for="weight">Вес при рождении (г):</label>
        <input type="number" id="weight">

        <label for="gestage">Гестационный возраст (нед):</label>
        <input type="number" id="gestage">

        <label for="crp">CRP/Альбумин:</label>
        <input type="number" step="0.1" id="crp">

        <label for="calprotectin">Кальпротектин (мкг/г):</label>
        <input type="number" id="calprotectin">

        <label for="fabp">I-FABP (нг/мл):</label>
        <input type="number" id="fabp">

        <button onclick="calculateRisk()">Рассчитать риск</button>

        <div class="result" id="result"></div>
    </div>

    <script>
        function calculateRisk() {
            let weight = parseFloat(document.getElementById('weight').value);
            let gestage = parseFloat(document.getElementById('gestage').value);
            let crp = parseFloat(document.getElementById('crp').value);
            let calprotectin = parseFloat(document.getElementById('calprotectin').value);
            let fabp = parseFloat(document.getElementById('fabp').value);

            let risk = 0;
            if (gestage < 30) risk += 10;
            if (weight < 1500) risk += 10;
            if (crp > 2) risk += 10;
            if (calprotectin > 200) risk += 10;
            if (fabp > 2.5) risk += 10;

            let resultText = `Риск НЭК: ${risk}%\n`;
            if (risk < 10) resultText += "Низкий риск. Стандартное наблюдение.";
            else if (risk < 30) resultText += "Умеренный риск. Наблюдение, контроль FABP и маркеров воспаления.";
            else resultText += "Высокий риск. Срочная диагностика, отмена питания, мониторинг FABP и кальпротектина.";

            document.getElementById('result').innerText = resultText;
        }
    </script>
</body>
</html>
