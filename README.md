<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YouTube Tags & Hashtags Generator</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        :root {
            --primary: #FF0000;
            --secondary: #282828;
            --accent: #065FD4;
            --light: #f8f9fa;
            --gray: #6c757d;
            --success: #28a745;
            --warning: #ffc107;
        }

        body {
            background-color: white;
            color: #333;
            line-height: 1.6;
        }

        /* Header Styles */
        header {
            background-color: white;
            color: var(--secondary);
            padding: 1.5rem 2rem;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .header-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            max-width: 1200px;
            margin: 0 auto;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 1.5rem;
            font-weight: 700;
        }

        .logo i {
            font-size: 1.8rem;
            color: var(--primary);
        }

        .logo span {
            background: linear-gradient(90deg, var(--primary), var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        nav ul {
            display: flex;
            list-style: none;
            gap: 2rem;
        }

        nav a {
            color: var(--secondary);
            text-decoration: none;
            font-weight: 500;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        nav a:hover {
            color: var(--primary);
        }

        /* Main Content Styles */
        main {
            max-width: 1200px;
            margin: 3rem auto;
            padding: 0 2rem;
        }

        .hero {
            text-align: center;
            padding: 3rem 1rem;
            margin-bottom: 3rem;
        }

        .hero h1 {
            font-size: 2.5rem;
            margin-bottom: 1rem;
            color: var(--secondary);
        }

        .hero p {
            color: var(--gray);
            max-width: 700px;
            margin: 0 auto 2rem;
            font-size: 1.1rem;
        }

        .generator-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 2rem;
            margin-bottom: 3rem;
        }

        @media (max-width: 768px) {
            .generator-container {
                grid-template-columns: 1fr;
            }
        }

        .input-section, .output-section {
            background: white;
            border-radius: 10px;
            padding: 2rem;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            border: 1px solid #eaeaea;
        }

        .section-title {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 1.5rem;
            color: var(--secondary);
            font-size: 1.3rem;
        }

        .section-title i {
            color: var(--primary);
        }

        .input-group {
            margin-bottom: 1.5rem;
        }

        .keyword-input {
            width: 100%;
            padding: 1rem 1.5rem;
            border: 2px solid #e1e5e9;
            border-radius: 8px;
            font-size: 1rem;
            outline: none;
            transition: all 0.3s ease;
        }

        .keyword-input:focus {
            border-color: var(--primary);
        }

        .generate-btn {
            background: linear-gradient(135deg, var(--primary), var(--accent));
            color: white;
            border: none;
            padding: 1rem 2rem;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 8px;
            width: 100%;
            justify-content: center;
        }

        .generate-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(255, 0, 0, 0.2);
        }

        .generate-btn:disabled {
            opacity: 0.7;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }

        .output-area {
            min-height: 200px;
            border: 1px solid #e1e5e9;
            border-radius: 8px;
            padding: 1.5rem;
            background-color: #f9f9f9;
            margin-bottom: 1.5rem;
        }

        .tags-container {
            display: flex;
            flex-wrap: wrap;
            gap: 0.5rem;
        }

        .tag {
            background: white;
            border: 1px solid #e1e5e9;
            border-radius: 20px;
            padding: 0.5rem 1rem;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .tag.hashtag {
            background: #f0f8ff;
            border-color: var(--accent);
            color: var(--accent);
        }

        .copy-btn {
            background: var(--success);
            color: white;
            border: none;
            padding: 0.8rem 1.5rem;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 8px;
            width: 100%;
            justify-content: center;
        }

        .copy-btn:hover {
            background: #218838;
        }

        /* Features Section */
        .features {
            background: white;
            border-radius: 10px;
            padding: 3rem 2rem;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            border: 1px solid #eaeaea;
            margin-bottom: 3rem;
        }

        .features h2 {
            text-align: center;
            margin-bottom: 2.5rem;
            font-size: 2rem;
            color: var(--secondary);
        }

        .features-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 2rem;
        }

        .feature {
            text-align: center;
            padding: 1.5rem;
            border-radius: 10px;
            transition: all 0.3s ease;
        }

        .feature:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
        }

        .feature-icon {
            width: 70px;
            height: 70px;
            margin: 0 auto 1.5rem;
            background: linear-gradient(135deg, var(--primary), var(--accent));
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.8rem;
        }

        .feature h3 {
            margin-bottom: 1rem;
            color: var(--secondary);
        }

        .feature p {
            color: var(--gray);
        }

        /* API Status */
        .api-status {
            text-align: center;
            margin-top: 1rem;
            padding: 0.5rem;
            border-radius: 5px;
            font-size: 0.9rem;
        }

        .api-status.active {
            background: rgba(40, 167, 69, 0.1);
            color: var(--success);
        }

        .api-status.inactive {
            background: rgba(255, 193, 7, 0.1);
            color: var(--warning);
        }

        .api-status.error {
            background: rgba(220, 53, 69, 0.1);
            color: #dc3545;
        }

        /* Loading Spinner */
        .spinner {
            display: none;
            width: 40px;
            height: 40px;
            margin: 0 auto;
            border: 4px solid rgba(255, 0, 0, 0.2);
            border-radius: 50%;
            border-top: 4px solid var(--primary);
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* Footer */
        footer {
            background: var(--secondary);
            color: white;
            text-align: center;
            padding: 2rem;
            margin-top: 3rem;
        }

        .footer-links {
            display: flex;
            justify-content: center;
            gap: 2rem;
            margin-bottom: 1.5rem;
        }

        .footer-links a {
            color: white;
            text-decoration: none;
            transition: all 0.3s ease;
        }

        .footer-links a:hover {
            color: var(--primary);
        }

        .copyright {
            color: #aaa;
            font-size: 0.9rem;
        }

        /* Responsive Styles */
        @media (max-width: 768px) {
            .header-container {
                flex-direction: column;
                gap: 1rem;
            }

            nav ul {
                gap: 1rem;
            }

            .hero h1 {
                font-size: 2rem;
            }

            .features-container {
                grid-template-columns: 1fr;
            }
        }

        @media (max-width: 576px) {
            main {
                padding: 0 1rem;
            }

            .hero {
                padding: 2rem 1rem;
            }

            .hero h1 {
                font-size: 1.8rem;
            }

            .input-section, .output-section {
                padding: 1.5rem;
            }

            .footer-links {
                flex-direction: column;
                gap: 1rem;
            }
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <div class="header-container">
            <div class="logo">
                <i class="fab fa-youtube"></i>
                <span>YT Tags Generator</span>
            </div>
            <nav>
                <ul>
                    <li><a href="#"><i class="fas fa-home"></i> Home</a></li>
                    <li><a href="#"><i class="fas fa-info-circle"></i> About</a></li>
                    <li><a href="#"><i class="fas fa-question-circle"></i> Help</a></li>
                    <li><a href="#"><i class="fas fa-envelope"></i> Contact</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <!-- Main Content -->
    <main>
        <section class="hero">
            <h1>YouTube Tags & Hashtags Generator</h1>
            <p>Generate optimized tags and hashtags for your YouTube videos to improve visibility and reach more viewers. No subscription required!</p>
        </section>

        <section class="generator-container">
            <div class="input-section">
                <h2 class="section-title">
                    <i class="fas fa-keyboard"></i>
                    <span>Enter Your Keyword</span>
                </h2>
                <div class="input-group">
                    <input type="text" class="keyword-input" id="keywordInput" placeholder="Enter your keyword (e.g., Email Marketing)">
                </div>
                <button class="generate-btn" id="generateBtn">
                    <i class="fas fa-magic"></i> Generate Tags & Hashtags
                </button>
                
                <div class="api-status active" id="apiStatus">
                    <i class="fas fa-circle"></i> System Ready - Using Smart Generator
                </div>
                
                <div class="spinner" id="spinner"></div>
            </div>

            <div class="output-section">
                <h2 class="section-title">
                    <i class="fas fa-tags"></i>
                    <span>Generated Results</span>
                </h2>
                <div class="output-area" id="outputArea">
                    <p id="placeholderText">Your generated tags and hashtags will appear here...</p>
                    <div class="tags-container" id="tagsContainer"></div>
                </div>
                <button class="copy-btn" id="copyBtn">
                    <i class="fas fa-copy"></i> Copy All Tags
                </button>
            </div>
        </section>

        <section class="features">
            <h2>Why Use Our Tag Generator?</h2>
            <div class="features-container">
                <div class="feature">
                    <div class="feature-icon">
                        <i class="fas fa-bolt"></i>
                    </div>
                    <h3>Fast Generation</h3>
                    <p>Get relevant tags and hashtags in seconds with our optimized algorithm.</p>
                </div>
                <div class="feature">
                    <div class="feature-icon">
                        <i class="fas fa-chart-line"></i>
                    </div>
                    <h3>SEO Optimized</h3>
                    <p>Improve your video's search ranking with carefully selected tags.</p>
                </div>
                <div class="feature">
                    <div class="feature-icon">
                        <i class="fas fa-users"></i>
                    </div>
                    <h3>Increase Reach</h3>
                    <p>Expand your audience with hashtags that attract more viewers.</p>
                </div>
                <div class="feature">
                    <div class="feature-icon">
                        <i class="fas fa-rocket"></i>
                    </div>
                    <h3>Completely Free</h3>
                    <p>No subscriptions, no hidden fees - generate unlimited tags for free.</p>
                </div>
            </div>
        </section>
    </main>

    <!-- Footer -->
    <footer>
        <div class="footer-links">
            <a href="#">Home</a>
            <a href="#">About</a>
            <a href="#">Privacy Policy</a>
            <a href="#">Terms of Service</a>
            <a href="#">Contact</a>
        </div>
        <p class="copyright">© 2023 YouTube Tags Generator. All rights reserved.</p>
    </footer>

    <script>
        // DOM Elements
        const generateBtn = document.getElementById('generateBtn');
        const keywordInput = document.getElementById('keywordInput');
        const outputArea = document.getElementById('outputArea');
        const tagsContainer = document.getElementById('tagsContainer');
        const copyBtn = document.getElementById('copyBtn');
        const spinner = document.getElementById('spinner');
        const apiStatus = document.getElementById('apiStatus');
        const placeholderText = document.getElementById('placeholderText');

        // Tag database for fallback
        const tagDatabase = {
            'email marketing': [
                'email marketing', 'email campaign', 'email strategy', 'digital marketing', 
                'email automation', 'lead generation', 'newsletter', 'email design',
                'marketing tips', 'business growth', 'email software', 'conversion rate',
                'email list', 'segmentation', 'personalization', 'click through rate',
                'email analytics', 'cold email', 'email templates', 'subject lines'
            ],
            'cooking': [
                'cooking', 'recipes', 'food', 'cooking tips', 'easy recipes', 
                'home cooking', 'cooking tutorial', 'quick meals', 'healthy cooking',
                'cooking techniques', 'beginner cooking', 'cooking hacks', 'meal prep',
                'cooking show', 'food preparation', 'culinary skills', 'kitchen tips',
                'cooking basics', 'food tutorial', 'cooking channel'
            ],
            'fitness': [
                'fitness', 'workout', 'exercise', 'gym', 'fitness tips', 
                'home workout', 'fitness routine', 'bodybuilding', 'cardio',
                'strength training', 'fitness motivation', 'health', 'wellness',
                'fitness journey', 'weight loss', 'muscle building', 'fitness guide',
                'fitness for beginners', 'workout plan', 'fitness goals'
            ],
            'programming': [
                'programming', 'coding', 'web development', 'software development', 
                'programming tutorial', 'coding tips', 'learn to code', 'programming languages',
                'javascript', 'python', 'java', 'html css', 'web design', 'app development',
                'coding for beginners', 'programming projects', 'code review', 'debugging',
                'programming career', 'software engineering'
            ],
            'travel': [
                'travel', 'travel vlog', 'adventure', 'travel tips', 'travel guide',
                'backpacking', 'solo travel', 'travel destinations', 'budget travel',
                'travel hacking', 'travel photography', 'cultural travel', 'road trip',
                'travel inspiration', 'wanderlust', 'travel experiences', 'travel planning',
                'travel advice', 'travel community', 'explore the world'
            ]
        };

        // Generate tags functionality - FIXED VERSION
        generateBtn.addEventListener('click', function() {
            const keyword = keywordInput.value.trim().toLowerCase();
            
            // Validate keyword
            if (!keyword) {
                alert('Please enter a keyword');
                return;
            }
            
            // Show loading spinner
            spinner.style.display = 'block';
            generateBtn.disabled = true;
            clearResults();
            
            // Use setTimeout to simulate async operation and allow UI to update
            setTimeout(() => {
                try {
                    let tags = [];
                    
                    // Try to find tags in our database first
                    if (tagDatabase[keyword]) {
                        tags = tagDatabase[keyword];
                        apiStatus.innerHTML = '<i class="fas fa-circle"></i> Using Smart Database';
                        apiStatus.className = 'api-status active';
                    } else {
                        // Generate tags based on keyword
                        tags = generateTagsFromKeyword(keyword);
                        apiStatus.innerHTML = '<i class="fas fa-circle"></i> Using AI Generator';
                        apiStatus.className = 'api-status active';
                    }
                    
                    // Display the tags
                    displayTags(tags, keyword);
                    
                } catch (error) {
                    console.error('Error generating tags:', error);
                    showError('Failed to generate tags. Please try again with a different keyword.');
                } finally {
                    // Hide loading spinner
                    spinner.style.display = 'none';
                    generateBtn.disabled = false;
                }
            }, 800);
        });

        // Generate tags based on keyword (fallback)
        function generateTagsFromKeyword(keyword) {
            const baseTags = [
                keyword,
                `${keyword} tips`,
                `${keyword} tutorial`,
                `how to ${keyword}`,
                `best ${keyword}`,
                `${keyword} for beginners`,
                `${keyword} guide`,
                `learn ${keyword}`,
                `${keyword} techniques`,
                `${keyword} 
