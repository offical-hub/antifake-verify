<!DOCTYPE html>
<html lang="zh">
<head>
  <meta charset="UTF-8" />
  <title>防伪验证</title>
  <style>
    body {
      font-family: "微软雅黑", sans-serif;
      background-color: #f8f8f8;
      padding: 20px;
    }

    .container {
      max-width: 600px;
      background: white;
      margin: auto;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
    }

    h2 {
      text-align: center;
      color: #333;
    }

    #code-info {
      background-color: #f0f0f0;
      padding: 10px;
      margin-bottom: 10px;
      border-left: 4px solid green;
    }

    input[type="text"] {
      width: 100%;
      padding: 10px;
      margin: 15px 0;
      border: 1px solid #ccc;
      border-radius: 6px;
    }

    button {
      width: 100%;
      padding: 10px;
      background-color: #0078D7;
      color: white;
      border: none;
      border-radius: 6px;
      font-size: 16px;
    }

    #result {
      margin-top: 20px;
      font-weight: bold;
      color: #333;
    }

    .footer {
      margin-top: 30px;
      text-align: center;
      font-size: 12px;
      color: #888;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>ACANA 官方防伪验证</h2>
    <p id="code-info">扫描后自动填写防伪码</p>

    <input type="text" id="code-input" placeholder="请输入防伪码">
    <button onclick="verifyCode()">验证</button>

    <p id="result"></p>

    <div class="footer">请认准官方防伪查询系统</div>
  </div>

  <script>
    const urlParams = new URLSearchParams(window.location.search);
    const codeFromURL = urlParams.get('code');
    if (codeFromURL) {
      document.getElementById('code-info').innerText = "扫描得到的防伪码：" + codeFromURL;
      document.getElementById('code-input').value = codeFromURL;
    }

    function verifyCode() {
      const input = document.getElementById('code-input').value;
      if (input === "83921179") {
        document.getElementById('result').innerText = "验证成功：此为正品，产地：加拿大\n查询时间：" + new Date().toLocaleString();
      } else {
        document.getElementById('result').innerText = "验证失败：防伪码无效或已被使用";
      }
    }
  </script>
</body>
</html>
