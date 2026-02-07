<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="UTF-8">

<title>CODE ARISE – C / C++ Compiler</title>



<style>

/\* ================= VARIABLES ================= \*/

:root{

&nbsp;   --accent:#6d28d9;

&nbsp;   --text:#022c22;

&nbsp;   --border:rgba(255,255,255,.35);

&nbsp;   --panel:rgba(255,255,255,.88);

}



body.dark{

&nbsp;   --text:#eaeaea;

&nbsp;   --border:#273043;

&nbsp;   --panel:#111821;

}



/\* ================= BASE ================= \*/

\*{box-sizing:border-box}



body{

&nbsp;   margin:0;

&nbsp;   font-family:"Segoe UI",system-ui,sans-serif;

&nbsp;   color:var(--text);



&nbsp;   /\* 🌿 PREMIUM TEAL / GOLD LIGHT MODE \*/

&nbsp;   background:

&nbsp;       radial-gradient(120% 80% at 10% 20%, rgba(16,185,129,.35), transparent 55%),

&nbsp;       radial-gradient(120% 80% at 90% 30%, rgba(20,184,166,.30), transparent 55%),

&nbsp;       radial-gradient(120% 80% at 30% 85%, rgba(34,197,94,.25), transparent 60%),

&nbsp;       linear-gradient(120deg,

&nbsp;           #022c22 0%,

&nbsp;           #064e3b 35%,

&nbsp;           #022c22 65%,

&nbsp;           #021b14 100%

&nbsp;       );



&nbsp;   background-size:200% 200%;

&nbsp;   animation:tealFlow 26s ease-in-out infinite;

&nbsp;   transition:.6s;

}



@keyframes tealFlow{

&nbsp;   0%{background-position:0% 50%}

&nbsp;   50%{background-position:100% 50%}

&nbsp;   100%{background-position:0% 50%}

}



body.dark{

&nbsp;   background:#0b0f14;

&nbsp;   animation:none;

}



/\* ================= LOADER ================= \*/

\#loader{

&nbsp;   position:fixed;

&nbsp;   inset:0;

&nbsp;   background:radial-gradient(circle,#2b0b4a,#050008);

&nbsp;   display:flex;

&nbsp;   align-items:center;

&nbsp;   justify-content:center;

&nbsp;   z-index:9999;

}



\#loaderText{

&nbsp;   font-size:3.8rem;

&nbsp;   letter-spacing:14px;

&nbsp;   color:#f5d0fe;

&nbsp;   text-shadow:

&nbsp;       0 0 45px #c084fc,

&nbsp;       0 0 120px #9333ea,

&nbsp;       0 0 200px #6d28d9;

&nbsp;   animation:glowFade .9s ease forwards;

}



@keyframes glowFade{

&nbsp;   0%{opacity:0;transform:scale(.9)}

&nbsp;   50%{opacity:1;transform:scale(1)}

&nbsp;   100%{opacity:0;transform:scale(1.1)}

}



/\* ================= MATRIX ================= \*/

\#matrix{

&nbsp;   position:fixed;

&nbsp;   inset:0;

&nbsp;   z-index:-5;

&nbsp;   opacity:0;

&nbsp;   transition:opacity 1s ease;

}

body.dark #matrix{opacity:1}



/\* ================= APP ================= \*/

.main{

&nbsp;   width:95%;

&nbsp;   max-width:1320px;

&nbsp;   margin:auto;

&nbsp;   padding:32px;

}



h1{

&nbsp;   text-align:center;

&nbsp;   font-size:3.2rem;

&nbsp;   letter-spacing:14px;

&nbsp;   margin-bottom:32px;

&nbsp;   color:#eafff5;

&nbsp;   text-shadow:0 10px 30px rgba(0,0,0,.35);

}



.top-bar{

&nbsp;   display:flex;

&nbsp;   justify-content:space-between;

&nbsp;   align-items:center;

&nbsp;   padding:18px 24px;

&nbsp;   border-radius:22px;

&nbsp;   background:var(--panel);

&nbsp;   backdrop-filter:blur(22px);

&nbsp;   border:1px solid var(--border);

&nbsp;   box-shadow:0 22px 50px rgba(0,0,0,.25);

}



.controls{display:flex;gap:14px}



select,button{

&nbsp;   background:transparent;

&nbsp;   color:var(--text);

&nbsp;   border:1px solid var(--accent);

&nbsp;   padding:10px 20px;

&nbsp;   border-radius:14px;

&nbsp;   cursor:pointer;

&nbsp;   font-size:.95rem;

&nbsp;   transition:.3s;

}



button:hover,select:hover{

&nbsp;   background:linear-gradient(135deg,#7c3aed,#a78bfa);

&nbsp;   color:white;

}



iframe{

&nbsp;   width:100%;

&nbsp;   height:520px;

&nbsp;   margin-top:30px;

&nbsp;   border-radius:22px;

&nbsp;   border:1px solid var(--border);

&nbsp;   background:black;

&nbsp;   box-shadow:0 25px 60px rgba(0,0,0,.35);

}



/\* ================= ERRORS ================= \*/

.errors{

&nbsp;   margin-top:30px;

&nbsp;   padding:24px 28px;

&nbsp;   border-radius:22px;

&nbsp;   background:var(--panel);

&nbsp;   backdrop-filter:blur(22px);

&nbsp;   border-left:6px solid var(--accent);

&nbsp;   border:1px solid var(--border);

&nbsp;   box-shadow:0 22px 50px rgba(0,0,0,.25);

}



.errors h3{

&nbsp;   margin-bottom:16px;

&nbsp;   letter-spacing:1px;

}



.errors ul{

&nbsp;   margin:0;

&nbsp;   padding-left:24px;

&nbsp;   font-family:Consolas, monospace;

&nbsp;   line-height:1.7;

&nbsp;   font-size:.95rem;

}

</style>

</head>



<body>



<!-- LOADER -->

<div id="loader">

&nbsp;   <div id="loaderText">CODE\&nbsp;ARISE</div>

</div>



<!-- MATRIX -->

<canvas id="matrix"></canvas>



<!-- APP -->

<div class="main" id="app" style="display:none">

&nbsp;   <h1>CODE ARISE</h1>



&nbsp;   <div class="top-bar">

&nbsp;       <div class="controls">

&nbsp;           <select onchange="switchCompiler(this.value)">

&nbsp;               <option value="cpp">C++</option>

&nbsp;               <option value="c">C</option>

&nbsp;           </select>

&nbsp;       </div>

&nbsp;       <button onclick="toggleTheme()">Toggle Theme</button>

&nbsp;   </div>



&nbsp;   <iframe id="compilerFrame" src="https://onecompiler.com/embed/cpp"></iframe>



&nbsp;   <div class="errors">

&nbsp;       <h3 id="errorTitle"></h3>

&nbsp;       <ul id="errorList"></ul>

&nbsp;   </div>

</div>



<script>

/\* ===== LOADER ===== \*/

setTimeout(()=>{

&nbsp;   document.getElementById("loader").style.display="none";

&nbsp;   document.getElementById("app").style.display="block";

},800);



/\* ===== MATRIX ===== \*/

const c=document.getElementById("matrix"),x=c.getContext("2d");

function resize(){c.width=innerWidth;c.height=innerHeight}

resize(); addEventListener("resize",resize);



const chars="01アカサタナABCDEFGHIJKLMNOPQRSTUVWXYZ";

const size=16,cols=Math.floor(innerWidth/size);

const drops=Array(cols).fill(1);



setInterval(()=>{

&nbsp;   if(!document.body.classList.contains("dark"))return;

&nbsp;   x.fillStyle="rgba(0,0,0,.05)";

&nbsp;   x.fillRect(0,0,c.width,c.height);

&nbsp;   x.fillStyle="#00ff88";

&nbsp;   x.font=size+"px monospace";

&nbsp;   drops.forEach((y,i)=>{

&nbsp;       const t=chars\[Math.random()\*chars.length|0];

&nbsp;       x.fillText(t,i\*size,y\*size);

&nbsp;       drops\[i]=y\*size>c.height\&\&Math.random()>.98?0:y+1;

&nbsp;   });

},35);



/\* ===== THEME ===== \*/

function toggleTheme(){

&nbsp;   document.body.classList.toggle("dark");

}



/\* ===== ERRORS ===== \*/

const errors={

&nbsp;   c:\[

&nbsp;       "Missing semicolon ( ; )",

&nbsp;       "Forgetting #include <stdio.h>",

&nbsp;       "Wrong format specifier in printf",

&nbsp;       "Using variables without declaration",

&nbsp;       "Array index out of bounds"

&nbsp;   ],

&nbsp;   cpp:\[

&nbsp;       "Missing semicolon ( ; )",

&nbsp;       "Forgetting #include <iostream>",

&nbsp;       "Using namespace std incorrectly",

&nbsp;       "Mixing C and C++ headers",

&nbsp;       "Mismatched braces { }"

&nbsp;   ]

};



function switchCompiler(lang){

&nbsp;   compilerFrame.src=lang==="c"

&nbsp;       ?"https://onecompiler.com/embed/c"

&nbsp;       :"https://onecompiler.com/embed/cpp";

&nbsp;   errorTitle.textContent=`\[ COMMON ${lang.toUpperCase()} ERRORS ]`;

&nbsp;   errorList.innerHTML="";

&nbsp;   errors\[lang].forEach(e=>{

&nbsp;       const li=document.createElement("li");

&nbsp;       li.textContent=e;

&nbsp;       errorList.appendChild(li);

&nbsp;   });

}



switchCompiler("cpp");

</script>



</body>

</html> 

