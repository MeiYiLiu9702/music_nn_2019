下載Youtube Audio Library的免費音樂
===
### [Youtube Aduio Library 網址](https://www.youtube.com/audiolibrary/music)

### 目的
希望透過HTTP GET的方式，請求API獲取存放音樂相關資訊的json檔案。

### API
`https://www.youtube.com/audioswap_ajax?action_get_tracks=1&ads=false&dl=true&s=music&mr=25&si=0&qid=0&sh=true`

### 實作的困難
需要在google登入的狀態下才能進行檔案的下載

### 解法
1. 直接在cilend side console運行javascript即可。
2. 透過python selenium自動開啟網頁，並執行javascript。
3. 透過python selenium自動開啟網頁，控制scroll載入資料，抓取HTML標籤。

### JavaScript download function
reference: [Using HTML5/JavaScript to generate and save a file](https://stackoverflow.com/questions/2897619/using-html5-javascript-to-generate-and-save-a-file)

```javascript
function download(filename, text) {
    var pom = document.createElement('a');
    pom.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(text));
    pom.setAttribute('download', filename);

    if (document.createEvent) {
        var event = document.createEvent('MouseEvents');
        event.initEvent('click', true, true);
        pom.dispatchEvent(event);
    }
    else {
        pom.click();
    }
}
```

### JavaScript Fetch API

```javascript
var data = undefined;

fetch('https://www.youtube.com/audioswap_ajax?action_get_tracks=1&ads=false&dl=true&s=music&mr=25&si=0&qid=0&sh=true')
  .then(function(response) {
    return response.json();
  })
  .then(function(myJson) {
    console.log(myJson);
	data = myJson;
  });
```

### Save data to .json

```javascript 
download('test.json',JSON.stringify(data))
```


### 安裝 selenium
```
pip install selenium
```

### 下載google driver
[download link](http://chromedriver.storage.googleapis.com/index.html?path=2.22/)