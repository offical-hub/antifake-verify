<!DOCTYPE html>
<html lang="zh">
<head>
  <meta charset="UTF-8">
  <title>防伪验证系统</title>
  <style>
    body {
      font-family: "Microsoft YaHei", Arial, sans-serif;
      background-color: #f0f0f0;
      padding: 40px;
    }
    .container {
      max-width: 800px;
      margin: auto;
      background: #fff;
      padding: 30px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    h2 {
      color: #333;
    }
    .top-image {
      width: 100%;
      max-height: 120px;
      object-fit: contain;
      margin-bottom: 20px;
    }
    .code-group {
      font-size: 22px;
      font-weight: bold;
      margin: 10px 0;
      letter-spacing: 4px;
    }
    .color-0 { color: #008000; }   /* 绿色 */
    .color-1 { color: #b4005a; }   /* 红紫 */
    .color-2 { color: #000000; }   /* 黑色 */
    .color-3 { color: #0096ff; }   /* 蓝色 */
    .qr-area {
      margin-top: 30px;
      text-align: center;
    }
    .qr-note {
      margin-top: 10px;
      font-size: 14px;
      color: #555;
    }
    .qr-legend {
      margin-top: 20px;
      font-size: 14px;
      color: #333;
    }
    .legend-box {
      display: flex;
      justify-content: center;
      margin-top: 10px;
      gap: 20px;
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
  </style>
</head>
<body>
  <div class="container">
    <!-- 顶部图片 Logo 或 Banner -->
    <img class="top-image" src="logo.jpg" alt="品牌Logo">

    <h2>防伪码验证结果</h2>
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

    <div class="qr-area">
      <img id="qrImage" src="qrcode-placeholder.png" alt="二维码" width="200" height="200">
      <div class="qr-note">请确保二维码与防伪码颜色一致</div>
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

    // 渲染内容
    renderCode(code);
    document.getElementById("timestamp").textContent = getCurrentTime();
  </script>
</body>
</html>
