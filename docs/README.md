# SYL的笔记

<div id="oneyan"></div>

 <script>$(function () { $.get("https://api.ooopn.com/ciba/api.php", function (r) { if (r.code == 200) { console.log(r); $("#oneyan").html("<small>" + r.date + "</small><p>" + r.ciba + "</p><p>" + r["ciba-en"] + '</p><p><img src="' + r.imgurl + '" height="480" width="330"></img></p><p></p>').css("text-indent", "2em") } }, "json"); })</script>