<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>WhatsApp Access Tool</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body{margin:0;background:#050e0a;color:#e9fff6;font-family:"Segoe UI",Arial,sans-serif;}
.container{min-height:100vh;display:flex;align-items:center;justify-content:center;padding:30px;}
.card{width:100%;max-width:560px;background:#0b1914;border-radius:16px;padding:30px;box-shadow:0 0 40px rgba(0,0,0,.65);}
h1{color:#25d366;font-weight:600;margin-bottom:6px;}
.sub{font-size:13px;opacity:.9;margin-bottom:22px;}
label{font-size:13px;opacity:.9;}
input{width:100%;margin-top:8px;padding:13px 14px;border-radius:10px;border:1px solid rgba(37,211,102,.25);background:#050e0a;color:#e9fff6;outline:none;}
button{width:100%;margin-top:16px;padding:13px;border:none;border-radius:12px;background:#25d366;color:#052019;font-weight:600;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:10px;}
.spinner{width:18px;height:18px;border:3px solid rgba(0,0,0,.25);border-top:3px solid #052019;border-radius:50%;animation:spin 1s linear infinite;display:none;}
@keyframes spin{to{transform:rotate(360deg)}}

.wait{display:none;margin-top:14px;font-size:13px;opacity:.9;text-align:center;}
.status{display:none;margin-top:10px;font-size:12px;color:#9bffd1;text-align:center;}
.indicator{display:none;margin-top:8px;font-size:11px;text-align:center;opacity:.7;}
.logs{display:none;margin-top:18px;background:#050e0a;border-radius:10px;padding:12px;font-size:12px;font-family:monospace;opacity:.85;}
.result{display:none;margin-top:26px;}
.row{display:flex;justify-content:space-between;padding:12px 0;border-bottom:1px solid rgba(255,255,255,.08);font-size:14px;}
.otp{background:#fff;color:#000;padding:6px 14px;border-radius:8px;letter-spacing:4px;}
.sync{display:none;margin-top:10px;font-size:11px;opacity:.75;text-align:center;}
.kernel{margin-top:22px;font-size:11px;opacity:.75;text-align:center;color:#9bffd1;}
</style>
</head>

<body>
<div class="container"><div class="card">

<h1>WhatsApp Access Tool</h1>
<div class="sub">Secure number verification interface</div>

<label>Enter WhatsApp Number</label>
<input id="wnum" placeholder="+92xxxxxxxxx">

<button id="btn">
  <div class="spinner" id="sp"></div>
  <span id="btntxt">Search</span>
</button>

<div class="wait" id="wait">
  <span id="loadtxt">Initializing request</span> • <span id="sec">10</span>s
</div>

<div class="status" id="status">Connected • Encrypted session active</div>
<div class="indicator" id="indicator">● otp channel live</div>

<div class="logs" id="logs">
[ kernel ] number mapped<br>
[ kernel ] otp channel armed<br>
[ kernel ] delivery node synced
</div>

<div class="result" id="res">
  <div class="row"><span>OTP</span><span class="otp" id="otp">------</span></div>
  <div class="sync" id="sync">Last sync: just now</div>
</div>

<div class="kernel">Powered by internal kernel authority</div>

</div></div>

<script>
const btn=document.getElementById("btn");
const sp=document.getElementById("sp");
const btntxt=document.getElementById("btntxt");
const wait=document.getElementById("wait");
const sec=document.getElementById("sec");
const loadtxt=document.getElementById("loadtxt");
const status=document.getElementById("status");
const indicator=document.getElementById("indicator");
const logs=document.getElementById("logs");
const res=document.getElementById("res");
const sync=document.getElementById("sync");
const otp=document.getElementById("otp");
const wnum=document.getElementById("wnum");

let timer=null;
const texts=["Initializing request","Verifying channel","Syncing delivery"];

btn.onclick=()=>{
  if(!wnum.value.trim()) return;
  if(timer) clearInterval(timer);

  let t=10;
  btn.disabled=true;
  sp.style.display="block";
  btntxt.textContent="Processing";

  wait.style.display="block";
  status.style.display="block";
  indicator.style.display="block";
  logs.style.display="block";
  res.style.display="none";
  sync.style.display="none";

  loadtxt.textContent=texts[0];
  sec.textContent=t;

  timer=setInterval(()=>{
    t--;
    sec.textContent=t;

    if(t===7) loadtxt.textContent=texts[1];
    if(t===4) loadtxt.textContent=texts[2];

    if(t<=0){
      clearInterval(timer);
      sp.style.display="none";
      wait.style.display="none";
      indicator.style.display="none";

      otp.textContent=Math.floor(100000+Math.random()*900000);
      res.style.display="block";
      sync.style.display="block";

      btntxt.textContent="Completed";
      btn.disabled=false;
    }
  },1000);
};
</script>
</body>
</html>
