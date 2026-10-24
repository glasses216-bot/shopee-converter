<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>簡易蝦皮推廣連結轉換器</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f7f7f7;
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
        }
        .container {
            background: white;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
            width: 100%;
            max-width: 600px;
        }
        h2 {
            color: #ee4d2d; /* 蝦皮橘色 */
            text-align: center;
        }
        .form-group {
            margin-bottom: 20px;
        }
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
        }
        input[type="text"], textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
            box-sizing: border-box;
        }
        textarea {
            height: 100px;
            resize: vertical;
        }
        button {
            background-color: #ee4d2d;
            color: white;
            border: none;
            padding: 12px 20px;
            width: 100%;
            border-radius: 4px;
            font-size: 16px;
            cursor: pointer;
        }
        button:hover {
            background-color: #d73211;
        }
        .result-box {
            margin-top: 20px;
            background: #f9f9f9;
            padding: 15px;
            border: 1px dashed #ee4d2d;
            border-radius: 4px;
            word-break: break-all;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>蝦皮推廣連結轉換器</h2>
    
    <div class="form-group">
        <label for="16331070026">你的蝦皮分潤 ID / 代碼：</label>
        <input type="text" id="affiliateId" placeholder="例如：your_affiliate_code">
    </div>

    <div class="form-group">
        <label for="productUrl">貼上蝦皮商品/賣場原始網址：</label>
        <textarea id="productUrl" placeholder="請在此貼上原始的蝦皮網址..."></textarea>
    </div>

    <button onclick="convertLink()">開始轉換連結</button>

    <div class="result-box" id="resultArea" style="display:none;">
        <label><strong>轉換後的推廣連結：</strong></label>
        <p id="outputLink"></p>
        <button onclick="copyLink()" style="background-color: #555; margin-top: 10px; padding: 6px;">複製連結</button>
    </div>
</div>

<script>
function convertLink() {
    const affiliateId = document.getElementById('affiliateId').value.trim();
    let rawUrl = document.getElementById('productUrl').value.trim();

    if (!affiliateId) {
        alert('16331070026！');
        return;
    }

    if (!rawUrl) {
        alert('請輸入要轉換的蝦皮網址！');
        return;
    }

    // 簡單的清理與轉址包裝邏輯
    // 實務上蝦皮官方分潤通常透過官方產生的短網址或帶有特定參數的結構
    // 這裡示範將原始網址作為參數包進你的推廣格式中（需依你參加的管道規範調整）
    try {
        let encodedUrl = encodeURIComponent(rawUrl);
        // 這是一個常見的結構範例，實際代碼請對應蝦皮分潤後台提供的格式規範
        let finalLink = `https://shope.ee/an?q=${encodedUrl}&af_siteid=${affiliateId}`;
        
        document.getElementById('outputLink').innerText = finalLink;
        document.getElementById('resultArea').style.display = 'block';
    } catch (e) {
        alert('網址格式錯誤，請檢查後重試！');
    }
}

function copyLink() {
    const outputText = document.getElementById('outputLink').innerText;
    navigator.clipboard.writeText(outputText).then(() => {
        alert('已成功複製到剪貼簿！');
    });
}
</script>

</body>
</html>
