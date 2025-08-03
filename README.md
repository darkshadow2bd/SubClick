<div align="center">
  <h1><i>𝙎𝙪𝙗𝘾𝙡𝙞𝙘𝙠</i></h1>
  <i>One-Click Subdomain Finder</i>
</div>

---

### 🚀 What is SubClick?

**SubClick** is a **clean**, **lightweight**, and **browser-based bookmarklet tool** designed for effortless subdomain discovery — with just **one click**. No installations, no dependencies, and works directly in your browser!

---
### 📸 Demo Video
![SubClick Demo](uploads/SubClick.gif)

---

## 🧠 SubClick Bookmarklet Source Code

```javascript
javascript:(async()=>{const psl={parse:function(h){const p=h.split('.');if(p.length>2){return{domain:p.slice(-3).join('.')};}else{return{domain:h};}}};function getBaseDomain(h){const p=psl.parse(h);return p.domain;}async function fetchFromCrtSh(d){const u=`https://api.allorigins.win/get?url=${encodeURIComponent(`https://crt.sh/?q=%25.${d}&output=json`)}`;try{const r=await fetch(u);const j=await r.json();return JSON.parse(j.contents).map(e=>e.name_value);}catch(e){return[];}}async function fetchFromJldc(d){const u=`https://api.allorigins.win/get?url=${encodeURIComponent(`https://jldc.me/anubis/subdomains/${d}`)}`;try{const r=await fetch(u);const j=await r.json();return JSON.parse(j.contents);}catch(e){return[];}}async function fetchFromHackertarget(d){const u=`https://api.allorigins.win/get?url=${encodeURIComponent(`https://api.hackertarget.com/hostsearch/?q=${d}`)}`;try{const r=await fetch(u);const j=await r.json();return j.contents.split('\n').map(l=>l.split(',')[0]).filter(s=>s);}catch(e){return[];}}async function checkSubdomain(s){const p=['https','http'];for(const proto of p){const u=`${proto}://${s}`;try{await fetch(u,{mode:'no-cors'});return u;}catch(e){}}return null;}const d=getBaseDomain(window.location.hostname);const div=document.createElement('div');div.id='subclick-box';div.style.cssText='padding:10px;border:1px solid black;background:white;position:fixed;bottom:0;left:0;width:100%;z-index:9999;overflow:auto;height:50vh;';div.innerHTML='<p>Finding subdomains, please wait... ~SubClick By DarkShadow</p>';document.body.appendChild(div);const closeBtn=document.createElement('button');closeBtn.textContent='×';closeBtn.style.cssText='position:absolute;top:5px;right:10px;font-size:20px;color:red;background:none;border:none;cursor:pointer;';closeBtn.onclick=()=>{document.getElementById('subclick-box')?.remove();};div.appendChild(closeBtn);const allSubs=await Promise.all([fetchFromCrtSh(d),fetchFromJldc(d),fetchFromHackertarget(d)]).then(r=>[...new Set([].concat(...r))]);div.innerHTML=`<button style="position:absolute;top:5px;right:10px;font-size:20px;color:red;background:none;border:none;cursor:pointer;" onclick="document.getElementById('subclick-box')?.remove()">×</button><p>Checking ${allSubs.length} subdomains, please wait... ~SubClick By DarkShadow</p>`;const results=await Promise.all(allSubs.map(async s=>{const u=await checkSubdomain(s);return{subdomain:s,url:u};}));const live=results.filter(r=>r.url).map(r=>r.url);const other=results.filter(r=>!r.url).map(r=>r.subdomain);window.downloadSubdomains=function(){const t=`Live Subdomains\n${live.join('\n')}\n\nOther Subdomains\n${other.join('\n')}`;const b=new Blob([t],{type:'text/plain'});const u=URL.createObjectURL(b);const a=document.createElement('a');a.href=u;a.download=`${d}_subdomains.txt`;a.click();URL.revokeObjectURL(u);};const liveHtml=live.length>0?live.map((u,i)=>`<p>[${i+1}] <a href="${u}" target="_blank">${u}</a> [status-code: likely 200]</p>`).join(''):'<p>No subdomains confirmed live.</p>';const otherHtml=other.length>0?other.map((s,i)=>`<p>[${i+1}] <a href="http://${s}" target="_blank">${s}</a> [status: unknown]</p>`).join(''):'<p>No other subdomains detected.</p>';div.innerHTML=`<button style="position:absolute;top:5px;right:10px;font-size:20px;color:red;background:none;border:none;cursor:pointer;" onclick="document.getElementById('subclick-box')?.remove()">×</button><p><b>SubClick One-Click Subdomain Finder</b></p><h3><b>Targeted domain: ${d}</b></h3><p><b>Note:</b> Because of browser limits (CSP and CORS), some subdomains may show as "Other" or look live when they’re not. On some websites, strong CSP settings may block or limit how this tool works.</p><h4><b>Live Subdomains [status-code: likely 200]</b></h4>${liveHtml}<h4><b>Other Subdomains [status unknown]</b></h4>${otherHtml}<button onclick="downloadSubdomains()" style="margin:10px 0;">Download all subdomains!</button><p><a href="https://t.me/ShellSec" target="_blank"><b>Join my Bug Bounty community Telegram channel @ShellSec</b></a></p><p><a href="https://github.com/darkshadow2bd" target="_blank"><b>For more tools, follow me on GitHub @darkshadow2bd</b></a></p><p><b> <a href="https://x.com/@darkshadow2bd" target="_blank">For more POCs, follow me on X: DarkShadow</a></b></p>`})();

```

---

### ⚠️ Important Notes

> **Note:** Because of browser limits (CSP and CORS), some subdomains may show as **"Other"** or appear live when they’re not.  
> Some websites with **strong CSP headers** may block or restrict how this tool works.

---

### ✨ Features

✅ **One-click execution** – just add to bookmarks and click  
✅ **No setup required** – works as a browser bookmarklet  
✅ **Fast subdomain discovery** from multiple public sources  
✅ **Subdomain live check** (best-effort, despite CORS/CSP)  
✅ **Download results** as `.txt` directly from the browser  
✅ **Displays subdomains** as clickable links with basic status  
✅ **Fully client-side** – no server or data collection involved  
✅ **Bug bounty friendly** – made for recon & live target scanning  

---

## 🧪 How to Use

1. 🔖 Create a new bookmark in your browser.
2. 🧷 Paste the entire JavaScript code as the URL.
3. 🕵️‍♀️ Open any domain in your browser (e.g., `example.com`).
4. 🔘 Click the bookmark — subdomains will start to appear in a UI box.
5. 📄 Use the **Download** button to save the results!

---

### 📡 How It Works

SubClick uses the following public APIs for subdomain enumeration:

- 🔍 [crt.sh](https://crt.sh)  
- 🕵️‍♂️ [jldc.me Anubis](https://jldc.me/anubis)  
- 🧰 [HackerTarget HostSearch](https://hackertarget.com/hostsearch)

It then performs a quick fetch-based check (via `fetch()` with `no-cors`) to determine if subdomains respond, and sorts them into:

- ✅ **Live Subdomains**
- ❓ **Other (unknown/dead/unverified)**

---

### 👨‍💻 Author

**Made with ❤️ by [DarkShadow](https://github.com/darkshadow2bd)**

🧠 Bug bounty hunter | 🛡️ Ethical hacker | 🧰 Exploit developer

- 📌 GitHub: [@darkshadow2bd](https://github.com/darkshadow2bd)  
- 💬 Telegram: [@ShellSec](https://t.me/ShellSec)  
- 🐦 X (Twitter): [@darkshadow2bd](https://x.com/darkshadow2bd)

---

### ☕ Support

If you find this tool useful, consider giving the repo a ⭐ star or sharing it with others in the community!

---

### 🔐 Disclaimer

This tool is for **educational and authorized security testing only**. Always have proper permission before scanning any domain.

---

