---
layout: post
title:  Yahoo YT Cookie Header Generator
date:   2016-09-08
excerpt: "This is for internal usage. If you can see this, please contact me"
tag:
published: false
---

<p>Copy and paste the webpage here:</p>
<a href="https://login.yahoo.com/config/login_dump_cookies" target="_blank">https://login.yahoo.com/config/login_dump_cookies</a>

<textarea id="allCookies" rows="10" cols="80" onload="span();"></textarea>

<br />

<button type="button" onclick="parse()">
Get YT Cookie
</button> 

<p>Result:</p>

<textarea id="result" wrap="soft" rows="10" cols="80" readonly> 
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