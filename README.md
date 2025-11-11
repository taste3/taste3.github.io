# Nicolas Patenaude

## Frigo Chouinard V0.2

<section id="game1">
  <div id="unity-container" class="unity-desktop">
    <canvas id="unity-canvas" width="960" height="600" tabindex="-1"></canvas>
    <div id="unity-loading-bar">
      <div id="unity-logo"></div>
      <div id="unity-progress-bar-empty">
        <div id="unity-progress-bar-full"></div>
      </div>
    </div>
    <div id="unity-warning"></div>
    <div id="unity-footer">
      <div id="unity-logo-title-footer"></div>
      <div id="unity-fullscreen-button"></div>
      <div id="unity-build-title">Frigo Chouinard</div>
    </div>
  </div>
</section>

<script>
  var canvas = document.querySelector("#unity-canvas");
  function unityShowBanner(msg, type) {
    var warningBanner = document.querySelector("#unity-warning");
    var div = document.createElement('div');
    div.innerHTML = msg;
    warningBanner.appendChild(div);
    if(type=='error') div.style='background:red;padding:10px;';
    else { if(type=='warning') div.style='background:yellow;padding:10px;'; setTimeout(()=>{ warningBanner.removeChild(div); },5000); }
  }
  var buildUrl = "Frigo/Build";
  var loaderUrl = buildUrl + "/WebGL.loader.js";
  var config = {
    dataUrl: buildUrl + "/WebGL.data.br",
    frameworkUrl: buildUrl + "/WebGL.framework.js.br",
    codeUrl: buildUrl + "/WebGL.wasm.br",
    streamingAssetsUrl: "StreamingAssets",
    companyName: "DefaultCompany",
    productName: "Frigo Chouinard",
    productVersion: "1.0",
    showBanner: unityShowBanner,
  };
  document.querySelector("#unity-loading-bar").style.display = "block";
  var script = document.createElement("script");
  script.src = loaderUrl;
  script.onload = () => {
    createUnityInstance(canvas, config, progress => {
      document.querySelector("#unity-progress-bar-full").style.width = 100*progress+"%";
    }).then(unityInstance => {
      document.querySelector("#unity-loading-bar").style.display="none";
      document.querySelector("#unity-fullscreen-button").onclick = ()=>unityInstance.SetFullscreen(1);
    }).catch(message=>alert(message));
  };
  document.body.appendChild(script);
</script>
