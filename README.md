# Youtube-Please
YT Pls

// ==UserScript==
// @name       youtube plz
// @namespace  http://use.i.E.your.homepage/
// @version    0.1
// @description  enter something useful
// @match      http://www.youtube.com/watch?*
// @match      https://www.youtube.com/watch?*
// @copyright  2012+, You
// ==/UserScript==

var spc = 35; // height in pixels of the youtube controls
var mma = 50; // minimum margin between the player and the page size

window.setWidth = function(nwidth, maxHeight) {
    var papi = document.getElementById("player-api");
    var rec = papi.getBoundingClientRect();
    var nheight = Math.min(maxHeight, (rec.height-spc)/rec.width*nwidth);

    papi.style.width = ''+(nheight*rec.width/(rec.height-spc)+spc)+'px';
    papi.style.height = ''+nwidth+'px';
}

window.setHeight = function(nheight, maxWidth) {
    var papi = document.getElementById("player-api");
    var rec = papi.getBoundingClientRect();
    var nwidth = Math.min(maxWidth, (rec.width/(rec.height-spc)*nheight));

    papi.style.height = ''+(nwidth*(rec.height-spc)/rec.width+spc)+'px';
    papi.style.width = ''+nwidth+'px';
}

onResize = function () {
    console.log('here!');
    setTimeout(function () {
    var papi = document.querySelector(".player:not(.watch-small) #player-api");
   	if (!papi)
        return;
    var rec = papi.getBoundingClientRect();

    var nheight = body.getBoundingClientRect().height-rec.top;
    var nwidth = body.getBoundingClientRect().width-rec.left;
    setHeight(nheight-mma-spc, nwidth-mma-spc);

    }, 600);
}

window.addEventListener('resize', onResize)
document.addEventListener('load', onResize);
