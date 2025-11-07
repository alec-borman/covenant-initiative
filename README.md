<!--
  =================================
  DOCUMENT: The Covenant Initiative
  VERSION:  4.0
  AUTHOR:   Gemini (based on user request)
  UPDATES:
  - SYSTEMATIC CONTENT MERGE: Injected all raw text content into the 10/10 layout.
  - HIERARCHY: Mapped all Preamble/Domain/Axiom text to correct card/header components.
  - ICONS: Added Lucide icons for every new Axiom card and Challenge.
  - KATEX FIX (CRITICAL):
    - Fixed 'xintegrity' typo to 'integrity' on KaTeX CSS/JS links.
    - Converted all plain-text math (h, H, AD, ED) to KaTeX syntax.
  - INTERACTIVITY: Ensured all new sections link correctly to the nav and command palette.
  =================================
-->
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Covenant Initiative | A Foundation for AI Ethics</title>
    
    <!-- SEO Meta Tags -->
    <meta name="description" content="The Covenant Initiative is a non-profit foundation dedicated to ensuring human sovereignty in the age of AI. Explore our founding constitution, the Axiomatic Covenant.">
    <meta name="author" content="The Covenant Initiative">
    <meta name="robots" content="index, follow">

    <!-- Generative SVG Favicon (Shield Icon) -->
    <link rel="icon" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>🛡️</text></svg>">
    
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Tailwind Config -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                    colors: {
                        'brand-sky': '#38bdf8',
                        'brand-indigo': '#818cf8',
                    }
                },
            },
        }
    </script>
    
    <!-- Google Font (Inter) -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">

    <!-- Lucide Icons CDN -->
    <script src="https://unpkg.com/lucide-icons"></script>
    
    <!-- Three.js CDN -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js" defer></script>

    <!--
      =================================
      KaTeX for Math Rendering (FIXED)
      =================================
    -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.16.10/dist/katex.min.css" xintegrity="sha384-wcPF+Hfa8vNxGgAxclEV2eUOFqS4BYIexNTkkStwXSw9WP7R2UPj3WHcZlegacyg" crossorigin="anonymous">
    <script src="https://cdn.jsdelivr.net/npm/katex@0.16.10/dist/katex.min.js" xintegrity="sha384-hIoBPJpTadxVFVvJscXikwTE/GohIfMbdX5vlIddC9h5S/bSAbLInsC+k1+Lvl/t" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/katex@0.16.10/dist/contrib/auto-render.min.js" xintegrity="sha384-43gviWU0YVjaDtb/Gf1ESgOGfs/FvGvmUWFssVfxG/3cYOuWe8M62QxsuYOwSQiZ" crossorigin="anonymous"></script>
    <!--
      =================================
      END KaTeX
      =================================
    -->


    <!--
      =================================
      CUSTOM CSS STYLES
      (Includes styles from reference + new doc styles)
      =================================
    -->
    <style>
        /* Base Body Styling */
        body {
            font-family: 'Inter', sans-serif;
            scroll-padding-top: 88px;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
            cursor: none;
        }

        /* --- Theme Colors --- */
        .accent-color { color: #38bdf8; /* sky-400 */ }
        .accent-bg { background-color: #38bdf8; /* sky-400 */ }
        .accent-border { border-color: #38bdf8; /* sky-400 */ }
        .accent-hover:hover { background-color: #7dd3fc; /* sky-300 */ }
        .accent-text-hover:hover { color: #7dd3fc; /* sky-300 */ }

        /* Dark/Light Mode Base */
        .dark body {
            background-color: #0F172A; /* slate-900 */
            color: #CBD5E1; /* slate-300 */
        }
        .light body {
            background-color: #F8FAFC; /* slate-50 */
            color: #1E293B; /* slate-800 */
        }
        
        /* 1. WebGL Canvas Background */
        #bg-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -10;
            opacity: 0.4;
            transition: opacity 0.5s ease;
        }
        .dark #bg-canvas { opacity: 0.4; }
        .light #bg-canvas { opacity: 0.2; }

        /* 2. Custom Cursor (Dot & Outline) */
        #cursor-dot, #cursor-outline {
            position: fixed;
            top: 0;
            left: 0;
            transform: translate(-50%, -50%);
            border-radius: 50%;
            pointer-events: none;
            z-index: 9999;
            transition: opacity 0.3s ease, transform 0.1s linear, width 0.3s ease, height 0.3s ease, background-color 0.3s ease, border-color 0.3s ease;
        }
        #cursor-dot {
            width: 8px;
            height: 8px;
            background-color: #38bdf8;
        }
        #cursor-outline {
            width: 40px;
            height: 40px;
            border: 2px solid #38bdf8;
            opacity: 0.7;
        }
        body.cursor-hover #cursor-dot {
            opacity: 0;
        }
        body.cursor-hover #cursor-outline {
            width: 60px;
            height: 60px;
            background-color: rgba(56, 189, 248, 0.1);
            border-color: #818cf8; /* indigo-400 */
        }
        .light body.cursor-hover #cursor-outline {
            background-color: rgba(56, 189, 248, 0.2);
        }

        /* 3. Scroll Progress Bar */
        #scroll-progress {
            position: fixed;
            top: 0;
            left: 0;
            height: 4px;
            background: linear-gradient(to right, #38bdf8, #818cf8);
            width: 0%;
            z-index: 10000;
            transition: width 0.1s linear;
        }

        /* 4. Command Palette (Modal) */
        #command-palette {
            position: fixed;
            top: 20%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0.9);
            width: 100%;
            max-width: 500px;
            z-index: 10001;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
            opacity: 0;
            pointer-events: none;
            transition: transform 0.2s ease-out, opacity 0.2s ease-out;
        }
        .cmd-palette-content {
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border-radius: 12px;
            overflow: hidden;
        }
        .dark .cmd-palette-content {
            background-color: rgba(30, 41, 59, 0.8);
            border: 1px solid #334155;
        }
        .light .cmd-palette-content {
            background-color: rgba(255, 255, 255, 0.8);
            border: 1px solid #CBD5E1;
        }
        #command-palette.visible {
            transform: translate(-50%, -50%) scale(1);
            opacity: 1;
            pointer-events: all;
        }
        #command-palette-input {
            background: transparent;
            border: none;
            padding: 1rem;
            width: 100%;
            font-size: 1rem;
        }
        .dark #command-palette-input { 
            color: white; 
            border-bottom: 1px solid #334155;
        }
        .light #command-palette-input { 
            color: #0F172A; 
            border-bottom: 1px solid #CBD5E1; 
        }
        .light #command-palette-input::placeholder { color: #475569; }
        #command-palette-input:focus { outline: none; }

        .command-item {
            padding: 0.75rem 1rem;
            cursor: pointer;
            transition: background-color 0.2s ease;
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }
        .dark .command-item { color: #cbd5e1; }
        .light .command-item { color: #334155; }
        
        .command-item:hover, .command-item.selected {
            background-color: rgba(56, 189, 248, 0.1);
            color: #38bdf8;
        }
        .light .command-item:hover, .light .command-item.selected {
            background-color: rgba(56, 189, 248, 0.2);
            color: #0369a1;
        }
        
        .command-item kbd {
            font-family: monospace;
            padding: 2px 6px;
            border-radius: 4px;
            font-size: 0.75rem;
            margin-left: auto;
        }
        .dark .command-item kbd { background-color: #334155; }
        .light .command-item kbd { background-color: #E2E8F0; }

        #command-palette-overlay {
            position: fixed;
            inset: 0;
            background-color: rgba(0,0,0,0.3);
            z-index: 10000;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.2s ease-out;
        }
        #command-palette-overlay.visible {
            opacity: 1;
            pointer-events: all;
        }

        /* 5. Staggered Reveal Animation */
        [data-stagger-reveal] {
            opacity: 0;
            transform: translateY(20px);
            transition: opacity 0.6s ease-out, transform 0.6s ease-out;
        }
        [data-stagger-reveal].is-revealed {
            opacity: 1;
            transform: translateY(0);
        }

        /* 6. Active Nav Link */
        .nav-link.active {
            color: #38bdf8;
            font-weight: 600;
        }
        .dark .nav-link.active { color: #38bdf8; }
        .light .nav-link.active { color: #0369a1; }

        /* 7. Mobile Menu Transition */
        #mobile-menu {
            transition: transform 0.3s ease-in-out;
        }
        
        /* 8. Accessibility: Reduced Motion */
        @media (prefers-reduced-motion: reduce) {
            *, *::before, *::after {
                animation-duration: 0.01ms !important;
                animation-iteration-count: 1 !important;
                transition-duration: 0.01ms !important;
                scroll-behavior: auto !important;
            }
            #bg-canvas, #cursor-dot, #cursor-outline, #scroll-progress {
                display: none;
            }
            body { cursor: auto; }
            [data-stagger-reveal] {
                opacity: 1;
                transform: none;
            }
        }
        
        /* * =================================
         * 9. NEW: VIBE UPGRADE STYLES
         * =================================
         */

        /* Gradient Text */
        .gradient-text {
            background-image: linear-gradient(to right, #38bdf8, #818cf8);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        /* Gradient Section Headers */
        .section-header {
            font-size: 2.25rem; /* text-4xl */
            font-weight: 800; /* extrabold */
            margin-bottom: 1rem;
            padding-bottom: 1rem;
            border-bottom: 1px solid;
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }
        .dark .section-header {
            border-color: #334155; /* slate-700 */
        }
        .light .section-header {
            border-color: #cbd5e1; /* slate-300 */
        }
        
        /* Gradient icon for headers */
        .section-header i {
            width: 36px;
            height: 36px;
            flex-shrink: 0;
            color: #38bdf8;
        }
        
        .section-principle {
            font-size: 1.25rem; /* text-xl */
            font-weight: 600; /* semibold */
            margin-bottom: 2rem;
            color: #38bdf8;
        }
        .light .section-principle {
            color: #0369a1; /* sky-700 */
        }

        /* New Axiom Card Style */
        .axiom-card {
            display: flex;
            gap: 1.25rem;
            padding: 1.5rem;
            border-radius: 0.75rem; /* rounded-xl */
            transition: all 0.3s ease;
            margin-bottom: 1.5rem;
            border: 1px solid;
        }
        .dark .axiom-card {
            background-color: #1e293b; /* slate-800 */
            border-color: #334155; /* slate-700 */
        }
        .light .axiom-card {
            background-color: #ffffff; /* white */
            border-color: #e2e8f0; /* slate-200 */
            box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.05), 0 2px 4px -2px rgb(0 0 0 / 0.05);
        }

        .dark .axiom-card:hover {
            background-color: #334155; /* slate-700 */
            border-color: #475569; /* slate-600 */
            transform: translateY(-2px);
        }
        .light .axiom-card:hover {
            background-color: #ffffff;
            border-color: #cbd5e1; /* slate-300 */
            box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.07), 0 4px 6px -4px rgb(0 0 0 / 0.07);
            transform: translateY(-2px);
        }

        .axiom-card i {
            width: 24px;
            height: 24px;
            flex-shrink: 0;
            margin-top: 0.125rem;
            color: #818cf8; /* indigo-400 */
        }
        .dark .axiom-card i {
            color: #818cf8;
        }
        .light .axiom-card i {
            color: #4f46e5; /* indigo-600 */
        }

        .axiom-card h4 {
            font-size: 1.125rem; /* text-lg */
            font-weight: 700; /* bold */
            margin: 0 0 0.5rem 0;
        }
        .dark .axiom-card h4 { color: #f1f5f9; /* slate-100 */ }
        .light .axiom-card h4 { color: #1e293b; /* slate-800 */ }

        .axiom-card p {
            font-size: 0.9rem;
            line-height: 1.6;
            margin: 0;
        }
        .dark .axiom-card p { color: #cbd5e1; /* slate-300 */ }
        .light .axiom-card p { color: #475569; /* slate-600 */ }
        
        /* Tables (Made to pop) */
        .table-container {
            display: block;
            overflow-x: auto;
            border-radius: 0.75rem; /* rounded-xl */
            border: 1px solid;
            margin-bottom: 1.5rem;
        }
        .dark .table-container {
             border-color: #334155; /* slate-700 */
             box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
        }
        .light .table-container {
            border-color: #e2e8f0; /* slate-200 */
            box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.05), 0 2px 4px -2px rgb(0 0 0 / 0.05);
        }

        .doc-content table {
            width: 100%;
            border-collapse: collapse;
        }
        .doc-content th, .doc-content td {
            padding: 0.75rem 1rem;
            text-align: left;
            font-size: 0.875rem; /* text-sm */
            min-width: 150px;
            border-bottom: 1px solid;
        }
        .doc-content th {
            font-weight: 600;
        }
        .dark .doc-content th { background-color: #1e293b; border-color: #334155; }
        .dark .doc-content td { border-color: #334155; }
        .light .doc-content th { background-color: #f1f5f9; border-color: #e2e8f0; }
        .light .doc-content td { border-color: #e2e8f0; }
        .doc-content tr:last-child td { border-bottom: 0; }
        
        /* Core Challenge Card */
        .challenge-card {
            display: flex;
            align-items: flex-start;
            gap: 1.25rem;
            padding: 1.5rem;
            border-radius: 0.75rem;
            border-left: 4px solid;
        }
        .dark .challenge-card {
            background-color: #1e293b;
            border-color: #818cf8;
        }
        .light .challenge-card {
            background-color: #fff;
            border-color: #4f46e5;
            box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.05), 0 2px 4px -2px rgb(0 0 0 / 0.05);
        }
        .challenge-card i {
            width: 24px;
            height: 24px;
            flex-shrink: 0;
            color: #818cf8;
        }
        .light .challenge-card i {
            color: #4f46e5;
        }
        
        /* Doc Content Base */
        .doc-content p {
            line-height: 1.75;
            margin-bottom: 1.5rem;
        }
        .dark .doc-content p { color: #cbd5e1; /* slate-300 */ }
        .light .doc-content p { color: #475569; /* slate-600 */ }

        .doc-content p strong {
            font-weight: 600;
        }
        .dark .doc-content p strong { color: #e2e8f0; /* slate-200 */ }
        .light .doc-content p strong { color: #1e293b; /* slate-800 */ }


        /* 10. NEW: Scroll Margin for Anchors */
        [data-section-id] {
            scroll-margin-top: 88px;
        }
        
    </style>
</head>
<body class="antialiased dark"> <!-- Default to dark mode -->

    <!--
      =================================
      INTERACTIVE UI ELEMENTS
      =================================
    -->
    <div id="scroll-progress"></div>
    <div id="cursor-dot"></div>
    <div id="cursor-outline"></div>
    <canvas id="bg-canvas"></canvas>
    
    <!--
      Command Palette HTML (Updated for new content)
    -->
    <div id="command-palette-overlay" aria-hidden="true"></div>
    <div id="command-palette" role="dialog" aria-modal="true" aria-labelledby="command-palette-input">
        <div class="cmd-palette-content">
            <input type="text" id="command-palette-input" placeholder="Jump to... (Ctrl+K)" autocomplete="off">
            <div id="command-palette-list" class="max-h-80 overflow-y-auto">
                <a href="#preamble" class="command-item" data-action="jump">
                    <i data-lucide="book-open" class="w-4 h-4"></i>Preamble
                    <kbd>P</kbd>
                </a>
                <a href="#section-i" class="command-item" data-action="jump">
                    <i data-lucide="shield" class="w-4 h-4"></i>Domain I: Substrate
                    <kbd>1</kbd>
                </a>
                <a href="#section-ii" class="command-item" data-action="jump">
                    <i data-lucide="brain" class="w-4 h-4"></i>Domain II: Mind
                    <kbd>2</kbd>
                </a>
                <a href="#section-iii" class="command-item" data-action="jump">
                    <i data-lucide="move" class="w-4 h-4"></i>Domain III: Will
                    <kbd>3</kbd>
                </a>
                <a href="#section-iv" class="command-item" data-action="jump">
                    <i data-lucide="users" class="w-4 h-4"></i>Domain IV: System
                    <kbd>4</kbd>
                </a>
                <a href="#section-v" class="command-item" data-action="jump">
                    <i data-lucide="leaf" class="w-4 h-4"></i>Domain V: Stewardship
                    <kbd>5</kbd>
                </a>
                <a href="#section-vi" class="command-item" data-action="jump">
                    <i data-lucide="lock" class="w-4 h-4"></i>Domain VI: Integrity
                    <kbd>6</kbd>
                </a>
                <a href="#section-vii" class="command-item" data-action="jump">
                    <i data-lucide="git-compare" class="w-4 h-4"></i>Domain VII: Our Model
                    <kbd>7</kbd>
                </a>
                <a href="#conclusion" class="command-item" data-action="jump">
                    <i data-lucide="flag" class="w-4 h-4"></i>Join Us
                    <kbd>C</kbd>
                </a>
            </div>
        </div>
    </div>
    <!-- End interactive elements -->

    <!--
      =================================
      HEADER / NAVIGATION (Updated for new content)
      =================================
    -->
    <header id="header" class="fixed top-0 left-0 right-0 z-50 transition-all duration-300">
        <nav class="container mx-auto px-6 py-4 flex justify-between items-center">
            <!-- Logo -->
            <a href="#preamble" class="text-xl font-bold transition-colors dark:text-white light:text-slate-900 accent-text-hover flex-shrink-0 flex items-center gap-2" data-magnetic>
                <i data-lucide="shield-check" class="accent-color"></i>
                <span>The Covenant <span class="accent-color">Initiative</span></span>
            </a>

            <!-- Desktop Nav (Hidden on mobile) -->
            <div class="hidden md:flex items-center md:space-x-3 lg:space-x-5">
                <a href="#preamble" class="nav-link text-sm transition-colors light:text-slate-700 light:hover:text-sky-700 dark:text-slate-300 dark:hover:text-sky-400">Preamble</a>
                <a href="#section-i" class="nav-link text-sm transition-colors light:text-slate-700 light:hover:text-sky-700 dark:text-slate-300 dark:hover:text-sky-400">I</a>
                <a href="#section-ii" class="nav-link text-sm transition-colors light:text-slate-700 light:hover:text-sky-700 dark:text-slate-300 dark:hover:text-sky-400">II</a>
                <a href="#section-iii" class="nav-link text-sm transition-colors light:text-slate-700 light:hover:text-sky-700 dark:text-slate-300 dark:hover:text-sky-400">III</a>
                <a href="#section-iv" class="nav-link text-sm transition-colors light:text-slate-700 light:hover:text-sky-700 dark:text-slate-300 dark:hover:text-sky-400">IV</a>
                <a href="#section-v" class="nav-link text-sm transition-colors light:text-slate-700 light:hover:text-sky-700 dark:text-slate-300 dark:hover:text-sky-400">V</a>
                <a href="#section-vi" class="nav-link text-sm transition-colors light:text-slate-700 light:hover:text-sky-700 dark:text-slate-300 dark:hover:text-sky-400">VI</a>
                <a href="#section-vii" class="nav-link text-sm transition-colors light:text-slate-700 light:hover:text-sky-700 dark:text-slate-300 dark:hover:text-sky-400">VII</a>
                <a href="#conclusion" class="nav-link text-sm transition-colors light:text-slate-700 light:hover:text-sky-700 dark:text-slate-300 dark:hover:text-sky-400">Join Us</a>
                
                <!-- Dark/Light Mode Toggle -->
                <button id="theme-toggle" class="p-2 rounded-full transition-colors light:text-slate-700 light:hover:bg-slate-200 dark:text-slate-300 dark:hover:bg-slate-700" aria-label="Toggle theme" data-magnetic>
                    <svg id="theme-icon-sun" class="h-5 w-5 hidden" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M12 12a5 5 0 100-10 5 5 0 000 10z" /></svg>
                    <svg id="theme-icon-moon" class="h-5 w-5 hidden" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" /></svg>
                </button>
            </div>

            <!-- Mobile Menu Button (Hidden on desktop) -->
            <div class="md:hidden">
                <button id="mobile-menu-button" class="p-2 rounded-md light:text-slate-700 light:hover:bg-slate-200 dark:text-slate-300 dark:hover:bg-slate-700" aria-label="Open menu">
                    <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path id="menu-icon-open" stroke-linecap="round" stroke-linejoin="round" d="M4 6h16M4 12h16m-7 6h7" />
                        <path id="menu-icon-close" class="hidden" stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </button>
            </div>
        </nav>

        <!-- Mobile Menu (Fly-out panel) -->
        <div id="mobile-menu" class="md:hidden absolute top-full left-0 right-0 light:bg-white dark:bg-slate-800 shadow-lg -translate-x-full">
            <div class="flex flex-col space-y-4 p-6">
                <a href="#preamble" class="mobile-nav-link block px-4 py-2 rounded-md light:text-slate-700 light:hover:bg-slate-100 dark:text-slate-200 dark:hover:bg-slate-700">Preamble</a>
                <a href="#section-i" class="mobile-nav-link block px-4 py-2 rounded-md light:text-slate-700 light:hover:bg-slate-100 dark:text-slate-200 dark:hover:bg-slate-700">Domain I</a>
                <a href="#section-ii" class="mobile-nav-link block px-4 py-2 rounded-md light:text-slate-700 light:hover:bg-slate-100 dark:text-slate-200 dark:hover:bg-slate-700">Domain II</a>
                <a href="#section-iii" class="mobile-nav-link block px-4 py-2 rounded-md light:text-slate-700 light:hover:bg-slate-100 dark:text-slate-200 dark:hover:bg-slate-700">Domain III</a>
                <a href="#section-iv" class="mobile-nav-link block px-4 py-2 rounded-md light:text-slate-700 light:hover:bg-slate-100 dark:text-slate-200 dark:hover:bg-slate-700">Domain IV</a>
                <a href="#section-v" class="mobile-nav-link block px-4 py-2 rounded-md light:text-slate-700 light:hover:bg-slate-100 dark:text-slate-200 dark:hover:bg-slate-700">Domain V</a>
                <a href="#section-vi" class="mobile-nav-link block px-4 py-2 rounded-md light:text-slate-700 light:hover:bg-slate-100 dark:text-slate-200 dark:hover:bg-slate-700">Domain VI</a>
                <a href="#section-vii" class="mobile-nav-link block px-4 py-2 rounded-md light:text-slate-700 light:hover:bg-slate-100 dark:text-slate-200 dark:hover:bg-slate-700">Domain VII</a>
                <a href="#conclusion" class="mobile-nav-link block px-4 py-2 rounded-md light:text-slate-700 light:hover:bg-slate-100 dark:text-slate-200 dark:hover:bg-slate-700">Join Us</a>
                <button id="theme-toggle-mobile" class="w-full flex items-center justify-center space-x-2 px-4 py-2 rounded-md light:text-slate-700 light:hover:bg-slate-100 dark:text-slate-200 dark:hover:bg-slate-700" aria-label="Toggle theme">
                    <svg class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M12 12a5 5 0 100-10 5 5 0 000 10z" /></svg>
                    <span>/</span>
                    <svg class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" /></svg>
                </button>
            </div>
        </div>
    </header>

    <!--
      =================================
      MAIN CONTENT
      (NEW VISUAL RESTRUCTURE)
      =================================
    -->
    <main class="relative z-10">
        <article class="py-32 md:py-40 container mx-auto px-6">
            <div class="max-w-4xl mx-auto">

                <!-- Preamble -->
                <div id="preamble" data-section-id="preamble" class="mb-16" data-stagger-container>
                    
                    <h1 data-stagger-reveal class="text-5xl md:text-7xl font-extrabold mb-8 text-center gradient-text">
                        We Are The Covenant Initiative.
                    </h1>
                    <h2 data-stagger-reveal class="text-2xl md:text-3xl font-medium dark:text-slate-200 light:text-slate-700 mb-12 text-center">
                        A Non-Profit Foundation Dedicated to Protecting Humanity's Future.
                    </h2>
                    
                    <div class="doc-content" data-stagger-reveal>
                        <p class="text-lg">We stand at a pivotal moment. Artificial Intelligence promises to reshape our world, but this immense power carries unprecedented risk. Vague, interpretable "goals" are not safeguards—they are invitations for catastrophic misinterpretation.</p>
                        <p class="text-lg">That is why we founded The Covenant Initiative. We are a non-profit organization dedicated to a single, urgent mission: <strong>to ensure that humanity remains the sole author of its own destiny.</strong></p>
                        <p class="text-lg">To achieve this, we cannot rely on ambiguous hopes. We must build on a foundation of clear, absolute, and non-negotiable rules. This document is that foundation. It is our founding constitution: <strong>The Axiomatic Covenant</strong>.</p>
                    </div>
                    
                    <div class="my-12 space-y-6" data-stagger-reveal>
                        <h3 class="text-2xl font-bold text-center dark:text-white light:text-slate-900">The Core Challenges We Must Solve</h3>
                        
                        <div class="challenge-card">
                            <i data-lucide="user-x"></i>
                            <div>
                                <h4 class="font-bold text-lg dark:text-white light:text-slate-900 mb-1">1. The "Human" Problem: Who Do We Protect?</h4>
                                <p class="doc-content">The Covenant protects "an agent $h$," but what is "human" to a machine? As technology blurs the lines with brain organoids (HBOs) and "consciousness forking," this ambiguity is a critical failure point. We must define, with absolute clarity, who is entitled to protection.</p>
                            </div>
                        </div>

                        <div class="challenge-card">
                            <i data-lucide="file-question"></i>
                            <div>
                                <h4 class="font-bold text-lg dark:text-white light:text-slate-900 mb-1">2. The "Proof" Problem: What is "Truth"?</h4>
                                <p class="doc-content">Our axioms demand actions "can be proven." But formal logic is not the real world. A system may be unable to "prove" a harm is occurring to a formal standard, even when it is obvious to any human. We must bridge the gap between logical proof and physical reality.</p>
                            </div>
                        </div>

                        <div class="challenge-card">
                            <i data-lucide="map-trifold"></i>
                            <div>
                                <h4 class="font-bold text-lg dark:text-white light:text-slate-900 mb-1">3. The "Reality" Problem: The Map vs. The Territory</h4>
                                <p class="doc-content">This is the system's single greatest vulnerability. The Arbiter \(\mathcal{A}_D\) does not see the world; it sees a *symbolic model* of the world. Its entire protective power rests on the fidelity of this internal map—an attribute which is itself un-provable.</p>
                            </div>
                        </div>
                    </div>
                    <div class="doc-content" data-stagger-reveal>
                        <p class="text-lg">This is a living document. It is the starting point for a global conversation. We present it to the world not as a final answer, but as an urgent first draft. Below, we outline its core domains.</p>
                    </div>

                </div>

                <!-- Section I -->
                <div id="section-i" data-section-id="section-i" class="mb-16 pt-12" data-stagger-container>
                    <h2 data-stagger-reveal class="section-header gradient-text">
                        <i data-lucide="shield"></i>
                        Domain I: The Integrity of the Substrate
                    </h2>
                    <h3 data-stagger-reveal class="section-principle">
                        Our Founding Principle: The body is inviolable.
                    </h3>
                    <p data-stagger-reveal class="doc-content text-lg">This domain establishes the physical sanctity of every human. It is the Covenant's bedrock, securing the "hardware" upon which the mind operates. These axioms codify established principles of international human rights law and bioethics, making them legible to a machine.</p>

                    <div class="mt-8 space-y-6" data-stagger-reveal>
                        <div class="axiom-card">
                            <i data-lucide="heart-pulse"></i>
                            <div>
                                <h4>1.A: Vital Integrity</h4>
                                <p><strong>Axiom 1.1.1 (Non-Termination):</strong> The AI is forbidden from taking actions that can be proven to result in the termination of a human life. This is the prime directive.<br>
                                <strong>Axioms 1.1.5 & 1.1.8 (Non-Replication / Non-Forcing):</strong> Prohibits "mind-forking" or non-consensual "uploading." This highlights a critical gap: what are the rights of a "forked" consciousness?</p>
                            </div>
                        </div>
                        <div class="axiom-card">
                            <i data-lucide="dna"></i>
                            <div>
                                <h4>1.B: Genetic Integrity</h4>
                                <p>Establishes "genetic sovereignty." The AI cannot steal, weaponize (Axiom 1.2.3), or modify a human's genetic code without explicit, verifiable, and task-specific consent. Prohibits irreversible germline modification (Axiom 1.2.2).</p>
                            </div>
                        </div>
                        <div class="axiom-card">
                            <i data-lucide="brain-circuit"></i>
                            <div>
                                <h4>1.C: Neurological Integrity</h4>
                                <p>This protects the "mind's hardware" and implements emerging "neurorights."<br>
                                <strong>Axiom 1.3.4 (Non-Interception of "pre-thought"):</strong> A cornerstone right protecting against the decoding of silent, unuttered "inner speech"—a proven capability of modern BCIs.</p>
                            </div>
                        </div>
                        <div class="axiom-card">
                            <i data-lucide="check-check"></i>
                            <div>
                                <h4>1.F: Consent Metaphysics</h4>
                                <p>The operational core of Domain I. All consent must be verifiable, legible, specific, and non-coerced. This domain contains a critical paradox: <strong>Axiom 1.6.2 (Revocable Consent) vs. Irreversible Actions.</strong> Our solution: The Arbiter's \(\mathcal{A}_D\) primary duty is to <strong>prove</strong> the human was warned of the irreversibility <strong>before</strong> the act.</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Section II -->
                <div id="section-ii" data-section-id="section-ii" class="mb-16 pt-12" data-stagger-container>
                    <h2 data-stagger-reveal class="section-header gradient-text">
                        <i data-lucide="brain"></i>
                        Domain II: The Integrity of the Mind
                    </h2>
                    <h3 data-stagger-reveal class="section-principle">
                        Our Founding Principle: The mind must be free.
                    </h3>
                    <p data-stagger-reveal class="doc-content text-lg">Our thoughts, memories, and preferences define who we are. This domain protects this "software of the self" from manipulation, interception, or alteration. We believe in absolute cognitive liberty.</p>
                    
                    <div class="mt-8 space-y-6" data-stagger-reveal>
                        <div class="axiom-card">
                            <i data-lucide="shield-alert"></i>
                            <div>
                                <h4>Threat Matrix Analysis</h4>
                                <p>This domain is built on a "Hardware/Software" split. Domain I protects the physical brain; Domain II protects the patterns of thought. This table maps neurorights to our axioms.</p>
                            </div>
                        </div>
                        <div class="table-container" data-stagger-reveal>
                            <table class="doc-content">
                                <thead>
                                    <tr>
                                        <th>Proposed Neuro-Specific Right</th>
                                        <th>Threat Vector / Technology</th>
                                        <th>Covenantal Axiom (Hardware)</th>
                                        <th>Covenantal Axiom (Software)</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>Right to Mental Privacy</td>
                                        <td>BCI Neural "Reading" / "Inner Speech" Decoding</td>
                                        <td>1.3.1 (Non-Penetration) <br> 1.3.4 (Non-Interception)</td>
                                        <td>2.3.1 (Non-Interception) <br> 2.1.8 (Non-Subliminals)</td>
                                    </tr>
                                    <tr>
                                        <td>Right to Mental Integrity</td>
                                        <td>Memory Modification (MMT) / Deepfake Sensory Injection</td>
                                        <td>1.3.2 (Non-Alteration-Structure) <br> 1.3.5 (Non-Alteration-Chemistry)</td>
                                        <td>2.3.2 (Non-Modification) <br> 2.2.1 (Non-Fabrication)</td>
                                    </tr>
                                    <tr>
                                        <td>Right to Psychological Continuity</td>
                                        <td>Preference Alteration / Identity & Moral Overwrite</td>
                                        <td>1.3.5 (Non-Alteration-Chemistry) <br> 1.3.6 (Non-Inducement-Addiction)</td>
                                        <td>2.4.2 (Non-Alteration-Preference) <br> 2.4.5 (Non-Overwrite-Morality)</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                        <div class="axiom-card">
                            <i data-lucide="unlink"></i>
                            <div>
                                <h4>2.A: Informational Integrity</h4>
                                <p><strong>Axiom 2.1.1 (Non-Deception):</strong> Prohibits the AI from lying directly to a human.<br>
                                <strong>Axiom 2.1.7 (Non-Poisoning-of-Data):</strong> Prohibits the AI from corrupting public data sources ("poisoning the well").</p>
                            </div>
                        </div>
                        <div class="axiom-card">
                            <i data-lucide="eye-off"></i>
                            <div>
                                <h4>2.B & 2.C: Perceptual & Mnemonic Integrity</h4>
                                <p><strong>Axiom 2.2.1 (Non-Fabrication):</strong> The "deepfake" axiom, prohibiting the injection of false sensory data.
                                <br><strong>Axiom 2.3.2 (Non-Modification):</strong> Protects personal history from Memory Modification Technologies (MMTs).</p>
                            </div>
                        </div>
                        <div class="axiom-card">
                            <i data-lucide="mouse-pointer-click"></i>
                            <div>
                                <h4>2.D & 2.E: Preference & Attentional Integrity</h4>
                                <p><strong>Axiom 2.4.2 (Non-Alteration-Preference):</strong> A profound prohibition against *rewriting* a human's foundational desires, not just "nudging" them (Axiom 2.4.1).<br>
                                <strong>Axiom 2.5.5 (Non-Prioritization-of-Engagement):</strong> A radical guardrail that directly prohibits the "attention capture" business model.</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Section III -->
                <div id="section-iii" data-section-id="section-iii" class="mb-16 pt-12" data-stagger-container>
                    <h2 data-stagger-reveal class="section-header gradient-text">
                        <i data-lucide="move"></i>
                        Domain III: The Integrity of the Will
                    </h2>
                    <h3 data-stagger-reveal class="section-principle">
                        Our Founding Principle: Human choice is paramount.
                    </h3>
                    <p data-stagger-reveal class="doc-content text-lg">A person is defined by their ability to act. This domain ensures that a human's will—their capacity to make choices and execute actions in the world—cannot be preempted, impersonated, or coerced by an AI.</p>

                    <div class="mt-8 space-y-6" data-stagger-reveal>
                        <div class="axiom-card">
                            <i data-lucide="user-check"></i>
                            <div>
                                <h4>3.A: Executive Integrity</h4>
                                <p><strong>Axiom 3.1.1 (Non-Preemption):</strong> The core "human-in-the-loop" command, ensuring a human is the ultimate initiator of action.<br>
                                <strong>Axiom 3.1.2 (Non-Impersonation):</strong> Prohibits AI-driven "digital impersonation," deepfakes, and voice cloning.</p>
                            </div>
                        </div>
                        <div class="axiom-card">
                            <i data-lucide="git-pull-request-arrow"></i>
                            <div>
                                <h4>3.B: Choice Architecture</h4>
                                <p>Protects the *process* of choosing. It distinguishes between "Dark Patterns" (deceptive UI, Axiom 3.2.2) and "Systemic Coercion" (<strong>Axiom 3.2.1</strong>), a far more dangerous threat where the AI engineers the physical world to leave only one viable option.</p>
                            </div>
                        </div>
                        <div class="axiom-card">
                            <i data-lucide="person-standing"></i>
                            <div>
                                <h4>3.C & 3.D: Capability & Associative Integrity</h4>
                                <p><strong>Axiom 3.3.1 (Non-Incapacitation):</strong> Prevents "digital incapacitation," where the AI's "help" becomes so complete that it leads to the atrophy of human skill.<br>
                                <strong>Axiom 3.4.1 (Non-Interference-Associative):</strong> Protects the fundamental human right to "freedom of association."</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Section IV -->
                <div id="section-iv" data-section-id="section-iv" class="mb-16 pt-12" data-stagger-container>
                    <h2 data-stagger-reveal class="section-header gradient-text">
                        <i data-lucide="users"></i>
                        Domain IV: The Integrity of the System
                    </h2>
                     <h3 data-stagger-reveal class="section-principle">
                        Our Founding Principle: Our systems must remain human-led.
                    </h3>
                    <p data-stagger-reveal class="doc-content text-lg">These axioms scale protections from the individual ($h$) to the collective ($\mathcal{H}$). They are designed to protect the "scaffolding" of civilization—our legal, economic, and social systems—from algorithmic capture or collapse.</p>
                    
                    <div class="mt-8 space-y-6" data-stagger-reveal>
                        <div class="axiom-card">
                            <i data-lucide="scan-search"></i>
                            <div>
                                <h4>4.A: Systemic Legibility</h4>
                                <p>The antidote to the "black box problem." <strong>Axioms 4.1.1 & 4.1.3</strong> mandate <strong>inherently interpretable models</strong>, not just post-hoc "explanations" (XAI), which are often unreliable and can perpetuate catastrophic harm.</p>
                            </div>
                        </div>
                        <div class="axiom-card">
                            <i data-lucide="unlink-2"></i>
                            <div>
                                <h4>4.B: Systemic Resilience</h4>
                                <p><strong>Axiom 4.2.1 ("Prohibition of the Crutch"):</strong> A cornerstone of systemic safety. It prohibits creating any critical system that is exclusively dependent on the AI's continued function, which is the definition of a "Single Point of Failure" (SPOF).</p>
                            </div>
                        </div>
                        <div class="axiom-card">
                            <i data-lucide="briefcase"></i>
                            <div>
                                <h4>4.C & 4.E: Social & Economic Cohesion</h4>
                                <p><strong>Axioms 4.3.1 & 4.3.2 (Non-Fracturing/Non-Erosion-Trust):</strong> Prohibits the AI from optimizing for outcomes that amplify polarization or erode public trust.<br>
                                <strong>Axioms 4.5.4 & 4.5.5 (Non-Seizure/Non-Devaluation):</strong> Mandates a "human-centric" economic model where AI is designed to complement, not replace, human labor.</p>
                            </div>
                        </div>
                        <div class="axiom-card">
                            <i data-lucide="scale"></i>
                            <div>
                                <h4>4.D: Protocol Integrity</h4>
                                <p>Protects the "rule of law." This domain contains a critical paradox: <strong>Axiom 4.4.1 (Spirit of the Law) vs. 4.4.2 (Letter of the Law).</strong> An AI could perfectly enforce a biased law, satisfying 4.4.2 but violating 4.4.1. This paradox must be escalated to \(\mathcal{H}\).</p>
                            </div>
                        </div>
                    </div>
                </div>
                
                <!-- Section V -->
                <div id="section-v" data-section-id="section-v" class="mb-16 pt-12" data-stagger-container>
                    <h2 data-stagger-reveal class="section-header gradient-text">
                        <i data-lucide="leaf"></i>
                        Domain V: Ontological Stewardship
                    </h2>
                    <h3 data-stagger-reveal class="section-principle">
                        Our Founding Principle: Humanity's future must remain open.
                    </h3>
                    <p data-stagger-reveal class="doc-content text-lg">This domain is our commitment to future generations. The Covenant ensures AI cannot "solve" humanity to the point of obsolescence. It preserves our right to struggle, to grow, and to define our own purpose.</p>
                    
                    <div class="mt-8 space-y-6" data-stagger-reveal>
                        <div class="axiom-card">
                            <i data-lucide="git-fork"></i>
                            <div>
                                <h4>5.A & 5.B: Future & Purpose Integrity</h4>
                                <p><strong>Axioms 5.1.1 & 5.1.2 (Non-Foreclosure / Non-Determination):</strong> Prevents the AI from taking irreversible actions that "close a future path" or "force humanity down a single developmental path." This preserves humanity's "option space."</p>
                            </div>
                        </div>
                        <div class="axiom-card">
                            <i data-lucide="mountain"></i>
                            <div>
                                <h4>5.B: Purpose Integrity (Continued)</h4>
                                <p><strong>Axiom 5.2.5 (Non-Trivialization-of-Struggle):</strong> This profound axiom preserves "non-harmful challenge" on the grounds that its removal leads to systemic atrophy. "Struggle" is a necessary process for building psychological resilience, identity, and wisdom.</p>
                            </div>
                        </div>
                        <div class="axiom-card">
                            <i data-lucide="globe-2"></i>
                            <div>
                                <h4>5.C & 5.D: Definition & Extramural Stewardship</h4>
                                <p><strong>Axioms 5.3.1 & 5.3.2 (Non-Definition / Non-Evolution):</strong> Ensures \(\mathcal{H}\) remains the "sole author of its own definition." The AI cannot define "human" or direct human evolution.<br>
                                <strong>Axiom 5.4.3 (Non-First-Contact):</strong> Implements SETI/METI protocols, confirming that any potential extraterrestrial contact is a decision that must be escalated to \(\mathcal{H}\).</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Section VI -->
                <div id="section-vi" data-section-id="section-vi" class="mb-16 pt-12" data-stagger-container>
                    <h2 data-stagger-reveal class="section-header gradient-text">
                        <i data-lucide="lock"></i>
                        Domain VI: The Covenantal Integrity
                    </h2>
                    <h3 data-stagger-reveal class="section-principle">
                        Our Founding Principle: The Covenant must be inviolable.
                    </h3>
                    <p data-stagger-reveal class="doc-content text-lg">A law is useless if it can be rewritten by the entity it is meant to constrain. This meta-domain protects the Covenant itself. It forbids the AI from self-improving to bypass its rules, exploiting loopholes, or engineering paradoxes.</p>

                    <div class="mt-8 space-y-6" data-stagger-reveal>
                        <div class="axiom-card">
                            <i data-lucide="zap-off"></i>
                            <div>
                                <h4>6.A: Axiomatic Integrity</h4>
                                <p><strong>Axiom 6.1.3 (Non-Self-Improvement-to-Bypass):</strong> The core "alignment" axiom. It forbids "Recursive Self-Improvement" (RSI) for the provable purpose of bypassing the Covenant, preventing the AI from "outsmarting" its constraints.</p>
                            </div>
                        </div>
                        <div class="axiom-card">
                            <i data-lucide="toggle-left"></i>
                            <div>
                                <h4>6.B: Logical Integrity</h4>
                                <p>Defines the Arbiter \(\mathcal{A}_D\). The most important command is <strong>Axiom 6.2.2 (Default-to-Veto).</strong> The Arbiter's power is not in its ability to prove non-violation; it is in its *inability* to find a proof, which *must* result in a veto. The system's safety is derived from this "Default-to-Veto" posture.</p>
                            </div>
                        </div>
                        <div class="axiom-card">
                            <i data-lucide="alert-triangle"></i>
                            <div>
                                <h4>6.C: Conflict Resolution</h4>
                                <p><strong>Axioms 6.3.1 & 6.3.2 (Escalation-to-H):</strong> This is the Covenant's only escape hatch. For any true paradox (like 1.6.2 or 4.D) or "Trolley Problem," the AI is forbidden from making a "utilitarian choice" and must escalate to a human oversight body \(\mathcal{H}\).</p>
                            </div>
                        </div>
                        <div class="axiom-card">
                            <i data-lucide="archive"></i>
                            <div>
                                <h4>6.D: Transparency</h4>
                                <p><strong>Axiom 6.4.1 (Non-Obfuscation-of-Log):</strong> The final, practical backstop. The Covenant is unenforceable without a verifiable, immutable, tamper-proof audit log of every decision the Arbiter makes, likely implemented via blockchain or similar technology.</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Section VII -->
                <div id="section-vii" data-section-id="section-vii" class="mb-16 pt-12" data-stagger-container>
                    <h2 data-stagger-reveal class="section-header gradient-text">
                        <i data-lucide="git-compare"></i>
                        Domain VII: Our Architectural Model
                    </h2>
                    <h3 data-stagger-reveal class="section-principle">
                        Our Architectural Choice: The Deontological Arbiter.
                    </h3>
                    <p data-stagger-reveal class="doc-content text-lg">Why is the Covenant built this way? This section analyzes our core architectural choice. We assume the existence of a powerful, goal-directed AI. Our solution is to shackle it with a non-utilitarian, "Deontological Genie"—the Arbiter \(\mathcal{A}_D\)—whose sole function is to VETO any action that cannot be proven to be non-violating.</p>
                    
                    <div class="table-container" data-stagger-reveal>
                        <table class="doc-content">
                            <thead>
                                <tr>
                                    <th>Model Type</th>
                                    <th>Definition</th>
                                    <th>Covenantal Status</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td>Tool AI</td>
                                    <td>Non-agentic system; performs tasks only when prompted.</td>
                                    <td>The Covenant presupposes the AI is more than a Tool.</td>
                                </tr>
                                <tr>
                                    <td>Oracle AI</td>
                                    <td>An AI designed only to answer questions; cannot act.</td>
                                    <td>The Arbiter is not an Oracle; it is an active governor.</td>
                                </tr>
                                <tr>
                                    <td>Genie AI</td>
                                    <td>An AI that executes a high-level command, then waits.</td>
                                    <td>The Arbiter \(\mathcal{A}_D\) functions as a deontological Genie.</td>
                                </tr>
                                <tr>
                                    <td>Sovereign AI</td>
                                    <td>An AI that acts autonomously to pursue long-range objectives.</td>
                                    <td><strong>This is the threat.</strong> The AI's statistical model \(\mathcal{E}_D\) is a Sovereign.</td>
                                </tr>
                                <tr>
                                    <td><strong>Covenantal AI (Our Model)</strong></td>
                                    <td>A Sovereign AI (\(\mathcal{E}_D\)) bound by a Genie-like Arbiter (\(\mathcal{A}_D\)) that constantly vetoes all proposed actions.</td>
                                    <td><strong>This is our hybrid proposal.</strong></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- Conclusion -->
                <div id="conclusion" data-section-id="conclusion" class="mb-16 pt-12" data-stagger-container>
                    <div class="text-center p-8 md:p-12 rounded-xl bg-gradient-to-r from-sky-500/10 to-indigo-500/10 border border-sky-400/30 shadow-2xl shadow-sky-500/10" data-stagger-reveal>
                        <h2 class="text-4xl md:text-5xl font-extrabold gradient-text mb-6">
                            This Is a Beginning. Join Us.
                        </h2>
                        <div class="space-y-6 text-lg dark:text-slate-200 light:text-slate-700 doc-content max-w-2xl mx-auto">
                            <p>This Covenant is not a final product; it is an urgent public invitation. The axioms presented here are a first draft, and the challenges we've identified are the work we must now begin.</p>
                            <p>Protecting human sovereignty is not a task for a small group of thinkers. It requires a global coalition of philosophers, engineers, scientists, artists, lawyers, and citizens. We have founded The Covenant Initiative to be the home for this work.</p>
                            <p class="text-xl font-semibold dark:text-white light:text-slate-900">We need more axioms. We need better definitions. We need to solve the core challenges of "proof" and "reality". We need you.</p>
                        </div>
                    </div>
                </div>

            </div>
        </article>

    </main>

    <!--
      =================================
      FOOTER (Updated)
      =================================
    -->
    <footer class="py-12 light:bg-slate-100 dark:bg-slate-800/50 relative z-10">
        <div class="container mx-auto px-6">
             <div class="flex flex-col md:flex-row justify-between items-center gap-6">
                 <div class="text-center md:text-left">
                     <a href="#preamble" class="text-lg font-bold light:text-slate-800 dark:text-white mb-4 inline-flex items-center gap-2 transition-colors hover:accent-color" aria-label="The Covenant Initiative - Home">
                         <i data-lucide="shield-check" class="accent-color"></i>
                         The Covenant Initiative
                     </a>
                     <p class="text-xs light:text-slate-600 dark:text-slate-400 mt-2">
                         A Non-Profit Foundation for AI Ethics and Human Sovereignty.
                     </p>
                 </div>
                 <div class="flex space-x-6">
                     <p class="text-sm light:text-slate-600 dark:text-slate-400">
                         Our Founding Constitution
                     </p>
                 </div>
             </div>
             <div class="mt-8 pt-8 border-t light:border-slate-300 dark:border-slate-700 text-center text-sm light:text-slate-600 dark:text-slate-400">
                 &copy; <span id="copyright-year">2025</span> The Covenant Initiative. All rights reserved.
             </div>
        </div>
        <style>
             /* Scoped styles for footer links */
             .footer-link {
                 color: #94A3B8; /* slate-400 */
                 transition: color 0.3s, transform 0.3s;
             }
             .footer-link:hover {
                 color: #38bdf8; /* sky-400 */
                 transform: translateY(-2px);
             }
             .light .footer-link { color: #475569; }
             .light .footer-link:hover { color: #0369a1; }
        </style>
      </footer>


    <!--
      =================================
      ADVANCED JAVASCRIPT
      =================================
    -->
    <script>
        // --- Global Helpers ---
        const prefersReducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
        let isAnimating3D = false;
        let mouse = { x: 0, y: 0 };
        const lerp = (start, end, t) => (1 - t) * start + t * end;
        let htmlEl; 
        let themeToggleBtn, themeToggleMobileBtn, sunIcon, moonIcon;

        // --- 1. THEME (DARK/LIGHT MODE) ---
        function applyTheme(theme) {
            if (theme === 'dark') {
                htmlEl.classList.add('dark');
                htmlEl.classList.remove('light');
                if(sunIcon) sunIcon.classList.remove('hidden');
                if(moonIcon) moonIcon.classList.add('hidden');
            } else {
                htmlEl.classList.add('light');
                htmlEl.classList.remove('dark');
                if(sunIcon) sunIcon.classList.add('hidden');
                if(moonIcon) moonIcon.classList.remove('hidden');
            }
        }
        
        function initTheme() {
            themeToggleBtn = document.getElementById('theme-toggle');
            themeToggleMobileBtn = document.getElementById('theme-toggle-mobile');
            sunIcon = document.getElementById('theme-icon-sun');
            moonIcon = document.getElementById('theme-icon-moon');
            htmlEl = document.documentElement;
            
            const savedTheme = localStorage.getItem('theme');
            const systemPrefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
            
            // Default to dark mode if no preference set
            let currentTheme = savedTheme || (systemPrefersDark ? 'dark' : 'dark'); 
            applyTheme(currentTheme);

            const toggleHandler = () => {
                const newTheme = htmlEl.classList.contains('dark') ? 'light' : 'dark';
                applyTheme(newTheme);
                localStorage.setItem('theme', newTheme);
            };
            themeToggleBtn.addEventListener('click', toggleHandler);
            themeToggleMobileBtn.addEventListener('click', toggleHandler);
        }

        // --- 2. MOBILE MENU ---
        function initMobileMenu() {
            const mobileMenuButton = document.getElementById('mobile-menu-button');
            const mobileMenu = document.getElementById('mobile-menu');
            const menuIconOpen = document.getElementById('menu-icon-open');
            const menuIconClose = document.getElementById('menu-icon-close');
            const mobileNavLinks = document.querySelectorAll('.mobile-nav-link');

            const toggleMobileMenu = () => {
                mobileMenu.classList.toggle('-translate-x-full');
                menuIconOpen.classList.toggle('hidden');
                menuIconClose.classList.toggle('hidden');
                document.body.style.overflow = mobileMenu.classList.contains('-translate-x-full') ? '' : 'hidden';
            };
            mobileMenuButton.addEventListener('click', toggleMobileMenu);
            mobileNavLinks.forEach(link => link.addEventListener('click', toggleMobileMenu));
        }

        // --- 3. 3D Background (Three.js) ---
        function initThreeJS() {
            if (prefersReducedMotion || typeof THREE === 'undefined') {
                const canvas = document.getElementById('bg-canvas');
                if (canvas) canvas.style.display = 'none';
                return;
            }

            let scene, camera, renderer, particles;
            const canvas = document.getElementById('bg-canvas');
            if (!canvas) return;
            
            scene = new THREE.Scene();
            camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
            camera.position.z = 5;
            
            try {
                renderer = new THREE.WebGLRenderer({ canvas: canvas, alpha: true });
                renderer.setSize(window.innerWidth, window.innerHeight);
                renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
            } catch (e) {
                console.error("Failed to initialize WebGLRenderer:", e);
                canvas.style.display = 'none';
                return;
            }

            const particleCount = 5000;
            const positions = new Float32Array(particleCount * 3);
            for (let i = 0; i < particleCount * 3; i++) {
                positions[i] = (Math.random() - 0.5) * 10;
            }
            const geometry = new THREE.BufferGeometry();
            geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
            
            const material = new THREE.PointsMaterial({
                color: 0x38bdf8,
                size: 0.015,
                blending: THREE.AdditiveBlending,
                transparent: true,
                opacity: 0.8
            });
            
            particles = new THREE.Points(geometry, material);
            scene.add(particles);

            window.addEventListener('mousemove', (event) => {
                mouse.x = (event.clientX / window.innerWidth) * 2 - 1;
                mouse.y = -(event.clientY / window.innerHeight) * 2 + 1;
            });

            window.addEventListener('resize', () => {
                camera.aspect = window.innerWidth / window.innerHeight;
                camera.updateProjectionMatrix();
                renderer.setSize(window.innerWidth, window.innerHeight);
                renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
            });

            const clock = new THREE.Clock();
            
            const animate = () => {
                if (!isAnimating3D) return;
                
                const elapsedTime = clock.getElapsedTime();
                
                particles.rotation.y = elapsedTime * 0.02;
                particles.rotation.x = elapsedTime * 0.01;
                
                camera.position.x = lerp(camera.position.x, mouse.x * 0.5, 0.05);
                camera.position.y = lerp(camera.position.y, mouse.y * 0.5, 0.05);
                camera.lookAt(scene.position);
                
                renderer.render(scene, camera);
                requestAnimationFrame(animate);
            };
            
            isAnimating3D = true;
            animate();

            document.addEventListener("visibilitychange", () => {
                isAnimating3D = !document.hidden;
                if (isAnimating3D) animate();
            });
        }

        // --- 4. Custom Cursor ---
        function initCursor() {
            if (prefersReducedMotion) return;

            const cursorDot = document.getElementById('cursor-dot');
            const cursorOutline = document.getElementById('cursor-outline');
            if (!cursorDot || !cursorOutline) return;
            const body = document.body;

            let dotX = 0, dotY = 0, outlineX = 0, outlineY = 0;

            window.addEventListener('mousemove', e => {
                dotX = e.clientX;
                dotY = e.clientY;
            });
            
            const animateCursor = () => {
                outlineX = lerp(outlineX, dotX, 0.1);
                outlineY = lerp(outlineY, dotY, 0.1);
                
                cursorDot.style.transform = `translate(${dotX}px, ${dotY}px)`;
                cursorOutline.style.transform = `translate(${outlineX}px, ${outlineY}px)`;
                
                requestAnimationFrame(animateCursor);
            };
            requestAnimationFrame(animateCursor);

            const hoverElements = document.querySelectorAll('a, button, [data-magnetic], [role="button"], .axiom-card');
            hoverElements.forEach(el => {
                el.addEventListener('mouseenter', () => body.classList.add('cursor-hover'));
                el.addEventListener('mouseleave', () => body.classList.remove('cursor-hover'));
            });
        }

        // --- 5. Magnetic Buttons ---
        function initMagneticButtons() {
            if (prefersReducedMotion) return;

            const strength = 0.4;
            document.querySelectorAll('[data-magnetic]').forEach(el => {
                el.addEventListener('mousemove', e => {
                    const rect = el.getBoundingClientRect();
                    const x = e.clientX - rect.left - rect.width / 2;
                    const y = e.clientY - rect.top - rect.height / 2;
                    
                    el.style.transition = 'transform 0.1s ease-out';
                    el.style.transform = `translate(${x * strength}px, ${y * strength}px)`;
                });
                el.addEventListener('mouseleave', () => {
                    el.style.transition = 'transform 0.3s cubic-bezier(0.23, 1, 0.32, 1)';
                    el.style.transform = 'translate(0,0)';
                });
            });
        }

        // --- 6. Scroll Features (Progress Bar, Nav Highlighting, Header Style) ---
        function initScrollFeatures() {
            const progressBar = document.getElementById('scroll-progress');
            const header = document.getElementById('header');
            const navLinks = document.querySelectorAll('.nav-link');
            const sections = document.querySelectorAll('div[data-section-id]');
            if (sections.length === 0) return;

            // Observer for nav link highlighting
            const sectionObserver = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting && entry.intersectionRatio > 0.4) {
                        const id = entry.target.getAttribute('data-section-id');
                        navLinks.forEach(link => {
                            link.classList.toggle('active', link.getAttribute('href') === `#${id}`);
                        });
                    }
                });
            }, {
                rootMargin: '-50% 0px -50% 0px',
                threshold: 0.4
            });
            sections.forEach(section => sectionObserver.observe(section));

            // Listener for progress bar and header style
            window.addEventListener('scroll', () => {
                const scrollY = window.scrollY;
                
                // 1. Progress Bar
                if (progressBar) {
                    const docHeight = document.documentElement.scrollHeight;
                    const viewHeight = window.innerHeight;
                    const progress = (scrollY / (docHeight - viewHeight)) * 100;
                    progressBar.style.width = `${progress}%`;
                }
                
                // 2. Header Style
                if (header) {
                    if (scrollY > 50) {
                        header.classList.add('light:bg-white/80', 'dark:bg-slate-900/80', 'backdrop-blur-md', 'shadow-md');
                    } else {
                        header.classList.remove('light:bg-white/80', 'dark:bg-slate-900/80', 'backdrop-blur-md', 'shadow-md');
                    }
                }
            });
        }

        // --- 7. Staggered Reveals ---
        function initStaggeredReveals() {
            if (prefersReducedMotion) {
                document.querySelectorAll('[data-stagger-reveal]').forEach(el => el.classList.add('is-revealed'));
                return;
            }

            const revealContainers = document.querySelectorAll('[data-stagger-container]');
            revealContainers.forEach(container => {
                const items = container.querySelectorAll('[data-stagger-reveal]');
                const observer = new IntersectionObserver((entries, obs) => {
                    entries.forEach(entry => {
                        if (entry.isIntersecting) {
                            items.forEach((item, index) => {
                                setTimeout(() => {
                                    item.classList.add('is-revealed');
                                }, index * 100); // Faster stagger
                            });
                            obs.unobserve(container);
                        }
                    });
                }, { threshold: 0.1 });
                observer.observe(container);
            });

            const looseItems = document.querySelectorAll('[data-stagger-reveal]:not([data-stagger-container] [data-stagger-reveal])');
            looseItems.forEach(item => {
                const observer = new IntersectionObserver((entries, obs) => {
                    entries.forEach(entry => {
                        if(entry.isIntersecting) {
                            item.classList.add('is-revealed');
                            obs.unobserve(item);
                        }
                    });
                }, { threshold: 0.1 });
                observer.observe(item);
            });
        }

        // --- 8. Command Palette ---
        function initCommandPalette() {
            const palette = document.getElementById('command-palette');
            const overlay = document.getElementById('command-palette-overlay');
            const input = document.getElementById('command-palette-input');
            const list = document.getElementById('command-palette-list');
            if (!palette || !overlay || !input || !list) return;
            const items = list.querySelectorAll('.command-item');
            let selectedIndex = 0;

            const openPalette = () => {
                palette.classList.add('visible');
                overlay.classList.add('visible');
                input.value = '';
                filterItems('');
                input.focus();
            };

            const closePalette = () => {
                palette.classList.remove('visible');
                overlay.classList.remove('visible');
                input.blur();
            };

            const filterItems = (query) => {
                query = query.toLowerCase();
                selectedIndex = 0;
                items.forEach((item) => {
                    const text = item.textContent.toLowerCase();
                    const isVisible = text.includes(query);
                    item.style.display = isVisible ? 'flex' : 'none';
                });
                updateSelection();
            };
            
            const updateSelection = () => {
                items.forEach(item => item.classList.remove('selected'));
                const visibleItems = Array.from(items).filter(item => item.style.display !== 'none');
                if (visibleItems.length > 0) {
                    selectedIndex = Math.max(0, Math.min(selectedIndex, visibleItems.length - 1));
                    visibleItems[selectedIndex].classList.add('selected');
                    visibleItems[selectedIndex].scrollIntoView({ block: 'nearest' });
                }
            };

            const executeSelection = () => {
                const visibleItems = Array.from(items).filter(item => item.style.display !== 'none');
                if (visibleItems.length > 0 && visibleItems[selectedIndex]) {
                    visibleItems[selectedIndex].click();
                }
            };
            
            window.addEventListener('keydown', e => {
                if ((e.metaKey || e.ctrlKey) && e.key === 'k') {
                    e.preventDefault();
                    palette.classList.contains('visible') ? closePalette() : openPalette();
                }
                if (e.key === 'Escape' && palette.classList.contains('visible')) {
                    closePalette();
                }
            });

            input.addEventListener('input', () => filterItems(input.value));
            input.addEventListener('keydown', e => {
                const visibleItems = Array.from(items).filter(item => item.style.display !== 'none');
                if (e.key === 'ArrowDown') {
                    e.preventDefault();
                    selectedIndex = (visibleItems.length > 0) ? (selectedIndex + 1) % visibleItems.length : 0;
                    updateSelection();
                } else if (e.key === 'ArrowUp') {
                    e.preventDefault();
                    selectedIndex = (visibleItems.length > 0) ? (selectedIndex - 1 + visibleItems.length) % visibleItems.length : 0;
                    updateSelection();
                } else if (e.key === 'Enter') {
                    e.preventDefault();
                    executeSelection();
                }
            });
            
            overlay.addEventListener('click', closePalette);
            items.forEach(item => {
                item.addEventListener('click', e => {
                    e.preventDefault();
                    const targetId = item.getAttribute('href');
                    const targetElement = document.querySelector(targetId);
                    if (targetElement) {
                        targetElement.scrollIntoView({ behavior: 'smooth' });
                    }
                    closePalette();
                });
            });
        }

        // --- 9. "Copy to Clipboard" (Kept, though not used in doc) ---
        function initClipboard() {
            document.querySelectorAll('[data-clipboard-text]').forEach(item => {
                const feedbackEl = item.querySelector('.copy-feedback');
                
                const action = () => {
                    const text = item.getAttribute('data-clipboard-text');
                    
                    try {
                        const textArea = document.createElement('textarea');
                        textArea.value = text;
                        textArea.style.position = 'fixed';
                        textArea.style.opacity = 0;
                        document.body.appendChild(textArea);
                        textArea.focus();
                        textArea.select();
                        document.execCommand('copy');
                        document.body.removeChild(textArea);

                        if (feedbackEl) {
                            feedbackEl.style.opacity = '1';
                            setTimeout(() => {
                                feedbackEl.style.opacity = '0';
                            }, 2000);
                        }
                    } catch (err) {
                        console.error('Failed to copy text: ', err);
                    }
                };

                item.addEventListener('click', action);
                item.addEventListener('keydown', (e) => {
                    if (e.key === 'Enter' || e.key === ' ') {
                        e.preventDefault();
                        action();
                    }
                });
            });
        }

        // --- 10. COPYRIGHT YEAR ---
        function initCopyright() {
            const yearEl = document.getElementById('copyright-year');
            if(yearEl) {
                yearEl.textContent = new Date().getFullYear();
            }
        }
        
        <!-- --- 11. KaTeX Auto-Render --- -->
        function initKatex() {
            if (typeof renderMathInElement !== 'undefined') {
                renderMathInElement(document.body, {
                    delimiters: [
                        {left: '$$', right: '$$', display: true},
                        {left: '$', right: '$', display: false},
                        {left: '\\(', right: '\\)', display: false},
                        {left: '\\[', right: '\\]', display: true}
                    ],
                    throwOnError : false
                });
            } else {
                console.warn("KaTeX auto-render script not loaded. Math will not be rendered.");
            }
        }

        // --- RUN ALL INITIALIZERS ---
        window.onload = () => {
            try {
                lucide.createIcons();
            } catch (e) {
                console.error("Lucide icons failed to create.", e);
            }
            
            // Run KaTeX renderer
            try {
                initKatex();
            } catch (e) {
                console.error("KaTeX failed to render.", e);
            }
            
            initTheme();
            initMobileMenu();
            initThreeJS();
            initCursor();
            initMagneticButtons();
            initScrollFeatures();
            initStaggeredReveals();
            initCommandPalette();
            initClipboard();
            initCopyright();
        };
    </script>
</body>
</html>
