<div align-items="center">
<a class="header-badge" target="_blank" href="https://www.linkedin.com/in/merve-%C3%B6-5062a5260/">
    <img src="https://img.shields.io/badge/style--5eba00.svg?label=LinkedIn&logo=linkedin&style=social">
  </a>

  <a class="header-badge" target="_blank" href="https://github.com/mrvozturk">
    <img alt="Twitter Follow" src="https://img.shields.io/twitter/follow/asabeneh?style=social">
  </a>

<sub>Author:
<a href="https://www.linkedin.com/in/merve-%C3%B6-5062a5260/" target="_blank">Merve Öztürk</a><br>
<small> May, 2023</small>
</sub>
</div>

[<< Day 2](../readMe.md) | [Day 3 >>](../02_Day_Introduction_to_React/02_introduction_to_react.md)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Translate App</title>
  
</head>
<body>
  <div class="container">
    <div class="row">
      <div class="col s8">
        <div class="card">
          <div class="card-content">
            <span class="card-title">Translate App</span>
            <div class="row">
              <form id="translate-form">
                <div class="input-field col s8">
                  <input type="text" name="word" id="word" value="Nasılsın" />
                  <label for="word">Çevirilecek Kelime</label>
                </div>
                <button type="submit" class="btn col s8">Çevir</button>
              </form>
            </div>
          </div>
        </div>
        <div class="card">
          <div class="card-header">
            <img src="images/en.png" id="outputImage" height="50px" width="50px" />
            <span class="card-title" id="outputLanguage">İngilizce</span>
          </div>
          <div class="card-content">
            <h5>Çevrilen Kelime: <span id="outputWord" style="color: red;">How are you?</span></h5>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div id="google_translate_element" style="position: fixed; bottom: 200px;"></div>

</body>
</html>

```


```js
   
    body {
      font-family: Arial, sans-serif;
      background-color: #f7f7f7;
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .container {
      max-width: 600px;
      padding: 40px;
      background-color: white;
      border-radius: 10px;
      box-shadow: 0 6px 12px rgba(0, 0, 0, 0.1);
    }
    .card-title {
      font-size: 32px;
      font-weight: bold;
      margin-bottom: 30px;
      text-align: center;
    }
    .input-field {
      display: flex;
      flex-direction: column;
      margin-bottom: 30px;
    }
    .input-field label {
      font-size: 24px;
      margin-bottom: 10px;
    }
    .input-field input[type="text"] {
      font-size: 22px;
      padding: 16px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    .btn {
      background-color: #007bff;
      color: white;
      font-size: 22px;
      border: none;
      margin-bottom: 20px;
      padding: 5px 120px;
      border-radius: 5px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    .btn:hover {
      background-color: #0056b3;
    }
    .output-section {
      margin-top: 40px;
      border-top: 1px solid #ccc;
      padding-top: 40px;
    }
    .output-capture {
      font-size: 24px;
      margin-top: 20px;
      color: #007bff;
    }

```

```js
 <script type="text/javascript">
    function googleTranslateElementInit() {
      new google.translate.TranslateElement({ pageLanguage: 'en', layout: google.translate.TranslateElement.InlineLayout.SIMPLE }, 'google_translate_element');
    }
  </script>
  <script type="text/javascript"
    src="//translate.google.com/translate_a/element.js?cb=googleTranslateElementInit"></script>
  <script type="text/javascript">
    document.getElementById("translate-form").addEventListener("submit", function (event) {
      event.preventDefault();
      const word = document.getElementById("word").value;
      const outputWord = document.getElementById("outputWord");
      const outputLanguage = document.getElementById("outputLanguage");
      const translationRequest = new XMLHttpRequest();
      translationRequest.open("GET", `https://translate.googleapis.com/translate_a/single?client=gtx&sl=auto&tl=en&dt=t&q=${word}`);
      translationRequest.onreadystatechange = function () {
        if (translationRequest.readyState === 4 && translationRequest.status === 200) {
          const response = JSON.parse(translationRequest.responseText);
          const translatedText = response[0][0][0];
          outputWord.textContent = translatedText;
          const detectedLanguage = response[2];
          outputLanguage.textContent = detectedLanguage.toUpperCase();
        }
      };
      translationRequest.send();
    });
  </script>

```