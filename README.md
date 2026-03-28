<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Zentrix Premium - Professional Hub</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    
    <style>
        :root {
            --bg: #0b0e14;
            --card: #1a1d26;
            --primary: #2563eb;
            --primary-dark: #1e40af;
            --accent: #f59e0b;
            --success: #10b981;
            --text: #ffffff;
            --text-dim: #9ca3af;
        }

        body { margin: 0; font-family: 'Poppins', sans-serif; background-color: var(--bg); color: var(--text); overflow-x: hidden; }

        /* MODERN LOGO ANIMATION */
        .zentrix-logo-container { display: flex; align-items: center; justify-content: center; margin-bottom: 30px; }
        .logo-ring { position: relative; width: 90px; height: 90px; border-radius: 50%; border: 4px solid var(--primary); display: flex; align-items: center; justify-content: center; box-shadow: 0 0 20px rgba(37, 99, 235, 0.3); animation: glow 2s infinite alternate; }
        .logo-inner-z { font-size: 50px; font-weight: 700; color: white; }
        
        @keyframes glow {
            from { transform: scale(1); box-shadow: 0 0 10px rgba(37, 99, 235, 0.3); }
            to { transform: scale(1.05); box-shadow: 0 0 30px rgba(37, 99, 235, 0.6); }
        }

        /* HEADER & NAVIGATION */
        header { padding: 15px 20px; display: flex; justify-content: space-between; align-items: center; background: var(--card); position: sticky; top: 0; z-index: 900; border-bottom: 1px solid rgba(255,255,255,0.1); }
        .lang-switch { background: var(--primary); color: white; border: none; padding: 6px 12px; border-radius: 20px; font-size: 11px; cursor: pointer; font-weight: 600; }

        /* SIDEBAR SYSTEM */
        .sidebar { position: fixed; left: -280px; top: 0; width: 280px; height: 100%; background: var(--card); transition: 0.4s cubic-bezier(0.4, 0, 0.2, 1); z-index: 1001; padding: 25px 20px; box-shadow: 10px 0 30px rgba(0,0,0,0.8); border-right: 2px solid var(--primary); box-sizing: border-box; }
        .sidebar.open { left: 0; }
        .sidebar-item { padding: 15px; border-bottom: 1px solid rgba(255,255,255,0.05); cursor: pointer; display: flex; align-items: center; gap: 12px; font-size: 14px; border-radius: 10px; margin-bottom: 5px; }
        .sidebar-item:hover { background: rgba(37, 99, 235, 0.1); color: var(--primary); }

        /* OVERLAY - FIXED SHADOW ISSUE */
        .overlay { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.7); z-index: 1000; backdrop-filter: blur(3px); }
        .overlay.active { display: block; }

        /* CONTENT CARDS */
        .section { display: none; padding: 20px; animation: fadeIn 0.5s ease; max-width: 600px; margin: 0 auto; }
        .active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .card { background: var(--card); border-radius: 24px; padding: 18px; margin-bottom: 25px; border: 1px solid rgba(255,255,255,0.05); box-shadow: 0 10px 25px rgba(0,0,0,0.3); }
        .video-box { position: relative; width: 100%; padding-bottom: 56.25%; height: 0; margin-bottom: 15px; border-radius: 18px; overflow: hidden; background: #000; }
        .video-box iframe { position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none; }

        /* SOCIAL BAR */
        .social-bar { display: flex; justify-content: space-around; padding: 12px 0; border-top: 1px solid rgba(255,255,255,0.05); margin-top: 10px; }
        .social-item { cursor: pointer; font-size: 13px; color: var(--text-dim); display: flex; align-items: center; gap: 6px; }
        .social-item.active-like { color: #ef4444; }

        /* BUTTONS & INPUTS */
        .input-box { width: 100%; padding: 16px; border-radius: 15px; border: 1px solid rgba(255,255,255,0.1); background: rgba(0,0,0,0.2); color: white; margin-bottom: 15px; box-sizing: border-box; }
        .btn { width: 100%; padding: 16px; border-radius: 15px; border: none; font-weight: 600; cursor: pointer; display: flex; justify-content: center; align-items: center; gap: 10px; }
        .btn-primary { background: linear-gradient(135deg, var(--primary), var(--primary-dark)); color: white; }
        .btn-wa { background: #25d366; color: white; margin-top: 10px; text-decoration: none; }

        /* ADMIN ELEMENTS */
        #adminBar { display: none; background: var(--accent); color: black; padding: 8px; text-align: center; font-size: 11px; font-weight: bold; }
    </style>
</head>
<body>

    <div id="adminBar">ADMIN ACTIVE: Use Code <span style="text-decoration:underline">ZENTRIX2026</span></div>
    <div id="overlay" class="overlay" onclick="toggleSidebar()"></div>

    <div id="sidebar" class="sidebar">
        <div style="text-align:center; margin-bottom: 30px;">
            <h2 style="color:var(--accent); margin:0">Zentrix<span style="color:white">App</span></h2>
        </div>
        <div class="sidebar-item" onclick="show('home')"><i class="fas fa-home"></i> <span class="tr" data-en="Feed" data-sw="Masomo">Feed</span></div>
        <div id="adminPostLink" class="sidebar-item" style="display:none;" onclick="show('admin_panel')"><i class="fas fa-plus-circle"></i> <span class="tr" data-en="Admin: Post" data-sw="Admin: Weka Somo">Admin: Post</span></div>
        <div class="sidebar-item" onclick="openWA()"><i class="fab fa-whatsapp"></i> WhatsApp Admin</div>
        <div class="sidebar-item" onclick="location.reload()" style="color:#ef4444; margin-top:40px;"><i class="fas fa-power-off"></i> Logout</div>
    </div>

    <header id="mainHeader" style="display:none;">
        <i class="fas fa-bars" onclick="toggleSidebar()" style="cursor:pointer; font-size:20px;"></i>
        <div style="font-weight:700">Zentrix<span style="color:var(--accent)">Premium</span></div>
        <button class="lang-switch" onclick="toggleLang()" id="lBtn">KISWAHILI</button>
    </header>

    <div id="auth" class="section active">
        <div style="text-align:center; padding-top: 50px;">
            <div class="zentrix-logo-container"><div class="logo-ring"><span class="logo-inner-z">Z</span></div></div>
            <h2 class="tr" data-en="Welcome Back" data-sw="Karibu Tena">Welcome Back</h2>
            <input type="text" id="u" class="input-box" placeholder="Username">
            <input type="password" id="p" class="input-box" placeholder="Password">
            <button class="btn btn-primary" onclick="login()">Login</button>
        </div>
    </div>

    <div id="verify" class="section">
        <div style="text-align:center;">
            <i class="fas fa-lock" style="font-size:50px; color:var(--accent); margin-bottom:20px;"></i>
            <h3 class="tr" data-en="Account Locked" data-sw="Akaunti Imefungwa">Account Locked</h3>
            <p class="tr" data-en="Get the 2026 Code from Ezra via WhatsApp." data-sw="Pata kodi ya 2026 kutoka kwa Ezra WhatsApp.">Get the code via WhatsApp.</p>
            <input type="text" id="code" class="input-box" style="text-align:center; font-size:22px" placeholder="CODE">
            <button class="btn btn-primary" onclick="checkCode()">Verify Now</button>
            <a href="#" onclick="openWA()" class="btn btn-wa"><i class="fab fa-whatsapp"></i> Chat with Ezra</a>
        </div>
    </div>

    <div id="home" class="section">
        <div id="feed">
            <div class="card">
                <div class="video-box"><iframe src="https://www.youtube.com/embed/dQw4w9WgXcQ" allowfullscreen></iframe></div>
                <h3>Welcome to the Future</h3>
                <p style="font-size:13px; color:var(--text-dim)">Start your professional journey in computer maintenance and graphics design today.</p>
                <div class="social-bar">
                    <div class="social-item" onclick="this.classList.toggle('active-like')"><i class="fas fa-heart"></i> Like</div>
                    <div class="social-item" onclick="alert('Comment box opening...')"><i class="fas fa-comment"></i> Comment</div>
                    <div class="social-item" onclick="openWA()"><i class="fas fa-share-alt"></i> Share</div>
                </div>
            </div>
        </div>
    </div>

    <div id="admin_panel" class="section">
        <div class="card" style="border: 2px dashed var(--primary)">
            <h3>Post New Lesson</h3>
            <input type="text" id="t" class="input-box" placeholder="Lesson Title">
            <textarea id="d" class="input-box" rows="3" placeholder="Description..."></textarea>
            <input type="text" id="v" class="input-box" placeholder="YouTube Embed Link">
            <button class="btn btn-primary" onclick="addPost()">Publish to Feed</button>
        </div>
    </div>

    <script>
        let lang = 'en';
        const wa = "255795191608";

        function toggleSidebar() {
            document.getElementById('sidebar').classList.toggle('open');
            document.getElementById('overlay').classList.toggle('active');
        }

        function toggleLang() {
            lang = (lang === 'en') ? 'sw' : 'en';
            document.querySelectorAll('.tr').forEach(e => e.innerText = e.getAttribute(`data-${lang}`));
            document.getElementById('lBtn').innerText = (lang === 'en') ? 'KISWAHILI' : 'ENGLISH';
        }

        function show(id) {
            document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            document.getElementById('sidebar').classList.remove('open');
            document.getElementById('overlay').classList.remove('active');
            document.getElementById('mainHeader').style.display = (id==='auth' || id==='verify') ? 'none' : 'flex';
        }

        function login() {
            let user = document.getElementById('u').value.toLowerCase();
            if(user === "admin") {
                document.getElementById('adminBar').style.display = 'block';
                document.getElementById('adminPostLink').style.display = 'flex';
                show('home');
            } else if(user !== "") { show('verify'); }
        }

        function checkCode() {
            if(document.getElementById('code').value === "ZENTRIX2026") { show('home'); }
            else { alert("Incorrect Code!"); }
        }

        function openWA() { window.open(`https://wa.me/${wa}?text=Habari Ezra, nahitaji msaada wa Zentrix App.`); }

        function addPost() {
            let title = document.getElementById('t').value;
            let desc = document.getElementById('d').value;
            let video = document.getElementById('v').value || "https://www.youtube.com/embed/dQw4w9WgXcQ";
            if(!title || !desc) return;
            let h = `<div class="card"><div class="video-box"><iframe src="${video}" allowfullscreen></iframe></div><h3>${title}</h3><p style="font-size:13px; color:var(--text-dim)">${desc}</p><div class="social-bar"><div class="social-item"><i class="fas fa-heart"></i> Like</div><div class="social-item"><i class="fas fa-comment"></i> Comment</div><div class="social-item"><i class="fas fa-share-alt"></i> Share</div></div></div>`;
            document.getElementById('feed').insertAdjacentHTML('afterbegin', h);
            show('home');
        }
    </script>
</body>
</html>
