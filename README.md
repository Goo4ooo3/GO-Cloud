<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>محرر الكود البرمجي</title>
    <!-- تحميل ملفات CSS الخاصة بـ CodeMirror -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.5/codemirror.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.5/theme/dracula.min.css">
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            height: 100vh;
            background-color: #1e1e1e; /* خلفية داكنة مشابهة لـ VS Code */
            color: #d4d4d4; /* لون النص مشابه لـ VS Code */
        }
        .editor-container {
            width: 90%;
            max-width: 800px;
            background-color: #1e1e1e; /* خلفية المحرر مشابهة لـ VS Code */
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
            border-radius: 8px;
            overflow: hidden;
            margin-top: 20px;
        }
        .CodeMirror {
            height: 70vh;
            background-color: #1e1e1e; /* خلفية المحرر مشابهة لـ VS Code */
            color: #d4d4d4; /* لون النص مشابه لـ VS Code */
        }
        .buttons {
            margin-top: 10px;
            display: flex;
            gap: 10px;
        }
        .button {
            padding: 10px 20px;
            background-color: #007acc; /* لون مشابه لأزرار VS Code */
            color: #fff;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        .button:hover {
            background-color: #005f99;
        }
    </style>
</head>
<body>
    <div class="editor-container">
        <textarea id="code-editor">// اكتب كودك هنا...</textarea>
    </div>
    <div class="buttons">
        <button class="button" onclick="saveFile()">حفظ الملف</button>
        <button class="button" onclick="openFile()">فتح ملف</button>
    </div>

    <!-- تحميل مكتبة CodeMirror وملحقاتها -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.5/codemirror.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.5/mode/javascript/javascript.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.5/mode/python/python.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.5/mode/xml/xml.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.5/mode/css/css.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.5/mode/htmlmixed/htmlmixed.min.js"></script>
    <script>
        // تهيئة محرر CodeMirror
        var editor = CodeMirror.fromTextArea(document.getElementById('code-editor'), {
            mode: "javascript", // يمكنك تغيير الوضع إلى "python" أو "htmlmixed" أو "css"
            lineNumbers: true,
            theme: "dracula", // يمكنك تغيير الثيم إلى "default" أو أي ثيم آخر من CodeMirror
            matchBrackets: true,
            autoCloseBrackets: true
        });

        // دالة لحفظ الملف
        function saveFile() {
            var content = editor.getValue();
            var blob = new Blob([content], { type: "text/plain;charset=utf-8" });
            var url = URL.createObjectURL(blob);
            var a = document.createElement("a");
            a.style.display = "none";
            a.href = url;
            a.download = "index.html"; // يمكنك تغيير اسم الملف والامتداد هنا
            document.body.appendChild(a);
            a.click();
            window.URL.revokeObjectURL(url);
        }

        // دالة لفتح ملف
        function openFile() {
            var input = document.createElement("input");
            input.type = "file";
            input.accept = ".txt,.js,.html,.css,.py"; // يمكنك تعديل الامتدادات المقبولة هنا
            input.onchange = function(event) {
                var file = event.target.files[0];
                if (file) {
                    var reader = new FileReader();
                    reader.onload = function(e) {
                        editor.setValue(e.target.result);
                    };
                    reader.readAsText(file);
                }
            };
            input.click();
        }
    </script>
</body>
</html>
