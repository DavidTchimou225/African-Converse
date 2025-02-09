# African-Converse
Convert African currencies and get the names of countries that use these currencies
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Convertisseur de Devises Africaines</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
    <style>
        body {
            background-color: #f5f5f5;
            font-family: Arial, sans-serif;
        }
        .container {
            max-width: 600px;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            margin-top: 50px;
        }
        h3 {
            text-align: center;
            color: #00796b;
        }
        .btn {
            width: 100%;
            background-color: #00796b;
        }
        #result {
            font-weight: bold;
            text-align: center;
            margin-top: 20px;
            color: #d32f2f;
        }
    </style>
</head>
<body>
    <div class="container">
        <h3>Convertisseur de Devises Africaines</h3>
        <div class="row">
            <div class="col s12 m6">
                <label for="fromCurrency">De :</label>
                <select id="fromCurrency" class="browser-default"></select>
            </div>
            <div class="col s12 m6">
                <label for="toCurrency">À :</label>
                <select id="toCurrency" class="browser-default"></select>
            </div>
        </div>
        <div class="row">
            <div class="col s12">
                <label for="amount">Montant :</label>
                <input type="number" id="amount" class="form-control" placeholder="Entrez le montant">
            </div>
        </div>
        <button class="btn waves-effect waves-light" id="convert">Convertir</button>
        <h5 id="result"></h5>
        <p id="currencyInfo" class="text-center"></p>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
    <script>
        const rates = {
            "XOF": { rate: 1, countries: ["Côte d'Ivoire", "Sénégal", "Mali", "Burkina Faso", "Togo", "Bénin", "Niger", "Guinée-Bissau"] },
            "XAF": { rate: 1.52, countries: ["Cameroun", "Gabon", "Congo", "Tchad", "Centrafrique", "Guinée Équatoriale"] },
            "NGN": { rate: 1.38, countries: ["Nigeria"] },
            "GHS": { rate: 70, countries: ["Ghana"] },
            "KES": { rate: 10, countries: ["Kenya"] }
        };

        $(document).ready(() => {
            Object.keys(rates).forEach(currency => {
                $("#fromCurrency, #toCurrency").append(new Option(currency, currency));
            });
        });

        $("#convert").click(() => {
            const from = $("#fromCurrency").val();
            const to = $("#toCurrency").val();
            const amount = parseFloat($("#amount").val());

            if (!amount || amount <= 0) {
                alert("Veuillez entrer un montant valide.");
                return;
            }

            const convertedAmount = (amount * rates[to].rate) / rates[from].rate;
            $("#result").text(`Montant converti : ${convertedAmount.toFixed(2)} ${to}`);
            $("#currencyInfo").text(`Pays utilisant ${to} : ${rates[to].countries.join(", ")}`);
        });
    </script>
</body>
</html>

