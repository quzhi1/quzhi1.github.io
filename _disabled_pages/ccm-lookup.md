---
layout: page
title: Yahoo CCM Look Up Tool
sitemap: false
permalink: /ccm-lookup.html
---

uuid:<br>
<input type="text" name="uuid" id="uuidInput" size="50"><br>

Source:<br>
<input type="radio" name="source" value="japi" checked> japi<br>
<input type="radio" name="source" value="contentOs"> content-yql<br>

Env:<br>
<input type="radio" name="env" value="prod" checked> prod<br>
<input type="radio" name="env" value="nonprod"> nonprod<br>

Args:<br>
<input type="checkbox" name="arg" value="ignore_constraints=embargo,expires,deleted" checked> show deleted<br>
<input type="checkbox" name="arg" value="critical_read=true"> critical read<br>
<input type="checkbox" name="arg" value="facets=self"> "self" facet only<br>

Num of revisions:<br>
<input type="radio" name="numRev" value="0" checked> Non<br>
<input type="radio" name="numRev" value="1"> 1<br>
<input type="radio" name="numRev" value="2"> 2<br>
<input type="radio" name="numRev" value="3"> 3<br>

<button type="button" onclick="showUrl()">
Show url
</button>

<p id='showUrl'></p>

<button type="button" onclick="openPage()">
Open
</button>

<script>
function generateUrl() {
    var uuid = $('#uuidInput').val();
        
        var japiProdBase = "http://japi1.global.media.gq1.yahoo.com:4080/content/v1/object/";
        var japiNonprodBase = "http://japi1.plt1.global.media.gq1.yahoo.com:4080/content/v1/object/";
        var contentProdBase = "http://os-content-boson-yql.media.yahoo.com/v1/content/";
        var contentNonprodBase = "http://os-content-boson-yql.trunk.development.manhattan.gq1.yahoo.com:4080/v1/content/";
        var base;
        var source = $('input[name=source]').filter(':checked').val();
        var env = $('input[name=env]').filter(':checked').val();
        if (source == "japi" && env == "prod") {
            base = japiProdBase;
        } else if (source == "japi" && env == "nonprod") {
            base = japiNonprodBase;
        } else if (source == "contentOs" && env == "prod") {
            base = contentProdBase;
        } else if (source == "japi" && env == "nonprod") {
            base = contentNonprodBase;
        }
        
        var args = '';
        var checkedArgs = $('input[name=arg]').filter(':checked');
        for (var i = 0; i < checkedArgs.length; i++) {
            args += checkedArgs.get(i).value + '&';
        }
        var numRev = $('input[name=numRev]').filter(':checked').val();
        if (numRev != 0) {
            args += 'numrevisions=' + numRev + '&';
        }
        if (args != '') {
            args = '?' + args.substring(0, args.length - 1); 
        }
        
        var url = base + uuid + args;
        if (uuid == '') {
            alert('uuid cannot be null');
            return null;
        }
        return url;
}

function openPage() {
    var url = generateUrl();
    if (url != null) {
        var win = window.open(url, '_blank');
        win.focus();
    }
}

function showUrl() {
    var url = generateUrl();
    if (url != null) {
        $('#showUrl').text(url);
    }
}
</script>