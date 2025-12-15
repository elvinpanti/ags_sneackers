<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AGS Sneaker Hub</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #0a0a0a;
            color: #fff;
            overflow-x: hidden;
        }

        /* Animated Background */
        .bg-animation {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: linear-gradient(45deg, #0a0a0a, #1a1a2e, #0a0a0a);
            background-size: 400% 400%;
            animation: gradientShift 15s ease infinite;
        }

        .bg-animation::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 600px;
            height: 600px;
            background-image: url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTAwMCIgaGVpZ2h0PSIxMDAwIiB2aWV3Qm94PSIwIDAgMTAwMCAxMDAwIiBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPgo8Y2lyY2xlIGN4PSI1MDAiIGN5PSI1MDAiIHI9IjQ1MCIgc3Ryb2tlPSIjZmY0NTAwIiBzdHJva2Utd2lkdGg9IjQwIiBmaWxsPSJub25lIiBvcGFjaXR5PSIwLjEiLz4KPHRleHQgeD0iNTAwIiB5PSIyNTAiIGZvbnQtZmFtaWx5PSJBcmlhbCBCbGFjayIgZm9udC1zaXplPSIxMjAiIGZvbnQtd2VpZ2h0PSI5MDAiIGZpbGw9IiNmZjQ1MDAiIG9wYWNpdHk9IjAuMSIgdGV4dC1hbmNob3I9Im1pZGRsZSI+QUcgU05FQUtFUiBIVUI8L3RleHQ+Cjwvc3ZnPg==');
            background-size: contain;
            background-repeat: no-repeat;
            background-position: center;
            opacity: 0.15;
            animation: rotate 30s linear infinite, pulse 4s ease-in-out infinite;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        @keyframes rotate {
            from { transform: translate(-50%, -50%) rotate(0deg); }
            to { transform: translate(-50%, -50%) rotate(360deg); }
        }

        @keyframes pulse {
            0%, 100% { opacity: 0.15; transform: translate(-50%, -50%) scale(1); }
            50% { opacity: 0.25; transform: translate(-50%, -50%) scale(1.1); }
        }

        /* Navigation */
        nav {
            position: fixed;
            top: 0;
            width: 100%;
            padding: 20px 50px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            z-index: 1000;
            background: rgba(10, 10, 10, 0.9);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        .logo {
            font-size: 28px;
            font-weight: bold;
            background: linear-gradient(45deg, #ff4500, #ffa500);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: glow 2s ease-in-out infinite;
            cursor: pointer;
            letter-spacing: 2px;
        }

        @keyframes glow {
            0%, 100% { filter: drop-shadow(0 0 10px rgba(255,69,0,0.5)); }
            50% { filter: drop-shadow(0 0 20px rgba(255,165,0,0.8)); }
        }

        .nav-links {
            display: flex;
            gap: 30px;
        }

        .nav-links a {
            color: #fff;
            text-decoration: none;
            position: relative;
            padding: 5px 0;
            transition: color 0.3s;
            cursor: pointer;
            font-weight: 500;
        }

        .nav-links a.active {
            color: #ff4500;
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 0;
            height: 2px;
            background: linear-gradient(90deg, #ff4500, #ffa500);
            transition: width 0.3s;
        }

        .nav-links a:hover::after,
        .nav-links a.active::after {
            width: 100%;
        }

        /* Page Container */
        .page {
            min-height: 100vh;
            padding-top: 80px;
            opacity: 0;
            transform: translateY(30px);
            transition: opacity 0.6s, transform 0.6s;
            display: none;
        }

        .page.active {
            display: block;
            animation: pageEnter 0.6s forwards;
        }

        @keyframes pageEnter {
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Home Page */
        .hero {
            height: calc(100vh - 80px);
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: column;
            text-align: center;
            position: relative;
        }

        .hero h1 {
            font-size: 80px;
            margin-bottom: 20px;
            background: linear-gradient(45deg, #fff, #ff4500, #ffa500, #fff);
            background-size: 300%;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: textShine 3s linear infinite;
        }

        @keyframes textShine {
            to { background-position: 300%; }
        }

        .hero p {
            font-size: 24px;
            color: #aaa;
            margin-bottom: 40px;
            animation: fadeInUp 1s ease-out 0.3s both;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .cta-button {
            padding: 15px 40px;
            font-size: 18px;
            background: linear-gradient(45deg, #ff4500, #ffa500);
            border: none;
            border-radius: 50px;
            color: #fff;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            transition: transform 0.3s;
            animation: fadeInUp 1s ease-out 0.6s both;
            font-weight: 600;
        }

        .cta-button::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.3);
            transform: translate(-50%, -50%);
            transition: width 0.6s, height 0.6s;
        }

        .cta-button:hover::before {
            width: 300px;
            height: 300px;
        }

        .cta-button:hover {
            transform: scale(1.05);
        }

        .cta-button span {
            position: relative;
            z-index: 1;
        }

        /* Floating Sneaker Icons */
        .particle {
            position: absolute;
            font-size: 30px;
            animation: float 20s infinite;
            opacity: 0.3;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0) translateX(0) rotate(0deg); }
            25% { transform: translateY(-100px) translateX(100px) rotate(90deg); }
            50% { transform: translateY(-200px) translateX(-50px) rotate(180deg); }
            75% { transform: translateY(-100px) translateX(-100px) rotate(270deg); }
        }

        /* Features Page */
        .features-page {
            padding: 100px 50px;
            max-width: 1200px;
            margin: 0 auto;
        }

        .features-title {
            text-align: center;
            font-size: 60px;
            margin-bottom: 60px;
            background: linear-gradient(45deg, #ff4500, #ffa500);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 40px;
        }

        .feature-card {
            background: rgba(255, 255, 255, 0.05);
            padding: 40px;
            border-radius: 20px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: transform 0.3s, box-shadow 0.3s;
            cursor: pointer;
            animation: cardSlideIn 0.6s ease-out forwards;
            opacity: 0;
        }

        .feature-card:nth-child(1) { animation-delay: 0.1s; }
        .feature-card:nth-child(2) { animation-delay: 0.2s; }
        .feature-card:nth-child(3) { animation-delay: 0.3s; }
        .feature-card:nth-child(4) { animation-delay: 0.4s; }
        .feature-card:nth-child(5) { animation-delay: 0.5s; }
        .feature-card:nth-child(6) { animation-delay: 0.6s; }

        @keyframes cardSlideIn {
            from {
                opacity: 0;
                transform: translateX(-50px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        .feature-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(255, 69, 0, 0.3);
            border-color: rgba(255, 69, 0, 0.5);
        }

        .feature-icon {
            font-size: 50px;
            margin-bottom: 20px;
            display: inline-block;
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        .feature-card h3 {
            font-size: 24px;
            margin-bottom: 15px;
            background: linear-gradient(45deg, #ff4500, #ffa500);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .feature-card p {
            color: #aaa;
            line-height: 1.6;
        }

        /* About Page */
        .about-page {
            padding: 100px 50px;
            max-width: 1000px;
            margin: 0 auto;
        }

        .about-content {
            background: rgba(255, 255, 255, 0.05);
            padding: 60px;
            border-radius: 30px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            animation: scaleIn 0.8s ease-out;
        }

        @keyframes scaleIn {
            from {
                opacity: 0;
                transform: scale(0.9);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }

        .about-content h2 {
            font-size: 50px;
            margin-bottom: 30px;
            background: linear-gradient(45deg, #ff4500, #ffa500);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .about-content p {
            font-size: 18px;
            line-height: 1.8;
            color: #ccc;
            margin-bottom: 20px;
        }

        .stats {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 30px;
            margin-top: 50px;
        }

        .stat-box {
            text-align: center;
            padding: 30px;
            background: rgba(255, 69, 0, 0.1);
            border-radius: 15px;
            border: 1px solid rgba(255, 69, 0, 0.3);
            transition: transform 0.3s;
        }

        .stat-box:hover {
            transform: scale(1.05);
        }

        .stat-number {
            font-size: 40px;
            font-weight: bold;
            color: #ff4500;
            margin-bottom: 10px;
        }

        .stat-label {
            color: #aaa;
            font-size: 14px;
        }

        /* Contact Page */
        .contact-page {
            padding: 100px 50px;
            max-width: 800px;
            margin: 0 auto;
        }

        .contact-form {
            background: rgba(255, 255, 255, 0.05);
            padding: 60px;
            border-radius: 30px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            animation: slideUp 0.8s ease-out;
        }

        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .contact-form h2 {
            font-size: 50px;
            margin-bottom: 40px;
            text-align: center;
            background: linear-gradient(45deg, #ff4500, #ffa500);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .form-group {
            margin-bottom: 30px;
        }

        .form-group label {
            display: block;
            margin-bottom: 10px;
            color: #aaa;
            font-size: 14px;
        }

        .form-group input,
        .form-group textarea {
            width: 100%;
            padding: 15px;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            color: #fff;
            font-size: 16px;
            transition: border-color 0.3s, box-shadow 0.3s;
        }

        .form-group input:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: #ff4500;
            box-shadow: 0 0 20px rgba(255, 69, 0, 0.3);
        }

        .form-group textarea {
            resize: vertical;
            min-height: 150px;
        }

        .submit-btn {
            width: 100%;
            padding: 15px;
            background: linear-gradient(45deg, #ff4500, #ffa500);
            border: none;
            border-radius: 10px;
            color: #fff;
            font-size: 18px;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.3s;
        }

        .submit-btn:hover {
            transform: scale(1.02);
        }
    </style>
</head>
<body>
    <div class="bg-animation"></div>

    <nav>
        <div class="logo" onclick="navigateTo('home')">AGS SNEAKER HUB</div>
        <div class="nav-links">
            <a onclick="navigateTo('home')" class="active">Home</a>
            <a onclick="navigateTo('features')">Collection</a>
            <a onclick="navigateTo('about')">About</a>
            <a onclick="navigateTo('contact')">Contact</a>
        </div>
    </nav>

    <!-- Home Page -->
    <div id="home" class="page active">
        <section class="hero">
            <h1>AGS SNEAKER HUB</h1>
            <p>Your Ultimate Destination for Premium Sneakers</p>
            <button class="cta-button" onclick="navigateTo('features')">
                <span>Explore Collection</span>
            </button>
        </section>
    </div>

    <!-- Features Page -->
    <div id="features" class="page">
        <div class="features-page">
            <h2 class="features-title">Our Collection</h2>
            <div class="features-grid">
                <div class="feature-card">
                    <div class="feature-icon">👟</div>
                    <h3>Latest Releases</h3>
                    <p>Get access to the newest and most sought-after sneaker drops before anyone else.</p>
                </div>
                <div class="feature-card">
                    <div class="feature-icon">⚡</div>
                    <h3>Limited Editions</h3>
                    <p>Exclusive limited edition sneakers from top brands that define your unique style.</p>
                </div>
                <div class="feature-card">
                    <div class="feature-icon">✨</div>
                    <h3>Premium Quality</h3>
                    <p>100% authentic sneakers verified and guaranteed for quality and originality.</p>
                </div>
                <div class="feature-card">
                    <div class="feature-icon">🎨</div>
                    <h3>Custom Designs</h3>
                    <p>Personalized sneaker customization services to make your kicks truly one-of-a-kind.</p>
                </div>
                <div class="feature-card">
                    <div class="feature-icon">🚀</div>
                    <h3>Fast Delivery</h3>
                    <p>Lightning-fast shipping to get your dream sneakers to your doorstep in record time.</p>
                </div>
                <div class="feature-card">
                    <div class="feature-icon">💎</div>
                    <h3>VIP Access</h3>
                    <p>Join our VIP club for early access to releases and exclusive member-only deals.</p>
                </div>
            </div>
        </div>
    </div>

    <!-- About Page -->
    <div id="about" class="page">
        <div class="about-page">
            <div class="about-content">
                <h2>About AGS Sneaker Hub</h2>
                <p>Welcome to AGS Sneaker Hub - where passion meets style. We're more than just a sneaker store; we're a community of sneaker enthusiasts dedicated to bringing you the finest footwear from around the globe.</p>
                <p>Founded by sneakerheads for sneakerheads, we understand what it takes to build the perfect collection. From classic retros to cutting-edge innovations, we curate every piece with care and authenticity.</p>
                <p>Our commitment is simple: provide access to the most coveted sneakers while maintaining the highest standards of quality and customer service. Your satisfaction is our passion.</p>
                
                <div class="stats">
                    <div class="stat-box">
                        <div class="stat-number">5000+</div>
                        <div class="stat-label">Sneakers Sold</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-number">2000+</div>
                        <div class="stat-label">Happy Customers</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-number">100%</div>
                        <div class="stat-label">Authentic</div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Contact Page -->
    <div id="contact" class="page">
        <div class="contact-page">
            <div class="contact-form">
                <h2>Get In Touch</h2>
                <form onsubmit="handleSubmit(event)">
                    <div class="form-group">
                        <label>Name</label>
                        <input type="text" placeholder="Your name" required>
                    </div>
                    <div class="form-group">
                        <label>Email</label>
                        <input type="email" placeholder="your@email.com" required>
                    </div>
                    <div class="form-group">
                        <label>Message</label>
                        <textarea placeholder="Looking for a specific sneaker? Let us know!" required></textarea>
                    </div>
                    <button type="submit" class="submit-btn">Send Message</button>
                </form>
            </div>
        </div>
    </div>

    <script>
        // Create floating sneaker icons
        function createParticles() {
            const hero = document.querySelector('.hero');
            if(hero) {
                const sneakerEmojis = ['👟', '👞', '🥾', '👠'];
                for(let i = 0; i < 15; i++) {
                    const particle = document.createElement('div');
                    particle.className = 'particle';
                    particle.textContent = sneakerEmojis[Math.floor(Math.random() * sneakerEmojis.length)];
                    particle.style.left = Math.random() * 100 + '%';
                    particle.style.top = Math.random() * 100 + '%';
                    particle.style.animationDelay = Math.random() * 10 + 's';
                    particle.style.animationDuration = (Math.random() * 10 + 15) + 's';
                    hero.appendChild(particle);
                }
            }
        }
        createParticles();

        // Navigation function
        function navigateTo(pageName) {
            // Remove active class from all pages
            document.querySelectorAll('.page').forEach(page => {
                page.classList.remove('active');
            });
            
            // Remove active class from all nav links
            document.querySelectorAll('.nav-links a').forEach(link => {
                link.classList.remove('active');
            });
            
            // Add active class to target page
            document.getElementById(pageName).classList.add('active');
            
            // Add active class to corresponding nav link
            document.querySelectorAll('.nav-links a').forEach(link => {
                if(link.textContent.toLowerCase() === pageName || 
                   (pageName === 'features' && link.textContent.toLowerCase() === 'collection')) {
                    link.classList.add('active');
                }
            });
            
            // Scroll to top smoothly
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // Handle form submission
        function handleSubmit(e) {
            e.preventDefault();
            alert('Thank you for reaching out! We will get back to you soon with the freshest kicks!');
            e.target.reset();
        }
    </script>
</body>
</html>
