# Football
addEventListener('click', () => score2.textContent = +score2.textContent + 1);

    score1.addEventListener('contextmenu', (e) => {
        e.preventDefault();
        score1.textContent = '0';
        score2.textContent = '0';
        time = 0;
        updateTimer();
    });

    score2.addEventListener('contextmenu', (e) => {
        e.preventDefault();
        score1.textContent = '0';
        score2.textContent = '0';
        time = 0;
        updateTimer();
    });

    // Цветовые полоски
    const colorPicker = document.getElementById('colorPicker');
    function showColorPicker(barId, triggerEl) {
        const rect = triggerEl.getBoundingClientRect();
        colorPicker.style.position = 'fixed';
        colorPicker.style.left = rect.left + 'px';
        colorPicker.style.top = rect.bottom + 'px';
        colorPicker.style.zIndex = 1000;
        colorPicker.onchange = () => {
            document.getElementById(barId).style.backgroundColor = colorPicker.value;
            colorPicker.style.left = '-9999px';
        };
        colorPicker.onblur = () => {
            colorPicker.style.left = '-9999px';
        };
        colorPicker.click();
    }

    // Загрузка логотипа
    const logo = document.getElementById('logo');
    const logoInput = document.getElementById('logoInput');
    logo.addEventListener('click', () => logoInput.click());
    logoInput.addEventListener('change', (e) => {
        const file = e.target.files[0];
        if (file) {
            const reader = new FileReader();
            reader.onload = (event) => {
                logo.src = event.target.result;
            };
            reader.readAsDataURL(file);
        }
    });
</script>

<input type="color" id="colorPicker" style="position:absolute; left:-9999px;">
</body>
</html>
..
