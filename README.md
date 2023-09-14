# Shapefile.js

這個專案是來自 calvinmetcalf 的 [shapefile-js](https://github.com/calvinmetcalf/shapefile-js) ，感謝 calvinmetcalf

這個專案在原版的基礎上增加了一個功能：允許使用者指定 dbf 檔的編碼方式。這個功能已經在使用 Big5 編碼時經過測試和驗證。如果您需要使用其他編碼，可能需要自行驗證。

## Usage

* 直接下載本專案 `/dist/` 下的 [shp.js](https://github.com/Rainbowrain-TW/shapefile-js/blob/main/dist/shp.js)

如果你需要使用 whitelist 這個參數, 請作為第三個參數

```javascript
shp(arrayBuffer, encoding).then(function(geojsonData){ /** do something with geojson */ });
```

## Example

HTML

```html
		<!-- 在 head 中引用 shp.js -->
		<script src="./js/shp.js"></script>
		<!-- ...其他程式碼... -->
        <div id="gisPanel">
            <input type="file" id="shpfileInput" onchange="fileSelected()" accept=".zip" multiple>
            <button onclick="readShapefile()">Read Shapefile</button>            
        </div>
		<!-- ...其他程式碼... -->
```

JavaScript

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

    // 使用 shpjs 解析 Shapefile Zip 並指定 dbf 檔的編碼為 Big5 
    shp(arrayBuffer, "Big5").then(function(geojsonData){
      console.log('geojsonData :>> ', geojsonData);

	  /** do things with geojsonData ... */      
    });
  };

  reader.onerror = function() {
    alert("讀取文件時出錯");
  };

  reader.readAsArrayBuffer(file);
}

function fileSelected() {    
  const files = fileInput.files;
  if (files.length > 0) {

    // 顯示檔案資訊
    const file = files[0];
    console.log("file :>> ", file);
    console.log("file.name :>> ", file.name);
    console.log("file.type :>> ", file.type);
    console.log("file.size :>> ", file.size);
    console.log("file.lastModifiedDate :>> ", file.lastModifiedDate);    
  }
}
```

### LICENSE
這個專案是基於 shapefile-js 修改的，遵循原專案的MIT許可證。詳細的許可證文本可以在 [這裡](https://github.com/calvinmetcalf/shapefile-js) 找到。