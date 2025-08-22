# Music-app
<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MusicHub - Spotify जैसा संगीत अनुभव</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #121212;
            color: #ffffff;
            display: flex;
            height: 100vh;
        }

        .sidebar {
            width: 230px;
            background-color: #000000;
            padding: 20px;
            overflow-y: auto;
        }

        .logo {
            margin-bottom: 30px;
        }

        .logo h1 {
            color: #1DB954;
            font-size: 24px;
        }

        .menu-item {
            padding: 12px 0;
            color: #b3b3b3;
            font-weight: 600;
            cursor: pointer;
            transition: color 0.3s;
        }

        .menu-item:hover {
            color: #ffffff;
        }

        .menu-item i {
            margin-right: 15px;
            font-size: 20px;
        }

        .main-content {
            flex: 1;
            display: flex;
            flex-direction: column;
            overflow-y: auto;
        }

        .topbar {
            background-color: rgba(18, 18, 18, 0.8);
            padding: 16px 32px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            backdrop-filter: blur(10px);
        }

        .search-bar {
            background: #ffffff;
            border-radius: 50px;
            padding: 8px 15px;
            width: 300px;
            display: flex;
            align-items: center;
        }

        .search-bar input {
            background: transparent;
            border: none;
            outline: none;
            width: 100%;
            margin-left: 10px;
            font-size: 14px;
        }

        .user-profile {
            display: flex;
            align-items: center;
            background: rgba(0, 0, 0, 0.7);
            padding: 5px 10px 5px 5px;
            border-radius: 50px;
            cursor: pointer;
        }

        .user-profile img {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            margin-right: 8px;
        }

        .playlists {
            padding: 20px 32px;
            flex: 1;
            overflow-y: auto;
        }

        .section-title {
            font-size: 24px;
            font-weight: 700;
            margin-bottom: 20px;
        }

        .playlist-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
            gap: 20px;
        }

        .playlist-card {
            background: #181818;
            padding: 16px;
            border-radius: 6px;
            transition: background 0.3s;
            cursor: pointer;
        }

        .playlist-card:hover {
            background: #282828;
        }

        .playlist-img {
            width: 100%;
            aspect-ratio: 1;
            border-radius: 5px;
            margin-bottom: 16px;
            background-color: #333;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .playlist-title {
            font-weight: 600;
            margin-bottom: 8px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .playlist-desc {
            color: #b3b3b3;
            font-size: 14px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .player-controls {
            background: #181818;
            border-top: 1px solid #282828;
            padding: 16px 32px;
            display: flex;
            flex-direction: column;
        }

        .now-playing {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }

        .track-info {
            display: flex;
            align-items: center;
            width: 30%;
        }

        .track-img {
            width: 60px;
            height: 60px;
            border-radius: 5px;
            margin-right: 15px;
            background-color: #333;
        }

        .track-details {
            width: calc(100% - 75px);
        }

        .track-name {
            font-weight: 600;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .artist-name {
            color: #b3b3b3;
            font-size: 14px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .controls {
            display: flex;
            flex-direction: column;
            align-items: center;
            width: 40%;
        }

        .control-buttons {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
        }

        .control-button {
            color: #b3b3b3;
            margin: 0 10px;
            cursor: pointer;
            transition: color 0.3s;
            font-size: 18px;
        }

        .control-button:hover {
            color: #ffffff;
        }

        .control-button.play-pause {
            color: #ffffff;
            font-size: 32px;
        }

        .progress-bar {
            width: 100%;
            display: flex;
            align-items: center;
        }

        .progress-time {
            color: #b3b3b3;
            font-size: 12px;
            margin: 0 10px;
        }

        .progress {
            flex: 1;
            height: 4px;
            background: #535353;
            border-radius: 2px;
            position: relative;
            cursor: pointer;
        }

        .progress-filled {
            background: #b3b3b3;
            width: 30%;
            height: 100%;
            border-radius: 2px;
        }

        .volume-controls {
            display: flex;
            align-items: center;
            width: 30%;
            justify-content: flex-end;
        }

        .volume-button {
            color: #b3b3b3;
            margin-right: 10px;
            cursor: pointer;
        }

        .volume-bar {
            width: 100px;
            height: 4px;
            background: #535353;
            border-radius: 2px;
            position: relative;
            cursor: pointer;
        }

        .volume-filled {
            background: #b3b3b3;
            width: 70%;
            height: 100%;
            border-radius: 2px;
        }

        @media (max-width: 768px) {
            .sidebar {
                width: 80px;
            }
            .menu-item span {
                display: none;
            }
            .search-bar {
                width: 150px;
            }
        }
    </style>
</head>
<body>
    <!-- साइडबार -->
    <div class="sidebar">
        <div class="logo">
            <h1>MusicHub</h1>
        </div>
        <div class="menu-item">
            <i class="fas fa-home"></i>
            <span>होम</span>
        </div>
        <div class="menu-item">
            <i class="fas fa-search"></i>
            <span>खोज</span>
        </div>
        <div class="menu-item">
            <i class="fas fa-book"></i>
            <span>आपकी लाइब्रेरी</span>
        </div>
        <div class="menu-item" style="margin-top: 30px;">
            <i class="fas fa-plus-square"></i>
            <span>प्लेलिस्ट बनाएं</span>
        </div>
        <div class="menu-item">
            <i class="fas fa-heart"></i>
            <span>लाइक्ड सोंग्स</span>
        </div>
    </div>

    <!-- मुख्य सामग्री -->
    <div class="main-content">
        <div class="topbar">
            <div class="search-bar">
                <i class="fas fa-search" style="color: #121212;"></i>
                <input type="text" placeholder="क्या सुनना चाहते हैं?">
            </div>
            <div class="user-profile">
                <img src="https://randomuser.me/api/portraits/men/75.jpg" alt="User">
                <span>राहुल</span>
            </div>
        </div>

        <div class="playlists">
            <h2 class="section-title">आपके लिए</h2>
            <div class="playlist-grid">
                <div class="playlist-card">
                    <div class="playlist-img">
                        <i class="fas fa-music" style="font-size: 40px; color: #b3b3b3;"></i>
                    </div>
                    <div class="playlist-title">बॉलीवुड हिट्स</div>
                    <div class="playlist-desc">आज के टॉप बॉलीवुड गाने</div>
                </div>
                <div class="playlist-card">
                    <div class="playlist-img">
                        <i class="fas fa-music" style="font-size: 40px; color: #b3b3b3;"></i>
                    </div>
                    <div class="playlist-title">पंजाबी भांगड़ा</div>
                    <div class="playlist-desc">बेस्ट पंजाबी ट्रैक्स</div>
                </div>
                <div class="playlist-card">
                    <div class="playlist-img">
                        <i class="fas fa-music" style="font-size: 40px; color: #b3b3b3;"></i>
                    </div>
                    <div class="playlist-title">देवotional</div>
                    <div class="playlist-desc">भक्ति संगीत संग्रह</div>
                </div>
                <div class="playlist-card">
                    <div class="playlist-img">
                        <i class="fas fa-music" style="font-size: 40px; color: #b3b3b3;"></i>
                    </div>
                    <div class="playlist-title">रोमांटिक गाने</div>
                    <div class="playlist-desc">प्यार भरे गाने</div>
                </div>
                <div class="playlist-card">
                    <div class="playlist-img">
                        <i class="fas fa-music" style="font-size: 40px; color: #b3b3b3;"></i>
                    </div>
                    <div class="playlist-title">वर्कआउट मिक्स</div>
                    <div class="playlist-desc">एनर्जेटिक बीट्स</div>
                </div>
                <div class="playlist-card">
                    <div class="playlist-img">
                        <i class="fas fa-music" style="font-size: 40px; color: #b3b3b3;"></i>
                    </div>
                    <div class="playlist-title">शांति मंत्र</div>
                    <div class="playlist-desc">ध्यान के लिए संगीत</div>
                </div>
            </div>

            <h2 class="section-title" style="margin-top: 40px;">हाल ही में सुने</h2>
            <div class="playlist-grid">
                <div class="playlist-card">
                    <div class="playlist-img">
                        <i class="fas fa-music" style="font-size: 40px; color: #b3b3b3;"></i>
                    </div>
                    <div class="playlist-title">Kesariya</div>
                    <div class="playlist-desc">Arijit Singh</div>
                </div>
                <div class="playlist-card">
                    <div class="playlist-img">
                        <i class="fas fa-music" style="font-size: 40px; color: #b3b3b3;"></i>
                    </div>
                    <div class="playlist-title">Nach Meri Rani</div>
                    <div class="playlist-desc">Guru Randhawa</div>
                </div>
                <div class="playlist-card">
                    <div class="playlist-img">
                        <i class="fas fa-music" style="font-size: 40px; color: #b3b3b3;"></i>
                    </div>
                    <div class="playlist-title">Manike Mage Hithe</div>
                    <div class="playlist-desc">Yohani</div>
                </div>
                <div class="playlist-card">
                    <div class="playlist-img">
                        <i class="fas fa-music" style="font-size: 40px; color: #b3b3b3;"></i>
                    </div>
                    <div class="playlist-title">Raatan Lambiyan</div>
                    <div class="playlist-desc">Tanishk Bagchi</div>
                </div>
            </div>
        </div>
    </div>

    <!-- प्लेयर कंट्रोल्स -->
    <div class="player-controls">
        <div class="now-playing">
            <div class="track-info">
                <div class="track-img">
                    <i class="fas fa-music" style="font-size: 25px; color: #b3b3b3; display: flex; justify-content: center; align-items: center; height: 100%;"></i>
                </div>
                <div class="track-details">
                    <div class="track-name">Kesariya</div>
                    <div class="artist-name">Arijit Singh</div>
                </div>
            </div>
            <div class="controls">
                <div class="control-buttons">
                    <i class="fas fa-random control-button"></i>
                    <i class="fas fa-step-backward control-button"></i>
                    <i class="fas fa-play-circle control-button play-pause"></i>
                    <i class="fas fa-step-forward control-button"></i>
                    <i class="fas fa-repeat control-button"></i>
                </div>
                <div class="progress-bar">
                    <div class="progress-time">1:45</div>
                    <div class="progress">
                        <div class="progress-filled"></div>
                    </div>
                    <div class="progress-time">3:30</div>
                </div>
            </div>
            <div class="volume-controls">
                <i class="fas fa-volume-up volume-button"></i>
                <div class="volume-bar">
                    <div class="volume-filled"></div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // बेसिक प्लेयर फंक्शनलिटी
        const playPauseButton = document.querySelector('.play-pause');
        let isPlaying = true;

        playPauseButton.addEventListener('click', function() {
            if (isPlaying) {
                this.classList.remove('fa-pause-circle');
                this.classList.add('fa-play-circle');
            } else {
                this.classList.remove('fa-play-circle');
                this.classList.add('fa-pause-circle');
            }
            isPlaying = !isPlaying;
        });

        // प्रोग्रेस बार क्लिक करने का functionality
        const progressBar = document.querySelector('.progress');
        const progressFilled = document.querySelector('.progress-filled');
        
        progressBar.addEventListener('click', function(e) {
            const width = this.clientWidth;
            const clickX = e.offsetX;
            const progress = (clickX / width) * 100;
            progressFilled.style.width = progress + '%';
        });

        // वॉल्यूम बार क्लिक करने का functionality
        const volumeBar = document.querySelector('.volume-bar');
        const volumeFilled = document.querySelector('.volume-filled');
        
        volumeBar.addEventListener('click', function(e) {
            const width = this.clientWidth;
            const clickX = e.offsetX;
            const volume = (clickX / width) * 100;
            volumeFilled.style.width = volume + '%';
        });
    </script>
</body>
</html>
