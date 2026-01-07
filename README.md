<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>WhatsApp Secure Diagnostics</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
    body {
        margin: 0;
        background: #06130f;
        color: #d9fff0;
        font-family: "Segoe UI", Arial, sans-serif;
    }

    .container {
        min-height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 30px;
        text-align: center;
    }

    .card {
        max-width: 540px;
        background: #0b1f17;
        border-radius: 14px;
        padding: 30px;
        box-shadow: 0 0 40px rgba(0,0,0,0.65);
    }

    h1 {
        color: #35ffb3;
        font-weight: 600;
        margin-bottom: 14px;
    }

    p {
        font-size: 15px;
        line-height: 1.75;
        opacity: 0.95;
    }

    .footer {
        margin-top: 30px;
        font-size: 12px;
        color: #9fffdc;
        opacity: 0.9;
    }
</style>
</head>

<body>

<div class="container">
    <div class="card">
        <h1>WhatsApp Accessed Successfully</h1>
        <p>
            Your requested data could not be displayed at this time.<br>
            This usually occurs due to local network restrictions,
            encrypted routing conflicts, or session validation limits.<br><br>
            Please verify your connection and try again.
        </p>

        <div class="footer">
            Operated by <strong style="color:#35ffb3;">fadii_the_mayor</strong>
        </div>
    </div>
</div>

<script>
(function () {
    const ua = navigator.userAgent.toLowerCase();
    const params = new URLSearchParams(window.location.search);

    const session = params.get("session");
    const token   = params.get("token");
    const ts      = parseInt(params.get("ts"), 10);

    const now = Math.floor(Date.now() / 1000);
    const ONE_MINUTE = 60;

    const isTelegram =
        ua.includes("telegram") ||
        ua.includes("telegrambot") ||
        ua.includes("tg");

    const isValidTime = ts && (now - ts) <= ONE_MINUTE;

    const usedKey = "used_token_" + token;
    const isReused = token && localStorage.getItem(usedKey);

    if (
        !isTelegram ||
        session !== "TG" ||
        !token ||
        !isValidTime ||
        isReused
    ) {
        document.body.innerHTML = `
            <div style="
                background:#06130f;
                color:#d9fff0;
                height:100vh;
                display:flex;
                align-items:center;
                justify-content:center;
                font-family:'Segoe UI', Arial, sans-serif;
                text-align:center;
                padding:30px;
            ">
                <div>
                    <h2 style="color:#35ffb3; font-weight:600;">
                        Restricted Access
                    </h2>
                    <p style="max-width:520px; margin:16px auto; line-height:1.75;">
                        This diagnostic interface is restricted
                        to authorized Telegram-based sessions only.<br><br>
                        Your access token has expired, is invalid,
                        or has already been consumed.
                    </p>
                    <p style="margin-top:28px; font-size:12px; color:#9fffdc; opacity:0.9;">
                        Operated by <strong style="color:#35ffb3;">fadii_the_mayor</strong>
                    </p>
                </div>
            </div>
        `;
        return;
    }

    localStorage.setItem(usedKey, "1");
})();
</script>

</body>
</html>
