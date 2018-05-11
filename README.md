# 13---Web-Scraping-and-Document-Databases




## Step 1 Scraping

This task will use BeautifulSoup,Pandas, and Requests and Splinter to scraping Mars related information 


```python
# Dependencies
from bs4 import BeautifulSoup as bs
import requests
import pymongo
import pandas as pd
from splinter import Browser
from splinter.exceptions import ElementDoesNotExist
import time

```


```python
 # Initialize PyMongo to work with MongoDBs
conn = 'mongodb://localhost:27017'
client = pymongo.MongoClient(conn)
```

#### NASA Mars News

We will scrape the lastest News Title and Paragragh Text from NASA Mars News Site(https://mars.nasa.gov/news/).


```python
# URL of page to be scraped
url1 = 'https://mars.nasa.gov/news/?page=0&per_page=40&order=publish_date+desc%2Ccreated_at+desc&search=&category=19%2C165%2C184%2C204&blank_scope=Latest'
# Retrieve page with the requests module
response = requests.get(url1)
```


```python
# Create a Beautiful Soup object
soup1 = bs(response.text, "html5lib")
type(soup1)
```




    bs4.BeautifulSoup




```python
 # Print formatted version of the soup
print(soup1.prettify())
```

    <!DOCTYPE html>
    <!--[if lte IE 9]> <p class="browsehappy">You are using an <strong>outdated</strong> browser. Please <a href="http://browsehappy.com/">upgrade your browser</a> to improve your experience.</p> <![endif]-->
    <html lang="en" xml:lang="en" xmlns="http://www.w3.org/1999/xhtml">
     <head>
      <meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
      <!-- Always force latest IE rendering engine or request Chrome Frame -->
      <meta content="IE=edge,chrome=1" http-equiv="X-UA-Compatible"/>
      <script type="text/javascript">
       window.NREUM||(NREUM={});NREUM.info={"beacon":"bam.nr-data.net","errorBeacon":"bam.nr-data.net","licenseKey":"5e33925808","applicationID":"59562082","transactionName":"JVcPR0MLWApSRU1eAQVVEhxSC1oSUlkWbBMHXwRAHhdcCUA=","queueTime":0,"applicationTime":212,"agent":""}
      </script>
      <script type="text/javascript">
       (window.NREUM||(NREUM={})).loader_config={xpid:"VQcPUlZTDxAFXVRUBQEPVA=="};window.NREUM||(NREUM={}),__nr_require=function(t,n,e){function r(e){if(!n[e]){var o=n[e]={exports:{}};t[e][0].call(o.exports,function(n){var o=t[e][1][n];return r(o||n)},o,o.exports)}return n[e].exports}if("function"==typeof __nr_require)return __nr_require;for(var o=0;o<e.length;o++)r(e[o]);return r}({1:[function(t,n,e){function r(t){try{s.console&&console.log(t)}catch(n){}}var o,i=t("ee"),a=t(15),s={};try{o=localStorage.getItem("__nr_flags").split(","),console&&"function"==typeof console.log&&(s.console=!0,o.indexOf("dev")!==-1&&(s.dev=!0),o.indexOf("nr_dev")!==-1&&(s.nrDev=!0))}catch(c){}s.nrDev&&i.on("internal-error",function(t){r(t.stack)}),s.dev&&i.on("fn-err",function(t,n,e){r(e.stack)}),s.dev&&(r("NR AGENT IN DEVELOPMENT MODE"),r("flags: "+a(s,function(t,n){return t}).join(", ")))},{}],2:[function(t,n,e){function r(t,n,e,r,s){try{p?p-=1:o(s||new UncaughtException(t,n,e),!0)}catch(f){try{i("ierr",[f,c.now(),!0])}catch(d){}}return"function"==typeof u&&u.apply(this,a(arguments))}function UncaughtException(t,n,e){this.message=t||"Uncaught error with no additional information",this.sourceURL=n,this.line=e}function o(t,n){var e=n?null:c.now();i("err",[t,e])}var i=t("handle"),a=t(16),s=t("ee"),c=t("loader"),f=t("gos"),u=window.onerror,d=!1,l="nr@seenError",p=0;c.features.err=!0,t(1),window.onerror=r;try{throw new Error}catch(h){"stack"in h&&(t(8),t(7),"addEventListener"in window&&t(5),c.xhrWrappable&&t(9),d=!0)}s.on("fn-start",function(t,n,e){d&&(p+=1)}),s.on("fn-err",function(t,n,e){d&&!e[l]&&(f(e,l,function(){return!0}),this.thrown=!0,o(e))}),s.on("fn-end",function(){d&&!this.thrown&&p>0&&(p-=1)}),s.on("internal-error",function(t){i("ierr",[t,c.now(),!0])})},{}],3:[function(t,n,e){t("loader").features.ins=!0},{}],4:[function(t,n,e){function r(t){}if(window.performance&&window.performance.timing&&window.performance.getEntriesByType){var o=t("ee"),i=t("handle"),a=t(8),s=t(7),c="learResourceTimings",f="addEventListener",u="resourcetimingbufferfull",d="bstResource",l="resource",p="-start",h="-end",m="fn"+p,w="fn"+h,v="bstTimer",y="pushState",g=t("loader");g.features.stn=!0,t(6);var b=NREUM.o.EV;o.on(m,function(t,n){var e=t[0];e instanceof b&&(this.bstStart=g.now())}),o.on(w,function(t,n){var e=t[0];e instanceof b&&i("bst",[e,n,this.bstStart,g.now()])}),a.on(m,function(t,n,e){this.bstStart=g.now(),this.bstType=e}),a.on(w,function(t,n){i(v,[n,this.bstStart,g.now(),this.bstType])}),s.on(m,function(){this.bstStart=g.now()}),s.on(w,function(t,n){i(v,[n,this.bstStart,g.now(),"requestAnimationFrame"])}),o.on(y+p,function(t){this.time=g.now(),this.startPath=location.pathname+location.hash}),o.on(y+h,function(t){i("bstHist",[location.pathname+location.hash,this.startPath,this.time])}),f in window.performance&&(window.performance["c"+c]?window.performance[f](u,function(t){i(d,[window.performance.getEntriesByType(l)]),window.performance["c"+c]()},!1):window.performance[f]("webkit"+u,function(t){i(d,[window.performance.getEntriesByType(l)]),window.performance["webkitC"+c]()},!1)),document[f]("scroll",r,{passive:!0}),document[f]("keypress",r,!1),document[f]("click",r,!1)}},{}],5:[function(t,n,e){function r(t){for(var n=t;n&&!n.hasOwnProperty(u);)n=Object.getPrototypeOf(n);n&&o(n)}function o(t){s.inPlace(t,[u,d],"-",i)}function i(t,n){return t[1]}var a=t("ee").get("events"),s=t(18)(a,!0),c=t("gos"),f=XMLHttpRequest,u="addEventListener",d="removeEventListener";n.exports=a,"getPrototypeOf"in Object?(r(document),r(window),r(f.prototype)):f.prototype.hasOwnProperty(u)&&(o(window),o(f.prototype)),a.on(u+"-start",function(t,n){var e=t[1],r=c(e,"nr@wrapped",function(){function t(){if("function"==typeof e.handleEvent)return e.handleEvent.apply(e,arguments)}var n={object:t,"function":e}[typeof e];return n?s(n,"fn-",null,n.name||"anonymous"):e});this.wrapped=t[1]=r}),a.on(d+"-start",function(t){t[1]=this.wrapped||t[1]})},{}],6:[function(t,n,e){var r=t("ee").get("history"),o=t(18)(r);n.exports=r,o.inPlace(window.history,["pushState","replaceState"],"-")},{}],7:[function(t,n,e){var r=t("ee").get("raf"),o=t(18)(r),i="equestAnimationFrame";n.exports=r,o.inPlace(window,["r"+i,"mozR"+i,"webkitR"+i,"msR"+i],"raf-"),r.on("raf-start",function(t){t[0]=o(t[0],"fn-")})},{}],8:[function(t,n,e){function r(t,n,e){t[0]=a(t[0],"fn-",null,e)}function o(t,n,e){this.method=e,this.timerDuration=isNaN(t[1])?0:+t[1],t[0]=a(t[0],"fn-",this,e)}var i=t("ee").get("timer"),a=t(18)(i),s="setTimeout",c="setInterval",f="clearTimeout",u="-start",d="-";n.exports=i,a.inPlace(window,[s,"setImmediate"],s+d),a.inPlace(window,[c],c+d),a.inPlace(window,[f,"clearImmediate"],f+d),i.on(c+u,r),i.on(s+u,o)},{}],9:[function(t,n,e){function r(t,n){d.inPlace(n,["onreadystatechange"],"fn-",s)}function o(){var t=this,n=u.context(t);t.readyState>3&&!n.resolved&&(n.resolved=!0,u.emit("xhr-resolved",[],t)),d.inPlace(t,y,"fn-",s)}function i(t){g.push(t),h&&(x?x.then(a):w?w(a):(E=-E,O.data=E))}function a(){for(var t=0;t<g.length;t++)r([],g[t]);g.length&&(g=[])}function s(t,n){return n}function c(t,n){for(var e in t)n[e]=t[e];return n}t(5);var f=t("ee"),u=f.get("xhr"),d=t(18)(u),l=NREUM.o,p=l.XHR,h=l.MO,m=l.PR,w=l.SI,v="readystatechange",y=["onload","onerror","onabort","onloadstart","onloadend","onprogress","ontimeout"],g=[];n.exports=u;var b=window.XMLHttpRequest=function(t){var n=new p(t);try{u.emit("new-xhr",[n],n),n.addEventListener(v,o,!1)}catch(e){try{u.emit("internal-error",[e])}catch(r){}}return n};if(c(p,b),b.prototype=p.prototype,d.inPlace(b.prototype,["open","send"],"-xhr-",s),u.on("send-xhr-start",function(t,n){r(t,n),i(n)}),u.on("open-xhr-start",r),h){var x=m&&m.resolve();if(!w&&!m){var E=1,O=document.createTextNode(E);new h(a).observe(O,{characterData:!0})}}else f.on("fn-end",function(t){t[0]&&t[0].type===v||a()})},{}],10:[function(t,n,e){function r(t){var n=this.params,e=this.metrics;if(!this.ended){this.ended=!0;for(var r=0;r<d;r++)t.removeEventListener(u[r],this.listener,!1);if(!n.aborted){if(e.duration=a.now()-this.startTime,4===t.readyState){n.status=t.status;var i=o(t,this.lastSize);if(i&&(e.rxSize=i),this.sameOrigin){var c=t.getResponseHeader("X-NewRelic-App-Data");c&&(n.cat=c.split(", ").pop())}}else n.status=0;e.cbTime=this.cbTime,f.emit("xhr-done",[t],t),s("xhr",[n,e,this.startTime])}}}function o(t,n){var e=t.responseType;if("json"===e&&null!==n)return n;var r="arraybuffer"===e||"blob"===e||"json"===e?t.response:t.responseText;return h(r)}function i(t,n){var e=c(n),r=t.params;r.host=e.hostname+":"+e.port,r.pathname=e.pathname,t.sameOrigin=e.sameOrigin}var a=t("loader");if(a.xhrWrappable){var s=t("handle"),c=t(11),f=t("ee"),u=["load","error","abort","timeout"],d=u.length,l=t("id"),p=t(14),h=t(13),m=window.XMLHttpRequest;a.features.xhr=!0,t(9),f.on("new-xhr",function(t){var n=this;n.totalCbs=0,n.called=0,n.cbTime=0,n.end=r,n.ended=!1,n.xhrGuids={},n.lastSize=null,p&&(p>34||p<10)||window.opera||t.addEventListener("progress",function(t){n.lastSize=t.loaded},!1)}),f.on("open-xhr-start",function(t){this.params={method:t[0]},i(this,t[1]),this.metrics={}}),f.on("open-xhr-end",function(t,n){"loader_config"in NREUM&&"xpid"in NREUM.loader_config&&this.sameOrigin&&n.setRequestHeader("X-NewRelic-ID",NREUM.loader_config.xpid)}),f.on("send-xhr-start",function(t,n){var e=this.metrics,r=t[0],o=this;if(e&&r){var i=h(r);i&&(e.txSize=i)}this.startTime=a.now(),this.listener=function(t){try{"abort"===t.type&&(o.params.aborted=!0),("load"!==t.type||o.called===o.totalCbs&&(o.onloadCalled||"function"!=typeof n.onload))&&o.end(n)}catch(e){try{f.emit("internal-error",[e])}catch(r){}}};for(var s=0;s<d;s++)n.addEventListener(u[s],this.listener,!1)}),f.on("xhr-cb-time",function(t,n,e){this.cbTime+=t,n?this.onloadCalled=!0:this.called+=1,this.called!==this.totalCbs||!this.onloadCalled&&"function"==typeof e.onload||this.end(e)}),f.on("xhr-load-added",function(t,n){var e=""+l(t)+!!n;this.xhrGuids&&!this.xhrGuids[e]&&(this.xhrGuids[e]=!0,this.totalCbs+=1)}),f.on("xhr-load-removed",function(t,n){var e=""+l(t)+!!n;this.xhrGuids&&this.xhrGuids[e]&&(delete this.xhrGuids[e],this.totalCbs-=1)}),f.on("addEventListener-end",function(t,n){n instanceof m&&"load"===t[0]&&f.emit("xhr-load-added",[t[1],t[2]],n)}),f.on("removeEventListener-end",function(t,n){n instanceof m&&"load"===t[0]&&f.emit("xhr-load-removed",[t[1],t[2]],n)}),f.on("fn-start",function(t,n,e){n instanceof m&&("onload"===e&&(this.onload=!0),("load"===(t[0]&&t[0].type)||this.onload)&&(this.xhrCbStart=a.now()))}),f.on("fn-end",function(t,n){this.xhrCbStart&&f.emit("xhr-cb-time",[a.now()-this.xhrCbStart,this.onload,n],n)})}},{}],11:[function(t,n,e){n.exports=function(t){var n=document.createElement("a"),e=window.location,r={};n.href=t,r.port=n.port;var o=n.href.split("://");!r.port&&o[1]&&(r.port=o[1].split("/")[0].split("@").pop().split(":")[1]),r.port&&"0"!==r.port||(r.port="https"===o[0]?"443":"80"),r.hostname=n.hostname||e.hostname,r.pathname=n.pathname,r.protocol=o[0],"/"!==r.pathname.charAt(0)&&(r.pathname="/"+r.pathname);var i=!n.protocol||":"===n.protocol||n.protocol===e.protocol,a=n.hostname===document.domain&&n.port===e.port;return r.sameOrigin=i&&(!n.hostname||a),r}},{}],12:[function(t,n,e){function r(){}function o(t,n,e){return function(){return i(t,[f.now()].concat(s(arguments)),n?null:this,e),n?void 0:this}}var i=t("handle"),a=t(15),s=t(16),c=t("ee").get("tracer"),f=t("loader"),u=NREUM;"undefined"==typeof window.newrelic&&(newrelic=u);var d=["setPageViewName","setCustomAttribute","setErrorHandler","finished","addToTrace","inlineHit","addRelease"],l="api-",p=l+"ixn-";a(d,function(t,n){u[n]=o(l+n,!0,"api")}),u.addPageAction=o(l+"addPageAction",!0),u.setCurrentRouteName=o(l+"routeName",!0),n.exports=newrelic,u.interaction=function(){return(new r).get()};var h=r.prototype={createTracer:function(t,n){var e={},r=this,o="function"==typeof n;return i(p+"tracer",[f.now(),t,e],r),function(){if(c.emit((o?"":"no-")+"fn-start",[f.now(),r,o],e),o)try{return n.apply(this,arguments)}catch(t){throw c.emit("fn-err",[arguments,this,t],e),t}finally{c.emit("fn-end",[f.now()],e)}}}};a("setName,setAttribute,save,ignore,onEnd,getContext,end,get".split(","),function(t,n){h[n]=o(p+n)}),newrelic.noticeError=function(t){"string"==typeof t&&(t=new Error(t)),i("err",[t,f.now()])}},{}],13:[function(t,n,e){n.exports=function(t){if("string"==typeof t&&t.length)return t.length;if("object"==typeof t){if("undefined"!=typeof ArrayBuffer&&t instanceof ArrayBuffer&&t.byteLength)return t.byteLength;if("undefined"!=typeof Blob&&t instanceof Blob&&t.size)return t.size;if(!("undefined"!=typeof FormData&&t instanceof FormData))try{return JSON.stringify(t).length}catch(n){return}}}},{}],14:[function(t,n,e){var r=0,o=navigator.userAgent.match(/Firefox[\/\s](\d+\.\d+)/);o&&(r=+o[1]),n.exports=r},{}],15:[function(t,n,e){function r(t,n){var e=[],r="",i=0;for(r in t)o.call(t,r)&&(e[i]=n(r,t[r]),i+=1);return e}var o=Object.prototype.hasOwnProperty;n.exports=r},{}],16:[function(t,n,e){function r(t,n,e){n||(n=0),"undefined"==typeof e&&(e=t?t.length:0);for(var r=-1,o=e-n||0,i=Array(o<0?0:o);++r<o;)i[r]=t[n+r];return i}n.exports=r},{}],17:[function(t,n,e){n.exports={exists:"undefined"!=typeof window.performance&&window.performance.timing&&"undefined"!=typeof window.performance.timing.navigationStart}},{}],18:[function(t,n,e){function r(t){return!(t&&t instanceof Function&&t.apply&&!t[a])}var o=t("ee"),i=t(16),a="nr@original",s=Object.prototype.hasOwnProperty,c=!1;n.exports=function(t,n){function e(t,n,e,o){function nrWrapper(){var r,a,s,c;try{a=this,r=i(arguments),s="function"==typeof e?e(r,a):e||{}}catch(f){l([f,"",[r,a,o],s])}u(n+"start",[r,a,o],s);try{return c=t.apply(a,r)}catch(d){throw u(n+"err",[r,a,d],s),d}finally{u(n+"end",[r,a,c],s)}}return r(t)?t:(n||(n=""),nrWrapper[a]=t,d(t,nrWrapper),nrWrapper)}function f(t,n,o,i){o||(o="");var a,s,c,f="-"===o.charAt(0);for(c=0;c<n.length;c++)s=n[c],a=t[s],r(a)||(t[s]=e(a,f?s+o:o,i,s))}function u(e,r,o){if(!c||n){var i=c;c=!0;try{t.emit(e,r,o,n)}catch(a){l([a,e,r,o])}c=i}}function d(t,n){if(Object.defineProperty&&Object.keys)try{var e=Object.keys(t);return e.forEach(function(e){Object.defineProperty(n,e,{get:function(){return t[e]},set:function(n){return t[e]=n,n}})}),n}catch(r){l([r])}for(var o in t)s.call(t,o)&&(n[o]=t[o]);return n}function l(n){try{t.emit("internal-error",n)}catch(e){}}return t||(t=o),e.inPlace=f,e.flag=a,e}},{}],ee:[function(t,n,e){function r(){}function o(t){function n(t){return t&&t instanceof r?t:t?c(t,s,i):i()}function e(e,r,o,i){if(!l.aborted||i){t&&t(e,r,o);for(var a=n(o),s=h(e),c=s.length,f=0;f<c;f++)s[f].apply(a,r);var d=u[y[e]];return d&&d.push([g,e,r,a]),a}}function p(t,n){v[t]=h(t).concat(n)}function h(t){return v[t]||[]}function m(t){return d[t]=d[t]||o(e)}function w(t,n){f(t,function(t,e){n=n||"feature",y[e]=n,n in u||(u[n]=[])})}var v={},y={},g={on:p,emit:e,get:m,listeners:h,context:n,buffer:w,abort:a,aborted:!1};return g}function i(){return new r}function a(){(u.api||u.feature)&&(l.aborted=!0,u=l.backlog={})}var s="nr@context",c=t("gos"),f=t(15),u={},d={},l=n.exports=o();l.backlog=u},{}],gos:[function(t,n,e){function r(t,n,e){if(o.call(t,n))return t[n];var r=e();if(Object.defineProperty&&Object.keys)try{return Object.defineProperty(t,n,{value:r,writable:!0,enumerable:!1}),r}catch(i){}return t[n]=r,r}var o=Object.prototype.hasOwnProperty;n.exports=r},{}],handle:[function(t,n,e){function r(t,n,e,r){o.buffer([t],r),o.emit(t,n,e)}var o=t("ee").get("handle");n.exports=r,r.ee=o},{}],id:[function(t,n,e){function r(t){var n=typeof t;return!t||"object"!==n&&"function"!==n?-1:t===window?0:a(t,i,function(){return o++})}var o=1,i="nr@id",a=t("gos");n.exports=r},{}],loader:[function(t,n,e){function r(){if(!x++){var t=b.info=NREUM.info,n=l.getElementsByTagName("script")[0];if(setTimeout(u.abort,3e4),!(t&&t.licenseKey&&t.applicationID&&n))return u.abort();f(y,function(n,e){t[n]||(t[n]=e)}),c("mark",["onload",a()+b.offset],null,"api");var e=l.createElement("script");e.src="https://"+t.agent,n.parentNode.insertBefore(e,n)}}function o(){"complete"===l.readyState&&i()}function i(){c("mark",["domContent",a()+b.offset],null,"api")}function a(){return E.exists&&performance.now?Math.round(performance.now()):(s=Math.max((new Date).getTime(),s))-b.offset}var s=(new Date).getTime(),c=t("handle"),f=t(15),u=t("ee"),d=window,l=d.document,p="addEventListener",h="attachEvent",m=d.XMLHttpRequest,w=m&&m.prototype;NREUM.o={ST:setTimeout,SI:d.setImmediate,CT:clearTimeout,XHR:m,REQ:d.Request,EV:d.Event,PR:d.Promise,MO:d.MutationObserver};var v=""+location,y={beacon:"bam.nr-data.net",errorBeacon:"bam.nr-data.net",agent:"js-agent.newrelic.com/nr-1071.min.js"},g=m&&w&&w[p]&&!/CriOS/.test(navigator.userAgent),b=n.exports={offset:s,now:a,origin:v,features:{},xhrWrappable:g};t(12),l[p]?(l[p]("DOMContentLoaded",i,!1),d[p]("load",r,!1)):(l[h]("onreadystatechange",o),d[h]("onload",r)),c("mark",["firstbyte",s],null,"api");var x=0,E=t(17)},{}]},{},["loader",2,10,4,3]);
      </script>
      <!-- Responsiveness -->
      <meta content="width=device-width, initial-scale=1.0" name="viewport"/>
      <!-- Favicon -->
      <link href="/apple-touch-icon.png" rel="apple-touch-icon" sizes="180x180"/>
      <link href="/favicon-32x32.png" rel="icon" sizes="32x32" type="image/png"/>
      <link href="/favicon-16x16.png" rel="icon" sizes="16x16" type="image/png"/>
      <link href="/manifest.json" rel="manifest"/>
      <link color="#e48b55" href="/safari-pinned-tab.svg" rel="mask-icon"/>
      <meta content="#000000" name="theme-color"/>
      <meta content="authenticity_token" name="csrf-param"/>
      <meta content="EZDS8ScHdvu4YMmV+jNfTk0PM5dHHtNU8cz/f7TYrco=" name="csrf-token"/>
      <title>
       News  – NASA’s Mars Exploration Program
      </title>
      <meta content="NASA’s Mars Exploration Program " property="og:site_name"/>
      <meta content="mars.nasa.gov" name="author"/>
      <meta content="Mars, missions, NASA, rover, Curiosity, Opportunity, InSight, Mars Reconnaissance Orbiter, facts" name="keywords"/>
      <meta content="NASA’s real-time portal for Mars exploration, featuring the last news, images, and discoveries from the Red Planet." name="description"/>
      <meta content="NASA’s real-time portal for Mars exploration, featuring the last news, images, and discoveries from the Red Planet." property="og:description"/>
      <meta content="NASA’s Mars Exploration Program : News " property="og:title"/>
      <meta content="https://mars.nasa.gov/news?page=0&amp;per_page=40&amp;order=publish_date+desc%2Ccreated_at+desc&amp;search=&amp;category=19%2C165%2C184%2C204&amp;blank_scope=Latest" property="og:url"/>
      <meta content="article" property="og:type"/>
      <meta content="2017-09-22 19:53:22 UTC" property="og:updated_time"/>
      <meta content="https://mars.nasa.gov/system/site_config_values/meta_share_images/1_142497main_PIA03154-200.jpg" property="og:image"/>
      <link href="https://mars.nasa.gov/system/site_config_values/meta_share_images/1_142497main_PIA03154-200.jpg" rel="image_src"/>
      <link href="https://fonts.googleapis.com/css?family=Montserrat:200,300,400,500,600,700|Raleway:300,400" rel="stylesheet"/>
      <link href="/assets/public_manifest-574a8376577ebdeea854fd2967ce0bef2e7d5cfd38633c33e8d92aed83e81c3a.css" media="all" rel="stylesheet"/>
      <link href="/assets/gulp/vendor/jquery.fancybox-364352e03618ba5a8da007665b1f0be31795293b22bc4d7c5974891d4976a137.css" media="screen" rel="stylesheet"/>
      <link href="/assets/gulp/print-240f8bfaa7f6402dfd6c49ee3c1ffea57a89ddd4c8c90e2f2a5c7d63c5753e32.css" media="print" rel="stylesheet"/>
      <script src="/assets/public_manifest-eed54cbc0cf59efc6cd5645db8873a28b8feb4489dd1ea1c3842a65c1a1d5dee.js">
      </script>
      <!--[if gt IE 8]><!-->
      <script src="/assets/not_ie8_manifest.js">
      </script>
      <!--[if !IE]>-->
      <script src="/assets/not_ie8_manifest.js">
      </script>
      <!--<![endif]-->
      <script src="/assets/vendor/jquery.fancybox-9d361e5f98a5c0f233a25df9252dbadea6897af1c0ef221d7465e1205941ea0d.js">
      </script>
      <script src="/assets/mb_manifest-86cde101f747092d1465039f6da3fd2930c66319387c196503d3f70665195392.js">
      </script>
      <!-- /twitter cards -->
      <meta content="summary_large_image" name="twitter:card"/>
      <meta content="News " name="twitter:title"/>
      <meta content="NASA’s real-time portal for Mars exploration, featuring the last news, images, and discoveries from the Red Planet." name="twitter:description"/>
      <meta content="https://mars.nasa.gov/system/site_config_values/meta_share_images/1_142497main_PIA03154-200.jpg" name="twitter:image"/>
     </head>
     <body id="news">
      <div id="main_container">
       <div id="site_body">
        <div class="site_header_area">
         <header class="site_header">
          <div class="brand_area">
           <div class="brand1">
            <a class="nasa_logo" href="http://www.nasa.gov" target="_blank" title="visit nasa.gov">
             NASA
            </a>
           </div>
           <div class="brand2">
            <a class="top_logo" href="https://science.nasa.gov/" target="_blank" title="Explore NASA Science">
             NASA Science
            </a>
            <a class="sub_logo" href="/mars-exploration/#" title="Mars">
             Mars Exploration Program
            </a>
           </div>
           <img alt="" class="print_only print_logo" src="/assets/logo_nasa_trio_black@2x.png"/>
          </div>
          <a class="visuallyhidden focusable" href="#page">
           Skip Navigation
          </a>
          <div class="right_header_container">
           <a class="menu_button" href="javascript:void(0);" id="menu_button">
            <span class="menu_icon">
             menu
            </span>
           </a>
           <a class="modal_close" id="modal_close">
            <span class="modal_close_icon">
            </span>
           </a>
          </div>
          <div class="nav_area">
           <div id="site_nav_container">
            <nav class="site_nav">
             <ul class="nav">
              <li>
               <div class="arrow_box">
                <span class="arrow_down">
                </span>
               </div>
               <div class="nav_title">
                <a class="main_nav_item" href="/#red_planet" target="_self">
                 The Red Planet
                </a>
               </div>
               <div class="global_subnav_container">
                <ul class="subnav">
                 <li>
                  <a href="/#red_planet/0" target="_self">
                   Dashboard
                  </a>
                 </li>
                 <li>
                  <a href="/#red_planet/1" target="_self">
                   Science Goals
                  </a>
                 </li>
                 <li>
                  <a href="/#red_planet/2" target="_self">
                   The Planet
                  </a>
                 </li>
                 <li>
                  <a href="/#red_planet/3" target="_self">
                   Atmosphere
                  </a>
                 </li>
                 <li>
                  <a href="/#red_planet/4" target="_self">
                   Astrobiology
                  </a>
                 </li>
                 <li>
                  <a href="/#red_planet/5" target="_self">
                   Past, Present, Future, Timeline
                  </a>
                 </li>
                </ul>
               </div>
               <div class="gradient_line">
               </div>
              </li>
              <li>
               <div class="arrow_box">
                <span class="arrow_down">
                </span>
               </div>
               <div class="nav_title">
                <a class="main_nav_item" href="/#mars_exploration_program" target="_self">
                 The Program
                </a>
               </div>
               <div class="global_subnav_container">
                <ul class="subnav">
                 <li>
                  <a href="/#mars_exploration_program/0" target="_self">
                   Mission Statement
                  </a>
                 </li>
                 <li>
                  <a href="/#mars_exploration_program/1" target="_self">
                   About the Program
                  </a>
                 </li>
                 <li>
                  <a href="/#mars_exploration_program/2" target="_self">
                   Organization
                  </a>
                 </li>
                 <li>
                  <a href="/#mars_exploration_program/3" target="_self">
                   Why Mars?
                  </a>
                 </li>
                 <li>
                  <a href="/#mars_exploration_program/4" target="_self">
                   Research Programs
                  </a>
                 </li>
                 <li>
                  <a href="/#mars_exploration_program/5" target="_self">
                   Planetary Resources
                  </a>
                 </li>
                 <li>
                  <a href="/#mars_exploration_program/6" target="_self">
                   Technologies
                  </a>
                 </li>
                </ul>
               </div>
               <div class="gradient_line">
               </div>
              </li>
              <li>
               <div class="arrow_box">
                <span class="arrow_down">
                </span>
               </div>
               <div class="nav_title">
                <a class="main_nav_item" href="/#news_and_events" target="_self">
                 News &amp; Events
                </a>
               </div>
               <div class="global_subnav_container">
                <ul class="subnav">
                 <li>
                  <a href="/news" target="_self">
                   News
                  </a>
                 </li>
                 <li>
                  <a href="/events" target="_self">
                   Events
                  </a>
                 </li>
                </ul>
               </div>
               <div class="gradient_line">
               </div>
              </li>
              <li>
               <div class="arrow_box">
                <span class="arrow_down">
                </span>
               </div>
               <div class="nav_title">
                <a class="main_nav_item" href="/#multimedia" target="_self">
                 Multimedia
                </a>
               </div>
               <div class="global_subnav_container">
                <ul class="subnav">
                 <li>
                  <a href="/multimedia/images/" target="_self">
                   Images
                  </a>
                 </li>
                 <li>
                  <a href="/multimedia/videos/" target="_self">
                   Videos
                  </a>
                 </li>
                </ul>
               </div>
               <div class="gradient_line">
               </div>
              </li>
              <li>
               <div class="arrow_box">
                <span class="arrow_down">
                </span>
               </div>
               <div class="nav_title">
                <a class="main_nav_item" href="/#missions" target="_self">
                 Missions
                </a>
               </div>
               <div class="global_subnav_container">
                <ul class="subnav">
                 <li>
                  <a href="/mars-exploration/missions/?category=167" target="_self">
                   Past
                  </a>
                 </li>
                 <li>
                  <a href="/mars-exploration/missions/?category=170" target="_self">
                   Present
                  </a>
                 </li>
                 <li>
                  <a href="/mars-exploration/missions/?category=171" target="_self">
                   Future
                  </a>
                 </li>
                 <li>
                  <a href="/mars-exploration/partners" target="_self">
                   International Partners
                  </a>
                 </li>
                </ul>
               </div>
               <div class="gradient_line">
               </div>
              </li>
              <li>
               <div class="nav_title">
                <a class="main_nav_item" href="/#more" target="_self">
                 More
                </a>
               </div>
               <div class="gradient_line">
               </div>
              </li>
              <li>
               <div class="nav_title">
                <a class="main_nav_item" href="/legacy" target="_self">
                 Legacy Site
                </a>
               </div>
               <div class="gradient_line">
               </div>
              </li>
             </ul>
             <form action="https://mars.nasa.gov/search/" class="overlay_search nav_search">
              <label class="search_label">
               Search
              </label>
              <input class="search_field" name="q" type="text" value=""/>
              <div class="search_submit">
              </div>
             </form>
            </nav>
           </div>
          </div>
         </header>
        </div>
        <div id="sticky_nav_spacer">
        </div>
        <div id="page">
         <!-- title to go in the page_header -->
         <div class="header_mask">
         </div>
         <div class="react_grid_list" data-react-class="GridListPage" data-react-props='{"left_column":false,"class_name":"","default_view":"list_view","model":"news_items","view_toggle":false,"search":true,"list_item":"News","title":"News","categories":["19,165,184,204"],"order":"publish_date desc,created_at desc","no_items_text":"There are no items matching these criteria.","per_page":null,"filters":"[ [ \"date\", [ [ \"2018\", \"2018\" ], [ \"2017\", \"2017\" ], [ \"2016\", \"2016\" ], [ \"2015\", \"2015\" ], [ \"2014\", \"2014\" ], [ \"2013\", \"2013\" ], [ \"2012\", \"2012\" ], [ \"2011\", \"2011\" ], [ \"2010\", \"2010\" ], [ \"2009\", \"2009\" ], [ \"2008\", \"2008\" ], [ \"2007\", \"2007\" ], [ \"2006\", \"2006\" ], [ \"2005\", \"2005\" ], [ \"2004\", \"2004\" ], [ \"2003\", \"2003\" ], [ \"2002\", \"2002\" ], [ \"2001\", \"2001\" ], [ \"2000\", \"2000\" ] ], [ \"Latest\", \"\" ], false ], [ \"categories\", [ [ \"Feature Stories\", 165 ], [ \"Press Releases\", 19 ], [ \"Spotlights\", 184 ], [ \"Status Reports\", 204 ] ], [ \"All Categories\", \"\" ], false ] ]","conditions":null,"scope_in_title":true,"options":{"blank_scope":"Latest"},"results_in_title":false}'>
         </div>
         <section class="module suggested_features">
          <div class="grid_layout">
           <header>
            <h2 class="module_title">
             You Might Also Like
            </h2>
           </header>
           <section>
            <script>
             $(document).ready(function(){
        $(".features").slick({
          dots: false,
          infinite: true,
          speed: 300,
          slide: '.features .slide',
          slidesToShow: 3,
          slidesToScroll: 3,
          lazyLoad: 'ondemand',
          centerMode: false,
          arrows: true,
          appendArrows: '.features .slick-nav',
          appendDots: ".features .slick-nav",
          responsive: [{"breakpoint":953,"settings":{"slidesToShow":2,"slidesToScroll":2,"centerMode":false}},{"breakpoint":480,"settings":{"slidesToShow":1,"slidesToScroll":1,"centerMode":true,"arrows":false,"centerPadding":"25px"}}]
        });
      });
            </script>
            <div class="features">
             <div class="slide">
              <div class="image_and_description_container">
               <a href="/news/8326/nasa-invests-in-visionary-technology/">
                <div class="rollover_description">
                 <div class="rollover_description_inner">
                  NASA is investing in technology concepts, including several from JPL, that may one day be used for future space exploration missions.
                 </div>
                 <div class="overlay_arrow">
                  <img alt="More" src="/assets/overlay-arrow.png"/>
                 </div>
                </div>
                <img alt="NASA Invests in Visionary Technology " class="img-lazy" data-lazy="/system/news_items/list_view_images/8326_niac320.jpg" src="/assets/loading_320x240.png"/>
               </a>
              </div>
              <div class="content_title">
               <a href="/news/8326/nasa-invests-in-visionary-technology/">
                NASA Invests in Visionary Technology
               </a>
              </div>
             </div>
             <div class="slide">
              <div class="image_and_description_container">
               <a href="/news/8325/nasa-is-ready-to-study-the-heart-of-mars/">
                <div class="rollover_description">
                 <div class="rollover_description_inner">
                  NASA is about to go on a journey to study the center of Mars.
                 </div>
                 <div class="overlay_arrow">
                  <img alt="More" src="/assets/overlay-arrow.png"/>
                 </div>
                </div>
                <img alt="NASA is Ready to Study the Heart of Mars" class="img-lazy" data-lazy="/system/news_items/list_view_images/8325_insight20180329b_320.jpg" src="/assets/loading_320x240.png"/>
               </a>
              </div>
              <div class="content_title">
               <a href="/news/8325/nasa-is-ready-to-study-the-heart-of-mars/">
                NASA is Ready to Study the Heart of Mars
               </a>
              </div>
             </div>
             <div class="slide">
              <div class="image_and_description_container">
               <a href="/news/8322/nasa-briefing-on-first-mission-to-study-mars-interior/">
                <div class="rollover_description">
                 <div class="rollover_description_inner">
                  NASA’s next mission to Mars will be the topic of a media briefing Thursday, March 29, at JPL. The briefing will air live on NASA Television and the agency’s website.
                 </div>
                 <div class="overlay_arrow">
                  <img alt="More" src="/assets/overlay-arrow.png"/>
                 </div>
                </div>
                <img alt="NASA Briefing on First Mission to Study Mars Interior" class="img-lazy" data-lazy="/system/news_items/list_view_images/8322_PIA22228_320.jpg" src="/assets/loading_320x240.png"/>
               </a>
              </div>
              <div class="content_title">
               <a href="/news/8322/nasa-briefing-on-first-mission-to-study-mars-interior/">
                NASA Briefing on First Mission to Study Mars Interior
               </a>
              </div>
             </div>
             <div class="slide">
              <div class="image_and_description_container">
               <a href="/news/8321/new-ar-mobile-app-features-3-d-nasa-spacecraft/">
                <div class="rollover_description">
                 <div class="rollover_description_inner">
                  NASA spacecraft travel to far-off destinations in space, but a new mobile app produced by NASA's Jet Propulsion Laboratory, Pasadena, California, brings spacecraft to users.
                 </div>
                 <div class="overlay_arrow">
                  <img alt="More" src="/assets/overlay-arrow.png"/>
                 </div>
                </div>
                <img alt="New 'AR' Mobile App Features 3-D NASA Spacecraft" class="img-lazy" data-lazy="/system/news_items/list_view_images/8321_list_image.jpg" src="/assets/loading_320x240.png"/>
               </a>
              </div>
              <div class="content_title">
               <a href="/news/8321/new-ar-mobile-app-features-3-d-nasa-spacecraft/">
                New 'AR' Mobile App Features 3-D NASA Spacecraft
               </a>
              </div>
             </div>
             <div class="slide">
              <div class="image_and_description_container">
               <a href="/news/8317/witness-first-mars-launch-from-west-coast/">
                <div class="rollover_description">
                 <div class="rollover_description_inner">
                  NASA invites digital creators to apply for social media credentials to cover the launch of the InSight mission to Mars, May 3-5, at California's Vandenberg Air Force Base.
                 </div>
                 <div class="overlay_arrow">
                  <img alt="More" src="/assets/overlay-arrow.png"/>
                 </div>
                </div>
                <img alt="Witness First Mars Launch from West Coast" class="img-lazy" data-lazy="/system/news_items/list_view_images/8317_list_image.jpg" src="/assets/loading_320x240.png"/>
               </a>
              </div>
              <div class="content_title">
               <a href="/news/8317/witness-first-mars-launch-from-west-coast/">
                Witness First Mars Launch from West Coast
               </a>
              </div>
             </div>
             <div class="slide">
              <div class="image_and_description_container">
               <a href="/news/8315/nasa-insight-mission-to-mars-arrives-at-launch-site/">
                <div class="rollover_description">
                 <div class="rollover_description_inner">
                  NASA's InSight spacecraft has arrived at Vandenberg Air Force Base in central California to begin final preparations for a launch this May.
                 </div>
                 <div class="overlay_arrow">
                  <img alt="More" src="/assets/overlay-arrow.png"/>
                 </div>
                </div>
                <img alt="NASA InSight Mission to Mars Arrives at Launch Site" class="img-lazy" data-lazy="/system/news_items/list_view_images/8315_list_image.jpg" src="/assets/loading_320x240.png"/>
               </a>
              </div>
              <div class="content_title">
               <a href="/news/8315/nasa-insight-mission-to-mars-arrives-at-launch-site/">
                NASA InSight Mission to Mars Arrives at Launch Site
               </a>
              </div>
             </div>
             <div class="grid_layout">
              <div class="slick-nav_container">
               <div class="slick-nav">
               </div>
              </div>
             </div>
            </div>
           </section>
          </div>
         </section>
        </div>
        <footer id="site_footer">
         <div class="grid_layout">
          <section class="upper_footer">
           <div class="share">
            <h2>
             Follow the Journey
            </h2>
            <div class="social_icons">
             <!-- AddThis Button BEGIN -->
             <div class="addthis_toolbox addthis_default_style addthis_32x32_style">
              <a addthis:userid="NASABeAMartian" class="addthis_button_twitter_follow icon">
               <img alt="twitter" src="/assets/twitter_icon@2x.png"/>
              </a>
              <a addthis:userid="NASABEAM" class="addthis_button_facebook_follow icon">
               <img alt="facebook" src="/assets/facebook_icon@2x.png"/>
              </a>
              <a addthis:userid="nasa" class="addthis_button_instagram_follow icon">
               <img alt="instagram" src="/assets/instagram_icon@2x.png"/>
              </a>
              <a addthis:url="https://mars.nasa.gov/rss/api/?feed=news&amp;category=all&amp;feedtype=rss" class="addthis_button_rss_follow icon">
               <img alt="rss" src="/assets/rss_icon@2x.png"/>
              </a>
             </div>
             <script>
              addthis_loader.init("//s7.addthis.com/js/300/addthis_widget.js#pubid=ra-5a690e4c1320e328", {follow: true})
             </script>
             <!-- AddThis Button END -->
            </div>
           </div>
           <div class="gradient_line">
           </div>
          </section>
          <section class="sitemap">
           <div class="sitemap_directory" id="sitemap_directory">
            <div class="sitemap_block">
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               <a href="/#red_planet">
                The Red Planet
               </a>
              </h3>
              <ul>
               <li>
                <div class="global_subnav_container">
                 <ul class="subnav">
                  <li>
                   <a href="/#red_planet/0" target="_self">
                    Dashboard
                   </a>
                  </li>
                  <li>
                   <a href="/#red_planet/1" target="_self">
                    Science Goals
                   </a>
                  </li>
                  <li>
                   <a href="/#red_planet/2" target="_self">
                    The Planet
                   </a>
                  </li>
                  <li>
                   <a href="/#red_planet/3" target="_self">
                    Atmosphere
                   </a>
                  </li>
                  <li>
                   <a href="/#red_planet/4" target="_self">
                    Astrobiology
                   </a>
                  </li>
                  <li>
                   <a href="/#red_planet/5" target="_self">
                    Past, Present, Future, Timeline
                   </a>
                  </li>
                 </ul>
                </div>
               </li>
              </ul>
             </div>
            </div>
            <div class="sitemap_block">
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               <a href="/#mars_exploration_program">
                The Program
               </a>
              </h3>
              <ul>
               <li>
                <div class="global_subnav_container">
                 <ul class="subnav">
                  <li>
                   <a href="/#mars_exploration_program/0" target="_self">
                    Mission Statement
                   </a>
                  </li>
                  <li>
                   <a href="/#mars_exploration_program/1" target="_self">
                    About the Program
                   </a>
                  </li>
                  <li>
                   <a href="/#mars_exploration_program/2" target="_self">
                    Organization
                   </a>
                  </li>
                  <li>
                   <a href="/#mars_exploration_program/3" target="_self">
                    Why Mars?
                   </a>
                  </li>
                  <li>
                   <a href="/#mars_exploration_program/4" target="_self">
                    Research Programs
                   </a>
                  </li>
                  <li>
                   <a href="/#mars_exploration_program/5" target="_self">
                    Planetary Resources
                   </a>
                  </li>
                  <li>
                   <a href="/#mars_exploration_program/6" target="_self">
                    Technologies
                   </a>
                  </li>
                 </ul>
                </div>
               </li>
              </ul>
             </div>
            </div>
            <div class="sitemap_block">
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               <a href="/#news_and_events">
                News &amp; Events
               </a>
              </h3>
              <ul>
               <li>
                <div class="global_subnav_container">
                 <ul class="subnav">
                  <li>
                   <a href="/news" target="_self">
                    News
                   </a>
                  </li>
                  <li>
                   <a href="/events" target="_self">
                    Events
                   </a>
                  </li>
                 </ul>
                </div>
               </li>
              </ul>
             </div>
            </div>
            <div class="sitemap_block">
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               <a href="/#multimedia">
                Multimedia
               </a>
              </h3>
              <ul>
               <li>
                <div class="global_subnav_container">
                 <ul class="subnav">
                  <li>
                   <a href="/multimedia/images/" target="_self">
                    Images
                   </a>
                  </li>
                  <li>
                   <a href="/multimedia/videos/" target="_self">
                    Videos
                   </a>
                  </li>
                 </ul>
                </div>
               </li>
              </ul>
             </div>
            </div>
            <div class="sitemap_block">
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               <a href="/#missions">
                Missions
               </a>
              </h3>
              <ul>
               <li>
                <div class="global_subnav_container">
                 <ul class="subnav">
                  <li>
                   <a href="/mars-exploration/missions/?category=167" target="_self">
                    Past
                   </a>
                  </li>
                  <li>
                   <a href="/mars-exploration/missions/?category=170" target="_self">
                    Present
                   </a>
                  </li>
                  <li>
                   <a href="/mars-exploration/missions/?category=171" target="_self">
                    Future
                   </a>
                  </li>
                  <li>
                   <a href="/mars-exploration/partners" target="_self">
                    International Partners
                   </a>
                  </li>
                 </ul>
                </div>
               </li>
              </ul>
             </div>
            </div>
            <div class="sitemap_block">
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               <a href="/#more">
                More
               </a>
              </h3>
              <ul>
               <li>
                <div class="global_subnav_container">
                 <ul class="subnav">
                 </ul>
                </div>
               </li>
              </ul>
             </div>
            </div>
            <div class="sitemap_block">
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               <a href="/legacy">
                Legacy Site
               </a>
              </h3>
              <ul>
               <li>
                <div class="global_subnav_container">
                 <ul class="subnav">
                  <li>
                   <a class="" href="/legacy" target="_self">
                    Legacy Site
                   </a>
                  </li>
                 </ul>
                </div>
               </li>
              </ul>
             </div>
            </div>
           </div>
           <div class="gradient_line">
           </div>
          </section>
          <section class="lower_footer">
           <div class="nav_container">
            <nav>
             <ul>
              <li>
               <a href="http://science.nasa.gov/" target="_blank">
                NASA Science Mission Directorate
               </a>
              </li>
              <li>
               <a href="https://www.jpl.nasa.gov/copyrights.php" target="_blank">
                Privacy
               </a>
              </li>
              <li>
               <a href="http://www.jpl.nasa.gov/imagepolicy/" target="_blank">
                Image Policy
               </a>
              </li>
              <li>
               <a href="https://mars.nasa.gov/feedback/" target="_self">
                Feedback
               </a>
              </li>
              <li>
               <a href="http://mars.nasa.gov/legacy" target="_blank">
                Legacy Mars Site
               </a>
              </li>
             </ul>
            </nav>
           </div>
           <div class="credits">
            <div class="footer_brands_top">
             <p>
              Managed by the Mars Exploration Program and the Jet Propulsion Laboratory for NASA’s Science Mission Directorate
             </p>
            </div>
            <!-- .footer_brands -->
            <!-- %a.jpl{href: "", target: "_blank"}Institution -->
            <!--  -->
            <!-- %a.caltech{href: "", target: "_blank"}Institution -->
            <!-- .staff -->
            <!-- %p -->
            <!-- - get_staff_for_category(get_field_from_admin_config(:web_staff_category_id)) -->
            <!-- - @staff.each_with_index do |staff, idx| -->
            <!-- - unless staff.is_in_footer == 0 -->
            <!-- = staff.title + ": " -->
            <!-- - if staff.contact_link =~ /@/ -->
            <!-- = mail_to staff.contact_link, staff.name, :subject => "[#{@site_title}]" -->
            <!-- - elsif staff.contact_link.present? -->
            <!-- = link_to staff.name, staff.contact_link -->
            <!-- - else -->
            <!-- = staff.name -->
            <!-- - unless (idx + 1 == @staff.size) -->
            <!-- %br -->
           </div>
          </section>
         </div>
        </footer>
       </div>
      </div>
      <script id="_fed_an_ua_tag" src="https://dap.digitalgov.gov/Universal-Federated-Analytics-Min.js?agency=NASA&amp;subagency=JPL-Mars-MEPJPL&amp;pua=UA-9453474-9,UA-118212757-11&amp;dclink=true&amp;sp=searchbox&amp;exts=tif,tiff,wav" type="text/javascript">
      </script>
     </body>
    </html>
    


```python
 # Extract the text from the class="content_title" and clean up the text use strip
news_title = soup1.find_all('div', class_='content_title')[0].find('a').text.strip()

#print title to check
print(news_title)
```

    NASA Invests in Visionary Technology
    


```python
 # Extract the paragraph from the class="rollover_description_inner" and clean up the text use strip
news_p = soup1.find_all('div', class_='rollover_description_inner')[0].text.strip()

#print paragraph to check
print(news_p)
```

    NASA is investing in technology concepts, including several from JPL, that may one day be used for future space exploration missions.
    

#### JPL Mars Space Images - Featured Image

Use splinter to navigate the JPL's Featured Space Image and scrape the current Featured Mars Image url (https://www.jpl.nasa.gov/spaceimages/?search=&category=Mars)


```python
# Execute Chromedriver
executable_path = {'executable_path': 'chromedriver.exe'}
browser = Browser('chrome', **executable_path, headless=False)
```


```python
# URL of page to be scraped
url2 = 'https://www.jpl.nasa.gov/spaceimages/?search=&category=Mars'

#Visit the page using the browser
browser.visit(url2)
```


```python
# assign html content
html = browser.html
# Create a Beautiful Soup object
soup2 = bs(html, "html5lib")
# Print formatted version of the soup
print(soup2.prettify())
```

    <!DOCTYPE html>
    <!--[if IE 9]> <html class="no-js ie ie9" lang="en"> <![endif]-->
    <!--[if IE 8]> <html class="no-js ie ie8" lang="en"> <![endif]-->
    <html class="js flexbox canvas canvastext webgl no-touch geolocation postmessage websqldatabase indexeddb hashchange history draganddrop websockets rgba hsla multiplebgs backgroundsize borderimage borderradius boxshadow textshadow opacity cssanimations csscolumns cssgradients cssreflections csstransforms csstransforms3d csstransitions fontface no-generatedcontent video audio localstorage sessionstorage webworkers applicationcache svg inlinesvg smil svgclippaths -webkit-" style="" xmlns="http://www.w3.org/1999/xhtml">
     <!-- START HEADER: "DEFAULT" -->
     <head>
      <script src="//m.addthis.com/live/red_lojson/300lo.json?si=5af50adabcc7c5c0&amp;bkl=0&amp;bl=1&amp;pdt=753&amp;sid=5af50adabcc7c5c0&amp;pub=&amp;rev=v8.3.12-wp&amp;ln=en&amp;pc=men&amp;cb=0&amp;ab=-&amp;dp=www.jpl.nasa.gov&amp;fp=spaceimages%2F%3Fsearch%3D%26category%3DMars&amp;fr=&amp;of=1&amp;pd=0&amp;irt=0&amp;vcl=0&amp;md=0&amp;ct=1&amp;tct=0&amp;abt=0&amp;cdn=0&amp;pi=1&amp;rb=0&amp;gen=100&amp;chr=UTF-8&amp;colc=1526008538269&amp;jsl=1&amp;skipb=1&amp;callback=addthis.cbs.oln9_131859561794785530" type="text/javascript">
      </script>
      <script async="" src="https://script.crazyegg.com/pages/scripts/0025/5267.js?423891" type="text/javascript">
      </script>
      <meta charset="utf-8"/>
      <!-- Always force latest IE rendering engine or request Chrome Frame -->
      <meta content="IE=edge,chrome=1" http-equiv="X-UA-Compatible"/>
      <meta content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" name="viewport"/>
      <title>
       Space Images
      </title>
      <style data-href="/assets/stylesheets/manifest.css" media="all">
       @import url("https://www.jpl.nasa.gov/assets/stylesheets/vendor/jquery.fancybox.css");@import url("https://www.jpl.nasa.gov/assets/stylesheets/vendor/jquery.fancybox-thumbs.css");html,body,div,span,applet,object,iframe,h1,h2,h3,h4,h5,h6,p,blockquote,pre,a,abbr,acronym,address,big,cite,code,del,dfn,em,img,ins,kbd,q,s,samp,small,strike,strong,sub,sup,tt,var,b,u,i,center,dl,dt,dd,ol,ul,li,fieldset,form,label,legend,table,caption,tbody,tfoot,thead,tr,th,td,article,aside,canvas,details,embed,figure,figcaption,footer,header,hgroup,menu,nav,output,ruby,section,summary,time,mark,audio,video{border:0;font-size:100%;font:inherit;vertical-align:baseline;margin:0;padding:0}article,aside,details,figcaption,figure,footer,header,hgroup,menu,nav,section{display:block}body{line-height:1}ol,ul{list-style:none}blockquote,q{quotes:none}blockquote:before,blockquote:after,q:before,q:after{content:none}table{border-collapse:collapse;border-spacing:0}html,button,input,select,textarea{color:#222}body{font-size:1em;line-height:1.4}::-moz-selection{background:#b3d4fc;text-shadow:none}::selection{background:#b3d4fc;text-shadow:none}hr{display:block;height:1px;border:0;border-top:1px solid #ccc;margin:1em 0;padding:0}audio,canvas,img,video{vertical-align:middle}fieldset{border:0;margin:0;padding:0}textarea{resize:vertical}.browsehappy{margin:0.2em 0;background:#ccc;color:#000;padding:0.2em 0}.ir{background-color:transparent;border:0;overflow:hidden;*text-indent:-9999px}.ir:before{content:"";display:block;width:0;height:150%}.hidden{display:none !important;visibility:hidden}.visuallyhidden{border:0;clip:rect(0 0 0 0);height:1px;margin:-1px;overflow:hidden;padding:0;position:absolute;width:1px}.visuallyhidden.focusable:active,.visuallyhidden.focusable:focus{clip:auto;height:auto;margin:0;overflow:visible;position:static;width:auto}.invisible{visibility:hidden}.clearfix:before,.main_nav_overlay .nav_item:before,.clearfix:after,.main_nav_overlay .nav_item:after{content:" ";display:table}.clearfix:after,.main_nav_overlay .nav_item:after{clear:both}.clearfix,.main_nav_overlay .nav_item{*zoom:1}@media print{*{background:transparent !important;color:#000 !important;box-shadow:none !important;text-shadow:none !important}a,a:visited{text-decoration:underline}a[href]:after{content:" (" attr(href) ")"}abbr[title]:after{content:" (" attr(title) ")"}.ir a:after,a[href^="javascript:"]:after,a[href^="#"]:after{content:""}pre,blockquote{border:1px solid #999;page-break-inside:avoid}thead{display:table-header-group}tr,img{page-break-inside:avoid}img{max-width:100% !important}@page{margin:0.5cm}p,h2,h3{orphans:3;widows:3}h2,h3{page-break-after:avoid}}.ui-helper-hidden{display:none}.ui-helper-hidden-accessible{position:absolute !important;clip:rect(1px 1px 1px 1px);clip:rect(1px, 1px, 1px, 1px)}.ui-helper-reset{margin:0;padding:0;border:0;outline:0;line-height:1.3;text-decoration:none;font-size:100%;list-style:none}.ui-helper-clearfix:before,.ui-helper-clearfix:after{content:"";display:table}.ui-helper-clearfix:after{clear:both}.ui-helper-clearfix{zoom:1}.ui-helper-zfix{width:100%;height:100%;top:0;left:0;position:absolute;opacity:0;filter:Alpha(Opacity=0)}.ui-state-disabled{cursor:default !important}.ui-icon{display:block;text-indent:-99999px;overflow:hidden;background-repeat:no-repeat}.ui-widget-overlay{position:absolute;top:0;left:0;width:100%;height:100%}.ui-slider{position:relative;text-align:left}.ui-slider .ui-slider-handle{position:absolute;z-index:2;width:6.2em;height:.7em;cursor:default}.ui-slider .ui-slider-range{position:absolute;z-index:1;font-size:.7em;display:block;border:0;background-position:0 0}.ui-slider-horizontal{height:.8em}.ui-slider-horizontal .ui-slider-handle{top:0;margin-left:0}.ui-slider-horizontal .ui-slider-range{top:0;height:100%}.ui-slider-horizontal .ui-slider-range-min{left:0}.ui-slider-horizontal .ui-slider-range-max{right:0}.ui-slider-vertical{width:.8em;height:100px}.ui-slider-vertical .ui-slider-handle{left:-.3em;margin-left:0;margin-bottom:-.6em}.ui-slider-vertical .ui-slider-range{left:0;width:100%}.ui-slider-vertical .ui-slider-range-min{bottom:0}.ui-slider-vertical .ui-slider-range-max{top:0}.ui-widget{font-family:Segoe UI,Arial,sans-serif;font-size:1.1em}.ui-widget .ui-widget{font-size:1em}.ui-widget input,.ui-widget select,.ui-widget textarea,.ui-widget button{font-family:Segoe UI,Arial,sans-serif;font-size:1em}.ui-widget-content{border:1px solid #666666;background:#000000;color:#ffffff}.ui-widget-content a{color:#ffffff}.ui-widget-header{border:1px solid #333333;background:#333333;color:#ffffff;font-weight:700}.ui-widget-header a{color:#ffffff}.ui-state-default,.ui-widget-content .ui-state-default,.ui-widget-header .ui-state-default{border:1px solid #666666;background:#555555;font-weight:700;color:#eeeeee}.ui-state-default a,.ui-state-default a:link,.ui-state-default a:visited{color:#eeeeee;text-decoration:none}.ui-state-hover a,.ui-state-hover a:hover{color:#ffffff;text-decoration:none}.ui-state-active,.ui-widget-content .ui-state-active,.ui-widget-header .ui-state-active{border:1px solid #ffaf0f;background:#f58400;font-weight:700;color:#ffffff}.ui-state-active a,.ui-state-active a:link,.ui-state-active a:visited{color:#ffffff;text-decoration:none}.ui-state-highlight,.ui-widget-content .ui-state-highlight,.ui-widget-header .ui-state-highlight{border:1px solid #cccccc;background:#eeeeee;color:#2e7db2}.ui-state-highlight a,.ui-widget-content .ui-state-highlight a,.ui-widget-header .ui-state-highlight a{color:#2e7db2}.ui-state-error,.ui-widget-content .ui-state-error,.ui-widget-header .ui-state-error{border:1px solid #ffb73d;background:#ffc73d;color:#111111}.ui-state-error a,.ui-widget-content .ui-state-error a,.ui-widget-header .ui-state-error a{color:#111111}.ui-state-error-text,.ui-widget-content .ui-state-error-text,.ui-widget-header .ui-state-error-text{color:#111111}.ui-priority-primary,.ui-widget-content .ui-priority-primary,.ui-widget-header .ui-priority-primary{font-weight:700}.ui-priority-secondary,.ui-widget-content .ui-priority-secondary,.ui-widget-header .ui-priority-secondary{opacity:.7;filter:Alpha(Opacity=70);font-weight:400}.ui-state-disabled,.ui-widget-content .ui-state-disabled,.ui-widget-header .ui-state-disabled{opacity:.35;filter:Alpha(Opacity=35);background-image:none}.ui-icon{width:16px;height:16px}.ui-icon-carat-1-n{background-position:0 0}.ui-icon-carat-1-ne{background-position:-16px 0}.ui-icon-carat-1-e{background-position:-32px 0}.ui-icon-carat-1-se{background-position:-48px 0}.ui-icon-carat-1-s{background-position:-64px 0}.ui-icon-carat-1-sw{background-position:-80px 0}.ui-icon-carat-1-w{background-position:-96px 0}.ui-icon-carat-1-nw{background-position:-112px 0}.ui-icon-carat-2-n-s{background-position:-128px 0}.ui-icon-carat-2-e-w{background-position:-144px 0}.ui-icon-triangle-1-n{background-position:0 -16px}.ui-icon-triangle-1-ne{background-position:-16px -16px}.ui-icon-triangle-1-e{background-position:-32px -16px}.ui-icon-triangle-1-se{background-position:-48px -16px}.ui-icon-triangle-1-s{background-position:-64px -16px}.ui-icon-triangle-1-sw{background-position:-80px -16px}.ui-icon-triangle-1-w{background-position:-96px -16px}.ui-icon-triangle-1-nw{background-position:-112px -16px}.ui-icon-triangle-2-n-s{background-position:-128px -16px}.ui-icon-triangle-2-e-w{background-position:-144px -16px}.ui-icon-arrow-1-n{background-position:0 -32px}.ui-icon-arrow-1-ne{background-position:-16px -32px}.ui-icon-arrow-1-e{background-position:-32px -32px}.ui-icon-arrow-1-se{background-position:-48px -32px}.ui-icon-arrow-1-s{background-position:-64px -32px}.ui-icon-arrow-1-sw{background-position:-80px -32px}.ui-icon-arrow-1-w{background-position:-96px -32px}.ui-icon-arrow-1-nw{background-position:-112px -32px}.ui-icon-arrow-2-n-s{background-position:-128px -32px}.ui-icon-arrow-2-ne-sw{background-position:-144px -32px}.ui-icon-arrow-2-e-w{background-position:-160px -32px}.ui-icon-arrow-2-se-nw{background-position:-176px -32px}.ui-icon-arrowstop-1-n{background-position:-192px -32px}.ui-icon-arrowstop-1-e{background-position:-208px -32px}.ui-icon-arrowstop-1-s{background-position:-224px -32px}.ui-icon-arrowstop-1-w{background-position:-240px -32px}.ui-icon-arrowthick-1-n{background-position:0 -48px}.ui-icon-arrowthick-1-ne{background-position:-16px -48px}.ui-icon-arrowthick-1-e{background-position:-32px -48px}.ui-icon-arrowthick-1-se{background-position:-48px -48px}.ui-icon-arrowthick-1-s{background-position:-64px -48px}.ui-icon-arrowthick-1-sw{background-position:-80px -48px}.ui-icon-arrowthick-1-w{background-position:-96px -48px}.ui-icon-arrowthick-1-nw{background-position:-112px -48px}.ui-icon-arrowthick-2-n-s{background-position:-128px -48px}.ui-icon-arrowthick-2-ne-sw{background-position:-144px -48px}.ui-icon-arrowthick-2-e-w{background-position:-160px -48px}.ui-icon-arrowthick-2-se-nw{background-position:-176px -48px}.ui-icon-arrowthickstop-1-n{background-position:-192px -48px}.ui-icon-arrowthickstop-1-e{background-position:-208px -48px}.ui-icon-arrowthickstop-1-s{background-position:-224px -48px}.ui-icon-arrowthickstop-1-w{background-position:-240px -48px}.ui-icon-arrowreturnthick-1-w{background-position:0 -64px}.ui-icon-arrowreturnthick-1-n{background-position:-16px -64px}.ui-icon-arrowreturnthick-1-e{background-position:-32px -64px}.ui-icon-arrowreturnthick-1-s{background-position:-48px -64px}.ui-icon-arrowreturn-1-w{background-position:-64px -64px}.ui-icon-arrowreturn-1-n{background-position:-80px -64px}.ui-icon-arrowreturn-1-e{background-position:-96px -64px}.ui-icon-arrowreturn-1-s{background-position:-112px -64px}.ui-icon-arrowrefresh-1-w{background-position:-128px -64px}.ui-icon-arrowrefresh-1-n{background-position:-144px -64px}.ui-icon-arrowrefresh-1-e{background-position:-160px -64px}.ui-icon-arrowrefresh-1-s{background-position:-176px -64px}.ui-icon-arrow-4{background-position:0 -80px}.ui-icon-arrow-4-diag{background-position:-16px -80px}.ui-icon-extlink{background-position:-32px -80px}.ui-icon-newwin{background-position:-48px -80px}.ui-icon-refresh{background-position:-64px -80px}.ui-icon-shuffle{background-position:-80px -80px}.ui-icon-transfer-e-w{background-position:-96px -80px}.ui-icon-transferthick-e-w{background-position:-112px -80px}.ui-icon-folder-collapsed{background-position:0 -96px}.ui-icon-folder-open{background-position:-16px -96px}.ui-icon-document{background-position:-32px -96px}.ui-icon-document-b{background-position:-48px -96px}.ui-icon-note{background-position:-64px -96px}.ui-icon-mail-closed{background-position:-80px -96px}.ui-icon-mail-open{background-position:-96px -96px}.ui-icon-suitcase{background-position:-112px -96px}.ui-icon-comment{background-position:-128px -96px}.ui-icon-person{background-position:-144px -96px}.ui-icon-print{background-position:-160px -96px}.ui-icon-trash{background-position:-176px -96px}.ui-icon-locked{background-position:-192px -96px}.ui-icon-unlocked{background-position:-208px -96px}.ui-icon-bookmark{background-position:-224px -96px}.ui-icon-tag{background-position:-240px -96px}.ui-icon-home{background-position:0 -112px}.ui-icon-flag{background-position:-16px -112px}.ui-icon-calendar{background-position:-32px -112px}.ui-icon-cart{background-position:-48px -112px}.ui-icon-pencil{background-position:-64px -112px}.ui-icon-clock{background-position:-80px -112px}.ui-icon-disk{background-position:-96px -112px}.ui-icon-calculator{background-position:-112px -112px}.ui-icon-zoomin{background-position:-128px -112px}.ui-icon-zoomout{background-position:-144px -112px}.ui-icon-search{background-position:-160px -112px}.ui-icon-wrench{background-position:-176px -112px}.ui-icon-gear{background-position:-192px -112px}.ui-icon-heart{background-position:-208px -112px}.ui-icon-star{background-position:-224px -112px}.ui-icon-link{background-position:-240px -112px}.ui-icon-cancel{background-position:0 -128px}.ui-icon-plus{background-position:-16px -128px}.ui-icon-plusthick{background-position:-32px -128px}.ui-icon-minus{background-position:-48px -128px}.ui-icon-minusthick{background-position:-64px -128px}.ui-icon-close{background-position:-80px -128px}.ui-icon-closethick{background-position:-96px -128px}.ui-icon-key{background-position:-112px -128px}.ui-icon-lightbulb{background-position:-128px -128px}.ui-icon-scissors{background-position:-144px -128px}.ui-icon-clipboard{background-position:-160px -128px}.ui-icon-copy{background-position:-176px -128px}.ui-icon-contact{background-position:-192px -128px}.ui-icon-image{background-position:-208px -128px}.ui-icon-video{background-position:-224px -128px}.ui-icon-script{background-position:-240px -128px}.ui-icon-alert{background-position:0 -144px}.ui-icon-info{background-position:-16px -144px}.ui-icon-notice{background-position:-32px -144px}.ui-icon-help{background-position:-48px -144px}.ui-icon-check{background-position:-64px -144px}.ui-icon-bullet{background-position:-80px -144px}.ui-icon-radio-on{background-position:-96px -144px}.ui-icon-radio-off{background-position:-112px -144px}.ui-icon-pin-w{background-position:-128px -144px}.ui-icon-pin-s{background-position:-144px -144px}.ui-icon-play{background-position:0 -160px}.ui-icon-pause{background-position:-16px -160px}.ui-icon-seek-next{background-position:-32px -160px}.ui-icon-seek-prev{background-position:-48px -160px}.ui-icon-seek-end{background-position:-64px -160px}.ui-icon-seek-start{background-position:-80px -160px}.ui-icon-seek-first{background-position:-80px -160px}.ui-icon-stop{background-position:-96px -160px}.ui-icon-eject{background-position:-112px -160px}.ui-icon-volume-off{background-position:-128px -160px}.ui-icon-volume-on{background-position:-144px -160px}.ui-icon-power{background-position:0 -176px}.ui-icon-signal-diag{background-position:-16px -176px}.ui-icon-signal{background-position:-32px -176px}.ui-icon-battery-0{background-position:-48px -176px}.ui-icon-battery-1{background-position:-64px -176px}.ui-icon-battery-2{background-position:-80px -176px}.ui-icon-battery-3{background-position:-96px -176px}.ui-icon-circle-plus{background-position:0 -192px}.ui-icon-circle-minus{background-position:-16px -192px}.ui-icon-circle-close{background-position:-32px -192px}.ui-icon-circle-triangle-e{background-position:-48px -192px}.ui-icon-circle-triangle-s{background-position:-64px -192px}.ui-icon-circle-triangle-w{background-position:-80px -192px}.ui-icon-circle-triangle-n{background-position:-96px -192px}.ui-icon-circle-arrow-e{background-position:-112px -192px}.ui-icon-circle-arrow-s{background-position:-128px -192px}.ui-icon-circle-arrow-w{background-position:-144px -192px}.ui-icon-circle-arrow-n{background-position:-160px -192px}.ui-icon-circle-zoomin{background-position:-176px -192px}.ui-icon-circle-zoomout{background-position:-192px -192px}.ui-icon-circle-check{background-position:-208px -192px}.ui-icon-circlesmall-plus{background-position:0 -208px}.ui-icon-circlesmall-minus{background-position:-16px -208px}.ui-icon-circlesmall-close{background-position:-32px -208px}.ui-icon-squaresmall-plus{background-position:-48px -208px}.ui-icon-squaresmall-minus{background-position:-64px -208px}.ui-icon-squaresmall-close{background-position:-80px -208px}.ui-icon-grip-dotted-vertical{background-position:0 -224px}.ui-icon-grip-dotted-horizontal{background-position:-16px -224px}.ui-icon-grip-solid-vertical{background-position:-32px -224px}.ui-icon-grip-solid-horizontal{background-position:-48px -224px}.ui-icon-gripsmall-diagonal-se{background-position:-64px -224px}.ui-icon-grip-diagonal-se{background-position:-80px -224px}.ui-corner-all,.ui-corner-top,.ui-corner-left,.ui-corner-tl{-moz-border-radius-topleft:6px;-webkit-border-top-left-radius:6px;-khtml-border-top-left-radius:6px;border-top-left-radius:6px}.ui-corner-all,.ui-corner-top,.ui-corner-right,.ui-corner-tr{-moz-border-radius-topright:6px;-webkit-border-top-right-radius:6px;-khtml-border-top-right-radius:6px;border-top-right-radius:6px}.ui-corner-all,.ui-corner-bottom,.ui-corner-left,.ui-corner-bl{-moz-border-radius-bottomleft:6px;-webkit-border-bottom-left-radius:6px;-khtml-border-bottom-left-radius:6px;border-bottom-left-radius:6px}.ui-corner-all,.ui-corner-bottom,.ui-corner-right,.ui-corner-br{-moz-border-radius-bottomright:6px;-webkit-border-bottom-right-radius:6px;-khtml-border-bottom-right-radius:6px;border-bottom-right-radius:6px}#simplemodal-overlay{background-color:#000}#simplemodal-container{height:360px;width:600px;color:#fff;background-color:#000;border:0;padding:0}#simplemodal-container .simplemodal-data{padding:20px 50px}.slick-slider{position:relative;display:block;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-touch-callout:none;-webkit-user-select:none;-khtml-user-select:none;-moz-user-select:none;-ms-user-select:none;user-select:none;-ms-touch-action:pan-y;touch-action:pan-y;-webkit-tap-highlight-color:transparent}.slick-list{position:relative;overflow:hidden;display:block;margin:0;padding:0}.slick-list:focus{outline:none}.slick-loading .slick-list{background:#fff url("https://www.jpl.nasa.gov/assets/stylesheets/./ajax-loader.gif") center center no-repeat}.slick-list.dragging{cursor:pointer;cursor:hand}.slick-slider .slick-list,.slick-track,.slick-slide,.slick-slide img{-webkit-transform:translate3d(0, 0, 0);-moz-transform:translate3d(0, 0, 0);-ms-transform:translate3d(0, 0, 0);-o-transform:translate3d(0, 0, 0);transform:translate3d(0, 0, 0)}.slick-track{position:relative;left:0;top:0;display:block;zoom:1}.slick-track:before,.slick-track:after{content:"";display:table}.slick-track:after{clear:both}.slick-loading .slick-track{visibility:hidden}.slick-slide{float:left;height:100%;min-height:1px;display:none}.slick-slide img{display:block}.slick-slide.slick-loading img{display:none}.slick-slide.dragging img{pointer-events:none}.slick-initialized .slick-slide{display:block}.slick-loading .slick-slide{visibility:hidden}.slick-vertical .slick-slide{display:block;height:auto;border:1px solid transparent}@font-face{font-family:"slick";src:url("https://www.jpl.nasa.gov/assets/stylesheets/./fonts/slick.eot");src:url("https://www.jpl.nasa.gov/assets/stylesheets/./fonts/slick.eot?#iefix") format("embedded-opentype"),url("https://www.jpl.nasa.gov/assets/stylesheets/./fonts/slick.woff") format("woff"),url("https://www.jpl.nasa.gov/assets/stylesheets/./fonts/slick.ttf") format("truetype"),url("https://www.jpl.nasa.gov/assets/stylesheets/./fonts/slick.svg#slick") format("svg");font-weight:normal;font-style:normal}.slick-prev,.slick-next{position:absolute;display:block;height:20px;width:20px;line-height:0;font-size:0;cursor:pointer;background:transparent;color:transparent;top:50%;margin-top:-10px;padding:0;border:none;outline:none}.slick-prev:hover,.slick-prev:focus,.slick-next:hover,.slick-next:focus{outline:none;background:transparent;color:transparent}.slick-prev:hover:before,.slick-prev:focus:before,.slick-next:hover:before,.slick-next:focus:before{opacity:1}.slick-prev.slick-disabled:before,.slick-next.slick-disabled:before{opacity:0.25}.slick-prev:before,.slick-next:before{font-family:"slick";font-size:20px;line-height:1;color:white;opacity:0.75;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale}.slick-prev{left:-25px}.slick-prev:before{content:"\2190"}.slick-next{right:-25px}.slick-next:before{content:"\2192"}.slick-slider{margin-bottom:30px}.slick-dots{position:absolute;bottom:-45px;list-style:none;display:block;text-align:center;padding:0;width:100%}.slick-dots li{position:relative;display:inline-block;height:20px;width:20px;margin:0 5px;padding:0;cursor:pointer}.slick-dots li button{border:0;background:transparent;display:block;height:20px;width:20px;outline:none;line-height:0;font-size:0;color:transparent;padding:5px;cursor:pointer}.slick-dots li button:hover,.slick-dots li button:focus{outline:none}.slick-dots li button:hover:before,.slick-dots li button:focus:before{opacity:1}.slick-dots li button:before{position:absolute;top:0;left:0;content:"\2022";width:20px;height:20px;font-family:"slick";font-size:6px;line-height:20px;text-align:center;color:black;opacity:0.25;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale}.slick-dots li.slick-active button:before{color:black;opacity:0.75}[dir="rtl"] .slick-next{right:auto;left:-25px}[dir="rtl"] .slick-next:before{content:"\2190"}[dir="rtl"] .slick-prev{right:-25px;left:auto}[dir="rtl"] .slick-prev:before{content:"\2192"}[dir="rtl"] .slick-slide{float:right}*,*:before,*:after{-moz-box-sizing:border-box;-webkit-box-sizing:border-box;box-sizing:border-box}html,html a,select,input{-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;text-rendering:optimizeLegibility}input.placeholder,textarea.placeholder{-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;text-rendering:optimizeLegibility}input:-moz-placeholder,textarea:-moz-placeholder{-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;text-rendering:optimizeLegibility}input::-moz-placeholder,textarea::-moz-placeholder{-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;text-rendering:optimizeLegibility}input::-webkit-input-placeholder,textarea::-webkit-input-placeholder{-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;text-rendering:optimizeLegibility}html,button,input,select,textarea{font-family:Helvetica, Arial, sans-serif}html{min-height:100%;-webkit-text-size-adjust:100%}body{font-family:Helvetica, Arial, sans-serif;font-size:96%;line-height:1.4;min-height:100%;position:relative}body.noscroll{overflow:hidden}@media (min-width: 600px){body{font-size:98%}}@media (min-width: 769px){body{font-size:100%}}@media (min-width: 1024px){body{font-size:102%}}@media (min-width: 1200px){body{font-size:104%}}h1{letter-spacing:-.03em}@media (min-width: 769px){h1{letter-spacing:-.04em}}h2{letter-spacing:-.02em}@media (min-width: 769px){h2{letter-spacing:-.03em}}h3{letter-spacing:-.01em}@media (min-width: 769px){h3{letter-spacing:-.02em}}h4{letter-spacing:-.01em}a{color:#0e7ee0;text-decoration:none}img{width:100%}i{font-style:italic}strong{font-weight:600}p{margin:1em 0}article{overflow:hidden;*zoom:1}@media (min-width: 769px){.mobile_only{display:none !important}}.gradient_line{margin-left:auto;margin-right:auto;content:" ";width:100%;height:1px;clear:both;background:#777777;background:-moz-linear-gradient(left, transparent, #777, transparent);background:-webkit-linear-gradient(left, transparent, #777, transparent);background:linear-gradient(to right, transparent, #777, transparent)}.scrollblock{background-color:white;z-index:10;position:relative;padding-top:0}ul.articles,.gallery_list{overflow:hidden;*zoom:1;margin-bottom:3em}ul.articles li,.gallery_list li{position:relative}.print_only{display:none}.module_title,.module_title_small,.media_feature_title,.sitemap_title,.nav_title,.article_title,.sidebar_title,.rollover_title{letter-spacing:-.04em}.module_title{letter-spacing:-.04em}.rollover_title{font-size:2.34em;margin-bottom:0em}@media (min-width: 600px){.rollover_title{font-size:2.7em;margin-bottom:0em}}@media (min-width: 769px){.rollover_title{font-size:3.06em;margin-bottom:0em}}@media (min-width: 1024px){.rollover_title{font-size:3.24em;margin-bottom:0em}}@media (min-width: 1200px){.rollover_title{font-size:3.42em;margin-bottom:0em}}.content_title{letter-spacing:0;font-weight:600}.module_title{font-size:1.82em;margin-bottom:0.3em;text-align:center;font-weight:700}@media (min-width: 600px){.module_title{font-size:2.1em;margin-bottom:0.54em}}@media (min-width: 769px){.module_title{font-size:2.38em;margin-bottom:0.78em}}@media (min-width: 1024px){.module_title{font-size:2.52em;margin-bottom:0.87em}}@media (min-width: 1200px){.module_title{font-size:2.66em;margin-bottom:0.96em}}@media (min-width: 600px){.grid_gallery .module_title{text-align:left;width:80%}}.module_title_small{font-size:1.4em;font-weight:700;display:inline-block}@media (min-width: 600px){.module_title_small{font-size:1.8em}}.filter_bar .module_title_small{text-align:left;width:90%}@media (min-width: 600px){.filter_bar .module_title_small{text-align:center}}.category_title{font-size:.9em;font-weight:600;color:#71a3d5;text-transform:uppercase;margin-bottom:6px}.multimedia_teaser .category_title{font-size:.8em}.primary_media_feature .media_feature_title{font-size:1.82em;margin-bottom:0em;font-weight:700;color:white}@media (min-width: 600px){.primary_media_feature .media_feature_title{font-size:2.1em;margin-bottom:0em}}@media (min-width: 769px){.primary_media_feature .media_feature_title{font-size:2.38em;margin-bottom:0em}}@media (min-width: 1024px){.primary_media_feature .media_feature_title{font-size:2.52em;margin-bottom:0em}}@media (min-width: 1200px){.primary_media_feature .media_feature_title{font-size:2.66em;margin-bottom:0em}}.media_feature .media_feature_title{font-size:1.43em;margin-bottom:0em;font-weight:700;color:white}@media (min-width: 600px){.media_feature .media_feature_title{font-size:1.65em;margin-bottom:0em}}@media (min-width: 769px){.media_feature .media_feature_title{font-size:1.87em;margin-bottom:0em}}@media (min-width: 1024px){.media_feature .media_feature_title{font-size:1.98em;margin-bottom:0em}}@media (min-width: 1200px){.media_feature .media_feature_title{font-size:2.09em;margin-bottom:0em}}.multimedia_module_gallery .media_feature_title{font-size:1.43em;margin-bottom:0em;color:white;font-weight:700}@media (min-width: 600px){.multimedia_module_gallery .media_feature_title{font-size:1.65em;margin-bottom:0em}}@media (min-width: 769px){.multimedia_module_gallery .media_feature_title{font-size:1.87em;margin-bottom:0em}}@media (min-width: 1024px){.multimedia_module_gallery .media_feature_title{font-size:1.98em;margin-bottom:0em}}@media (min-width: 1200px){.multimedia_module_gallery .media_feature_title{font-size:2.09em;margin-bottom:0em}}.article_title{font-size:1.82em;margin-bottom:0em;font-weight:700}@media (min-width: 600px){.article_title{font-size:2.1em;margin-bottom:0em}}@media (min-width: 769px){.article_title{font-size:2.38em;margin-bottom:0em}}@media (min-width: 1024px){.article_title{font-size:2.52em;margin-bottom:0em}}@media (min-width: 1200px){.article_title{font-size:2.66em;margin-bottom:0em}}.sidebar_title{font-size:1.55em;margin-bottom:0.6em;font-weight:700;margin-left:-1px}.links_module a{font-size:.9em;cursor:pointer}.site_header_area{position:absolute;width:100%;z-index:2000;height:70px;transition:background-color .5s ease-in-out}@media (min-width: 600px){.site_header_area{height:90px}}@media (min-width: 769px){.site_header_area{height:92px}}@media (min-width: 1024px){.site_header_area{height:105px}}.touch .iosWasZoomed .site_header_area{position:absolute !important;-webkit-box-shadow:none;-moz-box-shadow:none;box-shadow:none}@media screen and (orientation: portrait){.touch .site_header_area.fixed{position:fixed;background-color:#e4e9ef;-webkit-box-shadow:0 4px 4px -1px rgba(0,0,0,0.15);-moz-box-shadow:0 4px 4px -2px rgba(0,0,0,0.15);box-shadow:0 4px 4px -2px rgba(0,0,0,0.15);opacity:0}.touch .site_header_area.fixed.fixed_show{transition:opacity .5s ease-in-out;opacity:1}}.no-touch .site_header_area.fixed{position:fixed;background-color:#e4e9ef;-webkit-box-shadow:0 4px 4px -1px rgba(0,0,0,0.15);-moz-box-shadow:0 4px 4px -2px rgba(0,0,0,0.15);box-shadow:0 4px 4px -2px rgba(0,0,0,0.15);opacity:0}.no-touch .site_header_area.fixed.fixed_show{transition:opacity .5s ease-in-out;opacity:1}.site_header{clear:both;z-index:5;width:100%;height:100%;position:relative;margin:0 auto;-webkit-touch-callout:none;-webkit-user-select:none;-khtml-user-select:none;-moz-user-select:-moz-none;-ms-user-select:none;user-select:none;padding:.8em 0 0 .5em}@media (min-width: 600px){.site_header{padding:1em 0 0 1.2em}}@media (min-width: 769px){.site_header{padding:1.1em 0 0 1.5em}}@media (min-width: 1024px){.site_header{padding:1.1em 0 0 2em}}.site_header .brand_area{position:relative;background:url("https://www.jpl.nasa.gov/assets/images/logo_nasa_trio_white@2x.png") no-repeat;background-size:100%;z-index:300;display:inline-block;width:250px;height:56px}@media (min-width: 600px){.site_header .brand_area{width:330px;height:64px}}@media (min-width: 769px){.site_header .brand_area{margin:0}}@media (min-width: 1024px){.site_header .brand_area{width:362px;height:68px}}.site_header .brand_area .brand1{height:100%;width:25%;float:left}.site_header .brand_area .brand2{float:left;width:75%;height:100%}.site_header .brand_area .jpl_logo{text-indent:-9999px;width:100%;float:left;height:100%}.site_header .brand_area .caltech_logo{display:none}.site_header .brand_area .nasa_logo{text-indent:-9999px}.site_header a#jpl_logo,.site_header a#caltech_logo,.site_header a.nasa_logo{display:block;height:100%}.light_background .site_header .brand_area,.fixed .site_header .brand_area{background:url("https://www.jpl.nasa.gov/assets/images/logo_nasa_trio_black@2x.png") no-repeat;background-size:100%}.light_background .site_header .search_field,.light_background .site_header form.submit_newsletter .email_field,form.submit_newsletter .light_background .site_header .email_field,.fixed .site_header .search_field,.fixed .site_header form.submit_newsletter .email_field,form.submit_newsletter .fixed .site_header .email_field{background-color:white !important;color:#222222 !important}.light_background .site_header .search_field.placeholder,.light_background .site_header form.submit_newsletter .placeholder.email_field,form.submit_newsletter .light_background .site_header .placeholder.email_field,.fixed .site_header .search_field.placeholder,.fixed .site_header form.submit_newsletter .placeholder.email_field,form.submit_newsletter .fixed .site_header .placeholder.email_field{color:#5a6470 !important;opacity:1 !important}.light_background .site_header .search_field:-moz-placeholder,.light_background .site_header form.submit_newsletter .email_field:-moz-placeholder,form.submit_newsletter .light_background .site_header .email_field:-moz-placeholder,.fixed .site_header .search_field:-moz-placeholder,.fixed .site_header form.submit_newsletter .email_field:-moz-placeholder,form.submit_newsletter .fixed .site_header .email_field:-moz-placeholder{color:#5a6470 !important;opacity:1 !important}.light_background .site_header .search_field::-moz-placeholder,.light_background .site_header form.submit_newsletter .email_field::-moz-placeholder,form.submit_newsletter .light_background .site_header .email_field::-moz-placeholder,.fixed .site_header .search_field::-moz-placeholder,.fixed .site_header form.submit_newsletter .email_field::-moz-placeholder,form.submit_newsletter .fixed .site_header .email_field::-moz-placeholder{color:#5a6470 !important;opacity:1 !important}.light_background .site_header .search_field::-webkit-input-placeholder,.light_background .site_header form.submit_newsletter .email_field::-webkit-input-placeholder,form.submit_newsletter .light_background .site_header .email_field::-webkit-input-placeholder,.fixed .site_header .search_field::-webkit-input-placeholder,.fixed .site_header form.submit_newsletter .email_field::-webkit-input-placeholder,form.submit_newsletter .fixed .site_header .email_field::-webkit-input-placeholder{color:#5a6470 !important;opacity:1 !important}.light_background .site_header .section_search .search_submit,.light_background .site_header form.nav_search .search_submit,.light_background .site_header .overlay_search .search_submit,.light_background .site_header form.submit_newsletter .search_submit,form.submit_newsletter .light_background .site_header .section_search .email_submit,form.submit_newsletter .light_background .site_header form.nav_search .email_submit,form.submit_newsletter .light_background .site_header .overlay_search .email_submit,.light_background .site_header form.submit_newsletter .email_submit,.fixed .site_header .section_search .search_submit,.fixed .site_header form.nav_search .search_submit,.fixed .site_header .overlay_search .search_submit,.fixed .site_header form.submit_newsletter .search_submit,form.submit_newsletter .fixed .site_header .section_search .email_submit,form.submit_newsletter .fixed .site_header form.nav_search .email_submit,form.submit_newsletter .fixed .site_header .overlay_search .email_submit,.fixed .site_header form.submit_newsletter .email_submit{background:url("https://www.jpl.nasa.gov/assets/images/search_icon_darkgrey@2x.png") no-repeat 6px 9px transparent;background-size:20px}.light_background .site_header a.menu_button .menu_icon,.fixed .site_header a.menu_button .menu_icon{text-indent:-9999px;background:url("https://www.jpl.nasa.gov/assets/images/menu_icon_black@2x.png") center center no-repeat;background-size:25px 20px}@media (min-width: 600px){.light_background .site_header a.menu_button .menu_icon,.fixed .site_header a.menu_button .menu_icon{background:url("https://www.jpl.nasa.gov/assets/images/menu_button_jpl@2x.png") center center no-repeat;background-size:90%}}@media (min-width: 1200px){.light_background .site_header a.menu_button .menu_icon,.fixed .site_header a.menu_button .menu_icon{background-size:100%}}.main_nav_overlay .site_header .brand_area{background:url("https://www.jpl.nasa.gov/assets/images/logo_nasa_trio_white@2x.png") no-repeat;background-size:100%}.nav_area{position:absolute;top:1.1em;right:.3em}@media (min-width: 600px){.nav_area{top:1.7em;right:1em}}@media (min-width: 769px){.nav_area{top:1.8em}}@media (min-width: 1024px){.nav_area{top:2em}}@media (min-width: 600px){.nav_area{right:1.3em}}a.menu_button{position:relative;display:inline-block;vertical-align:middle;height:40px;padding:0.6em 1em 0;text-decoration:none}@media (min-width: 600px){a.menu_button{padding:0}}a.menu_button .menu_icon{text-indent:-9999px;display:inline-block;vertical-align:middle;width:25px;height:20px;background:url("https://www.jpl.nasa.gov/assets/images/menu_icon@2x.png") center center no-repeat;background-size:25px 20px}@media (min-width: 600px){a.menu_button .menu_icon{background:url("https://www.jpl.nasa.gov/assets/images/menu_button_jpl@2x.png") center center no-repeat;background-size:90%;width:140px;height:43px}}@media (min-width: 1200px){a.menu_button .menu_icon{background-size:100%}}a.menu_button .menu_label{display:none}@media (min-width: 769px){a.menu_button .menu_label{top:.1em;margin-left:.3em;position:relative;text-transform:uppercase;color:white}}.header_mask{background-color:#e4e9ef;height:70px}@media (min-width: 600px){.header_mask{height:90px}}@media (min-width: 769px){.header_mask{height:92px}}@media (min-width: 1024px){.header_mask{height:105px}}#home.no_background .header_mask,#home.dark_background .header_mask{display:none}#home.light_background .header_mask{position:absolute;top:0;left:0;display:block;z-index:1;width:100%;opacity:.5}.main_nav_overlay{display:none;position:absolute;top:0;left:0;min-height:100%;width:100%;z-index:210000;position:fixed;-ms-overflow-style:none;height:100%;overflow-y:scroll;-webkit-overflow-scrolling:touch;background-color:#395069;background-color:rgba(57,80,105,0.99)}.main_nav_overlay::-webkit-scrollbar{display:none}.main_nav_overlay .site_header{position:relative;margin-bottom:0;background-color:#395069;background-color:rgba(57,80,105,0.99);height:70px}@media (min-width: 600px){.main_nav_overlay .site_header{height:90px}}@media (min-width: 769px){.main_nav_overlay .site_header{height:92px}}@media (min-width: 1024px){.main_nav_overlay .site_header{height:105px}}.main_nav_overlay .navigation_area{margin-bottom:4em;padding-top:0;padding-bottom:2em;text-align:center}@media (min-width: 769px){.main_nav_overlay .navigation_area{padding-bottom:3em}}.main_nav_overlay #modal_close{display:block;text-indent:-9999px;width:57px;height:44px;background:url("https://www.jpl.nasa.gov/assets/images/close_x_icon_thick@2x.png") center no-repeat;background-size:31px 30px;cursor:pointer;position:absolute;top:1.1em;right:.3em}@media (min-width: 600px){.main_nav_overlay #modal_close{top:1.7em;right:1em}}@media (min-width: 769px){.main_nav_overlay #modal_close{top:1.8em}}@media (min-width: 1024px){.main_nav_overlay #modal_close{top:2em}}.main_nav_overlay .nav_area{display:none}.main_nav_overlay .arrow_box .arrow_down{display:none}.main_nav_overlay .nav_item{text-align:center;margin:1.5em auto 2em;text-transform:capitalize;-webkit-touch-callout:none;-webkit-user-select:none;-khtml-user-select:none;-moz-user-select:-moz-none;-ms-user-select:none;user-select:none}@media (min-width: 769px){.main_nav_overlay .nav_item{margin:.6em auto 2em}}.main_nav_overlay .nav_item:first-child{margin-top:0}.main_nav_overlay .nav_item .nav_title{padding:.28em 0;font-weight:600;color:white}.main_nav_overlay .nav_item .nav_title a{color:white}@media (min-width: 769px){.main_nav_overlay .nav_item .nav_title{padding:.8em 0 .4em}}.main_nav_overlay .nav_item .subnav li{font-weight:600;white-space:nowrap}.main_nav_overlay .nav_item a{color:#a5a6a7;text-decoration:none}.no-touch .main_nav_overlay .nav_item a:hover{color:white}.main_nav_overlay .nav_item .social_icons{padding-top:.5em}.main_nav_overlay .overlay_search{width:250px}.main_nav_overlay .overlay_search .search_field,.main_nav_overlay .overlay_search form.submit_newsletter .email_field,form.submit_newsletter .main_nav_overlay .overlay_search .email_field{width:100%;font-size:16px}@media (min-width: 600px){.main_nav_overlay .overlay_search{width:320px}}.main_nav_overlay .gradient_line{margin-left:auto;margin-right:auto;content:" ";width:100%;height:1px;clear:both;background:#61b6fd;background:-moz-linear-gradient(left, rgba(97,182,253,0), #61b6fd, rgba(97,182,253,0));background:-webkit-linear-gradient(left, rgba(97,182,253,0), #61b6fd, rgba(97,182,253,0));background:linear-gradient(to right, rgba(97,182,253,0), #61b6fd, rgba(97,182,253,0));width:50%}@media (min-width: 769px){.main_nav_overlay .gradient_line{width:25%}}@media (max-width: 768px){.main_nav_overlay .navigation_area{padding:0 2% 2em 2.8%}.main_nav_overlay .nav_item{text-align:left;margin:1em 0 .5em}.main_nav_overlay .nav_item.centered{text-align:center}.main_nav_overlay .nav_item.centered .nav_title{text-align:center;width:100%}.main_nav_overlay .nav_item .social_icons{margin-bottom:1.8em}.main_nav_overlay .gradient_line{width:100%}.main_nav_overlay .nav_title{margin-bottom:0;display:block;line-height:1.4em;font-weight:600;text-align:left;width:80%;font-size:1.2em;letter-spacing:-.01em;cursor:pointer;-webkit-tap-highlight-color:rgba(255,255,255,0);-webkit-tap-highlight-color:transparent}.main_nav_overlay .subnav{display:none;margin-bottom:.8em}.main_nav_overlay .subnav li{padding:.28em 0;display:block !important;font-size:1em}.main_nav_overlay .subnav li a{font-size:1em}.main_nav_overlay .overlay_search.top_search{margin:.7em 0 .5em;display:none}.main_nav_overlay .arrow_box{padding:20px 20px;width:52px;float:right;cursor:pointer;margin:-0.4em -.8em 0 0;display:block;text-align:center;-webkit-tap-highlight-color:rgba(255,255,255,0);-webkit-tap-highlight-color:transparent}.main_nav_overlay .arrow_box.reverse{transform:rotate(180deg);-ms-filter:"progid:DXImageTransform.Microsoft.Matrix(M11=-1, M12=1.2246063538223773e-16, M21=-1.2246063538223773e-16, M22=-1, SizingMethod='auto expand')"}.main_nav_overlay .arrow_box .arrow_down{display:block;width:0;height:0;border-left:6px solid rgba(255,255,255,0);border-right:6px solid rgba(255,255,255,0);border-top:8px solid #fff;float:right}}@media (min-width: 769px){.main_nav_overlay .nav_item{cursor:default}.main_nav_overlay .nav_title{font-size:2.05em;letter-spacing:-.02em}.main_nav_overlay .subnav{display:block !important}.main_nav_overlay .subnav li{display:inline-block !important;padding:.28em 1em}.main_nav_overlay .subnav li a{font-size:1.15em}}@media (min-width: 769px) and (min-width: 1024px){.main_nav_overlay .subnav li a{font-size:1.25em}}@media (min-width: 769px){.main_nav_overlay .overlay_search.top_search{margin:2em 0 1em}}.gradient_container_top,.gradient_container_bottom{height:200px;width:100%;position:absolute;z-index:1}.primary_media_feature.homepage_carousel .gradient_container_top,.primary_media_feature.homepage_carousel .gradient_container_bottom{z-index:7}.gradient_container_top{background:url('data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4gPHN2ZyB2ZXJzaW9uPSIxLjEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+PGRlZnM+PGxpbmVhckdyYWRpZW50IGlkPSJncmFkIiBncmFkaWVudFVuaXRzPSJvYmplY3RCb3VuZGluZ0JveCIgeDE9IjAuNSIgeTE9IjAuMCIgeDI9IjAuNSIgeTI9IjEuMCI+PHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwMDAwMCIgc3RvcC1vcGFjaXR5PSIwLjYiLz48c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwMDAwMDAiIHN0b3Atb3BhY2l0eT0iMC4wIi8+PC9saW5lYXJHcmFkaWVudD48L2RlZnM+PHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgZmlsbD0idXJsKCNncmFkKSIgLz48L3N2Zz4g');background:-webkit-gradient(linear, 50% 0%, 50% 100%, color-stop(0%, rgba(0,0,0,0.6)), color-stop(100%, transparent));background:-moz-linear-gradient(rgba(0,0,0,0.6), transparent);background:-webkit-linear-gradient(rgba(0,0,0,0.6), transparent);background:linear-gradient(rgba(0,0,0,0.6), transparent);top:0}.light_background .gradient_container_top{display:none}.no_background .gradient_container_top{background:none}.gradient_container_bottom{background:url('data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4gPHN2ZyB2ZXJzaW9uPSIxLjEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+PGRlZnM+PGxpbmVhckdyYWRpZW50IGlkPSJncmFkIiBncmFkaWVudFVuaXRzPSJvYmplY3RCb3VuZGluZ0JveCIgeDE9IjAuNSIgeTE9IjAuMCIgeDI9IjAuNSIgeTI9IjEuMCI+PHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwMDAwMCIgc3RvcC1vcGFjaXR5PSIwLjAiLz48c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwMDAwMDAiIHN0b3Atb3BhY2l0eT0iMC42Ii8+PC9saW5lYXJHcmFkaWVudD48L2RlZnM+PHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgZmlsbD0idXJsKCNncmFkKSIgLz48L3N2Zz4g');background:-webkit-gradient(linear, 50% 0%, 50% 100%, color-stop(0%, transparent), color-stop(100%, rgba(0,0,0,0.6)));background:-moz-linear-gradient(transparent, rgba(0,0,0,0.6));background:-webkit-linear-gradient(transparent, rgba(0,0,0,0.6));background:linear-gradient(transparent, rgba(0,0,0,0.6));bottom:0}.gradient_bottom_grid,.gradient_bottom_teasers,.grid_gallery.grid_view .bottom_gradient{background-image:url('data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4gPHN2ZyB2ZXJzaW9uPSIxLjEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+PGRlZnM+PGxpbmVhckdyYWRpZW50IGlkPSJncmFkIiBncmFkaWVudFVuaXRzPSJvYmplY3RCb3VuZGluZ0JveCIgeDE9IjAuNSIgeTE9IjAuMCIgeDI9IjAuNSIgeTI9IjEuMCI+PHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwMDAwMCIgc3RvcC1vcGFjaXR5PSIwLjAiLz48c3RvcCBvZmZzZXQ9IjMwJSIgc3RvcC1jb2xvcj0iIzAwMDAwMCIvPjxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0iIzAwMDAwMCIvPjwvbGluZWFyR3JhZGllbnQ+PC9kZWZzPjxyZWN0IHg9IjAiIHk9IjAiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIGZpbGw9InVybCgjZ3JhZCkiIC8+PC9zdmc+IA==');background-size:100%;background-image:-webkit-gradient(linear, 50% 0%, 50% 100%, color-stop(0%, transparent), color-stop(30%, #000), color-stop(100%, #000));background-image:-moz-linear-gradient(top, transparent 0%, #000 30%, #000 100%);background-image:-webkit-linear-gradient(top, transparent 0%, #000 30%, #000 100%);background-image:linear-gradient(to bottom, transparent 0%, #000 30%, #000 100%)}.ie9 .gradient_bottom_grid,.ie9 .gradient_bottom_teasers,.ie9 .grid_gallery.grid_view .bottom_gradient,.grid_gallery.grid_view .ie9 .bottom_gradient{filter:none;background:url(data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiA/Pgo8c3ZnIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgdmlld0JveD0iMCAwIDEgMSIgcHJlc2VydmVBc3BlY3RSYXRpbz0ibm9uZSI+CiAgPGxpbmVhckdyYWRpZW50IGlkPSJncmFkLXVjZ2ctZ2VuZXJhdGVkIiBncmFkaWVudFVuaXRzPSJ1c2VyU3BhY2VPblVzZSIgeDE9IjAlIiB5MT0iMCUiIHgyPSIwJSIgeTI9IjEwMCUiPgogICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwMDAwMCIgc3RvcC1vcGFjaXR5PSIwIi8+CiAgICA8c3RvcCBvZmZzZXQ9IjQ4JSIgc3RvcC1jb2xvcj0iIzAwMDAwMCIgc3RvcC1vcGFjaXR5PSIxIi8+CiAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwMDAwMDAiIHN0b3Atb3BhY2l0eT0iMSIvPgogIDwvbGluZWFyR3JhZGllbnQ+CiAgPHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9IjEiIGhlaWdodD0iMSIgZmlsbD0idXJsKCNncmFkLXVjZ2ctZ2VuZXJhdGVkKSIgLz4KPC9zdmc+)}.gradient_bottom_teasers{width:100%;height:38%;position:absolute;bottom:0}.primary_media_feature{margin-bottom:0}@media (min-width: 769px){.primary_media_feature{padding:0}}.primary_media_feature #masterslider .ms-nav-next,.primary_media_feature #masterslider .ms-nav-prev{display:none}@media (min-width: 769px){.primary_media_feature #masterslider .ms-nav-next,.primary_media_feature #masterslider .ms-nav-prev{display:block}}.primary_media_feature #masterslider .ms-nav-prev,.primary_media_feature #masterslider .ms-nav-next{width:40px;height:80px;margin-top:-60px}@media (min-width: 769px){.primary_media_feature #masterslider .ms-nav-prev,.primary_media_feature #masterslider .ms-nav-next{margin-top:-80px}}.primary_media_feature #masterslider .ms-nav-prev{background:url("https://www.jpl.nasa.gov/assets/images/arrow_left_darktheme.png");background-size:40px 95px;background-color:rgba(32,32,32,0.9);background-position:0;left:0;border-top-right-radius:6px;border-bottom-right-radius:6px}.primary_media_feature #masterslider .ms-nav-next{background:url("https://www.jpl.nasa.gov/assets/images/arrow_right_darktheme.png");background-size:40px 95px;background-color:rgba(32,32,32,0.9);background-position:0;right:0;border-top-left-radius:6px;border-bottom-left-radius:6px}.primary_media_feature #masterslider .ms-bullets{bottom:60px;z-index:10}@media (min-width: 600px){.primary_media_feature #masterslider .ms-bullets{bottom:90px}}@media (min-width: 769px){.primary_media_feature #masterslider .ms-bullets{bottom:110px}}.primary_media_feature #masterslider .ms-bullet{background-color:white;background-image:none;border-radius:50% 50% 50% 50%;height:8px;width:8px;opacity:0.5;margin:0 10px}.primary_media_feature #masterslider .ms-bullet:hover{opacity:1.0}.primary_media_feature #masterslider .ms-bullet-selected{opacity:1.0}.primary_media_feature.single{position:relative;margin-bottom:0;overflow:hidden}.primary_media_feature.single .carousel_item{height:300px;background-size:cover;position:relative;z-index:3;background-position:center}@media (min-width: 769px){.primary_media_feature.single .carousel_item{height:700px}}.primary_media_feature.single.video .play{display:none;position:absolute;top:47%;left:47%;top:calc(50%- 30px);left:calc(50%- 30px);top:-webkit-calc(50% - 30px);left:-webkit-calc(50% - 30px);width:60px;height:60px;padding-top:0;cursor:pointer;background:url("https://www.jpl.nasa.gov/assets/images/play-button.png") 0 0 no-repeat;z-index:10}.primary_media_feature.single.video .player{width:100%;height:100%;position:absolute;top:0;left:0;z-index:2}.primary_media_feature.homepage_carousel{margin-bottom:0}.primary_media_feature.homepage_carousel .main_feature{height:482px}@media only screen and (orientation: landscape){.primary_media_feature.homepage_carousel .main_feature{height:260px}}@media (min-width: 600px){.primary_media_feature.homepage_carousel .main_feature{height:420px}}@media only screen and (min-width: 600px) and (orientation: landscape){.primary_media_feature.homepage_carousel .main_feature{height:400px}}@media (min-width: 769px){.primary_media_feature.homepage_carousel .main_feature{height:400px}}@media only screen and (min-width: 769px) and (orientation: landscape){.primary_media_feature.homepage_carousel .main_feature{height:400px}}@media (min-width: 1024px){.primary_media_feature.homepage_carousel .main_feature{height:440px}}@media (min-width: 1200px){.primary_media_feature.homepage_carousel .main_feature{height:550px}}@media (min-width: 1700px){.primary_media_feature.homepage_carousel .main_feature{height:660px}}.primary_media_feature.homepage_carousel #masterslider{width:100%;height:100%}@media (min-width: 600px){.primary_media_feature.homepage_carousel{margin-bottom:-20px}}@media (min-width: 769px){.primary_media_feature.homepage_carousel{margin-bottom:-40px}}@media (min-width: 769px){.primary_media_feature.homepage_carousel .gradient_container_bottom{bottom:40px}}#home #site_nav_down{cursor:pointer;position:absolute;top:-32px;display:block;width:60px;height:40px;left:50%;margin-left:-30px;z-index:21}@media (min-width: 769px){#home #site_nav_down{top:-45px}}#home .site_nav_down_prompt{display:none}@media (min-width: 769px){#home .site_nav_down_prompt{display:block;position:absolute;top:.4em;z-index:20;width:100%;left:0;background-color:transparent !important;color:black;font-size:1.5em;text-align:center;font-weight:400;padding:18px 0;cursor:pointer;opacity:1;transition:opacity .5s ease-in}#home .site_nav_down_prompt span{color:#0e7ee0}#home .site_nav_down_prompt.hide{opacity:0}}#home .pointer_mask{height:25px;z-index:18;position:relative;top:-24px;width:100%}@media (min-width: 769px){#home .pointer_mask{height:40px;top:-38px}}#home .pointer_mask .arrow_masks{border-right:20px solid white;border-top:20px solid white;border-left:20px solid white;border-bottom:0px;display:inline-block;width:calc(50% - 20px);width:-webkit-calc(50% - 20px);height:100%;background-color:white}#home .pointer_mask .arrow_mask{display:inline-block;width:20px;height:100%;border-right:20px solid white;border-top:20px solid transparent;border-left:20px solid white;border-bottom:0px solid white}@media (min-width: 769px){#home .pointer_mask .arrow_mask{border-bottom:20px solid white}}.light_background .site_header form.nav_search,.section_search,.site_header form.nav_search,.overlay_search,form.submit_newsletter{color:white;display:inline-block;position:relative}.section_search .search_field,.site_header form.nav_search .search_field,.overlay_search .search_field,form.submit_newsletter .search_field,form.submit_newsletter .email_field{color:white;background-color:rgba(255,255,255,0.3)}.section_search .search_field.placeholder,.site_header form.nav_search .search_field.placeholder,.overlay_search .search_field.placeholder,form.submit_newsletter .search_field.placeholder,form.submit_newsletter .placeholder.email_field{color:white;-webkit-font-smoothing:antialiased}.section_search .search_field:-moz-placeholder,.site_header form.nav_search .search_field:-moz-placeholder,.overlay_search .search_field:-moz-placeholder,form.submit_newsletter .search_field:-moz-placeholder,form.submit_newsletter .email_field:-moz-placeholder{color:white;-webkit-font-smoothing:antialiased}.section_search .search_field::-moz-placeholder,.site_header form.nav_search .search_field::-moz-placeholder,.overlay_search .search_field::-moz-placeholder,form.submit_newsletter .search_field::-moz-placeholder,form.submit_newsletter .email_field::-moz-placeholder{color:white;-webkit-font-smoothing:antialiased}.section_search .search_field::-webkit-input-placeholder,.site_header form.nav_search .search_field::-webkit-input-placeholder,.overlay_search .search_field::-webkit-input-placeholder,form.submit_newsletter .search_field::-webkit-input-placeholder,form.submit_newsletter .email_field::-webkit-input-placeholder{color:white;-webkit-font-smoothing:antialiased}.section_search .search_field,.site_header form.nav_search .search_field,.overlay_search .search_field,form.submit_newsletter .search_field,form.submit_newsletter .email_field{font-size:16px;border:none;border-radius:4px;height:40px;padding-left:1.1em;padding-right:40px;padding-top:.2em}.section_search .search_field.placeholder,.site_header form.nav_search .search_field.placeholder,.overlay_search .search_field.placeholder,form.submit_newsletter .search_field.placeholder,form.submit_newsletter .placeholder.email_field{opacity:1 !important;font-family:Helvetica, Arial, sans-serif}.section_search .search_field:-moz-placeholder,.site_header form.nav_search .search_field:-moz-placeholder,.overlay_search .search_field:-moz-placeholder,form.submit_newsletter .search_field:-moz-placeholder,form.submit_newsletter .email_field:-moz-placeholder{opacity:1 !important;font-family:Helvetica, Arial, sans-serif}.section_search .search_field::-moz-placeholder,.site_header form.nav_search .search_field::-moz-placeholder,.overlay_search .search_field::-moz-placeholder,form.submit_newsletter .search_field::-moz-placeholder,form.submit_newsletter .email_field::-moz-placeholder{opacity:1 !important;font-family:Helvetica, Arial, sans-serif}.section_search .search_field::-webkit-input-placeholder,.site_header form.nav_search .search_field::-webkit-input-placeholder,.overlay_search .search_field::-webkit-input-placeholder,form.submit_newsletter .search_field::-webkit-input-placeholder,form.submit_newsletter .email_field::-webkit-input-placeholder{opacity:1 !important;font-family:Helvetica, Arial, sans-serif}.section_search .search_submit,.site_header form.nav_search .search_submit,.overlay_search .search_submit,form.submit_newsletter .search_submit,form.submit_newsletter .email_submit{background:url("https://www.jpl.nasa.gov/assets/images/search_icon@2x.png") no-repeat 6px 9px transparent;background-size:20px;position:absolute;right:0;top:0;cursor:pointer;border:none;width:40px;height:40px}.light_background .site_header form.nav_search .search_field,.section_search .search_field,.light_background .site_header form.nav_search form.submit_newsletter .email_field,form.submit_newsletter .light_background .site_header form.nav_search .email_field,.section_search form.submit_newsletter .email_field,form.submit_newsletter .section_search .email_field{background-color:white;color:#222222}.light_background .site_header form.nav_search .search_field.placeholder,.section_search .search_field.placeholder,.light_background .site_header form.nav_search form.submit_newsletter .placeholder.email_field,form.submit_newsletter .light_background .site_header form.nav_search .placeholder.email_field,.section_search form.submit_newsletter .placeholder.email_field,form.submit_newsletter .section_search .placeholder.email_field{color:#5a6470;opacity:1 !important}.light_background .site_header form.nav_search .search_field:-moz-placeholder,.section_search .search_field:-moz-placeholder,.light_background .site_header form.nav_search form.submit_newsletter .email_field:-moz-placeholder,form.submit_newsletter .light_background .site_header form.nav_search .email_field:-moz-placeholder,.section_search form.submit_newsletter .email_field:-moz-placeholder,form.submit_newsletter .section_search .email_field:-moz-placeholder{color:#5a6470;opacity:1 !important}.light_background .site_header form.nav_search .search_field::-moz-placeholder,.section_search .search_field::-moz-placeholder,.light_background .site_header form.nav_search form.submit_newsletter .email_field::-moz-placeholder,form.submit_newsletter .light_background .site_header form.nav_search .email_field::-moz-placeholder,.section_search form.submit_newsletter .email_field::-moz-placeholder,form.submit_newsletter .section_search .email_field::-moz-placeholder{color:#5a6470;opacity:1 !important}.light_background .site_header form.nav_search .search_field::-webkit-input-placeholder,.section_search .search_field::-webkit-input-placeholder,.light_background .site_header form.nav_search form.submit_newsletter .email_field::-webkit-input-placeholder,form.submit_newsletter .light_background .site_header form.nav_search .email_field::-webkit-input-placeholder,.section_search form.submit_newsletter .email_field::-webkit-input-placeholder,form.submit_newsletter .section_search .email_field::-webkit-input-placeholder{color:#5a6470;opacity:1 !important}#home.light_background .site_header form.nav_search .search_field,#home.light_background .section_search .search_field,#home.light_background .site_header form.nav_search form.submit_newsletter .email_field,form.submit_newsletter #home.light_background .site_header form.nav_search .email_field,#home.light_background .section_search form.submit_newsletter .email_field,form.submit_newsletter #home.light_background .section_search .email_field{background-color:rgba(255,255,255,0.8)}.light_background .site_header form.nav_search .search_submit,.section_search .search_submit,.light_background .site_header form.nav_search form.submit_newsletter .email_submit,form.submit_newsletter .light_background .site_header form.nav_search .email_submit,.section_search form.submit_newsletter .email_submit,form.submit_newsletter .section_search .email_submit{background:url("https://www.jpl.nasa.gov/assets/images/search_icon_darkgrey@2x.png") no-repeat 9px 12px transparent;background-size:20px;margin-top:-2px}.filter_bar .light_background .site_header form.nav_search .search_submit,.light_background .site_header .filter_bar form.nav_search .search_submit,.filter_bar .section_search .search_submit,.filter_bar .light_background .site_header form.nav_search form.submit_newsletter .email_submit,form.submit_newsletter .filter_bar .light_background .site_header form.nav_search .email_submit,.light_background .site_header .filter_bar form.nav_search form.submit_newsletter .email_submit,form.submit_newsletter .light_background .site_header .filter_bar form.nav_search .email_submit,.filter_bar .section_search form.submit_newsletter .email_submit,form.submit_newsletter .filter_bar .section_search .email_submit{background:url("https://www.jpl.nasa.gov/assets/images/search_icon_dark@2x.png") no-repeat 9px 12px transparent;background-size:20px}.site_header form.nav_search{display:none}@media (min-width: 769px){.site_header form.nav_search{display:inline-block}}.light_background .site_header form.nav_search{display:none}@media (min-width: 769px){.light_background .site_header form.nav_search{display:inline-block}}form.submit_newsletter{width:85%;max-width:300px;display:inline-block}form.submit_newsletter .email_field{width:100%}form.submit_newsletter .email_submit{background:url("https://www.jpl.nasa.gov/assets/stylesheets/../images/envelope_white@2x.png") no-repeat 4px 10px transparent;background-size:25px;opacity:.8}form.submit_newsletter .email_submit:hover{opacity:1}#secondary_column form.submit_newsletter{width:100%;max-width:none}#secondary_column form.submit_newsletter .search_field,#secondary_column form.submit_newsletter .email_field{background:#4b6a8d;border-radius:4px}form.list_form ul{padding:1em 0}form.list_form ul label{display:block;margin-bottom:5px}form.list_form ul input:not([type="checkbox"]):not([type="radio"]),form.list_form ul textarea{width:100%;border:none;border:1px solid #777777;border-radius:4px;padding:10px 12px;font-size:1em}form.list_form ul input[type="checkbox"]{width:auto}form.list_form li{margin-bottom:10px}form.list_form li.inline_item&gt;input,form.list_form li.inline_item&gt;label{display:inline-block}form.list_form li.inline_item.indented{margin-left:1.5em}@media (min-width: 600px){.grid_gallery .gallery_header{line-height:50px}}.grid_gallery .module_title_small{display:none}@media (min-width: 600px){.grid_gallery .module_title_small{display:block}}.grid_gallery .module_title{display:none}@media (min-width: 769px){.grid_gallery .module_title{display:block}}.grid_gallery ul.articles{margin-bottom:2em}.grid_gallery .image_and_description_container{position:relative}.grid_gallery .more_links{padding-top:2em;float:right;font-weight:600}.grid_gallery .more_links a{text-decoration:none;display:inline-block;color:#0e7ee0}.grid_gallery .more_links a:hover{text-decoration:underline}.grid_gallery .more_links a+a{margin-left:2em}.grid_gallery.grid_view .content_title{letter-spacing:-.03em;display:none}.grid_gallery.grid_view .image_and_description_container{min-height:0}.grid_gallery.grid_view .article_teaser_body{display:none}.grid_gallery.grid_view .img{position:relative}.grid_gallery.grid_view span.play_button{position:absolute;background:url("https://www.jpl.nasa.gov/assets/images/play-button.png") center center no-repeat;background-size:50px 50px;height:50px;width:50px;display:inline;left:42%;left:calc(50% - 25px);top:42%;top:calc(50% - 25px)}.grid_gallery.grid_view .bottom_gradient{color:white;display:block;position:relative;margin-top:-48px;height:126px;text-align:center}.grid_gallery.grid_view .bottom_gradient:before{content:'';display:inline-block;height:100%;vertical-align:middle;margin-right:-.25em}.grid_gallery.grid_view .bottom_gradient div{display:inline-block;vertical-align:middle;width:90%;text-align:left;margin-top:2.5em}#missions .grid_gallery.grid_view .bottom_gradient div{margin-top:1em;text-align:center}#missions .grid_gallery.grid_view .bottom_gradient div h3{font-size:1.4em;margin-bottom:.1em}.grid_gallery.grid_view .bottom_gradient h3{font-weight:600}.grid_gallery.grid_view li.slide{margin-bottom:0.84034%;width:49.57983%;float:left}.grid_gallery.grid_view li.slide:nth-child(2n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}.grid_gallery.grid_view li.slide:nth-child(2n+2){margin-left:50.42017%;margin-right:-100%;clear:none}@media (min-width: 600px){.grid_gallery.grid_view li.slide{width:24.36975%;float:left}.grid_gallery.grid_view li.slide:nth-child(4n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}.grid_gallery.grid_view li.slide:nth-child(4n+2){margin-left:25.21008%;margin-right:-100%;clear:none}.grid_gallery.grid_view li.slide:nth-child(4n+3){margin-left:50.42017%;margin-right:-100%;clear:none}.grid_gallery.grid_view li.slide:nth-child(4n+4){margin-left:75.63025%;margin-right:-100%;clear:none}}@media (min-width: 769px){.grid_gallery.grid_view li.slide{width:19.32773%;float:left}.grid_gallery.grid_view li.slide:nth-child(5n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}.grid_gallery.grid_view li.slide:nth-child(5n+2){margin-left:20.16807%;margin-right:-100%;clear:none}.grid_gallery.grid_view li.slide:nth-child(5n+3){margin-left:40.33613%;margin-right:-100%;clear:none}.grid_gallery.grid_view li.slide:nth-child(5n+4){margin-left:60.5042%;margin-right:-100%;clear:none}.grid_gallery.grid_view li.slide:nth-child(5n+5){margin-left:80.67227%;margin-right:-100%;clear:none}}@media (min-width: 1200px){.grid_gallery.grid_view li.slide{width:15.96639%;float:left}.grid_gallery.grid_view li.slide:nth-child(6n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}.grid_gallery.grid_view li.slide:nth-child(6n+2){margin-left:16.80672%;margin-right:-100%;clear:none}.grid_gallery.grid_view li.slide:nth-child(6n+3){margin-left:33.61345%;margin-right:-100%;clear:none}.grid_gallery.grid_view li.slide:nth-child(6n+4){margin-left:50.42017%;margin-right:-100%;clear:none}.grid_gallery.grid_view li.slide:nth-child(6n+5){margin-left:67.22689%;margin-right:-100%;clear:none}.grid_gallery.grid_view li.slide:nth-child(6n+6){margin-left:84.03361%;margin-right:-100%;clear:none}}.grid_gallery.grid_view li.slide a{text-decoration:none}#images .grid_gallery.grid_view li.slide{text-decoration:none;width:49.57983%;float:left;margin-bottom:0.84034%}#images .grid_gallery.grid_view li.slide:nth-child(2n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}#images .grid_gallery.grid_view li.slide:nth-child(2n+2){margin-left:50.42017%;margin-right:-100%;clear:none}@media (min-width: 480px){#images .grid_gallery.grid_view li.slide{width:32.77311%;float:left}#images .grid_gallery.grid_view li.slide:nth-child(3n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}#images .grid_gallery.grid_view li.slide:nth-child(3n+2){margin-left:33.61345%;margin-right:-100%;clear:none}#images .grid_gallery.grid_view li.slide:nth-child(3n+3){margin-left:67.22689%;margin-right:-100%;clear:none}}@media (min-width: 769px){#images .grid_gallery.grid_view li.slide{width:24.36975%;float:left}#images .grid_gallery.grid_view li.slide:nth-child(4n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}#images .grid_gallery.grid_view li.slide:nth-child(4n+2){margin-left:25.21008%;margin-right:-100%;clear:none}#images .grid_gallery.grid_view li.slide:nth-child(4n+3){margin-left:50.42017%;margin-right:-100%;clear:none}#images .grid_gallery.grid_view li.slide:nth-child(4n+4){margin-left:75.63025%;margin-right:-100%;clear:none}}@media (min-width: 1200px){#images .grid_gallery.grid_view li.slide{width:24.36975%;float:left}#images .grid_gallery.grid_view li.slide:nth-child(4n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}#images .grid_gallery.grid_view li.slide:nth-child(4n+2){margin-left:25.21008%;margin-right:-100%;clear:none}#images .grid_gallery.grid_view li.slide:nth-child(4n+3){margin-left:50.42017%;margin-right:-100%;clear:none}#images .grid_gallery.grid_view li.slide:nth-child(4n+4){margin-left:75.63025%;margin-right:-100%;clear:none}}#missions .grid_gallery.grid_view li.slide{text-decoration:none;width:49.57983%;float:left;margin-bottom:0.84034%}#missions .grid_gallery.grid_view li.slide:nth-child(2n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}#missions .grid_gallery.grid_view li.slide:nth-child(2n+2){margin-left:50.42017%;margin-right:-100%;clear:none}@media (min-width: 480px){#missions .grid_gallery.grid_view li.slide{width:32.77311%;float:left}#missions .grid_gallery.grid_view li.slide:nth-child(3n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}#missions .grid_gallery.grid_view li.slide:nth-child(3n+2){margin-left:33.61345%;margin-right:-100%;clear:none}#missions .grid_gallery.grid_view li.slide:nth-child(3n+3){margin-left:67.22689%;margin-right:-100%;clear:none}}@media (min-width: 769px){#missions .grid_gallery.grid_view li.slide{width:24.36975%;float:left}#missions .grid_gallery.grid_view li.slide:nth-child(4n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}#missions .grid_gallery.grid_view li.slide:nth-child(4n+2){margin-left:25.21008%;margin-right:-100%;clear:none}#missions .grid_gallery.grid_view li.slide:nth-child(4n+3){margin-left:50.42017%;margin-right:-100%;clear:none}#missions .grid_gallery.grid_view li.slide:nth-child(4n+4){margin-left:75.63025%;margin-right:-100%;clear:none}}@media (min-width: 1200px){#missions .grid_gallery.grid_view li.slide{width:24.36975%;float:left}#missions .grid_gallery.grid_view li.slide:nth-child(4n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}#missions .grid_gallery.grid_view li.slide:nth-child(4n+2){margin-left:25.21008%;margin-right:-100%;clear:none}#missions .grid_gallery.grid_view li.slide:nth-child(4n+3){margin-left:50.42017%;margin-right:-100%;clear:none}#missions .grid_gallery.grid_view li.slide:nth-child(4n+4){margin-left:75.63025%;margin-right:-100%;clear:none}}#news .grid_gallery.grid_view li.slide{width:49.57983%;float:left;margin-bottom:0.84034%}#news .grid_gallery.grid_view li.slide:nth-child(2n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}#news .grid_gallery.grid_view li.slide:nth-child(2n+2){margin-left:50.42017%;margin-right:-100%;clear:none}@media (min-width: 480px){#news .grid_gallery.grid_view li.slide{width:32.77311%;float:left}#news .grid_gallery.grid_view li.slide:nth-child(3n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}#news .grid_gallery.grid_view li.slide:nth-child(3n+2){margin-left:33.61345%;margin-right:-100%;clear:none}#news .grid_gallery.grid_view li.slide:nth-child(3n+3){margin-left:67.22689%;margin-right:-100%;clear:none}}@media (min-width: 1200px){#news .grid_gallery.grid_view li.slide{width:32.77311%;float:left}#news .grid_gallery.grid_view li.slide:nth-child(3n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}#news .grid_gallery.grid_view li.slide:nth-child(3n+2){margin-left:33.61345%;margin-right:-100%;clear:none}#news .grid_gallery.grid_view li.slide:nth-child(3n+3){margin-left:67.22689%;margin-right:-100%;clear:none}}.grid_gallery.list_view .img{float:right;margin-left:4%;margin-bottom:.5em;width:32%}@media (min-width: 600px){.grid_gallery.list_view .img{margin-left:0;margin-bottom:0;width:23.07692%;float:left;margin-right:2.5641%}}@media (min-width: 769px){.grid_gallery.list_view .img{width:23.72881%;float:left;margin-right:1.69492%}}@media (min-width: 1024px){.grid_gallery.list_view .img{width:23.72881%;float:left;margin-right:1.69492%}}.grid_gallery.list_view .list_text_content{width:auto}@media (min-width: 600px){.grid_gallery.list_view .list_text_content{width:74.35897%;float:right;margin-right:0}}@media (min-width: 769px){.grid_gallery.list_view .list_text_content{width:74.57627%;float:right;margin-right:0}}@media (min-width: 1024px){.grid_gallery.list_view .list_text_content{width:66.10169%;float:left;margin-right:1.69492%}}.grid_gallery.list_view .content_title{display:block;font-size:1.17em;margin-bottom:0.1em;margin-bottom:.2em;font-weight:600;text-decoration:none;color:black;cursor:pointer;letter-spacing:-.035em}@media (min-width: 600px){.grid_gallery.list_view .content_title{font-size:1.35em;margin-bottom:0.18em}}@media (min-width: 769px){.grid_gallery.list_view .content_title{font-size:1.53em;margin-bottom:0.26em}}@media (min-width: 1024px){.grid_gallery.list_view .content_title{font-size:1.62em;margin-bottom:0.29em}}@media (min-width: 1200px){.grid_gallery.list_view .content_title{font-size:1.71em;margin-bottom:0.32em}}@media (min-width: 1024px){.grid_gallery.list_view .article_teaser_body{font-size:1.1em}}.grid_gallery.list_view li.slide:first-child{border-top:1px solid #cccccc}.grid_gallery.list_view li.slide{border-bottom:1px solid #cccccc;overflow:hidden;*zoom:1;padding:1.2em 0}.grid_gallery.list_view li.slide a{text-decoration:none;color:#222222;cursor:pointer}.grid_gallery.list_view .bottom_gradient{display:none}.view_selectors{position:relative;margin:0 auto;text-align:center;width:106px;text-align:right}@media (min-width: 769px){.view_selectors{position:absolute;right:0;top:0;height:100%}}.view_selectors .nav_item{display:inline-block;position:relative;background-repeat:no-repeat;width:50px;height:50px;cursor:pointer;background-image:url("https://www.jpl.nasa.gov/assets/images/grid_list_icon.png");background-color:#e4e9ef;-webkit-touch-callout:none;-webkit-user-select:none;-khtml-user-select:none;-moz-user-select:-moz-none;-ms-user-select:none;user-select:none}.view_selectors .nav_item.list_icon{background-position:-4px -51px;border-radius:50%}.no-touch .view_selectors .nav_item.list_icon:hover{background-position:-4px -0px}.list_view .view_selectors .nav_item.list_icon{background-position:-4px -0px}.view_selectors .nav_item.grid_icon{background-position:-59px -51px;border-radius:50%}.no-touch .view_selectors .nav_item.grid_icon:hover{background-position:-59px -0px}.grid_view .view_selectors .nav_item.grid_icon{background-position:-59px -0px}.module header{margin-bottom:1em;position:relative}.module footer{text-align:center}.multimedia_teaser{-webkit-touch-callout:none;-webkit-user-select:none;-khtml-user-select:none;-moz-user-select:-moz-none;-ms-user-select:none;user-select:none;background-color:#e4e9ef}.events_teaser section{overflow:hidden}.events_teaser .slide_nav{display:block}@media (min-width: 769px){.events_teaser .slide_nav{display:none}}.events_teaser .event_teaser{min-height:99px;margin-bottom:4em}.events_teaser .util-carousel{margin-bottom:3em}.events_teaser .date{font-weight:200;margin-bottom:.1em;font-size:.9em}.events_teaser .title{font-weight:600;font-size:.9em}.multi_teaser{padding-top:4em;padding-bottom:3em;margin-bottom:0;background-color:#e4e9ef}.multi_teaser ul li{width:100%;float:left;margin-left:0;margin-right:0;margin-bottom:5.26316%}.multi_teaser ul li:last-child{margin-bottom:0}@media (min-width: 769px){.multi_teaser ul li{margin-bottom:0}}@media (min-width: 600px){.multi_teaser ul li{width:32.20339%;float:left}.multi_teaser ul li:nth-child(3n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}.multi_teaser ul li:nth-child(3n+2){margin-left:33.89831%;margin-right:-100%;clear:none}.multi_teaser ul li:nth-child(3n+3){margin-left:67.79661%;margin-right:-100%;clear:none}}.multi_teaser .image_and_description_container{position:relative}.multi_teaser .content_title{padding:.6em 0 0}.multi_teaser .content_title .date{font-weight:300;font-size:.9em;margin-bottom:.2em}.multi_teaser.events_teaser{background-color:white}.newsletter_follow_teaser.module{background-color:#e4e9ef;padding:1.5em 0 .5em 0}.newsletter_follow_teaser.module .share,.newsletter_follow_teaser.module .footer_newsletter{text-align:center;padding:1.69492%;margin-bottom:3em;width:100%}.newsletter_follow_teaser.module .share h2,.newsletter_follow_teaser.module .footer_newsletter h2{font-size:1.5em;font-weight:600;margin-bottom:0.6em;color:white;letter-spacing:-.035em}@media (min-width: 600px){.newsletter_follow_teaser.module .share h2,.newsletter_follow_teaser.module .footer_newsletter h2{font-size:1.6em}}@media (min-width: 1200px){.newsletter_follow_teaser.module .share h2,.newsletter_follow_teaser.module .footer_newsletter h2{font-size:1.8em}}.newsletter_follow_teaser.module .gradient_line_divider{margin:1em auto;display:none}@media (min-width: 600px){.newsletter_follow_teaser.module .footer_newsletter{width:48.71795%;float:left;margin-left:0;margin-right:-100%}}@media (min-width: 769px){.newsletter_follow_teaser.module .footer_newsletter{width:40.67797%;float:left;margin-left:8.47458%;margin-right:-100%}}@media (min-width: 600px){.newsletter_follow_teaser.module .share{width:48.71795%;float:left;margin-left:51.28205%;margin-right:-100%}}@media (min-width: 769px){.newsletter_follow_teaser.module .share{width:40.67797%;float:left;margin-left:50.84746%;margin-right:-100%}}.newsletter_follow_teaser.module .gradient_line_divider{margin-left:auto;margin-right:auto;content:" ";width:100%;height:1px;clear:both;background:white;background:-moz-linear-gradient(left, rgba(255,255,255,0), #fff, rgba(255,255,255,0));background:-webkit-linear-gradient(left, rgba(255,255,255,0), #fff, rgba(255,255,255,0));background:linear-gradient(to right, rgba(255,255,255,0), #fff, rgba(255,255,255,0));display:block}@media (min-width: 600px){.newsletter_follow_teaser.module .gradient_line_divider{display:none}}.newsletter_follow_teaser.module .share,.newsletter_follow_teaser.module .footer_newsletter{margin-bottom:1.5em}.newsletter_follow_teaser.module .share h2,.newsletter_follow_teaser.module .footer_newsletter h2{color:#222222}.newsletter_follow_teaser.module form.submit_newsletter .email_field{color:#343434;background-color:white}.newsletter_follow_teaser.module form.submit_newsletter .email_field.placeholder{color:#7b7b7b}.newsletter_follow_teaser.module form.submit_newsletter .email_field:-moz-placeholder{color:#7b7b7b}.newsletter_follow_teaser.module form.submit_newsletter .email_field::-moz-placeholder{color:#7b7b7b}.newsletter_follow_teaser.module form.submit_newsletter .email_field::-webkit-input-placeholder{color:#7b7b7b}.newsletter_follow_teaser.module .email_submit{background:url("https://www.jpl.nasa.gov/assets/stylesheets/../images/envelope_blue@2x.png") no-repeat 4px 10px transparent;background-size:25px}.newsletter_follow_teaser.module .share .all_icon{color:#14aaf7}.newsletter_teaser{background-color:#e4e9ef;padding-top:4em;padding-bottom:3em;margin-bottom:0}.newsletter_teaser .img_col{width:23.72881%;float:left;margin-left:25.42373%;margin-right:-100%}.newsletter_teaser .text_col{width:23.72881%;float:left;margin-left:50.84746%;margin-right:-100%}.image_teaser ul{width:100%;margin:0 auto}@media (min-width: 769px){.image_teaser ul{width:83.05085%}}.image_teaser .slide{width:100%;margin-bottom:5.26316%}@media (min-width: 600px){.image_teaser .slide{-moz-box-sizing:border-box;-webkit-box-sizing:border-box;box-sizing:border-box;width:50%;float:left;padding-left:0.83333%;padding-right:0.83333%}}@media (min-width: 769px){.image_teaser .slide{-moz-box-sizing:border-box;-webkit-box-sizing:border-box;box-sizing:border-box;width:50%;float:left;padding-left:0.83333%;padding-right:0.83333%}}.image_teaser .image_container{margin-bottom:1.69492%}.image_teaser .content_title{font-size:1.2em;margin-bottom:.1em}.grid_gallery+.image_teaser{padding-top:0}.player.lede{margin-bottom:2em}.facts_module .title{font-weight:600}.primary_media_feature .floating_text_area{position:absolute;color:white;width:95%;left:0;right:0;margin:0 auto;bottom:2em;text-align:center;z-index:2}@media (min-width: 769px){.primary_media_feature .floating_text_area{left:10%;width:80%}}.primary_media_feature .floating_text_area a{text-decoration:none;color:inherit}.primary_media_feature .floating_text_area .brand_title{font-size:.9em;font-weight:600;margin-bottom:6px}.primary_media_feature .floating_text_area .brand_title i{font-weight:200}.primary_media_feature .floating_text_area .category_title{color:white}.primary_media_feature .floating_text_area .media_feature_title{font-weight:600;line-height:1.2em;margin-bottom:.18em}.primary_media_feature .floating_text_area .description{display:none}@media (min-width: 769px){.primary_media_feature .floating_text_area .description{display:block;line-height:1.4em;margin-bottom:1.4em}}.primary_media_feature .floating_text_area footer{text-align:left}.primary_media_feature .floating_text_area.no_bg{color:white}.primary_media_feature .floating_text_area.bg_dark{background-color:black;background-color:rgba(0,0,0,0.5);padding:1.4em}.primary_media_feature .floating_text_area.bg_light{background-color:white;background-color:rgba(255,255,255,0.9);color:black;padding:1.4em}.primary_media_feature .floating_text_area.bg_light .category_title,.primary_media_feature .floating_text_area.bg_light .media_feature_title{color:black !important}@media (min-width: 769px){.primary_media_feature .floating_text_area.bg_light .category_title,.primary_media_feature .floating_text_area.bg_light .media_feature_title{color:white !important}}@media (min-width: 769px){.primary_media_feature .floating_text_area.bottom_left{width:21%;text-align:left;bottom:40px;left:12%}}@media (min-width: 769px){.primary_media_feature.centered_text .floating_text_area{left:0;right:0;width:80%}}@media (min-width: 769px){.primary_media_feature.centered_text .floating_text_area .description{width:500px;margin:15px auto 10px}}@media (min-width: 1024px){.primary_media_feature.centered_text .floating_text_area .description{width:550px}}.primary_media_feature.centered_text .floating_text_area footer{text-align:center;padding:1.2em 0 .2em}#missions_detail .primary_media_feature .floating_text_area{width:95%}@media (min-width: 600px){#missions_detail .primary_media_feature .floating_text_area{width:95%;left:0;right:0;text-align:left}}@media (min-width: 769px){#missions_detail .primary_media_feature .floating_text_area{width:90%}}@media (min-width: 1024px){#missions_detail .primary_media_feature .floating_text_area{max-width:1200px;width:97%}}.primary_media_feature.homepage_carousel .floating_text_area{width:100%;padding:1.4em;margin:0;bottom:4.2em;background:none}@media (min-width: 600px){.primary_media_feature.homepage_carousel .floating_text_area{bottom:7em}}@media (min-width: 769px){.primary_media_feature.homepage_carousel .floating_text_area{border-radius:6px;color:white;padding:1.4em;bottom:70px;text-align:left;transition:background-color .5s ease-out;right:auto;left:3%;width:40%}.primary_media_feature.homepage_carousel .floating_text_area:hover{background-color:black;background-color:rgba(32,32,32,0.9)}.primary_media_feature.homepage_carousel .floating_text_area:hover::before{opacity:0}.primary_media_feature.homepage_carousel .floating_text_area:hover .description{max-height:300px}.primary_media_feature.homepage_carousel .floating_text_area:hover .media_feature_title:after{opacity:0}.primary_media_feature.homepage_carousel .floating_text_area .description{max-height:0;overflow:hidden;transition:all .5s}.primary_media_feature.homepage_carousel .floating_text_area .description a{color:white}.primary_media_feature.homepage_carousel .floating_text_area .description a.detail_link{color:#44a2f5;display:block;margin:.7em 0 .6em}.primary_media_feature.homepage_carousel .floating_text_area .description a.detail_link:hover{color:#65b5fc}}@media (min-width: 1024px){.primary_media_feature.homepage_carousel .floating_text_area{width:435px;right:auto}}@media (min-width: 1200px){.primary_media_feature.homepage_carousel .floating_text_area{width:510px}}@media (min-width: 1700px){.primary_media_feature.homepage_carousel .floating_text_area{left:2%;width:760px}}@media (min-width: 769px){.primary_media_feature.homepage_carousel .floating_text_area.bottom_right{left:auto;right:3%}}@media (min-width: 1700px){.primary_media_feature.homepage_carousel .floating_text_area.bottom_right{right:2%}}.primary_media_feature.homepage_carousel .floating_text_area .media_feature_title{font-size:1.6em}@media (min-width: 600px){.primary_media_feature.homepage_carousel .floating_text_area .media_feature_title{font-size:2em}}@media (min-width: 769px){.primary_media_feature.homepage_carousel .floating_text_area .media_feature_title{font-size:2.1em;color:white;position:relative;margin-bottom:16px}.primary_media_feature.homepage_carousel .floating_text_area .media_feature_title:after{content:url("https://www.jpl.nasa.gov/assets/images/arrow_down_prompt.png");transition:opacity .25s;position:relative;top:-4px;left:10px;opacity:1}}@media (min-width: 1024px){.primary_media_feature.homepage_carousel .floating_text_area .media_feature_title{font-size:2.4em}}@media (min-width: 1200px){.primary_media_feature.homepage_carousel .floating_text_area .media_feature_title{font-size:2.7em}}@media (min-width: 1700px){.primary_media_feature.homepage_carousel .floating_text_area .media_feature_title{font-size:3em}}.button,.primary_media_feature.single .button,.outline_button{font-weight:600;display:inline-block;margin-bottom:.5em;margin-left:auto;margin-right:auto;background-color:#4b6a8d;color:white;line-height:1em;border:none;text-decoration:none;border-radius:4px;cursor:pointer;text-shadow:none;font-size:13px;padding:12px 24px;white-space:nowrap}@media (min-width: 769px){.button,.primary_media_feature.single .button,.outline_button{font-size:14px}}.no-touch .button:hover,.no-touch .outline_button:hover{background-color:#6083aa}@-moz-document url-prefix(){body .button,body .primary_media_feature.single .button,.primary_media_feature.single body .button,body .outline_button{padding-bottom:10px}body .primary_media_feature.single .button,body .primary_media_feature.single .outline_button,body .outline_button{padding-bottom:8px}@media (min-width: 769px){body .primary_media_feature.single .button,body .primary_media_feature.single .outline_button,body .outline_button{padding-bottom:10px}}}.button+.button,.outline_button+.button,.primary_media_feature.single .button+.button,.primary_media_feature.single .outline_button+.button,.button+.outline_button,.primary_media_feature.single .button+.outline_button,.outline_button+.outline_button{margin-left:1em}.primary_media_feature.single .button,.primary_media_feature.single .outline_button,.outline_button{border-radius:12px;border:2px solid white;border:2px solid rgba(255,255,255,0.8);background:none;color:#FFF;font-weight:600;text-transform:uppercase;padding:10px 13px}@media (min-width: 769px){.primary_media_feature.single .button,.primary_media_feature.single .outline_button,.outline_button{padding:12px 15px}}.primary_media_feature.single .dark.button,.primary_media_feature.single .dark.outline_button,.outline_button.dark{opacity:1;color:#777;border-color:#a5a6a7}.no-touch .primary_media_feature.single .button:hover,.no-touch .primary_media_feature.single .outline_button:hover,.no-touch .outline_button:hover{background-color:#6083aa;color:white;border-color:#6083aa;opacity:1}#site_footer{padding:2em 2em 5em 2em;background-color:black}#site_footer .gradient_line{margin-left:auto;margin-right:auto;content:" ";width:100%;height:1px;clear:both;background:#61b6fd;background:-moz-linear-gradient(left, transparent, #61b6fd, transparent);background:-webkit-linear-gradient(left, transparent, #61b6fd, transparent);background:linear-gradient(to right, transparent, #61b6fd, transparent);width:90%}@media (min-width: 769px){#site_footer .gradient_line{width:50%}}.upper_footer{padding:3em 0 4em}.upper_footer .grid_layout{width:100%}.upper_footer .share,.upper_footer .footer_newsletter{text-align:center;padding:1.69492%;margin-bottom:3em;width:100%}.upper_footer .share h2,.upper_footer .footer_newsletter h2{font-size:1.5em;font-weight:600;margin-bottom:0.6em;color:white;letter-spacing:-.035em}@media (min-width: 600px){.upper_footer .share h2,.upper_footer .footer_newsletter h2{font-size:1.6em}}@media (min-width: 1200px){.upper_footer .share h2,.upper_footer .footer_newsletter h2{font-size:1.8em}}.upper_footer .gradient_line_divider{margin:1em auto;display:none}@media (min-width: 600px){.upper_footer .footer_newsletter{width:48.71795%;float:left;margin-left:0;margin-right:-100%}}@media (min-width: 769px){.upper_footer .footer_newsletter{width:40.67797%;float:left;margin-left:8.47458%;margin-right:-100%}}@media (min-width: 600px){.upper_footer .share{width:48.71795%;float:left;margin-left:51.28205%;margin-right:-100%}}@media (min-width: 769px){.upper_footer .share{width:40.67797%;float:left;margin-left:50.84746%;margin-right:-100%}}#site_footer .sitemap{margin-bottom:3em}@media (min-width: 600px){#site_footer .sitemap .grid_layout{width:100%}}@media (min-width: large){#site_footer .sitemap .grid_layout{width:97%}}#site_footer .sitemap_directory{overflow:hidden;*zoom:1;margin-bottom:3em}#site_footer .sitemap_directory .footer_sitemap_item{margin-bottom:.6em}@media (min-width: 600px){#site_footer .sitemap_directory .footer_sitemap_item{margin-bottom:.2em}}@media (min-width: 1024px){#site_footer .sitemap_directory .footer_sitemap_item{margin-bottom:.2em;margin-left:10%}}#site_footer .sitemap_title{color:white;font-weight:600;text-transform:capitalize;font-size:1.2em;letter-spacing:-.01em;margin-bottom:.3em}@media (min-width: 600px){#site_footer .sitemap_title{font-size:1.1em}}@media (min-width: 1024px){#site_footer .sitemap_title{font-size:1.3em}}#site_footer .sitemap_block{text-align:center;width:100%}@media (min-width: 600px){#site_footer .sitemap_block{-moz-box-sizing:border-box;-webkit-box-sizing:border-box;box-sizing:border-box;width:25%;float:left;padding-left:0.83333%;padding-right:0.83333%;text-align:left}}@media (min-width: 600px){#site_footer ul.subnav{margin-bottom:1em}#site_footer ul.subnav li{padding-left:1em;text-indent:-1em;margin:.1em 0}}#site_footer ul.subnav a{color:#a5a6a7;text-decoration:none;font-size:1em}@media (min-width: 600px){#site_footer ul.subnav a{font-size:.85em}}@media (min-width: 1024px){#site_footer ul.subnav a{font-size:.95em}}.no-touch #site_footer ul.subnav a:hover{color:white}.lower_footer{overflow:hidden}.lower_footer .nav_container{margin:0 auto;position:relative;left:0;width:100%;margin-bottom:2.5em}@media (min-width: 1024px){.lower_footer .nav_container{padding-top:1em;position:absolute}}.lower_footer nav{text-transform:uppercase;text-align:center;margin-left:auto;margin-right:auto;font-size:.9em;color:#a5a6a7}.lower_footer nav a{color:#a5a6a7;text-decoration:none}.no-touch .lower_footer nav a:hover{color:white}.lower_footer nav li{margin:0 .6em;display:inline;line-height:2em}.lower_footer nav li+li:before{margin-left:.6em}.lower_footer .credits{color:#a5a6a7;width:100%;font-size:.9em;text-align:center;position:relative}.lower_footer .credits&gt;span{display:block}.lower_footer .credits a{color:#a5a6a7;text-decoration:none}.no-touch .lower_footer .credits a:hover{color:white}@media (min-width: 1024px){.lower_footer .credits{float:right;width:20%;text-align:left}.lower_footer .credits&gt;span{display:block}}.module{padding:2.3em 0 3em;position:relative}@media (min-width: 769px){.module{padding:4em 0 4.3em}}.grid_layout{max-width:100%;margin-left:auto;margin-right:auto;width:95%}.grid_layout:after{content:" ";display:block;clear:both}@media (min-width: 600px){.grid_layout{max-width:100%;margin-left:auto;margin-right:auto;width:95%}.grid_layout:after{content:" ";display:block;clear:both}}@media (min-width: 769px){.grid_layout{max-width:100%;margin-left:auto;margin-right:auto;width:90%}.grid_layout:after{content:" ";display:block;clear:both}}@media (min-width: 1024px){.grid_layout{max-width:1200px;width:97%}.content_page .grid_layout{width:90%}}@media (max-width: 479px){.slide_strips .grid_layout,.multimedia_teaser .grid_layout,.events_teaser .grid_layout{width:100%}.slide_strips .grid_layout header,.multimedia_teaser .grid_layout header,.events_teaser .grid_layout header{width:95%}.slide_strips .grid_layout footer,.multimedia_teaser .grid_layout footer,.events_teaser .grid_layout footer{width:95%}}@media (min-width: 600px){.slide_strips .grid_layout,.multimedia_teaser .grid_layout,.events_teaser .grid_layout{width:90%}}.homepage_carousel{background:black}.carousel_nav{position:absolute;bottom:30px;cursor:pointer;text-align:center;left:0;right:0;margin:0 auto}@media (min-width: 769px){.carousel_nav{bottom:60px}}.carousel_nav .dot_btns{position:relative;-webkit-touch-callout:none;-webkit-user-select:none;-khtml-user-select:none;-moz-user-select:-moz-none;-ms-user-select:none;user-select:none}.carousel_nav .dot_btns .prev,.carousel_nav .dot_btns .next{display:none}@media screen and (769px){.carousel_nav .dot_btns .prev,.carousel_nav .dot_btns .next{display:inline-block;position:relative;vertical-align:top;margin:6px 8px 0;width:10px;height:15px;background-image:url("https://www.jpl.nasa.gov/assets/arrows-carousel@2x.png");background-size:20px 30px}}.carousel_nav .dot_btns .dot_btn{display:inline-block;cursor:pointer;margin:0 -2px;padding:10px 11px}@media screen and (769px){.carousel_nav .dot_btns .dot_btn{margin:0;padding:10px 9px}}.carousel_nav .dot_btns .dot_btn .dot{background-color:white;border-radius:50% 50% 50% 50%;height:7px;width:7px;opacity:0.2}.no-touch .carousel_nav .dot_btns .dot_btn:hover .dot{opacity:1}.carousel_nav .dot_btns .dot_btn.active .dot{opacity:1}.addthis-smartlayers-desktop .addthis_32x32_style a{width:40px}.touch .addthis-smartlayers{position:relative}.social_icons{display:inline-block;margin-top:3px;white-space:nowrap}.social_icons .icon{display:inline-block;overflow:hidden;height:32px;width:32px;vertical-align:middle;cursor:pointer;border-radius:3px;padding:0 !important;margin-bottom:.6em}.social_icons .icon+.icon{margin-left:.6em}@media (min-width: 769px){.social_icons .icon+.icon{margin-left:.7em}}.social_icons .all_icon{height:32px;width:32px;position:relative;vertical-align:middle;color:#a5a6a7}.social_icons .all_icon span{text-decoration:none;font-size:1em;font-weight:600;position:absolute;bottom:0;left:0;width:100%;line-height:normal}.social_icons .all_icon:hover{color:white}.media_feature .window{width:100%;height:auto;position:absolute;overflow:hidden}@media (min-width: 769px){.media_feature .window{position:relative;height:600px}}.media_feature .window.mobile{height:auto;min-height:100%}.media_feature #featured_image{z-index:9;top:0;left:0;width:100%;overflow:hidden}@media (min-width: 769px){.media_feature #featured_image{position:absolute}}.media_feature.image_of_the_day{padding:0;overflow:hidden;background:black;min-height:300px}@media (min-width: 600px){.media_feature.image_of_the_day{height:335px}}@media (min-width: 769px){.media_feature.image_of_the_day{height:430px}}@media (min-width: 1024px){.media_feature.image_of_the_day{height:570px}}@media (min-width: 1200px){.media_feature.image_of_the_day{height:660px}}@media (min-width: 1700px){.media_feature.image_of_the_day{height:740px;max-height:800px}}.media_feature.image_of_the_day a.image_day{width:100%;height:100%;position:absolute;top:0;left:0;z-index:11}.media_feature.image_of_the_day .window{padding:2.3em 0 3em;height:100%}@media (min-width: 769px){.media_feature.image_of_the_day .window{padding:4em 0 4.3em}}.media_feature.image_of_the_day header{z-index:12;text-align:center}.media_feature.image_of_the_day header .header_link{width:100%}.media_feature.image_of_the_day header .category_title{color:white}.media_feature.image_of_the_day header .module_title{color:white;margin-bottom:20px}.media_feature.image_of_the_day .outline_button{opacity:1}.missions_teaser{color:white;padding:0;overflow:hidden;background:black}@media (min-width: 769px){.missions_teaser{height:auto}}.missions_teaser .window{padding:2.3em 0 3em;width:100%;z-index:11;height:100%;position:relative;overflow:hidden}@media (min-width: 769px){.missions_teaser .window{padding:4em 0 4.3em}}.missions_teaser .window.mobile{height:auto;min-height:100%}.missions_teaser #missions_image{position:absolute;z-index:9;top:0;left:0;height:100%;overflow:hidden}@media (min-width: 600px){.touch .missions_teaser #missions_image{width:150% !important}}.missions_teaser header{z-index:12;text-align:center;margin-bottom:2em}@media (min-width: 769px){.missions_teaser header{margin-bottom:3.2em}}.missions_teaser header .header_link{width:100%}.missions_teaser header .category_title{color:white}.missions_teaser header .module_title{color:white;margin-bottom:.4em}.missions_teaser header p{text-align:center;width:100%;margin:.3em auto 1em;color:#cccccc}@media (min-width: 600px){.missions_teaser header p{width:70%}}@media (min-width: 769px){.missions_teaser header p{width:60%}}@media (min-width: 1024px){.missions_teaser header p{width:50%}}.missions_teaser .missions_gallery{padding-bottom:1px;margin-bottom:2.4em}@media (min-width: 769px){.missions_teaser .missions_gallery{margin-bottom:3em}}.missions_teaser .missions_gallery .slide{border:1px solid #3A3A3A;overflow:hidden;width:47.36842%;float:left;margin-bottom:5.26316%}.missions_teaser .missions_gallery .slide:nth-child(2n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}.missions_teaser .missions_gallery .slide:nth-child(2n+2){margin-left:52.63158%;margin-right:-100%;clear:none}@media (min-width: 600px){.missions_teaser .missions_gallery .slide{width:23.72881%;float:left;margin-bottom:0}.missions_teaser .missions_gallery .slide:nth-child(4n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}.missions_teaser .missions_gallery .slide:nth-child(4n+2){margin-left:25.42373%;margin-right:-100%;clear:none}.missions_teaser .missions_gallery .slide:nth-child(4n+3){margin-left:50.84746%;margin-right:-100%;clear:none}.missions_teaser .missions_gallery .slide:nth-child(4n+4){margin-left:76.27119%;margin-right:-100%;clear:none}}.missions_teaser .missions_gallery .text_overlay{color:white;font-size:1.3em;font-weight:600;padding-bottom:.6em;z-index:1;padding:.6em}@media (min-width: 600px){.missions_teaser .missions_gallery .text_overlay{font-size:1.5em;padding-bottom:.8em}}.missions_teaser .missions_gallery .gradient_bottom_teasers{position:relative;margin-top:-25px;height:75px}@media (min-width: 600px){.missions_teaser .missions_gallery .gradient_bottom_teasers{margin-top:-35px;height:110px}}.missions_teaser .outline_button{opacity:1}.filter_bar{background-color:#e4e9ef;text-align:center;padding:1em 0 0}@media (min-width: 769px){.filter_bar{padding:2em 0}}.filter_bar form.section_search{display:none;padding-bottom:1em;max-width:380px;width:90%;margin:0 auto}@media (min-width: 769px){.filter_bar form.section_search{width:auto;max-width:none;display:block !important;padding-bottom:0}}@media screen and (orientation: portrait){.touch .filter_bar.fixed{position:fixed;top:0;left:0;z-index:20;width:100%;-webkit-box-shadow:0 4px 4px -1px rgba(0,0,0,0.15);-moz-box-shadow:0 4px 4px -2px rgba(0,0,0,0.15);box-shadow:0 4px 4px -2px rgba(0,0,0,0.15)}}.no-touch .filter_bar.fixed{position:fixed;top:0;left:0;z-index:20;width:100%;-webkit-box-shadow:0 4px 4px -1px rgba(0,0,0,0.15);-moz-box-shadow:0 4px 4px -2px rgba(0,0,0,0.15);box-shadow:0 4px 4px -2px rgba(0,0,0,0.15)}.filter_bar .search_binder{width:100%;margin-bottom:.7em}@media (min-width: 769px){.filter_bar .search_binder{position:relative;vertical-align:top;display:inline-block;width:auto;margin:0}}.filter_bar input.search_field,.filter_bar form.submit_newsletter input.email_field,form.submit_newsletter .filter_bar input.email_field{width:100%}@media (min-width: 769px){.filter_bar input.search_field,.filter_bar form.submit_newsletter input.email_field,form.submit_newsletter .filter_bar input.email_field{width:170px}}@media (min-width: 1024px){.filter_bar input.search_field,.filter_bar form.submit_newsletter input.email_field,form.submit_newsletter .filter_bar input.email_field{width:220px}}.filter_bar select{margin:0 auto .5em;float:none;width:100%;max-width:380px;padding:.5em 1em;font-size:16px;border:0;height:40px;vertical-align:middle;color:white;-webkit-appearance:none;-o-appearance:none;background:#4b6a8d url("https://www.jpl.nasa.gov/assets/images/arrows_select_box.png") no-repeat 94% 10px;font-weight:600}@media (min-width: 769px){.filter_bar select{margin-left:.5em;margin-bottom:0;width:160px}}@media (min-width: 1024px){.filter_bar select{width:200px}}.no-touch .filter_bar select:hover{cursor:pointer}.filter_bar select::-ms-expand{display:none}.filter_bar option{padding:0.5em 1em}.filter_bar header{display:inline-block;width:100%;text-align:left}@media (min-width: 600px){.filter_bar header{text-align:center}}@media (min-width: 769px){.filter_bar header{display:none}}.filter_bar .arrow_box{display:inline-block;position:absolute;padding:4px;cursor:pointer;right:0;bottom:7px;float:none;transition:all .2s}@media (min-width: 600px){.filter_bar .arrow_box{text-align:center}}.filter_bar .arrow_box.rotate_up{transform:rotate(180deg)}.filter_bar .arrow_box.rotate_right{transform:rotate(270deg)}.filter_bar .arrow_box.rotate_left{transform:rotate(90deg)}.filter_bar .arrow_box .arrow_down{display:block;border-left:8px solid transparent;border-right:8px solid transparent;border-top:8px solid #8597B1}.filter_bar_spanner{display:none}@media screen and (orientation: landscape){.touch .filter_bar_spanner{display:none !important}}@-moz-document url-prefix(){section.filter_bar select{background-image:none;padding:0.6em 1em 0.5em}}.ie9 section.filter_bar select{background-image:none}.rollover_description{opacity:0;height:0;z-index:1;overflow:hidden}.rollover_description .item_tease_overlay{color:white}.slide{position:relative;min-height:100%}.slide .overlay_arrow{display:none}.slide&gt;a{text-decoration:none;color:black}.no-touch .slide:hover .content_title{color:#366599;cursor:pointer}@media (min-width: 769px){.no-touch .slide:hover .rollover_description{padding:.9em;position:absolute;opacity:1;height:auto;top:0;right:0;width:100%;height:100%;color:white;background-color:rgba(67,93,122,0.95);cursor:pointer}.no-touch .slide:hover .rollover_title{font-size:1.6em;font-weight:600;margin-bottom:.2em}.no-touch .slide:hover .overlay_arrow{height:14px;width:14px;position:absolute;right:14px;bottom:18px;display:block}}.list_view .rollover_description{display:none}.release_heading{text-transform:uppercase;font-weight:600}.release_heading,.release_date{font-size:.9em;margin-bottom:.3em;display:inline-block}.slick-slider{margin-left:auto;margin-right:auto;width:100%}@media (min-width: 480px){.slick-slider{width:84%}}@media (min-width: 600px){.slick-slider{width:90%}}.slick-slider .slick-slide&gt;a{text-decoration:none;color:black}.slick-slider .slide{margin:0 6px}@media (min-width: 769px){.slick-slider .slide{margin:0 9px}}.image_and_description_container{position:relative;overflow:hidden}.image_and_description_container span.play_button{position:absolute;background:url("https://www.jpl.nasa.gov/assets/images/play-button.png") center center no-repeat;background-size:50px 50px;height:50px;width:50px;display:inline;left:42%;left:calc(50% - 25px);top:42%;top:calc(50% - 25px)}.slide_strips{overflow:hidden;padding-top:0}.slide_strips header{overflow:hidden}.slide_strips header h1.module_title{margin-bottom:.45em}.slide_strips header h1.module_title_small{display:inline-block;vertical-align:middle;width:20%}.slide_strips header .section_selector{text-align:center;display:inline-block;width:100%;position:relative;padding:1px 0;margin-bottom:1em}@media (min-width: 600px){.slide_strips header .section_selector{margin-bottom:1.6em}}@media (min-width: 769px){.slide_strips header .section_selector{margin-bottom:1.8em}}.slide_strips header .section_selector a{cursor:pointer;border-radius:50%;height:6em;width:6em;background-color:white;border:1px solid #777777;line-height:6em;color:#777777;line-height:4.3em;cursor:pointer;display:inline-block;text-transform:uppercase;font-size:.7em;transition:background .2s ease;line-height:6em;font-weight:600;letter-spacing:-.02em}@media (min-width: 769px){.slide_strips header .section_selector a{cursor:pointer;border-radius:50%;height:6.5em;width:6.5em;background-color:white;border:2px solid #a5a6a7;line-height:6.5em;font-size:.9em;line-height:6.5em}}.slide_strips header .section_selector a+a{margin-left:.2em}@media (min-width: 769px){.slide_strips header .section_selector a+a{margin-left:1em}}.no-touch .slide_strips header .section_selector a:hover,.slide_strips header .section_selector a.current{background-color:black;border-color:black;color:white;transition:none}.slide_strips header .section_selector .gradient_line{position:absolute;top:50%;z-index:-1;height:2px}.slide_strips .slide_strip_wrapper{-webkit-touch-callout:none;-webkit-user-select:none;-khtml-user-select:none;-moz-user-select:-moz-none;-ms-user-select:none;user-select:none;position:relative;min-height:100px;margin-bottom:40px}.slide_strips .slide_strip_wrapper .loading{display:none;background-image:url("https://www.jpl.nasa.gov/assets/stylesheets/ajax-loader.gif");width:32px;height:32px;margin-left:auto;margin-right:auto;position:relative;top:40px}.slide_strips .slide_strip_container{width:100%;left:0}.slide_strips .slide_strip{z-index:6;position:relative;left:0;opacity:0;-ms-filter:"progid:DXImageTransform.Microsoft.Alpha(Opacity=0)";margin-bottom:0}.slide_strips .slide_strip .slide{margin:0 6px}@media (min-width: 769px){.slide_strips .slide_strip .slide{margin:0 9px}}.slide_strips .content_title{padding:.6em 0 0;color:black;text-decoration:none}.slide_strips .content_titlea{text-decoration:none}.multimedia_teaser .multimedia_module_gallery{position:relative;overflow:visible}nav.slide_nav{width:100%;position:absolute;height:100%}nav.slide_nav .set_view_master_nav{display:none}@media (min-width: 480px){nav.slide_nav .set_view_master_nav{display:block;cursor:pointer;position:absolute;width:40px;height:40px;text-align:center;top:20%}}@media (min-width: 600px){nav.slide_nav .set_view_master_nav{top:20%}}@media (min-width: 769px){nav.slide_nav .set_view_master_nav{top:26%}}@media (min-width: 1024px){nav.slide_nav .set_view_master_nav{top:30%}}nav.slide_nav .set_view_master_nav .carousel_arrow_icon{background-image:url("https://www.jpl.nasa.gov/assets/images/arrows_carousel_round@2x.png");background-size:100px;width:40px;height:40px;display:inline-block;text-indent:-9999px}.multimedia_teaser nav.slide_nav .set_view_master_nav{top:38%}nav.slide_nav .prev_btn .carousel_arrow_icon,nav.slide_nav .next_btn .carousel_arrow_icon{background-position:0px 0px}@media (min-width: 480px){nav.slide_nav .prev_btn,nav.slide_nav .next_btn{opacity:.4;-webkit-tap-highlight-color:rgba(255,255,255,0);-webkit-tap-highlight-color:transparent}.no-touch nav.slide_nav .prev_btn:hover,.no-touch nav.slide_nav .next_btn:hover{opacity:1}.no-touch nav.slide_nav .prev_btn:hover.disabled,.no-touch nav.slide_nav .next_btn:hover.disabled{cursor:default;opacity:.1}nav.slide_nav .prev_btn.disabled,nav.slide_nav .next_btn.disabled{opacity:.1}}nav.slide_nav .prev_btn{left:-.5%}@media (min-width: 600px){nav.slide_nav .prev_btn{left:-2%}}@media (min-width: 769px){nav.slide_nav .prev_btn{left:-1.5%}}@media (min-width: 1024px){nav.slide_nav .prev_btn{left:-.5%}}@media (min-width: 1200px){nav.slide_nav .prev_btn{left:.5%}}nav.slide_nav .next_btn{right:-1.5%}@media (min-width: 600px){nav.slide_nav .next_btn{right:-2.5%}}@media (min-width: 769px){nav.slide_nav .next_btn{right:-2%}}@media (min-width: 1024px){nav.slide_nav .next_btn{right:-1%}}@media (min-width: 1200px){nav.slide_nav .next_btn{right:0}}nav.slide_nav .next_btn .carousel_arrow_icon{background-position:-50px 0px}.fancybox-overlay,#fancybox-lock{background:#000 !important}.fancybox-wrap,.fancybox-wrap *{-moz-box-sizing:content-box !important;-webkit-box-sizing:content-box !important;-safari-box-sizing:content-box !important;box-sizing:content-box !important}.fancybox-wrap .fancybox-inner{box-shadow:none !important;border-radius:2px !important}.fancybox-wrap .fancybox-title{font-size:16px;font-weight:600;letter-spacing:-0.01em;text-align:center;margin-top:16px;color:#E7E7E7;line-height:1.4em}@media (min-width: 769px){.fancybox-wrap .fancybox-title{font-size:17px}}@media (min-width: 1200px){.fancybox-wrap .fancybox-title{font-size:19px}}.fancybox-wrap .addthis_toolbox{display:inline-block;width:100%;margin-top:16px;white-space:nowrap}.fancybox-wrap a.addthis_button_compact{width:85px;border-radius:4px;overflow:hidden;height:35px}.fancybox-wrap a.addthis_button_compact img{vertical-align:top}.fancybox-wrap a.addthis_button_compact,.fancybox-wrap .button,.fancybox-wrap .primary_media_feature.single .button,.primary_media_feature.single .fancybox-wrap .button,.fancybox-wrap .outline_button{margin-right:6px;display:inline-block;vertical-align:top}.fancybox-wrap .button,.fancybox-wrap .primary_media_feature.single .button,.primary_media_feature.single .fancybox-wrap .button,.fancybox-wrap .outline_button{font-size:14px;padding-bottom:0;padding-left:1em;padding-right:1em;height:25px;letter-spacing:0;padding-top:10px}#fancybox-thumbs{background:#2A2A2A !important}#fancybox-thumbs .fancybox-thumb-prev,#fancybox-thumbs .fancybox-thumb-next{background:#4A4A4A !important}#fancybox-thumbs ul li{padding:2px !important}#fancybox-thumbs ul li a{border:2px solid #909090 !important;border-radius:2px !important;box-shadow:none !important}#fancybox-thumbs ul li.fancybox-thumb-active{padding:2px !important}#fancybox-thumbs ul li.fancybox-thumb-active a{border:2px solid #fff !important}.atm-i{display:none !important}figure{position:relative;margin-bottom:1em}@media (min-width: 769px){figure{margin-bottom:2em}}figure figcaption{margin-top:.8em;font-size:.8em;color:#5a6470}@media (min-width: 769px){figure figcaption{font-size:.88em}}figure a.play{position:relative}figure span.play_button{position:absolute;background:url("https://www.jpl.nasa.gov/assets/images/play-button.png") center center no-repeat;background-size:50px 50px;height:50px;width:50px;display:inline;left:42%;left:calc(50% - 25px);top:42%;top:calc(50% - 25px)}aside figure{margin-bottom:0}aside figure figcaption{margin-bottom:0}.content_page #page_header{margin-bottom:2em}.content_page #page_header .release_date{font-size:1em;color:#222222;white-space:nowrap}.content_page #page_header .author{margin:.5em 0 1.8em}.no-touch .content_page a:hover{border-bottom:1px solid}.content_page .main_feature .master-slider{width:100%;height:300px}@media (min-width: 600px){.content_page .main_feature .master-slider{height:400px}}.content_page .main_feature .master-slider .gradient_container_bottom{height:80px}.content_page .main_feature .master-slider .ms-nav-next,.content_page .main_feature .master-slider .ms-nav-prev{display:none}@media (min-width: 769px){.content_page .main_feature .master-slider .ms-nav-next,.content_page .main_feature .master-slider .ms-nav-prev{display:block}}.content_page .main_feature .master-slider .ms-bullets{bottom:30px}.content_page .main_feature .master-slider .ms-bullets-count{right:-50%;position:absolute}.content_page .main_feature .master-slider .ms-bullet{background-color:white;background-image:none;border-radius:50% 50% 50% 50%;height:10px;width:10px;opacity:0.5;margin:0 10px}.content_page .main_feature .master-slider .ms-bullet:hover,.content_page .main_feature .master-slider .ms-bullet.ms-bullet-selected{opacity:1.0}.content_page #primary_column{margin-bottom:5.26316%}@media (min-width: 600px){.content_page #primary_column{width:61.53846%;float:left;margin-right:2.5641%;margin-bottom:0}}@media (min-width: 769px){.content_page #primary_column{width:64.40678%;float:left;margin-right:1.69492%}}@media (min-width: 1024px){.content_page #primary_column{width:61.86441%;float:left;margin-right:1.69492%}}@media (min-width: 1200px){.content_page #primary_column{width:59.32203%;float:left;margin-right:1.69492%}}@media (min-width: 600px){.content_page #secondary_column{width:35.89744%;float:right;margin-right:0}}@media (min-width: 769px){.content_page #secondary_column{width:32.20339%;float:right;margin-right:0}}.article_image_container{margin-bottom:2.5641%}.article_image_container .caption{margin-top:.8em;color:#5a6470;font-size:0.8em;height:70px;overflow:hidden}.inner_nav li{display:inline-block}.inner_nav li a{font-weight:600}.inner_nav li a:hover{text-decoration:underline}.inner_nav li a:after{content:" |";color:#777777}.inner_nav li:last-child a:after{content:""}#secondary_column aside{border:1px solid #c1c1c1;padding:5.26316%;margin-bottom:7.14286%}#secondary_column aside:last-child{margin-bottom:0}aside .gallery_list{margin-bottom:0}aside .gallery_list li{margin-bottom:1em;position:relative}aside .gallery_list li:last-child{margin-bottom:0}aside .gallery_list .caption_overlay{position:absolute;top:0;left:0;width:50%;padding:.6em;color:white;font-weight:600}aside .gallery_list span.play_button{position:absolute;background:url("https://www.jpl.nasa.gov/assets/images/play-button.png") center center no-repeat;background-size:50px 50px;height:50px;width:50px;display:inline;left:42%;left:calc(50% - 25px);top:42%;top:calc(50% - 25px)}.links_module li{margin-bottom:1em}.page_subnav{position:relative;top:-1.6em;font-weight:600;font-size:.9em;letter-spacing:-.01em;font-family:Helvetica, Arial, sans-serif;cursor:pointer}@media (min-width: 769px){.page_subnav{top:-2.9em;font-size:1em}}.page_subnav li{margin:0 .5em .3em 0;display:inline-block}.page_subnav li.page_subnav_title{text-transform:uppercase;white-space:nowrap}.page_subnav li.page_subnav_title .divider{margin-left:.5em}.page_subnav li:last-child{margin:0}.page_subnav li a,.page_subnav li .divider{color:#a7afb8}.page_subnav li a{white-space:nowrap}.page_subnav li a:hover{text-decoration:none;border:none !important}.page_subnav li a:hover,.page_subnav li .current{color:#222222}.text_overlay{position:absolute;bottom:0;width:100%;text-align:center;padding:1.2em}.item_tease_overlay{margin-top:.3em;color:#cccccc;overflow:hidden}.article_nav{display:none}@media (min-width: 1024px){.article_nav{display:block;position:relative;z-index:11}.article_nav .article_nav_block{position:fixed;height:86px;display:inline-block;top:42.5%}.article_nav .article_nav_block .link_box{width:40px;background-color:#e4e9ef;display:inline;height:100%}.article_nav .article_nav_block .article_details{display:inline;width:250px;background-color:#FFF;text-decoration:none;color:#000;padding:10px;background-color:#e4e9ef}.article_nav .article_nav_block .article_details .img{margin-bottom:6px}.article_nav .article_nav_block .article_details .title{font-weight:600;font-size:.9em}.article_nav .article_nav_block .article_details .which{font-size:.8em;margin-bottom:12px}.article_nav .article_nav_block.prev{left:0}.article_nav .article_nav_block.prev .link_box{float:left}.article_nav .article_nav_block.prev .article_details{float:left;display:none}.article_nav .article_nav_block.next{right:0}.article_nav .article_nav_block.next .link_box{float:right}.article_nav .article_nav_block.next .article_details{display:none;float:right}.no-touch .article_nav .article_nav_block:hover .article_details{display:block}}.wysiwyg_content{line-height:1.4em}#primary_column .wysiwyg_content&gt;:first-child{margin-top:0}.wysiwyg_content p,.wysiwyg_content a{word-wrap:break-word}.wysiwyg_content h1,.wysiwyg_content h2,.wysiwyg_content h3,.wysiwyg_content h4{font-weight:600;margin:1.5em 0 .5em;line-height:1.2em}.wysiwyg_content h1{font-size:2.2em}.wysiwyg_content h2{font-size:1.8em}.wysiwyg_content h3{font-size:1.4em}.wysiwyg_content h4{font-weight:600;font-size:1.1em}.wysiwyg_content strong,.wysiwyg_content b,.wysiwyg_content .bold{font-weight:bold}.wysiwyg_content .small_text{font-size:.8em}.wysiwyg_content .inline_img,.wysiwyg_content .inline_img .inline_img_wide{margin:.4em 1.2em .9em 0;float:left;max-width:40%}.wysiwyg_content .inline_img.right,.wysiwyg_content .inline_img .right.inline_img_wide{margin-right:0;margin-left:1.2em;float:right}.wysiwyg_content .inline_img img,.wysiwyg_content .inline_img .inline_img_wide img{width:auto;max-width:100%}@media (min-width: 600px){.wysiwyg_content .inline_img,.wysiwyg_content .inline_img .inline_img_wide{max-width:100%}}.wysiwyg_content .inline_img .inline_img_wide{width:100%;max-width:100%}.wysiwyg_content .comment{color:red}.wysiwyg_content .pipe_divider{color:#cccccc}@media (min-width: 480px){.wysiwyg_content .video_embed #video_player{height:385px}}@media (min-width: 600px){.wysiwyg_content .video_embed #video_player{height:306px}}@media (min-width: 769px){.wysiwyg_content .video_embed #video_player{height:400px}}@media (min-width: 1024px){.wysiwyg_content .video_embed #video_player{height:485px}}.wysiwyg_content table{border-spacing:1px;border-collapse:separate;font-size:15px}#primary_column .wysiwyg_content table{margin:2em 0}#secondary_column .wysiwyg_content table{margin:1em 0;width:100%}.wysiwyg_content table th,.wysiwyg_content table td{padding:8px 10px}.wysiwyg_content table th{background-color:#ddd;font-weight:600}.wysiwyg_content table td{background-color:#eee}.wysiwyg_content table .table_top{vertical-align:top}.wysiwyg_content table h1,.wysiwyg_content table h2,.wysiwyg_content table h3,.wysiwyg_content table h4,.wysiwyg_content table h5{margin:.2em 0 .2em}.wysiwyg_content table.clear_table td{background-color:transparent}.wysiwyg_content table.line_separated_table{border-spacing:0}.wysiwyg_content table.line_separated_table td{background-color:transparent;border-bottom:1px solid #cccccc;padding:5px 12px 4px 0}.wysiwyg_content ul.spaced_list,.wysiwyg_content ul.bullet_list{padding-bottom:.5em}.wysiwyg_content ul.spaced_list li,.wysiwyg_content ul.bullet_list li{margin-bottom:.5em}.wysiwyg_content ul.bullet_list{margin-left:20px;list-style-type:disc}.wysiwyg_content ol.numbered_list{list-style-type:decimal;margin-left:2em}.wysiwyg_content ol.numbered_list li{margin-bottom:.5em}.wysiwyg_content ul.thumb_row{margin:1em 0}.wysiwyg_content ul.thumb_row li{width:31.81818%;float:left}.wysiwyg_content ul.thumb_row li:nth-child(3n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}.wysiwyg_content ul.thumb_row li:nth-child(3n+2){margin-left:34.09091%;margin-right:-100%;clear:none}.wysiwyg_content ul.thumb_row li:nth-child(3n+3){margin-left:68.18182%;margin-right:-100%;clear:none}@media (min-width: 480px){.wysiwyg_content ul.thumb_row li{width:18.36735%;float:left}.wysiwyg_content ul.thumb_row li:nth-child(5n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}.wysiwyg_content ul.thumb_row li:nth-child(5n+2){margin-left:20.40816%;margin-right:-100%;clear:none}.wysiwyg_content ul.thumb_row li:nth-child(5n+3){margin-left:40.81633%;margin-right:-100%;clear:none}.wysiwyg_content ul.thumb_row li:nth-child(5n+4){margin-left:61.22449%;margin-right:-100%;clear:none}.wysiwyg_content ul.thumb_row li:nth-child(5n+5){margin-left:81.63265%;margin-right:-100%;clear:none}}.wysiwyg_content ul.thumb_row li p{font-size:.9em;text-align:center}.wysiwyg_content .hr_custom{display:block;height:1px;border:0;border-top:1px solid #ccc;margin:1em 0;padding:0}.wysiwyg_content ul.image_text_list,.wysiwyg_content ul.image_text_sublist,.wysiwyg_content ul.small_image_text_list{margin-bottom:2em}#secondary_column .wysiwyg_content ul.image_text_list,#secondary_column .wysiwyg_content ul.image_text_sublist,#secondary_column .wysiwyg_content ul.small_image_text_list{margin-bottom:0}.wysiwyg_content ul.image_text_list li,.wysiwyg_content ul.image_text_sublist li,.wysiwyg_content ul.small_image_text_list li{border-bottom:1px solid #cccccc;overflow:hidden;*zoom:1;padding:1.5em 0 1.5em}.wysiwyg_content ul.image_text_list li a,.wysiwyg_content ul.image_text_sublist li a,.wysiwyg_content ul.small_image_text_list li a{text-decoration:none;cursor:pointer}#secondary_column .wysiwyg_content ul.image_text_list li:first-child,#secondary_column .wysiwyg_content ul.image_text_sublist li:first-child,#secondary_column .wysiwyg_content ul.small_image_text_list li:first-child{padding-top:.5em}.wysiwyg_content ul.image_text_list li:last-child,.wysiwyg_content ul.image_text_sublist li:last-child,.wysiwyg_content ul.small_image_text_list li:last-child{border-bottom:none}.wysiwyg_content ul.image_text_list .image_text_container,.wysiwyg_content ul.image_text_sublist .image_text_container,.wysiwyg_content ul.small_image_text_list .image_text_container{position:relative}.wysiwyg_content ul.image_text_list .image_text_container .img,.wysiwyg_content ul.image_text_sublist .image_text_container .img,.wysiwyg_content ul.small_image_text_list .image_text_container .img{float:right;margin-left:4%;margin-bottom:.5em;width:23%}@media (min-width: 600px){.wysiwyg_content ul.image_text_list .image_text_container .img,.wysiwyg_content ul.image_text_sublist .image_text_container .img,.wysiwyg_content ul.small_image_text_list .image_text_container .img{float:left;margin:0 3% 0 0}#secondary_column .wysiwyg_content ul.image_text_list .image_text_container .img,#secondary_column .wysiwyg_content ul.image_text_sublist .image_text_container .img,#secondary_column .wysiwyg_content ul.small_image_text_list .image_text_container .img{margin-right:4%;width:27%}}.wysiwyg_content ul.image_text_list .image_text_container .list_text_content,.wysiwyg_content ul.image_text_sublist .image_text_container .list_text_content,.wysiwyg_content ul.small_image_text_list .image_text_container .list_text_content{width:auto}@media (min-width: 600px){.wysiwyg_content ul.image_text_list .image_text_container .list_text_content,.wysiwyg_content ul.image_text_sublist .image_text_container .list_text_content,.wysiwyg_content ul.small_image_text_list .image_text_container .list_text_content{width:73%;float:left}#secondary_column .wysiwyg_content ul.image_text_list .image_text_container .list_text_content,#secondary_column .wysiwyg_content ul.image_text_sublist .image_text_container .list_text_content,#secondary_column .wysiwyg_content ul.small_image_text_list .image_text_container .list_text_content{width:69%}}.wysiwyg_content ul.image_text_list .image_text_container .date,.wysiwyg_content ul.image_text_sublist .image_text_container .date,.wysiwyg_content ul.small_image_text_list .image_text_container .date{font-size:.9em;margin-bottom:.3em;color:#222222}.wysiwyg_content ul.image_text_list .image_text_container .content_title,.wysiwyg_content ul.image_text_sublist .image_text_container .content_title,.wysiwyg_content ul.small_image_text_list .image_text_container .content_title{display:block;font-weight:600;text-decoration:none;color:black;cursor:pointer;letter-spacing:-.025em;line-height:1.3em;font-size:1.04em;margin-bottom:0em}@media (min-width: 600px){.wysiwyg_content ul.image_text_list .image_text_container .content_title,.wysiwyg_content ul.image_text_sublist .image_text_container .content_title,.wysiwyg_content ul.small_image_text_list .image_text_container .content_title{font-size:1.2em;margin-bottom:0em}}@media (min-width: 769px){.wysiwyg_content ul.image_text_list .image_text_container .content_title,.wysiwyg_content ul.image_text_sublist .image_text_container .content_title,.wysiwyg_content ul.small_image_text_list .image_text_container .content_title{font-size:1.36em;margin-bottom:0em}}@media (min-width: 1024px){.wysiwyg_content ul.image_text_list .image_text_container .content_title,.wysiwyg_content ul.image_text_sublist .image_text_container .content_title,.wysiwyg_content ul.small_image_text_list .image_text_container .content_title{font-size:1.44em;margin-bottom:0em}}@media (min-width: 1200px){.wysiwyg_content ul.image_text_list .image_text_container .content_title,.wysiwyg_content ul.image_text_sublist .image_text_container .content_title,.wysiwyg_content ul.small_image_text_list .image_text_container .content_title{font-size:1.52em;margin-bottom:0em}}#secondary_column .wysiwyg_content ul.image_text_list .image_text_container .content_title,#secondary_column .wysiwyg_content ul.image_text_sublist .image_text_container .content_title,#secondary_column .wysiwyg_content ul.small_image_text_list .image_text_container .content_title{font-size:0.78em;margin-bottom:0em}@media (min-width: 600px){#secondary_column .wysiwyg_content ul.image_text_list .image_text_container .content_title,#secondary_column .wysiwyg_content ul.image_text_sublist .image_text_container .content_title,#secondary_column .wysiwyg_content ul.small_image_text_list .image_text_container .content_title{font-size:0.9em;margin-bottom:0em}}@media (min-width: 769px){#secondary_column .wysiwyg_content ul.image_text_list .image_text_container .content_title,#secondary_column .wysiwyg_content ul.image_text_sublist .image_text_container .content_title,#secondary_column .wysiwyg_content ul.small_image_text_list .image_text_container .content_title{font-size:1.02em;margin-bottom:0em}}@media (min-width: 1024px){#secondary_column .wysiwyg_content ul.image_text_list .image_text_container .content_title,#secondary_column .wysiwyg_content ul.image_text_sublist .image_text_container .content_title,#secondary_column .wysiwyg_content ul.small_image_text_list .image_text_container .content_title{font-size:1.08em;margin-bottom:0em}}@media (min-width: 1200px){#secondary_column .wysiwyg_content ul.image_text_list .image_text_container .content_title,#secondary_column .wysiwyg_content ul.image_text_sublist .image_text_container .content_title,#secondary_column .wysiwyg_content ul.small_image_text_list .image_text_container .content_title{font-size:1.14em;margin-bottom:0em}}.wysiwyg_content ul.image_text_list .image_text_container .content_title a,.wysiwyg_content ul.image_text_sublist .image_text_container .content_title a,.wysiwyg_content ul.small_image_text_list .image_text_container .content_title a{color:black}.wysiwyg_content ul.image_text_list .image_text_container .article_teaser_body,.wysiwyg_content ul.image_text_sublist .image_text_container .article_teaser_body,.wysiwyg_content ul.small_image_text_list .image_text_container .article_teaser_body{font-size:1em}.wysiwyg_content ul.image_text_list .image_text_container .article_teaser_body&gt;:first-child,.wysiwyg_content ul.image_text_sublist .image_text_container .article_teaser_body&gt;:first-child,.wysiwyg_content ul.small_image_text_list .image_text_container .article_teaser_body&gt;:first-child{margin-top:.5em}.wysiwyg_content ul.image_text_list .image_text_container .article_teaser_body&gt;:last-child,.wysiwyg_content ul.image_text_sublist .image_text_container .article_teaser_body&gt;:last-child,.wysiwyg_content ul.small_image_text_list .image_text_container .article_teaser_body&gt;:last-child{margin-bottom:0}#secondary_column .wysiwyg_content ul.image_text_list .image_text_container .article_teaser_body,#secondary_column .wysiwyg_content ul.image_text_sublist .image_text_container .article_teaser_body,#secondary_column .wysiwyg_content ul.small_image_text_list .image_text_container .article_teaser_body{font-size:.9em}#primary_column .wysiwyg_content&gt;ul.image_text_list:first-child li:first-child,#primary_column .wysiwyg_content&gt;ul.image_text_sublist:first-child li:first-child,#primary_column .wysiwyg_content&gt;ul.small_image_text_list:first-child li:first-child{padding-top:0}.wysiwyg_content ul.image_text_sublist{margin-top:0}.wysiwyg_content ul.image_text_sublist li{border-bottom:none}.wysiwyg_content ul.image_text_sublist li:first-child{padding-top:0}@media (min-width: 600px){.wysiwyg_content ul.image_text_sublist{margin-left:9%}}.wysiwyg_content ul.image_text_sublist .image_text_container .img{width:15%}.wysiwyg_content ul.image_text_sublist .image_text_container .content_title{font-size:0.975em;margin-bottom:0em;letter-spacing:-.02em}@media (min-width: 600px){.wysiwyg_content ul.image_text_sublist .image_text_container .content_title{font-size:1.125em;margin-bottom:0em}}@media (min-width: 769px){.wysiwyg_content ul.image_text_sublist .image_text_container .content_title{font-size:1.275em;margin-bottom:0em}}@media (min-width: 1024px){.wysiwyg_content ul.image_text_sublist .image_text_container .content_title{font-size:1.35em;margin-bottom:0em}}@media (min-width: 1200px){.wysiwyg_content ul.image_text_sublist .image_text_container .content_title{font-size:1.425em;margin-bottom:0em}}.wysiwyg_content ul.small_image_text_list .image_text_container .img{width:15%}@media (min-width: 600px){.wysiwyg_content ul.small_image_text_list .image_text_container .list_text_content{width:80%}}.wysiwyg_content ul.small_image_text_list .image_text_container .list_text_content .content_title{font-size:0.975em;margin-bottom:0em;letter-spacing:-.02em}@media (min-width: 600px){.wysiwyg_content ul.small_image_text_list .image_text_container .list_text_content .content_title{font-size:1.125em;margin-bottom:0em}}@media (min-width: 769px){.wysiwyg_content ul.small_image_text_list .image_text_container .list_text_content .content_title{font-size:1.275em;margin-bottom:0em}}@media (min-width: 1024px){.wysiwyg_content ul.small_image_text_list .image_text_container .list_text_content .content_title{font-size:1.35em;margin-bottom:0em}}@media (min-width: 1200px){.wysiwyg_content ul.small_image_text_list .image_text_container .list_text_content .content_title{font-size:1.425em;margin-bottom:0em}}.wysiwyg_content .pagination{height:40px}.wysiwyg_content .pagination .previous{float:left}.wysiwyg_content .pagination .next{float:right}.wysiwyg_content .content_grid{margin:1.5em 0}.wysiwyg_content .content_grid:after{content:"";display:table;clear:both}.wysiwyg_content .content_grid .slide{margin-bottom:1.69492%;width:49.15254%;float:left}.wysiwyg_content .content_grid .slide:nth-child(2n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}.wysiwyg_content .content_grid .slide:nth-child(2n+2){margin-left:50.84746%;margin-right:-100%;clear:none}@media (min-width: 769px){.wysiwyg_content .content_grid .slide{width:23.72881%;float:left}.wysiwyg_content .content_grid .slide:nth-child(4n+1){margin-left:0;margin-right:-100%;clear:both;margin-left:0}.wysiwyg_content .content_grid .slide:nth-child(4n+2){margin-left:25.42373%;margin-right:-100%;clear:none}.wysiwyg_content .content_grid .slide:nth-child(4n+3){margin-left:50.84746%;margin-right:-100%;clear:none}.wysiwyg_content .content_grid .slide:nth-child(4n+4){margin-left:76.27119%;margin-right:-100%;clear:none}}@media (min-width: 600px){.wysiwyg_content .main_area_sitemap .sitemap .grid_layout{width:100%}}.wysiwyg_content .main_area_sitemap .sitemap_directory{overflow:hidden;*zoom:1}.wysiwyg_content .main_area_sitemap .sitemap_title{text-transform:capitalize}.wysiwyg_content .main_area_sitemap .sitemap_block{text-align:center;width:100%}@media (min-width: 600px){.wysiwyg_content .main_area_sitemap .sitemap_block{-moz-box-sizing:border-box;-webkit-box-sizing:border-box;box-sizing:border-box;width:25%;float:left;padding-left:0.83333%;padding-right:0.83333%;text-align:left}}@media (min-width: 600px){.wysiwyg_content .main_area_sitemap .subnav li{padding-left:1em;text-indent:-1em;margin:.1em 0}}.tooltipsy{background-color:rgba(250,250,250,0.8);font-size:.8em;padding:.4em .7em;color:#000;border-radius:6px;z-index:10;border:1px solid #e4e9ef}#main_container form.gsc-search-box{padding:0}#main_container form.gsc-search-box td.gsc-input{padding:0}#main_container.placeholder{-webkit-font-smoothing:antialiased}#main_container:-moz-placeholder{-webkit-font-smoothing:antialiased}#main_container::-moz-placeholder{-webkit-font-smoothing:antialiased}#main_container::-webkit-input-placeholder{-webkit-font-smoothing:antialiased}#main_container .gsc-tabsArea{border-color:#4b6a8d}#main_container .gsc-tabsArea&gt;div{overflow:hidden;position:relative;bottom:-2px}#main_container .gsc-tabsArea .gsc-tabhInactive{border-bottom:1px solid #4b6a8d}#main_container .gsc-tabsArea .gsc-tabhActive{border-color:#4b6a8d;border-bottom:none}#main_container .gcsc-branding{display:none}#main_container .gsc-control-cse table{margin:0}#main_container .gsc-input-box{height:auto;border-radius:6px;border-color:#B3BEC8;height:38px}#main_container .gsc-input-box .gsib_a{padding-top:9px;vertical-align:top}#main_container .gsc-input-box .gsib_b{padding-top:8px}#main_container .gsc-input-box .gsib_b a:hover{border-bottom:none}#main_container input.gsc-input{padding:12px 0 0 0;font-size:16px}#main_container td.gsc-search-button{padding-left:9px}#main_container input.gsc-search-button{border-radius:6px;height:38px;color:white;font-size:16px;font-weight:500;text-transform:uppercase;background:#4b6a8d url("https://www.jpl.nasa.gov/assets/images/search_icon.png") no-repeat center}#main_container input.gsc-search-button:hover{background-color:#6083aa}#main_container .gsc-selected-option-container{width:auto !important;max-width:none}#main_container td.gsc-clear-button{padding-left:4px}#main_container .cse .gsc-control-cse,#main_container .gsc-control-cse{padding:0}#main_container td.gsc-result-info-container{padding-left:0}#main_container .gs-no-results-result .gs-snippet,#main_container .gs-error-result .gs-snippet{padding:5px 0;margin:5px 0;border:none;background-color:transparent}#main_container .gsc-webResult.gsc-results{margin-top:0px}#main_container table.gsc-table-result{margin-top:13px}#main_container div.gsc-webResult.gsc-result{border-bottom:1px solid #CFD7E1;padding-bottom:16px;padding-top:16px;padding-left:0;margin-bottom:0px;margin-top:0px}#main_container td.gsc-table-cell-snippet-close{padding:0}#main_container div.gs-title{padding:0;height:auto;line-height:1.4em;text-decoration:none}#main_container .gsc-thumbnail-inside,#main_container .gsc-url-top{padding:0}#main_container td.gsc-table-cell-thumbnail{padding-top:3px}#main_container .gs-result a.gs-title,#main_container .gs-result a.gs-title b{color:#388FDA;text-decoration:none;font-weight:600;letter-spacing:-.035em;height:auto;padding:0}@media (min-width: 600px){#main_container .gs-result a.gs-title,#main_container .gs-result a.gs-title b{font-size:18px}}@media (min-width: 769px){#main_container .gs-result a.gs-title,#main_container .gs-result a.gs-title b{font-size:20px}}#main_container a.gs-title:hover{color:#115FA3}#main_container a.gs-title:hover b{color:#115FA3}#main_container .gs-webResult .gs-snippet,#main_container .gs-imageResult .gs-snippet,#main_container .gs-fileFormatType{color:#333;line-height:1.4em}@media (min-width: 1024px){#main_container .gs-webResult .gs-snippet,#main_container .gs-imageResult .gs-snippet,#main_container .gs-fileFormatType{font-size:15px}}#main_container .gs-webResult div.gs-visibleUrl,#main_container .gs-imageResult div.gs-visibleUrl{color:#888}#main_container .gsc-table-cell-thumbnail{padding:0 6px 0 0}@media (min-width: 600px){#main_container .gsc-table-cell-thumbnail{padding:0 12px 0 0}}@media (min-width: 1024px){#main_container .gsc-table-cell-thumbnail{padding:0 16px 0 0}}#main_container .gs-web-image-box{width:100px}@media (min-width: 600px){#main_container .gs-web-image-box{padding:0;width:125px}}#main_container img.gs-image,#main_container .gs-promotion-image-box img.gs-promotion-image{border:none;width:100%;height:auto;max-width:none;max-height:none}#main_container a.gs-image{display:block}#main_container .gsc-results .gsc-cursor-box{padding-top:2px}#main_container .gsc-results .gsc-cursor-box .gsc-cursor-page{color:#388FDA;font-size:17px}#main_container .gsc-results .gsc-cursor-box .gsc-cursor-current-page{color:#333;background-color:transparent;text-shadow:none;padding:0}#main_container .gsc-adBlock{display:none !important}#search article{overflow:visible}
      </style>
      <style data-href="/assets/stylesheets/print.css" media="print">
       .print_only{display:block}.print_logo{position:absolute;top:0;left:0}div#site_body{padding-top:3em}.site_header_area{top:0;position:absolute}.site_header_area.fixed{position:absolute !important}.site_header_area .brand1,.site_header_area .brand2{display:none}.content_page.module{padding-top:0}#missions_detail .content_page.module{padding-top:2em}.header_mask{height:30px}.custom_banner_container{height:68px}.custom_banner_container img{display:none}.custom_banner_container .banner_header_overlay{display:none}a[href]:after{content:""}.definition_teaser{color:white !important}.triple_teaser .column{width:31%;float:left}.triple_teaser .column+.column{margin-left:1%}#home .homepage_site_teaser .text_col{width:58%;float:left}#home .homepage_site_teaser .img_col{display:block !important;width:40%;float:right}#home .homepage_site_teaser .img_col img{display:block;float:right}#home .site_header_area{position:relative}.module.vital_signs{overflow:hidden;height:600px !important}.homepage_carousel .master-slider{height:auto !important;min-height:1px}.homepage_carousel #vital_signs_modal{height:auto !important;position:relative !important}.homepage_carousel .ms-container{display:none !important}#vital_signs_modal .left_col{width:40%;float:left}#vital_signs_modal .right_col{width:40%;float:right}.vital_signs_menu{margin-top:3em;border:1px solid black;border-width:1px 0}#site_footer .upper_footer,#site_footer .sitemap{display:none}#site_footer .lower_footer .nav_container{display:none}.content_page .main_feature .master-slider{overflow:hidden;text-align:center}.primary_media_feature .carousel_container{display:none}.wysiwyg_content blockquote{border:none}.content_page.module{padding-top:0}#primary_column{width:60%;float:left;overflow:hidden;position:relative;display:block}#secondary_column{width:32%;float:right;position:relative;font-size:80%}.grid_view .module_title{display:block}#fancybox-lock,.fancybox-overlay{display:none}.view_selectors{display:none}.multi_teaser,.teasers_module,.multimedia_teaser,.filter_bar,.tertiary_nav_container,.secondary_nav_mobile,.carousel_teaser,.image_of_the_day{display:none}
      </style>
      <script async="" src="https://www.google-analytics.com/analytics.js">
      </script>
      <script src="/assets/javascripts/public_manifest.js" type="text/javascript">
      </script>
      <style type="text/css">
      </style>
      <style>
      </style>
      <script src="/assets/javascripts/vendor/jquery.fancybox.js" type="text/javascript">
      </script>
      <script src="/assets/javascripts/vendor/jquery.fancybox-thumbs.js" type="text/javascript">
      </script>
      <style type="text/css">
       .fancybox-margin{margin-right:17px;}
      </style>
      <style type="text/css">
       .at-icon{fill:#fff;border:0}.at-icon-wrapper{display:inline-block;overflow:hidden}a .at-icon-wrapper{cursor:pointer}.at-rounded,.at-rounded-element .at-icon-wrapper{border-radius:12%}.at-circular,.at-circular-element .at-icon-wrapper{border-radius:50%}.addthis_32x32_style .at-icon{width:2pc;height:2pc}.addthis_24x24_style .at-icon{width:24px;height:24px}.addthis_20x20_style .at-icon{width:20px;height:20px}.addthis_16x16_style .at-icon{width:1pc;height:1pc}#at16lb{display:none;position:absolute;top:0;left:0;width:100%;height:100%;z-index:1001;background-color:#000;opacity:.001}#at_complete,#at_error,#at_share,#at_success{position:static!important}.at15dn{display:none}#at15s,#at16p,#at16p form input,#at16p label,#at16p textarea,#at_share .at_item{font-family:arial,helvetica,tahoma,verdana,sans-serif!important;font-size:9pt!important;outline-style:none;outline-width:0;line-height:1em}* html #at15s.mmborder{position:absolute!important}#at15s.mmborder{position:fixed!important;width:250px!important}#at15s{background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAoAAAAKCAYAAACNMs+9AAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAABtJREFUeNpiZGBgaGAgAjAxEAlGFVJHIUCAAQDcngCUgqGMqwAAAABJRU5ErkJggg==);float:none;line-height:1em;margin:0;overflow:visible;padding:5px;text-align:left;position:absolute}#at15s a,#at15s span{outline:0;direction:ltr;text-transform:none}#at15s .at-label{margin-left:5px}#at15s .at-icon-wrapper{width:1pc;height:1pc;vertical-align:middle}#at15s .at-icon{width:1pc;height:1pc}.at4-icon{display:inline-block;background-repeat:no-repeat;background-position:top left;margin:0;overflow:hidden;cursor:pointer}.addthis_16x16_style .at4-icon,.addthis_default_style .at4-icon,.at4-icon,.at-16x16{width:1pc;height:1pc;line-height:1pc;background-size:1pc!important}.addthis_32x32_style .at4-icon,.at-32x32{width:2pc;height:2pc;line-height:2pc;background-size:2pc!important}.addthis_24x24_style .at4-icon,.at-24x24{width:24px;height:24px;line-height:24px;background-size:24px!important}.addthis_20x20_style .at4-icon,.at-20x20{width:20px;height:20px;line-height:20px;background-size:20px!important}.at4-icon.circular,.circular .at4-icon,.circular.aticon{border-radius:50%}.at4-icon.rounded,.rounded .at4-icon{border-radius:4px}.at4-icon-left{float:left}#at15s .at4-icon{text-indent:20px;padding:0;overflow:visible;white-space:nowrap;background-size:1pc;width:1pc;height:1pc;background-position:top left;display:inline-block;line-height:1pc}.addthis_vertical_style .at4-icon,.at4-follow-container .at4-icon{margin-right:5px}html&gt;body #at15s{width:250px!important}#at15s.atm{background:none!important;padding:0!important;width:10pc!important}#at15s_inner{background:#fff;border:1px solid #fff;margin:0}#at15s_head{position:relative;background:#f2f2f2;padding:4px;cursor:default;border-bottom:1px solid #e5e5e5}.at15s_head_success{background:#cafd99!important;border-bottom:1px solid #a9d582!important}.at15s_head_success a,.at15s_head_success span{color:#000!important;text-decoration:none}#at15s_brand,#at15sptx,#at16_brand{position:absolute}#at15s_brand{top:4px;right:4px}.at15s_brandx{right:20px!important}a#at15sptx{top:4px;right:4px;text-decoration:none;color:#4c4c4c;font-weight:700}#at15sptx:hover{text-decoration:underline}#at16_brand{top:5px;right:30px;cursor:default}#at_hover{padding:4px}#at_hover .at_item,#at_share .at_item{background:#fff!important;float:left!important;color:#4c4c4c!important}#at_share .at_item .at-icon-wrapper{margin-right:5px}#at_hover .at_bold{font-weight:700;color:#000!important}#at_hover .at_item{width:7pc!important;padding:2px 3px!important;margin:1px;text-decoration:none!important}#at_hover .at_item.athov,#at_hover .at_item:focus,#at_hover .at_item:hover{margin:0!important}#at_hover .at_item.athov,#at_hover .at_item:focus,#at_hover .at_item:hover,#at_share .at_item.athov,#at_share .at_item:hover{background:#f2f2f2!important;border:1px solid #e5e5e5;color:#000!important;text-decoration:none}.ipad #at_hover .at_item:focus{background:#fff!important;border:1px solid #fff}.at15t{display:block!important;height:1pc!important;line-height:1pc!important;padding-left:20px!important;background-position:0 0;text-align:left}.addthis_button,.at15t{cursor:pointer}.addthis_toolbox a.at300b,.addthis_toolbox a.at300m{width:auto}.addthis_toolbox a{margin-bottom:5px;line-height:initial}.addthis_toolbox.addthis_vertical_style{width:200px}.addthis_button_facebook_like .fb_iframe_widget{line-height:100%}.addthis_button_facebook_like iframe.fb_iframe_widget_lift{max-width:none}.addthis_toolbox a.addthis_button_counter,.addthis_toolbox a.addthis_button_facebook_like,.addthis_toolbox a.addthis_button_facebook_send,.addthis_toolbox a.addthis_button_facebook_share,.addthis_toolbox a.addthis_button_foursquare,.addthis_toolbox a.addthis_button_google_plusone,.addthis_toolbox a.addthis_button_linkedin_counter,.addthis_toolbox a.addthis_button_pinterest_pinit,.addthis_toolbox a.addthis_button_stumbleupon_badge,.addthis_toolbox a.addthis_button_tweet{display:inline-block}.at-share-tbx-element .google_plusone_iframe_widget&gt;span&gt;div{vertical-align:top!important}.addthis_toolbox span.addthis_follow_label{display:none}.addthis_toolbox.addthis_vertical_style span.addthis_follow_label{display:block;white-space:nowrap}.addthis_toolbox.addthis_vertical_style a{display:block}.addthis_toolbox.addthis_vertical_style.addthis_32x32_style a{line-height:2pc;height:2pc}.addthis_toolbox.addthis_vertical_style .at300bs{margin-right:4px;float:left}.addthis_toolbox.addthis_20x20_style span{line-height:20px}.addthis_toolbox.addthis_32x32_style span{line-height:2pc}.addthis_toolbox.addthis_pill_combo_style .addthis_button_compact .at15t_compact,.addthis_toolbox.addthis_pill_combo_style a{float:left}.addthis_toolbox.addthis_pill_combo_style a.addthis_button_tweet{margin-top:-2px}.addthis_toolbox.addthis_pill_combo_style .addthis_button_compact .at15t_compact{margin-right:4px}.addthis_default_style .addthis_separator{margin:0 5px;display:inline}div.atclear{clear:both}.addthis_default_style .addthis_separator,.addthis_default_style .at4-icon,.addthis_default_style .at300b,.addthis_default_style .at300bo,.addthis_default_style .at300bs,.addthis_default_style .at300m{float:left}.at300b img,.at300bo img{border:0}a.at300b .at4-icon,a.at300m .at4-icon{display:block}.addthis_default_style .at300b,.addthis_default_style .at300bo,.addthis_default_style .at300m{padding:0 2px}.at300b,.at300bo,.at300bs,.at300m{cursor:pointer}.addthis_button_facebook_like.at300b:hover,.addthis_button_facebook_like.at300bs:hover,.addthis_button_facebook_send.at300b:hover,.addthis_button_facebook_send.at300bs:hover{opacity:1}.addthis_20x20_style .at15t,.addthis_20x20_style .at300bs{overflow:hidden;display:block;height:20px!important;width:20px!important;line-height:20px!important}.addthis_32x32_style .at15t,.addthis_32x32_style .at300bs{overflow:hidden;display:block;height:2pc!important;width:2pc!important;line-height:2pc!important}.at300bs{overflow:hidden;display:block;background-position:0 0;height:1pc;width:1pc;line-height:1pc!important}.addthis_default_style .at15t_compact,.addthis_default_style .at15t_expanded{margin-right:4px}#at_share .at_item{width:123px!important;padding:4px;margin-right:2px;border:1px solid #fff}#at16p{background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAoAAAAKCAYAAACNMs+9AAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAABtJREFUeNpiZGBgaGAgAjAxEAlGFVJHIUCAAQDcngCUgqGMqwAAAABJRU5ErkJggg==);z-index:10000001;position:absolute;top:50%;left:50%;width:300px;padding:10px;margin:0 auto;margin-top:-185px;margin-left:-155px;font-family:arial,helvetica,tahoma,verdana,sans-serif;font-size:9pt;color:#5e5e5e}#at_share{margin:0;padding:0}#at16pt{position:relative;background:#f2f2f2;height:13px;padding:5px 10px}#at16pt a,#at16pt h4{font-weight:700}#at16pt h4{display:inline;margin:0;padding:0;font-size:9pt;color:#4c4c4c;cursor:default}#at16pt a{position:absolute;top:5px;right:10px;color:#4c4c4c;text-decoration:none;padding:2px}#at15sptx:focus,#at16pt a:focus{outline:thin dotted}#at15s #at16pf a{top:1px}#_atssh{width:1px!important;height:1px!important;border:0!important}.atm{width:10pc!important;padding:0;margin:0;line-height:9pt;letter-spacing:normal;font-family:arial,helvetica,tahoma,verdana,sans-serif;font-size:9pt;color:#444;background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAoAAAAKCAYAAACNMs+9AAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAABtJREFUeNpiZGBgaGAgAjAxEAlGFVJHIUCAAQDcngCUgqGMqwAAAABJRU5ErkJggg==);padding:4px}.atm-f{text-align:right;border-top:1px solid #ddd;padding:5px 8px}.atm-i{background:#fff;border:1px solid #d5d6d6;padding:0;margin:0;box-shadow:1px 1px 5px rgba(0,0,0,.15)}.atm-s{margin:0!important;padding:0!important}.atm-s a:focus{border:transparent;outline:0;transition:none}#at_hover.atm-s a,.atm-s a{display:block;text-decoration:none;padding:4px 10px;color:#235dab!important;font-weight:400;font-style:normal;transition:none}#at_hover.atm-s .at_bold{color:#235dab!important}#at_hover.atm-s a:hover,.atm-s a:hover{background:#2095f0;text-decoration:none;color:#fff!important}#at_hover.atm-s .at_bold{font-weight:700}#at_hover.atm-s a:hover .at_bold{color:#fff!important}.atm-s a .at-label{vertical-align:middle;margin-left:5px;direction:ltr}.at_PinItButton{display:block;width:40px;height:20px;padding:0;margin:0;background-image:url(//s7.addthis.com/static/t00/pinit00.png);background-repeat:no-repeat}.at_PinItButton:hover{background-position:0 -20px}.addthis_toolbox .addthis_button_pinterest_pinit{position:relative}.at-share-tbx-element .fb_iframe_widget span{vertical-align:baseline!important}#at16pf{height:auto;text-align:right;padding:4px 8px}.at-privacy-info{position:absolute;left:7px;bottom:7px;cursor:pointer;text-decoration:none;font-family:helvetica,arial,sans-serif;font-size:10px;line-height:9pt;letter-spacing:.2px;color:#666}.at-privacy-info:hover{color:#000}.body .wsb-social-share .wsb-social-share-button-vert{padding-top:0;padding-bottom:0}.body .wsb-social-share.addthis_counter_style .addthis_button_tweet.wsb-social-share-button{padding-top:40px}.body .wsb-social-share.addthis_counter_style .addthis_button_google_plusone.wsb-social-share-button{padding-top:0}.body .wsb-social-share.addthis_counter_style .addthis_button_facebook_like.wsb-social-share-button{padding-top:21px}@media print{#at4-follow,#at4-share,#at4-thankyou,#at4-whatsnext,#at4m-mobile,#at15s,.at4,.at4-recommended{display:none!important}}@media screen and (max-width:400px){.at4win{width:100%}}@media screen and (max-height:700px) and (max-width:400px){.at4-thankyou-inner .at4-recommended-container{height:122px;overflow:hidden}.at4-thankyou-inner .at4-recommended .at4-recommended-item:first-child{border-bottom:1px solid #c5c5c5}}
      </style>
      <style type="text/css">
       .at-branding-logo{font-family:helvetica,arial,sans-serif;text-decoration:none;font-size:10px;display:inline-block;margin:2px 0;letter-spacing:.2px}.at-branding-logo .at-branding-icon{background-image:url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAoAAAAKCAMAAAC67D+PAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAAZQTFRF////+GlNUkcc1QAAAB1JREFUeNpiYIQDBjQmAwMmkwEM0JnY1WIxFyDAABGeAFEudiZsAAAAAElFTkSuQmCC")}.at-branding-logo .at-branding-icon,.at-branding-logo .at-privacy-icon{display:inline-block;height:10px;width:10px;margin-left:4px;margin-right:3px;margin-bottom:-1px;background-repeat:no-repeat}.at-branding-logo .at-privacy-icon{background-image:url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAkAAAAKCAMAAABR24SMAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAABhQTFRF8fr9ot/xXcfn2/P5AKva////////AKTWodjhjAAAAAd0Uk5T////////ABpLA0YAAAA6SURBVHjaJMzBDQAwCAJAQaj7b9xifV0kUKJ9ciWxlzWEWI5gMF65KUTv0VKkjVeTerqE/x7+9BVgAEXbAWI8QDcfAAAAAElFTkSuQmCC")}.at-branding-logo span{text-decoration:none}.at-branding-logo .at-branding-addthis,.at-branding-logo .at-branding-powered-by{color:#666}.at-branding-logo .at-branding-addthis:hover{color:#333}.at-cv-with-image .at-branding-addthis,.at-cv-with-image .at-branding-addthis:hover{color:#fff}a.at-branding-logo:visited{color:initial}.at-branding-info{display:inline-block;padding:0 5px;color:#666;border:1px solid #666;border-radius:50%;font-size:10px;line-height:9pt;opacity:.7;transition:all .3s ease;text-decoration:none}.at-branding-info span{border:0;clip:rect(0 0 0 0);height:1px;margin:-1px;overflow:hidden;padding:0;position:absolute;width:1px}.at-branding-info:before{content:'i';font-family:Times New Roman}.at-branding-info:hover{color:#0780df;border-color:#0780df}
      </style>
      <script async="" charset="utf-8" src="//s7.addthis.com/static/155.341d8bbafea741725b1c.js" type="text/javascript">
      </script>
      <script async="" charset="utf-8" src="//s7.addthis.com/static/152.ee3c08cb7372f3351376.js" type="text/javascript">
      </script>
     </head>
     <body class="dark_background logged_out mobile_menu" id="images" style="">
      <!--[if lt IE 9]>
          <div class='browsehappy' style='font-size: 30px; color: white; position:absolute; top: 0; margin: 0; height: 3000px; width: 100%; background: #000; z-index: 10000; padding: 5%;'>
            You are using an
            <strong>outdated</strong>
            browser. Please
            <a href='http://browsehappy.com/'>click here</a>
            to upgrade or change your browser.
          </div>
        <![endif]-->
      <div id="main_container">
       <div id="site_body">
        <div class="site_header_area">
         <header class="site_header">
          <div class="brand_area">
           <div class="brand1">
            <a class="nasa_logo" href="http://www.nasa.gov" title="NASA">
             NASA
            </a>
           </div>
           <div class="brand2">
            <div class="jpl_logo">
             <a href="//www.jpl.nasa.gov/" id="jpl_logo" title="Jet Propulsion Laboratory">
              Jet Propulsion Laboratory
             </a>
            </div>
            <div class="caltech_logo">
             <a href="http://www.caltech.edu/" id="caltech_logo" target="_blank" title="California Institute of Technology">
              California Institute of Technology
             </a>
            </div>
           </div>
           <img alt="" class="print_only print_logo" src="/assets/images/logo_nasa_trio_black@2x.png"/>
          </div>
          <a class="visuallyhidden focusable" href="#main">
           Skip Navigation
          </a>
          <div class="nav_area">
           <a class="menu_button" href="javascript:void(0);" id="menu_button" title="menu button">
            <span class="menu_icon">
             menu and search
            </span>
           </a>
          </div>
         </header>
        </div>
        <div class="main_nav_overlay">
         <div class="modal_menu">
          <header class="site_header clearfix">
           <div class="brand_area">
            <div class="brand1">
             <a class="nasa_logo" href="http://www.nasa.gov" title="">
             </a>
            </div>
            <div class="brand2">
             <div class="jpl_logo">
              <a class="" href="" id="jpl_logo" title="">
               Jet Propulsion Laboratory
              </a>
             </div>
             <div class="caltech_logo">
              <a class="" href="" id="caltech_logo" title="">
               California Institute of Technology
              </a>
             </div>
            </div>
            <img alt="" class="print_only print_logo" src="/assets/images/logo_nasa_trio_black@2x.png"/>
           </div>
           <a class="modal_close" id="modal_close" title="close menu">
            close menu
           </a>
           <div class="nav_area">
            <a class="menu_button modal_close" href="javascript:void(0);" id="menu_button" title="menu icon">
             <span class="menu_icon">
              menu
             </span>
            </a>
           </div>
          </header>
          <section class="navigation_area">
           <div class="grid_layout">
            <div class="directory">
             <form action="/search.php" class="overlay_search top_search">
              <input class="search_field" name="q" onblur="this.placeholder = 'search'" onfocus="this.placeholder = ''" placeholder="search" type="text" value=""/>
              <input class="search_submit" type="submit" value=""/>
             </form>
             <div class="nav_item">
              <div class="arrow_box">
               <span class="arrow_down">
               </span>
              </div>
              <h3 class="nav_title">
               <a href="/about">
                about JPL
               </a>
              </h3>
              <ul class="subnav">
               <li>
                <a href="/about">
                 about JPL
                </a>
               </li>
               <li>
                <a href="/about/exec.php">
                 executive council
                </a>
               </li>
               <li>
                <a href="/about/history.php">
                 history
                </a>
               </li>
               <li>
                <a href="/about/reports.php">
                 annual reports
                </a>
               </li>
               <li>
                <a href="/contact_JPL.php">
                 contact us
                </a>
               </li>
               <li>
                <a href="/opportunities/">
                 opportunities
                </a>
               </li>
              </ul>
             </div>
             <div class="gradient_line">
             </div>
             <div class="nav_item">
              <div class="arrow_box">
               <span class="arrow_down">
               </span>
              </div>
              <h3 class="nav_title">
               <a href="/events">
                public events
               </a>
              </h3>
              <ul class="subnav">
               <li>
                <a href="/events">
                 overview
                </a>
               </li>
               <li>
                <a href="/events/tours/views">
                 tours
                </a>
               </li>
               <li>
                <a href="/events/lectures.php">
                 lecture series
                </a>
               </li>
               <li>
                <a href="/events/speakers-bureau.php">
                 speakers bureau
                </a>
               </li>
               <li>
                <a href="/events/team-competitions.php">
                 team competitions
                </a>
               </li>
               <li>
                <a href="/events/special-events.php">
                 special events
                </a>
               </li>
              </ul>
             </div>
             <div class="gradient_line">
             </div>
             <div class="nav_item">
              <div class="arrow_box">
               <span class="arrow_down">
               </span>
              </div>
              <h3 class="nav_title">
               <a href="/edu/">
                education
               </a>
              </h3>
              <ul class="subnav">
               <li>
                <a href="/edu/intern/">
                 Intern
                </a>
               </li>
               <li>
                <a href="/edu/learn/">
                 Learn
                </a>
               </li>
               <li>
                <a href="/edu/teach/">
                 Teach
                </a>
               </li>
               <li>
                <a href="/edu/news/">
                 News
                </a>
               </li>
               <li>
                <a href="/edu/events/">
                 Events
                </a>
               </li>
              </ul>
             </div>
             <div class="gradient_line">
             </div>
             <div class="nav_item">
              <div class="arrow_box">
               <span class="arrow_down">
               </span>
              </div>
              <h3 class="nav_title">
               <a href="/news">
                news
               </a>
              </h3>
              <ul class="subnav">
               <li>
                <a href="/news">
                 latest news
                </a>
               </li>
               <li>
                <a href="/news/presskits.php">
                 press kits
                </a>
               </li>
               <li>
                <a href="/news/factsheets.php">
                 fact sheets
                </a>
               </li>
               <li>
                <a href="/news/mediainformation.php">
                 media information
                </a>
               </li>
               <li>
                <a href="http://blogs.jpl.nasa.gov">
                 blog
                </a>
               </li>
              </ul>
             </div>
             <div class="gradient_line">
             </div>
             <div class="nav_item">
              <div class="arrow_box">
               <span class="arrow_down">
               </span>
              </div>
              <h3 class="nav_title">
               <a href="/missions/">
                missions
               </a>
              </h3>
              <ul class="subnav">
               <li>
                <a href="/missions/?type=current">
                 current
                </a>
               </li>
               <li>
                <a href="/missions/?type=past">
                 past
                </a>
               </li>
               <li>
                <a href="/missions/?type=future">
                 future
                </a>
               </li>
               <li>
                <a href="/missions/?type=proposed">
                 proposed
                </a>
               </li>
               <li>
                <a href="/missions">
                 all
                </a>
               </li>
              </ul>
             </div>
             <div class="gradient_line">
             </div>
             <div class="nav_item">
              <div class="arrow_box">
               <span class="arrow_down">
               </span>
              </div>
              <h3 class="nav_title">
               <a href="/spaceimages">
                galleries
               </a>
              </h3>
              <ul class="subnav">
               <li>
                <a href="/spaceimages">
                 images
                </a>
               </li>
               <li>
                <a href="/videos">
                 videos
                </a>
               </li>
               <li>
                <a href="/infographics">
                 infographics
                </a>
               </li>
               <li>
                <a href="/multimedia/audio.php">
                 audio
                </a>
               </li>
               <li>
                <a href="/apps/">
                 apps
                </a>
               </li>
              </ul>
             </div>
             <div class="gradient_line">
             </div>
             <div class="nav_item centered">
              <h3 class="nav_title">
               <a href="/social">
                Follow JPL
               </a>
              </h3>
              <div class="social_icons">
               <!-- AddThis Button BEGIN -->
               <div class="addthis_toolbox addthis_default_style addthis_32x32_style">
                <a addthis:userid="NASAJPL" class="addthis_button_facebook_follow icon at300b" href="http://www.facebook.com/NASAJPL" target="_blank" title="Follow on Facebook">
                 <span class="at-icon-wrapper" style="background-color: rgb(59, 89, 152); line-height: 32px; height: 32px; width: 32px;">
                  <svg alt="Facebook" aria-labelledby="at-svg-facebook-1" class="at-icon at-icon-facebook" role="img" style="width: 32px; height: 32px;" title="Facebook" version="1.1" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                   <title id="at-svg-facebook-1" xmlns="http://www.w3.org/1999/xhtml">
                    Facebook
                   </title>
                   <g>
                    <path d="M22 5.16c-.406-.054-1.806-.16-3.43-.16-3.4 0-5.733 1.825-5.733 5.17v2.882H9v3.913h3.837V27h4.604V16.965h3.823l.587-3.913h-4.41v-2.5c0-1.123.347-1.903 2.198-1.903H22V5.16z" fill-rule="evenodd">
                    </path>
                   </g>
                  </svg>
                 </span>
                 <span class="addthis_follow_label">
                  Facebook
                 </span>
                </a>
                <a addthis:userid="NASAJPL" class="addthis_button_twitter_follow icon at300b" href="//twitter.com/NASAJPL" target="_blank" title="Follow on Twitter">
                 <span class="at-icon-wrapper" style="background-color: rgb(29, 161, 242); line-height: 32px; height: 32px; width: 32px;">
                  <svg alt="Twitter" aria-labelledby="at-svg-twitter-2" class="at-icon at-icon-twitter" role="img" style="width: 32px; height: 32px;" title="Twitter" version="1.1" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                   <title id="at-svg-twitter-2" xmlns="http://www.w3.org/1999/xhtml">
                    Twitter
                   </title>
                   <g>
                    <path d="M27.996 10.116c-.81.36-1.68.602-2.592.71a4.526 4.526 0 0 0 1.984-2.496 9.037 9.037 0 0 1-2.866 1.095 4.513 4.513 0 0 0-7.69 4.116 12.81 12.81 0 0 1-9.3-4.715 4.49 4.49 0 0 0-.612 2.27 4.51 4.51 0 0 0 2.008 3.755 4.495 4.495 0 0 1-2.044-.564v.057a4.515 4.515 0 0 0 3.62 4.425 4.52 4.52 0 0 1-2.04.077 4.517 4.517 0 0 0 4.217 3.134 9.055 9.055 0 0 1-5.604 1.93A9.18 9.18 0 0 1 6 23.85a12.773 12.773 0 0 0 6.918 2.027c8.3 0 12.84-6.876 12.84-12.84 0-.195-.005-.39-.014-.583a9.172 9.172 0 0 0 2.252-2.336" fill-rule="evenodd">
                    </path>
                   </g>
                  </svg>
                 </span>
                 <span class="addthis_follow_label">
                  Twitter
                 </span>
                </a>
                <a addthis:userid="JPLnews" class="addthis_button_youtube_follow icon at300b" href="http://www.youtube.com/user/JPLnews?sub_confirmation=1" target="_blank" title="Follow on YouTube">
                 <span class="at-icon-wrapper" style="background-color: rgb(205, 32, 31); line-height: 32px; height: 32px; width: 32px;">
                  <svg alt="YouTube" aria-labelledby="at-svg-youtube-3" class="at-icon at-icon-youtube" role="img" style="width: 32px; height: 32px;" title="YouTube" version="1.1" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                   <title id="at-svg-youtube-3" xmlns="http://www.w3.org/1999/xhtml">
                    YouTube
                   </title>
                   <g>
                    <path d="M13.73 18.974V12.57l5.945 3.212-5.944 3.192zm12.18-9.778c-.837-.908-1.775-.912-2.205-.965C20.625 8 16.007 8 16.007 8c-.01 0-4.628 0-7.708.23-.43.054-1.368.058-2.205.966-.66.692-.875 2.263-.875 2.263S5 13.303 5 15.15v1.728c0 1.845.22 3.69.22 3.69s.215 1.57.875 2.262c.837.908 1.936.88 2.426.975 1.76.175 7.482.23 7.482.15 0 .08 4.624.072 7.703-.16.43-.052 1.368-.057 2.205-.965.66-.69.875-2.262.875-2.262s.22-1.845.22-3.69v-1.73c0-1.844-.22-3.69-.22-3.69s-.215-1.57-.875-2.262z" fill-rule="evenodd">
                    </path>
                   </g>
                  </svg>
                 </span>
                 <span class="addthis_follow_label">
                  YouTube
                 </span>
                </a>
                <a addthis:userid="nasajpl" class="addthis_button_instagram_follow icon at300b" href="http://instagram.com/nasajpl" target="_blank" title="Follow on Instagram">
                 <span class="at-icon-wrapper" style="background-color: rgb(224, 53, 102); line-height: 32px; height: 32px; width: 32px;">
                  <svg alt="Instagram" aria-labelledby="at-svg-instagram-4" class="at-icon at-icon-instagram" role="img" style="width: 32px; height: 32px;" title="Instagram" version="1.1" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                   <title id="at-svg-instagram-4" xmlns="http://www.w3.org/1999/xhtml">
                    Instagram
                   </title>
                   <g>
                    <path d="M16 5c-2.987 0-3.362.013-4.535.066-1.17.054-1.97.24-2.67.512a5.392 5.392 0 0 0-1.95 1.268 5.392 5.392 0 0 0-1.267 1.95c-.272.698-.458 1.498-.512 2.67C5.013 12.637 5 13.012 5 16s.013 3.362.066 4.535c.054 1.17.24 1.97.512 2.67.28.724.657 1.337 1.268 1.95a5.392 5.392 0 0 0 1.95 1.268c.698.27 1.498.457 2.67.51 1.172.054 1.547.067 4.534.067s3.362-.013 4.535-.066c1.17-.054 1.97-.24 2.67-.51a5.392 5.392 0 0 0 1.95-1.27 5.392 5.392 0 0 0 1.268-1.95c.27-.698.457-1.498.51-2.67.054-1.172.067-1.547.067-4.534s-.013-3.362-.066-4.535c-.054-1.17-.24-1.97-.51-2.67a5.392 5.392 0 0 0-1.27-1.95 5.392 5.392 0 0 0-1.95-1.267c-.698-.272-1.498-.458-2.67-.512C19.363 5.013 18.988 5 16 5zm0 1.982c2.937 0 3.285.01 4.445.064 1.072.05 1.655.228 2.042.38.514.198.88.437 1.265.822.385.385.624.75.823 1.265.15.387.33.97.38 2.042.052 1.16.063 1.508.063 4.445 0 2.937-.01 3.285-.064 4.445-.05 1.072-.228 1.655-.38 2.042-.198.514-.437.88-.822 1.265-.385.385-.75.624-1.265.823-.387.15-.97.33-2.042.38-1.16.052-1.508.063-4.445.063-2.937 0-3.285-.01-4.445-.064-1.072-.05-1.655-.228-2.042-.38-.514-.198-.88-.437-1.265-.822a3.408 3.408 0 0 1-.823-1.265c-.15-.387-.33-.97-.38-2.042-.052-1.16-.063-1.508-.063-4.445 0-2.937.01-3.285.064-4.445.05-1.072.228-1.655.38-2.042.198-.514.437-.88.822-1.265.385-.385.75-.624 1.265-.823.387-.15.97-.33 2.042-.38 1.16-.052 1.508-.063 4.445-.063zm0 12.685a3.667 3.667 0 1 1 0-7.334 3.667 3.667 0 0 1 0 7.334zm0-9.316a5.65 5.65 0 1 0 0 11.3 5.65 5.65 0 0 0 0-11.3zm7.192-.222a1.32 1.32 0 1 1-2.64 0 1.32 1.32 0 0 1 2.64 0" fill-rule="evenodd">
                    </path>
                   </g>
                  </svg>
                 </span>
                 <span class="addthis_follow_label">
                  Instagram
                 </span>
                </a>
                <a class="icon all_icon" href="/social">
                 <span>
                  All
                 </span>
                </a>
                <div class="atclear">
                </div>
               </div>
              </div>
             </div>
             <form action="/search.php" class="overlay_search">
              <input class="search_field" name="q" onblur="this.placeholder = 'search'" onfocus="this.placeholder = ''" placeholder="search" type="text" value=""/>
              <input class="search_submit" type="submit" value=""/>
             </form>
            </div>
           </div>
          </section>
         </div>
        </div>
        <a name="main">
        </a>
        <div id="page">
         <!-- END HEADER: "DEFAULT" -->
         <!-- START CONTENT -->
         <section class="centered_text clearfix main_feature primary_media_feature single">
          <div class="carousel_container">
           <div class="carousel_items">
            <article alt="Chilean Volcanic Eruption Nighttime View" class="carousel_item" style="background-image: url('/spaceimages/images/wallpaper/PIA19382-1920x1200.jpg');">
             <div class="default floating_text_area ms-layer">
              <h2 class="category_title">
              </h2>
              <h2 class="brand_title">
               FEATURED IMAGE
              </h2>
              <h1 class="media_feature_title">
               Chilean Volcanic Eruption Nighttime View
              </h1>
              <div class="description">
              </div>
              <footer>
               <a class="button fancybox" data-description="The April 18, 2015 eruption of Calbuco Volcano in Chile, as seen by NASA's Terra spacecraft, led to the evacuation of thousands of citizens near the summit, blanketed nearby towns with a layer of ash, and disrupted air traffic." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/mediumsize/PIA19382_ip.jpg" data-link="/spaceimages/details.php?id=PIA19382" data-title="Chilean Volcanic Eruption Nighttime View" id="full_image">
                FULL IMAGE
               </a>
              </footer>
             </div>
             <div class="gradient_container_top">
             </div>
             <div class="gradient_container_bottom">
             </div>
            </article>
           </div>
          </div>
         </section>
         <section class="filter_bar module">
          <div class="grid_layout">
           <header>
            <h2 class="module_title_small">
             Mars Images
            </h2>
            <div class="arrow_box">
             <span class="arrow_down">
             </span>
            </div>
           </header>
           <form action="#submit" class="section_search">
            <div class="search_binder">
             <input class="search_field" name="search" onblur="this.placeholder = 'search'" onfocus="this.placeholder = ''" placeholder="search" type="text" value=""/>
             <input class="search_submit" type="submit" value=""/>
            </div>
            <select name="category" onchange="this.form.submit()">
             <option value="">
              All
             </option>
             <option value="featured">
              Featured
             </option>
             <option value="Asteroids and Comets">
              Asteroids and Comets
             </option>
             <option value="Dwarf Planet">
              Dwarf Planet
             </option>
             <option value="Earth">
              Earth
             </option>
             <option value="Ida">
              Ida
             </option>
             <option value="Jupiter">
              Jupiter
             </option>
             <option selected="selected" value="Mars">
              Mars
             </option>
             <option value="Mercury">
              Mercury
             </option>
             <option value="Neptune">
              Neptune
             </option>
             <option value="Saturn">
              Saturn
             </option>
             <option value="Spacecraft and Technology">
              Spacecraft and Technology
             </option>
             <option value="Spacecraft and Telescope">
              Spacecraft and Telescope
             </option>
             <option value="Sun">
              Sun
             </option>
             <option value="Universe">
              Universe
             </option>
             <option value="Uranus">
              Uranus
             </option>
             <option value="Venus">
              Venus
             </option>
            </select>
           </form>
          </div>
         </section>
         <div class="filter_bar_spanner" style="height: 106px;">
         </div>
         <script src="/assets/javascripts/grid_list_page.js" type="text/javascript">
         </script>
         <script>
          function build_image_item(data){
                var html = "&lt;li class=\"slide\"&gt;";
    			html += "&lt;a class='fancybox' data-fancybox-group='images' data-fancybox-href='" + data.images.full.src +"' data-title='" + data.title + "' data-description='" + data.tease + "' data-link='" + data.link + "' data-thumbnail='" + data.images.thumb.src + "'&gt;";
                html +=       "&lt;div class=\"image_and_description_container\"&gt;";
                html +=         "&lt;div class=\"rollover_description\" style=\"word-wrap: break-word;\"&gt;";
                html +=		      "&lt;h3 class=\"release_date\"&gt;"+data.date+"&lt;\/h3&gt;";
    		    html +=		      "&lt;div class=\"item_tease_overlay\"&gt;"+data.title+"&lt;\/div&gt;";
                html +=           "&lt;div class=\"overlay_arrow\"&gt;";
                html +=             "&lt;img alt=\"more arrow\" src=\"/assets/images/overlay-arrow.png\"&gt;";
                html +=           "&lt;\/div&gt;";
                html +=         "&lt;\/div&gt;";
                html +=         "&lt;div class=\"img\"&gt;&lt;img alt=\""+data.images.thumb.alt+"\" class=\"thumb\" src=\""+data.images.thumb.src+"\"&gt;&lt;\/div&gt;";
                html +=         "&lt;div class=\"list_text_content\"&gt;";
                html +=		      "&lt;div class=\"article_teaser_body\"&gt;"+data.date+"&lt;\/div&gt;";
                html +=           "&lt;div class=\"content_title\"&gt;";
                html +=             data.title
                html +=           "&lt;\/div&gt;";
                html +=           "&lt;div class=\"article_teaser_body\"&gt;"
                html +=             data.tease
                html +=           "&lt;\/div&gt;"
                html +=         "&lt;\/div&gt;"
                html +=       "&lt;\/div&gt;"
                html +=  "&lt;\/a&gt;";
                html +=  "&lt;\/li&gt;";
                return html;
            };
    		$(document).ready(function(){
    			$('ul.articles').more_items({"url": "/assets/json/getMore.php?images=true&amp;" + $.param(mb_utils._getQueryParams()), "build_item_fn": build_image_item})
    		});
         </script>
         <section class="grid_gallery module grid_view">
          <div class="grid_layout">
           <header>
            <h2 class="module_title">
             Mars Images
            </h2>
            <div class="view_selectors">
             <a class="nav_item ir list_icon">
              list view
             </a>
             <a class="nav_item ir grid_icon">
              grid view
             </a>
            </div>
           </header>
           <ul class="articles">
            <li class="slide">
             <a class="fancybox" data-description="This image of Gale Crater from NASA's 2001 Mars Odyssey spacecraft shows part of the huge layered deposit that covers much of the crater floor. The top of the image shows part of the crater rim, including one of the many small channels." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22389_hires.jpg" data-link="/spaceimages/details.php?id=PIA22389" data-thumbnail="/spaceimages/images/wallpaper/PIA22389-640x350.jpg" data-title="Gale Crater">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 10, 2018
                </h3>
                <div class="item_tease_overlay">
                 Gale Crater
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Gale Crater" class="thumb" src="/spaceimages/images/wallpaper/PIA22389-640x350.jpg" title="Gale Crater"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 10, 2018
                </div>
                <div class="content_title">
                 Gale Crater
                </div>
                <div class="article_teaser_body">
                 This image of Gale Crater from NASA's 2001 Mars Odyssey spacecraft shows part of the huge layered deposit that covers much of the crater floor. The top of the image shows part of the crater rim, including one of the many small channels.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's 2001 Mars Odyssey spacecraft shows part of the interior of Candor Chasma. At the bottom of the frame is a bright feature formed by layers of material deposited in the canyon after it formed." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22388_hires.jpg" data-link="/spaceimages/details.php?id=PIA22388" data-thumbnail="/spaceimages/images/wallpaper/PIA22388-640x350.jpg" data-title="Candor Chasma">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 9, 2018
                </h3>
                <div class="item_tease_overlay">
                 Candor Chasma
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Candor Chasma" class="thumb" src="/spaceimages/images/wallpaper/PIA22388-640x350.jpg" title="Candor Chasma"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 9, 2018
                </div>
                <div class="content_title">
                 Candor Chasma
                </div>
                <div class="article_teaser_body">
                 This image from NASA's 2001 Mars Odyssey spacecraft shows part of the interior of Candor Chasma. At the bottom of the frame is a bright feature formed by layers of material deposited in the canyon after it formed.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="The feature that crosses this image captured by NASA's 2001 Mars Odyssey spacecraft is a graben. Graben are formed by tectonic action, where a block of material moves downward between a pair of faults." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22387_hires.jpg" data-link="/spaceimages/details.php?id=PIA22387" data-thumbnail="/spaceimages/images/wallpaper/PIA22387-640x350.jpg" data-title="Labeatis Fossae">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 8, 2018
                </h3>
                <div class="item_tease_overlay">
                 Labeatis Fossae
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Labeatis Fossae" class="thumb" src="/spaceimages/images/wallpaper/PIA22387-640x350.jpg" title="Labeatis Fossae"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 8, 2018
                </div>
                <div class="content_title">
                 Labeatis Fossae
                </div>
                <div class="article_teaser_body">
                 The feature that crosses this image captured by NASA's 2001 Mars Odyssey spacecraft is a graben. Graben are formed by tectonic action, where a block of material moves downward between a pair of faults.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft shows the part of the crater rim and ejecta surrounding Lonar Crater in the northern plains of Vastitas Borealis." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22386_hires.jpg" data-link="/spaceimages/details.php?id=PIA22386" data-thumbnail="/spaceimages/images/wallpaper/PIA22386-640x350.jpg" data-title="Lonar Crater Ejecta">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 7, 2018
                </h3>
                <div class="item_tease_overlay">
                 Lonar Crater Ejecta
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Lonar Crater Ejecta" class="thumb" src="/spaceimages/images/wallpaper/PIA22386-640x350.jpg" title="Lonar Crater Ejecta"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 7, 2018
                </div>
                <div class="content_title">
                 Lonar Crater Ejecta
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft shows the part of the crater rim and ejecta surrounding Lonar Crater in the northern plains of Vastitas Borealis.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft shows one of the numerous unnamed channels in northern Terra Sabaea." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22384_hires.jpg" data-link="/spaceimages/details.php?id=PIA22384" data-thumbnail="/spaceimages/images/wallpaper/PIA22384-640x350.jpg" data-title="Terra Sabaea Channel">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 4, 2018
                </h3>
                <div class="item_tease_overlay">
                 Terra Sabaea Channel
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Terra Sabaea Channel" class="thumb" src="/spaceimages/images/wallpaper/PIA22384-640x350.jpg" title="Terra Sabaea Channel"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 4, 2018
                </div>
                <div class="content_title">
                 Terra Sabaea Channel
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft shows one of the numerous unnamed channels in northern Terra Sabaea.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="A group of dunes captured by NASA's 2001 Mars Odyssey spacecraft is visible on the floor of this unnamed crater in Arabia Terra. The dunes contain basaltic sand, which is darker than the dust covered materials of the rest of the crater." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22383_hires.jpg" data-link="/spaceimages/details.php?id=PIA22383" data-thumbnail="/spaceimages/images/wallpaper/PIA22383-640x350.jpg" data-title="Crater Dunes">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 3, 2018
                </h3>
                <div class="item_tease_overlay">
                 Crater Dunes
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Crater Dunes" class="thumb" src="/spaceimages/images/wallpaper/PIA22383-640x350.jpg" title="Crater Dunes"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 3, 2018
                </div>
                <div class="content_title">
                 Crater Dunes
                </div>
                <div class="article_teaser_body">
                 A group of dunes captured by NASA's 2001 Mars Odyssey spacecraft is visible on the floor of this unnamed crater in Arabia Terra. The dunes contain basaltic sand, which is darker than the dust covered materials of the rest of the crater.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="At the bottom of this image of Daedalia Planum is the uppermost rim of an impact crater. This image was captured by NASA's 2001 Mars Odyssey spacecraft." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22382_hires.jpg" data-link="/spaceimages/details.php?id=PIA22382" data-thumbnail="/spaceimages/images/wallpaper/PIA22382-640x350.jpg" data-title="Daedalia Planum">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 2, 2018
                </h3>
                <div class="item_tease_overlay">
                 Daedalia Planum
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Daedalia Planum" class="thumb" src="/spaceimages/images/wallpaper/PIA22382-640x350.jpg" title="Daedalia Planum"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 2, 2018
                </div>
                <div class="content_title">
                 Daedalia Planum
                </div>
                <div class="article_teaser_body">
                 At the bottom of this image of Daedalia Planum is the uppermost rim of an impact crater. This image was captured by NASA's 2001 Mars Odyssey spacecraft.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's 2001 Mars Odyssey spacecraft runs from northern Juventae Chasma to just short of the southern canyon wall." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22381_hires.jpg" data-link="/spaceimages/details.php?id=PIA22381" data-thumbnail="/spaceimages/images/wallpaper/PIA22381-640x350.jpg" data-title="Juventae Chasma">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 May 1, 2018
                </h3>
                <div class="item_tease_overlay">
                 Juventae Chasma
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Juventae Chasma" class="thumb" src="/spaceimages/images/wallpaper/PIA22381-640x350.jpg" title="Juventae Chasma"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 May 1, 2018
                </div>
                <div class="content_title">
                 Juventae Chasma
                </div>
                <div class="article_teaser_body">
                 This image from NASA's 2001 Mars Odyssey spacecraft runs from northern Juventae Chasma to just short of the southern canyon wall.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This enhanced color image from NASA's Mars Reconnaissance Orbiter shows eroded bedrock on the floor of a large ancient crater." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22439_hires.jpg" data-link="/spaceimages/details.php?id=PIA22439" data-thumbnail="/spaceimages/images/wallpaper/PIA22439-640x350.jpg" data-title="Bedrock on a Crater Floor">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 30, 2018
                </h3>
                <div class="item_tease_overlay">
                 Bedrock on a Crater Floor
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Bedrock on a Crater Floor" class="thumb" src="/spaceimages/images/wallpaper/PIA22439-640x350.jpg" title="Bedrock on a Crater Floor"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 30, 2018
                </div>
                <div class="content_title">
                 Bedrock on a Crater Floor
                </div>
                <div class="article_teaser_body">
                 This enhanced color image from NASA's Mars Reconnaissance Orbiter shows eroded bedrock on the floor of a large ancient crater.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="NASA's Opportunity rover has spent 13 years exploring a small region of Meridiani Planum which has a rather ordinary appearance as seen by NASA's Mars Reconnaissance Orbiter." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22438_hires.jpg" data-link="/spaceimages/details.php?id=PIA22438" data-thumbnail="/spaceimages/images/wallpaper/PIA22438-640x350.jpg" data-title="Exploring Meridiani Planum">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 30, 2018
                </h3>
                <div class="item_tease_overlay">
                 Exploring Meridiani Planum
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Exploring Meridiani Planum" class="thumb" src="/spaceimages/images/wallpaper/PIA22438-640x350.jpg" title="Exploring Meridiani Planum"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 30, 2018
                </div>
                <div class="content_title">
                 Exploring Meridiani Planum
                </div>
                <div class="article_teaser_body">
                 NASA's Opportunity rover has spent 13 years exploring a small region of Meridiani Planum which has a rather ordinary appearance as seen by NASA's Mars Reconnaissance Orbiter.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This color image from NASA's Mars Reconnaissance Orbiter (MRO) shows bedrock layers of diverse colors and composition." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22437_hires.jpg" data-link="/spaceimages/details.php?id=PIA22437" data-thumbnail="/spaceimages/images/wallpaper/PIA22437-640x350.jpg" data-title="Colorful Layers in Ariadnes Colles">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 30, 2018
                </h3>
                <div class="item_tease_overlay">
                 Colorful Layers in Ariadnes Colles
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Colorful Layers in Ariadnes Colles" class="thumb" src="/spaceimages/images/wallpaper/PIA22437-640x350.jpg" title="Colorful Layers in Ariadnes Colles"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 30, 2018
                </div>
                <div class="content_title">
                 Colorful Layers in Ariadnes Colles
                </div>
                <div class="article_teaser_body">
                 This color image from NASA's Mars Reconnaissance Orbiter (MRO) shows bedrock layers of diverse colors and composition.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This enhanced color image from NASA's Mars Reconnaissance Orbiter (MRO) shows the heavily channeled and ancient southern highlands of Mars. The elongated and jagged features are windblown dunes, perhaps hardened and eroded." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22436_hires.jpg" data-link="/spaceimages/details.php?id=PIA22436" data-thumbnail="/spaceimages/images/wallpaper/PIA22436-640x350.jpg" data-title="Channeled Southern Highlands">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 30, 2018
                </h3>
                <div class="item_tease_overlay">
                 Channeled Southern Highlands
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Channeled Southern Highlands" class="thumb" src="/spaceimages/images/wallpaper/PIA22436-640x350.jpg" title="Channeled Southern Highlands"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 30, 2018
                </div>
                <div class="content_title">
                 Channeled Southern Highlands
                </div>
                <div class="article_teaser_body">
                 This enhanced color image from NASA's Mars Reconnaissance Orbiter (MRO) shows the heavily channeled and ancient southern highlands of Mars. The elongated and jagged features are windblown dunes, perhaps hardened and eroded.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft shows one of the numerous unnamed channels located in northern Arabia Terra." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22380_hires.jpg" data-link="/spaceimages/details.php?id=PIA22380" data-thumbnail="/spaceimages/images/wallpaper/PIA22380-640x350.jpg" data-title="Arabia Terra Channel">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 30, 2018
                </h3>
                <div class="item_tease_overlay">
                 Arabia Terra Channel
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Arabia Terra Channel" class="thumb" src="/spaceimages/images/wallpaper/PIA22380-640x350.jpg" title="Arabia Terra Channel"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 30, 2018
                </div>
                <div class="content_title">
                 Arabia Terra Channel
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft shows one of the numerous unnamed channels located in northern Arabia Terra.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's 2001 Mars Odyssey spacecraft shows a section of Bahram Vallis. This channel is located in northern Lunae Planum, south of Kasei Valles." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22379_hires.jpg" data-link="/spaceimages/details.php?id=PIA22379" data-thumbnail="/spaceimages/images/wallpaper/PIA22379-640x350.jpg" data-title="Bahram Vallis">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 27, 2018
                </h3>
                <div class="item_tease_overlay">
                 Bahram Vallis
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Bahram Vallis" class="thumb" src="/spaceimages/images/wallpaper/PIA22379-640x350.jpg" title="Bahram Vallis"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 27, 2018
                </div>
                <div class="content_title">
                 Bahram Vallis
                </div>
                <div class="article_teaser_body">
                 This image from NASA's 2001 Mars Odyssey spacecraft shows a section of Bahram Vallis. This channel is located in northern Lunae Planum, south of Kasei Valles.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft shows the western rim of Bamberg Crater. The complex nature of the rim is one indication of the relative youth of this crater in relation to it's surrounding." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22378_hires.jpg" data-link="/spaceimages/details.php?id=PIA22378" data-thumbnail="/spaceimages/images/wallpaper/PIA22378-640x350.jpg" data-title="Bamberg Crater">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 26, 2018
                </h3>
                <div class="item_tease_overlay">
                 Bamberg Crater
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Bamberg Crater" class="thumb" src="/spaceimages/images/wallpaper/PIA22378-640x350.jpg" title="Bamberg Crater"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 26, 2018
                </div>
                <div class="content_title">
                 Bamberg Crater
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft shows the western rim of Bamberg Crater. The complex nature of the rim is one indication of the relative youth of this crater in relation to it's surrounding.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="The rounded hills in this image from NASA's 2001 Mars Odyssey spacecraft are located in Arcadia Planitia. Broad linear ridges and groups of hills in this region are part of Phlegra Dorsa and Phlegra Montes." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22377_hires.jpg" data-link="/spaceimages/details.php?id=PIA22377" data-thumbnail="/spaceimages/images/wallpaper/PIA22377-640x350.jpg" data-title="Arcadia Planitia Hills">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 25, 2018
                </h3>
                <div class="item_tease_overlay">
                 Arcadia Planitia Hills
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Arcadia Planitia Hills" class="thumb" src="/spaceimages/images/wallpaper/PIA22377-640x350.jpg" title="Arcadia Planitia Hills"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 25, 2018
                </div>
                <div class="content_title">
                 Arcadia Planitia Hills
                </div>
                <div class="article_teaser_body">
                 The rounded hills in this image from NASA's 2001 Mars Odyssey spacecraft are located in Arcadia Planitia. Broad linear ridges and groups of hills in this region are part of Phlegra Dorsa and Phlegra Montes.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="The northern margins of Arabia Terra and Terra Sabaea contain many unnamed channels. This channel is located in Terra Sabaea. The channel flow is toward the top of this image from NASA's 2001 Mars Odyssey spacecraft." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22376_hires.jpg" data-link="/spaceimages/details.php?id=PIA22376" data-thumbnail="/spaceimages/images/wallpaper/PIA22376-640x350.jpg" data-title="Terra Sabaea Channel">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 24, 2018
                </h3>
                <div class="item_tease_overlay">
                 Terra Sabaea Channel
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Terra Sabaea Channel" class="thumb" src="/spaceimages/images/wallpaper/PIA22376-640x350.jpg" title="Terra Sabaea Channel"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 24, 2018
                </div>
                <div class="content_title">
                 Terra Sabaea Channel
                </div>
                <div class="article_teaser_body">
                 The northern margins of Arabia Terra and Terra Sabaea contain many unnamed channels. This channel is located in Terra Sabaea. The channel flow is toward the top of this image from NASA's 2001 Mars Odyssey spacecraft.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft shows one of the mega-gullies that empties into Echus Chasma. Echus Chasma is approximately 4km deep in this region, and is the source of Kasei Valles." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22375_hires.jpg" data-link="/spaceimages/details.php?id=PIA22375" data-thumbnail="/spaceimages/images/wallpaper/PIA22375-640x350.jpg" data-title="Echus Chasma Gully">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 23, 2018
                </h3>
                <div class="item_tease_overlay">
                 Echus Chasma Gully
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Echus Chasma Gully" class="thumb" src="/spaceimages/images/wallpaper/PIA22375-640x350.jpg" title="Echus Chasma Gully"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 23, 2018
                </div>
                <div class="content_title">
                 Echus Chasma Gully
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft shows one of the mega-gullies that empties into Echus Chasma. Echus Chasma is approximately 4km deep in this region, and is the source of Kasei Valles.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft shows a small portion of Lobo Vallis near where it recombines with Kasei Valles and empties into Chryse Planitia." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22374_hires.jpg" data-link="/spaceimages/details.php?id=PIA22374" data-thumbnail="/spaceimages/images/wallpaper/PIA22374-640x350.jpg" data-title="Lobo Vallis">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 20, 2018
                </h3>
                <div class="item_tease_overlay">
                 Lobo Vallis
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Lobo Vallis" class="thumb" src="/spaceimages/images/wallpaper/PIA22374-640x350.jpg" title="Lobo Vallis"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 20, 2018
                </div>
                <div class="content_title">
                 Lobo Vallis
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft shows a small portion of Lobo Vallis near where it recombines with Kasei Valles and empties into Chryse Planitia.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="Located on the western margin of Lunae Planum, Sacra Fossae is a group of linear depressions. The right angle turns and uniform width seen in this image from NASA's 2001 Mars Odyssey spacecraft indicate that these channels were formed by faulting." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22373_hires.jpg" data-link="/spaceimages/details.php?id=PIA22373" data-thumbnail="/spaceimages/images/wallpaper/PIA22373-640x350.jpg" data-title="Sacra Fossae">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 19, 2018
                </h3>
                <div class="item_tease_overlay">
                 Sacra Fossae
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Sacra Fossae" class="thumb" src="/spaceimages/images/wallpaper/PIA22373-640x350.jpg" title="Sacra Fossae"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 19, 2018
                </div>
                <div class="content_title">
                 Sacra Fossae
                </div>
                <div class="article_teaser_body">
                 Located on the western margin of Lunae Planum, Sacra Fossae is a group of linear depressions. The right angle turns and uniform width seen in this image from NASA's 2001 Mars Odyssey spacecraft indicate that these channels were formed by faulting.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="Osuga Valles is a complex set of channels located near Eos Chasma. This image was captured by NASA's 2001 Mars Odyssey spacecraft." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22372_hires.jpg" data-link="/spaceimages/details.php?id=PIA22372" data-thumbnail="/spaceimages/images/wallpaper/PIA22372-640x350.jpg" data-title="Osuga Valles">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 18, 2018
                </h3>
                <div class="item_tease_overlay">
                 Osuga Valles
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Osuga Valles" class="thumb" src="/spaceimages/images/wallpaper/PIA22372-640x350.jpg" title="Osuga Valles"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 18, 2018
                </div>
                <div class="content_title">
                 Osuga Valles
                </div>
                <div class="article_teaser_body">
                 Osuga Valles is a complex set of channels located near Eos Chasma. This image was captured by NASA's 2001 Mars Odyssey spacecraft.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="Bonestell Crater is a relatively young crater located in Acidalia Planitia. The grooved surface of the ejecta blanket is evident in this image from NASA's 2001 Mars Odyssey spacecraft." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22371_hires.jpg" data-link="/spaceimages/details.php?id=PIA22371" data-thumbnail="/spaceimages/images/wallpaper/PIA22371-640x350.jpg" data-title="Bonestell Crater">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 17, 2018
                </h3>
                <div class="item_tease_overlay">
                 Bonestell Crater
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Bonestell Crater" class="thumb" src="/spaceimages/images/wallpaper/PIA22371-640x350.jpg" title="Bonestell Crater"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 17, 2018
                </div>
                <div class="content_title">
                 Bonestell Crater
                </div>
                <div class="article_teaser_body">
                 Bonestell Crater is a relatively young crater located in Acidalia Planitia. The grooved surface of the ejecta blanket is evident in this image from NASA's 2001 Mars Odyssey spacecraft.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's Mars Reconnaissance Orbiter (MRO) shows chaos terrain on Mars' equator." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22435_hires.jpg" data-link="/spaceimages/details.php?id=PIA22435" data-thumbnail="/spaceimages/images/wallpaper/PIA22435-640x350.jpg" data-title="Chaos Terrain">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 16, 2018
                </h3>
                <div class="item_tease_overlay">
                 Chaos Terrain
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Chaos Terrain" class="thumb" src="/spaceimages/images/wallpaper/PIA22435-640x350.jpg" title="Chaos Terrain"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 16, 2018
                </div>
                <div class="content_title">
                 Chaos Terrain
                </div>
                <div class="article_teaser_body">
                 This image from NASA's Mars Reconnaissance Orbiter (MRO) shows chaos terrain on Mars' equator.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's Mars Reconnaissance Orbiter (MRO) shows bedrock units with diverse colors indicating different mineral concentrations." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22434_hires.jpg" data-link="/spaceimages/details.php?id=PIA22434" data-thumbnail="/spaceimages/images/wallpaper/PIA22434-640x350.jpg" data-title="Diverse Lithologies on a Crater Floor">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 16, 2018
                </h3>
                <div class="item_tease_overlay">
                 Diverse Lithologies on a Crater Floor
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Diverse Lithologies on a Crater Floor" class="thumb" src="/spaceimages/images/wallpaper/PIA22434-640x350.jpg" title="Diverse Lithologies on a Crater Floor"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 16, 2018
                </div>
                <div class="content_title">
                 Diverse Lithologies on a Crater Floor
                </div>
                <div class="article_teaser_body">
                 This image from NASA's Mars Reconnaissance Orbiter (MRO) shows bedrock units with diverse colors indicating different mineral concentrations.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's Mars Reconnaissance Orbiter (MRO) shows a field of boulders." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22433_hires.jpg" data-link="/spaceimages/details.php?id=PIA22433" data-thumbnail="/spaceimages/images/wallpaper/PIA22433-640x350.jpg" data-title="Bouldery Plains">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 16, 2018
                </h3>
                <div class="item_tease_overlay">
                 Bouldery Plains
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Bouldery Plains" class="thumb" src="/spaceimages/images/wallpaper/PIA22433-640x350.jpg" title="Bouldery Plains"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 16, 2018
                </div>
                <div class="content_title">
                 Bouldery Plains
                </div>
                <div class="article_teaser_body">
                 This image from NASA's Mars Reconnaissance Orbiter (MRO) shows a field of boulders.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's Mars Reconnaissance Orbiter shows remarkably young lava flows in Elysium Planitia. There are almost no impact craters over this flow, indicating that it is probably only a few million years old." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22432_hires.jpg" data-link="/spaceimages/details.php?id=PIA22432" data-thumbnail="/spaceimages/images/wallpaper/PIA22432-640x350.jpg" data-title="Young Lava Flows">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 16, 2018
                </h3>
                <div class="item_tease_overlay">
                 Young Lava Flows
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Young Lava Flows" class="thumb" src="/spaceimages/images/wallpaper/PIA22432-640x350.jpg" title="Young Lava Flows"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 16, 2018
                </div>
                <div class="content_title">
                 Young Lava Flows
                </div>
                <div class="article_teaser_body">
                 This image from NASA's Mars Reconnaissance Orbiter shows remarkably young lava flows in Elysium Planitia. There are almost no impact craters over this flow, indicating that it is probably only a few million years old.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft shows several craters. The interior of the central one has retained much of the original topography, including the central peak." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22370_hires.jpg" data-link="/spaceimages/details.php?id=PIA22370" data-thumbnail="/spaceimages/images/wallpaper/PIA22370-640x350.jpg" data-title="Arabia Terra Crater">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 16, 2018
                </h3>
                <div class="item_tease_overlay">
                 Arabia Terra Crater
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Arabia Terra Crater" class="thumb" src="/spaceimages/images/wallpaper/PIA22370-640x350.jpg" title="Arabia Terra Crater"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 16, 2018
                </div>
                <div class="content_title">
                 Arabia Terra Crater
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft shows several craters. The interior of the central one has retained much of the original topography, including the central peak.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft is located in an unnamed crater within Tyrrhena Terra. The 'mitten' shaped feature extends from the crater rim (bottom of frame) onto the crater floor." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22368_hires.jpg" data-link="/spaceimages/details.php?id=PIA22368" data-thumbnail="/spaceimages/images/wallpaper/PIA22368-640x350.jpg" data-title="Landslide">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 13, 2018
                </h3>
                <div class="item_tease_overlay">
                 Landslide
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Landslide" class="thumb" src="/spaceimages/images/wallpaper/PIA22368-640x350.jpg" title="Landslide"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 13, 2018
                </div>
                <div class="content_title">
                 Landslide
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft is located in an unnamed crater within Tyrrhena Terra. The 'mitten' shaped feature extends from the crater rim (bottom of frame) onto the crater floor.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="Olympica Fossae is a complex channel located on the volcanic plains between Alba Mons and Olympus Mons. The sinuosity of the large channel in the middle of this image from NASA's 2001 Mars Odyssey indicates that this is a channel created by liquid flow." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22367_hires.jpg" data-link="/spaceimages/details.php?id=PIA22367" data-thumbnail="/spaceimages/images/wallpaper/PIA22367-640x350.jpg" data-title="Olympica Fossae">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 12, 2018
                </h3>
                <div class="item_tease_overlay">
                 Olympica Fossae
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Olympica Fossae" class="thumb" src="/spaceimages/images/wallpaper/PIA22367-640x350.jpg" title="Olympica Fossae"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 12, 2018
                </div>
                <div class="content_title">
                 Olympica Fossae
                </div>
                <div class="article_teaser_body">
                 Olympica Fossae is a complex channel located on the volcanic plains between Alba Mons and Olympus Mons. The sinuosity of the large channel in the middle of this image from NASA's 2001 Mars Odyssey indicates that this is a channel created by liquid flow.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="Lyot Crater is a large, complex crater in the northern lowlands of Vastitas Borealis. This image from NASA's 2001 Mars Odyssey spacecraft is located along the southern rim of the crater and shows part of the dune fields located on the floor of the crater." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22366_hires.jpg" data-link="/spaceimages/details.php?id=PIA22366" data-thumbnail="/spaceimages/images/wallpaper/PIA22366-640x350.jpg" data-title="Lyot Crater">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 11, 2018
                </h3>
                <div class="item_tease_overlay">
                 Lyot Crater
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Lyot Crater" class="thumb" src="/spaceimages/images/wallpaper/PIA22366-640x350.jpg" title="Lyot Crater"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 11, 2018
                </div>
                <div class="content_title">
                 Lyot Crater
                </div>
                <div class="article_teaser_body">
                 Lyot Crater is a large, complex crater in the northern lowlands of Vastitas Borealis. This image from NASA's 2001 Mars Odyssey spacecraft is located along the southern rim of the crater and shows part of the dune fields located on the floor of the crater.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image captured by NASA's 2001 Mars Odyssey spacecraft is located in Medusae Fossae. Along the cliffside several dark streaks are visible." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22365_hires.jpg" data-link="/spaceimages/details.php?id=PIA22365" data-thumbnail="/spaceimages/images/wallpaper/PIA22365-640x350.jpg" data-title="Wind + Gravity">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 10, 2018
                </h3>
                <div class="item_tease_overlay">
                 Wind + Gravity
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Wind + Gravity" class="thumb" src="/spaceimages/images/wallpaper/PIA22365-640x350.jpg" title="Wind + Gravity"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 10, 2018
                </div>
                <div class="content_title">
                 Wind + Gravity
                </div>
                <div class="article_teaser_body">
                 This image captured by NASA's 2001 Mars Odyssey spacecraft is located in Medusae Fossae. Along the cliffside several dark streaks are visible.
                </div>
               </div>
              </div>
             </a>
            </li>
            <li class="slide">
             <a class="fancybox" data-description="This image from NASA's 2001 Mars Odyssey spacecraft is located along the northern margin of Terra Sirenum. This unnamed channel contains a small channel within a larger channel." data-fancybox-group="images" data-fancybox-href="/spaceimages/images/largesize/PIA22364_hires.jpg" data-link="/spaceimages/details.php?id=PIA22364" data-thumbnail="/spaceimages/images/wallpaper/PIA22364-640x350.jpg" data-title="Inner Channel">
              <div class="image_and_description_container">
               <div class="rollover_description">
                <h3 class="release_date">
                 April 9, 2018
                </h3>
                <div class="item_tease_overlay">
                 Inner Channel
                </div>
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <div class="img">
                <img alt="Inner Channel" class="thumb" src="/spaceimages/images/wallpaper/PIA22364-640x350.jpg" title="Inner Channel"/>
               </div>
               <div class="list_text_content">
                <div class="article_teaser_body">
                 April 9, 2018
                </div>
                <div class="content_title">
                 Inner Channel
                </div>
                <div class="article_teaser_body">
                 This image from NASA's 2001 Mars Odyssey spacecraft is located along the northern margin of Terra Sirenum. This unnamed channel contains a small channel within a larger channel.
                </div>
               </div>
              </div>
             </a>
            </li>
           </ul>
           <footer>
            <div class="more_button">
             <a class="button" href="">
              MORE
             </a>
            </div>
           </footer>
          </div>
         </section>
         <section class="image_teaser module">
          <div class="grid_layout">
           <header>
            <h1 class="module_title">
            </h1>
           </header>
           <ul class="module_gallery gallery_list">
            <li class="slide">
             <div class="image_container">
              <a href="http://photojournal.jpl.nasa.gov/">
               <img alt="jpl photojournal" class="thumb" src="/assets/images/content/tmp/images/jpl_photojournal(3x1).jpg"/>
              </a>
             </div>
             <div class="content_title">
              <a href="http://photojournal.jpl.nasa.gov/">
               JPL Photojournal
              </a>
             </div>
             <div class="article_teaser_body">
              Access to the full library of publicly released images from various Solar System exploration programs
             </div>
            </li>
            <li class="slide">
             <div class="image_container">
              <a href="http://www.nasa.gov/multimedia/imagegallery/">
               <img alt="Great images in NASA" class="thumb" src="/assets/images/content/tmp/images/nasa_images(3x1).jpg"/>
              </a>
             </div>
             <div class="content_title">
              <a href="http://www.nasa.gov/multimedia/imagegallery/">
               Great images in NASA
              </a>
             </div>
             <div class="article_teaser_body">
              A selection of the best-known images from a half-century of exploration and discovery
             </div>
            </li>
           </ul>
          </div>
         </section>
         <section class="multi_teaser module">
          <div class="grid_layout">
           <header>
            <h1 class="module_title">
             You Might Also Like
            </h1>
           </header>
           <ul class="module_gallery gallery_list">
            <li class="slide">
             <a href="//www.jpl.nasa.gov/news/news.php?feature=7114">
              <div class="image_and_description_container">
               <div class="rollover_description">
                NASA's Mars InSight mission launched this morning on a 300-million-mile trip to Mars to study for the first time what lies deep beneath the surface of the Red Planet.
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <img alt="NASA InSight spacecraft launches" src="//imagecache.jpl.nasa.gov/images/640x350/liftoff20180505-16-640x350.jpg"/>
              </div>
              <div class="content_title">
               NASA, ULA Launch Mission to Study How Mars Was Made
              </div>
             </a>
            </li>
            <li class="slide">
             <a href="//www.jpl.nasa.gov/news/news.php?feature=7115">
              <div class="image_and_description_container">
               <div class="rollover_description">
                MarCO is a pair of tiny spacecraft that launched with NASA's InSight lander today.
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <img alt="An artist's rendering of the twin Mars Cube One (MarCO) spacecraft" src="//imagecache.jpl.nasa.gov/images/640x350/PIA22314-16-640x350.jpg"/>
              </div>
              <div class="content_title">
               NASA's First Deep-Space CubeSats Say: 'Polo!'
              </div>
             </a>
            </li>
            <li class="slide">
             <a href="//www.jpl.nasa.gov/news/news.php?feature=7113">
              <div class="image_and_description_container">
               <div class="rollover_description">
                All systems are go for NASA's next launch to the Red Planet.
                <div class="overlay_arrow">
                 <img alt="more arrow" src="/assets/images/overlay-arrow.png"/>
                </div>
               </div>
               <img alt="This artist's concept shows the InSight lander" src="//imagecache.jpl.nasa.gov/images/640x350/PIA22227-16-640x350.jpg"/>
              </div>
              <div class="content_title">
               NASA's First Mission to Study the Interior of Mars Awaits May 5 Launch
              </div>
             </a>
            </li>
           </ul>
           <footer>
            <a class="outline_button dark" href="/news">
             more news
            </a>
           </footer>
          </div>
         </section>
         <!-- END CONTENT -->
         <script src="/Scripts/custom_detail.js" type="text/javascript">
         </script>
         <!-- START FOOTER: "DEFAULT" -->
        </div>
        <footer class="clearfix" id="site_footer">
         <section class="upper_footer">
          <div class="grid_layout">
           <div class="footer_newsletter">
            <h2>
             Get the Newsletter
            </h2>
            <form action="/signup/index.php" class="submit_newsletter" method="post">
             <input class="email_field" name="email_field" onblur="this.placeholder = 'enter email address'" onfocus="this.placeholder = ''" placeholder="enter email address" type="email" value=""/>
             <input class="email_submit" type="submit" value=""/>
            </form>
           </div>
           <div class="gradient_line_divider">
           </div>
           <div class="share">
            <h2>
             Follow JPL
            </h2>
            <div class="social_icons">
             <!-- AddThis Button BEGIN -->
             <div class="addthis_toolbox addthis_default_style addthis_32x32_style">
              <a addthis:userid="NASAJPL" class="addthis_button_facebook_follow icon at300b" href="http://www.facebook.com/NASAJPL" target="_blank" title="Follow on Facebook">
               <span class="at-icon-wrapper" style="background-color: rgb(59, 89, 152); line-height: 32px; height: 32px; width: 32px;">
                <svg alt="Facebook" aria-labelledby="at-svg-facebook-5" class="at-icon at-icon-facebook" role="img" style="width: 32px; height: 32px;" title="Facebook" version="1.1" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                 <title id="at-svg-facebook-5" xmlns="http://www.w3.org/1999/xhtml">
                  Facebook
                 </title>
                 <g>
                  <path d="M22 5.16c-.406-.054-1.806-.16-3.43-.16-3.4 0-5.733 1.825-5.733 5.17v2.882H9v3.913h3.837V27h4.604V16.965h3.823l.587-3.913h-4.41v-2.5c0-1.123.347-1.903 2.198-1.903H22V5.16z" fill-rule="evenodd">
                  </path>
                 </g>
                </svg>
               </span>
               <span class="addthis_follow_label">
                Facebook
               </span>
              </a>
              <a addthis:userid="NASAJPL" class="addthis_button_twitter_follow icon at300b" href="//twitter.com/NASAJPL" target="_blank" title="Follow on Twitter">
               <span class="at-icon-wrapper" style="background-color: rgb(29, 161, 242); line-height: 32px; height: 32px; width: 32px;">
                <svg alt="Twitter" aria-labelledby="at-svg-twitter-6" class="at-icon at-icon-twitter" role="img" style="width: 32px; height: 32px;" title="Twitter" version="1.1" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                 <title id="at-svg-twitter-6" xmlns="http://www.w3.org/1999/xhtml">
                  Twitter
                 </title>
                 <g>
                  <path d="M27.996 10.116c-.81.36-1.68.602-2.592.71a4.526 4.526 0 0 0 1.984-2.496 9.037 9.037 0 0 1-2.866 1.095 4.513 4.513 0 0 0-7.69 4.116 12.81 12.81 0 0 1-9.3-4.715 4.49 4.49 0 0 0-.612 2.27 4.51 4.51 0 0 0 2.008 3.755 4.495 4.495 0 0 1-2.044-.564v.057a4.515 4.515 0 0 0 3.62 4.425 4.52 4.52 0 0 1-2.04.077 4.517 4.517 0 0 0 4.217 3.134 9.055 9.055 0 0 1-5.604 1.93A9.18 9.18 0 0 1 6 23.85a12.773 12.773 0 0 0 6.918 2.027c8.3 0 12.84-6.876 12.84-12.84 0-.195-.005-.39-.014-.583a9.172 9.172 0 0 0 2.252-2.336" fill-rule="evenodd">
                  </path>
                 </g>
                </svg>
               </span>
               <span class="addthis_follow_label">
                Twitter
               </span>
              </a>
              <a addthis:userid="JPLnews" class="addthis_button_youtube_follow icon at300b" href="http://www.youtube.com/user/JPLnews?sub_confirmation=1" target="_blank" title="Follow on YouTube">
               <span class="at-icon-wrapper" style="background-color: rgb(205, 32, 31); line-height: 32px; height: 32px; width: 32px;">
                <svg alt="YouTube" aria-labelledby="at-svg-youtube-7" class="at-icon at-icon-youtube" role="img" style="width: 32px; height: 32px;" title="YouTube" version="1.1" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                 <title id="at-svg-youtube-7" xmlns="http://www.w3.org/1999/xhtml">
                  YouTube
                 </title>
                 <g>
                  <path d="M13.73 18.974V12.57l5.945 3.212-5.944 3.192zm12.18-9.778c-.837-.908-1.775-.912-2.205-.965C20.625 8 16.007 8 16.007 8c-.01 0-4.628 0-7.708.23-.43.054-1.368.058-2.205.966-.66.692-.875 2.263-.875 2.263S5 13.303 5 15.15v1.728c0 1.845.22 3.69.22 3.69s.215 1.57.875 2.262c.837.908 1.936.88 2.426.975 1.76.175 7.482.23 7.482.15 0 .08 4.624.072 7.703-.16.43-.052 1.368-.057 2.205-.965.66-.69.875-2.262.875-2.262s.22-1.845.22-3.69v-1.73c0-1.844-.22-3.69-.22-3.69s-.215-1.57-.875-2.262z" fill-rule="evenodd">
                  </path>
                 </g>
                </svg>
               </span>
               <span class="addthis_follow_label">
                YouTube
               </span>
              </a>
              <a addthis:userid="nasajpl" class="addthis_button_instagram_follow icon at300b" href="http://instagram.com/nasajpl" target="_blank" title="Follow on Instagram">
               <span class="at-icon-wrapper" style="background-color: rgb(224, 53, 102); line-height: 32px; height: 32px; width: 32px;">
                <svg alt="Instagram" aria-labelledby="at-svg-instagram-8" class="at-icon at-icon-instagram" role="img" style="width: 32px; height: 32px;" title="Instagram" version="1.1" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                 <title id="at-svg-instagram-8" xmlns="http://www.w3.org/1999/xhtml">
                  Instagram
                 </title>
                 <g>
                  <path d="M16 5c-2.987 0-3.362.013-4.535.066-1.17.054-1.97.24-2.67.512a5.392 5.392 0 0 0-1.95 1.268 5.392 5.392 0 0 0-1.267 1.95c-.272.698-.458 1.498-.512 2.67C5.013 12.637 5 13.012 5 16s.013 3.362.066 4.535c.054 1.17.24 1.97.512 2.67.28.724.657 1.337 1.268 1.95a5.392 5.392 0 0 0 1.95 1.268c.698.27 1.498.457 2.67.51 1.172.054 1.547.067 4.534.067s3.362-.013 4.535-.066c1.17-.054 1.97-.24 2.67-.51a5.392 5.392 0 0 0 1.95-1.27 5.392 5.392 0 0 0 1.268-1.95c.27-.698.457-1.498.51-2.67.054-1.172.067-1.547.067-4.534s-.013-3.362-.066-4.535c-.054-1.17-.24-1.97-.51-2.67a5.392 5.392 0 0 0-1.27-1.95 5.392 5.392 0 0 0-1.95-1.267c-.698-.272-1.498-.458-2.67-.512C19.363 5.013 18.988 5 16 5zm0 1.982c2.937 0 3.285.01 4.445.064 1.072.05 1.655.228 2.042.38.514.198.88.437 1.265.822.385.385.624.75.823 1.265.15.387.33.97.38 2.042.052 1.16.063 1.508.063 4.445 0 2.937-.01 3.285-.064 4.445-.05 1.072-.228 1.655-.38 2.042-.198.514-.437.88-.822 1.265-.385.385-.75.624-1.265.823-.387.15-.97.33-2.042.38-1.16.052-1.508.063-4.445.063-2.937 0-3.285-.01-4.445-.064-1.072-.05-1.655-.228-2.042-.38-.514-.198-.88-.437-1.265-.822a3.408 3.408 0 0 1-.823-1.265c-.15-.387-.33-.97-.38-2.042-.052-1.16-.063-1.508-.063-4.445 0-2.937.01-3.285.064-4.445.05-1.072.228-1.655.38-2.042.198-.514.437-.88.822-1.265.385-.385.75-.624 1.265-.823.387-.15.97-.33 2.042-.38 1.16-.052 1.508-.063 4.445-.063zm0 12.685a3.667 3.667 0 1 1 0-7.334 3.667 3.667 0 0 1 0 7.334zm0-9.316a5.65 5.65 0 1 0 0 11.3 5.65 5.65 0 0 0 0-11.3zm7.192-.222a1.32 1.32 0 1 1-2.64 0 1.32 1.32 0 0 1 2.64 0" fill-rule="evenodd">
                  </path>
                 </g>
                </svg>
               </span>
               <span class="addthis_follow_label">
                Instagram
               </span>
              </a>
              <a class="icon all_icon" href="/social">
               <span>
                All
               </span>
              </a>
              <div class="atclear">
              </div>
             </div>
             <script>
              addthis_loader.init("//s7.addthis.com/js/300/addthis_widget.js#pubid=ra-5429eeee4e460927", {follow: true})
             </script>
            </div>
           </div>
          </div>
          <div class="gradient_line">
          </div>
         </section>
         <section class="sitemap">
          <div class="grid_layout">
           <div class="sitemap_directory">
            <div class="sitemap_block">
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               about JPL
              </h3>
              <ul class="subnav">
               <li>
                <a href="/about/">
                 About JPL
                </a>
               </li>
               <li>
                <a href="/about/exec.php">
                 Executive Council
                </a>
               </li>
               <li>
                <a href="/about/history.php">
                 History
                </a>
               </li>
               <li>
                <a href="/about/reports.php">
                 Annual Reports
                </a>
               </li>
               <li>
                <a href="/contact_JPL.php">
                 Contact Us
                </a>
               </li>
               <li>
                <a href="/opportunities/">
                 Opportunities
                </a>
               </li>
               <li>
                <a href="/acquisition/">
                 Doing Business with JPL
                </a>
               </li>
              </ul>
             </div>
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               missions
              </h3>
              <ul class="subnav">
               <li>
                <a href="/missions/?type=current">
                 Current
                </a>
               </li>
               <li>
                <a href="/missions/?type=past">
                 Past
                </a>
               </li>
               <li>
                <a href="/missions/?type=future">
                 Future
                </a>
               </li>
               <li>
                <a href="/missions/?type=proposed">
                 Proposed
                </a>
               </li>
               <li>
                <a href="/missions">
                 All
                </a>
               </li>
              </ul>
             </div>
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               galleries
              </h3>
              <ul class="subnav">
               <li>
                <a href="/spaceimages/">
                 JPL Space Images
                </a>
               </li>
               <li>
                <a href="/videos/">
                 Videos
                </a>
               </li>
               <li>
                <a href="/infographics/">
                 Infographics
                </a>
               </li>
               <li>
                <a href="https://photojournal.jpl.nasa.gov/">
                 Photojournal
                </a>
               </li>
               <li>
                <a href="http://www.nasaimages.org/">
                 NASA Images
                </a>
               </li>
               <li>
                <a href="/apps/">
                 Mobile Apps
                </a>
               </li>
              </ul>
             </div>
            </div>
            <div class="sitemap_block">
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               education
              </h3>
              <ul class="subnav">
               <li>
                <a href="/edu/intern/">
                 Intern
                </a>
               </li>
               <li>
                <a href="/edu/learn/">
                 Learn
                </a>
               </li>
               <li>
                <a href="/edu/teach/">
                 Teach
                </a>
               </li>
               <li>
                <a href="/edu/news/">
                 News
                </a>
               </li>
               <li>
                <a href="/edu/events/">
                 Events
                </a>
               </li>
              </ul>
             </div>
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               news
              </h3>
              <ul class="subnav">
               <li>
                <a href="/news">
                 Latest News
                </a>
               </li>
               <li>
                <a href="/news/presskits.php">
                 Press Kits
                </a>
               </li>
               <li>
                <a href="/news/factsheets.php">
                 Fact Sheets
                </a>
               </li>
               <li>
                <a href="/news/mediainformation.php">
                 Media Information
                </a>
               </li>
               <li>
                <a href="/universe/">
                 Universe Newspaper
                </a>
               </li>
              </ul>
             </div>
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               public events
              </h3>
              <ul class="subnav">
               <li>
                <a href="/events/">
                 Overview
                </a>
               </li>
               <li>
                <a href="/events/tours/views/">
                 Tours
                </a>
               </li>
               <li>
                <a href="/events/lectures.php">
                 Lecture Series
                </a>
               </li>
               <li>
                <a href="/events/speakers-bureau.php">
                 Speakers Bureau
                </a>
               </li>
               <li>
                <a href="/events/team-competitions.php">
                 Team Competitions
                </a>
               </li>
               <li>
                <a href="/events/special-events.php">
                 Special Events
                </a>
               </li>
              </ul>
             </div>
            </div>
            <div class="sitemap_block">
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               Our Sites
              </h3>
              <ul class="subnav">
               <li>
                <a href="/asteroidwatch/">
                 Asteroid Watch
                </a>
               </li>
               <li>
                <a href="http://saturn.jpl.nasa.gov/index.cfm">
                 Cassini - Mission to Saturn
                </a>
               </li>
               <li>
                <a href="http://climate.nasa.gov">
                 Earth / Global Climate Change
                </a>
               </li>
               <li>
                <a href="http://planetquest.jpl.nasa.gov">
                 Exoplanet Exploration
                </a>
               </li>
               <li>
                <a href="/missions/juno/">
                 Juno - Mission to Jupiter
                </a>
               </li>
               <li>
                <a href="http://marsprogram.jpl.nasa.gov/">
                 Mars Exploration
                </a>
               </li>
               <li>
                <a href="http://marsprogram.jpl.nasa.gov/msl/">
                 Mars Science Laboratory / Curiosity
                </a>
               </li>
               <li>
                <a href="http://rosetta.jpl.nasa.gov/">
                 Rosetta - Understanding Comets
                </a>
               </li>
               <li>
                <a href="http://scienceandtechnology.jpl.nasa.gov/">
                 Science and Technology
                </a>
               </li>
               <li>
                <a href="http://solarsystem.nasa.gov/">
                 Solar System Exploration
                </a>
               </li>
               <li>
                <a href="http://eyes.nasa.gov/">
                 Eyes on the Solar System
                </a>
               </li>
               <li>
                <a href="http://eyes.nasa.gov/earth/">
                 Eyes on the Earth
                </a>
               </li>
               <li>
                <a href="http://eyes.nasa.gov/exoplanets/">
                 Eyes on Exoplanets
                </a>
               </li>
               <li>
                <a href="http://www.spitzer.caltech.edu/">
                 Spitzer Space Telescope
                </a>
               </li>
              </ul>
             </div>
            </div>
            <div class="sitemap_block">
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               Follow JPL
              </h3>
              <ul class="subnav">
               <li>
                <a href="/signup/">
                 Newsletter
                </a>
               </li>
               <li>
                <a href="https://www.facebook.com/NASAJPL">
                 Facebook
                </a>
               </li>
               <li>
                <a href="http://twitter.com/NASAJPL">
                 Twitter
                </a>
               </li>
               <li>
                <a href="http://www.youtube.com/user/JPLnews">
                 YouTube
                </a>
               </li>
               <li>
                <a href="http://www.flickr.com/photos/nasa-jpl">
                 Flickr
                </a>
               </li>
               <li>
                <a href="http://instagram.com/nasajpl">
                 Instagram
                </a>
               </li>
               <li>
                <a href="https://www.linkedin.com/company/2004/">
                 LinkedIn
                </a>
               </li>
               <li>
                <a href="http://itunes.apple.com/podcast/hd-nasas-jet-propulsion-laboratory/id262254981">
                 iTunes
                </a>
               </li>
               <li>
                <a href="http://www.ustream.tv/nasajpl">
                 UStream
                </a>
               </li>
               <li>
                <a href="/rss/">
                 RSS
                </a>
               </li>
               <li>
                <a href="http://blogs.jpl.nasa.gov">
                 Blog
                </a>
               </li>
               <li>
                <a href="/onthego/">
                 Mobile
                </a>
               </li>
               <li>
                <a href="/social/">
                 All Social Media
                </a>
               </li>
              </ul>
             </div>
             <div class="footer_sitemap_item">
              <h3 class="sitemap_title">
               NASA
              </h3>
              <ul class="subnav">
               <li>
                <a href="http://jplwater.nasa.gov">
                 NASA Water Cleanup
                </a>
               </li>
               <li>
                <a href="http://www.hq.nasa.gov/office/pao/FOIA/agency/">
                 FOIA
                </a>
               </li>
              </ul>
             </div>
            </div>
           </div>
          </div>
          <div class="gradient_line">
          </div>
         </section>
         <section class="lower_footer">
          <div class="nav_container">
           <nav>
            <ul>
             <li>
              <a href="http://www.nasa.gov/" target="_blank">
               NASA
              </a>
             </li>
             |
             <li>
              <a href="http://www.caltech.edu/" target="_blank">
               Caltech
              </a>
             </li>
             |
             <li>
              <a href="/copyrights.php">
               Privacy
              </a>
             </li>
             |
             <li>
              <a href="/imagepolicy">
               Image Policy
              </a>
             </li>
             |
             <li>
              <a href="/faq.php">
               FAQ
              </a>
             </li>
             |
             <li>
              <a href="/contact_JPL.php">
               Feedback
              </a>
             </li>
            </ul>
           </nav>
          </div>
          <div class="credits">
           <span class="credits_manager">
            Site Manager: Jon Nelson
           </span>
           <span class="credits_webmaster">
            Webmasters: Tony Greicius, Luis Espinoza, Anil Natha
           </span>
          </div>
         </section>
        </footer>
       </div>
      </div>
      <script src="/assets/javascripts/vendor/prefixfree.js" type="text/javascript">
      </script>
      <script src="/assets/javascripts/vendor/prefixfree.jquery.js" type="text/javascript">
      </script>
      <script id="_fed_an_ua_tag" src="https://dap.digitalgov.gov/Universal-Federated-Analytics-Min.js?agency=NASA&amp;pua=UA-45212297-1&amp;subagency=JPL&amp;dclink=true&amp;sp=search,s,q&amp;sdor=false&amp;exts=tif,tiff" type="text/javascript">
      </script>
      <script type="text/javascript">
       setTimeout(function(){var a=document.createElement("script");
    var b=document.getElementsByTagName("script")[0];
    a.src=document.location.protocol+"//script.crazyegg.com/pages/scripts/0025/5267.js?"+Math.floor(new Date().getTime()/3600000);
    a.async=true;a.type="text/javascript";b.parentNode.insertBefore(a,b)}, 1);
      </script>
      <!-- END FOOTER: "DEFAULT" -->
      <div id="_atssh" style="visibility: hidden; height: 1px; width: 1px; position: absolute; top: -9999px; z-index: 100000;">
       <iframe id="_atssh199" src="https://s7.addthis.com/static/sh.1836a2a6d9443e6d814c8dfc.html#rand=0.7791144665828342&amp;iit=1526008538244&amp;tmr=load%3D1526008538079%26core%3D1526008538109%26main%3D1526008538232%26ifr%3D1526008538256&amp;cb=0&amp;cdn=0&amp;md=0&amp;kw=&amp;ab=-&amp;dh=www.jpl.nasa.gov&amp;dr=&amp;du=https%3A%2F%2Fwww.jpl.nasa.gov%2Fspaceimages%2F%3Fsearch%3D%26category%3DMars&amp;href=https%3A%2F%2Fwww.jpl.nasa.gov%2Fspaceimages%2F&amp;dt=Space%20Images&amp;dbg=0&amp;cap=tc%3D0%26ab%3D0&amp;inst=1&amp;jsl=1&amp;prod=undefined&amp;lng=en&amp;ogt=&amp;pc=men&amp;pub=&amp;ssl=1&amp;sid=5af50adabcc7c5c0&amp;srf=0.01&amp;ver=300&amp;xck=1&amp;xtr=0&amp;og=&amp;csi=undefined&amp;rev=v8.3.12-wp&amp;ct=1&amp;xld=1&amp;xd=1" style="height: 1px; width: 1px; position: absolute; top: 0px; z-index: 100000; border: 0px; left: 0px;" title="AddThis utility frame">
       </iframe>
      </div>
      <style id="service-icons-0">
      </style>
     </body>
    </html>
    


```python
#Scrape Path for the Feature Image. got the partial path of the url
partial_address = soup2.find_all('a', class_='fancybox')[0].get('data-fancybox-href').strip()
```


```python
#combine the root url to get the full address
featured_image_url = "https://www.jpl.nasa.gov"+partial_address

#Print to check the full URL
print(featured_image_url)

#browse to check url
browser.visit(featured_image_url)
```

    https://www.jpl.nasa.gov/spaceimages/images/mediumsize/PIA19382_ip.jpg
    

#### Mars Weather

Use splinter to scrape the latest Mars weather tweet from the Mars Weather twitter account  (https://twitter.com/marswxreport?lang=en)


```python
# Execute Chromedriver (add in again in case you close the browser)
executable_path = {'executable_path': 'chromedriver.exe'}
browser = Browser('chrome', **executable_path, headless=False)
```


```python
# URL of page to be scraped
url3 = 'https://twitter.com/marswxreport?lang=en'

#Visit the page using the browser
browser.visit(url3)
```


```python
# assign html content
html = browser.html
# Create a Beautiful Soup object
soup3 = bs(html, "html5lib")
# Print formatted version of the soup
print(soup3.prettify())
```

    <!DOCTYPE html>
    <html data-scribe-reduced-action-queue="true" lang="en" xmlns="http://www.w3.org/1999/xhtml">
     <head>
      <meta charset="utf-8"/>
      <script nonce="">
       !function(){window.initErrorstack||(window.initErrorstack=[]),window.onerror=function(r,i,n,o,t){r.indexOf("Script error.")&gt;-1||window.initErrorstack.push({errorMsg:r,url:i,lineNumber:n,column:o,errorObj:t})}}();
      </script>
      <script id="bouncer_terminate_iframe" nonce="">
       if (window.top != window) {
      window.top.postMessage({'bouncer': true, 'event': 'complete'}, '*');
    }
      </script>
      <script id="ttft_boot_data" nonce="">
       window.ttftData={"transaction_id":"00f113cd00185a06.82feac4c5b1d5a0e\u003c:00f600bf00adad58","server_request_start_time":1526008541646,"user_id":null,"is_ssl":true,"rendered_on_server":true,"is_tfe":true,"client":"macaw-swift","tfe_version":"tsa_b\/1.0.1\/20180504.1941.bd0c413","ttft_browser":"chrome"};!function(){function t(t,n){window.ttftData&amp;&amp;!window.ttftData[t]&amp;&amp;(window.ttftData[t]=n)}function n(){return o?Math.round(w.now()+w.timing.navigationStart):(new Date).getTime()}var w=window.performance,o=w&amp;&amp;w.now;window.ttft||(window.ttft={}),window.ttft.recordMilestone||(window.ttft.recordMilestone=t),window.ttft.now||(window.ttft.now=n)}();
      </script>
      <script id="swift_action_queue" nonce="">
       !function(){function e(e){if(e||(e=window.event),!e)return!1;if(e.timestamp=(new Date).getTime(),!e.target&amp;&amp;e.srcElement&amp;&amp;(e.target=e.srcElement),document.documentElement.getAttribute("data-scribe-reduced-action-queue"))for(var t=e.target;t&amp;&amp;t!=document.body;){if("A"==t.tagName)return;t=t.parentNode}return i("all",o(e)),a(e)?(document.addEventListener||(e=o(e)),e.preventDefault=e.stopPropagation=e.stopImmediatePropagation=function(){},y?(v.push(e),i("captured",e)):i("ignored",e),!1):(i("direct",e),!0)}function t(e){n();for(var t,r=0;t=v[r];r++){var a=e(t.target),i=a.closest("a")[0];if("click"==t.type&amp;&amp;i){var o=e.data(i,"events"),u=o&amp;&amp;o.click,c=!i.hostname.match(g)||!i.href.match(/#$/);if(!u&amp;&amp;c){window.location=i.href;continue}}a.trigger(e.event.fix(t))}window.swiftActionQueue.wasFlushed=!0}function r(){for(var e in b)if("all"!=e)for(var t=b[e],r=0;r&lt;t.length;r++)console.log("actionQueue",c(t[r]))}function n(){clearTimeout(w);for(var e,t=0;e=h[t];t++)document["on"+e]=null}function a(e){if(!e.target)return!1;var t=e.target,r=(t.tagName||"").toLowerCase();if(e.metaKey)return!1;if(e.shiftKey&amp;&amp;"a"==r)return!1;if(t.hostname&amp;&amp;!t.hostname.match(g))return!1;if(e.type.match(p)&amp;&amp;s(t))return!1;if("label"==r){var n=t.getAttribute("for");if(n){var a=document.getElementById(n);if(a&amp;&amp;f(a))return!1}else for(var i,o=0;i=t.childNodes[o];o++)if(f(i))return!1}return!0}function i(e,t){t.bucket=e,b[e].push(t)}function o(e){var t={};for(var r in e)t[r]=e[r];return t}function u(e){for(;e&amp;&amp;e!=document.body;){if("A"==e.tagName)return e;e=e.parentNode}}function c(e){var t=[];e.bucket&amp;&amp;t.push("["+e.bucket+"]"),t.push(e.type);var r,n,a=e.target,i=u(a),o="",c=e.timestamp&amp;&amp;e.timestamp-d;return"click"===e.type&amp;&amp;i?(r=i.className.trim().replace(/\s+/g,"."),n=i.id.trim(),o=/[^#]$/.test(i.href)?" ("+i.href+")":"",a='"'+i.innerText.replace(/\n+/g," ").trim()+'"'):(r=a.className.trim().replace(/\s+/g,"."),n=a.id.trim(),a=a.tagName.toLowerCase(),e.keyCode&amp;&amp;(a=String.fromCharCode(e.keyCode)+" : "+a)),t.push(a+o+(n&amp;&amp;"#"+n)+(!n&amp;&amp;r?"."+r:"")),c&amp;&amp;t.push(c),t.join(" ")}function f(e){var t=(e.tagName||"").toLowerCase();return"input"==t&amp;&amp;"checkbox"==e.getAttribute("type")}function s(e){var t=(e.tagName||"").toLowerCase();return"textarea"==t||"input"==t&amp;&amp;"text"==e.getAttribute("type")||"true"==e.getAttribute("contenteditable")}for(var m,d=(new Date).getTime(),l=1e4,g=/^([^\.]+\.)*twitter\.com$/,p=/^key/,h=["click","keydown","keypress","keyup"],v=[],w=null,y=!0,b={captured:[],ignored:[],direct:[],all:[]},k=0;m=h[k];k++)document["on"+m]=e;w=setTimeout(function(){y=!1},l),window.swiftActionQueue={buckets:b,flush:t,logActions:r,wasFlushed:!1}}();
      </script>
      <script id="composition_state" nonce="">
       !function(){function t(t){t.target.setAttribute("data-in-composition","true")}function n(t){t.target.removeAttribute("data-in-composition")}document.addEventListener&amp;&amp;(document.addEventListener("compositionstart",t,!1),document.addEventListener("compositionend",n,!1))}();
      </script>
      <link class="coreCSSBundles" href="https://abs.twimg.com/a/1525911434/css/t1/twitter_core.bundle.css" rel="stylesheet"/>
      <link class="moreCSSBundles" href="https://abs.twimg.com/a/1525911434/css/t1/twitter_more_1.bundle.css" rel="stylesheet"/>
      <link class="moreCSSBundles" href="https://abs.twimg.com/a/1525911434/css/t1/twitter_more_2.bundle.css" rel="stylesheet"/>
      <link href="https://pbs.twimg.com" rel="dns-prefetch"/>
      <link href="https://t.co" rel="dns-prefetch"/>
      <link as="script" href="https://abs.twimg.com/k/en/init.en.0be835e04b9a8e74d6e4.js" rel="preload"/>
      <link as="script" href="https://abs.twimg.com/k/en/0.commons.en.4d8648629a08e456bcce.js" rel="preload"/>
      <link as="script" href="https://abs.twimg.com/k/en/3.pages_profile.en.bec8d66aad5e3a7b2f56.js" rel="preload"/>
      <script id="sentry_init" nonce="">
       window.sentry_version_id = 'SENTRY-BUILD-1525911434';
      window.sentry_api_key = '9d016e799f5b44ba81aa497f929a9df8';
      window.sentry_user_hash = 'a693d70b4b06b658c8c50760e58cab82e16c0f3ca8f9bdcaa0446d77ce03c9f1';
      </script>
      <script defer="" id="sentry_load" nonce="" src="https://abs.twimg.com/static/raven.3.13.1.min.js">
      </script>
      <script defer="" id="sentry_init_2" nonce="" src="https://abs.twimg.com/static/raven_init.4.js">
      </script>
      <title>
       Mars Weather (@MarsWxReport) | Twitter
      </title>
      <meta content="NOODP" name="robots"/>
      <meta content="The latest Tweets from Mars Weather (@MarsWxReport). Updates as avail from the REMS weather instrument aboard @MarsCuriosity.  Data credit: Centro deAstrobiologia, FMI, JPL/NASA, Not an official acct. Gale Crater, Mars" name="description"/>
      <meta content="//abs.twimg.com/favicons/win8-tile-144.png" name="msapplication-TileImage"/>
      <meta content="#00aced" name="msapplication-TileColor"/>
      <link color="#1da1f2" href="https://abs.twimg.com/a/1525911434/icons/favicon.svg" rel="mask-icon" sizes="any"/>
      <link href="//abs.twimg.com/favicons/favicon.ico" rel="shortcut icon" type="image/x-icon"/>
      <link href="https://abs.twimg.com/icons/apple-touch-icon-192x192.png" rel="apple-touch-icon" sizes="192x192"/>
      <link href="/manifest.json" rel="manifest"/>
      <meta content="profile" id="swift-page-name" name="swift-page-name"/>
      <meta content="profile" id="swift-section-name" name="swift-page-section"/>
      <link href="https://twitter.com/marswxreport" rel="canonical"/>
      <link href="https://twitter.com/marswxreport" hreflang="x-default" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=fr" hreflang="fr" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=en" hreflang="en" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=ar" hreflang="ar" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=ja" hreflang="ja" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=es" hreflang="es" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=de" hreflang="de" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=it" hreflang="it" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=id" hreflang="id" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=pt" hreflang="pt" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=ko" hreflang="ko" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=tr" hreflang="tr" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=ru" hreflang="ru" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=nl" hreflang="nl" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=fil" hreflang="fil" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=ms" hreflang="ms" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=zh-tw" hreflang="zh-tw" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=zh-cn" hreflang="zh-cn" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=hi" hreflang="hi" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=no" hreflang="no" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=sv" hreflang="sv" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=fi" hreflang="fi" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=da" hreflang="da" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=pl" hreflang="pl" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=hu" hreflang="hu" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=fa" hreflang="fa" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=he" hreflang="he" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=ur" hreflang="ur" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=th" hreflang="th" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=uk" hreflang="uk" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=ca" hreflang="ca" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=ga" hreflang="ga" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=el" hreflang="el" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=eu" hreflang="eu" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=cs" hreflang="cs" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=gl" hreflang="gl" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=ro" hreflang="ro" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=hr" hreflang="hr" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=en-gb" hreflang="en-gb" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=vi" hreflang="vi" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=bn" hreflang="bn" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=bg" hreflang="bg" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=sr" hreflang="sr" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=sk" hreflang="sk" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=gu" hreflang="gu" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=mr" hreflang="mr" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=ta" hreflang="ta" rel="alternate"/>
      <link href="https://twitter.com/marswxreport?lang=kn" hreflang="kn" rel="alternate"/>
      <link href="https://publish.twitter.com/oembed?url=https://twitter.com/MarsWxReport" rel="alternate" title="Mars Weather (@MarsWxReport) | Twitter" type="application/json+oembed"/>
      <link href="https://mobile.twitter.com/marswxreport?locale=en" media="handheld, only screen and (max-width: 640px)" rel="alternate"/>
      <link href="android-app://com.twitter.android/twitter/user?screen_name=MarsWxReport&amp;ref_src=twsrc%5Egoogle%7Ctwcamp%5Eandroidseo%7Ctwgr%5Eprofile" rel="alternate"/>
      <link href="/opensearch.xml" rel="search" title="Twitter" type="application/opensearchdescription+xml"/>
      <link id="async-css-placeholder"/>
      <meta content="twitter://user?screen_name=MarsWxReport" property="al:ios:url"/>
      <meta content="333903271" property="al:ios:app_store_id"/>
      <meta content="Twitter" property="al:ios:app_name"/>
      <meta content="twitter://user?screen_name=MarsWxReport" property="al:android:url"/>
      <meta content="com.twitter.android" property="al:android:package"/>
      <meta content="Twitter" property="al:android:app_name"/>
      <script async="" charset="utf-8" src="https://abs.twimg.com/k/en/0.commons.en.4d8648629a08e456bcce.js" type="text/javascript">
      </script>
      <script async="" charset="utf-8" src="https://abs.twimg.com/k/en/3.pages_profile.en.bec8d66aad5e3a7b2f56.js" type="text/javascript">
      </script>
     </head>
     <body class="three-col logged-out user-style-MarsWxReport ms-windows enhanced-mini-profile ProfilePage ProfilePage--withWarning swift-loading" data-fouc-class-names="swift-loading" dir="ltr">
      <script id="swift_loading_indicator" nonce="">
       document.body.className=document.body.className+" "+document.body.getAttribute("data-fouc-class-names");
      </script>
      <noscript>
       &lt;form action="https://mobile.twitter.com/i/nojs_router?path=%2Fmarswxreport&amp;amp;lang=en" method="POST" class="NoScriptForm"&gt;
            &lt;input type="hidden" value="b79b982cf6601a1f3e594e3d344bc5c307a442ae" name="authenticity_token"&gt;
    
            &lt;div class="NoScriptForm-content"&gt;
              &lt;span class="NoScriptForm-logo Icon Icon--logo Icon--extraLarge"&gt;&lt;/span&gt;
              &lt;p&gt;We've detected that JavaScript is disabled in your browser. Would you like to proceed to legacy Twitter?&lt;/p&gt;
              &lt;p class="NoScriptForm-buttonContainer"&gt;&lt;button type="submit" class="EdgeButton EdgeButton--primary"&gt;Yes&lt;/button&gt;&lt;/p&gt;
            &lt;/div&gt;
          &lt;/form&gt;
      </noscript>
      <a class="u-hiddenVisually focusable" href="#timeline">
       Skip to content
      </a>
      <div class="route-profile" data-at-shortcutkeys='{"Enter":"Open Tweet details","o":"Expand photo","/":"Search","?":"This menu","j":"Next Tweet","k":"Previous Tweet","Space":"Page down",".":"Load new Tweets","gu":"Go to user\u2026"}' id="doc">
       <div class="topbar js-topbar">
        <div class="js-banners" id="banners">
         <div class="Banner Banner--aboveNav Banner-darkGray gdpr-privacy-banner">
          <div class="Banner-contentContainer">
           <div class="Banner-textContent" id="account-suspended">
            <p class="title">
             Twitter has a new Terms of Service and Privacy Policy, effective May 25, 2018.
             <a class="learn-more" href="https://help.twitter.com/rules-and-policies/update-privacy-policy" rel="noopener" target="_blank">
              Learn more
             </a>
            </p>
           </div>
           <div class="Banner-actions">
            <button class="EdgeButton EdgeButton--transparent" type="button">
             Got it
            </button>
           </div>
          </div>
         </div>
        </div>
        <div class="global-nav global-nav--newLoggedOut" data-section-term="top_nav">
         <div class="global-nav-inner">
          <div class="container">
           <ul class="nav js-global-actions" id="global-actions" role="navigation">
            <li class="home" data-global-action="home" id="global-nav-home">
             <a class="js-nav js-tooltip js-dynamic-tooltip" data-component-context="home_nav" data-nav="home" data-placement="bottom" href="/">
              <span class="Icon Icon--bird Icon--large">
              </span>
              <span aria-hidden="true" class="text">
               Home
              </span>
              <span class="u-hiddenVisually a11y-inactive-page-text">
               Home
              </span>
              <span class="u-hiddenVisually a11y-active-page-text">
               Home, current page.
              </span>
             </a>
            </li>
            <li class="moments" data-global-action="moments" id="global-nav-moments">
             <a class="js-nav js-tooltip js-dynamic-tooltip" data-component-context="moments_nav" data-nav="moments" data-placement="bottom" href="/i/moments">
              <span class="Icon Icon--lightning Icon--large">
              </span>
              <span class="Icon Icon--lightningFilled Icon--large">
              </span>
              <span aria-hidden="true" class="text">
               Moments
              </span>
              <span class="u-hiddenVisually a11y-inactive-page-text">
               Moments
              </span>
              <span class="u-hiddenVisually a11y-active-page-text">
               Moments, current page.
              </span>
             </a>
            </li>
           </ul>
           <div class="pull-right nav-extras">
            <div role="search">
             <form action="/search" class="t1-form form-search js-search-form" id="global-nav-search">
              <label class="visuallyhidden" for="search-query">
               Search query
              </label>
              <input autocomplete="off" class="search-input" id="search-query" name="q" placeholder="Search Twitter" spellcheck="false" type="text"/>
              <span class="search-icon js-search-action">
               <button class="Icon Icon--medium Icon--search nav-search" type="submit">
                <span class="visuallyhidden">
                 Search Twitter
                </span>
               </button>
              </span>
              <div class="dropdown-menu typeahead" role="listbox">
               <div aria-hidden="true" class="dropdown-caret">
                <div class="caret-outer">
                </div>
                <div class="caret-inner">
                </div>
               </div>
               <div class="dropdown-inner js-typeahead-results" role="presentation">
                <div class="typeahead-saved-searches" role="presentation">
                 <h3 class="typeahead-category-title saved-searches-title" id="saved-searches-heading">
                  Saved searches
                 </h3>
                 <ul class="typeahead-items saved-searches-list" role="presentation">
                  <li class="typeahead-item typeahead-saved-search-item" role="presentation">
                   <span aria-hidden="true" class="Icon Icon--close">
                    <span class="visuallyhidden">
                     Remove
                    </span>
                   </span>
                   <a aria-describedby="saved-searches-heading" class="js-nav" data-ds="saved_search" data-query-source="" data-search-query="" href="" role="option" tabindex="-1">
                   </a>
                  </li>
                 </ul>
                </div>
                <ul class="typeahead-items typeahead-topics" role="presentation">
                 <li class="typeahead-item typeahead-topic-item" role="presentation">
                  <a class="js-nav" data-ds="topics" data-query-source="typeahead_click" data-search-query="" href="" role="option" tabindex="-1">
                  </a>
                 </li>
                </ul>
                <ul class="typeahead-items typeahead-accounts social-context js-typeahead-accounts" role="presentation">
                 <li class="typeahead-item typeahead-account-item js-selectable" data-remote="true" data-score="" data-user-id="" data-user-screenname="" role="presentation">
                  <a class="js-nav" data-ds="account" data-query-source="typeahead_click" data-search-query="" role="option">
                   <div class="js-selectable typeahead-in-conversation hidden">
                    <span class="Icon Icon--follower Icon--small">
                    </span>
                    <span class="typeahead-in-conversation-text">
                     In this conversation
                    </span>
                   </div>
                   <img alt="" class="avatar size32"/>
                   <span class="typeahead-user-item-info account-group">
                    <span class="fullname">
                    </span>
                    <span class="UserBadges">
                     <span class="Icon Icon--verified js-verified hidden">
                      <span class="u-hiddenVisually">
                       Verified account
                      </span>
                     </span>
                     <span class="Icon Icon--protected js-protected hidden">
                      <span class="u-hiddenVisually">
                       Protected Tweets
                      </span>
                     </span>
                    </span>
                    <span class="UserNameBreak">
                    </span>
                    <span class="username u-dir" dir="ltr">
                     @
                     <b>
                     </b>
                    </span>
                   </span>
                   <span class="typeahead-social-context">
                   </span>
                  </a>
                 </li>
                 <li class="js-selectable typeahead-accounts-shortcut js-shortcut" role="presentation">
                  <a class="js-nav" data-ds="account_search" data-query-source="typeahead_click" data-search-query="" data-shortcut="true" href="" role="option">
                  </a>
                 </li>
                </ul>
                <ul class="typeahead-items typeahead-trend-locations-list" role="presentation">
                 <li class="typeahead-item typeahead-trend-locations-item" role="presentation">
                  <a class="js-nav" data-ds="trend_location" data-search-query="" href="" role="option" tabindex="-1">
                  </a>
                 </li>
                </ul>
                <div class="typeahead-user-select" role="presentation">
                 <div class="typeahead-empty-suggestions" role="presentation">
                  Suggested users
                 </div>
                 <ul class="typeahead-items typeahead-selected js-typeahead-selected" role="presentation">
                  <li class="typeahead-item typeahead-selected-item js-selectable" data-remote="true" data-score="" data-user-id="" data-user-screenname="" role="presentation">
                   <a class="js-nav" data-ds="account" data-query-source="typeahead_click" data-search-query="" role="option">
                    <img alt="" class="avatar size32"/>
                    <span class="typeahead-user-item-info account-group">
                     <span class="select-status deselect-user js-deselect-user Icon Icon--check">
                     </span>
                     <span class="select-status select-disabled Icon Icon--unfollow">
                     </span>
                     <span class="fullname">
                     </span>
                     <span class="UserBadges">
                      <span class="Icon Icon--verified js-verified hidden">
                       <span class="u-hiddenVisually">
                        Verified account
                       </span>
                      </span>
                      <span class="Icon Icon--protected js-protected hidden">
                       <span class="u-hiddenVisually">
                        Protected Tweets
                       </span>
                      </span>
                     </span>
                     <span class="UserNameBreak">
                     </span>
                     <span class="username u-dir" dir="ltr">
                      @
                      <b>
                      </b>
                     </span>
                    </span>
                   </a>
                  </li>
                  <li class="typeahead-selected-end" role="presentation">
                  </li>
                 </ul>
                 <ul class="typeahead-items typeahead-accounts js-typeahead-accounts" role="presentation">
                  <li class="typeahead-item typeahead-account-item js-selectable" data-remote="true" data-score="" data-user-id="" data-user-screenname="" role="presentation">
                   <a class="js-nav" data-ds="account" data-query-source="typeahead_click" data-search-query="" role="option">
                    <img alt="" class="avatar size32"/>
                    <span class="typeahead-user-item-info account-group">
                     <span class="select-status deselect-user js-deselect-user Icon Icon--check">
                     </span>
                     <span class="select-status select-disabled Icon Icon--unfollow">
                     </span>
                     <span class="fullname">
                     </span>
                     <span class="UserBadges">
                      <span class="Icon Icon--verified js-verified hidden">
                       <span class="u-hiddenVisually">
                        Verified account
                       </span>
                      </span>
                      <span class="Icon Icon--protected js-protected hidden">
                       <span class="u-hiddenVisually">
                        Protected Tweets
                       </span>
                      </span>
                     </span>
                     <span class="UserNameBreak">
                     </span>
                     <span class="username u-dir" dir="ltr">
                      @
                      <b>
                      </b>
                     </span>
                    </span>
                   </a>
                  </li>
                  <li class="typeahead-accounts-end" role="presentation">
                  </li>
                 </ul>
                </div>
                <div class="typeahead-dm-conversations" role="presentation">
                 <ul class="typeahead-items typeahead-dm-conversation-items" role="presentation">
                  <li class="typeahead-item typeahead-dm-conversation-item" role="presentation">
                   <a role="option" tabindex="-1">
                   </a>
                  </li>
                 </ul>
                </div>
               </div>
              </div>
             </form>
            </div>
            <ul class="nav secondary-nav language-dropdown">
             <li class="dropdown js-language-dropdown">
              <a class="dropdown-toggle js-dropdown-toggle" href="#supported_languages">
               <small>
                Language:
               </small>
               <span class="js-current-language">
                English
               </span>
               <b class="caret">
               </b>
              </a>
              <div class="dropdown-menu dropdown-menu--rightAlign is-forceRight">
               <div class="dropdown-caret right">
                <span class="caret-outer">
                </span>
                <span class="caret-inner">
                </span>
               </div>
               <ul id="supported_languages">
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="id" href="?lang=id" rel="noopener" title="Indonesian">
                  Bahasa Indonesia
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="msa" href="?lang=msa" rel="noopener" title="Malay">
                  Bahasa Melayu
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="ca" href="?lang=ca" rel="noopener" title="Catalan">
                  Català
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="cs" href="?lang=cs" rel="noopener" title="Czech">
                  Ceština
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="da" href="?lang=da" rel="noopener" title="Danish">
                  Dansk
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="de" href="?lang=de" rel="noopener" title="German">
                  Deutsch
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="en-gb" href="?lang=en-gb" rel="noopener" title="British English">
                  English UK
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="es" href="?lang=es" rel="noopener" title="Spanish">
                  Español
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="fil" href="?lang=fil" rel="noopener" title="Filipino">
                  Filipino
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="fr" href="?lang=fr" rel="noopener" title="French">
                  Français
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="hr" href="?lang=hr" rel="noopener" title="Croatian">
                  Hrvatski
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="it" href="?lang=it" rel="noopener" title="Italian">
                  Italiano
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="hu" href="?lang=hu" rel="noopener" title="Hungarian">
                  Magyar
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="nl" href="?lang=nl" rel="noopener" title="Dutch">
                  Nederlands
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="no" href="?lang=no" rel="noopener" title="Norwegian">
                  Norsk
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="pl" href="?lang=pl" rel="noopener" title="Polish">
                  Polski
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="pt" href="?lang=pt" rel="noopener" title="Portuguese">
                  Português
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="ro" href="?lang=ro" rel="noopener" title="Romanian">
                  Româna
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="sk" href="?lang=sk" rel="noopener" title="Slovak">
                  Slovencina
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="fi" href="?lang=fi" rel="noopener" title="Finnish">
                  Suomi
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="sv" href="?lang=sv" rel="noopener" title="Swedish">
                  Svenska
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="vi" href="?lang=vi" rel="noopener" title="Vietnamese">
                  Ti?ng Vi?t
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="tr" href="?lang=tr" rel="noopener" title="Turkish">
                  Türkçe
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="el" href="?lang=el" rel="noopener" title="Greek">
                  ????????
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="bg" href="?lang=bg" rel="noopener" title="Bulgarian">
                  ????????? ????
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="ru" href="?lang=ru" rel="noopener" title="Russian">
                  ???????
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="sr" href="?lang=sr" rel="noopener" title="Serbian">
                  ??????
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="uk" href="?lang=uk" rel="noopener" title="Ukrainian">
                  ?????????? ????
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="he" href="?lang=he" rel="noopener" title="Hebrew">
                  ????????
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="ar" href="?lang=ar" rel="noopener" title="Arabic">
                  ???????
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="fa" href="?lang=fa" rel="noopener" title="Persian">
                  ?????
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="mr" href="?lang=mr" rel="noopener" title="Marathi">
                  ?????
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="hi" href="?lang=hi" rel="noopener" title="Hindi">
                  ??????
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="bn" href="?lang=bn" rel="noopener" title="Bangla">
                  ?????
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="gu" href="?lang=gu" rel="noopener" title="Gujarati">
                  ???????
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="ta" href="?lang=ta" rel="noopener" title="Tamil">
                  ?????
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="kn" href="?lang=kn" rel="noopener" title="Kannada">
                  ?????
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="th" href="?lang=th" rel="noopener" title="Thai">
                  ???????
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="ko" href="?lang=ko" rel="noopener" title="Korean">
                  ???
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="ja" href="?lang=ja" rel="noopener" title="Japanese">
                  ???
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="zh-cn" href="?lang=zh-cn" rel="noopener" title="Simplified Chinese">
                  ????
                 </a>
                </li>
                <li>
                 <a class="js-language-link js-tooltip" data-lang-code="zh-tw" href="?lang=zh-tw" rel="noopener" title="Traditional Chinese">
                  ????
                 </a>
                </li>
               </ul>
              </div>
              <div class="js-front-language">
               <form action="/sessions/change_locale" class="t1-form language" method="POST">
                <input name="lang" type="hidden"/>
                <input name="redirect" type="hidden"/>
                <input name="authenticity_token" type="hidden" value="b79b982cf6601a1f3e594e3d344bc5c307a442ae"/>
               </form>
              </div>
             </li>
            </ul>
            <ul class="nav secondary-nav session-dropdown" id="session">
             <li class="dropdown js-session">
              <a class="dropdown-toggle js-dropdown-toggle dropdown-signin" data-nav="login" href="/login" id="signin-link" role="button">
               <small>
                Have an account?
               </small>
               <span class="emphasize">
                Log in
               </span>
               <span class="caret">
               </span>
              </a>
              <div class="dropdown-menu dropdown-form dropdown-menu--rightAlign is-forceRight" id="signin-dropdown">
               <div class="dropdown-caret right">
                <span class="caret-outer">
                </span>
                <span class="caret-inner">
                </span>
               </div>
               <div class="signin-dialog-body">
                <div>
                 Have an account?
                </div>
                <form action="https://twitter.com/sessions" class="LoginForm js-front-signin" data-component="login_callout" data-element="form" method="post">
                 <div class="LoginForm-input LoginForm-username">
                  <input autocomplete="username" class="text-input email-input js-signin-email" name="session[username_or_email]" placeholder="Phone, email, or username" type="text"/>
                 </div>
                 <div class="LoginForm-input LoginForm-password">
                  <input autocomplete="current-password" class="text-input" name="session[password]" placeholder="Password" type="password"/>
                 </div>
                 <div class="LoginForm-rememberForgot">
                  <label>
                   <input checked="checked" name="remember_me" type="checkbox" value="1"/>
                   <span>
                    Remember me
                   </span>
                  </label>
                  <span class="separator">
                   ·
                  </span>
                  <a class="forgot" href="/account/begin_password_reset" rel="noopener">
                   Forgot password?
                  </a>
                 </div>
                 <input class="EdgeButton EdgeButton--primary EdgeButton--medium submit js-submit" type="submit" value="Log in"/>
                 <input name="return_to_ssl" type="hidden" value="true"/>
                 <input name="scribe_log" type="hidden"/>
                 <input name="redirect_after_login" type="hidden" value="/marswxreport?lang=en"/>
                 <input name="authenticity_token" type="hidden" value="b79b982cf6601a1f3e594e3d344bc5c307a442ae"/>
                 <input autocomplete="off" name="ui_metrics" type="hidden" value='{"rf":{"fedd104b6131ef40af0569335a0cb4c69556f94250f21d0b8c980bfb0e4fbe1e":-64,"afdfc66adcbf938e3e701f4ed3d086495dcd2c4a07f0d1dc0f455e3d52996ca4":-160,"acffd5ed4d04fe961027909b6266b62113e43abcc0d7e46a516f40abf3c79091":0,"ab19693a16e92a84ea8b5878af8a69d65ee4d8c92789b936039d592c3602e54d":-15},"s":"T9Eb6JD31YNDxvcsL2jL2nC6XjW2icobCK_S-nlNV-V3GgCidBs44znxaq7Yjgfw-05NSNH75b_MbrJfCn0oXZtyTcLA9pIedG_H2zWueXRFaVgr2vnJpS1hujrRaPtgp10t49MX2RcDqxDsbbVEuGgymRVsj9XioCUvUQFLevq_aoainJd_gA5VcK7Q9fDxoM_qplCtAvERWlLqL5BhooBXO4rTjdD8z70ZuqlyZ0VAE5CO4a706wV_vkAQqZaLOUOw66NJGgmuku47Im0gd6mQxY3ug42n5uAZmy6DLd7BtLsqbmVDfaB4wHYm9gJt2wVpOvgpLOO95KWQMkq0WwAAAWNNMnR2"}'/>
                 <script async="" src="/i/js_inst?c_name=ui_metrics">
                 </script>
                </form>
                <hr/>
                <div class="signup SignupForm">
                 <div class="SignupForm-header">
                  New to Twitter?
                 </div>
                 <a class="EdgeButton EdgeButton--secondary EdgeButton--medium u-block js-signup" data-component="signup_callout" data-element="dropdown" href="https://twitter.com/signup" role="button">
                  Sign up
                 </a>
                </div>
               </div>
              </div>
             </li>
            </ul>
           </div>
          </div>
         </div>
        </div>
       </div>
       <div class="topbar-spacer" style="padding-top: 108px;">
       </div>
       <div id="page-outer">
        <div class="AppContent" id="page-container">
         <style id="user-style-MarsWxReport">
          a,
      a:hover,
      a:focus,
      a:active {
        color: #0084B4;
      }
    
      .u-textUserColor,
      .u-textUserColorHover:hover,
      .u-textUserColorHover:hover .ProfileTweet-actionCount,
      .u-textUserColorHover:focus {
        color: #0084B4 !important;
      }
    
      .u-borderUserColor,
      .u-borderUserColorHover:hover,
      .u-borderUserColorHover:focus {
        border-color: #0084B4 !important;
      }
    
      .u-bgUserColor,
      .u-bgUserColorHover:hover,
      .u-bgUserColorHover:focus {
        background-color: #0084B4 !important;
      }
    
      .u-dropdownUserColor &gt; li:hover,
      .u-dropdownUserColor &gt; li:focus,
      .u-dropdownUserColor &gt; li &gt; button:hover,
      .u-dropdownUserColor &gt; li &gt; button:focus,
      .u-dropdownUserColor &gt; li &gt; a:focus,
      .u-dropdownUserColor &gt; li &gt; a:hover {
        color: #fff !important;
        background-color: #0084B4 !important;
      }
    
      .u-boxShadowInsetUserColorHover:hover,
      .u-boxShadowInsetUserColorHover:focus {
        box-shadow: inset 0 0 0 5px #0084B4 !important;
      }
    
      .u-dropdownOpenUserColor.dropdown.open .dropdown-toggle {
        color: #0084B4;
      }
    
    
      .u-textUserColorLight {
        color: #99CDE1 !important;
      }
    
      .u-borderUserColorLight,
      .u-borderUserColorLightFocus:focus,
      .u-borderUserColorLightHover:hover,
      .u-borderUserColorLightHover:focus {
        border-color: #99CDE1 !important;
      }
    
      .u-bgUserColorLight {
        background-color: #99CDE1 !important;
      }
    
    
      .u-boxShadowUserColorLighterFocus:focus {
        box-shadow: 0 0 8px rgba(0, 0, 0, 0.05), inset 0 1px 2px rgba(0,132,180,0.25) !important;
      }
    
    
      .u-textUserColorLightest {
        color: #E5F2F7 !important;
      }
    
      .u-borderUserColorLightest {
        border-color: #E5F2F7 !important;
      }
    
      .u-bgUserColorLightest {
        background-color: #E5F2F7 !important;
      }
    
    
      .u-textUserColorLighter {
        color: #BFE0EC !important;
      }
    
      .u-borderUserColorLighter {
        border-color: #BFE0EC !important;
      }
    
      .u-bgUserColorLighter {
        background-color: #BFE0EC !important;
      }
    
    
      .u-bgUserColorDarkHover:hover {
        background-color: #05719A !important;
      }
    
      .u-borderUserColorDark {
        border-color: #05719A !important;
      }
    
    
      .u-bgUserColorDarkerActive:active {
        background-color: #0A5F81 !important;
      }
    
    
    
    
    
    
    
    
    
    
    
    
    
    a,
    .btn-link,
    .btn-link:focus,
    .icon-btn,
    
    
    
    .pretty-link b,
    .pretty-link:hover s,
    .pretty-link:hover b,
    .pretty-link:focus s,
    .pretty-link:focus b,
    
    .metadata a:hover,
    .metadata a:focus,
    
    a.account-group:hover .fullname,
    a.account-group:focus .fullname,
    .account-summary:focus .fullname,
    
    .message .message-text a,
    .message .message-text button,
    .stats a strong,
    .plain-btn:hover,
    .plain-btn:focus,
    .dropdown.open .user-dropdown.plain-btn,
    .open &gt; .plain-btn,
    #global-actions .new:before,
    .module .list-link:hover,
    .module .list-link:focus,
    
    .stats a:hover,
    .stats a:hover strong,
    .stats a:focus,
    .stats a:focus strong,
    
    .find-friends-sources li:hover .source,
    
    
    
    
    
    .stream-item a:hover .fullname,
    .stream-item a:focus .fullname,
    
    .stream-item .view-all-supplements:hover,
    .stream-item .view-all-supplements:focus,
    
    .tweet .time a:hover,
    .tweet .time a:focus,
    .tweet .details.with-icn b,
    .tweet .details.with-icn .Icon,
    
    .stream-item:hover .original-tweet .details b,
    .stream-item .original-tweet.focus .details b,
    .stream-item.open .original-tweet .details b,
    
    .client-and-actions a:hover,
    .client-and-actions a:focus,
    
    .dismiss-btn:hover b,
    
    .tweet .context .pretty-link:hover s,
    .tweet .context .pretty-link:hover b,
    .tweet .context .pretty-link:focus s,
    .tweet .context .pretty-link:focus b,
    
    .list .username a:hover,
    .list .username a:focus,
    .list-membership-container .create-a-list,
    .list-membership-container .create-a-list:hover,
    .new-tweets-bar,
    
    
    
    .card .list-details a:hover,
    .card .list-details a:focus,
    .card .card-body:hover .attribution,
    .card .card-body .attribution:focus {
      color: #0084B4;
    }
    
    
    
    
      
      .FoundMediaSearch--keyboard .FoundMediaSearch-focusable.is-focused {
        border-color: #0084B4;
      }
    
      
      .photo-selector:hover .btn,
      .icon-btn:hover,
      .icon-btn:active,
      .icon-btn.active,
      .icon-btn.enabled {
        border-color: #0084B4;
        border-color: rgba(0,132,180,0.4);
        color: #0084B4;
      }
    
      
      .photo-selector:hover .btn,
      .icon-btn:hover {
        background-image: linear-gradient(rgba(255,255,255,0), rgba(0,132,180,0.1));
      }
    
      .icon-btn.disabled,
      .icon-btn.disabled:hover,
      .icon-btn[disabled],
      .icon-btn[aria-disabled=true] {
        color: #0084B4;
      }
    
      
      
    
      .EdgeButton--primary,
      .EdgeButton--primary:focus {
        background-color: #329CC3;
        border-color: transparent;
      }
    
      .EdgeButton--primary:hover,
      .EdgeButton--primary:active {
        background-color: #0084B4;
        border-color: #0084B4;
      }
    
      .EdgeButton--primary:focus {
        box-shadow:
          0 0 0 2px #FFFFFF,
          0 0 0 4px #99CDE1;
      }
    
      .EdgeButton--primary:active {
        box-shadow:
          0 0 0 2px #FFFFFF,
          0 0 0 4px #329CC3;
      }
    
      
      
    
      .EdgeButton--secondary,
      .EdgeButton--secondary:hover,
      .EdgeButton--secondary:focus,
      .EdgeButton--secondary:active {
        border-color: #0084B4;
        color: #0084B4;
      }
    
      .EdgeButton--secondary:hover,
      .EdgeButton--secondary:active {
        background-color: #E5F2F7;
      }
    
      .EdgeButton--secondary:focus {
        box-shadow:
          0 0 0 2px #FFFFFF,
          0 0 0 4px rgba(0,132,180,0.4);
      }
    
      .EdgeButton--secondary:active {
        box-shadow:
          0 0 0 2px #FFFFFF,
          0 0 0 4px #0084B4;
      }
    
      
      
    
      .EdgeButton--invertedPrimary {
        color: #0084B4 !important;
      }
    
      .EdgeButton--invertedPrimary:focus {
        box-shadow:
          0 0 0 2px #0084B4,
          0 0 0 4px #99CDE1;
      }
    
      .EdgeButton--invertedPrimary:active {
        box-shadow:
          0 0 0 2px #0084B4,
          0 0 0 4px #FFFFFF;
      }
    
      
      
    
      .EdgeButton--invertedSecondary {
        background-color: #0084B4;
      }
    
      .EdgeButton--invertedSecondary:hover {
        background-color: #329CC3;
      }
    
      .EdgeButton--invertedSecondary:focus {
        box-shadow:
          0 0 0 2px #0084B4,
          0 0 0 4px #99CDE1;
      }
    
      .EdgeButton--invertedSecondary:active {
        box-shadow:
          0 0 0 2px #0084B4,
          0 0 0 4px #FFFFFF;
      }
    
      
    
      .btn:focus,
      .btn.focus,
      .Button:focus,
      .EmojiPicker-item.is-focused,
      .EmojiPicker .EmojiCategoryIcon:focus,
      .EmojiPicker-skinTone:focus + .EmojiPicker-skinToneSwatch,
      a:focus &gt; img:first-child:last-child,
      button:focus {
        box-shadow:
          0 0 0 2px #FFFFFF,
          0 0 2px 4px rgba(0,132,180,0.4);
      }
    
      .selected-stream-item:focus {
        box-shadow: 0 0 0 3px rgba(0,132,180,0.4);
      }
    
      
      .js-navigable-stream.stream-table-view .selected-stream-item[tabindex="-1"]:focus {
        outline: 3px solid rgba(0,132,180,0.4) !important;
      }
    
      
      .js-navigable-stream.stream-table-view .selected-stream-item:focus {
        box-shadow: none;
      }
    
      
    
      .global-dm-nav.new.with-count .dm-new .count-inner {
        background: #0084B4;
      }
    
      .global-nav .people .count .count-inner {
        background: #0084B4;
      }
    
      .dropdown-menu li &gt; a:hover,
      .dropdown-menu li &gt; a:focus,
      .dropdown-menu .dropdown-link:hover,
      .dropdown-menu .dropdown-link:focus,
      .dropdown-menu .dropdown-link.is-focused,
      .dropdown-menu li:hover .dropdown-link,
      .dropdown-menu li:focus .dropdown-link,
      .dropdown-menu .selected a,
      .dropdown-menu .dropdown-link.selected {
        background-color: #0084B4 !important;
      }
    
      /* for items in typeahead dropdown menu on logged in pages */
      .dropdown-menu .typeahead-items li &gt; a:focus,
      .dropdown-menu .typeahead-items li &gt; a:hover,
      .dropdown-menu .typeahead-items .selected,
      .dropdown-menu .typeahead-items .selected a {
        background-color: #E5F2F7 !important;
        color: #0084B4 !important;
      }
    
      .typeahead a:hover,
      .typeahead a:hover strong,
      .typeahead a:hover .fullname,
      .typeahead .selected a,
      .typeahead .selected strong,
      .typeahead .selected .fullname,
      .typeahead .selected .Icon--close {
        color: #0084B4 !important;
      }
    
    
    .home-tweet-box,
    .LiveVideo-tweetBox,
    .RetweetDialog-commentBox {
      background-color: #E5F2F7;
    }
    
    .top-timeline-tweetbox .timeline-tweet-box .tweet-form.condensed .tweet-box {
      color: #0084B4;
    }
    
    .RichEditor,
    .TweetBoxAttachments {
      border-color: #BFE0EC;
    }
    
    input:focus,
    textarea:focus,
    div[contenteditable="true"]:focus,
    div[contenteditable="true"].fake-focus,
    div[contenteditable="plaintext-only"]:focus,
    div[contenteditable="plaintext-only"].fake-focus {
      border-color: #99CDE1;
      box-shadow: inset 0 0 0 1px rgba(0,132,180,0.7);
    }
    
    .tweet-box textarea:focus,
    .tweet-box input[type=text],
    .currently-dragging .tweet-form.is-droppable .tweet-drag-help,
    .tweet-box[contenteditable="true"]:focus,
    .RichEditor.is-fakeFocus,
    .RichEditor.is-fakeFocus ~ .TweetBoxAttachments {
      border-color: #99CDE1;
      box-shadow: 0 0 0 1px #99CDE1;
    }
    
    .MomentCapsuleItem.selected-stream-item:focus {
      box-shadow: 0 0 0 3px rgba(0,132,180,0.4);
    }
    
    
    
    
    s,
    .pretty-link:hover s,
    .pretty-link:focus s,
    .stream-item-activity-notification .latest-tweet .tweet-row a:hover s,
    .stream-item-activity-notification .latest-tweet .tweet-row a:focus s {
        color: #0084B4;
    }
    
    
    
    .vellip,
    .vellip:before,
    .vellip:after,
    .conversation-module &gt; li:after,
    .conversation-module &gt; li:before,
    .ThreadedConversation--loneTweet:after,
    .ThreadedConversation-tweet:not(.is-hiddenAncestor) ~ .ThreadedConversation-tweet:before,
    .ThreadedConversation-tweet:after,
    .ThreadedConversation-moreReplies:before,
    .ThreadedConversation-viewOther:before,
    .ThreadedConversation-unavailableTweet:before,
    .ThreadedConversation-unavailableTweet:after,
    .ThreadedConversation--permalinkTweetWithAncestors:before,
    .mini-avatar-with-thread:before,
    .permalink.self-thread-permalink-with-descendant .permalink-tweet-container:after,
    .permalink.self-thread-permalink-with-descendant .inline-reply-tweetbox-container:after {
        border-color: #99CDE1;
    }
    
    
    
    
    .tweet .sm-reply,
    .tweet .sm-rt,
    .tweet .sm-fav,
    .tweet .sm-image,
    .tweet .sm-video,
    .tweet .sm-audio,
    .tweet .sm-geo,
    .tweet .sm-in,
    .tweet .sm-trash,
    .tweet .sm-more,
    .tweet .sm-page,
    .tweet .sm-embed,
    .tweet .sm-summary,
    .tweet .sm-chat,
    
    .timelines-navigation .active .profile-nav-icon,
    .timelines-navigation .profile-nav-icon:hover,
    .timelines-navigation .profile-nav-link:focus .profile-nav-icon,
    
    .sm-top-tweet {
        background-color: #0084B4;
    }
    
    .enhanced-mini-profile .mini-profile .profile-summary {
      background-image: url(https://pbs.twimg.com/profile_banners/786939553/1403835009/mobile);
    }
    
      #global-tweet-dialog .modal-header,
      #Tweetstorm-dialog .modal-header {
        border-bottom: solid 1px rgba(0,132,180,0.25);
      }
    
      #global-tweet-dialog .modal-tweet-form-container,
      #Tweetstorm-dialog .modal-body {
        background-color: #0084B4;
        background: rgba(0,132,180,0.1);
      }
    
      .TweetstormDialog-reply-context .tweet-box-avatar:after,
      .TweetstormDialog-reply-context .tweet-box-avatar:before,
      .TweetstormDialog-tweet-box .tweet-box-avatar:after,
      .TweetstormDialog-tweet-box .tweet-box-avatar:before {
        border-color: #99CDE1;
      }
    
      .global-nav .search-input:focus,
      .global-nav .search-input.focus {
        border: 2px solid #0084B4;
      }
    }
    
      .inline-reply-tweetbox {
        background-color: #E5F2F7;
      }
         </style>
         <div class="ProfileCanopy ProfileCanopy--withNav ProfileCanopy--large js-variableHeightTopBar">
          <div class="ProfileCanopy-inner">
           <div class="ProfileCanopy-header u-bgUserColor">
            <div class="ProfileCanopy-headerBg">
             <img alt="" src="https://pbs.twimg.com/profile_banners/786939553/1403835009/1500x500"/>
            </div>
            <div class="AppContainer">
             <div class="ProfileCanopy-avatar">
              <div class="ProfileAvatar">
               <a class="ProfileAvatar-container u-block js-tooltip profile-picture" data-resolved-url-large="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_400x400.jpg" data-url="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_400x400.jpg" href="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_400x400.jpg" rel="noopener" target="_blank" title="Mars Weather">
                <img alt="Mars Weather" class="ProfileAvatar-image " src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_400x400.jpg"/>
               </a>
              </div>
             </div>
             <div class="ProfileCanopy-headerPromptAnchor">
             </div>
            </div>
           </div>
           <div class="ProfileCanopy-navBar u-boxShadow">
            <div class="AppContainer">
             <div class="Grid Grid--withGutter">
              <div class="Grid-cell u-size1of3 u-lg-size1of4">
               <div class="ProfileCanopy-card" role="presentation">
                <div class="ProfileCardMini">
                 <a class="ProfileCardMini-avatar profile-picture js-tooltip" data-resolved-url-large="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere.jpg" data-url="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere.jpg" href="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere.jpg" rel="noopener" target="_blank" title="Mars Weather">
                  <img alt="Mars Weather" class="ProfileCardMini-avatarImage" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_normal.jpg"/>
                 </a>
                 <div class="ProfileCardMini-details">
                  <div class="ProfileNameTruncated account-group">
                   <div class="u-textTruncate u-inlineBlock">
                    <a class="fullname ProfileNameTruncated-link u-textInheritColor js-nav" data-aria-label-part="" href="/MarsWxReport">
                     Mars Weather
                    </a>
                   </div>
                   <span class="UserBadges">
                   </span>
                  </div>
                  <div class="ProfileCardMini-screenname">
                   <a class="ProfileCardMini-screennameLink u-linkComplex js-nav u-dir" dir="ltr" href="/MarsWxReport">
                    <span class="username u-dir" dir="ltr">
                     @
                     <b class="u-linkComplex-target">
                      MarsWxReport
                     </b>
                    </span>
                   </a>
                  </div>
                 </div>
                </div>
               </div>
              </div>
              <div class="Grid-cell u-size2of3 u-lg-size3of4">
               <div class="ProfileCanopy-nav">
                <div class="ProfileNav" data-user-id="786939553" role="navigation">
                 <ul class="ProfileNav-list">
                  <li class="ProfileNav-item ProfileNav-item--tweets is-active">
                   <a class="ProfileNav-stat ProfileNav-stat--link u-borderUserColor u-textCenter js-tooltip js-nav" data-nav="tweets" tabindex="0" title="1,439 Tweets">
                    <span aria-hidden="true" class="ProfileNav-label">
                     Tweets
                    </span>
                    <span class="u-hiddenVisually">
                     Tweets, current page.
                    </span>
                    <span class="ProfileNav-value" data-count="1439" data-is-compact="false">
                     1,439
                    </span>
                   </a>
                  </li>
                  <li class="ProfileNav-item ProfileNav-item--following">
                   <a class="ProfileNav-stat ProfileNav-stat--link u-borderUserColor u-textCenter js-tooltip js-openSignupDialog js-nonNavigable u-textUserColor" data-nav="following" href="/MarsWxReport/following" title="54 Following">
                    <span aria-hidden="true" class="ProfileNav-label">
                     Following
                    </span>
                    <span class="u-hiddenVisually">
                     Following
                    </span>
                    <span class="ProfileNav-value" data-count="54" data-is-compact="false">
                     54
                    </span>
                   </a>
                  </li>
                  <li class="ProfileNav-item ProfileNav-item--followers">
                   <a class="ProfileNav-stat ProfileNav-stat--link u-borderUserColor u-textCenter js-tooltip js-openSignupDialog js-nonNavigable u-textUserColor" data-nav="followers" href="/MarsWxReport/followers" title="39,932 Followers">
                    <span aria-hidden="true" class="ProfileNav-label">
                     Followers
                    </span>
                    <span class="u-hiddenVisually">
                     Followers
                    </span>
                    <span class="ProfileNav-value" data-count="39932" data-is-compact="true">
                     39.9K
                    </span>
                   </a>
                  </li>
                  <li class="ProfileNav-item ProfileNav-item--favorites" data-more-item=".ProfileNav-dropdownItem--favorites">
                   <a class="ProfileNav-stat ProfileNav-stat--link u-borderUserColor u-textCenter js-tooltip js-openSignupDialog js-nonNavigable u-textUserColor" data-nav="favorites" href="/MarsWxReport/likes" title="190 Likes">
                    <span aria-hidden="true" class="ProfileNav-label">
                     Likes
                    </span>
                    <span class="u-hiddenVisually">
                     Likes
                    </span>
                    <span class="ProfileNav-value" data-count="190" data-is-compact="false">
                     190
                    </span>
                   </a>
                  </li>
                  <li class="ProfileNav-item ProfileNav-item--lists" data-more-item=".ProfileNav-dropdownItem--lists">
                   <a class="ProfileNav-stat ProfileNav-stat--link u-borderUserColor u-textCenter js-tooltip js-openSignupDialog js-nonNavigable u-textUserColor" data-nav="all_lists" href="/MarsWxReport/lists" title="9 Lists">
                    <span aria-hidden="true" class="ProfileNav-label">
                     Lists
                    </span>
                    <span class="u-hiddenVisually">
                     Lists
                    </span>
                    <span class="ProfileNav-value" data-is-compact="false">
                     9
                    </span>
                   </a>
                  </li>
                  <li class="ProfileNav-item ProfileNav-item--more dropdown is-hidden">
                   <a class="ProfileNav-stat ProfileNav-stat--link ProfileNav-stat--moreLink js-openSignupDialog js-nonNavigable" href="#more" role="button">
                    <span class="ProfileNav-label">
                    </span>
                    <span class="ProfileNav-value">
                     More
                     <span class="ProfileNav-dropdownCaret Icon Icon--medium Icon--caretDown">
                     </span>
                    </span>
                   </a>
                   <div class="dropdown-menu">
                    <div class="dropdown-caret">
                     <span class="caret-outer">
                     </span>
                     <span class="caret-inner">
                     </span>
                    </div>
                    <ul>
                     <li>
                      <a class="ProfileNav-dropdownItem ProfileNav-dropdownItem--favorites is-hidden u-bgUserColorHover u-bgUserColorFocus u-linkClean js-nav" href="/MarsWxReport/likes">
                       Likes
                      </a>
                     </li>
                     <li>
                      <a class="ProfileNav-dropdownItem ProfileNav-dropdownItem--lists is-hidden u-bgUserColorHover u-bgUserColorFocus u-linkClean js-nav" href="/MarsWxReport/lists">
                       Lists
                      </a>
                     </li>
                    </ul>
                   </div>
                  </li>
                  <li class="ProfileNav-item ProfileNav-item--userActions u-floatRight u-textRight with-rightCaret ">
                   <div class="UserActions u-textLeft">
                    <div class="user-actions btn-group not-following " data-name="Mars Weather" data-protected="false" data-screen-name="MarsWxReport" data-user-id="786939553">
                     <span class="UserActions-moreActions u-inlineBlock">
                      <button class="js-tooltip unmute-button btn small plain-btn" data-placement="top" title="Unmute @MarsWxReport" type="button">
                       <span class="Icon Icon--muted Icon--medium">
                        <span class="visuallyhidden">
                         Unmute
                         <span class="username u-dir u-textTruncate" dir="ltr">
                          @
                          <b>
                           MarsWxReport
                          </b>
                         </span>
                        </span>
                       </span>
                      </button>
                      <button class="first-load js-tooltip mute-button btn small plain-btn" data-placement="top" title="Mute @MarsWxReport" type="button">
                       <span class="Icon Icon--unmuted Icon--medium">
                        <span class="visuallyhidden">
                         Mute
                         <span class="username u-dir u-textTruncate" dir="ltr">
                          @
                          <b>
                           MarsWxReport
                          </b>
                         </span>
                        </span>
                       </span>
                      </button>
                     </span>
                     <span class="user-actions-follow-button js-follow-btn follow-button">
                      <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text follow-text" type="button">
                       <span aria-hidden="true">
                        Follow
                       </span>
                       <span class="u-hiddenVisually">
                        Follow
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </span>
                      </button>
                      <button class=" EdgeButton EdgeButton--primary EdgeButton--medium button-text following-text" type="button">
                       <span aria-hidden="true">
                        Following
                       </span>
                       <span class="u-hiddenVisually">
                        Following
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </span>
                      </button>
                      <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unfollow-text" type="button">
                       <span aria-hidden="true">
                        Unfollow
                       </span>
                       <span class="u-hiddenVisually">
                        Unfollow
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </span>
                      </button>
                      <button class=" EdgeButton EdgeButton--invertedDanger EdgeButton--medium button-text blocked-text" type="button">
                       <span aria-hidden="true">
                        Blocked
                       </span>
                       <span class="u-hiddenVisually">
                        Blocked
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </span>
                      </button>
                      <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unblock-text" type="button">
                       <span aria-hidden="true">
                        Unblock
                       </span>
                       <span class="u-hiddenVisually">
                        Unblock
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </span>
                      </button>
                      <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text pending-text" type="button">
                       <span aria-hidden="true">
                        Pending
                       </span>
                       <span class="u-hiddenVisually">
                        Pending follow request from
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </span>
                      </button>
                      <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text cancel-text" type="button">
                       <span aria-hidden="true">
                        Cancel
                       </span>
                       <span class="u-hiddenVisually">
                        Cancel your follow request to
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </span>
                      </button>
                     </span>
                    </div>
                   </div>
                  </li>
                 </ul>
                </div>
               </div>
              </div>
             </div>
            </div>
           </div>
          </div>
         </div>
         <div class="AppContainer">
          <div aria-labelledby="content-main-heading" class="AppContent-main content-main u-cf" role="main">
           <div class="Grid Grid--withGutter">
            <div class="Grid-cell u-size1of3 u-lg-size1of4">
             <div class="Grid Grid--withGutter">
              <div class="Grid-cell">
               <div class="ProfileSidebar ProfileSidebar--withLeftAlignment">
                <div class="ProfileHeaderCard">
                 <h1 class="ProfileHeaderCard-name">
                  <a class="ProfileHeaderCard-nameLink u-textInheritColor js-nav" href="/MarsWxReport">
                   Mars Weather
                  </a>
                 </h1>
                 <h2 class="ProfileHeaderCard-screenname u-inlineBlock u-dir" dir="ltr">
                  <a class="ProfileHeaderCard-screennameLink u-linkComplex js-nav" href="/MarsWxReport">
                   <span class="username u-dir" dir="ltr">
                    @
                    <b class="u-linkComplex-target">
                     MarsWxReport
                    </b>
                   </span>
                  </a>
                 </h2>
                 <p class="ProfileHeaderCard-bio u-dir" dir="ltr">
                  Updates as avail from the REMS weather instrument aboard
                  <a class="tweet-url twitter-atreply pretty-link" data-mentioned-user-id="0" dir="ltr" href="/MarsCuriosity" rel="nofollow">
                   <s>
                    @
                   </s>
                   <b>
                    MarsCuriosity
                   </b>
                  </a>
                  .  Data credit: Centro deAstrobiologia, FMI, JPL/NASA, Not an official acct.
                 </p>
                 <div class="ProfileHeaderCard-location ">
                  <span aria-hidden="true" class="Icon Icon--geo Icon--medium" role="presentation">
                  </span>
                  <span class="ProfileHeaderCard-locationText u-dir" dir="ltr">
                   Gale Crater, Mars
                  </span>
                 </div>
                 <div class="ProfileHeaderCard-url ">
                  <span aria-hidden="true" class="Icon Icon--url Icon--medium" role="presentation">
                  </span>
                  <span class="ProfileHeaderCard-urlText u-dir">
                   <a class="u-textUserColor" href="http://t.co/OcX0oySes3" rel="me nofollow noopener" target="_blank" title="http://mars.nasa.gov/msl/mission/instruments/environsensors/rems/">
                    mars.nasa.gov/msl/mission/in…
                   </a>
                  </span>
                 </div>
                 <div class="ProfileHeaderCard-joinDate">
                  <span aria-hidden="true" class="Icon Icon--calendar Icon--medium" role="presentation">
                  </span>
                  <span class="ProfileHeaderCard-joinDateText js-tooltip u-dir" dir="ltr" title="5:48 AM - 28 Aug 2012">
                   Joined August 2012
                  </span>
                 </div>
                 <div class="ProfileHeaderCard-birthdate u-hidden">
                  <span aria-hidden="true" class="Icon Icon--balloon Icon--medium" role="presentation">
                  </span>
                  <span class="ProfileHeaderCard-birthdateText u-dir" dir="ltr">
                  </span>
                 </div>
                </div>
                <div class="PhotoRail">
                 <div class="PhotoRail-heading">
                  <span aria-hidden="true" class="Icon Icon--camera Icon--medium" role="presentation">
                  </span>
                  <span class="PhotoRail-headingText">
                   <a class="PhotoRail-headingWithCount js-nav" href="/MarsWxReport/media">
                    181 Photos and videos
                   </a>
                   <a class="PhotoRail-headingWithoutCount js-nav" href="/MarsWxReport/media">
                    Photos and videos
                   </a>
                  </span>
                 </div>
                 <div class="PhotoRail-mediaBox">
                  <span class="js-photoRailInsertPoint">
                  </span>
                 </div>
                </div>
               </div>
              </div>
             </div>
            </div>
            <div class="Grid-cell u-size2of3 u-lg-size3of4">
             <div class="Grid Grid--withGutter">
              <div class="Grid-cell">
               <div class="js-profileClusterFollow">
               </div>
              </div>
              <div class="Grid-cell u-lg-size2of3 " data-test-selector="ProfileTimeline">
               <div class="ProfileHeading">
                <div class="ProfileHeading-spacer">
                </div>
                <div class="ProfileHeading-content">
                 <h2 class="ProfileHeading-title u-hiddenVisually " id="content-main-heading">
                  Tweets
                 </h2>
                 <ul class="ProfileHeading-toggle">
                  <li class="ProfileHeading-toggleItem is-active" data-element-term="tweets_toggle">
                   <span aria-hidden="true">
                    Tweets
                   </span>
                   <span class="u-hiddenVisually">
                    Tweets, current page.
                   </span>
                  </li>
                  <li class="ProfileHeading-toggleItem u-textUserColor" data-element-term="tweets_with_replies_toggle">
                   <a class="ProfileHeading-toggleLink js-openSignupDialog js-nonNavigable" data-nav="tweets_with_replies_toggle" href="/MarsWxReport/with_replies">
                    Tweets &amp; replies
                   </a>
                  </li>
                  <li class="ProfileHeading-toggleItem u-textUserColor" data-element-term="photos_and_videos_toggle">
                   <a class="ProfileHeading-toggleLink js-openSignupDialog js-nonNavigable" data-nav="photos_and_videos_toggle" href="/MarsWxReport/media">
                    Media
                   </a>
                  </li>
                 </ul>
                </div>
               </div>
               <div class="ProfileWarningTimeline" data-element-context="blocked_profile">
                <h2 class="ProfileWarningTimeline-heading" id="content-main-heading">
                 You blocked
                 <span class="username u-dir u-textTruncate" dir="ltr">
                  @
                  <b>
                   MarsWxReport
                  </b>
                 </span>
                </h2>
                <p class="ProfileWarningTimeline-explanation">
                 Are you sure you want to view these Tweets? Viewing Tweets won't unblock
                 <span class="username u-dir u-textTruncate" dir="ltr">
                  @
                  <b>
                   MarsWxReport
                  </b>
                 </span>
                </p>
                <button class="EdgeButton EdgeButton--tertiary ProfileWarningTimeline-button">
                 Yes, view profile
                </button>
               </div>
               <div class="ScrollBumpDialog modal-container" id="scroll-bump-dialog">
                <div class="modal draggable">
                 <div class="modal-content clearfix">
                  <button class="modal-btn modal-close js-close" type="button">
                   <span class="Icon Icon--close Icon--medium">
                    <span class="visuallyhidden">
                     Close
                    </span>
                   </span>
                  </button>
                  <div class="modal-header">
                   <h3 class="modal-title">
                    Mars Weather followed
                   </h3>
                  </div>
                  <div class="modal-body">
                   <div class="loading">
                    <span class="spinner-bigger">
                    </span>
                   </div>
                   <ol class="ScrollBumpDialog-usersList clearfix js-users-list">
                   </ol>
                  </div>
                 </div>
                </div>
               </div>
               <div class="ProfileTimeline " id="timeline">
                <div class="stream-container " data-max-position="994766443555250176" data-min-position="982045230638739457">
                 <div class="stream-item js-new-items-bar-container">
                 </div>
                 <div class="stream">
                  <ol class="stream-items js-navigable-stream" id="stream-items-id">
                   <li class="js-stream-item stream-item stream-item " data-item-id="994766443555250176" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"994766443555250176","scribe_component":"tweet"}' id="stream-item-tweet-994766443555250176">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="994766443555250176" data-disclosure-type="" data-follows-you="false" data-item-id="994766443555250176" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/994766443555250176" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="994766443555250176" data-tweet-nonce="994766443555250176-db2ac3f3-4321-4ab8-9e00-814ac2a93ebb" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate ">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="994766443555250176" href="/MarsWxReport/status/994766443555250176" title="7:29 PM - 10 May 2018">
                         <span aria-hidden="true" class="_timestamp js-short-timestamp js-relative-timestamp" data-long-form="true" data-time="1526005776" data-time-ms="1526005776000">
                          46m
                         </span>
                         <span class="u-hiddenVisually" data-aria-label-part="last">
                          46 minutes ago
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <p aria-hidden="true" class="u-hiddenVisually" data-aria-label-part="1">
                       Mars Weather Retweeted Sam Sun
                      </p>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="4" lang="en">
                        <a class="twitter-hashtag pretty-link js-nav" data-query-source="hashtag_click" dir="ltr" href="/hashtag/InSight?src=hash">
                         <s>
                          #
                         </s>
                         <b>
                          InSight
                         </b>
                        </a>
                        rising above the California fog on liftoff.
                        <a class="twitter-timeline-link u-hidden" data-expanded-url="https://twitter.com/birdsnspace/status/993603886106660864" dir="ltr" href="https://t.co/7bMYYBvGlA" rel="nofollow noopener" target="_blank" title="https://twitter.com/birdsnspace/status/993603886106660864">
                         <span class="tco-ellipsis">
                         </span>
                         <span class="invisible">
                          https://
                         </span>
                         <span class="js-display-url">
                          twitter.com/birdsnspace/st
                         </span>
                         <span class="invisible">
                          atus/993603886106660864
                         </span>
                         <span class="tco-ellipsis">
                          <span class="invisible">
                          </span>
                          …
                         </span>
                        </a>
                       </p>
                      </div>
                      <p aria-hidden="true" class="u-hiddenVisually" data-aria-label-part="3">
                       Mars Weather added,
                      </p>
                      <div class="QuoteTweet u-block js-tweet-details-fixer">
                       <div class="QuoteTweet-container">
                        <a aria-hidden="true" class="QuoteTweet-link js-nav" data-conversation-id="993603886106660864" href="/BirdsNSpace/status/993603886106660864">
                        </a>
                        <div class="QuoteTweet-innerContainer u-cf js-permalink js-media-container" data-conversation-id="993603886106660864" data-item-id="993603886106660864" data-item-type="tweet" data-screen-name="BirdsNSpace" data-user-id="993061794296938497" href="/BirdsNSpace/status/993603886106660864" tabindex="0">
                         <div class="tweet-content">
                          <div class="QuoteMedia">
                           <div class="QuoteMedia-container js-quote-media-container">
                            <div class="QuoteMedia-singlePhoto">
                             <div class="QuoteMedia-photoContainer js-quote-photo" data-dominant-color="[38,19,10]" data-element-context="platform_photo_card" data-image-url="https://pbs.twimg.com/media/Dcn5APsVMAAj80X.jpg" style="background-color:rgba(38,19,10,1.0);">
                              <img alt="" data-aria-label-part="" src="https://pbs.twimg.com/media/Dcn5APsVMAAj80X.jpg" style="height: 100%; left: -25px;"/>
                             </div>
                            </div>
                           </div>
                          </div>
                          <div class="QuoteTweet-authorAndText u-alignTop">
                           <div class="QuoteTweet-originalAuthor u-cf u-textTruncate stream-item-header account-group js-user-profile-link">
                            <b class="QuoteTweet-fullname u-linkComplex-target">
                             Sam Sun
                            </b>
                            <span class="UserBadges">
                            </span>
                            <span class="UserNameBreak">
                            </span>
                            <span class="username u-dir u-textTruncate" dir="ltr">
                             @
                             <b>
                              BirdsNSpace
                             </b>
                            </span>
                           </div>
                           <div class="QuoteTweet-text tweet-text u-dir js-ellipsis" data-aria-label-part="2" dir="ltr" lang="en">
                            I've been quietly supporting
                            <span class="twitter-atreply pretty-link js-nav" data-mentioned-user-id="21292523" dir="ltr">
                             <s>
                              @
                             </s>
                             <b>
                              NASASpaceFlight
                             </b>
                            </span>
                            with aerial launch photography for a while but finally joining the twittersphere as this photo of the Mars
                            <span class="twitter-hashtag pretty-link js-nav" data-query-source="hashtag_click" dir="ltr">
                             <s>
                              #
                             </s>
                             <b>
                              InSight
                             </b>
                            </span>
                            launch wanted my audience.
                            <span class="twitter-hashtag pretty-link js-nav" data-query-source="hashtag_click" dir="ltr">
                             <s>
                              #
                             </s>
                             <b>
                              myfirstTweet
                             </b>
                            </span>
                            <span class="twitter-timeline-link u-hidden" data-pre-embedded="true" dir="ltr">
                             pic.twitter.com/51q1OFpU9j
                            </span>
                           </div>
                          </div>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-994766443555250176">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-retweet-count-aria-994766443555250176">
                           0 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="2">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-994766443555250176">
                           2 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-994766443555250176" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-994766443555250176" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-994766443555250176" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            2
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            2
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="994366302545498113" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"994366302545498113","scribe_component":"tweet"}' id="stream-item-tweet-994366302545498113">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="994366302545498113" data-disclosure-type="" data-follows-you="false" data-item-id="994366302545498113" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/994366302545498113" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="994366302545498113" data-tweet-nonce="994366302545498113-f57dfa51-0dc5-40c3-9b53-9b07ced4a009" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="994366302545498113" href="/MarsWxReport/status/994366302545498113" title="4:59 PM - 9 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1525910375" data-time-ms="1525910375000">
                          May 9
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2045 (May 08, 2018), Sunny, high -7C/19F, low -74C/-101F, pressure at 7.33 hPa, daylight 05:22-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-994366302545498113">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="5">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-994366302545498113">
                           5 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="9">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-994366302545498113">
                           9 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-994366302545498113" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-994366302545498113" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            5
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            5
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-994366302545498113" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            9
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            9
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="994076500340215809" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"994076500340215809","scribe_component":"tweet"}' id="stream-item-tweet-994076500340215809">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="994076500340215809" data-disclosure-type="" data-follows-you="false" data-item-id="994076500340215809" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/994076500340215809" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="994076500340215809" data-tweet-nonce="994076500340215809-9688eee4-4577-4903-82b4-eb1767d69422" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate ">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="994076500340215809" href="/MarsWxReport/status/994076500340215809" title="9:48 PM - 8 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1525841281" data-time-ms="1525841281000">
                          May 8
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <p aria-hidden="true" class="u-hiddenVisually" data-aria-label-part="1">
                       Mars Weather Retweeted Doug Ellison
                      </p>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="4" lang="en">
                        What a long beautiful neck full of science you have Curiosity’s Earth bound twin sister
                        <a class="twitter-timeline-link u-hidden" data-expanded-url="https://twitter.com/doug_ellison/status/994057810668212225" dir="ltr" href="https://t.co/NIJoNgmRzy" rel="nofollow noopener" target="_blank" title="https://twitter.com/doug_ellison/status/994057810668212225">
                         <span class="tco-ellipsis">
                         </span>
                         <span class="invisible">
                          https://
                         </span>
                         <span class="js-display-url">
                          twitter.com/doug_ellison/s
                         </span>
                         <span class="invisible">
                          tatus/994057810668212225
                         </span>
                         <span class="tco-ellipsis">
                          <span class="invisible">
                          </span>
                          …
                         </span>
                        </a>
                       </p>
                      </div>
                      <p aria-hidden="true" class="u-hiddenVisually" data-aria-label-part="3">
                       Mars Weather added,
                      </p>
                      <div class="QuoteTweet u-block js-tweet-details-fixer">
                       <div class="QuoteTweet-container">
                        <a aria-hidden="true" class="QuoteTweet-link js-nav" data-conversation-id="994057810668212225" href="/doug_ellison/status/994057810668212225">
                        </a>
                        <div class="QuoteTweet-innerContainer u-cf js-permalink js-media-container" data-conversation-id="994057810668212225" data-item-id="994057810668212225" data-item-type="tweet" data-screen-name="doug_ellison" data-user-id="15402623" href="/doug_ellison/status/994057810668212225" tabindex="0">
                         <div class="tweet-content">
                          <div class="QuoteMedia">
                           <div class="QuoteMedia-container js-quote-media-container">
                            <div class="QuoteMedia-singlePhoto">
                             <div class="QuoteMedia-photoContainer js-quote-photo" data-dominant-color="[64,61,47]" data-element-context="platform_photo_card" data-image-url="https://pbs.twimg.com/media/DcuaTNwVMAEqy3k.jpg" style="background-color:rgba(64,61,47,1.0);">
                              <img alt="" data-aria-label-part="" src="https://pbs.twimg.com/media/DcuaTNwVMAEqy3k.jpg" style="width: 100%; top: -81px;"/>
                             </div>
                            </div>
                           </div>
                          </div>
                          <div class="QuoteTweet-authorAndText u-alignTop">
                           <div class="QuoteTweet-originalAuthor u-cf u-textTruncate stream-item-header account-group js-user-profile-link">
                            <b class="QuoteTweet-fullname u-linkComplex-target">
                             Doug Ellison
                            </b>
                            <span class="UserBadges">
                            </span>
                            <span class="UserNameBreak">
                            </span>
                            <span class="username u-dir u-textTruncate" dir="ltr">
                             @
                             <b>
                              doug_ellison
                             </b>
                            </span>
                           </div>
                           <div class="QuoteTweet-text tweet-text u-dir js-ellipsis" data-aria-label-part="2" dir="ltr" lang="en">
                            So important to visit the testbed every now and again....reminds me of the hardware I'm operating on Mars. Having a mental model of it really helps with planning. Watching this hardware execute commands makes it all a lot less intangible.
                            <span class="twitter-timeline-link u-hidden" data-pre-embedded="true" dir="ltr">
                             pic.twitter.com/lMHq3kUlLp
                            </span>
                           </div>
                           <div class="self-thread-context">
                            Show this thread
                           </div>
                          </div>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-994076500340215809">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="1">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-994076500340215809">
                           1 retweet
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="4">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-994076500340215809">
                           4 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-994076500340215809" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-994076500340215809" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            1
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            1
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-994076500340215809" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            4
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            4
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="994003918148571136" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"994003918148571136","scribe_component":"tweet"}' id="stream-item-tweet-994003918148571136">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="994003918148571136" data-disclosure-type="" data-follows-you="false" data-item-id="994003918148571136" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/994003918148571136" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="994003918148571136" data-tweet-nonce="994003918148571136-ad1c7c7d-4dfa-4ad5-a908-93caebec15ba" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="994003918148571136" href="/MarsWxReport/status/994003918148571136" title="4:59 PM - 8 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1525823976" data-time-ms="1525823976000">
                          May 8
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2043 (May 06, 2018), Sunny, high -14C/6F, low -71C/-95F, pressure at 7.36 hPa, daylight 05:22-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-994003918148571136">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="7">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-994003918148571136">
                           7 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="19">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-994003918148571136">
                           19 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-994003918148571136" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-994003918148571136" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            7
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            7
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-994003918148571136" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="993641532522684416" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"993641532522684416","scribe_component":"tweet"}' id="stream-item-tweet-993641532522684416">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="993641532522684416" data-disclosure-type="" data-follows-you="false" data-item-id="993641532522684416" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/993641532522684416" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="993641532522684416" data-tweet-nonce="993641532522684416-de85f648-428e-447e-883d-5ed075a1e807" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="993641532522684416" href="/MarsWxReport/status/993641532522684416" title="4:59 PM - 7 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1525737576" data-time-ms="1525737576000">
                          May 7
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2042 (May 05, 2018), Sunny, high -7C/19F, low -72C/-97F, pressure at 7.30 hPa, daylight 05:23-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-993641532522684416">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="9">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-993641532522684416">
                           9 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="18">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-993641532522684416">
                           18 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-993641532522684416" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-993641532522684416" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            9
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            9
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-993641532522684416" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            18
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            18
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="992554379961126912" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"992554379961126912","scribe_component":"tweet"}' id="stream-item-tweet-992554379961126912">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="992554379961126912" data-disclosure-type="" data-follows-you="false" data-item-id="992554379961126912" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/992554379961126912" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="992554379961126912" data-tweet-nonce="992554379961126912-5cbd843e-8801-4e9b-b340-8096052da3da" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="992554379961126912" href="/MarsWxReport/status/992554379961126912" title="4:59 PM - 4 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1525478379" data-time-ms="1525478379000">
                          May 4
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2039 (May 02, 2018), Sunny, high 0C/32F, low -74C/-101F, pressure at 7.28 hPa, daylight 05:23-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-992554379961126912">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="8">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-992554379961126912">
                           8 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="18">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-992554379961126912">
                           18 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-992554379961126912" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-992554379961126912" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            8
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            8
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-992554379961126912" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            18
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            18
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="992191996340199424" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"992191996340199424","scribe_component":"tweet"}' id="stream-item-tweet-992191996340199424">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="992191996340199424" data-disclosure-type="" data-follows-you="false" data-item-id="992191996340199424" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/992191996340199424" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="992191996340199424" data-tweet-nonce="992191996340199424-dfb8edf8-c55f-447a-acdd-74431708b1b3" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="992191996340199424" href="/MarsWxReport/status/992191996340199424" title="4:59 PM - 3 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1525391980" data-time-ms="1525391980000">
                          May 3
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2038 (May 01, 2018), Sunny, high -3C/26F, low -74C/-101F, pressure at 7.26 hPa, daylight 05:23-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-992191996340199424">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="7">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-992191996340199424">
                           7 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="17">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-992191996340199424">
                           17 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-992191996340199424" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-992191996340199424" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            7
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            7
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-992191996340199424" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            17
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            17
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="991467229471440898" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"991467229471440898","scribe_component":"tweet"}' id="stream-item-tweet-991467229471440898">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="991467229471440898" data-disclosure-type="" data-follows-you="false" data-item-id="991467229471440898" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/991467229471440898" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="991467229471440898" data-tweet-nonce="991467229471440898-c6af5173-b534-4bd7-a8dd-8006e68f22b2" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="991467229471440898" href="/MarsWxReport/status/991467229471440898" title="4:59 PM - 1 May 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1525219182" data-time-ms="1525219182000">
                          May 1
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2037 (April 30, 2018), Sunny, high -2C/28F, low -75C/-103F, pressure at 7.25 hPa, daylight 05:24-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-991467229471440898">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="8">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-991467229471440898">
                           8 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="15">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-991467229471440898">
                           15 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-991467229471440898" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-991467229471440898" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            8
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            8
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-991467229471440898" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            15
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            15
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="991104845095555073" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"991104845095555073","scribe_component":"tweet"}' id="stream-item-tweet-991104845095555073">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="991104845095555073" data-disclosure-type="" data-follows-you="false" data-item-id="991104845095555073" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/991104845095555073" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="991104845095555073" data-tweet-nonce="991104845095555073-632e5530-cbf1-469e-90fb-620acbbb7fe4" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="991104845095555073" href="/MarsWxReport/status/991104845095555073" title="4:59 PM - 30 Apr 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1525132783" data-time-ms="1525132783000">
                          Apr 30
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2036 (April 29, 2018), Sunny, high -5C/23F, low -72C/-97F, pressure at 7.28 hPa, daylight 05:24-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-991104845095555073">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="10">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-991104845095555073">
                           10 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="19">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-991104845095555073">
                           19 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-991104845095555073" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-991104845095555073" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            10
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            10
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-991104845095555073" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="990017691770597376" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"990017691770597376","scribe_component":"tweet"}' id="stream-item-tweet-990017691770597376">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="990017691770597376" data-disclosure-type="" data-follows-you="false" data-item-id="990017691770597376" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/990017691770597376" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="990017691770597376" data-tweet-nonce="990017691770597376-22388fbc-51db-4bbd-b61e-1ab7dfd3efa4" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="990017691770597376" href="/MarsWxReport/status/990017691770597376" title="4:59 PM - 27 Apr 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1524873586" data-time-ms="1524873586000">
                          Apr 27
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2033 (April 25, 2018), Sunny, high -10C/14F, low -71C/-95F, pressure at 7.23 hPa, daylight 05:24-17:20
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-990017691770597376">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="10">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-990017691770597376">
                           10 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="19">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-990017691770597376">
                           19 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-990017691770597376" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-990017691770597376" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            10
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            10
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-990017691770597376" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="989292923329146880" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"989292923329146880","scribe_component":"tweet"}' id="stream-item-tweet-989292923329146880">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="989292923329146880" data-disclosure-type="" data-follows-you="false" data-item-id="989292923329146880" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/989292923329146880" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="989292923329146880" data-tweet-nonce="989292923329146880-09ac7803-f258-4e09-bb6d-8138ca29ecaa" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="989292923329146880" href="/MarsWxReport/status/989292923329146880" title="4:59 PM - 25 Apr 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1524700787" data-time-ms="1524700787000">
                          Apr 25
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2030 (April 22, 2018), Sunny, high -4C/24F, low -73C/-99F, pressure at 7.21 hPa, daylight 05:25-17:21
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-989292923329146880">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="6">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-989292923329146880">
                           6 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="22">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-989292923329146880">
                           22 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-989292923329146880" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-989292923329146880" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            6
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            6
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-989292923329146880" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            22
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            22
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="988568154732482561" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"988568154732482561","scribe_component":"tweet"}' id="stream-item-tweet-988568154732482561">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="988568154732482561" data-disclosure-type="" data-follows-you="false" data-item-id="988568154732482561" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/988568154732482561" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="988568154732482561" data-tweet-nonce="988568154732482561-7c1af47c-5cd5-4c00-b638-f8958e7e15f7" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="988568154732482561" href="/MarsWxReport/status/988568154732482561" title="4:59 PM - 23 Apr 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1524527989" data-time-ms="1524527989000">
                          Apr 23
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2029 (April 21, 2018), Sunny, high -11C/12F, low -72C/-97F, pressure at 7.22 hPa, daylight 05:25-17:21
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-988568154732482561">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="13">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-988568154732482561">
                           13 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="21">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-988568154732482561">
                           21 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-988568154732482561" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-988568154732482561" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            13
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            13
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-988568154732482561" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            21
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            21
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="987481001935949825" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"987481001935949825","scribe_component":"tweet"}' id="stream-item-tweet-987481001935949825">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="987481001935949825" data-disclosure-type="" data-follows-you="false" data-item-id="987481001935949825" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/987481001935949825" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="987481001935949825" data-tweet-nonce="987481001935949825-50a9a77a-a0a7-4738-bc6f-15eaf6cccd8f" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="987481001935949825" href="/MarsWxReport/status/987481001935949825" title="4:59 PM - 20 Apr 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1524268792" data-time-ms="1524268792000">
                          Apr 20
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2026 (April 18, 2018), Sunny, high -6C/21F, low -73C/-99F, pressure at 7.19 hPa, daylight 05:26-17:21
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-987481001935949825">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="11">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-987481001935949825">
                           11 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="23">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-987481001935949825">
                           23 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-987481001935949825" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-987481001935949825" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            11
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            11
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-987481001935949825" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            23
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            23
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="986756236937957379" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"986756236937957379","scribe_component":"tweet"}' id="stream-item-tweet-986756236937957379">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="986756236937957379" data-disclosure-type="" data-follows-you="false" data-item-id="986756236937957379" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/986756236937957379" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="986756236937957379" data-tweet-nonce="986756236937957379-ff8c0ecc-61b2-47b0-b549-1d2b8510666a" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="986756236937957379" href="/MarsWxReport/status/986756236937957379" title="4:59 PM - 18 Apr 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1524095994" data-time-ms="1524095994000">
                          Apr 18
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2024 (April 16, 2018), Sunny, high -7C/19F, low -76C/-104F, pressure at 7.20 hPa, daylight 05:26-17:21
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-986756236937957379">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="8">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-986756236937957379">
                           8 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="19">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-986756236937957379">
                           19 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-986756236937957379" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-986756236937957379" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            8
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            8
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-986756236937957379" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="986031468571803648" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"986031468571803648","scribe_component":"tweet"}' id="stream-item-tweet-986031468571803648">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="986031468571803648" data-disclosure-type="" data-follows-you="false" data-item-id="986031468571803648" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/986031468571803648" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="986031468571803648" data-tweet-nonce="986031468571803648-ec3f83f0-3041-4828-8c9e-9874494623b6" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="986031468571803648" href="/MarsWxReport/status/986031468571803648" title="4:59 PM - 16 Apr 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1523923196" data-time-ms="1523923196000">
                          Apr 16
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2022 (April 14, 2018), Sunny, high -4C/24F, low -73C/-99F, pressure at 7.19 hPa, daylight 05:27-17:21
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-986031468571803648">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="9">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-986031468571803648">
                           9 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="19">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-986031468571803648">
                           19 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-986031468571803648" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-986031468571803648" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            9
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            9
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-986031468571803648" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="984944314924007425" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"984944314924007425","scribe_component":"tweet"}' id="stream-item-tweet-984944314924007425">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="984944314924007425" data-disclosure-type="" data-follows-you="false" data-item-id="984944314924007425" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/984944314924007425" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="984944314924007425" data-tweet-nonce="984944314924007425-c8cb6630-8a30-4817-ab83-873c7e78bbfb" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="984944314924007425" href="/MarsWxReport/status/984944314924007425" title="4:59 PM - 13 Apr 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1523663998" data-time-ms="1523663998000">
                          Apr 13
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2019 (April 11, 2018), Sunny, high -6C/21F, low -75C/-103F, pressure at 7.18 hPa, daylight 05:27-17:21
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-984944314924007425">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="6">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-984944314924007425">
                           6 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="19">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-984944314924007425">
                           19 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-984944314924007425" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-984944314924007425" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            6
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            6
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-984944314924007425" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="983857162966446081" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"983857162966446081","scribe_component":"tweet"}' id="stream-item-tweet-983857162966446081">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="983857162966446081" data-disclosure-type="" data-follows-you="false" data-item-id="983857162966446081" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/983857162966446081" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="983857162966446081" data-tweet-nonce="983857162966446081-584c7c46-6bd3-49b4-a244-1875ce0ad231" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="983857162966446081" href="/MarsWxReport/status/983857162966446081" title="5:00 PM - 10 Apr 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1523404801" data-time-ms="1523404801000">
                          Apr 10
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2017 (April 09, 2018), Sunny, high -6C/21F, low -75C/-103F, pressure at 7.17 hPa, daylight 05:28-17:21
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="1">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-reply-count-aria-983857162966446081">
                           1 reply
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="6">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-983857162966446081">
                           6 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="17">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-983857162966446081">
                           17 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-983857162966446081" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            1
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-983857162966446081" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            6
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            6
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-983857162966446081" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            17
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            17
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="983494779764989952" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"983494779764989952","scribe_component":"tweet"}' id="stream-item-tweet-983494779764989952">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="983494779764989952" data-disclosure-type="" data-follows-you="false" data-item-id="983494779764989952" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/983494779764989952" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="983494779764989952" data-tweet-nonce="983494779764989952-6248bad2-a811-49eb-93da-1149948b84c8" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="983494779764989952" href="/MarsWxReport/status/983494779764989952" title="5:00 PM - 9 Apr 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1523318402" data-time-ms="1523318402000">
                          Apr 9
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2016 (April 08, 2018), Sunny, high -9C/15F, low -73C/-99F, pressure at 7.18 hPa, daylight 05:28-17:21
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-983494779764989952">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="10">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-983494779764989952">
                           10 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="21">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-983494779764989952">
                           21 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-983494779764989952" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-983494779764989952" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            10
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            10
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-983494779764989952" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            21
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            21
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="982543512058122241" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"982543512058122241","scribe_component":"tweet"}' id="stream-item-tweet-982543512058122241">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet tweet-has-context has-cards has-content " data-conversation-id="982543512058122241" data-disclosure-type="" data-follows-you="false" data-has-cards="true" data-item-id="982543512058122241" data-mentions="milkysa NASAJPL Wikipedia" data-name="Dr Jess Wade ???????" data-permalink-path="/jesswade/status/982543512058122241" data-reply-to-users-json="[{&quot;id_str&quot;:&quot;20904490&quot;,&quot;screen_name&quot;:&quot;jesswade&quot;,&quot;name&quot;:&quot;Dr Jess Wade \ud83d\udc69\ud83c\udffb\u200d\ud83d\udd2c&quot;,&quot;emojified_name&quot;:{&quot;text&quot;:&quot;Dr Jess Wade \ud83d\udc69\ud83c\udffb\u200d\ud83d\udd2c&quot;,&quot;emojified_text_as_html&quot;:&quot;Dr Jess Wade \u003cspan class=\&quot;Emoji Emoji--forLinks\&quot; style=\&quot;background-image:url('https:\/\/abs.twimg.com\/emoji\/v2\/72x72\/1f469-1f3fb-200d-1f52c.png')\&quot; title=\&quot;Female scientist (light skin tone)\&quot; aria-label=\&quot;Emoji: Female scientist (light skin tone)\&quot;\u003e&amp;nbsp;\u003c\/span\u003e\u003cspan class=\&quot;visuallyhidden\&quot; aria-hidden=\&quot;true\&quot;\u003e\ud83d\udc69\ud83c\udffb\u200d\ud83d\udd2c\u003c\/span\u003e&quot;}},{&quot;id_str&quot;:&quot;786939553&quot;,&quot;screen_name&quot;:&quot;MarsWxReport&quot;,&quot;name&quot;:&quot;Mars Weather&quot;,&quot;emojified_name&quot;:{&quot;text&quot;:&quot;Mars Weather&quot;,&quot;emojified_text_as_html&quot;:&quot;Mars Weather&quot;}},{&quot;id_str&quot;:&quot;104056037&quot;,&quot;screen_name&quot;:&quot;milkysa&quot;,&quot;name&quot;:&quot;Sarah Milkovich&quot;,&quot;emojified_name&quot;:{&quot;text&quot;:&quot;Sarah Milkovich&quot;,&quot;emojified_text_as_html&quot;:&quot;Sarah Milkovich&quot;}},{&quot;id_str&quot;:&quot;19802879&quot;,&quot;screen_name&quot;:&quot;NASAJPL&quot;,&quot;name&quot;:&quot;NASA JPL&quot;,&quot;emojified_name&quot;:{&quot;text&quot;:&quot;NASA JPL&quot;,&quot;emojified_text_as_html&quot;:&quot;NASA JPL&quot;}},{&quot;id_str&quot;:&quot;86390214&quot;,&quot;screen_name&quot;:&quot;Wikipedia&quot;,&quot;name&quot;:&quot;Wikipedia&quot;,&quot;emojified_name&quot;:{&quot;text&quot;:&quot;Wikipedia&quot;,&quot;emojified_text_as_html&quot;:&quot;Wikipedia&quot;}},{&quot;id_str&quot;:&quot;29719864&quot;,&quot;screen_name&quot;:&quot;WES1919&quot;,&quot;name&quot;:&quot;Women's Eng. Society&quot;,&quot;emojified_name&quot;:{&quot;text&quot;:&quot;Women's Eng. Society&quot;,&quot;emojified_text_as_html&quot;:&quot;Women&amp;#39;s Eng. Society&quot;}},{&quot;id_str&quot;:&quot;628765360&quot;,&quot;screen_name&quot;:&quot;Science_Grrl&quot;,&quot;name&quot;:&quot;Science Grrl&quot;,&quot;emojified_name&quot;:{&quot;text&quot;:&quot;Science Grrl&quot;,&quot;emojified_text_as_html&quot;:&quot;Science Grrl&quot;}},{&quot;id_str&quot;:&quot;800459756292882432&quot;,&quot;screen_name&quot;:&quot;500womensci&quot;,&quot;name&quot;:&quot;500womenscientists&quot;,&quot;emojified_name&quot;:{&quot;text&quot;:&quot;500womenscientists&quot;,&quot;emojified_text_as_html&quot;:&quot;500womenscientists&quot;}},{&quot;id_str&quot;:&quot;3283774369&quot;,&quot;screen_name&quot;:&quot;WikiWomenInRed&quot;,&quot;name&quot;:&quot;Women in Red&quot;,&quot;emojified_name&quot;:{&quot;text&quot;:&quot;Women in Red&quot;,&quot;emojified_text_as_html&quot;:&quot;Women in Red&quot;}},{&quot;id_str&quot;:&quot;806526020&quot;,&quot;screen_name&quot;:&quot;Rocket_Woman1&quot;,&quot;name&quot;:&quot;Vinita Marwaha Madill&quot;,&quot;emojified_name&quot;:{&quot;text&quot;:&quot;Vinita Marwaha Madill&quot;,&quot;emojified_text_as_html&quot;:&quot;Vinita Marwaha Madill&quot;}},{&quot;id_str&quot;:&quot;989452274&quot;,&quot;screen_name&quot;:&quot;Stemettes&quot;,&quot;name&quot;:&quot;Stemettes \ud83d\udc99 \u2605 # +&quot;,&quot;emojified_name&quot;:{&quot;text&quot;:&quot;Stemettes \ud83d\udc99 \u2605 # +&quot;,&quot;emojified_text_as_html&quot;:&quot;Stemettes \u003cspan class=\&quot;Emoji Emoji--forLinks\&quot; style=\&quot;background-image:url('https:\/\/abs.twimg.com\/emoji\/v2\/72x72\/1f499.png')\&quot; title=\&quot;Blue heart\&quot; aria-label=\&quot;Emoji: Blue heart\&quot;\u003e&amp;nbsp;\u003c\/span\u003e\u003cspan class=\&quot;visuallyhidden\&quot; aria-hidden=\&quot;true\&quot;\u003e\ud83d\udc99\u003c\/span\u003e \u2605 # +&quot;}}]" data-retweet-id="982801230832513024" data-retweeter="MarsWxReport" data-screen-name="jesswade" data-tagged="milkysa WES1919 NASAJPL Science_Grrl 500womensci WikiWomenInRed Rocket_Woman1 Stemettes" data-tweet-id="982543512058122241" data-tweet-nonce="982543512058122241-0670d7fa-c2db-4f2b-b910-3a57beae353f" data-tweet-stat-initialized="true" data-user-id="20904490" data-you-block="false" data-you-follow="false">
                     <div class="context">
                      <div class="tweet-context with-icn ">
                       <span class="Icon Icon--small Icon--retweeted">
                       </span>
                       <span class="js-retweet-text">
                        <a class="pretty-link js-user-profile-link" data-user-id="786939553" href="/MarsWxReport" rel="noopener">
                         <b>
                          Mars Weather
                         </b>
                        </a>
                        Retweeted
                       </span>
                      </div>
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="20904490" href="/jesswade">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/916307807573594112/sifVb75j_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Dr Jess Wade
                          <span aria-label="Emoji: Female scientist (light skin tone)" class="Emoji Emoji--forLinks" style="background-image:url('https://abs.twimg.com/emoji/v2/72x72/1f469-1f3fb-200d-1f52c.png')" title="Female scientist (light skin tone)">
                          </span>
                          <span aria-hidden="true" class="visuallyhidden">
                           ???????
                          </span>
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          jesswade
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="982543512058122241" href="/jesswade/status/982543512058122241" title="2:00 AM - 7 Apr 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1523091602" data-time-ms="1523091602000">
                          Apr 7
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        <img alt="??" aria-label="Emoji: Satellite" class="Emoji Emoji--forText" draggable="false" src="https://abs.twimg.com/emoji/v2/72x72/1f6f0.png" title="Satellite"/>
                        Meet Dr Sarah Milkovich (
                        <a class="twitter-atreply pretty-link js-nav" data-mentioned-user-id="104056037" dir="ltr" href="/milkysa">
                         <s>
                          @
                         </s>
                         <b>
                          milkysa
                         </b>
                        </a>
                        ), lead of Science Operations for Mars 2020
                        <a class="twitter-atreply pretty-link js-nav" data-mentioned-user-id="19802879" dir="ltr" href="/NASAJPL">
                         <s>
                          @
                         </s>
                         <b>
                          NASAJPL
                         </b>
                        </a>
                        . Milkovich was responsible for the MRO HiRISE
                        <img alt="??" aria-label="Emoji: Camera with flash" class="Emoji Emoji--forText" draggable="false" src="https://abs.twimg.com/emoji/v2/72x72/1f4f8.png" title="Camera with flash"/>
                        of the surface of Mars in 2012. New
                        <a class="twitter-atreply pretty-link js-nav" data-mentioned-user-id="86390214" dir="ltr" href="/Wikipedia">
                         <s>
                          @
                         </s>
                         <b>
                          Wikipedia
                         </b>
                        </a>
                        page:
                        <a class="twitter-timeline-link" data-expanded-url="https://en.wikipedia.org/wiki/Sarah_Milkovich" dir="ltr" href="https://t.co/DNl9S6dZvb" rel="nofollow noopener" target="_blank" title="https://en.wikipedia.org/wiki/Sarah_Milkovich">
                         <span class="tco-ellipsis">
                         </span>
                         <span class="invisible">
                          https://
                         </span>
                         <span class="js-display-url">
                          en.wikipedia.org/wiki/Sarah_Mil
                         </span>
                         <span class="invisible">
                          kovich
                         </span>
                         <span class="tco-ellipsis">
                          <span class="invisible">
                          </span>
                          …
                         </span>
                        </a>
                        <a class="twitter-hashtag pretty-link js-nav" data-query-source="hashtag_click" dir="ltr" href="/hashtag/womeninSTEM?src=hash">
                         <s>
                          #
                         </s>
                         <b>
                          womeninSTEM
                         </b>
                        </a>
                        <a class="twitter-timeline-link u-hidden" data-pre-embedded="true" dir="ltr" href="https://t.co/Kqz4Bpc9e2">
                         pic.twitter.com/Kqz4Bpc9e2
                        </a>
                       </p>
                      </div>
                      <div class="AdaptiveMediaOuterContainer">
                       <div class="AdaptiveMedia ">
                        <div class="AdaptiveMedia-container">
                         <div class="AdaptiveMedia-quadPhoto">
                          <div class="AdaptiveMedia-threeQuartersWidthPhoto">
                           <div class="AdaptiveMedia-photoContainer js-adaptive-photo " data-dominant-color="[43,51,64]" data-element-context="platform_photo_card" data-image-url="https://pbs.twimg.com/media/DaKyENcXkAEqRuZ.jpg" style="background-color:rgba(43,51,64,1.0);">
                            <img alt="" data-aria-label-part="" src="https://pbs.twimg.com/media/DaKyENcXkAEqRuZ.jpg" style="height: 100%; left: -41px;"/>
                           </div>
                          </div>
                          <div class="AdaptiveMedia-thirdHeightPhotoContainer">
                           <div class="AdaptiveMedia-thirdHeightPhoto">
                            <div class="AdaptiveMedia-photoContainer js-adaptive-photo " data-dominant-color="[64,50,37]" data-element-context="platform_photo_card" data-image-url="https://pbs.twimg.com/media/DaKyENXX4AAHX3-.jpg" style="background-color:rgba(64,50,37,1.0);">
                             <img alt="" data-aria-label-part="" src="https://pbs.twimg.com/media/DaKyENXX4AAHX3-.jpg" style="width: 100%; top: -13px;"/>
                            </div>
                           </div>
                           <div class="AdaptiveMedia-thirdHeightPhoto">
                            <div class="AdaptiveMedia-photoContainer js-adaptive-photo " data-dominant-color="[42,51,64]" data-element-context="platform_photo_card" data-image-url="https://pbs.twimg.com/media/DaKyENYWAAAz8C9.jpg" style="background-color:rgba(42,51,64,1.0);">
                             <img alt="" data-aria-label-part="" src="https://pbs.twimg.com/media/DaKyENYWAAAz8C9.jpg" style="height: 100%; left: -10px;"/>
                            </div>
                           </div>
                           <div class="AdaptiveMedia-thirdHeightPhoto">
                            <div class="AdaptiveMedia-photoContainer js-adaptive-photo " data-dominant-color="[61,61,64]" data-element-context="platform_photo_card" data-image-url="https://pbs.twimg.com/media/DaKyENfX0AAYa-0.jpg" style="background-color:rgba(61,61,64,1.0);">
                             <img alt="" data-aria-label-part="" src="https://pbs.twimg.com/media/DaKyENfX0AAYa-0.jpg" style="height: 100%; left: -42px;"/>
                            </div>
                           </div>
                          </div>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="media-tags-container">
                       <div class="media-tagging-block">
                        <a class="js-user-profile-link" data-user-id="104056037" href="/milkysa" rel="noopener">
                         Sarah Milkovich
                        </a>
                        ,
                        <a class="js-user-profile-link" data-user-id="29719864" href="/WES1919" rel="noopener">
                         Women's Eng. Society
                        </a>
                        ,
                        <a class="js-user-profile-link" data-user-id="19802879" href="/NASAJPL" rel="noopener">
                         NASA JPL
                        </a>
                        and
                        <a class="request-tagging-popup" data-activity-popup-title="Tagged in this photo" rel="noopener">
                         <b>
                          5 others
                         </b>
                        </a>
                        <div class="popup-tagged-users-list hidden">
                         <ol class="activity-popup-users">
                          <li class="js-stream-item stream-item stream-item " data-item-id="982543512058122241" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"982543512058122241","scribe_component":"tweet"}' id="stream-item-tweet-982543512058122241">
                           <div class="account js-actionable-user js-profile-popup-actionable " data-emojified-name="" data-feedback-token="" data-impression-id="" data-name="Sarah Milkovich" data-screen-name="milkysa" data-user-id="104056037">
                            <div class="follow-bar">
                             <div class="user-actions btn-group not-following " data-name="Sarah Milkovich" data-protected="false" data-screen-name="milkysa" data-user-id="104056037">
                              <span class="user-actions-follow-button js-follow-btn follow-button">
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text follow-text" type="button">
                                <span aria-hidden="true">
                                 Follow
                                </span>
                                <span class="u-hiddenVisually">
                                 Follow
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   milkysa
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--primary EdgeButton--medium button-text following-text" type="button">
                                <span aria-hidden="true">
                                 Following
                                </span>
                                <span class="u-hiddenVisually">
                                 Following
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   milkysa
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unfollow-text" type="button">
                                <span aria-hidden="true">
                                 Unfollow
                                </span>
                                <span class="u-hiddenVisually">
                                 Unfollow
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   milkysa
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--invertedDanger EdgeButton--medium button-text blocked-text" type="button">
                                <span aria-hidden="true">
                                 Blocked
                                </span>
                                <span class="u-hiddenVisually">
                                 Blocked
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   milkysa
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unblock-text" type="button">
                                <span aria-hidden="true">
                                 Unblock
                                </span>
                                <span class="u-hiddenVisually">
                                 Unblock
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   milkysa
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text pending-text" type="button">
                                <span aria-hidden="true">
                                 Pending
                                </span>
                                <span class="u-hiddenVisually">
                                 Pending follow request from
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   milkysa
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text cancel-text" type="button">
                                <span aria-hidden="true">
                                 Cancel
                                </span>
                                <span class="u-hiddenVisually">
                                 Cancel your follow request to
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   milkysa
                                  </b>
                                 </span>
                                </span>
                               </button>
                              </span>
                             </div>
                            </div>
                            <div class="activity-user-profile-content">
                             <div class=" content">
                              <div class="stream-item-header">
                               <a class="account-group js-user-profile-link" href="/milkysa" rel="noopener">
                                <img alt="" class="avatar js-action-profile-avatar " data-user-id="104056037" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_normal.jpg"/>
                                <strong class="fullname">
                                 Sarah Milkovich
                                </strong>
                                <span class="UserBadges">
                                </span>
                                <span class="UserNameBreak">
                                </span>
                                <span class="username u-dir u-textTruncate" dir="ltr">
                                 @
                                 <b>
                                  milkysa
                                 </b>
                                </span>
                               </a>
                              </div>
                              <p class="bio u-dir" dir="ltr">
                               Updates as avail from the REMS weather instrument aboard
                               <a class="tweet-url twitter-atreply pretty-link" data-mentioned-user-id="0" dir="ltr" href="/MarsCuriosity" rel="nofollow">
                                <s>
                                 @
                                </s>
                                <b>
                                 MarsCuriosity
                                </b>
                               </a>
                               .  Data credit: Centro deAstrobiologia, FMI, JPL/NASA, Not an official acct.
                              </p>
                             </div>
                            </div>
                           </div>
                          </li>
                          <li class="js-stream-item stream-item stream-item " data-item-id="982543512058122241" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"982543512058122241","scribe_component":"tweet"}' id="stream-item-tweet-982543512058122241">
                           <div class="account js-actionable-user js-profile-popup-actionable " data-emojified-name="" data-feedback-token="" data-impression-id="" data-name="Women's Eng. Society" data-screen-name="WES1919" data-user-id="29719864">
                            <div class="follow-bar">
                             <div class="user-actions btn-group not-following " data-name="Women's Eng. Society" data-protected="false" data-screen-name="WES1919" data-user-id="29719864">
                              <span class="user-actions-follow-button js-follow-btn follow-button">
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text follow-text" type="button">
                                <span aria-hidden="true">
                                 Follow
                                </span>
                                <span class="u-hiddenVisually">
                                 Follow
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   WES1919
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--primary EdgeButton--medium button-text following-text" type="button">
                                <span aria-hidden="true">
                                 Following
                                </span>
                                <span class="u-hiddenVisually">
                                 Following
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   WES1919
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unfollow-text" type="button">
                                <span aria-hidden="true">
                                 Unfollow
                                </span>
                                <span class="u-hiddenVisually">
                                 Unfollow
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   WES1919
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--invertedDanger EdgeButton--medium button-text blocked-text" type="button">
                                <span aria-hidden="true">
                                 Blocked
                                </span>
                                <span class="u-hiddenVisually">
                                 Blocked
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   WES1919
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unblock-text" type="button">
                                <span aria-hidden="true">
                                 Unblock
                                </span>
                                <span class="u-hiddenVisually">
                                 Unblock
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   WES1919
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text pending-text" type="button">
                                <span aria-hidden="true">
                                 Pending
                                </span>
                                <span class="u-hiddenVisually">
                                 Pending follow request from
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   WES1919
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text cancel-text" type="button">
                                <span aria-hidden="true">
                                 Cancel
                                </span>
                                <span class="u-hiddenVisually">
                                 Cancel your follow request to
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   WES1919
                                  </b>
                                 </span>
                                </span>
                               </button>
                              </span>
                             </div>
                            </div>
                            <div class="activity-user-profile-content">
                             <div class=" content">
                              <div class="stream-item-header">
                               <a class="account-group js-user-profile-link" href="/WES1919" rel="noopener">
                                <img alt="" class="avatar js-action-profile-avatar " data-user-id="29719864" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_normal.jpg"/>
                                <strong class="fullname">
                                 Women's Eng. Society
                                </strong>
                                <span class="UserBadges">
                                </span>
                                <span class="UserNameBreak">
                                </span>
                                <span class="username u-dir u-textTruncate" dir="ltr">
                                 @
                                 <b>
                                  WES1919
                                 </b>
                                </span>
                               </a>
                              </div>
                              <p class="bio u-dir" dir="ltr">
                               Updates as avail from the REMS weather instrument aboard
                               <a class="tweet-url twitter-atreply pretty-link" data-mentioned-user-id="0" dir="ltr" href="/MarsCuriosity" rel="nofollow">
                                <s>
                                 @
                                </s>
                                <b>
                                 MarsCuriosity
                                </b>
                               </a>
                               .  Data credit: Centro deAstrobiologia, FMI, JPL/NASA, Not an official acct.
                              </p>
                             </div>
                            </div>
                           </div>
                          </li>
                          <li class="js-stream-item stream-item stream-item " data-item-id="982543512058122241" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"982543512058122241","scribe_component":"tweet"}' id="stream-item-tweet-982543512058122241">
                           <div class="account js-actionable-user js-profile-popup-actionable " data-emojified-name="" data-feedback-token="" data-impression-id="" data-name="NASA JPL" data-screen-name="NASAJPL" data-user-id="19802879">
                            <div class="follow-bar">
                             <div class="user-actions btn-group not-following " data-name="NASA JPL" data-protected="false" data-screen-name="NASAJPL" data-user-id="19802879">
                              <span class="user-actions-follow-button js-follow-btn follow-button">
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text follow-text" type="button">
                                <span aria-hidden="true">
                                 Follow
                                </span>
                                <span class="u-hiddenVisually">
                                 Follow
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   NASAJPL
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--primary EdgeButton--medium button-text following-text" type="button">
                                <span aria-hidden="true">
                                 Following
                                </span>
                                <span class="u-hiddenVisually">
                                 Following
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   NASAJPL
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unfollow-text" type="button">
                                <span aria-hidden="true">
                                 Unfollow
                                </span>
                                <span class="u-hiddenVisually">
                                 Unfollow
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   NASAJPL
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--invertedDanger EdgeButton--medium button-text blocked-text" type="button">
                                <span aria-hidden="true">
                                 Blocked
                                </span>
                                <span class="u-hiddenVisually">
                                 Blocked
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   NASAJPL
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unblock-text" type="button">
                                <span aria-hidden="true">
                                 Unblock
                                </span>
                                <span class="u-hiddenVisually">
                                 Unblock
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   NASAJPL
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text pending-text" type="button">
                                <span aria-hidden="true">
                                 Pending
                                </span>
                                <span class="u-hiddenVisually">
                                 Pending follow request from
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   NASAJPL
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text cancel-text" type="button">
                                <span aria-hidden="true">
                                 Cancel
                                </span>
                                <span class="u-hiddenVisually">
                                 Cancel your follow request to
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   NASAJPL
                                  </b>
                                 </span>
                                </span>
                               </button>
                              </span>
                             </div>
                            </div>
                            <div class="activity-user-profile-content">
                             <div class=" content">
                              <div class="stream-item-header">
                               <a class="account-group js-user-profile-link" href="/NASAJPL" rel="noopener">
                                <img alt="" class="avatar js-action-profile-avatar " data-user-id="19802879" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_normal.jpg"/>
                                <strong class="fullname">
                                 NASA JPL
                                </strong>
                                <span class="UserBadges">
                                </span>
                                <span class="UserNameBreak">
                                </span>
                                <span class="username u-dir u-textTruncate" dir="ltr">
                                 @
                                 <b>
                                  NASAJPL
                                 </b>
                                </span>
                               </a>
                              </div>
                              <p class="bio u-dir" dir="ltr">
                               Updates as avail from the REMS weather instrument aboard
                               <a class="tweet-url twitter-atreply pretty-link" data-mentioned-user-id="0" dir="ltr" href="/MarsCuriosity" rel="nofollow">
                                <s>
                                 @
                                </s>
                                <b>
                                 MarsCuriosity
                                </b>
                               </a>
                               .  Data credit: Centro deAstrobiologia, FMI, JPL/NASA, Not an official acct.
                              </p>
                             </div>
                            </div>
                           </div>
                          </li>
                          <li class="js-stream-item stream-item stream-item " data-item-id="982543512058122241" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"982543512058122241","scribe_component":"tweet"}' id="stream-item-tweet-982543512058122241">
                           <div class="account js-actionable-user js-profile-popup-actionable " data-emojified-name="" data-feedback-token="" data-impression-id="" data-name="Science Grrl" data-screen-name="Science_Grrl" data-user-id="628765360">
                            <div class="follow-bar">
                             <div class="user-actions btn-group not-following " data-name="Science Grrl" data-protected="false" data-screen-name="Science_Grrl" data-user-id="628765360">
                              <span class="user-actions-follow-button js-follow-btn follow-button">
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text follow-text" type="button">
                                <span aria-hidden="true">
                                 Follow
                                </span>
                                <span class="u-hiddenVisually">
                                 Follow
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Science_Grrl
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--primary EdgeButton--medium button-text following-text" type="button">
                                <span aria-hidden="true">
                                 Following
                                </span>
                                <span class="u-hiddenVisually">
                                 Following
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Science_Grrl
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unfollow-text" type="button">
                                <span aria-hidden="true">
                                 Unfollow
                                </span>
                                <span class="u-hiddenVisually">
                                 Unfollow
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Science_Grrl
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--invertedDanger EdgeButton--medium button-text blocked-text" type="button">
                                <span aria-hidden="true">
                                 Blocked
                                </span>
                                <span class="u-hiddenVisually">
                                 Blocked
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Science_Grrl
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unblock-text" type="button">
                                <span aria-hidden="true">
                                 Unblock
                                </span>
                                <span class="u-hiddenVisually">
                                 Unblock
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Science_Grrl
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text pending-text" type="button">
                                <span aria-hidden="true">
                                 Pending
                                </span>
                                <span class="u-hiddenVisually">
                                 Pending follow request from
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Science_Grrl
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text cancel-text" type="button">
                                <span aria-hidden="true">
                                 Cancel
                                </span>
                                <span class="u-hiddenVisually">
                                 Cancel your follow request to
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Science_Grrl
                                  </b>
                                 </span>
                                </span>
                               </button>
                              </span>
                             </div>
                            </div>
                            <div class="activity-user-profile-content">
                             <div class=" content">
                              <div class="stream-item-header">
                               <a class="account-group js-user-profile-link" href="/Science_Grrl" rel="noopener">
                                <img alt="" class="avatar js-action-profile-avatar " data-user-id="628765360" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_normal.jpg"/>
                                <strong class="fullname">
                                 Science Grrl
                                </strong>
                                <span class="UserBadges">
                                </span>
                                <span class="UserNameBreak">
                                </span>
                                <span class="username u-dir u-textTruncate" dir="ltr">
                                 @
                                 <b>
                                  Science_Grrl
                                 </b>
                                </span>
                               </a>
                              </div>
                              <p class="bio u-dir" dir="ltr">
                               Updates as avail from the REMS weather instrument aboard
                               <a class="tweet-url twitter-atreply pretty-link" data-mentioned-user-id="0" dir="ltr" href="/MarsCuriosity" rel="nofollow">
                                <s>
                                 @
                                </s>
                                <b>
                                 MarsCuriosity
                                </b>
                               </a>
                               .  Data credit: Centro deAstrobiologia, FMI, JPL/NASA, Not an official acct.
                              </p>
                             </div>
                            </div>
                           </div>
                          </li>
                          <li class="js-stream-item stream-item stream-item " data-item-id="982543512058122241" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"982543512058122241","scribe_component":"tweet"}' id="stream-item-tweet-982543512058122241">
                           <div class="account js-actionable-user js-profile-popup-actionable " data-emojified-name="" data-feedback-token="" data-impression-id="" data-name="500womenscientists" data-screen-name="500womensci" data-user-id="800459756292882432">
                            <div class="follow-bar">
                             <div class="user-actions btn-group not-following " data-name="500womenscientists" data-protected="false" data-screen-name="500womensci" data-user-id="800459756292882432">
                              <span class="user-actions-follow-button js-follow-btn follow-button">
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text follow-text" type="button">
                                <span aria-hidden="true">
                                 Follow
                                </span>
                                <span class="u-hiddenVisually">
                                 Follow
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   500womensci
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--primary EdgeButton--medium button-text following-text" type="button">
                                <span aria-hidden="true">
                                 Following
                                </span>
                                <span class="u-hiddenVisually">
                                 Following
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   500womensci
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unfollow-text" type="button">
                                <span aria-hidden="true">
                                 Unfollow
                                </span>
                                <span class="u-hiddenVisually">
                                 Unfollow
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   500womensci
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--invertedDanger EdgeButton--medium button-text blocked-text" type="button">
                                <span aria-hidden="true">
                                 Blocked
                                </span>
                                <span class="u-hiddenVisually">
                                 Blocked
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   500womensci
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unblock-text" type="button">
                                <span aria-hidden="true">
                                 Unblock
                                </span>
                                <span class="u-hiddenVisually">
                                 Unblock
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   500womensci
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text pending-text" type="button">
                                <span aria-hidden="true">
                                 Pending
                                </span>
                                <span class="u-hiddenVisually">
                                 Pending follow request from
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   500womensci
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text cancel-text" type="button">
                                <span aria-hidden="true">
                                 Cancel
                                </span>
                                <span class="u-hiddenVisually">
                                 Cancel your follow request to
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   500womensci
                                  </b>
                                 </span>
                                </span>
                               </button>
                              </span>
                             </div>
                            </div>
                            <div class="activity-user-profile-content">
                             <div class=" content">
                              <div class="stream-item-header">
                               <a class="account-group js-user-profile-link" href="/500womensci" rel="noopener">
                                <img alt="" class="avatar js-action-profile-avatar " data-user-id="800459756292882432" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_normal.jpg"/>
                                <strong class="fullname">
                                 500womenscientists
                                </strong>
                                <span class="UserBadges">
                                </span>
                                <span class="UserNameBreak">
                                </span>
                                <span class="username u-dir u-textTruncate" dir="ltr">
                                 @
                                 <b>
                                  500womensci
                                 </b>
                                </span>
                               </a>
                              </div>
                              <p class="bio u-dir" dir="ltr">
                               Updates as avail from the REMS weather instrument aboard
                               <a class="tweet-url twitter-atreply pretty-link" data-mentioned-user-id="0" dir="ltr" href="/MarsCuriosity" rel="nofollow">
                                <s>
                                 @
                                </s>
                                <b>
                                 MarsCuriosity
                                </b>
                               </a>
                               .  Data credit: Centro deAstrobiologia, FMI, JPL/NASA, Not an official acct.
                              </p>
                             </div>
                            </div>
                           </div>
                          </li>
                          <li class="js-stream-item stream-item stream-item " data-item-id="982543512058122241" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"982543512058122241","scribe_component":"tweet"}' id="stream-item-tweet-982543512058122241">
                           <div class="account js-actionable-user js-profile-popup-actionable " data-emojified-name="" data-feedback-token="" data-impression-id="" data-name="Women in Red" data-screen-name="WikiWomenInRed" data-user-id="3283774369">
                            <div class="follow-bar">
                             <div class="user-actions btn-group not-following " data-name="Women in Red" data-protected="false" data-screen-name="WikiWomenInRed" data-user-id="3283774369">
                              <span class="user-actions-follow-button js-follow-btn follow-button">
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text follow-text" type="button">
                                <span aria-hidden="true">
                                 Follow
                                </span>
                                <span class="u-hiddenVisually">
                                 Follow
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   WikiWomenInRed
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--primary EdgeButton--medium button-text following-text" type="button">
                                <span aria-hidden="true">
                                 Following
                                </span>
                                <span class="u-hiddenVisually">
                                 Following
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   WikiWomenInRed
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unfollow-text" type="button">
                                <span aria-hidden="true">
                                 Unfollow
                                </span>
                                <span class="u-hiddenVisually">
                                 Unfollow
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   WikiWomenInRed
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--invertedDanger EdgeButton--medium button-text blocked-text" type="button">
                                <span aria-hidden="true">
                                 Blocked
                                </span>
                                <span class="u-hiddenVisually">
                                 Blocked
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   WikiWomenInRed
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unblock-text" type="button">
                                <span aria-hidden="true">
                                 Unblock
                                </span>
                                <span class="u-hiddenVisually">
                                 Unblock
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   WikiWomenInRed
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text pending-text" type="button">
                                <span aria-hidden="true">
                                 Pending
                                </span>
                                <span class="u-hiddenVisually">
                                 Pending follow request from
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   WikiWomenInRed
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text cancel-text" type="button">
                                <span aria-hidden="true">
                                 Cancel
                                </span>
                                <span class="u-hiddenVisually">
                                 Cancel your follow request to
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   WikiWomenInRed
                                  </b>
                                 </span>
                                </span>
                               </button>
                              </span>
                             </div>
                            </div>
                            <div class="activity-user-profile-content">
                             <div class=" content">
                              <div class="stream-item-header">
                               <a class="account-group js-user-profile-link" href="/WikiWomenInRed" rel="noopener">
                                <img alt="" class="avatar js-action-profile-avatar " data-user-id="3283774369" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_normal.jpg"/>
                                <strong class="fullname">
                                 Women in Red
                                </strong>
                                <span class="UserBadges">
                                </span>
                                <span class="UserNameBreak">
                                </span>
                                <span class="username u-dir u-textTruncate" dir="ltr">
                                 @
                                 <b>
                                  WikiWomenInRed
                                 </b>
                                </span>
                               </a>
                              </div>
                              <p class="bio u-dir" dir="ltr">
                               Updates as avail from the REMS weather instrument aboard
                               <a class="tweet-url twitter-atreply pretty-link" data-mentioned-user-id="0" dir="ltr" href="/MarsCuriosity" rel="nofollow">
                                <s>
                                 @
                                </s>
                                <b>
                                 MarsCuriosity
                                </b>
                               </a>
                               .  Data credit: Centro deAstrobiologia, FMI, JPL/NASA, Not an official acct.
                              </p>
                             </div>
                            </div>
                           </div>
                          </li>
                          <li class="js-stream-item stream-item stream-item " data-item-id="982543512058122241" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"982543512058122241","scribe_component":"tweet"}' id="stream-item-tweet-982543512058122241">
                           <div class="account js-actionable-user js-profile-popup-actionable " data-emojified-name="" data-feedback-token="" data-impression-id="" data-name="Vinita Marwaha Madill" data-screen-name="Rocket_Woman1" data-user-id="806526020">
                            <div class="follow-bar">
                             <div class="user-actions btn-group not-following " data-name="Vinita Marwaha Madill" data-protected="false" data-screen-name="Rocket_Woman1" data-user-id="806526020">
                              <span class="user-actions-follow-button js-follow-btn follow-button">
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text follow-text" type="button">
                                <span aria-hidden="true">
                                 Follow
                                </span>
                                <span class="u-hiddenVisually">
                                 Follow
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Rocket_Woman1
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--primary EdgeButton--medium button-text following-text" type="button">
                                <span aria-hidden="true">
                                 Following
                                </span>
                                <span class="u-hiddenVisually">
                                 Following
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Rocket_Woman1
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unfollow-text" type="button">
                                <span aria-hidden="true">
                                 Unfollow
                                </span>
                                <span class="u-hiddenVisually">
                                 Unfollow
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Rocket_Woman1
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--invertedDanger EdgeButton--medium button-text blocked-text" type="button">
                                <span aria-hidden="true">
                                 Blocked
                                </span>
                                <span class="u-hiddenVisually">
                                 Blocked
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Rocket_Woman1
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unblock-text" type="button">
                                <span aria-hidden="true">
                                 Unblock
                                </span>
                                <span class="u-hiddenVisually">
                                 Unblock
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Rocket_Woman1
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text pending-text" type="button">
                                <span aria-hidden="true">
                                 Pending
                                </span>
                                <span class="u-hiddenVisually">
                                 Pending follow request from
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Rocket_Woman1
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text cancel-text" type="button">
                                <span aria-hidden="true">
                                 Cancel
                                </span>
                                <span class="u-hiddenVisually">
                                 Cancel your follow request to
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Rocket_Woman1
                                  </b>
                                 </span>
                                </span>
                               </button>
                              </span>
                             </div>
                            </div>
                            <div class="activity-user-profile-content">
                             <div class=" content">
                              <div class="stream-item-header">
                               <a class="account-group js-user-profile-link" href="/Rocket_Woman1" rel="noopener">
                                <img alt="" class="avatar js-action-profile-avatar " data-user-id="806526020" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_normal.jpg"/>
                                <strong class="fullname">
                                 Vinita Marwaha Madill
                                </strong>
                                <span class="UserBadges">
                                </span>
                                <span class="UserNameBreak">
                                </span>
                                <span class="username u-dir u-textTruncate" dir="ltr">
                                 @
                                 <b>
                                  Rocket_Woman1
                                 </b>
                                </span>
                               </a>
                              </div>
                              <p class="bio u-dir" dir="ltr">
                               Updates as avail from the REMS weather instrument aboard
                               <a class="tweet-url twitter-atreply pretty-link" data-mentioned-user-id="0" dir="ltr" href="/MarsCuriosity" rel="nofollow">
                                <s>
                                 @
                                </s>
                                <b>
                                 MarsCuriosity
                                </b>
                               </a>
                               .  Data credit: Centro deAstrobiologia, FMI, JPL/NASA, Not an official acct.
                              </p>
                             </div>
                            </div>
                           </div>
                          </li>
                          <li class="js-stream-item stream-item stream-item " data-item-id="982543512058122241" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"982543512058122241","scribe_component":"tweet"}' id="stream-item-tweet-982543512058122241">
                           <div class="account js-actionable-user js-profile-popup-actionable " data-emojified-name="" data-feedback-token="" data-impression-id="" data-name="Stemettes ?? ? # +" data-screen-name="Stemettes" data-user-id="989452274">
                            <div class="follow-bar">
                             <div class="user-actions btn-group not-following " data-name="Stemettes ?? ? # +" data-protected="false" data-screen-name="Stemettes" data-user-id="989452274">
                              <span class="user-actions-follow-button js-follow-btn follow-button">
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text follow-text" type="button">
                                <span aria-hidden="true">
                                 Follow
                                </span>
                                <span class="u-hiddenVisually">
                                 Follow
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Stemettes
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--primary EdgeButton--medium button-text following-text" type="button">
                                <span aria-hidden="true">
                                 Following
                                </span>
                                <span class="u-hiddenVisually">
                                 Following
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Stemettes
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unfollow-text" type="button">
                                <span aria-hidden="true">
                                 Unfollow
                                </span>
                                <span class="u-hiddenVisually">
                                 Unfollow
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Stemettes
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--invertedDanger EdgeButton--medium button-text blocked-text" type="button">
                                <span aria-hidden="true">
                                 Blocked
                                </span>
                                <span class="u-hiddenVisually">
                                 Blocked
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Stemettes
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--danger EdgeButton--medium button-text unblock-text" type="button">
                                <span aria-hidden="true">
                                 Unblock
                                </span>
                                <span class="u-hiddenVisually">
                                 Unblock
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Stemettes
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text pending-text" type="button">
                                <span aria-hidden="true">
                                 Pending
                                </span>
                                <span class="u-hiddenVisually">
                                 Pending follow request from
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Stemettes
                                  </b>
                                 </span>
                                </span>
                               </button>
                               <button class=" EdgeButton EdgeButton--secondary EdgeButton--medium button-text cancel-text" type="button">
                                <span aria-hidden="true">
                                 Cancel
                                </span>
                                <span class="u-hiddenVisually">
                                 Cancel your follow request to
                                 <span class="username u-dir u-textTruncate" dir="ltr">
                                  @
                                  <b>
                                   Stemettes
                                  </b>
                                 </span>
                                </span>
                               </button>
                              </span>
                             </div>
                            </div>
                            <div class="activity-user-profile-content">
                             <div class=" content">
                              <div class="stream-item-header">
                               <a class="account-group js-user-profile-link" href="/Stemettes" rel="noopener">
                                <img alt="" class="avatar js-action-profile-avatar " data-user-id="989452274" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_normal.jpg"/>
                                <strong class="fullname">
                                 Stemettes
                                 <span aria-label="Emoji: Blue heart" class="Emoji Emoji--forLinks" style="background-image:url('https://abs.twimg.com/emoji/v2/72x72/1f499.png')" title="Blue heart">
                                 </span>
                                 <span aria-hidden="true" class="visuallyhidden">
                                  ??
                                 </span>
                                 ? # +
                                </strong>
                                <span class="UserBadges">
                                </span>
                                <span class="UserNameBreak">
                                </span>
                                <span class="username u-dir u-textTruncate" dir="ltr">
                                 @
                                 <b>
                                  Stemettes
                                 </b>
                                </span>
                               </a>
                              </div>
                              <p class="bio u-dir" dir="ltr">
                               Updates as avail from the REMS weather instrument aboard
                               <a class="tweet-url twitter-atreply pretty-link" data-mentioned-user-id="0" dir="ltr" href="/MarsCuriosity" rel="nofollow">
                                <s>
                                 @
                                </s>
                                <b>
                                 MarsCuriosity
                                </b>
                               </a>
                               .  Data credit: Centro deAstrobiologia, FMI, JPL/NASA, Not an official acct.
                              </p>
                             </div>
                            </div>
                           </div>
                          </li>
                         </ol>
                        </div>
                       </div>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="1">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-reply-count-aria-982543512058122241">
                           1 reply
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="31">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-982543512058122241">
                           31 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="85">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-982543512058122241">
                           85 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-982543512058122241" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            1
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-982543512058122241" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            31
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            31
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-982543512058122241" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            85
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            85
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                   <li class="js-stream-item stream-item stream-item " data-item-id="982045230638739457" data-item-type="tweet" data-suggestion-json='{"suggestion_details":{},"tweet_ids":"982045230638739457","scribe_component":"tweet"}' id="stream-item-tweet-982045230638739457">
                    <div class="tweet js-stream-tweet js-actionable-tweet js-profile-popup-actionable dismissible-content original-tweet js-original-tweet " data-conversation-id="982045230638739457" data-disclosure-type="" data-follows-you="false" data-item-id="982045230638739457" data-name="Mars Weather" data-permalink-path="/MarsWxReport/status/982045230638739457" data-reply-to-users-json='[{"id_str":"786939553","screen_name":"MarsWxReport","name":"Mars Weather","emojified_name":{"text":"Mars Weather","emojified_text_as_html":"Mars Weather"}}]' data-screen-name="MarsWxReport" data-tweet-id="982045230638739457" data-tweet-nonce="982045230638739457-b3a80cc5-2d37-4b74-a259-c0ce8461bb57" data-tweet-stat-initialized="true" data-user-id="786939553" data-you-block="false" data-you-follow="false">
                     <div class="context">
                     </div>
                     <div class="content">
                      <div class="stream-item-header">
                       <a class="account-group js-account-group js-action-profile js-user-profile-link js-nav" data-user-id="786939553" href="/MarsWxReport">
                        <img alt="" class="avatar js-action-profile-avatar" src="https://pbs.twimg.com/profile_images/2552209293/220px-Mars_atmosphere_bigger.jpg"/>
                        <span class="FullNameGroup">
                         <strong class="fullname show-popup-with-id u-textTruncate " data-aria-label-part="">
                          Mars Weather
                         </strong>
                         <span>
                          ?
                         </span>
                         <span class="UserBadges">
                         </span>
                         <span class="UserNameBreak">
                         </span>
                        </span>
                        <span class="username u-dir u-textTruncate" data-aria-label-part="" dir="ltr">
                         @
                         <b>
                          MarsWxReport
                         </b>
                        </span>
                       </a>
                       <small class="time">
                        <a class="tweet-timestamp js-permalink js-nav js-tooltip" data-conversation-id="982045230638739457" href="/MarsWxReport/status/982045230638739457" title="5:00 PM - 5 Apr 2018">
                         <span class="_timestamp js-short-timestamp " data-aria-label-part="last" data-long-form="true" data-time="1522972803" data-time-ms="1522972803000">
                          Apr 5
                         </span>
                        </a>
                       </small>
                       <div class="ProfileTweet-action ProfileTweet-action--more js-more-ProfileTweet-actions">
                        <div class="dropdown">
                         <button class="ProfileTweet-actionButton u-textUserColorHover dropdown-toggle js-dropdown-toggle" type="button">
                          <div class="IconContainer js-tooltip" title="More">
                           <span class="Icon Icon--caretDownLight Icon--small">
                           </span>
                           <span class="u-hiddenVisually">
                            More
                           </span>
                          </div>
                         </button>
                         <div class="dropdown-menu is-autoCentered">
                          <div class="dropdown-caret">
                           <div class="caret-outer">
                           </div>
                           <div class="caret-inner">
                           </div>
                          </div>
                          <ul>
                           <li class="copy-link-to-tweet js-actionCopyLinkToTweet">
                            <button class="dropdown-link" type="button">
                             Copy link to Tweet
                            </button>
                           </li>
                           <li class="embed-link js-actionEmbedTweet" data-nav="embed_tweet">
                            <button class="dropdown-link" type="button">
                             Embed Tweet
                            </button>
                           </li>
                          </ul>
                         </div>
                        </div>
                       </div>
                      </div>
                      <div class="js-tweet-text-container">
                       <p class="TweetTextSize TweetTextSize--normal js-tweet-text tweet-text" data-aria-label-part="0" lang="en">
                        Sol 2012 (April 04, 2018), Sunny, high -7C/19F, low -74C/-101F, pressure at 7.15 hPa, daylight 05:29-17:22
                       </p>
                      </div>
                      <div class="stream-item-footer">
                       <div class="ProfileTweet-actionCountList u-hiddenVisually">
                        <span class="ProfileTweet-action--reply u-hiddenVisually">
                         <span aria-hidden="true" class="ProfileTweet-actionCount" data-tweet-stat-count="0">
                          <span class="ProfileTweet-actionCountForAria" id="profile-tweet-action-reply-count-aria-982045230638739457">
                           0 replies
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--retweet u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="10">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-retweet-count-aria-982045230638739457">
                           10 retweets
                          </span>
                         </span>
                        </span>
                        <span class="ProfileTweet-action--favorite u-hiddenVisually">
                         <span class="ProfileTweet-actionCount" data-tweet-stat-count="19">
                          <span class="ProfileTweet-actionCountForAria" data-aria-label-part="" id="profile-tweet-action-favorite-count-aria-982045230638739457">
                           19 likes
                          </span>
                         </span>
                        </span>
                       </div>
                       <div aria-label="Tweet actions" class="ProfileTweet-actionList js-actions" role="group">
                        <div class="ProfileTweet-action ProfileTweet-action--reply">
                         <button aria-describedby="profile-tweet-action-reply-count-aria-982045230638739457" class="ProfileTweet-actionButton js-actionButton js-actionReply" data-modal="ProfileTweet-reply" type="button">
                          <div class="IconContainer js-tooltip" title="Reply">
                           <span class="Icon Icon--medium Icon--reply">
                           </span>
                           <span class="u-hiddenVisually">
                            Reply
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount ProfileTweet-actionCount--isZero ">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--retweet js-toggleState js-toggleRt">
                         <button aria-describedby="profile-tweet-action-retweet-count-aria-982045230638739457" class="ProfileTweet-actionButton js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweet
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            10
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo js-actionButton js-actionRetweet" data-modal="ProfileTweet-retweet" type="button">
                          <div class="IconContainer js-tooltip" title="Undo retweet">
                           <span class="Icon Icon--medium Icon--retweet">
                           </span>
                           <span class="u-hiddenVisually">
                            Retweeted
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            10
                           </span>
                          </span>
                         </button>
                        </div>
                        <div class="ProfileTweet-action ProfileTweet-action--favorite js-toggleState">
                         <button aria-describedby="profile-tweet-action-favorite-count-aria-982045230638739457" class="ProfileTweet-actionButton js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Like
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                         <button class="ProfileTweet-actionButtonUndo ProfileTweet-action--unfavorite u-linkClean js-actionButton js-actionFavorite" type="button">
                          <div class="IconContainer js-tooltip" title="Undo like">
                           <span class="Icon Icon--heart Icon--medium" role="presentation">
                           </span>
                           <div class="HeartAnimation">
                           </div>
                           <span class="u-hiddenVisually">
                            Liked
                           </span>
                          </div>
                          <span class="ProfileTweet-actionCount">
                           <span aria-hidden="true" class="ProfileTweet-actionCountForPresentation">
                            19
                           </span>
                          </span>
                         </button>
                        </div>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="dismiss-module">
                     <div class="dismissed-module">
                      <div class="feedback-actions">
                       <div class="feedback-action" data-feedback-type="DontLike" data-feedback-url="">
                        <div class="action-confirmation dismiss-module-item">
                         Thanks. Twitter will use this to make your timeline better.
                         <span class="undo-action">
                          Undo
                         </span>
                        </div>
                       </div>
                      </div>
                      <div class="child-feedback-confirmation">
                       <div class="child-confirmation-item">
                        <span class="child-confirmation-text">
                        </span>
                        <span class="undo-child-feedback-action">
                         Undo
                        </span>
                       </div>
                      </div>
                     </div>
                    </div>
                   </li>
                  </ol>
                  <div class="stream-footer ">
                   <div class="timeline-end has-items has-more-items">
                    <div class="stream-end">
                     <div class="stream-end-inner">
                      <span class="Icon Icon--large Icon--logo">
                      </span>
                      <p class="empty-text">
                       @MarsWxReport hasn't Tweeted yet.
                      </p>
                      <p>
                       <button class="btn-link back-to-top hidden" type="button">
                        Back to top ?
                       </button>
                      </p>
                     </div>
                    </div>
                    <div class="stream-loading">
                     <div class="stream-end-inner">
                      <span class="spinner" title="Loading...">
                      </span>
                     </div>
                    </div>
                   </div>
                  </div>
                  <div class="stream-fail-container">
                   <div class="js-stream-whale-end stream-whale-end stream-placeholder centered-placeholder">
                    <div class="stream-end-inner">
                     <h2 class="title">
                      Loading seems to be taking a while.
                     </h2>
                     <p>
                      Twitter may be over capacity or experiencing a momentary hiccup.
                      <a class="try-again-after-whale" href="#" role="button">
                       Try again
                      </a>
                      or visit
                      <a href="http://status.twitter.com" rel="noopener" target="_blank">
                       Twitter Status
                      </a>
                      for more information.
                     </p>
                    </div>
                   </div>
                  </div>
                  <ol class="hidden-replies-container">
                  </ol>
                 </div>
                </div>
               </div>
              </div>
              <div class="Grid-cell u-size1of3">
               <div class="Grid Grid--withGutter">
                <div class="Grid-cell">
                 <div class="ProfileSidebar ProfileSidebar--withRightAlignment">
                  <div class="MoveableModule">
                   <div class="SidebarCommonModules">
                    <div class="SignupCallOut module js-signup-call-out ">
                     <div class="SignupCallOut-header">
                      <h3 class="SignupCallOut-title u-textBreak">
                       New to Twitter?
                      </h3>
                     </div>
                     <div class="SignupCallOut-subheader">
                      Sign up now to get your own personalized timeline!
                     </div>
                     <div class="signup SignupForm ">
                      <a class="EdgeButton EdgeButton--large EdgeButton--primary SignupForm-submit u-block js-signup " data-component="signup_callout" data-element="form" href="https://twitter.com/signup" role="button">
                       Sign up
                      </a>
                     </div>
                    </div>
                    <div class="RelatedUsers module u-hidden">
                     <div class="RelatedUsers-header">
                      <h3 class="RelatedUsers-title">
                       You may also like
                      </h3>
                      ·
                      <button class="btn-link js-refresh-related-users" type="button">
                       Refresh
                      </button>
                     </div>
                     <div class="RelatedUsers-users">
                     </div>
                    </div>
                    <div class="module Trends trends hidden">
                     <div class="trends-inner">
                      <div class="flex-module trends-container ">
                       <div class="flex-module-header">
                        <h3>
                         <span class="trend-location js-trend-location">
                          false
                         </span>
                        </h3>
                       </div>
                       <div class="flex-module-inner">
                        <ul class="trend-items js-trends">
                        </ul>
                       </div>
                      </div>
                     </div>
                    </div>
                    <div class="Footer module roaming-module Footer--slim Footer--blankBackground">
                     <div class="flex-module">
                      <div class="flex-module-inner js-items-container">
                       <ul class="u-cf">
                        <li class="Footer-item Footer-copyright copyright">
                         © 2018 Twitter
                        </li>
                        <li class="Footer-item">
                         <a class="Footer-link" href="/about" rel="noopener">
                          About
                         </a>
                        </li>
                        <li class="Footer-item">
                         <a class="Footer-link" href="//support.twitter.com" rel="noopener">
                          Help Center
                         </a>
                        </li>
                        <li class="Footer-item">
                         <a class="Footer-link" href="/tos" rel="noopener">
                          Terms
                         </a>
                        </li>
                        <li class="Footer-item">
                         <a class="Footer-link" href="/privacy" rel="noopener">
                          Privacy policy
                         </a>
                        </li>
                        <li class="Footer-item">
                         <a class="Footer-link" href="//support.twitter.com/articles/20170514" rel="noopener">
                          Cookies
                         </a>
                        </li>
                        <li class="Footer-item">
                         <a class="Footer-link" href="//support.twitter.com/articles/20170451" rel="noopener">
                          Ads info
                         </a>
                        </li>
                       </ul>
                      </div>
                     </div>
                    </div>
                   </div>
                  </div>
                 </div>
                </div>
               </div>
              </div>
             </div>
            </div>
           </div>
          </div>
         </div>
         <div class="trends-dialog modal-container" id="trends_dialog">
          <div class="modal draggable">
           <div class="modal-content">
            <button class="modal-btn modal-close js-close" type="button">
             <span class="Icon Icon--close Icon--medium">
              <span class="visuallyhidden">
               Close
              </span>
             </span>
            </button>
            <div class="modal-header">
             <h3 class="modal-title">
              Choose a trend location
             </h3>
            </div>
            <div class="modal-body">
             <div class="trends-dialog-error">
              <p>
              </p>
             </div>
             <div class="trends-wrapper" id="trends_dialog_content">
              <div class="loading">
               <span class="spinner-bigger">
               </span>
              </div>
             </div>
            </div>
           </div>
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="alert-messages hidden" id="message-drawer">
       <div class="message ">
        <div class="message-inside">
         <span class="message-text">
         </span>
         <a class="Icon Icon--close Icon--medium dismiss" href="#" role="button">
          <span class="visuallyhidden">
           Dismiss
          </span>
         </a>
        </div>
       </div>
      </div>
      <div class="gallery-overlay">
      </div>
      <div class="Gallery with-tweet">
       <style class="Gallery-styles">
       </style>
       <div class="Gallery-closeTarget">
       </div>
       <div class="Gallery-content">
        <button class="modal-btn modal-close modal-close-fixed js-close" type="button">
         <span class="Icon Icon--close Icon--large">
          <span class="visuallyhidden">
           Close
          </span>
         </span>
        </button>
        <div class="Gallery-media">
        </div>
        <div class="GalleryNav GalleryNav--prev">
         <span class="GalleryNav-handle GalleryNav-handle--prev">
          <span class="Icon Icon--caretLeft Icon--large">
           <span class="u-hiddenVisually">
            Previous
           </span>
          </span>
         </span>
        </div>
        <div class="GalleryNav GalleryNav--next">
         <span class="GalleryNav-handle GalleryNav-handle--next">
          <span class="Icon Icon--caretRight Icon--large">
           <span class="u-hiddenVisually">
            Next
           </span>
          </span>
         </span>
        </div>
        <div class="GalleryTweet">
        </div>
       </div>
      </div>
      <div class="modal-overlay">
      </div>
      <div id="profile-hover-container">
      </div>
      <div class="modal-container" id="goto-user-dialog">
       <div class="modal modal-small draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Go to a person's profile
          </h3>
         </div>
         <div class="modal-body">
          <div class="modal-inner">
           <form class="t1-form goto-user-form">
            <input aria-label="User" class="input-block username-input" placeholder="Start typing a name to jump to a profile" type="text"/>
            <div class="dropdown-menu typeahead" role="listbox">
             <div aria-hidden="true" class="dropdown-caret">
              <div class="caret-outer">
              </div>
              <div class="caret-inner">
              </div>
             </div>
             <div class="dropdown-inner js-typeahead-results" role="presentation">
              <div class="typeahead-saved-searches" role="presentation">
               <h3 class="typeahead-category-title saved-searches-title" id="saved-searches-heading">
                Saved searches
               </h3>
               <ul class="typeahead-items saved-searches-list" role="presentation">
                <li class="typeahead-item typeahead-saved-search-item" role="presentation">
                 <span aria-hidden="true" class="Icon Icon--close">
                  <span class="visuallyhidden">
                   Remove
                  </span>
                 </span>
                 <a aria-describedby="saved-searches-heading" class="js-nav" data-ds="saved_search" data-query-source="" data-search-query="" href="" role="option" tabindex="-1">
                 </a>
                </li>
               </ul>
              </div>
              <ul class="typeahead-items typeahead-topics" role="presentation">
               <li class="typeahead-item typeahead-topic-item" role="presentation">
                <a class="js-nav" data-ds="topics" data-query-source="typeahead_click" data-search-query="" href="" role="option" tabindex="-1">
                </a>
               </li>
              </ul>
              <ul class="typeahead-items typeahead-accounts social-context js-typeahead-accounts" role="presentation">
               <li class="typeahead-item typeahead-account-item js-selectable" data-remote="true" data-score="" data-user-id="" data-user-screenname="" role="presentation">
                <a class="js-nav" data-ds="account" data-query-source="typeahead_click" data-search-query="" role="option">
                 <div class="js-selectable typeahead-in-conversation hidden">
                  <span class="Icon Icon--follower Icon--small">
                  </span>
                  <span class="typeahead-in-conversation-text">
                   In this conversation
                  </span>
                 </div>
                 <img alt="" class="avatar size32"/>
                 <span class="typeahead-user-item-info account-group">
                  <span class="fullname">
                  </span>
                  <span class="UserBadges">
                   <span class="Icon Icon--verified js-verified hidden">
                    <span class="u-hiddenVisually">
                     Verified account
                    </span>
                   </span>
                   <span class="Icon Icon--protected js-protected hidden">
                    <span class="u-hiddenVisually">
                     Protected Tweets
                    </span>
                   </span>
                  </span>
                  <span class="UserNameBreak">
                  </span>
                  <span class="username u-dir" dir="ltr">
                   @
                   <b>
                   </b>
                  </span>
                 </span>
                 <span class="typeahead-social-context">
                 </span>
                </a>
               </li>
               <li class="js-selectable typeahead-accounts-shortcut js-shortcut" role="presentation">
                <a class="js-nav" data-ds="account_search" data-query-source="typeahead_click" data-search-query="" data-shortcut="true" href="" role="option">
                </a>
               </li>
              </ul>
              <ul class="typeahead-items typeahead-trend-locations-list" role="presentation">
               <li class="typeahead-item typeahead-trend-locations-item" role="presentation">
                <a class="js-nav" data-ds="trend_location" data-search-query="" href="" role="option" tabindex="-1">
                </a>
               </li>
              </ul>
              <div class="typeahead-user-select" role="presentation">
               <div class="typeahead-empty-suggestions" role="presentation">
                Suggested users
               </div>
               <ul class="typeahead-items typeahead-selected js-typeahead-selected" role="presentation">
                <li class="typeahead-item typeahead-selected-item js-selectable" data-remote="true" data-score="" data-user-id="" data-user-screenname="" role="presentation">
                 <a class="js-nav" data-ds="account" data-query-source="typeahead_click" data-search-query="" role="option">
                  <img alt="" class="avatar size32"/>
                  <span class="typeahead-user-item-info account-group">
                   <span class="select-status deselect-user js-deselect-user Icon Icon--check">
                   </span>
                   <span class="select-status select-disabled Icon Icon--unfollow">
                   </span>
                   <span class="fullname">
                   </span>
                   <span class="UserBadges">
                    <span class="Icon Icon--verified js-verified hidden">
                     <span class="u-hiddenVisually">
                      Verified account
                     </span>
                    </span>
                    <span class="Icon Icon--protected js-protected hidden">
                     <span class="u-hiddenVisually">
                      Protected Tweets
                     </span>
                    </span>
                   </span>
                   <span class="UserNameBreak">
                   </span>
                   <span class="username u-dir" dir="ltr">
                    @
                    <b>
                    </b>
                   </span>
                  </span>
                 </a>
                </li>
                <li class="typeahead-selected-end" role="presentation">
                </li>
               </ul>
               <ul class="typeahead-items typeahead-accounts js-typeahead-accounts" role="presentation">
                <li class="typeahead-item typeahead-account-item js-selectable" data-remote="true" data-score="" data-user-id="" data-user-screenname="" role="presentation">
                 <a class="js-nav" data-ds="account" data-query-source="typeahead_click" data-search-query="" role="option">
                  <img alt="" class="avatar size32"/>
                  <span class="typeahead-user-item-info account-group">
                   <span class="select-status deselect-user js-deselect-user Icon Icon--check">
                   </span>
                   <span class="select-status select-disabled Icon Icon--unfollow">
                   </span>
                   <span class="fullname">
                   </span>
                   <span class="UserBadges">
                    <span class="Icon Icon--verified js-verified hidden">
                     <span class="u-hiddenVisually">
                      Verified account
                     </span>
                    </span>
                    <span class="Icon Icon--protected js-protected hidden">
                     <span class="u-hiddenVisually">
                      Protected Tweets
                     </span>
                    </span>
                   </span>
                   <span class="UserNameBreak">
                   </span>
                   <span class="username u-dir" dir="ltr">
                    @
                    <b>
                    </b>
                   </span>
                  </span>
                 </a>
                </li>
                <li class="typeahead-accounts-end" role="presentation">
                </li>
               </ul>
              </div>
              <div class="typeahead-dm-conversations" role="presentation">
               <ul class="typeahead-items typeahead-dm-conversation-items" role="presentation">
                <li class="typeahead-item typeahead-dm-conversation-item" role="presentation">
                 <a role="option" tabindex="-1">
                 </a>
                </li>
               </ul>
              </div>
             </div>
            </div>
           </form>
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="QuickPromoteDialog modal-container" id="quick-promote-dialog">
       <div class="modal draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close modal-close-fixed js-close" type="button">
          <span class="Icon Icon--close Icon--large">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Promote this Tweet
          </h3>
         </div>
         <div class="modal-body">
          <div class="quick-promote-view-container">
           <div class="media">
            <iframe class="quick-promote-iframe js-initial-focus" frameborder="0" scrolling="no" src="">
            </iframe>
           </div>
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="block-user-dialog">
       <div class="modal draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Block
          </h3>
         </div>
         <div class="tweet-loading">
          <div class="spinner-bigger">
          </div>
         </div>
         <div class="modal-body modal-tweet">
         </div>
         <div class="modal-footer">
          <button class="EdgeButton EdgeButton--tertiary cancel-action js-close">
           Cancel
          </button>
          <button class="EdgeButton EdgeButton--danger block-action">
           Block
          </button>
         </div>
        </div>
       </div>
      </div>
      <div id="geo-disabled-dropdown">
       <div tabindex="-1">
        <div class="dropdown-caret">
         <span class="caret-outer">
         </span>
         <span class="caret-inner">
         </span>
        </div>
        <ul>
         <li class="geo-not-enabled-yet">
          <h2>
           Tweet with a location
          </h2>
          <p>
           You can add location information to your Tweets, such as your city or precise location, from the web and via third-party applications. You always have the option to delete your Tweet location history.
           <a href="http://support.twitter.com/forums/26810/entries/78525" rel="noopener" target="_blank">
            Learn more
           </a>
          </p>
          <div>
           <button class="geo-turn-on EdgeButton EdgeButton--primary" type="button">
            Turn on
           </button>
           <button class="geo-not-now EdgeButton EdgeButton--secondary" type="button">
            Not now
           </button>
          </div>
         </li>
        </ul>
       </div>
      </div>
      <div id="geo-enabled-dropdown">
       <div tabindex="-1">
        <div class="dropdown-caret">
         <span class="caret-outer">
         </span>
         <span class="caret-inner">
         </span>
        </div>
        <div>
         <div class="geo-query-location">
          <input autocomplete="off" class="GeoSearch-queryInput" placeholder="Search for a neighborhood or city" type="text"/>
          <span class="Icon Icon--search">
          </span>
         </div>
         <div class="geo-dropdown-status">
         </div>
         <ul class="GeoSearch-dropdownMenu">
         </ul>
        </div>
       </div>
      </div>
      <div class="modal-container" id="list-membership-dialog">
       <div class="modal modal-small draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Your lists
          </h3>
         </div>
         <div class="modal-body">
          <div class="list-membership-content">
          </div>
          <span class="spinner lists-spinner" title="Loading…">
          </span>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="list-operations-dialog">
       <div class="modal modal-medium draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Create a new list
          </h3>
         </div>
         <div class="modal-body">
          <div class="list-editor">
           <div class="field">
            <label class="t1-label" for="list-name">
             List name
            </label>
            <input class="text" id="list-name" name="name" type="text" value=""/>
           </div>
           <hr/>
           <div class="field">
            <label class="t1-label" for="list-description">
             Description
            </label>
            <textarea id="list-description" name="description"></textarea>
            <span class="help-text">
             Under 100 characters, optional
            </span>
           </div>
           <hr/>
           <fieldset class="field">
            <legend class="t1-legend">
             Privacy
            </legend>
            <div class="options">
             <label class="t1-label" for="list-public-radio">
              <input checked="checked" class="radio" id="list-public-radio" name="mode" type="radio" value="public"/>
              <b>
               Public
              </b>
              · Anyone can follow this list
             </label>
             <label class="t1-label" for="list-private-radio">
              <input class="radio" id="list-private-radio" name="mode" type="radio" value="private"/>
              <b>
               Private
              </b>
              · Only you can access this list
             </label>
            </div>
           </fieldset>
           <hr/>
           <div class="list-editor-save">
            <button class="EdgeButton EdgeButton--secondary update-list-button" data-list-id="" type="button">
             Save list
            </button>
           </div>
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="activity-popup-dialog">
       <div class="modal draggable">
        <div class="modal-content clearfix">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
          </h3>
         </div>
         <div class="modal-body">
          <div class="tweet-loading">
           <div class="spinner-bigger">
           </div>
          </div>
          <div class="activity-popup-dialog-content modal-tweet clearfix">
          </div>
          <div class="loading">
           <span class="spinner-bigger">
           </span>
          </div>
          <div class="activity-popup-dialog-users clearfix">
          </div>
          <div class="activity-popup-dialog-footer">
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="copy-link-to-tweet-dialog">
       <div class="modal modal-medium draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Copy link to Tweet
          </h3>
         </div>
         <div class="modal-body">
          <div class="copy-link-to-tweet-container">
           <label class="t1-label">
            <p class="copy-link-to-tweet-instructions">
             Here's the URL for this Tweet. Copy it to easily share with friends.
            </p>
            <textarea class="link-to-tweet-destination js-initial-focus u-dir" dir="ltr" readonly=""></textarea>
           </label>
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="embed-tweet-dialog">
       <div class="modal modal-medium draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title embed-tweet-title">
           Embed this Tweet
          </h3>
          <h3 class="modal-title embed-video-title">
           Embed this Video
          </h3>
         </div>
         <div class="modal-body">
          <div class="embed-code-container">
           <p class="embed-tweet-instructions">
            Add this Tweet to your website by copying the code below.
            <a href="https://dev.twitter.com/web/embedded-tweets" rel="noopener" target="_blank">
             Learn more
            </a>
           </p>
           <p class="embed-video-instructions">
            Add this video to your website by copying the code below.
            <a href="https://dev.twitter.com/web/embedded-tweets" rel="noopener" target="_blank">
             Learn more
            </a>
           </p>
           <form class="t1-form">
            <div class="embed-destination-wrapper">
             <div class="embed-overlay embed-overlay-spinner">
              <div class="embed-overlay-content">
              </div>
             </div>
             <div class="embed-overlay embed-overlay-error">
              <p class="embed-overlay-content">
               Hmm, there was a problem reaching the server.
               <button class="btn-link retry-embed" type="button">
                Try again?
               </button>
              </p>
             </div>
             <textarea class="embed-destination js-initial-focus"></textarea>
             <div class="embed-options">
              <div class="embed-include-parent-tweet">
               <label class="t1-label" for="include-parent-tweet">
                <input checked="" class="include-parent-tweet" id="include-parent-tweet" type="checkbox"/>
                Include parent Tweet
               </label>
              </div>
              <div class="embed-include-card">
               <label class="t1-label" for="include-card">
                <input checked="" class="include-card" id="include-card" type="checkbox"/>
                Include media
               </label>
              </div>
             </div>
            </div>
           </form>
           <p class="embed-tweet-description">
            By embedding Twitter content in your website or app, you are agreeing to the Twitter
            <a href="https://dev.twitter.com/overview/terms/agreement" rel="noopener">
             Developer Agreement
            </a>
            and
            <a href="https://dev.twitter.com/overview/terms/policy" rel="noopener">
             Developer Policy
            </a>
            .
           </p>
           <h3 class="embed-preview-header">
            Preview
           </h3>
           <div class="embed-preview">
           </div>
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container why-this-ad-dialog" id="why-this-ad-dialog">
       <div class="modal modal-large draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title why-this-ad-title">
           Why you're seeing this ad
          </h3>
         </div>
         <div class="why-this-ad-content">
          <div class="why-this-ad-spinner">
           <div class="spinner-bigger">
           </div>
          </div>
          <iframe aria-hidden="true" class="hidden" id="why-this-ad-frame" scrolling="auto">
          </iframe>
         </div>
        </div>
       </div>
      </div>
      <div class="LoginDialog modal-container u-textCenter" id="login-dialog">
       <div class="modal modal-large draggable">
        <div class="LoginDialog-content modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Log in to Twitter
          </h3>
         </div>
         <div class="LoginDialog-body modal-body">
          <div class="LoginDialog-bird">
           <span class="Icon Icon--bird Icon--large">
           </span>
          </div>
          <div class="LoginDialog-form">
           <form action="https://twitter.com/sessions" class="LoginForm js-front-signin" data-component="dialog" data-element="login" method="post">
            <div class="LoginForm-input LoginForm-username">
             <input autocomplete="username" class="text-input email-input js-signin-email" name="session[username_or_email]" placeholder="Phone, email, or username" type="text"/>
            </div>
            <div class="LoginForm-input LoginForm-password">
             <input autocomplete="current-password" class="text-input" name="session[password]" placeholder="Password" type="password"/>
            </div>
            <div class="LoginForm-rememberForgot">
             <label>
              <input checked="checked" name="remember_me" type="checkbox" value="1"/>
              <span>
               Remember me
              </span>
             </label>
             <span class="separator">
              ·
             </span>
             <a class="forgot" href="/account/begin_password_reset" rel="noopener">
              Forgot password?
             </a>
            </div>
            <input class="EdgeButton EdgeButton--primary EdgeButton--medium submit js-submit" type="submit" value="Log in"/>
            <input name="return_to_ssl" type="hidden" value="true"/>
            <input name="scribe_log" type="hidden"/>
            <input name="redirect_after_login" type="hidden" value="/marswxreport?lang=en"/>
            <input name="authenticity_token" type="hidden" value="b79b982cf6601a1f3e594e3d344bc5c307a442ae"/>
            <input autocomplete="off" name="ui_metrics" type="hidden" value='{"rf":{"fedd104b6131ef40af0569335a0cb4c69556f94250f21d0b8c980bfb0e4fbe1e":-64,"afdfc66adcbf938e3e701f4ed3d086495dcd2c4a07f0d1dc0f455e3d52996ca4":-160,"acffd5ed4d04fe961027909b6266b62113e43abcc0d7e46a516f40abf3c79091":0,"ab19693a16e92a84ea8b5878af8a69d65ee4d8c92789b936039d592c3602e54d":-15},"s":"T9Eb6JD31YNDxvcsL2jL2nC6XjW2icobCK_S-nlNV-V3GgCidBs44znxaq7Yjgfw-05NSNH75b_MbrJfCn0oXZtyTcLA9pIedG_H2zWueXRFaVgr2vnJpS1hujrRaPtgp10t49MX2RcDqxDsbbVEuGgymRVsj9XioCUvUQFLevq_aoainJd_gA5VcK7Q9fDxoM_qplCtAvERWlLqL5BhooBXO4rTjdD8z70ZuqlyZ0VAE5CO4a706wV_vkAQqZaLOUOw66NJGgmuku47Im0gd6mQxY3ug42n5uAZmy6DLd7BtLsqbmVDfaB4wHYm9gJt2wVpOvgpLOO95KWQMkq0WwAAAWNNMnR2"}'/>
            <script async="" src="/i/js_inst?c_name=ui_metrics">
            </script>
           </form>
          </div>
         </div>
         <div class="LoginDialog-footer modal-footer u-textCenter">
          Don't have an account?
          <a class="LoginDialog-signupLink" href="https://twitter.com/signup" rel="noopener">
           Sign up »
          </a>
         </div>
        </div>
       </div>
      </div>
      <div class="SignupDialog modal-container u-textCenter" id="signup-dialog">
       <div class="modal modal-large draggable">
        <div class="SignupDialog-content modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Sign up for Twitter
          </h3>
         </div>
         <div class="SignupDialog-body modal-body">
          <div class="SignupDialog-icon">
           <span class="Icon Icon--bird Icon--extraLarge">
           </span>
          </div>
          <h2 class="SignupDialog-heading">
           Not on Twitter? Sign up, tune into the things you care about, and get updates as they happen.
          </h2>
          <div class="SignupDialog-form">
           <div class="signup SignupForm ">
            <a class="EdgeButton EdgeButton--large EdgeButton--primary SignupForm-submit u-block js-signup " data-component="dialog" data-element="signup" href="https://twitter.com/signup" role="button">
             Sign up
            </a>
           </div>
          </div>
         </div>
         <div class="SignupDialog-footer modal-footer u-textCenter">
          Have an account?
          <a class="SignupDialog-signinLink" href="/login" rel="noopener">
           Log in »
          </a>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="sms-codes-dialog">
       <div class="modal modal-medium draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Two-way (sending and receiving) short codes:
          </h3>
         </div>
         <div class="modal-body">
          <table cellpadding="0" cellspacing="0" id="sms_codes">
           <thead>
            <tr>
             <th>
              Country
             </th>
             <th>
              Code
             </th>
             <th>
              For customers of
             </th>
            </tr>
           </thead>
           <tbody>
            <tr>
             <td>
              United States
             </td>
             <td>
              40404
             </td>
             <td>
              (any)
             </td>
            </tr>
            <tr>
             <td>
              Canada
             </td>
             <td>
              21212
             </td>
             <td>
              (any)
             </td>
            </tr>
            <tr>
             <td>
              United Kingdom
             </td>
             <td>
              86444
             </td>
             <td>
              Vodafone, Orange, 3, O2
             </td>
            </tr>
            <tr>
             <td>
              Brazil
             </td>
             <td>
              40404
             </td>
             <td>
              Nextel, TIM
             </td>
            </tr>
            <tr>
             <td>
              Haiti
             </td>
             <td>
              40404
             </td>
             <td>
              Digicel, Voila
             </td>
            </tr>
            <tr>
             <td>
              Ireland
             </td>
             <td>
              51210
             </td>
             <td>
              Vodafone, O2
             </td>
            </tr>
            <tr>
             <td>
              India
             </td>
             <td>
              53000
             </td>
             <td>
              Bharti Airtel, Videocon, Reliance
             </td>
            </tr>
            <tr>
             <td>
              Indonesia
             </td>
             <td>
              89887
             </td>
             <td>
              AXIS, 3, Telkomsel, Indosat, XL Axiata
             </td>
            </tr>
            <tr>
             <td rowspan="2">
              Italy
             </td>
             <td>
              4880804
             </td>
             <td>
              Wind
             </td>
            </tr>
            <tr>
             <td>
              3424486444
             </td>
             <td>
              Vodafone
             </td>
            </tr>
           </tbody>
           <tfoot>
            <tr>
             <td colspan="3">
              »
              <a class="js-initial-focus" href="http://support.twitter.com/articles/14226-how-to-find-your-twitter-short-code-or-long-code" rel="noopener" target="_blank">
               See SMS short codes for other countries
              </a>
             </td>
            </tr>
           </tfoot>
          </table>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="leadgen-confirm-dialog">
       <div class="modal draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close js-close" type="button">
          <span class="Icon Icon--close Icon--medium">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
           Confirmation
          </h3>
         </div>
         <div class="modal-body">
          <div class="leadgen-card-container">
           <div class="media">
            <iframe class="cards2-promotion-iframe" frameborder="0" scrolling="no" src="">
            </iframe>
           </div>
          </div>
          <div class="js-macaw-cards-iframe-container" data-card-name="promotion">
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="AuthWebViewDialog modal-container" id="auth-webview-dialog">
       <div class="modal draggable">
        <div class="modal-content">
         <button class="modal-btn modal-close modal-close-fixed js-close" type="button">
          <span class="Icon Icon--close Icon--large">
           <span class="visuallyhidden">
            Close
           </span>
          </span>
         </button>
         <div class="modal-header">
          <h3 class="modal-title">
          </h3>
         </div>
         <div class="modal-body">
          <div class="auth-webview-view-container">
           <div class="media">
            <iframe class="auth-webview-card-iframe js-initial-focus" frameborder="0" height="500px" scrolling="no" src="" width="590px">
            </iframe>
           </div>
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="promptbird-modal-prompt">
       <div class="modal">
        <button class="modal-btn js-promptDismiss modal-close js-close" type="button">
         <span class="Icon Icon--close Icon--medium">
          <span class="visuallyhidden">
           Close
          </span>
         </span>
        </button>
        <div class="modal-content">
        </div>
       </div>
      </div>
      <div class="modal-container UIWalkthrough" id="ui-walkthrough-dialog">
       <div class="UIWalkthrough-clickBlocker">
       </div>
       <div class="modal modal-small">
        <div class="UIWalkthrough-caret">
        </div>
        <div class="modal-content">
         <div class="modal-body">
          <div class="UIWalkthrough-header">
           <span class="UIWalkthrough-stepProgress">
           </span>
           <button class="UIWalkthrough-skip js-close">
            Skip all
           </button>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--welcome">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--home UIWalkthrough-icon">
            </span>
            Welcome home!
           </h3>
           <p class="UIWalkthrough-message">
            This timeline is where you’ll spend most of your time, getting instant updates about what matters to you.
           </p>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--unfollow">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--smileRating1Fill UIWalkthrough-icon">
            </span>
            Tweets not working for you?
           </h3>
           <p class="UIWalkthrough-message">
            Hover over the profile pic and click the Following button to unfollow any account.
           </p>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--like">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--heart UIWalkthrough-icon">
            </span>
            Say a lot with a little
           </h3>
           <p class="UIWalkthrough-message">
            When you see a Tweet you love, tap the heart — it lets  the person who wrote it know you shared the love.
           </p>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--retweet">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--retweet UIWalkthrough-icon">
            </span>
            Spread the word
           </h3>
           <p class="UIWalkthrough-message">
            The fastest way to share someone else’s Tweet with your followers is with a Retweet. Tap the icon to send it instantly.
           </p>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--reply">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--reply UIWalkthrough-icon">
            </span>
            Join the conversation
           </h3>
           <p class="UIWalkthrough-message">
            Add your thoughts about any Tweet with a Reply. Find a topic you’re passionate about, and jump right in.
           </p>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--trends">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--discover UIWalkthrough-icon">
            </span>
            Learn the latest
           </h3>
           <p class="UIWalkthrough-message">
            Get instant insight into what people are talking about now.
           </p>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--wtf">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--follow UIWalkthrough-icon">
            </span>
            Get more of what you love
           </h3>
           <p class="UIWalkthrough-message">
            Follow more accounts to get instant updates about topics you care about.
           </p>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--search">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--search UIWalkthrough-icon">
            </span>
            Find what's happening
           </h3>
           <p class="UIWalkthrough-message">
            See the latest conversations about any topic instantly.
           </p>
          </div>
          <div class="UIWalkthrough-step UIWalkthrough-step--moments">
           <h3 class="UIWalkthrough-title">
            <span class="Icon Icon--lightning UIWalkthrough-icon">
            </span>
            Never miss a Moment
           </h3>
           <p class="UIWalkthrough-message">
            Catch up instantly on the best stories happening as they unfold.
           </p>
          </div>
         </div>
         <div class="modal-footer">
          <button class="EdgeButton EdgeButton--tertiary u-floatLeft plain-btn UIWalkthrough-button js-previous-step">
           Back
          </button>
          <button class="EdgeButton EdgeButton--secondary UIWalkthrough-button js-next-step js-initial-focus">
           Next
          </button>
         </div>
        </div>
       </div>
      </div>
      <div class="modal-container" id="create-custom-timeline-dialog">
      </div>
      <div class="modal-container" id="edit-custom-timeline-dialog">
      </div>
      <div class="modal-container" id="curate-dialog">
      </div>
      <div class="modal-container" id="media-edit-dialog">
      </div>
      <div class="PermalinkOverlay PermalinkOverlay-with-background " id="permalink-overlay">
       <div class="PermalinkProfile-dismiss modal-close-fixed">
        <span class="Icon Icon--close">
        </span>
       </div>
       <button class="PermalinkOverlay-next PermalinkOverlay-button u-posFixed js-next" type="button">
        <span class="Icon Icon--caretLeft Icon--large">
        </span>
        <span class="u-hiddenVisually">
         Next Tweet from user
        </span>
       </button>
       <div class="PermalinkOverlay-modal">
        <div class="PermalinkOverlay-spinnerContainer u-hidden">
         <div class="PermalinkOverlay-spinner">
         </div>
        </div>
        <div class="PermalinkOverlay-content">
         <div class="PermalinkOverlay-body">
         </div>
        </div>
       </div>
      </div>
      <div class="hidden" id="hidden-content">
       <iframe aria-hidden="true" class="tweet-post-iframe" name="tweet-post-iframe">
       </iframe>
       <iframe aria-hidden="true" class="dm-post-iframe" name="dm-post-iframe">
       </iframe>
      </div>
      <script id="track-ttft-body-script" nonce="">
       if(window.ttft){
        window.ttft.recordMilestone('page', document.getElementById('swift-page-name').getAttribute('content'));
        window.ttft.recordMilestone('section', document.getElementById('swift-section-name').getAttribute('content'));
        window.ttft.recordMilestone('client_record_time', window.ttft.now());
      }
      </script>
      <input class="json-data" id="init-data" type="hidden" value='{"keyboardShortcuts":[{"name":"Actions","description":"Shortcuts for common actions.","shortcuts":[{"keys":["Enter"],"description":"Open Tweet details"},{"keys":["o"],"description":"Expand photo"},{"keys":["\/"],"description":"Search"}]},{"name":"Navigation","description":"Shortcuts for navigating between items in timelines.","shortcuts":[{"keys":["?"],"description":"This menu"},{"keys":["j"],"description":"Next Tweet"},{"keys":["k"],"description":"Previous Tweet"},{"keys":["Space"],"description":"Page down"},{"keys":["."],"description":"Load new Tweets"}]},{"name":"Timelines","description":"Shortcuts for navigating to different timelines or pages.","shortcuts":[{"keys":["g","u"],"description":"Go to user\u2026"}]}],"baseFoucClass":"swift-loading","bodyFoucClassNames":"swift-loading","assetsBasePath":"https:\/\/abs.twimg.com\/a\/1525911434\/","assetVersionKey":"ba93fd","emojiAssetsPath":"https:\/\/abs.twimg.com\/emoji\/v2\/72x72\/","environment":"production","formAuthenticityToken":"b79b982cf6601a1f3e594e3d344bc5c307a442ae","loggedIn":false,"screenName":null,"fullName":null,"userId":null,"guestId":"152600854153603238","createdAt":null,"needsPhoneVerification":false,"allowAdsPersonalization":true,"scribeBufferSize":3,"pageName":"profile","sectionName":"profile","scribeParameters":{},"recaptchaApiUrl":"https:\/\/www.google.com\/recaptcha\/api\/js\/recaptcha_ajax.js","internalReferer":null,"geoEnabled":false,"typeaheadData":{"accounts":{"enabled":true,"localQueriesEnabled":false,"remoteQueriesEnabled":true,"limit":6},"trendLocations":{"enabled":true},"dmConversations":{"enabled":false},"followedSearches":{"enabled":false},"savedSearches":{"enabled":false,"items":[]},"dmAccounts":{"enabled":false,"localQueriesEnabled":false,"remoteQueriesEnabled":false,"onlyDMable":true},"mediaTagAccounts":{"enabled":false,"localQueriesEnabled":false,"remoteQueriesEnabled":false,"onlyShowUsersWithCanMediaTag":false,"currentUserId":-1},"selectedUsers":{"enabled":false},"prefillUsers":{"enabled":false},"topics":{"enabled":true,"localQueriesEnabled":false,"remoteQueriesEnabled":true,"prefetchLimit":500,"limit":4},"concierge":{"enabled":false,"localQueriesEnabled":false,"remoteQueriesEnabled":false,"prefetchLimit":500,"limit":6},"recentSearches":{"enabled":false},"hashtags":{"enabled":false,"localQueriesEnabled":false,"remoteQueriesEnabled":true,"prefetchLimit":500},"useIndexedDB":false,"showSearchAccountSocialContext":false,"showDebugInfo":false,"useThrottle":true,"accountsOnTop":false,"remoteDebounceInterval":300,"remoteThrottleInterval":300,"tweetContextEnabled":false,"fullNameMatchingInCompose":true,"topicsWithFiltersEnabled":false},"shellReferrer":null,"dm":{"notifications":false,"usePushForNotifications":true,"participant_max":50,"welcome_message_add_to_conversation_enabled":true,"poll_options":{"foreground_poll_interval":3000,"burst_poll_interval":3000,"burst_poll_duration":300000,"max_poll_interval":60000},"card_prefetch":true,"card_prefetch_interval_in_seconds":2000,"dm_quick_reply_options_panel_dismiss_in_ms":2000,"open_dm_enabled":false},"autoplayDisabled":false,"pushStatePageLimit":500000,"routes":{"profile":"\/"},"pushState":true,"viewContainer":"#page-container","href":"\/marswxreport?lang=en","searchPathWithQuery":"\/search?q=query&amp;src=typd","composeAltText":false,"night_mode_activated":false,"user_color":null,"deciders":{"gdprAgeGateDialog":false,"gdprSoftBounceDialog":false,"geo_picker_incident_reset":true,"custom_timeline_curation":false,"native_notifications":true,"disable_ajax_datatype_default_to_text":false,"dm_polling_frequency_in_seconds":3000,"dm_granular_mute_controls":true,"enable_media_tag_prefetch":true,"enableMacawNymizerConversionLanding":false,"hqImageUploads":false,"live_pipeline_consume":true,"mqImageUploads":false,"partnerIdSyncEnabled":true,"sruMediaCategory":true,"photoSruGifLimitMb":15,"promoted_logging_force_post":true,"promoted_video_logging_enabled":true,"pushState":true,"emojiNewCategory":false,"contentEditablePlainTextOnly":false,"web_client_api_stats":false,"web_perftown_stats":true,"web_perftown_ttft":false,"web_client_events_ttft":true,"log_push_state_ttft_metrics":true,"web_sru_stats":false,"web_upload_video":true,"web_upload_video_advanced":false,"upload_video_size":500,"useVmapVariants":false,"autoplayPreviewPreroll":true,"moments_home_module":false,"moments_lohp_enabled":true,"enableNativePush":true,"autoSubscribeNativePush":false,"allowWebPushVapidUpgrade":true,"stickersInteractivity":true,"stickersInteractivityDuringLoading":true,"stickersExperience":true,"dynamic_video_ads_include_long_videos":true,"push_state_size":1000,"live_video_media_control_enabled":false,"cards2_enable_periscope_card_transition":true,"use_api_for_retweet_and_unretweet":false,"use_api_for_follow_and_unfollow":true,"edge_probe_enabled":false,"like_over_http_client":true,"enable_inline_location":true,"enable_tweetstorm_creation":true,"enable_tweetstorm_drafts":false,"enable_tweetstorm_tooltip":true,"text_length_for_tweetstorm_tooltip":50,"dm_report_webview_macaw_swift_enabled":true,"page_title_unread_notification_count":false,"page_title_badge_after_unread_tweets":20},"experiments":{},"toasts_dm":false,"toasts_timeline":false,"toasts_dm_poll_scale":60,"defaultNotificationIcon":"https:\/\/abs.twimg.com\/a\/1525911434\/img\/t1\/mobile\/wp7_app_icon.png","promptbirdData":{"promptbirdEnabled":false,"immediateTriggers":["PullToRefresh","Navigate"],"format":"ProfileOther"},"pageContext":"profile","passwordResetAdvancedLoginForm":true,"skipAutoSignupDialog":false,"shouldReplaceSignupWithLogin":false,"hashflagBaseUrl":"https:\/\/abs.twimg.com\/hashflags\/","activeHashflags":{"growtogether":"GrowTogether_v4\/GrowTogether_v4.png","???":"Thanos2018_v3\/Thanos2018_v3.png","nellepieghedeltempo":"megmurray\/megmurray.png","infinitygauntlet":"Thanos2018_v3\/Thanos2018_v3.png","voicetop8":"thevoices14\/thevoices14.png","zee5launch":"zeefive\/zeefive.png","beashinboner":"BeAShinboner\/BeAShinboner.png","jurassicworldfallenkingdom":"Jurassic_World_emoji_v2\/Jurassic_World_emoji_v2.png","bemorepirate":"seaofthieves\/seaofthieves.png","thanos":"Thanos2018_v3\/Thanos2018_v3.png","asianpacificheritagemonth":"AsianHeritageMonth2018\/AsianHeritageMonth2018.png","mymammamia":"MammaMia2_v3\/MammaMia2_v3.png","cabelopantene":"CabeloPanten\/CabeloPanten.png","????_?????":"digitallabsUAE\/digitallabsUAE.png","incrediblesevent":"incredibles2_v5\/incredibles2_v5.png","justask":"AmazonEchoIndiav2\/AmazonEchoIndiav2.png","thefinalscandal":"TGIT_Scandal_2017_v4\/TGIT_Scandal_2017_v4.png","kathnielforvivo":"Kathniel\/Kathniel.png","finalspace":"TBSfinalspace\/TBSfinalspace.png","????":"Interkorea2018\/Interkorea2018.png","sr3mm":"RaeSremmurd2018\/RaeSremmurd2018.png","???":"okoye_blackpanther\/okoye_blackpanther.png","?????????5??":"Klabemoji\/Klabemoji.png","scandal":"TGIT_Scandal_2017_v4\/TGIT_Scandal_2017_v4.png","sejaguerreira":"megmurray\/megmurray.png","theremixshow":"AmazonRemix_v2\/AmazonRemix_v2.png","debatedeldebate":"MXDebates2018\/MXDebates2018.png","debateine":"MXDebates2018\/MXDebates2018.png","heretheycome":"NBA_2017_18_PHI\/NBA_2017_18_PHI.png","frozone":"Frozone\/Frozone.png","???":"StarWarsSolo_Chewie\/StarWarsSolo_Chewie.png","mrswer":"mrswho\/mrswho.png","srh":"IPL_Sunrisers\/IPL_Sunrisers.png","?????":"Ednamode_v2\/Ednamode_v2.png","timesup":"TimesUp_v2\/TimesUp_v2.png","thealienist":"TNT-Alienist\/TNT-Alienist.png","????":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","noonlovesmums":"noon_v3\/noon_v3.png","fearthewalkingdead":"FearTWD\/FearTWD.png","eljettadetuvida":"ElJettaDeTuVida\/ElJettaDeTuVida.png","voiceresults":"thevoices14\/thevoices14.png","??????????":"JapanAzurlane2018_v3\/JapanAzurlane2018_v3.png","tauboladengangoogle":"GoogleIDSoccer\/GoogleIDSoccer.png","zee5meinfeelhai":"zeefive\/zeefive.png","teamlucious":"empire\/empire.png","charlieputh":"CharliePuthAlbum2018_v2\/CharliePuthAlbum2018_v2.png","idolduets":"americanidol2018_v2\/americanidol2018_v2.png","thanosdemandsyoursilence":"Thanos2018_v3\/Thanos2018_v3.png","dirtywater":"redsox2018_v2\/redsox2018_v2.png","flickertourlive":"NiallHoran2018\/NiallHoran2018.png","mntwins":"MinnesotaTwins2018\/MinnesotaTwins2018.png","?????????????":"incredibles2_v5\/incredibles2_v5.png","tgitlife":"TGIT_Popcorn_v3\/TGIT_Popcorn_v3.png","owlmvp":"TmobileOWLMVP\/TmobileOWLMVP.png","dwts":"DWTSAthletes2018_v2\/DWTSAthletes2018_v2.png","yovotoporque":"MexicoCityElections18\/MexicoCityElections18.png","infinitywar":"Thanos2018_v3\/Thanos2018_v3.png","livepunjabiplaypunjabi":"IPL_KingsXIPunjab\/IPL_KingsXIPunjab.png","nammakarnatakafirst":"congressq1\/congressq1.png","gobolts":"NHL_2017_2018_Lightning_v2\/NHL_2017_2018_Lightning_v2.png","lacasadepapel":"LaCasaDePapel\/LaCasaDePapel.png","finalspacetbs":"TBSfinalspace\/TBSfinalspace.png","idolpremiere":"americanidol2018_v2\/americanidol2018_v2.png","weareresourcers":"MarqueemployeurVeolia\/MarqueemployeurVeolia.png","vidastarz":"vidaemoji\/vidaemoji.png","teenmom2":"MTVTeenMom2018\/MTVTeenMom2018.png","voicetop4":"thevoices14\/thevoices14.png","beingserena":"SerenaWilliams2018\/SerenaWilliams2018.png","archie":"RiverdaleS2_2018_v2\/RiverdaleS2_2018_v2.png","juegaméxico":"coronafutbol2018\/coronafutbol2018.png","periscope":"Periscope\/Periscope.png","dancingwiththestars":"DWTSAthletes2018_v2\/DWTSAthletes2018_v2.png","dashparr":"incredibles2_v5\/incredibles2_v5.png","empirepremiere":"empire\/empire.png","gokingsgo":"NHL_2017_2018_LAKings_v2\/NHL_2017_2018_LAKings_v2.png","????tv":"JapanAzurlaneWeather\/JapanAzurlaneWeather.png","chewbacca":"StarWarsSolo_Chewie\/StarWarsSolo_Chewie.png","ifeelprettyfilm":"feelpretty_v2\/feelpretty_v2.png","jbfa":"JamesBeardAwards2018\/JamesBeardAwards2018.png","eurovision":"Eurovision2018Main\/Eurovision2018Main.png","violetaparr":"incredibles2_v5\/incredibles2_v5.png","voicenotes":"CharliePuthAlbum2018_v2\/CharliePuthAlbum2018_v2.png","britainsgottalent2018":"BGT2018\/BGT2018.png","bestoftweets":"BestofTweets2018\/BestofTweets2018.png","nialllive":"NiallHoran2018\/NiallHoran2018.png","animalifantastici":"fantasticbeasts_v2\/fantasticbeasts_v2.png","jackjackparr":"JackJack\/JackJack.png","animauxfantastiques":"fantasticbeasts_v2\/fantasticbeasts_v2.png","killmonger":"killmonger_blackpanther\/killmonger_blackpanther.png","rolltide":"Alabama_CFBPlayoff_Teamv3\/Alabama_CFBPlayoff_Teamv3.png","???_???_????":"HeroNextToHero\/HeroNextToHero.png","lovetwitter":"LoveTwitter\/LoveTwitter.png","mrtvatisina":"aqp2018_v3\/aqp2018_v3.png","????????????2":"incredibles2_v5\/incredibles2_v5.png","detroitbasketball":"NBA_2017_18_DET\/NBA_2017_18_DET.png","scotiarewardsyou":"scotiabankswish\/scotiabankswish.png","rootedinoakland":"OaklandAthletics2018\/OaklandAthletics2018.png","texasrangers":"TexasRangers2018\/TexasRangers2018.png","volvooceanrace":"VolvoOceanRace\/VolvoOceanRace.png","????=????":"JackJack\/JackJack.png","teenmom":"MTVTeenMom2018\/MTVTeenMom2018.png","megmurry":"megmurray\/megmurray.png","mammamia":"MammaMia2_v3\/MammaMia2_v3.png","cbj":"NHL_2017_2018_BlueJackets_v2\/NHL_2017_2018_BlueJackets_v2.png","aapi":"AsianHeritageMonth2018\/AsianHeritageMonth2018.png","piensoyvoto":"MXvoterengagement2018\/MXvoterengagement2018.png","harryandmeghan":"royalwedding2018\/royalwedding2018.png","?????2":"incredibles2_v5\/incredibles2_v5.png","espejopublico":"EspejoPublico_2017_2018\/EspejoPublico_2017_2018.png","losincreíbles2":"incredibles2_v5\/incredibles2_v5.png","idolfinale":"americanidol2018_v2\/americanidol2018_v2.png","nowwerise":"NHL_2017_2018_NJDevils_v2\/NHL_2017_2018_NJDevils_v2.png","amazonecho":"AmazonEchoIndiav2\/AmazonEchoIndiav2.png","chewie":"StarWarsSolo_Chewie\/StarWarsSolo_Chewie.png","stanleycup":"StanleyCup2018\/StanleyCup2018.png","soloastarwarsstory":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","nba":"NBA_2017_18_NBA\/NBA_2017_18_NBA.png","rockies25th":"ColoradoRockies2018\/ColoradoRockies2018.png","kkrhaitaiyaar":"IPL_Kolkata\/IPL_Kolkata.png","nocapes":"Ednamode_v2\/Ednamode_v2.png","billions":"billions-showtime\/billions-showtime.png","bethechange":"BeTheChange_v2\/BeTheChange_v2.png","?????":"StarWarsSolo_Lando\/StarWarsSolo_Lando.png","idolonabc":"americanidol2018_v2\/americanidol2018_v2.png","canadiandream":"ChevroletCanadianDream2018\/ChevroletCanadianDream2018.png","followtheball":"waltdisneyoscars2018\/waltdisneyoscars2018.png","valla":"FranceBlizzardOWL_LAValiant\/FranceBlizzardOWL_LAValiant.png","?????":"nakia_blackpanther\/nakia_blackpanther.png","teamaxe":"billions-showtime\/billions-showtime.png","unpliegueeneltiempo":"megmurray\/megmurray.png","hollywoodweek":"americanidol2018_v2\/americanidol2018_v2.png","statebankofindia":"SBIBank_v3\/SBIBank_v3.png","?????????":"mrswho\/mrswho.png","movietvawards":"MTVMovieAwards2018\/MTVMovieAwards2018.png","??????":"incredibles2_v5\/incredibles2_v5.png","shieldsup":"FranceBlizzardOWL_LAGladiators\/FranceBlizzardOWL_LAGladiators.png","empirewednesday":"empire\/empire.png","lafamaviveenti":"movistar\/movistar.png","millenniumfalcon":"StarWarsSolo_Chewie\/StarWarsSolo_Chewie.png","????":"MothersDay2018\/MothersDay2018.png","senhorincrível":"MrIncredible\/MrIncredible.png","eleccionescolombia":"colombianelection2018\/colombianelection2018.png","elastigirl":"MrsIncredible\/MrsIncredible.png","infinitystones":"Thanos2018_v3\/Thanos2018_v3.png","goavsgo":"NHL_2017_2018_COAvalanche_v2\/NHL_2017_2018_COAvalanche_v2.png","wannasprite":"q2spriteemoji\/q2spriteemoji.png","labarramáspower":"Entel_Mundial_Peru\/Entel_Mundial_Peru.png","mcdbreakfast":"mcdonaldsmcgriddle\/mcdonaldsmcgriddle.png","7afl":"AFL2018\/AFL2018.png","???????":"japanfanta\/japanfanta.png","????":"japanfanta\/japanfanta.png","amtodmbfn":"BuzzFeedMorning_v3\/BuzzFeedMorning_v3.png","produitsbio":"FranceFleuryMichon\/FranceFleuryMichon.png","torcidan1":"brahma\/brahma.png","sxswestworld":"Westworld2MidSeason\/Westworld2MidSeason.png","????":"mbaku_v2\/mbaku_v2.png","asksweetbitter":"STARZSweetbitter18\/STARZSweetbitter18.png","mutuaopen":"MutuaMadridOpen\/MutuaMadridOpen.png","mammamia2movie":"MammaMia2_v3\/MammaMia2_v3.png","voiceplayoffs":"thevoices14\/thevoices14.png","juntosmiami":"MiamiMarlins2018\/MiamiMarlins2018.png","????":"okoye_blackpanther\/okoye_blackpanther.png","myxmusicawards2018":"MYXMusicAwards2018\/MYXMusicAwards2018.png","pegote":"GrefusaPipas_v2\/GrefusaPipas_v2.png","ekstracashback":"TokopediaRamadan2018_v2\/TokopediaRamadan2018_v2.png","toystoryland":"waltdisneyoscars2018\/waltdisneyoscars2018.png","onthebus":"NRLTigers2018\/NRLTigers2018.png","??????":"MothersDay2018\/MothersDay2018.png","fallenkingdom":"Jurassic_World_emoji_v2\/Jurassic_World_emoji_v2.png","letsgobucs":"PittsburghPirates2018\/PittsburghPirates2018.png","??????????":"incredibles2_v5\/incredibles2_v5.png","seaofthieves":"seaofthieves\/seaofthieves.png","ittakeseverything":"NBA_2017_18_LAC\/NBA_2017_18_LAC.png","mammamiaherewegoagain":"MammaMia2_v3\/MammaMia2_v3.png","gliincredibili2":"incredibles2_v5\/incredibles2_v5.png","voicebattles":"thevoices14\/thevoices14.png","powerglide":"RaeSremmurd2018\/RaeSremmurd2018.png","amtodm":"BuzzFeedMorning_v3\/BuzzFeedMorning_v3.png","maythefourth":"StarWarsSolo_Chewie\/StarWarsSolo_Chewie.png","qira":"StarWarsSolo_Qira\/StarWarsSolo_Qira.png","estesíesdebate":"MXcitydebate2018\/MXcitydebate2018.png","doitbigger":"NBAPelicans2018\/NBAPelicans2018.png","?????":"Thanos2018_v3\/Thanos2018_v3.png","aquietplacethailand":"aqp2018_v3\/aqp2018_v3.png","scandalfinale":"TGIT_Scandal_2017_v4\/TGIT_Scandal_2017_v4.png","iamopl":"iamopl_v2\/iamopl_v2.png","shocktheworld":"FranceBlizzardOWL_SanFrancisco\/FranceBlizzardOWL_SanFrancisco.png","signoraquale":"mrswhich\/mrswhich.png","vidafinale":"vidaemoji\/vidaemoji.png","blackpantherlive":"blackpanther_live_v5\/blackpanther_live_v5.png","fearthedeer":"NBA_2017_18_MIL\/NBA_2017_18_MIL.png","am2dmbf":"BuzzFeedMorning_v3\/BuzzFeedMorning_v3.png","thevoiceau":"TheVoiceAU2018\/TheVoiceAU2018.png","mrincreíble":"MrIncredible\/MrIncredible.png","jackwhite":"Jackwhite_v2\/Jackwhite_v2.png","vibranium":"blackpanther_live_v5\/blackpanther_live_v5.png","stayquiet":"aqp2018_v3\/aqp2018_v3.png","rêvecanadien":"ChevroletCanadianDream2018\/ChevroletCanadianDream2018.png","???????":"incredibles2_v5\/incredibles2_v5.png","hansolo":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","?????":"JapanAzurlane2018_v4\/JapanAzurlane2018_v4.png","tictocnews":"bloombergtictoc2018\/bloombergtictoc2018.png","violetparr":"incredibles2_v5\/incredibles2_v5.png","ramadanekstra":"TokopediaRamadan2018_v2\/TokopediaRamadan2018_v2.png","?????":"GatsbyDeo2018\/GatsbyDeo2018.png","sharkteam":"Sharkteam\/Sharkteam.png","mbaku":"mbaku_v2\/mbaku_v2.png","fièrementpoulet":"ChickenPeople2018\/ChickenPeople2018.png","alômãe":"BrazilWorldCup2018_AloMae_v2\/BrazilWorldCup2018_AloMae_v2.png","royalwedding":"royalwedding2018\/royalwedding2018.png","jurassic":"Jurassic_World_emoji_v2\/Jurassic_World_emoji_v2.png","beardawards":"JamesBeardAwards2018\/JamesBeardAwards2018.png","supertroopers":"SuperTroopers2\/SuperTroopers2.png","jabaritribe":"mbaku_v2\/mbaku_v2.png","violettaparr":"incredibles2_v5\/incredibles2_v5.png","piedpiper":"SiliconValleyHBO2018\/SiliconValleyHBO2018.png","premiosmtvmiaw":"MTVMiawAwardsBR2018\/MTVMiawAwardsBR2018.png","señoraqué":"mrswhatsit\/mrswhatsit.png","theremixamazon":"AmazonRemix_v2\/AmazonRemix_v2.png","aquietplace":"aqp2018_v3\/aqp2018_v3.png","incrediblesday":"incredibles2_v5\/incredibles2_v5.png","knicks":"NBA_2017_18_NYK\/NBA_2017_18_NYK.png","kohlscash":"kohlscash2018_v2\/kohlscash2018_v2.png","????????????":"mrswhich\/mrswhich.png","123cuéntalo":"GrefusaPipas_v2\/GrefusaPipas_v2.png","???????1??":"catemoji_v2\/catemoji_v2.png","chaostakescontrol":"westworldpremiere2018\/westworldpremiere2018.png","cesar":"cesar2018\/cesar2018.png","?????????":"JapanAzurlaneWeather\/JapanAzurlaneWeather.png","fantasticbeasts":"fantasticbeasts_v2\/fantasticbeasts_v2.png","bluejays":"TorontoBlueJays2018_v3\/TorontoBlueJays2018_v3.png","??????_????":"SAIB\/SAIB.png","????":"shuri_blackpanther\/shuri_blackpanther.png","????????":"IPL_Rajasthan\/IPL_Rajasthan.png","mammamiafilm":"MammaMia2_v3\/MammaMia2_v3.png","iaytsa":"tecatemundial_v2\/tecatemundial_v2.png","sansunbruit":"aqp2018_v3\/aqp2018_v3.png","siliconhbo":"SiliconValleyHBO2018\/SiliconValleyHBO2018.png","riverdalecw":"RiverdaleS2_2018_v2\/RiverdaleS2_2018_v2.png","doitbig":"NBA_2017_18_NOP\/NBA_2017_18_NOP.png","??????????":"killmonger_blackpanther\/killmonger_blackpanther.png","prixbestoftweets":"BestofTweets2018\/BestofTweets2018.png","?????_?????_??????":"SaudiEnergy\/SaudiEnergy.png","karnatakaelections2018":"KarnatakaStateElections2018\/KarnatakaStateElections2018.png","????????????":"japanfanta\/japanfanta.png","maythefourthbewithyou":"StarWarsSolo_Chewie\/StarWarsSolo_Chewie.png","debatechilango":"MXcitydebate2018\/MXcitydebate2018.png","landocalrissian":"StarWarsSolo_Lando\/StarWarsSolo_Lando.png","finaisnbb":"NBBFinais2018\/NBBFinais2018.png","??????????5??":"LoveLiveKlab2018\/LoveLiveKlab2018.png","empirefox":"empire\/empire.png","redv":"NRLRedV2018\/NRLRedV2018.png","sweetbittertv":"STARZSweetbitter18\/STARZSweetbitter18.png","rallytogether":"Cleveland2018\/Cleveland2018.png","??????????????2018":"KarnatakaStateElections2018\/KarnatakaStateElections2018.png","westworld":"Westworld2MidSeason\/Westworld2MidSeason.png","navakarnataka2025":"congressq1\/congressq1.png","starwarsday":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","buzzcity":"NBA_2017_18_CHA\/NBA_2017_18_CHA.png","mrindestructible":"MrIncredible\/MrIncredible.png","apnibhashameinfeelhai":"zeefive\/zeefive.png","bostonup":"FranceBlizzardOWL_Boston\/FranceBlizzardOWL_Boston.png","everybodyin":"ChicagoCubs2018\/ChicagoCubs2018.png","snowapp":"snowcorp\/snowcorp.png","apahm":"AsianHeritageMonth2018\/AsianHeritageMonth2018.png","bestoftweetsawards":"BestofTweets2018\/BestofTweets2018.png","golalazo":"Golalazo2018\/Golalazo2018.png","solopasaconpipasg":"GrefusaPipas_v2\/GrefusaPipas_v2.png","rockets":"NBA_2017_18_HOU\/NBA_2017_18_HOU.png","myincrediblesreview":"incredibles2_v5\/incredibles2_v5.png","bgt2018":"BGT2018\/BGT2018.png","?????":"Frozone\/Frozone.png","jurassicpark":"Jurassic_World_emoji_v2\/Jurassic_World_emoji_v2.png","??????????????":"KarnatakaStateElections2018\/KarnatakaStateElections2018.png","greysanatomyfinale":"TGIT_Meredith_2017_v7\/TGIT_Meredith_2017_v7.png","pipasgdegrefusa":"GrefusaPipas_v2\/GrefusaPipas_v2.png","dodgers":"LADodgers2018\/LADodgers2018.png","faisonsgrandirlebio":"FranceFleuryMichon\/FranceFleuryMichon.png","wpgwhiteout":"NHL_2017_2018_Jets_v2\/NHL_2017_2018_Jets_v2.png","aquietplaceinmy":"aqp2018_v3\/aqp2018_v3.png","violetteparr":"incredibles2_v5\/incredibles2_v5.png","grefusa":"GrefusaPipas_v2\/GrefusaPipas_v2.png","onepursuit":"WashingtonNationals2018\/WashingtonNationals2018.png","wearegeelong":"WeAreGeelong_v2\/WeAreGeelong_v2.png","proudibmer":"IBMThink2018_v2\/IBMThink2018_v2.png","jackwhitelive":"Jackwhite_v2\/Jackwhite_v2.png","mmopen18":"MutuaMadridOpen\/MutuaMadridOpen.png","gladiatorsout":"TGIT_Scandal_2017_v4\/TGIT_Scandal_2017_v4.png","greysanatomy":"TGIT_Meredith_2017_v7\/TGIT_Meredith_2017_v7.png","thewayiam":"CharliePuthAlbum2018_v2\/CharliePuthAlbum2018_v2.png","wethenorth":"NBA_2017_18_TOR\/NBA_2017_18_TOR.png","sbinews":"SBIBank_v3\/SBIBank_v3.png","findlucious":"empire\/empire.png","senhoraqual":"mrswhich\/mrswhich.png","lafamaviveenmi":"movistar\/movistar.png","rednose":"RedNoseDay2018\/RedNoseDay2018.png","sejaguerreiro":"megmurray\/megmurray.png","happymammasday":"MammaMia2_v3\/MammaMia2_v3.png","noseson":"RedNoseDay2018\/RedNoseDay2018.png","mammamiamovie":"MammaMia2_v3\/MammaMia2_v3.png","halamadrid":"realmadrid\/realmadrid.png","?????":"Vimto2018\/Vimto2018.png","gorabbitohs":"NRLsouths2018\/NRLsouths2018.png","gospursgo":"NBA_2017_18_SAS\/NBA_2017_18_SAS.png","?????????":"IPL_Delhi\/IPL_Delhi.png","???????":"StarWarsSolo_Chewie\/StarWarsSolo_Chewie.png","thenextidol":"americanidol2018_v2\/americanidol2018_v2.png","dubnation":"NBA_2017_18_GSW\/NBA_2017_18_GSW.png","??????_????":"SAIB\/SAIB.png","starwars":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","raesremmurd":"RaeSremmurd2018\/RaeSremmurd2018.png","panteranegra":"blackpanther_live_v5\/blackpanther_live_v5.png","takenote":"NBA_2017_18_UTA\/NBA_2017_18_UTA.png","generationdbacks":"ArizonaDBacks_v2\/ArizonaDBacks_v2.png","niallhoranlive":"NiallHoran2018\/NiallHoran2018.png","sweetbitterstarz":"STARZSweetbitter18\/STARZSweetbitter18.png","ifeelprettymovie":"feelpretty_v2\/feelpretty_v2.png","unviajeeneltiempo":"megmurray\/megmurray.png","crédito10millones":"CumbreInfonavit2018_v3\/CumbreInfonavit2018_v3.png","madamequi":"mrswho\/mrswho.png","????":"StarWarsSolo_Qira\/StarWarsSolo_Qira.png","??????":"ShowMeTheGift2018_v2\/ShowMeTheGift2018_v2.png","juntossomos10":"MastercardSoccer\/MastercardSoccer.png","juegamexico":"coronafutbol2018\/coronafutbol2018.png","afl":"AFL18\/AFL18.png","??????":"StarWarsSolo_Chewie\/StarWarsSolo_Chewie.png","pdomjnate":"FranceBlizzardOWL_Philadelphia\/FranceBlizzardOWL_Philadelphia.png","greysfinale":"TGIT_Meredith_2017_v7\/TGIT_Meredith_2017_v7.png","blackpanther":"blackpanther_live_v5\/blackpanther_live_v5.png","riverdale":"RiverdaleS2_2018_v2\/RiverdaleS2_2018_v2.png","thedynastybegins":"FranceBlizzardOWL_Seoul\/FranceBlizzardOWL_Seoul.png","sraqué":"mrswhatsit\/mrswhatsit.png","hiljainenpaikka":"aqp2018_v3\/aqp2018_v3.png","zezé":"JackJack\/JackJack.png","ifeelpretty":"feelpretty_v2\/feelpretty_v2.png","nowruz":"nowruz2018_v4\/nowruz2018_v4.png","vidalia":"vidaemoji\/vidaemoji.png","cgb41":"AsahiGroupFoods\/AsahiGroupFoods.png","pacers":"NBA_2017_18_IND\/NBA_2017_18_IND.png","????????":"blackpanther_live_v5\/blackpanther_live_v5.png","mexicanelection":"mexicanpresidentialelection2018\/mexicanpresidentialelection2018.png","??????_????":"SAIB\/SAIB.png","????":"ImagscgStage2018\/ImagscgStage2018.png","thisismycrew":"MilwaukeeBrewers2018\/MilwaukeeBrewers2018.png","umadobranotempo":"megmurray\/megmurray.png","???":"Frozone\/Frozone.png","whateverittakes":"NBA_2017_18_CLE_v2\/NBA_2017_18_CLE_v2.png","unraccourcidansletemps":"megmurray\/megmurray.png","askvida":"vidaemoji\/vidaemoji.png","???????????":"japanfanta\/japanfanta.png","solostarwars":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","mytwitteranniversary":"MyTwitterAnniversary\/MyTwitterAnniversary.png","askalexa":"AmazonEchoIndiav2\/AmazonEchoIndiav2.png","thrunthru":"NRLtitans2018\/NRLtitans2018.png","statebank":"SBIBank_v3\/SBIBank_v3.png","daszeiträtsel":"megmurray\/megmurray.png","infonavitonu":"CumbreInfonavit2018_v3\/CumbreInfonavit2018_v3.png","eleccionchilanga":"MexicoCityElections18\/MexicoCityElections18.png","ogprofilepic":"lastOG_v2\/lastOG_v2.png","nbbnotwitter":"Emoji_NBB_2017_2018\/Emoji_NBB_2017_2018.png","forvida":"vidaemoji\/vidaemoji.png","??????????":"IPL_Kolkata\/IPL_Kolkata.png","karnatakaelections":"KarnatakaStateElections2018\/KarnatakaStateElections2018.png","marvelfansunited":"Thanos2018_v3\/Thanos2018_v3.png","yaytza":"tecatemundial_v2\/tecatemundial_v2.png","cheddarlive":"Cheddar_Emoji_v4\/Cheddar_Emoji_v4.png","tapegao":"GrefusaPipas_v2\/GrefusaPipas_v2.png","12points":"Eurovision2018\/Eurovision2018.png","????":"Frozone\/Frozone.png","swaelee":"RaeSremmurd2018\/RaeSremmurd2018.png","???":"Ednamode_v2\/Ednamode_v2.png","mooncake":"TBSfinalspace\/TBSfinalspace.png","mnwild":"NHL_2017_2018_MNwild_v2\/NHL_2017_2018_MNwild_v2.png","turtlerat":"capitolonemarchmadness\/capitolonemarchmadness.png","letsmarchnova":"VillanovaYearLong\/VillanovaYearLong.png","roseanneonabc":"ABCRoseanneV2\/ABCRoseanneV2.png","????":"Interkorea2018\/Interkorea2018.png","think18":"IBMThink2018_v2\/IBMThink2018_v2.png","alomae":"BrazilWorldCup2018_AloMae_v2\/BrazilWorldCup2018_AloMae_v2.png","soisuneguerriere":"megmurray\/megmurray.png","?????":"mbaku_v2\/mbaku_v2.png","haloson":"haloson\/haloson.png","letsgoducks":"NHL_2017_2018_Ducks_v2\/NHL_2017_2018_Ducks_v2.png","choosechicken":"ChickenPeople2018\/ChickenPeople2018.png","???????":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","realmadrid":"realmadrid\/realmadrid.png","decision2018":"KarnatakaStateElections2018\/KarnatakaStateElections2018.png","hansolostarwars":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","mumbaiindians":"IPL_MumbaiIndians_v2\/IPL_MumbaiIndians_v2.png","?????????":"StarWarsSolo_Lando\/StarWarsSolo_Lando.png","whitetina":"vidaemoji\/vidaemoji.png","empireseason4":"empire\/empire.png","douzepoints":"Eurovision2018\/Eurovision2018.png","vivoxkathniel":"Kathniel\/Kathniel.png","dirtyfrida":"vidaemoji\/vidaemoji.png","????????":"JackJack\/JackJack.png","americanidol":"americanidol2018_v2\/americanidol2018_v2.png","noonwomen":"noon_v3\/noon_v3.png","tvoshortdoc":"TVOShortDocs\/TVOShortDocs.png","??????":"killmonger_blackpanther\/killmonger_blackpanther.png","weflyasone":"weflyasone_v2\/weflyasone_v2.png","greysabc":"TGIT_Meredith_2017_v7\/TGIT_Meredith_2017_v7.png","allforone":"NBA_2017_18_CLE\/NBA_2017_18_CLE.png","flyeaglesfly":"Eaglesv4\/Eaglesv4.png","violetapêra":"incredibles2_v5\/incredibles2_v5.png","???_??????":"noon_v3\/noon_v3.png","tchalla":"blackpanther_live_v5\/blackpanther_live_v5.png","umlugarsilencioso":"aqp2018_v3\/aqp2018_v3.png","ftwd":"FearTWD\/FearTWD.png","??":"JackJack\/JackJack.png","vungdatcamlang":"aqp2018_v3\/aqp2018_v3.png","????????":"MrIncredible\/MrIncredible.png","infonavit":"CumbreInfonavit2018_v3\/CumbreInfonavit2018_v3.png","alienisttnt":"TNT-Alienist\/TNT-Alienist.png","myogprofilepic":"lastOG_v2\/lastOG_v2.png","????????":"MrsIncredible\/MrsIncredible.png","lallavedelmundial":"ClaroCAM\/ClaroCAM.png","westworldhbo":"Westworld2MidSeason\/Westworld2MidSeason.png","mangerbio":"FranceFleuryMichon\/FranceFleuryMichon.png","karnatakaelection2018":"KarnatakaStateElections2018\/KarnatakaStateElections2018.png","mcdonaldsmorning":"mcdonaldsmcgriddle\/mcdonaldsmcgriddle.png","netneutrality":"Net_Emoji_v3\/Net_Emoji_v3.png","battleswon":"USMC2018_V2\/USMC2018_V2.png","thealienisttnt":"TNT-Alienist\/TNT-Alienist.png","yonobysbi":"SBIBank_v3\/SBIBank_v3.png","asianamericanpacificislanderheritagemonth":"AsianHeritageMonth2018\/AsianHeritageMonth2018.png","breakfastatmcdonalds":"mcdonaldsmcgriddle\/mcdonaldsmcgriddle.png","??":"cocacolaAyataka\/cocacolaAyataka.png","amtodmbf":"BuzzFeedMorning_v3\/BuzzFeedMorning_v3.png","orangearmy":"IPL_Sunrisers\/IPL_Sunrisers.png","llavemundialista":"ClaroCAM\/ClaroCAM.png","yaytsa":"tecatemundial_v2\/tecatemundial_v2.png","popbuzzpresents":"PopbuzzPresents_Emoji\/PopbuzzPresents_Emoji.png","internetpower":"Entel_Mundial_Peru\/Entel_Mundial_Peru.png","mtvmiaw18":"MTVMiawAwardsBR2018\/MTVMiawAwardsBR2018.png","hallabol":"IPL_Rajasthan\/IPL_Rajasthan.png","supertroopers420":"SuperTroopers2\/SuperTroopers2.png","???????":"aqp2018_v3\/aqp2018_v3.png","????????????":"megmurray\/megmurray.png","zee5":"zeefive\/zeefive.png","whitehot":"NBAHeat2018\/NBAHeat2018.png","cichemiejsce":"aqp2018_v3\/aqp2018_v3.png","?????????????":"blackpanther_live_v5\/blackpanther_live_v5.png","osincríveis2":"incredibles2_v5\/incredibles2_v5.png","??????????":"cocacolaAyataka\/cocacolaAyataka.png","voiceblinds":"thevoices14\/thevoices14.png","sacramentoproud":"NBA_2017_18_SAC\/NBA_2017_18_SAC.png","thunderup":"NBA_2017_18_OKC\/NBA_2017_18_OKC.png","signoracose":"mrswhatsit\/mrswhatsit.png","nbatwitter":"NBATwitter_Emoji___v4\/NBATwitter_Emoji___v4.png","pipasg":"GrefusaPipas_v2\/GrefusaPipas_v2.png","gelado":"Frozone\/Frozone.png","???????":"JapanAzurlane2018_v4\/JapanAzurlane2018_v4.png","station19":"station19\/station19.png","upupcronulla":"NRLsharks2018\/NRLsharks2018.png","f4glory":"Euroleague_2018_v2\/Euroleague_2018_v2.png","dcfamily":"NBA_2017_18_WAS\/NBA_2017_18_WAS.png","?????":"SaudiEnergy\/SaudiEnergy.png","bebold":"PhiladelphiaPhillies2018\/PhiladelphiaPhillies2018.png","tvoshortdocs":"TVOShortDocs\/TVOShortDocs.png","???_????_????":"noon_v3\/noon_v3.png","??????????":"megmurray\/megmurray.png","unexpectmore":"unexpectmore\/unexpectmore.png","whistlepodu":"IPL_Chennai\/IPL_Chennai.png","billionspremiere":"billions-showtime\/billions-showtime.png","prixbestoftweet":"BestofTweets2018\/BestofTweets2018.png","mothersday":"MothersDay2018\/MothersDay2018.png","flashparr":"incredibles2_v5\/incredibles2_v5.png","lacasadicarta":"LaCasaDePapel\/LaCasaDePapel.png","sessizbiryer":"aqp2018_v3\/aqp2018_v3.png","celtics":"NBA_2017_18_BOS\/NBA_2017_18_BOS.png","twdxfeartwd":"FearTWD\/FearTWD.png","hausdesgeldes":"LaCasaDePapel\/LaCasaDePapel.png","????_???_???":"HeroNextToHero_v2\/HeroNextToHero_v2.png","echoindia":"AmazonEchoIndiav2\/AmazonEchoIndiav2.png","jamesbeard":"JamesBeardAwards2018\/JamesBeardAwards2018.png","philaunite":"NBASixers2018\/NBASixers2018.png","standwithus":"NHL_2017_2018_Preds_v2\/NHL_2017_2018_Preds_v2.png","ekstraflashsale":"TokopediaRamadan2018_v2\/TokopediaRamadan2018_v2.png","votamexico":"mexicanpresidentialelection2018\/mexicanpresidentialelection2018.png","olanrogers":"TBSfinalspace\/TBSfinalspace.png","sraquién":"mrswho\/mrswho.png","billionsfinale":"billions-showtime\/billions-showtime.png","pilasconelvoto":"colombianelection2018\/colombianelection2018.png","bobparr":"MrIncredible\/MrIncredible.png","ogtracy":"ogtracy\/ogtracy.png","begiant":"GWSGIANTS\/GWSGIANTS.png","???":"Thanos2018_v3\/Thanos2018_v3.png","sweetbitter":"STARZSweetbitter18\/STARZSweetbitter18.png","melbourneproud":"NRLmelbourne2018\/NRLmelbourne2018.png","siberius":"Frozone\/Frozone.png","mtvawards":"MTVMovieAwards2018\/MTVMovieAwards2018.png","inc4karnataka":"congressq1\/congressq1.png","mrswho":"mrswho\/mrswho.png","mtvmiaw2018":"MTVMiawAwardsBR2018\/MTVMiawAwardsBR2018.png","cumbreinfonavit2018":"CumbreInfonavit2018_v3\/CumbreInfonavit2018_v3.png","mffl":"NBA_2017_18_DAL\/NBA_2017_18_DAL.png","tasuave":"GrefusaPipas_v2\/GrefusaPipas_v2.png","sweetbitterpremiere":"STARZSweetbitter18\/STARZSweetbitter18.png","vidapremiere":"vidaemoji\/vidaemoji.png","freshevents":"freshevents2018Q2\/freshevents2018Q2.png","lamamámáspower":"Entel_Mundial_Peru\/Entel_Mundial_Peru.png","wakandaweekend":"BlackPantherHomeEnt2018\/BlackPantherHomeEnt2018.png","lesindestructibles2":"incredibles2_v5\/incredibles2_v5.png","sfgiants":"SFGiants2018\/SFGiants2018.png","cajamágica":"MutuaMadridOpen\/MutuaMadridOpen.png","mrswhich":"mrswhich\/mrswhich.png","am2dm":"BuzzFeedMorning_v3\/BuzzFeedMorning_v3.png","showmethegift":"ShowMeTheGift2018_v2\/ShowMeTheGift2018_v2.png","earntomorrow":"NHL_2017_2018_PhillyFlyers_v2\/NHL_2017_2018_PhillyFlyers_v2.png","whatblackpanthermeanstome":"BlackPantherHomeEnt2018\/BlackPantherHomeEnt2018.png","todoestáporver":"vodafone2018\/vodafone2018.png","elecciones2018":"mexicanpresidentialelection2018\/mexicanpresidentialelection2018.png","dildilli":"IPL_Delhi\/IPL_Delhi.png","surlechemindubio":"FranceFleuryMichon\/FranceFleuryMichon.png","burnblue":"FranceBlizzardOWL_Dallas\/FranceBlizzardOWL_Dallas.png","???????????????":"japanfanta\/japanfanta.png","esc2018":"Eurovision2018Main\/Eurovision2018Main.png","soychilangoyosivoto":"MexicoCityElections18\/MexicoCityElections18.png","grindcity":"NBA_2017_18_MEM\/NBA_2017_18_MEM.png","senhoraquem":"mrswho\/mrswho.png","jxmtro":"RaeSremmurd2018\/RaeSremmurd2018.png","sliceline":"SiliconValleyHBO2018\/SiliconValleyHBO2018.png","ahm":"AsianHeritageMonth2018\/AsianHeritageMonth2018.png","rbgmovie":"RBG2018\/RBG2018.png","janaaashirwadayatre":"congressq1_2\/congressq1_2.png","redscountry":"CincinnatiReds2018\/CincinnatiReds2018.png","votolibre":"mexicanpresidentialelection2018\/mexicanpresidentialelection2018.png","mrincredible":"MrIncredible\/MrIncredible.png","cesar2018":"cesar2018\/cesar2018.png","o2priority":"followtherabbit_o2\/followtherabbit_o2.png","flechapêra":"incredibles2_v5\/incredibles2_v5.png","toyotahotpass":"toyotaracing\/toyotaracing.png","thelastog":"lastOG_v2\/lastOG_v2.png","3elieve":"NHL_2017_2018_Penguins_v2\/NHL_2017_2018_Penguins_v2.png","cumbreinfonavit":"CumbreInfonavit2018_v3\/CumbreInfonavit2018_v3.png","jurassicpark25":"Jurassic_World_emoji_v2\/Jurassic_World_emoji_v2.png","ontariovotes":"OntarioElection2018\/OntarioElection2018.png","mr????????":"MrIncredible\/MrIncredible.png","siliconvalleyhbo":"SiliconValleyHBO2018\/SiliconValleyHBO2018.png","gotiges":"gotiges\/gotiges.png","swaecation":"RaeSremmurd2018\/RaeSremmurd2018.png","orlandopirates":"SouthAfrica_OrlandoPirates_May2018\/SouthAfrica_OrlandoPirates_May2018.png","apihm":"AsianHeritageMonth2018\/AsianHeritageMonth2018.png","roseanne":"ABCRoseanneV2\/ABCRoseanneV2.png","???????":"Ednamode_v2\/Ednamode_v2.png","mamamia2":"MammaMia2_v3\/MammaMia2_v3.png","askanobel":"askanobel\/askanobel.png","pru14":"MalaysianElection2018\/MalaysianElection2018.png","ridemcowboys":"NRLcowboys2018_v2\/NRLcowboys2018_v2.png","???":"shuri_blackpanther\/shuri_blackpanther.png","mcdonaldsbreakfast":"mcdonaldsmcgriddle\/mcdonaldsmcgriddle.png","letsgonewarriors":"LetsGoneWarriors_v2\/LetsGoneWarriors_v2.png","flexweave":"reebokflexweave_v2\/reebokflexweave_v2.png","myincredibles2review":"incredibles2_v5\/incredibles2_v5.png","mulherelástica":"MrsIncredible\/MrsIncredible.png","mcdmorning":"mcdonaldsmcgriddle\/mcdonaldsmcgriddle.png","slimjxmmi":"RaeSremmurd2018\/RaeSremmurd2018.png","doramilaje":"okoye_blackpanther\/okoye_blackpanther.png","colombiadecide":"colombianelection2018\/colombianelection2018.png","cannes71":"FranceFestivalCannes2018\/FranceFestivalCannes2018.png","remixtrailer":"AmazonRemix_v2\/AmazonRemix_v2.png","eatlikeapro":"EatLikeAPro2018V2\/EatLikeAPro2018V2.png","truetoatlanta":"NBA_2017_18_ATL\/NBA_2017_18_ATL.png","????????????":"mrswhatsit\/mrswhatsit.png","goldenbuzzer":"BGT2018\/BGT2018.png","bgt":"BGT2018\/BGT2018.png","????????":"megmurray\/megmurray.png","thedarkorder":"Thanos2018_v3\/Thanos2018_v3.png","???":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","unpostotranquillo":"aqp2018_v3\/aqp2018_v3.png","??":"StarWarsSolo_Qira\/StarWarsSolo_Qira.png","teamcookie":"empire\/empire.png","marchforourlives":"marchforourlives\/marchforourlives.png","sjsharks":"NHL_2017_2018_SJSharks_v2\/NHL_2017_2018_SJSharks_v2.png","scandalabc":"TGIT_Scandal_2017_v4\/TGIT_Scandal_2017_v4.png","vivov9kathniel":"Kathniel\/Kathniel.png","rusianosharáhéroes":"tecatemundial_v2\/tecatemundial_v2.png","?????":"InterKoreapt2\/InterKoreapt2.png","theincredibles":"incredibles2_v5\/incredibles2_v5.png","teamchuck":"billions-showtime\/billions-showtime.png","sunsat50":"NBA_2017_18_PHX\/NBA_2017_18_PHX.png","theremixtrailer":"AmazonRemix_v2\/AmazonRemix_v2.png","jughead":"RiverdaleS2_2018_v2\/RiverdaleS2_2018_v2.png","?????":"SaudiEnergy\/SaudiEnergy.png","?????":"MrsIncredible\/MrsIncredible.png","jurassicworld":"Jurassic_World_emoji_v2\/Jurassic_World_emoji_v2.png","madamequidam":"mrswhich\/mrswhich.png","?????":"JapanAzurlaneWeather\/JapanAzurlaneWeather.png","famaabailar":"movistar\/movistar.png","debatecapital":"MXcitydebate2018\/MXcitydebate2018.png","????????":"cocacolaAyataka\/cocacolaAyataka.png","chopon":"atlantabraves2018\/atlantabraves2018.png","empirewed":"empire\/empire.png","mmopen":"MutuaMadridOpen\/MutuaMadridOpen.png","???_?????":"HeroNextToHero\/HeroNextToHero.png","ibmer":"IBMThink2018_v2\/IBMThink2018_v2.png","empire":"empire\/empire.png","lafamaviveenmí":"movistar\/movistar.png","madamequiproquo":"mrswhatsit\/mrswhatsit.png","nyxl":"FranceBlizzardOWL_NY\/FranceBlizzardOWL_NY.png","asianheritagemonth":"AsianHeritageMonth2018\/AsianHeritageMonth2018.png","masterchefbr":"MasterChefBR2018\/MasterChefBR2018.png","????_?????":"Vimto2018\/Vimto2018.png","mmas2018":"MYXMusicAwards2018\/MYXMusicAwards2018.png","nuevojetta":"ElJettaDeTuVida\/ElJettaDeTuVida.png","voicepremiere":"thevoices14\/thevoices14.png","proudtobeabulldog":"NRLbulldogs2018\/NRLbulldogs2018.png","freshempire":"freshevents2018Q2\/freshevents2018Q2.png","rednoseday":"RedNoseDay2018\/RedNoseDay2018.png","megustaquevotes":"MXvoterengagement2018\/MXvoterengagement2018.png","?????":"Vimto2018\/Vimto2018.png","????????":"MrsIncredible\/MrsIncredible.png","gatsby?????":"GatsbyDeo2018\/GatsbyDeo2018.png","voicefinale":"thevoices14\/thevoices14.png","césar":"cesar2018_2\/cesar2018_2.png","heforshe":"HeForShe_fixed\/HeForShe_fixed.png","??????????":"Thanos2018_v3\/Thanos2018_v3.png","proudlysydney":"sydneyswans\/sydneyswans.png","7candal":"TGIT_Scandal_2017_v4\/TGIT_Scandal_2017_v4.png","????????":"cocacolaAyataka2\/cocacolaAyataka2.png","theonlywayisessex":"TOWIE\/TOWIE.png","hereweare":"HereWeAre_v3\/HereWeAre_v3.png","heatculture":"NBA_2017_18_MIA\/NBA_2017_18_MIA.png","ligadia":"LigaDia_Emoji_v2\/LigaDia_Emoji_v2.png","tracymorgan":"ogtracy\/ogtracy.png","uptheante":"FranceBlizzardOWL_Houston\/FranceBlizzardOWL_Houston.png","?????_???????_?????????":"SAIB\/SAIB.png","vimto":"Vimto2018\/Vimto2018.png","twd":"FearTWD\/FearTWD.png","200añosdepureza":"Lanjaron200emoji\/Lanjaron200emoji.png","?????":"GatsbyDeo2018\/GatsbyDeo2018.png","?????????":"AsahiGroupFoods\/AsahiGroupFoods.png","incrediblespremiere":"incredibles2_v5\/incredibles2_v5.png","beronica":"RiverdaleS2_2018_v2\/RiverdaleS2_2018_v2.png","jointhehuddle":"AFLWestCoast\/AFLWestCoast.png","lasuertenojuega":"La_Suerte_No_Juega_v2\/La_Suerte_No_Juega_v2.png","moneyheist":"LaCasaDePapel\/LaCasaDePapel.png","playbold":"IPL_Challengers_v2\/IPL_Challengers_v2.png","strengthinnumbers":"NBA_2017_18_GSW_v2\/NBA_2017_18_GSW_v2.png","welcometowestworld":"Westworld2MidSeason\/Westworld2MidSeason.png","donthesash":"EssendonFC\/EssendonFC.png","whywewearblack":"TimesUp_v2\/TimesUp_v2.png","eleccionesmexico":"mexicanpresidentialelection2018\/mexicanpresidentialelection2018.png","lgm":"NYMets2018\/NYMets2018.png","alienist":"TNT-Alienist\/TNT-Alienist.png","helenparr":"MrsIncredible\/MrsIncredible.png","allaboard":"Eurvosion2018AllAboard_jellyfish\/Eurvosion2018AllAboard_jellyfish.png","roseanneabc":"ABCRoseanneV2\/ABCRoseanneV2.png","?????????":"aqp2018_v3\/aqp2018_v3.png","varchie":"RiverdaleS2_2018_v2\/RiverdaleS2_2018_v2.png","aquietplaceid":"aqp2018_v3\/aqp2018_v3.png","???":"nakia_blackpanther\/nakia_blackpanther.png","showyouremotions":"laysshowyouremotions\/laysshowyouremotions.png","snozberries":"SuperTroopers2\/SuperTroopers2.png","thealamode":"capitolonemarchmadness\/capitolonemarchmadness.png","heronexttohero":"HeroNextToHero\/HeroNextToHero.png","thatshowwetalk":"zeefive\/zeefive.png","??_????":"Vimto2018\/Vimto2018.png","simplyamazing":"NissanESLeaf2018\/NissanESLeaf2018.png","unlugartranquilo":"aqp2018_v3\/aqp2018_v3.png","???":"StarWarsSolo_Qira\/StarWarsSolo_Qira.png","unlugarensilencio":"aqp2018_v3\/aqp2018_v3.png","???":"Azurlane_v2\/Azurlane_v2.png","wakandaforever":"BlackPantherHomeEnt2018\/BlackPantherHomeEnt2018.png","?????":"nowruz2018_v4\/nowruz2018_v4.png","?????":"fantasticbeasts_v2\/fantasticbeasts_v2.png","mrswelche":"mrswhich\/mrswhich.png","onlywayisessex":"TOWIE\/TOWIE.png","idolshowcase":"americanidol2018_v2\/americanidol2018_v2.png","bringthemayhem":"FranceBlizzardOWL_Florida\/FranceBlizzardOWL_Florida.png","nhlbruins":"NHL_2017_2018_NHLBruins_v4\/NHL_2017_2018_NHLBruins_v4.png","ednamoda":"Ednamode_v2\/Ednamode_v2.png","blackhistorymonth":"BlackHistoryMonth\/BlackHistoryMonth.png","aapihm":"AsianHeritageMonth2018\/AsianHeritageMonth2018.png","velvetyvoice":"capitolonemarchmadness\/capitolonemarchmadness.png","electrifytheworld":"NissanESLeaf2018\/NissanESLeaf2018.png","vegasborn":"NHL_2017_2018_VegasKnights_v3\/NHL_2017_2018_VegasKnights_v3.png","oncealways":"SouthAfrica_OrlandoPirates_May2018\/SouthAfrica_OrlandoPirates_May2018.png","vivov9malltour":"Kathniel\/Kathniel.png","metoo":"MeToo_v3\/MeToo_v3.png","??????":"Interkorea2018\/Interkorea2018.png","battleforkarnataka":"KarnatakaStateElections2018\/KarnatakaStateElections2018.png","wemetontwitter":"WeMetOnt_Emoji\/WeMetOnt_Emoji.png","colombia2018":"colombianelection2018\/colombianelection2018.png","jackjack":"JackJack\/JackJack.png","maythe4thbewithyou":"StarWarsSolo_Chewie\/StarWarsSolo_Chewie.png","0427????":"Thanos2018_v3\/Thanos2018_v3.png","hazmatch":"colombianelection2018\/colombianelection2018.png","??":"JapanAzurlane2018_v4\/JapanAzurlane2018_v4.png","theterror":"theterror\/theterror.png","navakarnatakanirmana":"congressq1\/congressq1.png","kathnielforvivov9":"Kathniel\/Kathniel.png","niallhoranflicker":"NiallHoran2018\/NiallHoran2018.png","bestoftweet":"BestofTweets2018\/BestofTweets2018.png","beawarrior":"megmurray\/megmurray.png","interkorean":"Interkorea2018\/Interkorea2018.png","jw2":"Jurassic_World_emoji_v2\/Jurassic_World_emoji_v2.png","accesomundialista":"ClaroCAM\/ClaroCAM.png","nakia":"nakia_blackpanther\/nakia_blackpanther.png","feelpretty":"feelpretty_v2\/feelpretty_v2.png","westworlds2":"Westworld2MidSeason\/Westworld2MidSeason.png","animaisfantasticos":"fantasticbeasts_v2\/fantasticbeasts_v2.png","dwtsathletes":"DWTSAthletes2018_v2\/DWTSAthletes2018_v2.png","greatestseasonever":"FlonaseQ1_v2\/FlonaseQ1_v2.png","wearemanly":"NRLmanly2018\/NRLmanly2018.png","???????":"JapanAzurlane2018_v3\/JapanAzurlane2018_v3.png","wegohard":"NBA_2017_18_BKLYN\/NBA_2017_18_BKLYN.png","???":"MothersDay2018\/MothersDay2018.png","jp25":"Jurassic_World_emoji_v2\/Jurassic_World_emoji_v2.png","supertroopers2":"SuperTroopers2\/SuperTroopers2.png","cannes2018":"FranceFestivalCannes2018\/FranceFestivalCannes2018.png","??????????":"aqp2018_v3\/aqp2018_v3.png","???????":"fantasticbeasts_v2\/fantasticbeasts_v2.png","neversettle":"Astros2018\/Astros2018.png","think2018":"IBMThink2018_v2\/IBMThink2018_v2.png","????????":"aqp2018_v3\/aqp2018_v3.png","euroleague":"Euroleague_2018_v2\/Euroleague_2018_v2.png","solomovie":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","ibm":"IBMThink2018_v2\/IBMThink2018_v2.png","voicenotestour":"CharliePuthAlbum2018_v2\/CharliePuthAlbum2018_v2.png","??????":"deadpooljapan18_v2\/deadpooljapan18_v2.png","chookity":"TBSfinalspace\/TBSfinalspace.png","sbi":"SBIBank_v3\/SBIBank_v3.png","séunaguerrera":"megmurray\/megmurray.png","bhm":"BlackHistoryMonth\/BlackHistoryMonth.png","capitalstb":"GlobalCapitalSummertimeBall2018\/GlobalCapitalSummertimeBall2018.png","masterchef":"spainmasterchef\/spainmasterchef.png","cusrise":"NBACeltics2018\/NBACeltics2018.png","eleccionesméxico":"mexicanpresidentialelection2018\/mexicanpresidentialelection2018.png","flècheparr":"incredibles2_v5\/incredibles2_v5.png","?????????????":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","mcdsbreakfast":"mcdonaldsmcgriddle\/mcdonaldsmcgriddle.png","?????_?????":"SAIB\/SAIB.png","mrswhatsit":"mrswhatsit\/mrswhatsit.png","royalwedding2018":"royalwedding2018\/royalwedding2018.png","bullsnation":"NBA_2017_18_CHI\/NBA_2017_18_CHI.png","interkoreansummit":"Interkorea2018\/Interkorea2018.png","nrl":"NRL2018\/NRL2018.png","fanantonio":"capitolonemarchmadness\/capitolonemarchmadness.png","??":"StarWarsSolo_Lando\/StarWarsSolo_Lando.png","????_???_???":"HeroNextToHero\/HeroNextToHero.png","senhoraqueé":"mrswhatsit\/mrswhatsit.png","mammamia2":"MammaMia2_v3\/MammaMia2_v3.png","britainsgottalent":"BGT2018\/BGT2018.png","voiceknockouts":"thevoices14\/thevoices14.png","césar2018":"cesar2018_2\/cesar2018_2.png","followtherabbit":"followtherabbit_v2\/followtherabbit_v2.png","????????_??":"noon_v3\/noon_v3.png","feartwd":"FearTWD\/FearTWD.png","jurassicworld2":"Jurassic_World_emoji_v2\/Jurassic_World_emoji_v2.png","blacklivesmatter":"BlackHistoryMonth\/BlackHistoryMonth.png","pinkcarpetmtvmiaw":"MTVMiawAwardsBR2018\/MTVMiawAwardsBR2018.png","breyersdelights":"impossiblepossiblebreyers\/impossiblepossiblebreyers.png","fightingforglory":"FranceBlizzardOWL_Shanghai\/FranceBlizzardOWL_Shanghai.png","westworldseason2":"Westworld2MidSeason\/Westworld2MidSeason.png","dillydilly":"dillydillyUK\/dillydillyUK.png","allcaps":"NHL_2017_2018_Caps_v2\/NHL_2017_2018_Caps_v2.png","mrssoundso":"mrswhatsit\/mrswhatsit.png","eaststowin":"NRLRoosters2018\/NRLRoosters2018.png","darkorder":"Thanos2018_v3\/Thanos2018_v3.png","milehighbasketball":"NBA_2017_18_DEN_v2\/NBA_2017_18_DEN_v2.png","serenawilliams":"SerenaWilliams2018\/SerenaWilliams2018.png","threemuskamigos":"capitolonemarchmadness\/capitolonemarchmadness.png","?????":"Interkorea2018\/Interkorea2018.png","bronxnation":"NRLBroncos2018\/NRLBroncos2018.png","votaméxico":"mexicanpresidentialelection2018\/mexicanpresidentialelection2018.png","supersuit":"Frozone\/Frozone.png","animalesfantásticos":"fantasticbeasts_v2\/fantasticbeasts_v2.png","onpoli":"OntarioElection2018\/OntarioElection2018.png","suerteono":"La_Suerte_No_Juega_v2\/La_Suerte_No_Juega_v2.png","hangnélkül":"aqp2018_v3\/aqp2018_v3.png","okoye":"okoye_blackpanther\/okoye_blackpanther.png","mtvaward":"MTVMovieAwards2018\/MTVMovieAwards2018.png","??????_??????":"SaudiEnergy\/SaudiEnergy.png","sracuál":"mrswhich\/mrswhich.png","puremagic":"NBA_2017_18_ORL\/NBA_2017_18_ORL.png","biobox":"FranceFleuryMichon\/FranceFleuryMichon.png","porvida":"vidaemoji\/vidaemoji.png","letsgopadres":"SDPadres2018\/SDPadres2018.png","malaysiaelection":"MalaysianElection2018\/MalaysianElection2018.png","incredibles2":"incredibles2_v5\/incredibles2_v5.png","??????????????":"IPL_MumbaiIndians_v2\/IPL_MumbaiIndians_v2.png","thelastogtbs":"lastOG_v2\/lastOG_v2.png","??":"aqp2018_v3\/aqp2018_v3.png","ripcity":"NBA_2017_18_POR\/NBA_2017_18_POR.png","detroitsummers":"DetroitTigers2018\/DetroitTigers2018.png","mrincredibile":"MrIncredible\/MrIncredible.png","doneforme":"CharliePuthAlbum2018_v2\/CharliePuthAlbum2018_v2.png","frozono":"Frozone\/Frozone.png","????":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","??????":"MothersDay2018\/MothersDay2018.png","jamesbeardawards":"JamesBeardAwards2018\/JamesBeardAwards2018.png","lakeshow":"NBA_2017_18_LAL\/NBA_2017_18_LAL.png","o2music":"followtherabbit_o2\/followtherabbit_o2.png","thevoice":"thevoices14\/thevoices14.png","señoracuál":"mrswhich\/mrswhich.png","fastestfeet":"reebokflexweave_v2\/reebokflexweave_v2.png","wrinkleintime":"megmurray\/megmurray.png","onelxn":"OntarioElection2018\/OntarioElection2018.png","kohlscashsweepstakes":"kohlscash2v2\/kohlscash2v2.png","estamosenlachampions":"NissanUCL2018\/NissanUCL2018.png","sheinspiresme":"HereWeAre_v3\/HereWeAre_v3.png","rcb":"IPL_Challengers_v2\/IPL_Challengers_v2.png","discoverwestworld":"Westworld2MidSeason\/Westworld2MidSeason.png","???????":"JapanAzurlaneWeather\/JapanAzurlaneWeather.png","divebartour":"BLDiveBar_v2\/BLDiveBar_v2.png","mrsincredible":"MrsIncredible\/MrsIncredible.png","snowcam":"snowcorp\/snowcorp.png","lastog":"lastOG_v2\/lastOG_v2.png","??????":"aqp2018_v3\/aqp2018_v3.png","boundbyblue":"AFLBoundbyBlue\/AFLBoundbyBlue.png","impossiblepossible":"impossiblepossiblebreyers\/impossiblepossiblebreyers.png","karnatakaelection":"KarnatakaStateElections2018\/KarnatakaStateElections2018.png","mcgriddles":"mcdonaldsmcgriddle\/mcdonaldsmcgriddle.png","lifefindsaway":"Jurassic_World_emoji_v2\/Jurassic_World_emoji_v2.png","tmltalk":"NHL_2017_2018_MapleLeafs_v2\/NHL_2017_2018_MapleLeafs_v2.png","vidachallenge":"vidaemoji\/vidaemoji.png","??????????":"IPL_Chennai\/IPL_Chennai.png","nissanleaf":"NissanESLeaf2018\/NissanESLeaf2018.png","piratesre8orn":"SouthAfrica_OrlandoPirates_May2018\/SouthAfrica_OrlandoPirates_May2018.png","citychampions":"CityChampions2018\/CityChampions2018.png","raisedroyal":"kcroyals2018\/kcroyals2018.png","????????????":"AsahiGroupFoods\/AsahiGroupFoods.png","playtheremix":"AmazonRemix_v2\/AmazonRemix_v2.png","avaduvernay":"AvaDuVernay\/AvaDuVernay.png","???????????":"AvaDuVernay\/AvaDuVernay.png","raysup":"TampaBayRays2018\/TampaBayRays2018.png","weareraiders":"NRLraiders2018\/NRLraiders2018.png","maythe4th":"StarWarsSolo_Chewie\/StarWarsSolo_Chewie.png","tenistve":"MutuaMadridOpen\/MutuaMadridOpen.png","???_???_????":"HeroNextToHero_v2\/HeroNextToHero_v2.png","truetotheblue":"SeattleMariners2018\/SeattleMariners2018.png","ednamode":"Ednamode_v2\/Ednamode_v2.png","pipercoin":"SiliconValleyHBO2018\/SiliconValleyHBO2018.png","towie":"TOWIE\/TOWIE.png","lando":"StarWarsSolo_Lando\/StarWarsSolo_Lando.png","???????":"StarWarsSolo_HanSolo\/StarWarsSolo_HanSolo.png","bestneverrest":"MercedesGermany_BestNeverRest\/MercedesGermany_BestNeverRest.png","tgit":"TGIT_Popcorn_v3\/TGIT_Popcorn_v3.png","aceshigh":"FranceBlizzardOWL_London\/FranceBlizzardOWL_London.png","signorachi":"mrswho\/mrswho.png","persiannewyear":"nowruz2018_v4\/nowruz2018_v4.png","stlcards":"StLouisCardinals2018\/StLouisCardinals2018.png","nbb":"Emoji_NBB_2017_2018\/Emoji_NBB_2017_2018.png","???????????????????":"fantasticbeasts_v2\/fantasticbeasts_v2.png","bughead":"RiverdaleS2_2018_v2\/RiverdaleS2_2018_v2.png","whitesox":"whitesox2018\/whitesox2018.png","gonosetonose":"RedNoseDay2018\/RedNoseDay2018.png","myvimto":"Vimto2018\/Vimto2018.png","señoraquién":"mrswho\/mrswho.png","birdland":"orioles2018_v2\/orioles2018_v2.png","???????":"catemoji_v2\/catemoji_v2.png","pinstripepride":"NYYankees2018\/NYYankees2018.png","todoestaporver":"vodafone2018\/vodafone2018.png","espejopúblico":"EspejoPublico_2017_2018\/EspejoPublico_2017_2018.png","empirepreshow":"empire\/empire.png","?????_??????":"SaudiEnergy\/SaudiEnergy.png","thehaloway":"LAAngels2018\/LAAngels2018.png","shuri":"shuri_blackpanther\/shuri_blackpanther.png","axenolollabr":"AxeLollapalooza\/AxeLollapalooza.png","???????????????":"Adsforgood_Japan2018_v2\/Adsforgood_Japan2018_v2.png","ge14":"MalaysianElection2018\/MalaysianElection2018.png","dieunglaublichen2":"incredibles2_v5\/incredibles2_v5.png","wakanda":"blackpanther_live_v5\/blackpanther_live_v5.png","alleyesnorth":"NBA_2017_18_MIN\/NBA_2017_18_MIN.png","????????????????????":"MrIncredible\/MrIncredible.png","kxip":"IPL_KingsXIPunjab\/IPL_KingsXIPunjab.png"},"profile_user":{"id":786939553,"id_str":"786939553","name":"Mars Weather","screen_name":"MarsWxReport","location":"Gale Crater, Mars","url":"http:\/\/mars.nasa.gov\/msl\/mission\/instruments\/environsensors\/rems\/","description":"Updates as avail from the REMS weather instrument aboard @MarsCuriosity.  Data credit: Centro deAstrobiologia, FMI, JPL\/NASA, Not an official acct.","protected":false,"followers_count":39932,"friends_count":54,"listed_count":300,"created_at":"Tue Aug 28 12:48:50 +0000 2012","favourites_count":190,"utc_offset":null,"time_zone":null,"geo_enabled":true,"verified":false,"statuses_count":1439,"lang":"en","contributors_enabled":false,"is_translator":false,"is_translation_enabled":false,"profile_background_color":"C0DEED","profile_background_image_url":"http:\/\/pbs.twimg.com\/profile_background_images\/822695755\/913d559a238a92c0f31aed92bb0e0082.jpeg","profile_background_image_url_https":"https:\/\/pbs.twimg.com\/profile_background_images\/822695755\/913d559a238a92c0f31aed92bb0e0082.jpeg","profile_background_tile":false,"profile_image_url":"http:\/\/pbs.twimg.com\/profile_images\/2552209293\/220px-Mars_atmosphere_normal.jpg","profile_image_url_https":"https:\/\/pbs.twimg.com\/profile_images\/2552209293\/220px-Mars_atmosphere_normal.jpg","profile_banner_url":"https:\/\/pbs.twimg.com\/profile_banners\/786939553\/1403835009","profile_link_color":"0084B4","profile_sidebar_border_color":"FFFFFF","profile_sidebar_fill_color":"DDEEF6","profile_text_color":"333333","profile_use_background_image":true,"has_extended_profile":false,"default_profile":false,"default_profile_image":false,"following":null,"follow_request_sent":null,"notifications":null,"business_profile_state":"none","translator_type":"none"},"profileEditingCSSBundle":"https:\/\/abs.twimg.com\/a\/1525911434\/css\/t1\/twitter_profile_editing.bundle.css","profile_id":786939553,"business_profile":false,"b2c_logged_out_support_indicators_enabled":true,"business_profile_featured_collections_complete":false,"cardsGallery":true,"injectComposedTweets":false,"inlineProfileEditing":false,"gdprSoftBounceEnabled":false,"isClusterFollowReplenishEnabled":false,"autoplayEnabled":true,"periscopeLiveStatusPollInterval":15000,"trendsCacheKey":null,"decider_personalized_trends":false,"trendsEndpoint":"\/i\/trends","wtfOptions":{"pc":true,"connections":true,"limit":3,"display_location":"profile-sidebar","dismissable":true,"similar_to_user_id":"786939553"},"showSensitiveContent":false,"autoPlayBalloonsAnimation":false,"momentsNuxTooltipsEnabled":false,"isCurrentUser":false,"isSensitiveProfile":false,"timeline_url":"\/i\/profiles\/show\/MarsWxReport\/timeline\/tweets","initialState":{"title":"Mars Weather (@MarsWxReport) | Twitter","section":null,"module":"app\/pages\/profile\/highline_landing","cache_ttl":300,"body_class_names":"three-col logged-out user-style-MarsWxReport ms-windows enhanced-mini-profile ProfilePage ProfilePage--withWarning","doc_class_names":"route-profile","route_name":"profile","page_container_class_names":"AppContent","ttft_navigation":false}}'/>
      <input class="swift-boot-module" type="hidden" value="app/pages/profile/highline_landing"/>
      <input id="swift-module-path" type="hidden" value="https://abs.twimg.com/k/swift/en"/>
      <script async="" src="https://abs.twimg.com/k/en/init.en.0be835e04b9a8e74d6e4.js">
      </script>
     </body>
    </html>
    


```python
#scrap latest Mars weather tweet
mars_weather = soup3.find_all('p', class_='TweetTextSize TweetTextSize--normal js-tweet-text tweet-text')[0].text

#print to check tweet
print(mars_weather)
```

    #InSight rising above the California fog on liftoff.https://twitter.com/birdsnspace/status/993603886106660864 …
    

#### Mars Facts

Use Pandas to scrape the table from Mars Facts webpage and convert the data to a HTML table string


```python
# URL of page to be scraped
url4 = 'https://space-facts.com/mars/'
```


```python
# use Pandas to get the url table
tables = pd.read_html(url4)
tables
```




    [                      0                              1
     0  Equatorial Diameter:                       6,792 km
     1       Polar Diameter:                       6,752 km
     2                 Mass:  6.42 x 10^23 kg (10.7% Earth)
     3                Moons:            2 (Phobos & Deimos)
     4       Orbit Distance:       227,943,824 km (1.52 AU)
     5         Orbit Period:           687 days (1.9 years)
     6  Surface Temperature:                  -153 to 20 °C
     7         First Record:              2nd millennium BC
     8          Recorded By:           Egyptian astronomers]




```python
# Convert list of table into pandas dataframe
df = tables[0]

# update column name
df.columns=['description','value']

# inspect dataframe
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>description</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Equatorial Diameter:</td>
      <td>6,792 km</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Polar Diameter:</td>
      <td>6,752 km</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mass:</td>
      <td>6.42 x 10^23 kg (10.7% Earth)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Moons:</td>
      <td>2 (Phobos &amp; Deimos)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Orbit Distance:</td>
      <td>227,943,824 km (1.52 AU)</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Orbit Period:</td>
      <td>687 days (1.9 years)</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Surface Temperature:</td>
      <td>-153 to 20 °C</td>
    </tr>
    <tr>
      <th>7</th>
      <td>First Record:</td>
      <td>2nd millennium BC</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Recorded By:</td>
      <td>Egyptian astronomers</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Set the index to the description column

df.set_index('description', inplace=True)
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>value</th>
    </tr>
    <tr>
      <th>description</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Equatorial Diameter:</th>
      <td>6,792 km</td>
    </tr>
    <tr>
      <th>Polar Diameter:</th>
      <td>6,752 km</td>
    </tr>
    <tr>
      <th>Mass:</th>
      <td>6.42 x 10^23 kg (10.7% Earth)</td>
    </tr>
    <tr>
      <th>Moons:</th>
      <td>2 (Phobos &amp; Deimos)</td>
    </tr>
    <tr>
      <th>Orbit Distance:</th>
      <td>227,943,824 km (1.52 AU)</td>
    </tr>
    <tr>
      <th>Orbit Period:</th>
      <td>687 days (1.9 years)</td>
    </tr>
    <tr>
      <th>Surface Temperature:</th>
      <td>-153 to 20 °C</td>
    </tr>
    <tr>
      <th>First Record:</th>
      <td>2nd millennium BC</td>
    </tr>
    <tr>
      <th>Recorded By:</th>
      <td>Egyptian astronomers</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Use pandas to  generate HTML tables from DataFrames and save as html file
df.to_html('table.html')

```

#### Mars Hemisperes

USGS Astrogeology site to obtain high resolution images for each of Mar's hemispheres


```python
# Execute Chromedriver (add in again in case you close the browser)
executable_path = {'executable_path': 'chromedriver.exe'}
browser = Browser('chrome', **executable_path, headless=False)
```


```python
# URL of page to be scraped
url5 = 'https://astrogeology.usgs.gov/search/results?q=hemisphere+enhanced&k1=target&v1=Mars'

#Visit the page using the browser
browser.visit(url5)
```


```python
# assign html content
html = browser.html
# Create a Beautiful Soup object
soup5 = bs(html,"html5lib")
# Print formatted version of the soup
print(soup5.prettify())
```

    <!DOCTYPE html>
    <html lang="en" xmlns="http://www.w3.org/1999/xhtml">
     <head>
      <link href="//ajax.googleapis.com/ajax/libs/jqueryui/1.11.3/themes/smoothness/jquery-ui.css" rel="stylesheet" type="text/css"/>
      <script async="" src="https://ssl.google-analytics.com/ga.js" type="text/javascript">
      </script>
      <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js" type="text/javascript">
      </script>
      <title>
       Astropedia Search Results | USGS Astrogeology Science Center
      </title>
      <meta content="USGS Astrogeology Science Center Astropedia search results." name="description"/>
      <meta content="USGS,Astrogeology Science Center,Cartography,Geology,Space,Geological Survey,Mapping" name="keywords"/>
      <meta content="IE=edge" http-equiv="X-UA-Compatible"/>
      <meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
      <meta content="width=device-width, initial-scale=1, maximum-scale=1" name="viewport"/>
      <meta content="x61hXXVj7wtfBSNOPnTftajMsZ5yB2W-qRoyr7GtOKM" name="google-site-verification"/>
      <!--<link rel="stylesheet" href="http://fonts.googleapis.com/css?family=Open+Sans:400italic,400,bold"/>-->
      <link href="/css/main.css" media="screen" rel="stylesheet"/>
      <link href="/css/print.css" media="print" rel="stylesheet"/>
      <!--[if lt IE 9]>
    			<script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script>
    			<script src="/js/respond.min.js"></script>
    			<link rel="stylesheet" type="text/css" href="/css/ie.css"/>
                            <script>
                              document.createElement('header');
                              document.createElement('nav');
                              document.createElement('section');
                              document.createElement('article');
                              document.createElement('aside');
                              document.createElement('footer');
                              document.createElement('hgroup');
                            </script>
                      <![endif]-->
      <link href="/favicon.ico" rel="icon" type="image/x-ico"/>
     </head>
     <body id="results">
      <header>
       <h1>
        Astrogeology Science Center
       </h1>
       <a href="http://www.usgs.gov">
        <img alt="USGS: Science for a Changing World" class="logo" height="70" src="/images/usgs_logo_main_2x.png" width="180"/>
       </a>
      </header>
      <div class="wrapper">
       <nav>
        <a href="#" id="nav-toggle" title="Navigation Menu">
         Menu
        </a>
        <ul class="dropdown dropdown-horizontal" id="yw0">
         <li>
          <a href="/">
           Home
          </a>
         </li>
         <li>
          <a href="/about">
           About
          </a>
          <ul>
           <li>
            <a href="/about/careers">
             Careers
            </a>
           </li>
           <li>
            <a href="/contact">
             Contact
            </a>
           </li>
           <li>
            <a href="/about/events">
             Events
            </a>
           </li>
           <li>
            <a href="/site/glossary">
             Glossary
            </a>
           </li>
           <li>
            <a href="/about/mission">
             Mission
            </a>
           </li>
           <li>
            <a href="/news">
             News
            </a>
           </li>
           <li>
            <a href="/people">
             People
            </a>
           </li>
           <li>
            <a href="/about/using-our-images">
             Using Our Images
            </a>
           </li>
           <li>
            <a href="/about/visitors">
             Visitors
            </a>
           </li>
          </ul>
         </li>
         <li>
          <a href="/facilities">
           Labs / Facilities
          </a>
          <ul>
           <li>
            <a href="/facilities/flynn-creek-crater-sample-collection">
             Flynn Creek Crater Sample Collection
            </a>
           </li>
           <li>
            <a href="http://www.moon-cal.org">
             Lunar Calibration Project
            </a>
           </li>
           <li>
            <a href="/facilities/meteor-crater-sample-collection">
             Meteor Crater Sample Collection
            </a>
           </li>
           <li>
            <a href="/facilities/mrctr">
             MRCTR GIS Lab
            </a>
           </li>
           <li>
            <a href="/facilities/cartography-and-imaging-sciences-node-of-nasa-planetary-data-system">
             PDS Cartography and Imaging Sciences Node
            </a>
           </li>
           <li>
            <a href="/pds/annex">
             PDS IMG Annex
            </a>
           </li>
           <li>
            <a href="/facilities/photogrammetry-guest-facility">
             Photogrammetry Guest Facility
            </a>
           </li>
           <li>
            <a href="/rpif">
             Regional Planetary Information Facility (RPIF)
            </a>
           </li>
          </ul>
         </li>
         <li>
          <a href="/maps">
           Maps / Products
          </a>
          <ul>
           <li>
            <a href="/search">
             Product Search
            </a>
           </li>
           <li>
            <a href="http://planetarynames.wr.usgs.gov">
             Gazetteer of Planetary Nomenclature
            </a>
           </li>
           <li>
            <a href="http://planetarymapping.wr.usgs.gov">
             Geologic Mapping Program
            </a>
           </li>
           <li>
            <a href="http://pilot.wr.usgs.gov">
             Planetary Image Locator Tool (PILOT)
            </a>
           </li>
           <li>
            <a href="/search/planetary-index">
             Planetary Map Index
            </a>
           </li>
          </ul>
         </li>
         <li>
          <a href="/geology">
           Missions / Research
          </a>
          <ul>
           <li>
            <a href="/geology/mars-dunes">
             Mars Dunes
            </a>
           </li>
           <li>
            <a href="/geology/mars-ice">
             Mars Ice
            </a>
           </li>
           <li>
            <a href="/missions">
             Mission Support
            </a>
           </li>
           <li>
            <a href="/solar-system">
             Solar System
            </a>
           </li>
           <li>
            <a href="/groups">
             Working Groups
            </a>
           </li>
          </ul>
         </li>
         <li>
          <a href="/tools">
           Tools
          </a>
          <ul>
           <li>
            <a href="http://planetarynames.wr.usgs.gov">
             Gazetteer of Planetary Nomenclature
            </a>
           </li>
           <li>
            <a href="http://isis.astrogeology.usgs.gov">
             Integrated Software for Imagers and Spectrometers (ISIS)
            </a>
           </li>
           <li>
            <a href="http://astrogeology.usgs.gov/tools/map-a-planet-2">
             Map a Planet 2
            </a>
           </li>
           <li>
            <a href="http://pilot.wr.usgs.gov">
             Planetary Image Locator Tool (PILOT)
            </a>
           </li>
           <li>
            <a href="http://astrocloud.wr.usgs.gov/">
             Projection on the Web (POW)
            </a>
           </li>
          </ul>
         </li>
        </ul>
        <form action="/search/results" class="search" id="search" method="get">
         <input title="Search Astropedia" type="submit" value=""/>
         <input name="q" placeholder="Search" type="text"/>
         <input name="__ncforminfo" type="hidden" value="aecV491P5u_Fdfp4xFkO9IQKqOy3NGwbEmxCTP6CtmR1y1Owbs_ycxfH6r-IwwnJg7M2GNdBvZnu5_S3IPhw7vV2VFT7mzSObNGnE7see2A="/>
        </form>
       </nav>
       <div class="container">
        <form action="/search/results" class="bar widget block" id="search-bar">
         <input name="q" type="hidden" value="hemisphere-enhanced"/>
         <input name="target" type="hidden" value="Mars"/>
         <input name="__ncforminfo" type="hidden" value="aecV491P5u_Fdfp4xFkO9IQKqOy3NGwbEmxCTP6CtmRNym3Nnh3Cg2G7CZEdkUSrhlWVSS2zpJFr3Ed6X7tJhzLRcANqgkCkvrJrKBjLbxmpIuA9bB_D4g=="/>
        </form>
        <div class="full-content">
         <section class="block" id="results-accordian">
          <div class="result-list" data-section="product" id="product-section">
           <div class="accordian">
            <h2>
             Products
            </h2>
            <span class="count">
             4 Results
            </span>
            <span class="collapse">
             Collapse
            </span>
           </div>
           <div class="collapsible results">
            <div class="item">
             <a class="itemLink product-item" href="/search/map/Mars/Viking/cerberus_enhanced">
              <img alt="Cerberus Hemisphere Enhanced thumbnail" class="thumb" src="/cache/images/dfaf3849e74bf973b59eb50dab52b583_cerberus_enhanced.tif_thumb.png"/>
             </a>
             <div class="description">
              <a class="itemLink product-item" href="/search/map/Mars/Viking/cerberus_enhanced">
               <h3>
                Cerberus Hemisphere Enhanced
               </h3>
              </a>
              <span class="subtitle" style="float:left">
               image/tiff 21 MB
              </span>
              <span class="pubDate" style="float:right">
              </span>
              <br/>
              <p>
               Mosaic of the Cerberus hemisphere of Mars projected into point perspective, a view similar to that which one would see from a spacecraft. This mosaic is composed of 104 Viking Orbiter images acquired…
              </p>
             </div>
             <!-- end description -->
            </div>
            <div class="item">
             <a class="itemLink product-item" href="/search/map/Mars/Viking/schiaparelli_enhanced">
              <img alt="Schiaparelli Hemisphere Enhanced thumbnail" class="thumb" src="/cache/images/7677c0a006b83871b5a2f66985ab5857_schiaparelli_enhanced.tif_thumb.png"/>
             </a>
             <div class="description">
              <a class="itemLink product-item" href="/search/map/Mars/Viking/schiaparelli_enhanced">
               <h3>
                Schiaparelli Hemisphere Enhanced
               </h3>
              </a>
              <span class="subtitle" style="float:left">
               image/tiff 35 MB
              </span>
              <span class="pubDate" style="float:right">
              </span>
              <br/>
              <p>
               Mosaic of the Schiaparelli hemisphere of Mars projected into point perspective, a view similar to that which one would see from a spacecraft. The images were acquired in 1980 during early northern…
              </p>
             </div>
             <!-- end description -->
            </div>
            <div class="item">
             <a class="itemLink product-item" href="/search/map/Mars/Viking/syrtis_major_enhanced">
              <img alt="Syrtis Major Hemisphere Enhanced thumbnail" class="thumb" src="/cache/images/aae41197e40d6d4f3ea557f8cfe51d15_syrtis_major_enhanced.tif_thumb.png"/>
             </a>
             <div class="description">
              <a class="itemLink product-item" href="/search/map/Mars/Viking/syrtis_major_enhanced">
               <h3>
                Syrtis Major Hemisphere Enhanced
               </h3>
              </a>
              <span class="subtitle" style="float:left">
               image/tiff 25 MB
              </span>
              <span class="pubDate" style="float:right">
              </span>
              <br/>
              <p>
               Mosaic of the Syrtis Major hemisphere of Mars projected into point perspective, a view similar to that which one would see from a spacecraft. This mosaic is composed of about 100 red and violet…
              </p>
             </div>
             <!-- end description -->
            </div>
            <div class="item">
             <a class="itemLink product-item" href="/search/map/Mars/Viking/valles_marineris_enhanced">
              <img alt="Valles Marineris Hemisphere Enhanced thumbnail" class="thumb" src="/cache/images/04085d99ec3713883a9a57f42be9c725_valles_marineris_enhanced.tif_thumb.png"/>
             </a>
             <div class="description">
              <a class="itemLink product-item" href="/search/map/Mars/Viking/valles_marineris_enhanced">
               <h3>
                Valles Marineris Hemisphere Enhanced
               </h3>
              </a>
              <span class="subtitle" style="float:left">
               image/tiff 27 MB
              </span>
              <span class="pubDate" style="float:right">
              </span>
              <br/>
              <p>
               Mosaic of the Valles Marineris hemisphere of Mars projected into point perspective, a view similar to that which one would see from a spacecraft. The distance is 2500 kilometers from the surface of…
              </p>
             </div>
             <!-- end description -->
            </div>
            <script>
             addBases=[];;if(typeof resetLayerSwitcher==="function"){resetLayerSwitcher(false)};var productTotal = 4;
            </script>
           </div>
           <!-- end this-section -->
          </div>
         </section>
        </div>
       </div>
       <div class="icons projects black scroll-wrapper">
        <div class="scroll">
         <a class="icon" href="http://isis.astrogeology.usgs.gov" title="Integrated Software for Imagers and Spectrometers">
          <img alt="ISIS Logo" height="112" src="/images/logos/isis_2x.jpg" width="112"/>
          <span class="label">
           ISIS
          </span>
         </a>
         <a class="icon" href="http://planetarynames.wr.usgs.gov" title="Gazetteer of Planetary Nomenclature">
          <img alt="Nomenclature Logo" height="112" src="/images/logos/nomenclature_2x.jpg" width="112"/>
          <span class="label">
           Planetary Nomenclature
          </span>
         </a>
         <a class="icon" href="http://astrogeology.usgs.gov/tools/map" title="Map a Planet 2">
          <img alt="Map-a-Planet Logo" height="112" src="/images/logos/map_a_planet_2x.jpg" width="112"/>
          <span class="label">
           Map a Planet 2
          </span>
         </a>
         <a class="icon" href="/facilities/imaging-node-of-nasa-planetary-data-system-pds" title="PDS Imaging Node">
          <img alt="PDS Logo" height="112" src="/images/pds_logo-black-web.png"/>
          <span class="label">
           PDS Imaging Node
          </span>
         </a>
         <!--
    						<a title="Astropedia Search" href="/search" class="icon">
    							<img alt="Astropedia Logo" height="112" width="112" src="/images/logos/astropedia_2x.jpg"/>
    							<span class="label">Astropedia</span>
    						</a>
    -->
         <a class="icon" href="/rpif" title="Regional Planetary Image Facility">
          <img alt="RPIF Logo" height="112" src="/images/logos/rpif_2x.jpg" width="112"/>
          <span class="label">
           RPIF
          </span>
         </a>
         <a class="icon" href="/facilities/photogrammetry-guest-facility" title="Photogrammetry Guest Facility">
          <img alt="Photogrammetry Guest Faciltiy Logo" height="112" src="/images/logos/photogrammetry_2x.jpg" width="112"/>
          <span class="label">
           Photogrammetry Guest Facility
          </span>
         </a>
         <a class="icon" href="http://pilot.wr.usgs.gov" title="Planetary Image Locator Tool">
          <img alt="Pilot Logo" height="112" src="/images/logos/pilot_2x.jpg" width="112"/>
          <span class="label">
           PILOT
          </span>
         </a>
         <a class="icon" href="/facilities/mrctr" title="Mapping, Remote-sensing, Cartography, Technology and Research GIS Lab">
          <img alt="MRCTR GIS Lab Logo" height="112" src="/images/logos/mrctr_2x.jpg" width="112"/>
          <span class="label">
           MRCTR GIS Lab
          </span>
         </a>
        </div>
       </div>
       <footer>
        <div class="left">
         <a href="http://astrogeology.usgs.gov">
          Home
         </a>
         |
         <a href="http://astrogeology.usgs.gov/contact">
          Contact
         </a>
         |
         <a href="http://astrogeology.usgs.gov/about/events">
          Events
         </a>
         |
         <a href="http://astrogeology.usgs.gov/news">
          News
         </a>
        </div>
        <div class="right">
         <a href="http://www.doi.gov">
          U.S. Department of Interior
         </a>
         |
         <a href="http://www.usgs.gov">
          U.S. Geological Survey
         </a>
         |
         <a href="http://www.usa.gov">
          USA.gov
         </a>
        </div>
       </footer>
      </div>
      <!--
    		<div class="credit">
    			<small>Background Credits: NASA/USGS</small>
    		</div>
    -->
      <div class="page-background" style="
    			background:url('/images/backgrounds/mars.jpg');
    			filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(
    				src='/images/backgrounds/mars.jpg', sizingMethod='scale');
    		">
      </div>
      <script type="text/javascript">
       var baseUrl = "";
    
    
    var _gaq = _gaq || [];_gaq.push(['_setAccount', 'UA-27613186-1']);_gaq.push(['_trackPageview']);(function() { var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js'; var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);})();
      </script>
      <script src="//ajax.googleapis.com/ajax/libs/jqueryui/1.11.3/jquery-ui.min.js" type="text/javascript">
      </script>
      <script src="/js/general.js" type="text/javascript">
      </script>
     </body>
    </html>
    


```python
# assigned list to store:
hemisphere_image_urls = []
```


```python
# create empty dict
dict = {}
```


```python
# get all the title
results = soup5.find_all('h3')
```


```python
# Loop through each result
for result in results:
    # Get text info from result
    itema = result.text
    time.sleep(1)    
    browser.click_link_by_partial_text(itema)
    time.sleep(1)
    # assign html content
    htmla = browser.html
    # Create a Beautiful Soup object
    soupa = bs(htmla,"html5lib")
    time.sleep(1)
    # Grab the image link
    linka = soupa.find_all('div', class_="downloads")[0].find_all('a')[0].get("href")
        # Pass title to Dict
    time.sleep(1)
    dict["title"]=itema
    # Pass url to Dict
    dict["img_url"]=linka
    # Append Dict to the list 
    hemisphere_image_urls.append(dict)
    # Clean Up Dict
    dict = {}
    browser.click_link_by_partial_text('Back')
    time.sleep(1)
```


```python
# review List
hemisphere_image_urls
```




    [{'img_url': 'http://astropedia.astrogeology.usgs.gov/download/Mars/Viking/cerberus_enhanced.tif/full.jpg',
      'title': 'Cerberus Hemisphere Enhanced'},
     {'img_url': 'http://astropedia.astrogeology.usgs.gov/download/Mars/Viking/schiaparelli_enhanced.tif/full.jpg',
      'title': 'Schiaparelli Hemisphere Enhanced'},
     {'img_url': 'http://astropedia.astrogeology.usgs.gov/download/Mars/Viking/syrtis_major_enhanced.tif/full.jpg',
      'title': 'Syrtis Major Hemisphere Enhanced'},
     {'img_url': 'http://astropedia.astrogeology.usgs.gov/download/Mars/Viking/valles_marineris_enhanced.tif/full.jpg',
      'title': 'Valles Marineris Hemisphere Enhanced'}]


