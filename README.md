<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cinta Aisyah Putri - Backend Student</title>
    
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/animejs/3.2.1/anime.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/OwlCarousel2/2.3.4/owl.carousel.min.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/OwlCarousel2/2.3.4/assets/owl.carousel.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css"/>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --falu-red: #6f1d1bff;
            --lion: #bb9457ff;
            --bistre: #432818ff;
            --brown: #99582aff;
            --peach: #ffe6a7ff;
        }
        
        /* --- Base Styles --- */
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: 'Inter', sans-serif;
            background: linear-gradient(135deg, var(--bistre) 0%, var(--brown) 50%, var(--bistre) 100%);
            color: #e2e8f0;
            overflow-x: hidden;
            cursor: none;
        }
        .font-heading { font-family: 'Space Grotesk', sans-serif; }
        
        /* --- Enhanced Cursor --- */
        .cursor-main {
            position: fixed;
            width: 20px;
            height: 20px;
            background: radial-gradient(circle, var(--peach) 0%, var(--lion) 100%);
            border-radius: 50%;
            pointer-events: none;
            z-index: 9999;
            transition: transform 0.1s ease-out;
            box-shadow: 0 0 20px rgba(255, 230, 167, 0.5);
        }
        
        .cursor-trail {
            position: fixed;
            width: 6px;
            height: 6px;
            background: rgba(255, 230, 167, 0.3);
            border-radius: 50%;
            pointer-events: none;
            z-index: 9998;
        }
        
        .cursor-main.hover {
            transform: scale(1.5);
            background: radial-gradient(circle, var(--falu-red) 0%, var(--brown) 100%);
            box-shadow: 0 0 30px rgba(111, 29, 27, 0.8);
        }
        
        /* --- Touch Effects --- */
        .touch-ripple {
            position: absolute;
            border-radius: 50%;
            background: radial-gradient(circle, rgba(111, 29, 27, 0.3) 0%, transparent 70%);
            transform: scale(0);
            animation: ripple 0.6s ease-out;
        }
        
        @keyframes ripple {
            to { transform: scale(4); opacity: 0; }
        }
        
        /* --- Components --- */
        #three-bg { position: fixed; top: 0; left: 0; width: 100%; height: 100%; z-index: -1; }
        
        .text-gradient {
            background: linear-gradient(135deg, var(--peach) 0%, var(--lion) 50%, var(--falu-red) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .glass-card {
            background: rgba(67, 40, 24, 0.4);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 230, 167, 0.2);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            position: relative;
            overflow: hidden;
        }
        
        .glass-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 230, 167, 0.1), transparent);
            transition: left 0.5s;
        }
        
        .glass-card:hover::before { left: 100%; }
        .glass-card:hover {
            transform: translateY(-10px);
            border-color: rgba(111, 29, 27, 0.5);
            box-shadow: 0 20px 40px rgba(111, 29, 27, 0.1);
        }
        
        .navbar {
            backdrop-filter: blur(20px);
            background: rgba(67, 40, 24, 0.8);
            border-bottom: 1px solid rgba(255, 230, 167, 0.2);
        }
        
        .skill-bar {
            background: rgba(153, 88, 42, 0.5);
            border-radius: 10px;
            height: 12px;
            overflow: hidden;
            position: relative;
        }
        
        .skill-progress {
            height: 100%;
            background: linear-gradient(90deg, var(--lion), var(--peach));
            border-radius: 10px;
            position: relative;
            overflow: hidden;
        }
        
        .skill-progress::after {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
            animation: shimmer 2s infinite;
        }
        
        @keyframes shimmer {
            0% { left: -100%; }
            100% { left: 100%; }
        }
        
        .warm-card {
            background: linear-gradient(135deg, var(--brown) 0%, var(--lion) 100%);
            border: 2px solid var(--peach);
            position: relative;
        }
        
        .warm-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(45deg, transparent 30%, rgba(255, 255, 255, 0.1) 50%, transparent 70%);
            opacity: 0;
            transition: opacity 0.3s;
        }
        
        .warm-card:hover::before { opacity: 1; }
        
        /* --- Animations --- */
        .floating {
            animation: float 3s ease-in-out infinite;
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }
        
        .pulse-glow {
            animation: pulse-glow 2s ease-in-out infinite alternate;
        }
        
        @keyframes pulse-glow {
            from { box-shadow: 0 0 20px rgba(255, 230, 167, 0.5); }
            to { box-shadow: 0 0 40px rgba(111, 29, 27, 0.8); }
        }
        
        /* --- Alert Styles --- */
        .custom-alert {
            position: fixed;
            top: 20px;
            right: 20px;
            background: rgba(67, 40, 24, 0.9);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(111, 29, 27, 0.5);
            border-radius: 12px;
            padding: 16px 24px;
            color: #e2e8f0;
            z-index: 10000;
            transform: translateX(400px);
            transition: transform 0.3s ease-out;
        }
        
        .custom-alert.show { transform: translateX(0); }
        
        /* --- Responsive --- */
        @media (max-width: 768px) {
            .cursor-main, .cursor-trail { display: none; }
            body { cursor: default; }
        }
        
        /* --- Scrollbar --- */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: var(--bistre); }
        ::-webkit-scrollbar-thumb { 
            background: linear-gradient(135deg, var(--lion), var(--peach)); 
            border-radius: 4px; 
        }
        ::-webkit-scrollbar-thumb:hover { 
            background: linear-gradient(135deg, var(--brown), var(--falu-red)); 
        }
        
        html { scroll-behavior: smooth; }
        
        /* Footer Hover */
        footer a:hover {
            color: var(--falu-red) !important;
        }
    </style>
</head>
<body class="antialiased">
    
    <!-- Enhanced Cursor -->
    <div class="cursor-main"></div>
    
    <!-- Three.js Background -->
    <canvas id="three-bg"></canvas>
    
    <!-- Custom Alert -->
    <div id="customAlert" class="custom-alert">
        <div class="flex items-center">
            <i class="fas fa-info-circle text-yellow-400 mr-3"></i>
            <span id="alertText">Selamat datang di profil GitHub saya!</span>
        </div>
    </div>

    <!-- Navigation -->
    <nav class="navbar fixed top-0 w-full z-50 transition-all duration-300">
        <div class="container mx-auto flex justify-between items-center px-6 py-4">
            <a href="#home" class="interactive font-heading text-xl font-bold text-white hover:text-yellow-300 transition-colors">
                <i class="fas fa-code mr-2"></i>CintaAisyahPutri
            </a>
            <div class="hidden md:flex items-center space-x-8 text-slate-300">
                <a href="#about" class="interactive hover:text-yellow-300 transition-colors">About</a>
                <a href="#skills" class="interactive hover:text-yellow-300 transition-colors">Skills</a>
                <a href="#git-commands" class="interactive hover:text-yellow-300 transition-colors">Git Commands</a>
                <a href="#projects" class="interactive hover:text-yellow-300 transition-colors">Projects</a>
                <a href="#contact" class="interactive bg-orange-600 hover:bg-orange-700 px-4 py-2 rounded-lg transition-colors">Contact</a>
            </div>
            <button class="md:hidden text-white" onclick="toggleMobileMenu()">
                <i class="fas fa-bars"></i>
            </button>
        </div>
    </nav>
    
    <main>
        <!-- Hero Section -->
        <section id="home" class="min-h-screen flex items-center justify-center text-center relative px-4">
            <div class="max-w-4xl mx-auto">
                <div class="floating">
                    <div class="w-32 h-32 mx-auto mb-8 rounded-full bg-gradient-to-br from-yellow-500 to-orange-400 p-1">
                        <div class="w-full h-full rounded-full bg-slate-800 flex items-center justify-center">
                            <i class="fas fa-user-graduate text-4xl text-yellow-400"></i>
                        </div>
                    </div>
                </div>
                
                <h1 class="font-heading text-5xl md:text-7xl lg:text-8xl font-bold text-white mb-6 animate__animated animate__fadeInDown">
                    <span class="text-gradient">Cinta Aisyah Putri</span>
                    <br>
                    <span class="text-2xl md:text-3xl lg:text-4xl font-normal">Backend Student</span>
                </h1>
                
                <!-- Image after Welcome Title -->
                <img src="bg.png" alt="Background Image" class="mx-auto mb-6 rounded-lg shadow-lg max-w-md" style="filter: drop-shadow(0 10px 20px rgba(0,0,0,0.3));">
                
                <p class="text-lg md:text-xl mt-6 max-w-3xl mx-auto text-slate-300 animate__animated animate__fadeInUp animate__delay-1s">
                    Siswa <strong>Backend</strong> dari <em>SMK Palapa Semarang</em> yang selalu penasaran dengan hal-hal baru. Passionate dalam <strong>mengkode</strong>, <strong>menggambar</strong>, <strong>bermain violin</strong>, dan segala sesuatu yang saya senangi! Selalu siap belajar dan eksplorasi teknologi terbaru.
                </p>
                
                <div class="mt-10 flex flex-col sm:flex-row gap-4 justify-center animate__animated animate__zoomIn animate__delay-2s">
                    <a href="#projects" class="interactive bg-orange-500 hover:bg-orange-600 text-white px-8 py-3 rounded-lg font-semibold transition-all pulse-glow">
                        <i class="fas fa-rocket mr-2"></i>Lihat Proyek Saya
                    </a>
                    <a href="#contact" class="interactive border-2 border-yellow-500 text-yellow-400 hover:bg-yellow-500 hover:text-white px-8 py-3 rounded-lg font-semibold transition-all">
                        <i class="fas fa-envelope mr-2"></i>Hubungi Saya
                    </a>
                </div>
            </div>
        </section>

        <!-- About Section -->
        <section id="about" class="py-24 relative">
            <div class="container mx-auto px-6">
                <div class="text-center mb-16">
                    <h2 class="font-heading text-4xl md:text-5xl font-bold text-gradient mb-4" data-aos="fade-up">
                        Tentang Saya
                    </h2>
                    <p class="text-slate-400 max-w-2xl mx-auto" data-aos="fade-up" data-aos-delay="100">
                        Perjalanan saya dimulai dari rasa ingin tahu yang besar terhadap dunia pemrograman
                    </p>
                </div>
                
                <div class="grid md:grid-cols-2 gap-12 items-center">
                    <div class="space-y-6" data-aos="fade-right">
                        <div class="glass-card p-8 rounded-xl">
                            <h3 class="font-heading text-2xl font-bold text-white mb-4">
                                <i class="fas fa-lightbulb text-yellow-400 mr-3"></i>
                                Filosofi Belajar
                            </h3>
                            <p class="text-slate-300 leading-relaxed">
                                Saya percaya bahwa belajar coding adalah tentang eksplorasi dan kreativitas. Setiap kode yang saya tulis adalah petualangan baru, terinspirasi dari hobi menggambar dan bermain violin yang mengajarkan kesabaran dan harmoni.
                            </p>
                        </div>
                        
                        <div class="glass-card p-8 rounded-xl">
                            <h3 class="font-heading text-2xl font-bold text-white mb-4">
                                <i class="fas fa-target text-yellow-400 mr-3"></i>
                                Fokus Utama
                            </h3>
                            <p class="text-slate-300 leading-relaxed">
                                Sebagai backend student, saya fokus pada pengembangan server-side yang efisien. Selalu penasaran dengan teknologi baru, dari API hingga database, sambil menikmati hobi yang membuat hidup lebih berwarna.
                            </p>
                        </div>
                    </div>
                    
                    <div class="text-center" data-aos="fade-left">
                        <div class="relative inline-block">
                            <div class="w-80 h-80 rounded-full bg-gradient-to-br from-orange-600 to-yellow-400 p-2">
                                <div class="w-full h-full rounded-full bg-slate-800 flex items-center justify-center">
                                    <i class="fas fa-code text-8xl text-yellow-400"></i>
                                </div>
                            </div>
                            <div class="absolute -top-4 -right-4 w-16 h-16 bg-yellow-400 rounded-full flex items-center justify-center animate-pulse">
                                <i class="fas fa-star text-slate-800 text-xl"></i>
                            </div>
                        </div>
                        
                        <div class="mt-8 flex justify-center space-x-6">
                            <a href="https://github.com/CintaAisyahPutri" class="interactive text-3xl text-slate-400 hover:text-yellow-300 transition-colors">
                                <i class="fab fa-github"></i>
                            </a>
                            <a href="https://linkedin.com/in/cintaaisyahputri" class="interactive text-3xl text-slate-400 hover:text-yellow-300 transition-colors">
                                <i class="fab fa-linkedin"></i>
                            </a>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Skills Section -->
        <section id="skills" class="py-24 bg-slate-900/50">
            <div class="container mx-auto px-6">
                <div class="text-center mb-16">
                    <h2 class="font-heading text-4xl md:text-5xl font-bold text-gradient mb-4" data-aos="fade-up">
                        Keahlian Teknis
                    </h2>
                    <p class="text-slate-400 max-w-2xl mx-auto" data-aos="fade-up" data-aos-delay="100">
                        Teknologi yang saya pelajari sebagai backend student yang penasaran
                    </p>
                </div>
                
                <div class="grid md:grid-cols-2 gap-8 max-w-4xl mx-auto">
                    <div class="glass-card p-8 rounded-xl" data-aos="fade-up" data-aos-delay="200">
                        <h3 class="font-heading text-xl font-bold text-white mb-6">Backend Basics</h3>
                        <div class="space-y-4">
                            <div class="skill-item">
                                <div class="flex justify-between mb-2">
                                    <span class="text-yellow-400 font-semibold">Node.js & Express</span>
                                    <span class="text-slate-400">80%</span>
                                </div>
                                <div class="skill-bar">
                                    <div class="skill-progress" style="width: 80%"></div>
                                </div>
                            </div>
                            <div class="skill-item">
                                <div class="flex justify-between mb-2">
                                    <span class="text-yellow-400 font-semibold">REST API</span>
                                    <span class="text-slate-400">75%</span>
                                </div>
                                <div class="skill-bar">
                                    <div class="skill-progress" style="width: 75%"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="glass-card p-8 rounded-xl" data-aos="fade-up" data-aos-delay="300">
                        <h3 class="font-heading text-xl font-bold text-white mb-6">Tools & Others</h3>
                        <div class="space-y-4">
                            <div class="skill-item">
                                <div class="flex justify-between mb-2">
                                    <span class="text-yellow-400 font-semibold">MongoDB & SQL</span>
                                    <span class="text-slate-400">70%</span>
                                </div>
                                <div class="skill-bar">
                                    <div class="skill-progress" style="width: 70%"></div>
                                </div>
                            </div>
                            <div class="skill-item">
                                <div class="flex justify-between mb-2">
                                    <span class="text-yellow-400 font-semibold">Git & Version Control</span>
                                    <span class="text-slate-400">85%</span>
                                </div>
                                <div class="skill-bar">
                                    <div class="skill-progress" style="width: 85%"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Git Commands Section -->
        <section id="git-commands" class="py-24">
            <div class="container mx-auto px-6">
                <div class="text-center mb-16">
                    <h2 class="font-heading text-4xl md:text-5xl font-bold text-gradient mb-4" data-aos="fade-up">
                        Useful Git Commands
                    </h2>
                    <p class="text-slate-400 max-w-2xl mx-auto" data-aos="fade-up" data-aos-delay="100">
                        Cheat sheet sederhana untuk Git, terinspirasi dari <a href="https://www.geeksforgeeks.org/git/useful-github-commands/" class="text-yellow-400 hover:text-yellow-300">GeeksforGeeks</a> dan <a href="https://git-scm.com/cheat-sheet.html" class="text-yellow-400 hover:text-yellow-300">Git Cheat Sheet</a>
                    </p>
                </div>
                
                <div class="grid md:grid-cols-2 gap-8 max-w-4xl mx-auto">
                    <div class="glass-card p-8 rounded-xl" data-aos="fade-up" data-aos-delay="200">
                        <h3 class="font-heading text-xl font-bold text-white mb-6">Basic Commands</h3>
                        <div class="space-y-4 text-sm">
                            <code class="block bg-slate-800 p-2 rounded">git init</code>
                            <code class="block bg-slate-800 p-2 rounded">git clone &lt;url&gt;</code>
                            <code class="block bg-slate-800 p-2 rounded">git add .</code>
                            <code class="block bg-slate-800 p-2 rounded">git commit -m "message"</code>
                            <code class="block bg-slate-800 p-2 rounded">git push origin main</code>
                        </div>
                    </div>
                    
                    <div class="glass-card p-8 rounded-xl" data-aos="fade-up" data-aos-delay="300">
                        <h3 class="font-heading text-xl font-bold text-white mb-6">Branch & Merge</h3>
                        <div class="space-y-4 text-sm">
                            <code class="block bg-slate-800 p-2 rounded">git branch &lt;name&gt;</code>
                            <code class="block bg-slate-800 p-2 rounded">git checkout &lt;name&gt;</code>
                            <code class="block bg-slate-800 p-2 rounded">git merge &lt;name&gt;</code>
                            <code class="block bg-slate-800 p-2 rounded">git pull origin main</code>
                            <code class="block bg-slate-800 p-2 rounded">git status</code>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Projects Section -->
        <section id="projects" class="py-24 bg-slate-900/50">
            <div class="container mx-auto px-6">
                <div class="text-center mb-16">
                    <h2 class="font-heading text-4xl md:text-5xl font-bold text-gradient mb-4" data-aos="fade-up">
                        Proyek Saya
                    </h2>
                    <p class="text-slate-400 max-w-2xl mx-auto" data-aos="fade-up" data-aos-delay="100">
                        Beberapa proyek sederhana sebagai backend student
                    </p>
                </div>
                
                <div class="space-y-16">
                    <div class="grid md:grid-cols-2 gap-8 items-center" data-aos="fade-up">
                        <div class="glass-card p-8 rounded-xl">
                            <div class="flex items-center mb-4">
                                <i class="fas fa-server text-yellow-400 text-2xl mr-3"></i>
                                <h3 class="font-heading text-2xl font-bold text-white">Simple REST API</h3>
                            </div>
                            <p class="text-slate-300 mb-6 leading-relaxed">
                                API sederhana untuk manajemen data siswa menggunakan Node.js dan MongoDB. Masih dalam pengembangan, tapi menyenangkan untuk belajar!
                            </p>
                            <div class="flex flex-wrap gap-2 mb-6">
                                <span class="px-3 py-1 bg-orange-500/20 text-orange-400 rounded-full text-sm">Node.js</span>
                                <span class="px-3 py-1 bg-yellow-500/20 text-yellow-400 rounded-full text-sm">MongoDB</span>
                            </div>
                            <a href="https://github.com/CintaAisyahPutri/simple-api" class="interactive text-yellow-400 hover:text-yellow-300 font-semibold">
                                Lihat Detail <i class="fas fa-arrow-right ml-1"></i>
                            </a>
                        </div>
                        
                        <div class="glass-card p-6 rounded-xl bg-slate-800/50">
                            <pre class="text-sm text-slate-300 overflow-x-auto"><code>{
  "student": {
    "id": 1,
    "name": "Cinta Aisyah Putri",
    "school": "SMK Palapa Semarang",
    "hobby": "Coding & Violin"
  }
}</code></pre>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Contact Section -->
        <section id="contact" class="py-24">
            <div class="container mx-auto px-6 text-center">
                <div class="max-w-3xl mx-auto">
                    <h2 class="font-heading text-4xl md:text-5xl font-bold text-gradient mb-6" data-aos="fade-up">
                        Mari Berkoneksi
                    </h2>
                    <p class="text-slate-400 text-lg mb-8" data-aos="fade-up" data-aos-delay="100">
                        Tertarik berkolaborasi atau sekadar ngobrol tentang coding dan hobi? Hubungi saya!
                    </p>
        
                    <div class="flex flex-col sm:flex-row gap-4 justify-center" data-aos="fade-up" data-aos-delay="200">
                        <a href="mailto:cintaaisyahputri@example.com" class="interactive bg-orange-500 hover:bg-orange-600 text-white px-8 py-4 rounded-lg font-semibold transition-all pulse-glow">
                            <i class="fas fa-envelope mr-2"></i>cintaaisyahputri@example.com
                        </a>
                        <a href="https://t.me/CintaAisyah" class="interactive border-2 border-orange-500 text-orange-400 hover:bg-orange-500 hover:text-white px-8 py-4 rounded-lg font-semibold transition-all">
                            <i class="fab fa-telegram mr-2"></i>Telegram
                        </a>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <!-- Footer -->
    <footer class="py-12 border-t border-slate-700/50">
        <div class="container mx-auto px-6 text-center">
            <div class="flex justify-center space-x-6 mb-6">
                <a href="https://github.com/CintaAisyahPutri" class="interactive text-slate-400 hover:text-yellow-300 text-2xl transition-colors">
                    <i class="fab fa-github"></i>
                </a>
                <a href="https://linkedin.com/in/cintaaisyahputri" class="interactive text-slate-400 hover:text-yellow-300 text-2xl transition-colors">
                    <i class="fab fa-linkedin"></i>
                </a>
                <a href="mailto:cintaaisyahputri@example.com" class="interactive text-slate-400 hover:text-yellow-300 text-2xl transition-colors">
                    <i class="fas fa-envelope"></i>
                </a>
            </div>
            <p class="text-slate-500 text-sm">© 2025 Cinta Aisyah Putri. Dibuat dengan <i class="fas fa-heart text-red-500"></i> dan inspirasi dari kakak kelas saya. Selalu penasaran!</p>
        </div>
    </footer>
    
    <!-- AOS Library -->
    <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">
    <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>

    <script>
        // --- GLOBAL VARIABLES ---
        let mouseX = 0, mouseY = 0;
        let cursorTrails = [];
        let scene, camera, renderer, particles, particleSystem;
        
        // --- ENHANCED CURSOR SYSTEM ---
        function initCursor() {
            const cursor = document.querySelector('.cursor-main');
            const trailCount = 10;
            
            // Create cursor trails
            for (let i = 0; i < trailCount; i++) {
                const trail = document.createElement('div');
                trail.className = 'cursor-trail';
                trail.style.opacity = (1 - i / trailCount) * 0.5;
                trail.style.transform = `scale(${1 - i / trailCount})`;
                document.body.appendChild(trail);
                cursorTrails.push({ element: trail, x: 0, y: 0, delay: i * 2 });
            }
            
            // Mouse move handler
            document.addEventListener('mousemove', (e) => {
                mouseX = e.clientX;
                mouseY = e.clientY;
                
                // Update main cursor
                gsap.to(cursor, {
                    x: mouseX - 10,
                    y: mouseY - 10,
                    duration: 0.1,
                    ease: "power2.out"
                });
                
                // Update trails with delay
                cursorTrails.forEach((trail, index) => {
                    gsap.to(trail.element, {
                        x: mouseX - 3,
                        y: mouseY - 3,
                        duration: 0.3 + index * 0.05,
                        ease: "power2.out"
                    });
                });
            });
            
            // Interactive elements
            document.querySelectorAll('.interactive').forEach(el => {
                el.addEventListener('mouseenter', () => {
                    cursor.classList.add('hover');
                });
                el.addEventListener('mouseleave', () => {
                    cursor.classList.remove('hover');
                });
            });
        }
        
        // --- TOUCH EFFECTS ---
        function initTouchEffects() {
            if ('ontouchstart' in window) {
                document.addEventListener('touchstart', (e) => {
                    const touch = e.touches[0];
                    createTouchRipple(touch.clientX, touch.clientY);
                });
            }
        }
        
        function createTouchRipple(x, y) {
            const ripple = document.createElement('div');
            ripple.className = 'touch-ripple';
            ripple.style.left = x + 'px';
            ripple.style.top = y + 'px';
            ripple.style.width = '20px';
            ripple.style.height = '20px';
            document.body.appendChild(ripple);
            
            setTimeout(() => {
                ripple.remove();
            }, 600);
        }
        
        // --- THREE.JS ENHANCED BACKGROUND ---
        function initThreeJS() {
            scene = new THREE.Scene();
            camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
            renderer = new THREE.WebGLRenderer({ 
                canvas: document.getElementById('three-bg'), 
                alpha: true,
                antialias: true
            });
            renderer.setSize(window.innerWidth, window.innerHeight);
            renderer.setPixelRatio(window.devicePixelRatio);
            
            // Enhanced particle system with warm colors
            const particleCount = 1500;
            const positions = new Float32Array(particleCount * 3);
            const colors = new Float32Array(particleCount * 3);
            const velocities = new Float32Array(particleCount * 3);
            
            for (let i = 0; i < particleCount; i++) {
                // Positions
                positions[i * 3] = (Math.random() - 0.5) * 20;
                positions[i * 3 + 1] = (Math.random() - 0.5) * 20;
                positions[i * 3 + 2] = (Math.random() - 0.5) * 20;
                
                // Colors (Warm theme)
                const rand = Math.random();
                if (rand < 0.4) {
                    colors[i * 3] = 1.0;     // R
                    colors[i * 3 + 1] = 0.9; // G
                    colors[i * 3 + 2] = 0.6; // B
                } else if (rand < 0.7) {
                    colors[i * 3] = 0.7;     // R
                    colors[i * 3 + 1] = 0.6; // G
                    colors[i * 3 + 2] = 0.2; // B
                } else {
                    colors[i * 3] = 1.0;     // R
                    colors[i * 3 + 1] = 0.8; // G
                    colors[i * 3 + 2] = 0.4; // B
                }
                
                // Velocities
                velocities[i * 3] = (Math.random() - 0.5) * 0.02;
                velocities[i * 3 + 1] = (Math.random() - 0.5) * 0.02;
                velocities[i * 3 + 2] = (Math.random() - 0.5) * 0.02;
            }
            
            const geometry = new THREE.BufferGeometry();
            geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
            geometry.setAttribute('color', new THREE.BufferAttribute(colors, 3));
            geometry.setAttribute('velocity', new THREE.BufferAttribute(velocities, 3));
            
            const material = new THREE.PointsMaterial({
                size: 0.02,
                vertexColors: true,
                transparent: true,
                opacity: 0.8,
                blending: THREE.AdditiveBlending
            });
            
            particleSystem = new THREE.Points(geometry, material);
            scene.add(particleSystem);
            
            // Add floating geometric shapes
            addFloatingShapes();
            
            camera.position.z = 8;
            animateThreeJS();
        }
        
        function addFloatingShapes() {
            const shapeGeometries = [
                new THREE.BoxGeometry(0.3, 0.3, 0.3),
                new THREE.SphereGeometry(0.2, 8, 8),
                new THREE.ConeGeometry(0.2, 0.4, 6)
            ];
            
            const shapeMaterial = new THREE.MeshBasicMaterial({
                color: 0xffe6a7,
                transparent: true,
                opacity: 0.3,
                wireframe: true
            });
            
            for (let i = 0; i < 8; i++) {
                const geometry = shapeGeometries[Math.floor(Math.random() * shapeGeometries.length)];
                const mesh = new THREE.Mesh(geometry, shapeMaterial);
                
                mesh.position.set(
                    (Math.random() - 0.5) * 15,
                    (Math.random() - 0.5) * 15,
                    (Math.random() - 0.5) * 10
                );
                
                mesh.rotation.set(
                    Math.random() * Math.PI,
                    Math.random() * Math.PI,
                    Math.random() * Math.PI
                );
                
                scene.add(mesh);
            }
        }
        
        function animateThreeJS() {
            requestAnimationFrame(animateThreeJS);
            
            // Animate particles
            const positions = particleSystem.geometry.attributes.position.array;
            const velocities = particleSystem.geometry.attributes.velocity.array;
            
            for (let i = 0; i < positions.length; i += 3) {
                positions[i] += velocities[i];
                positions[i + 1] += velocities[i + 1];
                positions[i + 2] += velocities[i + 2];
                
                // Boundary check
                if (Math.abs(positions[i]) > 10) velocities[i] *= -1;
                if (Math.abs(positions[i + 1]) > 10) velocities[i + 1] *= -1;
                if (Math.abs(positions[i + 2]) > 10) velocities[i + 2] *= -1;
            }
            
            particleSystem.geometry.attributes.position.needsUpdate = true;
            
            // Rotate particle system based on mouse
            particleSystem.rotation.x += 0.001;
            particleSystem.rotation.y += 0.002;
            
            // Mouse interaction
            if (mouseX && mouseY) {
                const mouseXNorm = (mouseX / window.innerWidth) * 2 - 1;
                const mouseYNorm = -(mouseY / window.innerHeight) * 2 + 1;
                
                gsap.to(particleSystem.rotation, {
                    x: mouseYNorm * 0.1,
                    y: mouseXNorm * 0.1,
                    duration: 2,
                    ease: "power2.out"
                });
            }
            
            // Animate floating shapes
            scene.children.forEach((child, index) => {
                if (child.type === 'Mesh') {
                    child.rotation.x += 0.01;
                    child.rotation.y += 0.01;
                    child.position.y += Math.sin(Date.now() * 0.001 + index) * 0.001;
                }
            });
            
            renderer.render(scene, camera);
        }
        
        // --- SKILL ANIMATIONS ---
        function animateSkills() {
            const skillBars = document.querySelectorAll('.skill-progress');
            
            skillBars.forEach((bar, index) => {
                const width = bar.style.width;
                bar.style.width = '0%';
                
                setTimeout(() => {
                    anime({
                        targets: bar,
                        width: width,
                        duration: 1500,
                        easing: 'easeOutExpo',
                        delay: index * 200
                    });
                }, 500);
            });
        }
        
        // --- SCROLL ANIMATIONS ---
        function initScrollAnimations() {
            gsap.registerPlugin(ScrollTrigger);
            
            // Navbar animation
            gsap.to('.navbar', {
                scrollTrigger: {
                    trigger: 'body',
                    start: 'top top',
                    end: 'bottom bottom',
                    scrub: true
                },
                backgroundColor: 'rgba(67, 40, 24, 0.95)',
                duration: 0.3
            });
            
            // Section animations
            gsap.utils.toArray('section').forEach((section, index) => {
                gsap.from(section, {
                    scrollTrigger: {
                        trigger: section,
                        start: 'top 80%',
                        end: 'bottom 20%',
                        scrub: 1
                    },
                    y: 50,
                    opacity: 0.8,
                    duration: 1
                });
            });
            
            // Skills section trigger
            ScrollTrigger.create({
                trigger: '#skills',
                start: 'top 70%',
                onEnter: animateSkills,
                once: true
            });
        }
        
        // --- CUSTOM ALERT SYSTEM ---
        function showAlert(message, type = 'info') {
            const alert = document.getElementById('customAlert');
            const alertText = document.getElementById('alertText');
            const icon = alert.querySelector('i');
            
            alertText.textContent = message;
            
            // Change icon based on type
            switch (type) {
                case 'success':
                    icon.className = 'fas fa-check-circle text-green-400 mr-3';
                    break;
                case 'error':
                    icon.className = 'fas fa-exclamation-triangle text-red-400 mr-3';
                    break;
                default:
                    icon.className = 'fas fa-info-circle text-yellow-400 mr-3';
            }
            
            alert.classList.add('show');
            
            setTimeout(() => {
                alert.classList.remove('show');
            }, 3000);
        }
        
        // --- MOBILE MENU ---
        function toggleMobileMenu() {
            // Simple mobile menu toggle (you can enhance this)
            showAlert('Menu mobile segera hadir!', 'info');
        }
        
        // --- RESIZE HANDLER ---
        function handleResize() {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        }
        
        // --- INITIALIZATION ---
        document.addEventListener('DOMContentLoaded', () => {
            // Initialize AOS
            AOS.init({
                duration: 1000,
                once: true,
                offset: 100,
                easing: 'ease-out-cubic'
            });
            
            // Initialize all systems
            initCursor();
            initTouchEffects();
            initThreeJS();
            initScrollAnimations();
            
            // Show welcome message
            setTimeout(() => {
                showAlert('Selamat datang! Mari eksplorasi bersama 🚀', 'success');
            }, 1000);
            
            // Add event listeners
            window.addEventListener('resize', handleResize);
            
            // Smooth scrolling for navigation links
            document.querySelectorAll('a[href^="#"]').forEach(anchor => {
                anchor.addEventListener('click', function (e) {
                    e.preventDefault();
                    const target = document.querySelector(this.getAttribute('href'));
                    if (target) {
                        target.scrollIntoView({
                            behavior: 'smooth',
                            block: 'start'
                        });
                    }
                });
            });
            
            // Add loading animation
            gsap.from('body', {
                opacity: 0,
                duration: 1,
                ease: 'power2.out'
            });
        });
        
        // --- EASTER EGG ---
        let konamiCode = [];
        const konamiSequence = [38, 38, 40, 40, 37, 39, 37, 39, 66, 65]; // Up Up Down Down Left Right Left Right B A
        
        document.addEventListener('keydown', (e) => {
            konamiCode.push(e.keyCode);
            if (konamiCode.length > konamiSequence.length) {
                konamiCode.shift();
            }
            
            if (konamiCode.join(',') === konamiSequence.join(',')) {
                showAlert('Easter egg! Penasaran terpenuhi! 🎻', 'success');
                document.body.style.filter = 'hue-rotate(30deg)';
                setTimeout(() => {
                    document.body.style.filter = 'none';
                }, 3000);
            }
        });
    </script>
</body>
</html>
