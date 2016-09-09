---
layout: page
title: Yahoo YT Cookie Generator
sitemap: false
permalink: /yahoo-cookie.html
---
<p>Copy and paste the webpage here:</p>
<a href="https://login.yahoo.com/config/login_dump_cookies" target="_blank">https://login.yahoo.com/config/login_dump_cookies</a>

<textarea id="allCookies" rows="10" width="100%" onload="span();"></textarea>

<br />

<button type="button" onclick="parse()">
Get YT Cookie
</button> 

<p>Result:</p>

<textarea id="result" wrap="soft" rows="10" width="100%" readonly> 
</textarea>

<br />

<script>
function parse() {
    var input = document.getElementById("allCookies").value;
    var allCookiesObject = JSON.parse(input);
    var tRaw = allCookiesObject["Raw Cookies"]["T"]["Raw value"];
    var yRaw = allCookiesObject["Raw Cookies"]["Y"]["Raw value"];
    var result = "Cookie: T=" + tRaw + ";Y=" + yRaw; 
    document.getElementById("result").innerHTML = result;
}
</script>