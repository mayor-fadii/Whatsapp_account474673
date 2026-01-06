<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>WhatsApp Secure Access</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
    body{
        margin:0;
        padding:0;
        background:#020d0a;
        font-family:"Courier New", monospace;
        color:#00ff9c;
    }

    /* scanlines */
    body::before{
        content:"";
        position:fixed;
        inset:0;
        background:repeating-linear-gradient(
            to bottom,
            rgba(255,255,255,0.02),
            rgba(255,255,255,0.02) 1px,
            transparent 1px,
            transparent 3px
        );
        pointer-events:none;
    }

    .container{
        max-width:900px;
        margin:60px auto;
        padding:25px;
    }

    .heading{
        text-align:center;
        font-size:26px;
        font-weight:bold;
        margin-bottom:28px;
        text-shadow:0 0 15px #00ff9c;
    }

    /* OWNER BADGE — clearly visible */
    .owner-badge{
        text-align:center;
        margin-bottom:26px;
    }
    .owner-badge span{
        display:inline-block;
        padding:12px 26px;
        border:1px solid #00ff9c;
        border-radius:30px;
        color:#00ff9c;
        font-size:14px;
        letter-spacing:1px;
        text-shadow:0 0 14px #00ff9c;
        box-shadow:0 0 30px rgba(0,255,156,0.45);
        background:rgba(0,255,156,0.08);
    }

    .terminal{
        background:#010f0b;
        border:1px solid #00ff9c;
        border-radius:10px;
        padding:25px;
        box-shadow:0 0 35px rgba(0,255,156,0.25);
    }

    .terminal-header{
        font-size:14px;
        margin-bottom:12px;
        color:#6bffcb;
    }

    .status{
        font-size:14px;
        margin-bottom:18px;
        color:#9cffde;
    }

    .timer{
        font-weight:bold;
        color:#e8fff6;
        text-shadow:0 0 12px #00ff9c;
    }

    .data-area{
        border:1px dashed #00ff9c;
        border-radius:6px;
        padding:24px;
        text-align:center;
        background:rgba(0,255,156,0.05);
        min-height:80px;
    }

    .blink{ animation:blink 1s infinite; }
    @keyframes blink{
        0%{opacity:1}
        50%{opacity:0}
        100%{opacity:1}
    }

    .footer{
        margin-top:35px;
        text-align:center;
        font-size:12px;
        color:#7dffcf;
        opacity:0.75;
    }
</style>
</head>

<body>

<div class="container">

    <div class="heading">
        Your Accessed Data is here... 👇🏻
    </div>

    <div class="owner-badge">
        <span>AUTHORIZED OPERATOR • fadii_the_mayor</span>
    </div>

    <div class="terminal">
        <div class="terminal-header">
            root@whatsapp-node:/secure/session <span class="blink">█</span>
        </div>

        <div class="status" id="statusText">
            Fetching WhatsApp data… Please wait
            (<span class="timer" id="timer">10:00</span>)
        </div>

        <div class="data-area" id="dataBox">
            Initializing end‑to‑end encrypted channel…
        </div>
    </div>

    <div class="footer">
        WHATSAPP SECURE INTERFACE • TRACE SHIELD ACTIVE
    </div>

</div>

<script>
    // 10 minutes = 600 seconds
    let timeLeft = 600;

    const timerEl = document.getElementById("timer");
    const dataBox = document.getElementById("dataBox");
    const statusText = document.getElementById("statusText");

    function formatTime(sec){
        const m = Math.floor(sec / 60);
        const s = sec % 60;
        return `${String(m).padStart(2,'0')}:${String(s).padStart(2,'0')}`;
    }

    timerEl.textContent = formatTime(timeLeft);

    const countdown = setInterval(()=>{
        timeLeft--;
        timerEl.textContent = formatTime(timeLeft);

        if(timeLeft <= 0){
            clearInterval(countdown);
            statusText.textContent = "Data retrieval failed";
            dataBox.innerHTML = `
                Your data is not showing due to your network connection.<br>
                Kindly check your connection and try again.
            `;
        }
    },1000);
</script>

</body>
</html>
