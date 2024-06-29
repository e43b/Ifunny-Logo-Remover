document.getElementById('upload').addEventListener('change', function(e) {
    const files = e.target.files;
    const pixelsToRemove = parseInt(document.getElementById('pixel-input').value) || 20;
    processFiles(files, pixelsToRemove);
});

document.getElementById('process-urls').addEventListener('click', function() {
    const urls = document.getElementById('url-input').value.split(',').map(url => url.trim());
    const pixelsToRemove = parseInt(document.getElementById('pixel-input').value) || 20;
    processUrls(urls, pixelsToRemove);
});

function processFiles(files, pixelsToRemove) {
    const imagesContainer = document.getElementById('images');
    imagesContainer.innerHTML = '';
    let processedCount = 0;

    Array.from(files).forEach(file => {
        const reader = new FileReader();

        reader.onload = function(event) {
            const img = new Image();
            img.src = event.target.result;

            img.onload = function() {
                createImagePair(img, img.src, pixelsToRemove);
                processedCount++;
                if (processedCount === files.length) {
                    document.getElementById('instructions').style.display = 'block';
                }
            };
        };
        reader.readAsDataURL(file);
    });
}

function processUrls(urls, pixelsToRemove) {
    const imagesContainer = document.getElementById('images');
    imagesContainer.innerHTML = '';
    let processedCount = 0;

    urls.forEach(url => {
        const img = new Image();
        img.crossOrigin = 'Anonymous';
        img.src = url;

        img.onload = function() {
            createImagePair(img, url, pixelsToRemove);
            processedCount++;
            if (processedCount === urls.length) {
                document.getElementById('instructions').style.display = 'block';
            }
        };

        img.onerror = function() {
            console.error(`Erro ao carregar imagem da URL: ${url}`);
        };
    });
}

function createImagePair(img, originalSrc, pixelsToRemove) {
    const imagesContainer = document.getElementById('images');
    const imagePair = document.createElement('div');
    imagePair.className = 'image-pair';

    const originalImgContainer = document.createElement('div');
    const originalImg = document.createElement('img');
    originalImg.src = originalSrc;
    originalImg.alt = 'Imagem Original';
    originalImg.addEventListener('click', function() {
        downloadImage(originalSrc, 'original_image.png');
    });

    const originalLabel = document.createElement('div');
    originalLabel.className = 'image-label';
    originalLabel.innerText = 'Imagem Original';

    originalImgContainer.appendChild(originalLabel);
    originalImgContainer.appendChild(originalImg);

    const canvas = document.createElement('canvas');
    const ctx = canvas.getContext('2d');
    canvas.width = img.width;
    canvas.height = img.height - pixelsToRemove;

    ctx.drawImage(img, 0, 0, img.width, img.height - pixelsToRemove, 0, 0, img.width, img.height - pixelsToRemove);

    const processedImgContainer = document.createElement('div');
    const processedImg = new Image();
    processedImg.src = canvas.toDataURL('image/png');
    processedImg.alt = 'Imagem Sem Logo';
    processedImg.addEventListener('click', function() {
        downloadImage(processedImg.src, 'image_without_logo.png');
    });

    const processedLabel = document.createElement('div');
    processedLabel.className = 'image-label';
    processedLabel.innerText = 'Imagem com a Logo Removida';

    processedImgContainer.appendChild(processedLabel);
    processedImgContainer.appendChild(processedImg);

    imagePair.appendChild(originalImgContainer);
    imagePair.appendChild(processedImgContainer);
    imagesContainer.appendChild(imagePair);
}

function downloadImage(dataUrl, filename) {
    const a = document.createElement('a');
    a.href = dataUrl;
    a.download = filename;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
}
