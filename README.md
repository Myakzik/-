# Конвертер Валют
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Конвертер валют | Курсы валют онлайн</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #1e2a3a, #0f1724);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .glass-card {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(12px);
            border-radius: 32px;
            padding: 30px 28px;
            width: 100%;
            max-width: 550px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
            border: 1px solid rgba(255, 255, 255, 0.2);
            transition: all 0.2s ease;
        }

        h1 {
            text-align: center;
            color: #f0f3fa;
            font-weight: 600;
            font-size: 1.9rem;
            margin-bottom: 10px;
            letter-spacing: -0.5px;
        }

        .sub {
            text-align: center;
            color: #a0b3d9;
            margin-bottom: 28px;
            font-size: 0.85rem;
            border-bottom: 1px dashed rgba(255,255,255,0.2);
            display: inline-block;
            width: 100%;
            padding-bottom: 8px;
        }

        .converter-panel {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 24px;
            padding: 20px;
            margin-bottom: 28px;
        }

        .currency-row {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
            margin-bottom: 22px;
            align-items: flex-end;
        }

        .currency-box {
            flex: 1;
            min-width: 130px;
        }

        label {
            display: block;
            font-size: 0.75rem;
            text-transform: uppercase;
            font-weight: 600;
            letter-spacing: 1px;
            color: #bbd1ff;
            margin-bottom: 6px;
        }

        select, input {
            width: 100%;
            padding: 12px 14px;
            background: #1e2a36;
            border: 1px solid #3f4e62;
            border-radius: 20px;
            font-size: 1rem;
            color: white;
            outline: none;
            transition: all 0.2s;
        }

        select:focus, input:focus {
            border-color: #5d9eff;
            box-shadow: 0 0 6px rgba(93, 158, 255, 0.5);
        }

        input {
            background: #0f1a22;
        }

        input::placeholder {
            color: #7f8c9a;
        }

        .swap-btn {
            background: #2c3e4e;
            border: none;
            color: white;
            font-size: 1.5rem;
            cursor: pointer;
            padding: 8px 16px;
            border-radius: 40px;
            margin-top: 24px;
            transition: 0.2s;
            font-weight: bold;
        }

        .swap-btn:hover {
            background: #3e5a6c;
            transform: scale(1.02);
        }

        .result-area {
            background: #08121c;
            border-radius: 28px;
            padding: 16px 20px;
            text-align: center;
            margin: 20px 0;
        }

        .result-value {
            font-size: 2.2rem;
            font-weight: 800;
            color: #d4f1ff;
            word-break: break-word;
        }

        .rate-info {
            font-size: 0.8rem;
            color: #8ea1bd;
            margin-top: 8px;
        }

        .update-btn {
            background: #2c5f8a;
            border: none;
            padding: 10px 20px;
            border-radius: 40px;
            color: white;
            font-weight: bold;
            cursor: pointer;
            width: 100%;
            margin-bottom: 20px;
            transition: 0.2s;
            font-size: 0.9rem;
        }

        .update-btn:hover {
            background: #1e4a6e;
        }

        .history-box {
            background: rgba(0, 0, 0, 0.4);
            border-radius: 24px;
            padding: 12px 16px;
        }

        .history-header {
            display: flex;
            justify-content: space-between;
            align-items: baseline;
            margin-bottom: 12px;
            flex-wrap: wrap;
        }

        .history-header h3 {
            color: #eef5ff;
            font-size: 1.2rem;
        }

        .clear-history {
            background: #902e3a;
            border: none;
            padding: 6px 14px;
            border-radius: 50px;
            color: white;
            cursor: pointer;
            font-size: 0.7rem;
            font-weight: bold;
        }

        .history-list {
            max-height: 220px;
            overflow-y: auto;
            padding-right: 5px;
        }

        .history-item {
            background: #0e1a24;
            margin: 8px 0;
            padding: 10px 14px;
            border-radius: 18px;
            display: flex;
            justify-content: space-between;
            font-size: 0.85rem;
            color: #dce6f5;
            border-left: 3px solid #5d9eff;
        }

        .history-date {
            font-size: 0.7rem;
            color: #8da1c2;
        }

        ::-webkit-scrollbar {
            width: 5px;
        }

        ::-webkit-scrollbar-track {
            background: #1c2a36;
            border-radius: 10px;
        }

        ::-webkit-scrollbar-thumb {
            background: #5d9eff;
            border-radius: 10px;
        }

        footer {
            text-align: center;
            font-size: 0.7rem;
            color: #6a7c99;
            margin-top: 20px;
        }

        @media (max-width: 480px) {
            .glass-card {
                padding: 18px;
            }
            .result-value {
                font-size: 1.6rem;
            }
        }
    </style>
</head>
<body>
<div class="glass-card">
    <h1>💱 Конвертер валют</h1>
    <div class="sub">актуальные курсы • история</div>

    <div class="converter-panel">
        <div class="currency-row">
            <div class="currency-box">
                <label>Из валюты</label>
                <select id="fromCurrency">
                    <option value="USD">🇺🇸 USD - Доллар США</option>
                    <option value="EUR">🇪🇺 EUR - Евро</option>
                    <option value="RUB">🇷🇺 RUB - Российский рубль</option>
                    <option value="KZT">🇰🇿 KZT - Казахстанский тенге</option>
                    <option value="GBP">🇬🇧 GBP - Фунт стерлингов</option>
                    <option value="CNY">🇨🇳 CNY - Китайский юань</option>
                </select>
            </div>
            <div class="currency-box">
                <label>В валюту</label>
                <select id="toCurrency">
                    <option value="EUR">🇪🇺 EUR - Евро</option>
                    <option value="USD">🇺🇸 USD - Доллар США</option>
                    <option value="RUB">🇷🇺 RUB - Российский рубль</option>
                    <option value="KZT">🇰🇿 KZT - Казахстанский тенге</option>
                    <option value="GBP">🇬🇧 GBP - Фунт стерлингов</option>
                    <option value="CNY">🇨🇳 CNY - Китайский юань</option>
                </select>
            </div>
        </div>

        <div class="currency-row">
            <div class="currency-box">
                <label>Сумма</label>
                <input type="number" id="amount" value="100" step="any" placeholder="Введите сумму">
            </div>
            <div class="currency-box">
                <label>Результат</label>
                <input type="text" id="result" readonly placeholder="0.00" style="background:#0a1118; font-weight:600;">
            </div>
        </div>

        <div style="display: flex; gap: 10px; margin-top: 8px;">
            <button id="convertBtn" class="update-btn" style="background:#3b6e4b; margin-bottom:0;">💲 Конвертировать</button>
            <button id="swapCurrenciesBtn" class="swap-btn" style="margin-top:0;">⇄</button>
        </div>
    </div>

    <div class="result-area">
        <div class="result-value" id="liveResult">—</div>
        <div class="rate-info" id="rateMessage">Курс: загружается...</div>
    </div>

    <button id="fetchRatesBtn" class="update-btn">🔄 Обновить курсы (через API)</button>

    <div class="history-box">
        <div class="history-header">
            <h3>📜 История конвертаций</h3>
            <button id="clearHistoryBtn" class="clear-history">Очистить историю</button>
        </div>
        <div id="historyList" class="history-list">
            <div style="text-align:center; padding: 18px; color:#788aa8;">Здесь будут сохранённые операции</div>
        </div>
    </div>
    <footer>Курсы от exchangerate-api (mock + backup fallback)</footer>
</div>

<script>
    // -------- СТАТИЧЕСКИЕ ФИКС КУРСЫ (запасной вариант) ----------
    const FALLBACK_RATES = {
        USD: 1,
        EUR: 0.92,
        RUB: 92.5,
        KZT: 460.2,
        GBP: 0.79,
        CNY: 7.25
    };

    let currentRates = { ...FALLBACK_RATES };   // храним текущие курсы (относительно USD)
    let lastUpdateTime = null;

    // -------- РАБОТА С LOCALSTORAGE (история) ----------
    let history = [];

    function loadHistoryFromStorage() {
        const stored = localStorage.getItem("currency_converter_history");
        if (stored) {
            try {
                history = JSON.parse(stored);
                if (!Array.isArray(history)) history = [];
            } catch(e) { history = []; }
        } else {
            history = [];
        }
        renderHistory();
    }

    function saveHistoryToStorage() {
        localStorage.setItem("currency_converter_history", JSON.stringify(history.slice(-20))); // храним максимум 20
    }

    function addToHistory(fromCurr, toCurr, amount, converted, rateUsed) {
        const now = new Date();
        const timeStr = now.toLocaleString();
        history.unshift({   // новые записи сверху
            from: fromCurr,
            to: toCurr,
            amount: amount,
            result: converted,
            rate: rateUsed,
            date: timeStr
        });
        if (history.length > 20) history.pop();
        saveHistoryToStorage();
        renderHistory();
    }

    function renderHistory() {
        const container = document.getElementById("historyList");
        if (!container) return;
        if (history.length === 0) {
            container.innerHTML = '<div style="text-align:center; padding: 18px; color:#788aa8;">📭 История пуста. Сделайте конвертацию</div>';
            return;
        }
        let html = '';
        for (let item of history) {
            html += `
                <div class="history-item">
                    <div>
                        <strong>${item.amount} ${item.from}</strong> → <strong>${item.result.toFixed(4)} ${item.to}</strong><br>
                        <span class="history-date">Курс: 1 ${item.from} = ${item.rate.toFixed(6)} ${item.to}</span>
                    </div>
                    <div class="history-date">${item.date}</div>
                </div>
            `;
        }
        container.innerHTML = html;
    }

    function clearHistory() {
        history = [];
        saveHistoryToStorage();
        renderHistory();
    }

    // ---------- КОНВЕРТАЦИЯ ----------
    // курсы хранятся относительно USD: например currentRates["EUR"] = сколько EUR за 1 USD
    function convertCurrency(amount, fromCurr, toCurr, rates) {
        if (!rates[fromCurr] || !rates[toCurr]) return null;
        // сначала переводим в USD, затем в целевую валюту
        const amountInUSD = amount / rates[fromCurr];
        const result = amountInUSD * rates[toCurr];
        return result;
    }

    function performConversionAndSave() {
        const fromCurr = document.getElementById("fromCurrency").value;
        const toCurr = document.getElementById("toCurrency").value;
        let amount = parseFloat(document.getElementById("amount").value);
        if (isNaN(amount) || amount <= 0) {
            amount = 0;
            document.getElementById("amount").value = 0;
        }

        if (!currentRates[fromCurr] || !currentRates[toCurr]) {
            document.getElementById("liveResult").innerText = "Ошибка курсов";
            document.getElementById("result").value = "Ошибка";
            return;
        }

        const converted = convertCurrency(amount, fromCurr, toCurr, currentRates);
        if (converted === null) return;

        const formatted = converted.toFixed(6);
        document.getElementById("result").value = formatted;
        document.getElementById("liveResult").innerHTML = `${amount} ${fromCurr} = <span style="color:#6bf06b;">${Number(converted).toFixed(4)} ${toCurr}</span>`;

        // курс 1 from -> to
        const rateOne = converted / amount;
        document.getElementById("rateMessage").innerHTML = `🔁 1 ${fromCurr} ≈ ${rateOne.toFixed(6)} ${toCurr}  (данные: ${lastUpdateTime ? lastUpdateTime : 'фикс-курсы'})`;

        // Добавляем в историю
        if (amount > 0) {
            addToHistory(fromCurr, toCurr, amount, converted, rateOne);
        }
    }

    // ---------- ЗАГРУЗКА КУРСОВ ЧЕРЕЗ API (exchangerate-api.com) ----------
    async function fetchExchangeRates() {
        const apiKey = "37d7f8a6f12e4fc5a7c7920fe14fedf8";   // публичный демо-ключ (exchangerate-api)
        // API: https://v6.exchangerate-api.com/v6/API_KEY/latest/USD
        const url = `https://v6.exchangerate-api.com/v6/${apiKey}/latest/USD`;
        
        try {
            document.getElementById("rateMessage").innerHTML = "⏳ Загрузка курсов с API...";
            const response = await fetch(url);
            if (!response.ok) throw new Error("API ответил ошибкой");
            const data = await response.json();
            if (data.result === "success" && data.conversion_rates) {
                const newRates = { ...data.conversion_rates };
                // оставляем только нужные нам валюты: USD, EUR, RUB, KZT, GBP, CNY
                const allowed = ["USD", "EUR", "RUB", "KZT", "GBP", "CNY"];
                const filtered = {};
                for (let curr of allowed) {
                    if (newRates[curr]) {
                        filtered[curr] = newRates[curr];
                    } else {
                        // fallback внутри
                        filtered[curr] = FALLBACK_RATES[curr];
                    }
                }
                // Убедимся, что USD = 1 (по API он и есть 1)
                filtered["USD"] = 1;
                currentRates = filtered;
                const nowDate = new Date().toLocaleTimeString();
                lastUpdateTime = nowDate;
                document.getElementById("rateMessage").innerHTML = `✅ Курсы обновлены (${nowDate}) | 1 USD = ${currentRates.EUR} EUR / ${currentRates.RUB} RUB`;
                performConversionAndSave();  // сразу обновить результат
            } else {
                throw new Error("Неверный ответ API");
            }
        } catch (error) {
            console.warn("Ошибка API, используем фиксированные курсы", error);
            currentRates = { ...FALLBACK_RATES };
            lastUpdateTime = "фикс-курсы (офлайн)";
            document.getElementById("rateMessage").innerHTML = "⚠️ Ошибка API, используются локальные курсы. Нажмите ещё раз для проверки соединения";
            performConversionAndSave();
        }
    }

    // Функция для принудительной смены валют местами
    function swapCurrencies() {
        const fromSelect = document.getElementById("fromCurrency");
        const toSelect = document.getElementById("toCurrency");
        const temp = fromSelect.value;
        fromSelect.value = toSelect.value;
        toSelect.value = temp;
        performConversionAndSave();
    }

    // ----------------- инициализация и обработчики -----------------
    document.addEventListener("DOMContentLoaded", () => {
        loadHistoryFromStorage();
        
        // первоначальная попытка подгрузить курсы (если интернет есть)
        fetchExchangeRates().then(() => {
            performConversionAndSave();
        }).catch(() => {
            currentRates = { ...FALLBACK_RATES };
            lastUpdateTime = "локальные";
            document.getElementById("rateMessage").innerHTML = "💾 Работаем с запасными курсами (обновите через кнопку)";
            performConversionAndSave();
        });

        const convertBtn = document.getElementById("convertBtn");
        const swapBtn = document.getElementById("swapCurrenciesBtn");
        const fetchBtn = document.getElementById("fetchRatesBtn");
        const clearHistoryBtn = document.getElementById("clearHistoryBtn");
        const amountInput = document.getElementById("amount");
        const fromCurrSel = document.getElementById("fromCurrency");
        const toCurrSel = document.getElementById("toCurrency");

        convertBtn.addEventListener("click", () => performConversionAndSave());
        swapBtn.addEventListener("click", () => swapCurrencies());
        fetchBtn.addEventListener("click", () => fetchExchangeRates());
        clearHistoryBtn.addEventListener("click", () => clearHistory());
        
        amountInput.addEventListener("input", () => performConversionAndSave());
        fromCurrSel.addEventListener("change", () => performConversionAndSave());
        toCurrSel.addEventListener("change", () => performConversionAndSave());
    });
</script>
</body>
</html>
