# JavaScript Async Await

在現代的網頁和應用程式開發中，非同步程式設計是不可或缺的一部分。它允許程式在等待某個長時間操作（例如網絡請求）完成時繼續執行其他任務，從而提高應用的響應性和效能。

JavaScript 提供了幾種處理非同步操作的方法，其中最常用的是 Promises 和 Async/Await。

## Outline 

- 異步與同步編程
- Promise 是什麼
- Async Await 是什麼
- Async Await 的好處

## 異步與同步編程

同步指的是在程式執行過程中，任務按照碼順序逐一執行，每一項任務的啟動都需等待前一項任務完成後才能進行。這種模式下，任何執行耗時的操作都會導致程式暫停執行，直至該操作完成。換句話說，同步操作的執行方式是線性的、順序的，易於理解和預測，但在處理耗時任務時可能會導致效率低下。

異步允許在等待耗時操作（如網絡請求、文件讀寫等）的完成期間，程式可以繼續執行後續的任務，而不是無謂地等待。這意味著異步操作可以在背景中進行，一旦完成，就會通過回調函數、Promises 或 Async/Await 等機制返回結果。異步編程是非阻塞的，能夠提高應用程序的響應性和效率，特別是在處理I/O密集型任務時。

    ```javascript
    // 同步編程
    let a = 1 
    let b = 2 

    // 100ms 後執行
    setTimeout(function() {
        console.log('Timeout:' + a)
    }, 100)

    a = 10 

    fetch('/').then(function () {
        console.log('Fetch')
    })

    dconosle.log('Synchronous')

    conosol.log(a)
    console.log(b)
    
    // Synchronous 10 2 Fetch Timeout: 10
    ```


## Promise 是什麼

Promise 是 JavaScript 中用於非同步運算的一個對象。它代表了一個將要完成或失敗的操作和它的結果值。Promise 有三種狀態：

- Pending（等待中）：初始狀態，非同步操作尚未完成也未被拒絕。
- Fulfilled（已實現）：意味著操作成功完成。
- Rejected（已拒絕）：意味著操作失敗。 

使用 Promise 主要透過其構造函數來創建，並提供兩個方法：resolve（成功時調用）和 reject（失敗時調用）。透過 .then() 方法來處理成功的情況，用 .catch() 方法來處理錯誤。

## Async Await 是什麼

async 和 await 是建立在 Promise 上的語法糖，使非同步操作代碼更加簡潔易讀。async 關鍵字用於聲明一個函數是異步的，表示該函數的執行將返回一個 Promise。await 關鍵字用於等待一個 Promise 對象解決，只能在 async 函數內部使用。

在一個 async 函數中，你可以使用 await 關鍵字來等待 Promise 的解決，從而使非同步代碼看起來像同步代碼一樣易於理解和管理

## Async Await 的好處

- 簡化代碼: 使用 Async/Await 可以使非同步代碼的結構更清晰，減少了 .then() 和 .catch() 的鏈式調用，使代碼更加直觀和易於理解。

- 錯誤處理: Async/Await 使得使用傳統的 try/catch 語法來處理非同步操作中的錯誤成為可能，這讓錯誤處理更加直觀和方便。

## Code Example

```javascript
function makeRequest(location) {
    return new Promise((resolve, reject) => {
        console.log(`Making request to ${location}`);
        if (location === 'Google') {
            resolve('Google says hi');
        } else {
            reject('We can only talk to Google');
        }
    })
}

function processRequest(response) {
    return new Promise((resolve, reject) => {
        console.log('Processing response');
        resolve(`Extra Information + ${response}`);
    })
}
```

- Promise

```javascript
 makeRequest('Facebook').then(response => {
     console.log('Response received');
     return processRequest(response);
 }).then(processResponse => {
     console.log(processResponse);
 }).catch(err => {
     console.log(err);
 })
```

- Async Await

```javascript
sync function doWork() {
    try {
        const response = await makeRequest('Facebook');
        console.log('Response received');
        const processedResponse = await processRequest(response);
        console.log(processedResponse);
    } catch (err) {
        console.log(err);
    }    
}

doWork();
```

以上，我們可以看到使用 Async/Await 的代碼更加簡潔易讀，並且錯誤處理更加直觀。
