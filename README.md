<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .wheel-and-hamster {
            --dur: 1s;
            position: relative;
            width: 12em;
            height: 12em;
            font-size: 14px;
        }
        .wheel,
        .hamster,
        .hamster div,
        .spoke {
            position: absolute;
        }
        .wheel,
        .spoke {
            border-radius: 50%;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }
        .wheel {
            background: radial-gradient(100% 100% at center, hsla(0,0%,60%,0) 47.8%, hsl(0,0%,60%) 48%);
            z-index: 2;
        }
        .hamster {
            animation: hamster var(--dur) ease-in-out infinite;
            top: 50%;
            left: calc(50% - 3.5em);
            width: 7em;
            height: 3.75em;
            transform: rotate(4deg) translate(-0.8em,1.85em);
            transform-origin: 50% 0;
            z-index: 1;
        }
        .hamster__head {
            animation: hamsterHead var(--dur) ease-in-out infinite;
            background: hsl(30,90%,55%);
            border-radius: 70% 30% 0 100% / 40% 25% 25% 60%;
            box-shadow: 0 -0.25em 0 hsl(30,90%,80%) inset,
                        0.75em -1.55em 0 hsl(30,90%,90%) inset;
            top: 0;
            left: -2em;
            width: 2.75em;
            height: 2.5em;
            transform-origin: 100% 50%;
        }
        .hamster__ear {
            animation: hamsterEar var(--dur) ease-in-out infinite;
            background: hsl(0,90%,85%);
            border-radius: 50%;
            box-shadow: -0.25em 0 hsl(30,90%,55%) inset;
            top: -0.25em;
            right: -0.25em;
            width: 0.75em;
            height: 0.75em;
            transform-origin: 50% 75%;
        }
        .hamster__eye {
            animation: hamsterEye var(--dur) linear infinite;
            background-color: hsl(0,0%,0%);
            border-radius: 50%;
            top: 0.375em;
            left: 1.25em;
            width: 0.5em;
            height: 0.5em;
        }
        .hamster__nose {
            background: hsl(0,90%,75%);
            border-radius: 35% 65% 85% 15% / 70% 50% 50% 30%;
            top: 0.75em;
            left: 0;
            width: 0.2em;
            height: 0.25em;
        }
        .hamster__body {
            animation: hamsterBody var(--dur) ease-in-out infinite;
            background: hsl(30,90%,90%);
            border-radius: 50% 30% 50% 30% / 15% 60% 40% 40%;
            box-shadow: 0.1em 0.75em 0 hsl(30,90%,55%) inset,
                        0.15em -0.5em 0 hsl(30,90%,80%) inset;
            top: 0.25em;
            left: 2em;
            width: 4.5em;
            height: 3em;
            transform-origin: 17% 50%;
            transform-style: preserve-3d;
        }
        .hamster__limb--fr,
        .hamster__limb--fl {
            clip-path: polygon(0 0,100% 0,70% 80%,60% 100%,0% 100%,40% 80%);
            top: 2em;
            left: 0.5em;
            width: 1em;
            height: 1.5em;
            transform-origin: 50% 0;
        }
        .hamster__limb--fr {
            animation: hamsterFRLimb var(--dur) linear infinite;
            background: linear-gradient(hsl(30,90%,80%) 80%,hsl(0,90%,75%) 80%);
            transform: rotate(15deg) translateZ(-1px);
        }
        .hamster__limb--fl {
            animation: hamsterFLLimb var(--dur) linear infinite;
            background: linear-gradient(hsl(30,90%,90%) 80%,hsl(0,90%,85%) 80%);
            transform: rotate(15deg);
        }
        .hamster__limb--br,
        .hamster__limb--bl {
            border-radius: 0.75em 0.75em 0 0;
            clip-path: polygon(0 0,100% 0,100% 30%,70% 90%,70% 100%,30% 100%,40% 90%,0% 30%);
            top: 1em;
            left: 2.8em;
            width: 1.5em;
            height: 2.5em;
            transform-origin: 50% 30%;
        }
        .hamster__limb--br {
            animation: hamsterBRLimb var(--dur) linear infinite;
            background: linear-gradient(hsl(30,90%,80%) 90%,hsl(0,90%,75%) 90%);
            transform: rotate(-25deg) translateZ(-1px);
        }
        .hamster__limb--bl {
            animation: hamsterBLLimb var(--dur) linear infinite;
            background: linear-gradient(hsl(30,90%,90%) 90%,hsl(0,90%,85%) 90%);
            transform: rotate(-25deg);
        }
        .hamster__tail {
            animation: hamsterTail var(--dur) linear infinite;
            background: hsl(0,90%,85%);
            border-radius: 0.25em 50% 50% 0.25em;
            box-shadow: 0 -0.2em 0 hsl(0,90%,75%) inset;
            top: 1.5em;
            right: -0.5em;
            width: 1em;
            height: 0.5em;
            transform: rotate(30deg) translateZ(-1px);
            transform-origin: 0.25em 0.25em;
        }
        .spoke {
            animation: spoke var(--dur) linear infinite;
            background: radial-gradient(100% 100% at center,hsl(0,0%,60%) 4.8%,hsla(0,0%,60%,0) 5%),
                        linear-gradient(hsla(0,0%,55%,0) 46.9%,hsl(0,0%,65%) 47% 52.9%,hsla(0,0%,65%,0) 53%) 50% 50% / 99% 99% no-repeat;
        }
        @keyframes hamster {
            from, to { transform: rotate(4deg) translate(-0.8em,1.85em); }
            50% { transform: rotate(0) translate(-0.8em,1.85em); }
        }
        @keyframes hamsterHead {
            from, 25%, 50%, 75%, to { transform: rotate(0); }
            12.5%, 37.5%, 62.5%, 87.5% { transform: rotate(8deg); }
        }
        @keyframes hamsterEye {
            from, 90%, to { transform: scaleY(1); }
            95% { transform: scaleY(0); }
        }
        @keyframes hamsterEar {
            from, 25%, 50%, 75%, to { transform: rotate(0); }
            12.5%, 37.5%, 62.5%, 87.5% { transform: rotate(12deg); }
        }
        @keyframes hamsterBody {
            from, 25%, 50%, 75%, to { transform: rotate(0); }
            12.5%, 37.5%, 62.5%, 87.5% { transform: rotate(-2deg); }
        }
        @keyframes hamsterFRLimb {
            from, 25%, 50%, 75%, to { transform: rotate(50deg) translateZ(-1px); }
            12.5%, 37.5%, 62.5%, 87.5% { transform: rotate(-30deg) translateZ(-1px); }
        }
        @keyframes hamsterFLLimb {
            from, 25%, 50%, 75%, to { transform: rotate(-30deg); }
            12.5%, 37.5%, 62.5%, 87.5% { transform: rotate(50deg); }
        }
        @keyframes hamsterBRLimb {
            from, 25%, 50%, 75%, to { transform: rotate(-60deg) translateZ(-1px); }
            12.5%, 37.5%, 62.5%, 87.5% { transform: rotate(20deg) translateZ(-1px); }
        }
        @keyframes hamsterBLLimb {
            from, 25%, 50%, 75%, to { transform: rotate(20deg); }
            12.5%, 37.5%, 62.5%, 87.5% { transform: rotate(-60deg); }
        }
        @keyframes hamsterTail {
            from, 25%, 50%, 75%, to { transform: rotate(30deg) translateZ(-1px); }
            12.5%, 37.5%, 62.5%, 87.5% { transform: rotate(10deg) translateZ(-1px); }
        }
        @keyframes spoke {
            from { transform: rotate(0); }
            to { transform: rotate(-1turn); }
        }
    </style>
</head>
<body class="bg-slate-900 min-h-screen flex items-center justify-center m-0 overflow-hidden font-sans">
    <div aria-label="Orange and tan hamster running in a metal wheel" role="img" class="wheel-and-hamster">
        <div class="wheel"></div>
        <div class="hamster">
            <div class="hamster__body">
                <div class="hamster__head">
                    <div class="hamster__ear"></div>
                    <div class="hamster__eye"></div>
                    <div class="hamster__nose"></div>
                </div>
                <div class="hamster__limb hamster__limb--fr"></div>
                <div class="hamster__limb hamster__limb--fl"></div>
                <div class="hamster__limb hamster__limb--br"></div>
                <div class="hamster__limb hamster__limb--bl"></div>
                <div class="hamster__tail"></div>
            </div>
        </div>
        <div class="spoke"></div>
    </div>
    <div id="developmentModal" class="fixed inset-0 z-50 flex items-center justify-center bg-black/60 backdrop-blur-sm transition-opacity duration-300">
        <div class="bg-white rounded-2xl shadow-2xl max-w-sm w-full mx-4 p-8 relative text-center transform transition-transform scale-100 duration-300" id="modalContent">
            <button id="closeModalBtn" class="absolute top-4 right-4 text-gray-400 hover:text-gray-800 transition-colors bg-gray-100 hover:bg-gray-200 rounded-full w-8 h-8 flex items-center justify-center focus:outline-none" aria-label="Cerrar">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                </svg>
            </button>
            <div class="mb-4 text-amber-500">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-16 w-16 mx-auto" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
                </svg>
            </div>
            <h2 class="text-2xl font-bold text-gray-800">Página web en desarrollo para fines de informacion para tramites</h2>
            <p class="text-gray-500 text-lg font-medium">Próximamente 01/09/2026</p>
        </div>
    </div>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const modal = document.getElementById('developmentModal');
            const closeBtn = document.getElementById('closeModalBtn');
            const modalContent = document.getElementById('modalContent');
            const closeModal = () => {
                modal.classList.add('opacity-0');
                modalContent.classList.add('scale-95');
                setTimeout(() => {
                    modal.style.display = 'none';
                }, 300);
            };
            closeBtn.addEventListener('click', closeModal);
            modal.addEventListener('click', (e) => {
                if (e.target === modal) {
                    closeModal();
                }
            });
        });
    </script>
</body>
</html>
