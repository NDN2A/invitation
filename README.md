<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>دعوة خاصة ومميزة</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            /* خلفية داكنة وفخمة تبرز ألوان بطاقتك */
            background: linear-gradient(135deg, #0f172a, #1e293b);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            font-family: system-ui, -apple-system, sans-serif;
            overflow: hidden;
        }

        .wrapper {
            display: flex;
            flex-direction: column;
            align-items: center;
            max-width: 90%;
            max-height: 95vh;
            /* تأثير ظهور تدريجي مريح للعين */
            animation: fadeIn 1.2s ease-out forwards;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: scale(0.95); }
            to { opacity: 1; transform: scale(1); }
        }

        /* إطار الصورة الفخم */
        .invitation-frame {
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.6);
            border-radius: 16px;
            overflow: hidden;
            border: 1px solid rgba(255, 255, 255, 0.1);
            display: flex;
        }

        img {
            max-width: 100%;
            max-height: 75vh; /* متوافق مع شاشات الهواتف والكمبيوتر */
            display: block;
            object-fit: contain;
        }

        /* زر إعادة تشغيل التأثير */
        .celebrate-btn {
            margin-top: 20px;
            padding: 12px 28px;
            background: linear-gradient(45deg, #d4af37, #f3e5ab);
            color: #000;
            border: none;
            border-radius: 50px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(212, 175, 55, 0.3);
            transition: all 0.3s ease;
            z-index: 10;
        }

        .celebrate-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(212, 175, 55, 0.5);
        }
    </style>
</head>
<body>

    <div class="wrapper">
        <div class="invitation-frame">
            <img id="invitationImg" src="" alt="دعوة خاصة">
        </div>
        <button class="celebrate-btn" onclick="fireConfetti()">أطلق التأثيرات مجدداً 🎉</button>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    
    <script>
        // 1. قراءة اسم الصورة المكتوب في الرابط
        const urlParams = new URLSearchParams(window.location.search);
        const imgParam = urlParams.get('card');
        
        // حدد هنا اسم الصورة الافتراضية لو فتح شخص الرابط الأساسي بدون تحديد أستاذ
        const defaultImage = "1.jpg"; 

        const imgElement = document.getElementById('invitationImg');
        
        // تغيير مصدر الصورة بناءً على الرابط
        if (imgParam) {
            imgElement.src = imgParam;
        } else {
            imgElement.src = defaultImage;
        }

        // 2. دالة تأثير القصاصات الملونة الاحترافية (تستمر لـ 3 ثوانٍ بشكل متفجر)
        function fireConfetti() {
            var duration = 3 * 1000;
            var animationEnd = Date.now() + duration;
            var defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 1000 };

            var interval = setInterval(function() {
                var timeLeft = animationEnd - Date.now();

                if (timeLeft <= 0) {
                    return clearInterval(interval);
                }

                var particleCount = 50 * (timeLeft / duration);
                // إطلاق القصاصات من أماكن عشوائية في الشاشة
                confetti(Object.assign({}, defaults, { particleCount, origin: { x: Math.random(), y: Math.random() - 0.2 } }));
            }, 250);
        }

        // تشغيل التأثير تلقائياً بمجرد اكتمال تحميل الصفحة بـ 400 جزء من الثانية
        window.onload = function() {
            setTimeout(fireConfetti, 400);
        };
    </script>
</body>
</html>
