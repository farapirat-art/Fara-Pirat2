<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Удостоверение личности</title>
    <style>
        * { box-sizing: border-box; }
        body { 
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; 
            background-color: #f8f9fa; margin: 0; display: flex; flex-direction: column; height: 100vh; color: #333;
        }

        /* Шапка с кнопкой назад */
        .header { 
            display: flex; align-items: center; padding: 15px; background: white; position: relative;
        }
        .back-btn { 
            font-size: 24px; cursor: pointer; background: none; border: none; padding: 0 10px; color: #333;
        }
        .title { flex-grow: 1; text-align: center; font-weight: 600; font-size: 17px; margin-right: 34px; }

        /* Вкладки (Tabs) */
        .tabs { 
            display: flex; background: #eee; margin: 10px 15px; border-radius: 10px; padding: 2px;
        }
        .tab { 
            flex: 1; text-align: center; padding: 8px; font-size: 14px; border-radius: 8px; cursor: pointer; color: #666;
        }
        .tab.active { background: white; color: #000; box-shadow: 0 2px 4px rgba(0,0,0,0.1); font-weight: 500; }

        /* Центральная часть */
        .content { 
            flex-grow: 1; display: flex; flex-direction: column; justify-content: center; align-items: center; padding: 20px;
        }
        
        /* Кнопка в центре */
        .upload-area {
            width: 100%; max-width: 320px; height: 200px; border: 2px dashed #ccc; border-radius: 15px;
            display: flex; flex-direction: column; justify-content: center; align-items: center;
            cursor: pointer; background: #fff; transition: 0.3s;
        }
        .upload-area:hover { border-color: #0089d0; background: #f0faff; }
        .upload-icon { font-size: 40px; color: #0089d0; margin-bottom: 10px; }
        
        #preview { 
            width: 100%; height: 100%; object-fit: contain; border-radius: 12px; display: none; 
        }

        /* Подвал с кнопками */
        .footer { padding: 20px; background: white; }
        .btn { 
            width: 100%; padding: 14px; border-radius: 12px; border: none; font-size: 16px; font-weight: 600; 
            margin-bottom: 10px; cursor: pointer; display: flex; align-items: center; justify-content: center; gap: 8px;
        }
        .btn-blue { background-color: #0089d0; color: white; }
        .btn-outline { background-color: white; color: #0089d0; border: 1.5px solid #0089d0; }

        input[type="file"] { display: none; }
    </style>
</head>
<body>

    <div class="header">
        <button class="back-btn" onclick="alert('Назад')">←</button>
        <div class="title">Удостоверение личности</div>
    </div>

    <div class="tabs">
        <div class="tab active">Документ</div>
        <div class="tab">Реквизиты</div>
    </div>

    <div class="content">
        <input type="file" id="fileInput" accept="image/*">
        <div class="upload-area" id="dropZone" onclick="document.getElementById('fileInput').click()">
            <div id="upload-ui">
                <div class="upload-icon">📷</div>
                <div style="color: #0089d0; font-weight: 500;">Нажмите, чтобы сделать фото</div>
            </div>
            <img id="preview" src="" alt="Ваше фото">
        </div>
        <p id="error-text" style="color: #888; font-size: 13px; margin-top: 15px;">Failed to load file.</p>
    </div>

    <div class="footer">
        <button class="btn btn-blue" onclick="document.getElementById('fileInput').click()">
            📄 Предъявить документ
        </button>
        <button class="btn btn-outline">
            📤 Отправить документ
        </button>
    </div>

    <script>
        const fileInput = document.getElementById('fileInput');
        const preview = document.getElementById('preview');
        const uploadUI = document.getElementById('upload-ui');
        const errorText = document.getElementById('error-text');
        const dropZone = document.getElementById('dropZone');

        fileInput.addEventListener('change', function() {
            const file = this.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    preview.src = e.target.result;
                    preview.style.display = 'block';
                    uploadUI.style.display = 'none';
                    errorText.style.display = 'none';
                    dropZone.style.border = 'none'; // Убираем рамку после загрузки
                }
                reader.readAsDataURL(file);
            }
        });
    </script>

</body>
</html>
