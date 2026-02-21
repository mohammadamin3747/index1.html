<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>پایگاه سایبری محمدامین</title>
    <style>
        :root { --main-color: #00ff41; --bg-color: #0d0d0d; --chat-bg: #1a1a1a; }
        body { background-color: var(--bg-color); color: var(--main-color); font-family: 'Segoe UI', Tahoma, sans-serif; display: flex; flex-direction: column; align-items: center; justify-content: center; height: 100vh; margin: 0; overflow: hidden; }
        
        /* افکت ماتریکسی در پس‌زمینه */
        .header-title { font-size: 1.5rem; text-shadow: 0 0 10px var(--main-color); margin-bottom: 20px; letter-spacing: 2px; }

        .chat-container { width: 400px; height: 550px; background: var(--chat-bg); border: 1px solid var(--main-color); border-radius: 15px; display: flex; flex-direction: column; box-shadow: 0 0 30px rgba(0, 255, 65, 0.2); }
        .status-bar { padding: 10px; font-size: 12px; border-bottom: 1px solid #333; display: flex; justify-content: space-between; background: #222; border-radius: 15px 15px 0 0; }
        
        .messages { flex: 1; padding: 15px; overflow-y: auto; display: flex; flex-direction: column; gap: 12px; scrollbar-width: thin; scrollbar-color: var(--main-color) transparent; }
        .msg { padding: 10px 15px; border-radius: 12px; font-size: 14px; line-height: 1.5; max-width: 85%; position: relative; }
        .received { background: #333; color: #fff; align-self: flex-start; border-bottom-right-radius: 2px; }
        .sent { background: var(--main-color); color: #000; align-self: flex-end; border-bottom-left-radius: 2px; font-weight: bold; }

        .input-area { padding: 15px; background: #222; display: flex; gap: 10px; border-radius: 0 0 15px 15px; }
        input { flex: 1; background: #000; border: 1px solid #444; padding: 12px; color: var(--main-color); border-radius: 5px; outline: none; }
        input:focus { border-color: var(--main-color); }
        button { background: var(--main-color); border: none; color: black; padding: 0 20px; border-radius: 5px; cursor: pointer; font-weight: bold; transition: 0.3s; }
        button:hover { background: #00cc33; box-shadow: 0 0 10px var(--main-color); }

        /* سیستم هشدار */
        #alert-box { color: #ff4444; font-size: 12px; margin-top: 5px; display: none; }
    </style>
</head>
<body>

<div class="header-title">MOHAMMAD AMIN TERMINAL v1.0</div>

<div class="chat-container">
    <div class="status-bar">
        <span>وضعیت: متصل (Secure)</span>
        <span>IP: 127.0.0.1</span>
    </div>
    <div class="messages" id="chatBox">
        <div class="msg received">خوش آمدید اعلی‌حضرت. سیستم آماده دریافت دستورات است.</div>
    </div>
    <div class="input-area">
        <div style="display: flex; flex-direction: column; width: 100%;">
            <div style="display: flex; gap: 10px;">
                <input type="text" id="userMsg" placeholder="تایپ کنید...">
                <button onclick="sendMessage()">ارسال</button>
            </div>
            <div id="alert-box">⚠️ هشدار: کاراکتر غیرمجاز شناسایی شد! (محافظت کلاه خاکستری)</div>
        </div>
    </div>
</div>

<script>
    function sendMessage() {
        const input = document.getElementById("userMsg");
        const chatBox = document.getElementById("chatBox");
        const alertBox = document.getElementById("alert-box");
        const val = input.value;

        // سیستم تشخیص نفوذ (IDS) ساده برای کلاه خاکستری‌ها
        const illegalChars = ["<", ">", "script", "DROP", "SELECT"];
        let isSafe = true;

        illegalChars.forEach(char => {
            if (val.includes(char)) isSafe = false;
        });

        if (!isSafe) {
            alertBox.style.display = "block";
            setTimeout(() => { alertBox.style.display = "none"; }, 3000);
            input.value = "";
            return;
        }

        if (val.trim() !== "") {
            let newMsg = document.createElement("div");
            newMsg.className = "msg sent";
            newMsg.innerText = val;
            chatBox.appendChild(newMsg);
            input.value = "";
            chatBox.scrollTop = chatBox.scrollHeight;

            // پاسخ خودکار سیستم
            setTimeout(() => {
                let reply = document.createElement("div");
                reply.className = "msg received";
                reply.innerText = "پیام شما در دیتابیس امن ذخیره شد.";
                chatBox.appendChild(reply);
                chatBox.scrollTop = chatBox.scrollHeight;
            }, 1000);
        }
    }

    // ارسال با دکمه Enter
    document.getElementById("userMsg").addEventListener("keypress", function(e) {
        if (e.key === "Enter") sendMessage();
    });
</script>

</body>
</html>
