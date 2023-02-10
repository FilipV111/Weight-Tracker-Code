# Weight-Tracker-Code



<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weight Loss Tracker</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,500;0,600;0,700;0,800;0,900;1,100;1,200&display=swap" rel="stylesheet">
    <style>
        body
        {
        margin: 0px;
        padding: 0px;
        }
        #containerWeightDisplay, #containerWeightEntry {
            background: url("App Background.png");
            padding: 15px;
            font-family: 'Poppins', sans-serif;
            color: white;
            height: 1000px;
        }
        h1{
            left: 15px;
            top: 40px;

            font-family: 'Poppins';
            font-style: normal;
            font-weight: 700;
            font-size: 36px;
            line-height: 111%;
            /* or 40px */

            text-align: center;
        }

        #currentWeight, #enterWeight{
            width: 100%;
            height: 200px;
            left: 15px;
            top: 150px;
            text-align: center;
            background-color: #648381;
            box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
            border-radius: 15px;
        }

        h2, #outputDate{
            font-size: 2em;
            margin-top: 15px;
            margin-bottom: 10px;
            font-weight: 500;
        }

        .weight{
            font-size: 3em;
        }

        p {
            font-size: 1.25em;
            margin-top: 0px;
            font-weight: 500;
        }

        #containerWeightDisplay p{
            font-size: 1.25em;
            margin-top: -20px;
            font-weight: 500;
        }

        

        #weightRecords{
            text-align: center;
        }

        #btnRecord, #btnSave{
            width: 100%;
            background-color: #FFBF46;
            color: white;
            margin-top: 15px;
            height: 50px;
            box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
            font-size: 1.5em;
            font-weight: 500;
        }

        #newWeight{
            background: #F2F4FF;
            border-radius: 15px;
            height: 34px;
            font-size: 1.5em;
            font-weight: 700;
            width: 100px;
            text-align: center;
        }

        #weightHistory{
            text-align: center;
            font-weight: 700;
        }

        .weightHistoryCell {
            background-color: white;
            color: black;
            margin-top: 15px;
            height: 50px;
            box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
            font-size: 1.5em;
            font-weight: 500;
            border-radius: 15px;
            line-height: 50px;
            padding-left: 15px;
            padding-right: 15px;
        }

        .left {
            float: left;
        }

        .right {
            float: right;
        }
    </style>
</head>
<body>
    <div id="containerWeightDisplay">
        <h1>WEIGHT LOSS TRACKER</h1>
        <div id="currentWeight">
            <h2>CURRENT WEIGHT</h2>
            <div class="weight"><output id="mainWeight">XXX</output></div>
            <p>pounds</p>
        </div>
        <button id="btnRecord">RECORD YOUR WEIGHT</button>
        <div id="weightHistory">
            <h2>WEIGHT HISTORY</h2>
        </div>
    </div>
    <div id="containerWeightEntry">
        <h1>WEIGHT LOSS TRACKER</h1>
        <div id="weightRecords">
            <div id="enterWeight">
                <h2>ENTER WEIGHT</h2>
                <div id="weightEntry">
                    <input type="text" id="newWeight"/>
                </div>
                <p>pounds</p>
            </div>
            <div id="enterWeight">
                <h2>DATE</h2>
                <output id="outputDate"></output>
            </div>
            <button id="btnSave">SAVE</button>
    </div>
    <script>
        const containerWeightEntry = document.getElementById("containerWeightEntry");
        const containerWeightDisplay = document.getElementById("containerWeightDisplay");
        const btnRecord = document.getElementById("btnRecord");
        const outputDate = document.getElementById("outputDate");
        const btnSave = document.getElementById("btnSave");
        const newWeight = document.getElementById("newWeight");
        const weightHistory = document.getElementById("weightHistory");
        const mainWeight = document.getElementById("mainWeight");
        let weightData = [];
        

        btnRecord.onclick = () => {
            containerWeightDisplay.style.display = "none";
            containerWeightEntry.style.display = "block";
            newWeight.value = "";

        }

        btnSave.onclick = () => {
            containerWeightDisplay.style.display = "block";
            containerWeightEntry.style.display = "none";
            const theWeight = newWeight.value;
            const weight = new Object;
            weight.newWeight = theWeight;
            weight.date = getDate();
            weightData.push(weight);
            localStorage.setItem("weightHistory", JSON.stringify(weightData));
            weightHistory.innerHTML = "<h2>WEIGHT HISTORY</h2>";
            displayWeightHistory();
        }

        const getDate = () => {
            const dateObj = new Date();
            const month = dateObj.getUTCMonth() + 1; //months from 1-12
            const day = dateObj.getUTCDate();
            const year = dateObj.getUTCFullYear();

            const newDate = month + "." + day + "." + year;
            return newDate;
        }

        const displayWeightHistory = () => {
            let theWeights = localStorage.getItem("weightHistory");
            if(theWeights != null) {
                weightData = JSON.parse(theWeights);
                let x = 0;
                let lastWeight = 0;
                while (x < weightData.length){
                    const date = weightData[x].date;
                    const weight = weightData[x].newWeight;
                    lastWeight = weight;
                    const out = `<div class='weightHistoryCell'><span class='left'>${date}</span> <span class='right'>${weight}</span></div>`
                    weightHistory.innerHTML += out;
                    x++;
                } 
                mainWeight.innerHTML = lastWeight;
            } else {
                let lastWeight = "---";
                mainWeight.innerHTML = lastWeight;
            }
        }

        containerWeightEntry.style.display = "none";
        outputDate.innerHTML = getDate();
        displayWeightHistory();

    </script>
</body>
</html>


























































































