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
    color:#e9fff6;
    font-family:"Segoe UI",Arial,sans-serif;
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
    padding:30px;
    box-shadow:0 0 40px rgba(0,0,0,.65);
}
h1{
    color:#25d366;
    font-weight:600;
    margin-bottom:6px;
}
.sub{
    font-size:13px;
    opacity:.9;
    margin-bottom:22px;
}
label{
    font-size:13px;
    opacity:.9;
}
input{
    width:100%;
    margin-top:8px;
    padding:13px 14px;
    border-radius:10px;
    border:1px solid rgba(37,211,102,.25);
    background:#050e0a;
    color:#e9fff6;
    outline:none;
}
button{
    width:100%;
    margin-top:16px;
    padding:13px;
    border:none;
    border-radius:12px;
    background:#25d366;
    color:#052019;
    font-weight:600;
    cursor:pointer;
    display:flex;
    align-items:center;
    justify-content:center;
    gap:10px;
}
.spinner{
    width:18px;
    height:18px;
    border:3px solid rgba(0,0,0,.25);
    border-top:3px solid #052019;
    border-radius:50%;
    animation:spin 1s linear infinite;
    display:none;
}
@keyframes spin{to{transform:rotate(360deg)}}

.wait{
    display:none;
    margin-top:14px;
    font-size:13px;
    opacity:.9;
    text-align:center;
}

.result{
    display:none;
    margin-top:26px;
}
.row{
    display:flex;
    justify-content:space-between;
    padding:12px 0;
    border-bottom:1px solid rgba(255,255,255,.08);
    font-size:14px;
}
.dots{
    letter-spacing:4px;
    opacity:.85;
}
.footer{
    margin-top:26px;
    font-size:12px;
    opacity:.9;
    text-align:center;
    color:#9bffd1;
}
</style>
</head>

<body>
<div class="container">
<div class="card">

<h1>WhatsApp Access Tool</h1>
<div class="sub">Secure number verification interface</div>

<label>Enter WhatsApp Number</label>
<input id="wnum" placeholder="+92xxxxxxxxx">

<button id="btn" onclick="start()">
    <div class="spinner" id="sp"></div>
    <span id="btntxt">Search</span>
</button>

<div class="wait" id="wait">
    Please wait <span id="sec">10</span> seconds
</div>

<div class="result" id="res">
    <div class="row"><span>OTP</span><span class="dots">••••••</span></div>
</div>

<div class="footer">
    Operated by <strong style="color:#25d366;">fadii_the_mayor</strong>
</div>

</div>
</div>

<script>
let t=10, timer;
function start(){
    if(!wnum.value.trim()) return;
    btn.disabled=true;
    sp.style.display="block";
    btntxt.textContent="Processing";
    wait.style.display="block";
    sec.textContent=t;

    timer=setInterval(()=>{
        t--;
        sec.textContent=t;
        if(t<=0){
            clearInterval(timer);
            sp.style.display="none";
            wait.style.display="none";
            res.style.display="block";
        }
    },1000);
}
</script>
</body>
</html>
