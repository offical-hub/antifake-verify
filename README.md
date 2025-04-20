<!DOCTYPE html>
<html lang="zh">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>防伪查询</title>
  <style>
    body {
      font-family: "Microsoft YaHei", Arial, sans-serif;
      background-color: #f0f0f0;
      margin: 0;
      padding: 20px;
    }
    .container {
      max-width: 800px;
      margin: auto;
      background: #fff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    h2 {
      color: #333;
      font-size: 20px;
    }
    .top-image {
      width: 100%;
      max-height: 100px;
      object-fit: contain;
      margin-bottom: 15px;
    }
    .code-group {
      font-size: 20px;
      font-weight: bold;
      margin: 10px 0;
      letter-spacing: 4px;
      word-wrap: break-word;
    }
    .color-0 { color: #008000; }
    .color-1 { color: #b4005a; }
    .color-2 { color: #000000; }
    .color-3 { color: #0096ff; }
    .qr-area {
      margin-top: 25px;
      text-align: center;
    }
    .qr-note {
      margin-top: 10px;
      font-size: 14px;
      color: #555;
    }
    .qr-legend {
      margin-top: 15px;
      font-size: 14px;
      color: #333;
    }
    .legend-box {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      margin-top: 10px;
      gap: 12px;
    }
    .legend-item {
      display: flex;
      align-items: center;
      gap: 6px;
    }
    .color-box {
      width: 14px;
      height: 14px;
      display: inline-block;
      border-radius: 3px;
    }
    img.qr-generated {
      width: 180px;
      height: 180px;
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <div class="container">
    <img class="top-image" src="logo.jpg" alt="品牌Logo" />

    <h2>防伪查询</h2>
    <p>尊敬的用户您好，</p>
    <p>你所查询的16位防伪码为：</p>

    <div id="codeContainer">
      <div class="code-group" id="line1"></div>
      <div class="code-group" id="line2"></div>
    </div>

    <p>此防伪码正确。感谢您的查询！</p>
    <p>首次查询时间：<span id="timestamp">加载中...</span></p>
    <p>原产地：美国</p>
    <p style="color: red;">请核对16位防伪码及二维码的颜色。</p>

    <!-- 新增的二维码图像 -->
    <div class="qr-area">
      <img class="qr-generated" src="https://api.qrserver.com/v1/create-qr-code/?size=200x200&data=https://offical-hub.github.io/antifake-verify/" alt="跳转二维码" />
      <div class="qr-note">↑ 手机扫码可跳转防伪验证页面</div>

      <div class="qr-legend">
        <div class="legend-box">
          <div class="legend-item"><span class="color-box" style="background:#008000;"></span> 左上：绿色</div>
          <div class="legend-item"><span class="color-box" style="background:#b4005a;"></span> 右上：红紫</div>
          <div class="legend-item"><span class="color-box" style="background:#000000;"></span> 左下：黑色</div>
          <div class="legend-item"><span class="color-box" style="background:#0096ff;"></span> 右下：蓝色</div>
        </div>
      </div>
    </div>
  </div>

  <script>
    const params = new URLSearchParams(window.location.search);
    const code = params.get("code");

    const colorMap = ["color-0", "color-1", "color-2", "color-3"];
    const colorSeq = [
      [0, 1, 2, 3],
      [1, 2, 3, 0],
      [2, 3, 0, 1],
      [3, 0, 1, 2]
    ];

    function renderCode(codeStr) {
      if (!codeStr || codeStr.length !== 16) {
        document.getElementById("line1").textContent = "防伪码无效";
        return;
      }

      const line1 = document.getElementById("line1");
      const line2 = document.getElementById("line2");

      line1.innerHTML = "";
      line2.innerHTML = "";

      for (let i = 0; i < 8; i++) {
        const span = document.createElement("span");
        const group = Math.floor(i / 4);
        const colorClass = colorMap[colorSeq[group][i % 4]];
        span.className = colorClass;
        span.textContent = codeStr[i];
        line1.appendChild(span);
      }

      for (let i = 8; i < 16; i++) {
        const span = document.createElement("span");
        const group = Math.floor((i - 8) / 4) + 2;
        const colorClass = colorMap[colorSeq[group][i % 4]];
        span.className = colorClass;
        span.textContent = codeStr[i];
        line2.appendChild(span);
      }
    }

    function getCurrentTime() {
      const now = new Date();
      const yyyy = now.getFullYear();
      const mm = String(now.getMonth() + 1).padStart(2, '0');
      const dd = String(now.getDate()).padStart(2, '0');
      const hh = String(now.getHours()).padStart(2, '0');
      const mi = String(now.getMinutes()).padStart(2, '0');
      return `${yyyy}-${mm}-${dd} ${hh}:${mi}`;
    }

    renderCode(code);
    document.getElementById("timestamp").textContent = getCurrentTime();
  </script>
</body>
</html>

