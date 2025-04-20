<!DOCTYPE html>
<html lang="zh">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>防伪查询</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
      background-color: #f5f5f5;
      color: #333;
      line-height: 1.5;
      padding: 0;
    }
    
    .container {
      width: 100%;
      max-width: 100%;
      margin: 0 auto;
      background: #fff;
      min-height: 100vh;
      padding: 15px;
    }
    
    .header {
      text-align: center;
      margin-bottom: 20px;
    }
    
    .logo {
      width: 100%;
      max-width: 300px;
      height: auto;
      margin: 0 auto 15px;
      display: block;
    }
    
    .title {
      font-size: 22px;
      font-weight: bold;
      color: #333;
      margin-bottom: 15px;
      text-align: center;
    }
    
    .result-card {
      background: #fff;
      border-radius: 12px;
      padding: 20px;
      margin-bottom: 20px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.05);
    }
    
    .code-container {
      margin: 20px 0;
    }
    
    .code-row {
      display: flex;
      justify-content: center;
      margin-bottom: 10px;
    }
    
    .code-digit {
      font-size: 24px;
      font-weight: bold;
      width: 30px;
      text-align: center;
      margin: 0 2px;
    }
    
    .color-0 { color: #008000; } /* 绿色 */
    .color-1 { color: #b4005a; } /* 红紫 */
    .color-2 { color: #000000; } /* 黑色 */
    .color-3 { color: #0096ff; } /* 蓝色 */
    
    .qr-container {
      text-align: center;
      margin: 25px 0;
    }
    
    .qr-image {
      width: 200px;
      height: 200px;
      margin: 0 auto;
      display: block;
    }
    
    .qr-note {
      font-size: 14px;
      color: #666;
      margin-top: 10px;
    }
    
    .info-item {
      margin-bottom: 10px;
      font-size: 15px;
    }
    
    .info-label {
      font-weight: bold;
      color: #555;
    }
    
    .warning {
      color: #e74c3c;
      font-weight: bold;
      margin: 15px 0;
    }
    
    .legend-container {
      margin-top: 25px;
      padding: 15px;
      background: #f9f9f9;
      border-radius: 10px;
    }
    
    .legend-title {
      font-size: 16px;
      font-weight: bold;
      margin-bottom: 10px;
      text-align: center;
    }
    
    .legend-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
    }
    
    .legend-item {
      display: flex;
      align-items: center;
      font-size: 14px;
    }
    
    .color-box {
      width: 16px;
      height: 16px;
      border-radius: 3px;
      margin-right: 8px;
    }
    
    /* 响应式调整 */
    @media (max-width: 400px) {
      .code-digit {
        font-size: 20px;
        width: 24px;
      }
      
      .qr-image {
        width: 180px;
        height: 180px;
      }
      
      .legend-grid {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="header">
      <img class="logo" src="logo.jpg" alt="品牌Logo" onerror="this.style.display='none'">
      <h1 class="title">防伪查询结果</h1>
    </div>
    
    <div class="result-card">
      <p class="info-item">尊敬的用户您好，</p>
      <p class="info-item">您所查询的16位防伪码为：</p>
      
      <div class="code-container">
        <div class="code-row" id="line1"></div>
        <div class="code-row" id="line2"></div>
      </div>
      
      <p class="info-item">此防伪码<span style="color:#27ae60;font-weight:bold;">正确</span>。感谢您的查询！</p>
      
      <div class="info-item">
        <span class="info-label">首次查询时间：</span>
        <span id="timestamp">加载中...</span>
      </div>
      
      <div class="info-item">
        <span class="info-label">原产地：</span>
        <span>美国</span>
      </div>
      
      <p class="warning">请核对16位防伪码及二维码的颜色。</p>
      
      <div class="qr-container">
        <img id="qrImage" class="qr-image" src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyMDAiIGhlaWdodD0iMjAwIiB2aWV3Qm94PSIwIDAgMjAwIDIwMCI+PHJlY3Qgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgZmlsbD0id2hpdGUiLz48dGV4dCB4PSI1MCUiIHk9IjUwJSIgZm9udC1mYW1pbHk9IkFyaWFsIiBmb250LXNpemU9IjE0IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBhbGlnbm1lbnQtYmFzZWxpbmU9Im1pZGRsZSIgZmlsbD0iIzMzMyI+UXIgQ29kZSBQbGFjZWhvbGRlcjwvdGV4dD48L3N2Zz4=" alt="二维码">
        <p class="qr-note">请确保二维码与防伪码颜色一致</p>
      </div>
    </div>
    
    <div class="legend-container">
      <div class="legend-title">二维码四象限颜色说明</div>
      <div class="legend-grid">
        <div class="legend-item">
          <div class="color-box" style="background:#008000;"></div>
          <span>左上：绿色</span>
        </div>
        <div class="legend-item">
          <div class="color-box" style="background:#b4005a;"></div>
          <span>右上：红紫</span>
        </div>
        <div class="legend-item">
          <div class="color-box" style="background:#000000;"></div>
          <span>左下：黑色</span>
        </div>
        <div class="legend-item">
          <div class="color-box" style="background:#0096ff;"></div>
          <span>右下：蓝色</span>
        </div>
      </div>
    </div>
  </div>

  <script>
    // 获取URL中的防伪码参数
    const params = new URLSearchParams(window.location.search);
    const code = params.get("code");
    
    // 颜色配置
    const colorMap = ["color-0", "color-1", "color-2", "color-3"];
    const colorSeq = [
      [0, 1, 2, 3],
      [1, 2, 3, 0],
      [2, 3, 0, 1],
      [3, 0, 1, 2]
    ];
    
    // 生成彩色二维码
    function generateColoredQR(text, size = 200) {
      return new Promise((resolve) => {
        const qr = new QRCode({
          content: text,
          padding: 4,
          width: size,
          height: size,
          colorDark: "#000000",
          colorLight: "#ffffff",
          correctLevel: QRCode.CorrectLevel.H
        });
        
        const svg = qr.svg();
        const img = new Image();
        img.onload = () => resolve(img);
        img.src = 'data:image/svg+xml;base64,' + btoa(unescape(encodeURIComponent(svg)));
      });
    }
    
    // 渲染防伪码
    function renderSecurityCode(codeStr) {
      if (!codeStr || codeStr.length !== 16) {
        document.getElementById("line1").innerHTML = '<span style="color:red;">防伪码无效</span>';
        return;
      }
      
      const line1 = document.getElementById("line1");
      const line2 = document.getElementById("line2");
      
      line1.innerHTML = '';
      line2.innerHTML = '';
      
      // 第一行8位数字
      for (let i = 0; i < 8; i++) {
        const group = Math.floor(i / 4);
        const colorClass = colorMap[colorSeq[group][i % 4]];
        const digit = document.createElement("span");
        digit.className = `code-digit ${colorClass}`;
        digit.textContent = codeStr[i];
        line1.appendChild(digit);
      }
      
      // 第二行8位数字
      for (let i = 8; i < 16; i++) {
        const group = Math.floor((i - 8) / 4) + 2;
        const colorClass = colorMap[colorSeq[group][i % 4]];
        const digit = document.createElement("span");
        digit.className = `code-digit ${colorClass}`;
        digit.textContent = codeStr[i];
        line2.appendChild(digit);
      }
    }
    
    // 显示当前时间
    function showCurrentTime() {
      const now = new Date();
      const options = { 
        year: 'numeric', 
        month: '2-digit', 
        day: '2-digit', 
        hour: '2-digit', 
        minute: '2-digit',
        hour12: false
      };
      document.getElementById("timestamp").textContent = now.toLocaleString('zh-CN', options);
    }
    
    // 页面加载完成后执行
    document.addEventListener('DOMContentLoaded', () => {
      showCurrentTime();
      
      if (code) {
        renderSecurityCode(code);
        
        // 生成二维码（实际应用中应从后端获取）
        const qrText = `https://your-domain.com/verify?code=${code}`;
        generateColoredQR(qrText).then(img => {
          document.getElementById("qrImage").src = img.src;
        });
      } else {
        document.getElementById("line1").innerHTML = '<span style="color:red;">未提供防伪码</span>';
      }
    });
  </script>
  
  <!-- QRCode生成库 -->
  <script src="https://cdn.jsdelivr.net/npm/qrcode-svg@1.0.0/dist/qrcode.min.js"></script>
</body>
</html>
