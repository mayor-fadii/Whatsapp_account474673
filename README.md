<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>WhatsApp Access Tool</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
    body{
        margin:0;
        background:#050e0a;
        color:#d7fff1;
        font-family:"Segoe UI", Arial, sans-serif;
    }

    .container{
        min-height:100vh;
        display:flex;
        align-items:center;
        justify-content:center;
        padding:30px;
    }

    .card{
        width:100%;
        max-width:560px;
        background:#0b1914;
        border-radius:16px;
        padding:32px;
        box-shadow:0 0 45px rgba(0,0,0,.65);
    }

    h1{
        color:#25d366;
        font-weight:600;
        margin-bottom:8px;
    }

    .sub{
        font-size:13px;
        opacity:.9;
        margin-bottom:22px;
        line-height:1.6;
    }

    label{
        font-size:13px;
        opacity:.9;
    }

    input{
        width:100%;
        margin-top:8px;
        padding:13px 15px;
        border-radius:10px;
        border:none;
        outline:none;
        background:#050e0a;
        color:#d7fff1;
        font-size:14px;
        border:1px solid rgba(37,211,102,.25);
    }

    input::placeholder{
        color:#9beac1;
        opacity:.75;
    }

    button{
        width:100%;
        margin-top:16px;
        padding:13px;
        border-radius:12px;
        border:none;
        background:#25d366;
        color:#062017;
        font-weight:600;
        font-size:14px;
        cursor:pointer;
        transition:.2s;
    }

    button:hover{
        opacity:.9;
    }

    .processing{
        display:none;
        margin-top:22px;
        font-size:14px;
        opacity:.9;
        text-align:center;
    }

    /* ===== RESULT ===== */
    .result{
        display:none;
        margin-top:28px;
        text-align:center;
    }

    .result-title{
        font-size:18px;
        color:#25d366;
        font-weight:600;
        margin-bottom:18px;
    }

    .blur-emoji{
        filter:blur(5px);
        margin-left:6px;
    }

    .emoji-wrapper{
        display:flex;
        align-items:center;
        justify-content:center;
        gap:20px;
        margin-bottom:20px;
    }

    .arrow{
        font-size:28px;
        cursor:pointer;
        user-select:none;
        color:#25d366;
        transition:.2s;
    }

    .arrow:hover{
        transform:scale(1.15);
        opacity:.85;
    }

    .emoji-box{
        width:160px;
        height:160px;
        border-radius:22px;
        background:#07130f;
        display:flex;
        align-items:center;
        justify-content:center;
        font-size:64px;
        border:1px solid rgba(37,211,102,.22);
        box-shadow:0 0 28px rgba(0,0,0,.55);
        user-select:none;
    }

    .success{
        font-size:14px;
        margin-top:10px;
        opacity:.95;
    }

    .footer{
        margin-top:30px;
        font-size:12px;
        color:#9bffd1;
        opacity:.9;
        text-align:center;
    }
</style>
</head>

<body>

<div class="container">
<div class="card">

    <h1>WhatsApp Access Tool</h1>
    <div class="sub">
        Secure interface for WhatsApp account data inspection.
    </div>

    <label>Enter WhatsApp Number / Username</label>
    <input type="text" id="number" placeholder="+92xxxxxxxxx" autocomplete="off">

    <button onclick="startSearch()">Search</button>

    <div class="processing" id="processing">
        Establishing secure channel… please wait
    </div>

    <div class="result" id="result">

        <div class="result-title">
            Your Accessed Data is here
            <span class="blur-emoji">📲</span>
        </div>

        <div class="emoji-wrapper">
            <div class="arrow" onclick="prevEmoji()">‹</div>
            <div class="emoji-box" id="emojiBox">📡</div>
            <div class="arrow" onclick="nextEmoji()">›</div>
        </div>

        <div class="success">
            Accessed successfully.
        </div>

    </div>

    <div class="footer">
        Operated by <strong style="color:#25d366;">fadii_the_mayor</strong>
    </div>

</div>
</div>

<script>
const emojis = ["📡","💬","📲","🗂️","🧠","🔐","⚙️","🛰️"];
let index = 0;

function startSearch(){
    const val = document.getElementById("number").value.trim();
    if(!val) return;

    document.getElementById("result").style.display = "none";
    document.getElementById("processing").style.display = "block";

    setTimeout(() => {
        document.getElementById("processing").style.display = "none";
        document.getElementById("result").style.display = "block";
    }, 5000);
}

function nextEmoji(){
    index = (index + 1) % emojis.length;
    document.getElementById("emojiBox").textContent = emojis[index];
}

function prevEmoji(){
    index = (index - 1 + emojis.length) % emojis.length;
    document.getElementById("emojiBox").textContent = emojis[index];
}
</script>

</body>
</html>
