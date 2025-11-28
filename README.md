# Supresa
foto
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Surpresa Especial!</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            color: #333;
            text-align: center;
            padding: 20px;
        }

        h1 {
            color: #e91e63;
            font-size: 24px;
        }

        .container {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 20px;
        }

        .heart {
            font-size: 120px;
            cursor: pointer;
            transition: transform 0.3s ease-in-out;
            margin-bottom: 30px;
            animation: pulse 1.5s infinite;
            user-select: none;
        }

        .heart:hover {
            transform: scale(1.1);
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        .imagem-oculta {
            opacity: 0;
            max-height: 0;
            overflow: hidden;
            transition: opacity 1s ease-in-out, max-height 1s ease-in-out;
            width: 90%;
            max-width: 400px;
        }

        .imagem-oculta img {
            width: 100%;
            height: auto;
            display: block;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        }

        .mostra-imagem {
            opacity: 1;
            max-height: 800px;
            margin-top: 20px;
        }

        .actions {
            margin-top: 20px;
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            justify-content: center;
        }

        .btn {
            background: #25D366;
            color: white;
            border: none;
            padding: 10px 14px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .btn:active { transform: translateY(1px); }

        .btn-secondary {
            background: #0084ff;
        }

        .note {
            margin-top: 12px;
            color: #666;
            font-size: 13px;
            max-width: 640px;
        }
    </style>
</head>
<body>

    <h1>Toque no coração para uma surpresa!</h1>

    <div class="container">
        <div class="heart" id="botao-coracao" title="Toque para ver a surpresa">
            ❤️
        </div>

        <div class="imagem-oculta" id="foto-surpresa">
            <img id="foto-revelada" src="" alt="Nossa Foto Especial">
        </div>

        <div class="actions">
            <button class="btn" id="compartilhar-whatsapp" title="Compartilhar no WhatsApp">Compartilhar no WhatsApp</button>
            <button class="btn btn-secondary" id="copiar-link" title="Gerar e copiar link de dados">Gerar/Copiar link (dados)</button>
        </div>

        <div class="note" id="nota-uso">
            Dica: para compartilhar corretamente abra este arquivo a partir de uma URL pública (ex.: GitHub Pages, Netlify). Se não tiver uma URL pública, use "Gerar/Copiar link (dados)" e cole manualmente no WhatsApp — esse link de dados pode ser muito longo e alguns dispositivos não o aceitarão.
        </div>
    </div>

    <script>
        const coracao = document.getElementById('botao-coracao');
        const fotoContainer = document.getElementById('foto-surpresa');
        const fotoElement = document.getElementById('foto-revelada');

        // Link Direto do Imgur Inserido:
        const imageUrl = "https://i.imgur.com/Ngu6DrJ.jpeg";
        fotoElement.src = imageUrl;

        coracao.addEventListener('click', function() {
            fotoContainer.classList.add('mostra-imagem');
            coracao.style.animation = 'none';
            coracao.style.cursor = 'default';
        });

        // Função para abrir WhatsApp com uma mensagem pré-preenchida
        function openWhatsAppWithText(text) {
            const encoded = encodeURIComponent(text);
            const waUrl = `https://api.whatsapp.com/send?text=${encoded}`;
            window.open(waUrl, '_blank');
        }

        document.getElementById('compartilhar-whatsapp').addEventListener('click', async () => {
            const hostedUrl = prompt('Cole aqui a URL pública deste arquivo (ex.: https://seusite.com/Supresa.html). Deixe em branco para tentar usar um link de dados (pode não funcionar em todos os dispositivos):', '');

            if (hostedUrl && hostedUrl.trim() !== '') {
                const message = `Uma surpresa para você! Abra aqui: ${hostedUrl}`;
                openWhatsAppWithText(message);
                return;
            }

            const html = document.documentElement.outerHTML;
            const dataUrl = 'data:text/html;charset=utf-8,' + encodeURIComponent(html);

            if (dataUrl.length <= 2000) {
                const message = `Abra esta surpresa: ${dataUrl}`;
                openWhatsAppWithText(message);
                return;
            }

            try {
                await navigator.clipboard.writeText(dataUrl);
                alert('O link de dados (muito longo) foi copiado para a área de transferência. Cole no WhatsApp para enviar.');
            } catch (err) {
                prompt('O link é muito longo para abrir automaticamente. Copie manualmente abaixo:', dataUrl);
            }
        });

        document.getElementById('copiar-link').addEventListener('click', async () => {
            const html = document.documentElement.outerHTML;
            const dataUrl = 'data:text/html;charset=utf-8,' + encodeURIComponent(html);
            try {
                await navigator.clipboard.writeText(dataUrl);
                alert('Link de dados copiado para a área de transferência. Cole no WhatsApp ou onde desejar.');
            } catch (err) {
                prompt('Não foi possível copiar automaticamente. Copie manualmente abaixo:', dataUrl);
            }
        });
    </script>

</body>
</html>
