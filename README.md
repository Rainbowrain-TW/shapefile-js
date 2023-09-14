# Shapefile.js

這個 repo 是來自 calvinmetcalf 的 [shapefile-js](https://github.com/calvinmetcalf/shapefile-js) ，感謝 calvinmetcalf

這個 repo 只多了一個功能
．使用 shp 時可以增加一個字串參數作為 dbf 檔的 encoding

## Usage

```javascript
shp(arrayBuffer, encoding).then(function(geojsonData){ /** do something with geojson */ });
```

## Example

```html
        <div id="gisPanel">
            <input type="file" id="shpfileInput" onchange="fileSelected()" accept=".zip" multiple>
            <button onclick="readShapefile()">Read Shapefile</button>            
        </div>
```

```javascript
function readShapefile() {
  const inputElement = document.getElementById('shpfileInput');
  const files = inputElement.files;

  if (files.length === 0) {
    alert("請先選擇 Shapefile（壓縮成 .zip 格式）");
    return;
  }

  const file = files[0];
  const reader = new FileReader();

  reader.onload = function(e) {
    const arrayBuffer = e.target.result;

    // 使用 shpjs 解析 Shapefile
    shp(arrayBuffer, "Big5").then(function(geojsonData){
      console.log('geojsonData :>> ', geojsonData);
      
    });
  };

  reader.onerror = function() {
    alert("讀取文件時出錯");
  };

  reader.readAsArrayBuffer(file);
}

function fileSelected() {    
  var files = fileInput.files;
  if (files.length > 0) {

    // 顯示檔案資訊
    var file = files[0];
    console.log("file :>> ", file);
    console.log("file.name :>> ", file.name);
    console.log("file.type :>> ", file.type);
    console.log("file.size :>> ", file.size);
    console.log("file.lastModifiedDate :>> ", file.lastModifiedDate);    
  }
}
```