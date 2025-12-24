<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Astola TV - Enchanting World of Live Streaming</title>
  <style>
    :root {
      --bg: #0a0a1f;
      --primary: #00ff9d;
      --secondary: #ff00aa;
      --text: #ffffff;
      --card: rgba(20, 20, 40, 0.7);
      --glow: 0 0 20px rgba(0, 255, 157, 0.6);
    }
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #0a0a1f, #001f3f);
      color: var(--text);
      height: 100vh;
      overflow: hidden;
      display: flex;
      flex-direction: column;
    }
    @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;800&display=swap');
    header {
      background: rgba(0, 0, 0, 0.5);
      backdrop-filter: blur(10px);
      padding: 15px;
      text-align: center;
      font-size: 2.5rem;
      font-weight: 800;
      letter-spacing: 4px;
      text-shadow: var(--glow);
      color: var(--primary);
      position: relative;
      z-index: 10;
    }
    #search-bar {
      position: absolute;
      top: 20px;
      right: 20px;
      padding: 12px 20px;
      width: 300px;
      border-radius: 30px;
      border: 2px solid var(--primary);
      background: rgba(0,0,0,0.4);
      color: white;
      font-size: 1rem;
      box-shadow: var(--glow);
      transition: 0.3s;
    }
    #search-bar:focus {
      outline: none;
      width: 350px;
      box-shadow: 0 0 30px rgba(0, 255, 157, 0.8);
    }
    #logo-container {
      height: 120px;
      display: flex;
      align-items: center;
      justify-content: center;
      position: relative;
      overflow: hidden;
      background: radial-gradient(circle, #001f3f, #0a0a1f);
    }
    #particles {
      position: absolute;
      width: 100%;
      height: 100%;
    }
    .container {
      display: flex;
      flex: 1;
      overflow: hidden;
    }
    #player-container {
      width: 360px;
      height: 260px;
      min-height: 260px;
      position: absolute;
      top: 160px;
      left: 20px;
      z-index: 10;
      background: #000;
      border-radius: 20px;
      box-shadow: 0 0 40px rgba(0, 255, 157, 0.8);
      display: flex;
      flex-direction: column;
      padding: 10px;
    }
    #video-player {
      width: 100%;
      height: calc(100% - 90px);
      border-radius: 15px;
      overflow: hidden;
    }
    #quality-controls {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 8px;
      margin: 8px 0;
    }
    .quality-btn {
      padding: 6px 12px;
      background: rgba(0, 255, 157, 0.2);
      border: 1px solid var(--primary);
      border-radius: 20px;
      color: white;
      cursor: pointer;
      font-size: 0.85rem;
      transition: 0.3s;
    }
    .quality-btn.active, .quality-btn:hover {
      background: var(--primary);
      color: #000;
      box-shadow: var(--glow);
    }
    #now-playing {
      margin-top: 4px;
      font-size: 1rem;
      font-weight: 600;
      text-shadow: var(--glow);
      color: var(--primary);
      text-align: center;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
    #channel-list {
      width: 100%;
      height: 100%;
      overflow-y: auto;
      padding: 20px 20px 20px 400px;
      box-sizing: border-box;
      background: var(--card);
      backdrop-filter: blur(10px);
    }
    .country-group {
      margin: 15px 0;
      border-radius: 15px;
      overflow: hidden;
      background: rgba(0,0,0,0.4);
      box-shadow: 0 4px 20px rgba(0,0,0,0.6);
    }
    .country-title {
      padding: 18px;
      background: linear-gradient(90deg, var(--primary), var(--secondary));
      font-weight: 700;
      color: #000;
      cursor: pointer;
      font-size: 1.3rem;
      text-align: center;
      text-transform: uppercase;
      letter-spacing: 1px;
    }
    .country-title::before {
      content: "▶ ";
      transition: 0.3s;
    }
    .country-group.collapsed .country-title::before {
      content: "▼ ";
    }
    .country-group.collapsed .channels {
      display: none;
    }
    .channel {
      display: flex;
      align-items: center;
      padding: 15px;
      cursor: pointer;
      transition: all 0.4s ease;
      border-bottom: 1px solid rgba(255,255,255,0.1);
    }
    .channel:hover {
      background: rgba(0, 255, 157, 0.2);
      transform: translateX(10px);
      box-shadow: var(--glow);
    }
    .channel.active {
      background: linear-gradient(90deg, var(--primary), transparent);
      box-shadow: var(--glow);
    }
    .channel img {
      width: 60px;
      height: 60px;
      border-radius: 12px;
      margin-right: 15px;
      object-fit: cover;
      box-shadow: 0 0 15px rgba(0,0,0,0.7);
      background: #000;
    }
    .channel-name {
      flex: 1;
      font-size: 1.1rem;
      font-weight: 500;
    }
    #loading-message {
      position: absolute;
      color: var(--primary);
      font-size: 1.5rem;
      text-shadow: var(--glow);
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      z-index: 5;
    }

    @media (max-width: 900px) {
      #player-container {
        position: static;
        width: 100%;
        height: 300px;
        border-radius: 0 0 20px 20px;
        box-shadow: 0 10px 30px rgba(0, 255, 157, 0.5);
      }
      #video-player {
        height: calc(100% - 100px);
      }
      #quality-controls {
        gap: 10px;
      }
      .quality-btn {
        padding: 8px 14px;
        font-size: 0.95rem;
      }
      #channel-list {
        padding: 20px;
      }
      #search-bar {
        position: static;
        width: 90%;
        margin: 10px auto;
        display: block;
      }
      header {
        font-size: 2rem;
      }
      #logo-container {
        height: 100px;
      }
      #now-playing {
        font-size: 1.2rem;
      }
    }
  </style>
  <script src="https://vjs.zencdn.net/8.10.0/video.min.js"></script>
  <link href="https://vjs.zencdn.net/8.10.0/video-js.css" rel="stylesheet" />
  <script src="https://cdn.jsdelivr.net/npm/particles.js@2.0.0/particles.min.js"></script>
</head>
<body>
  <header>Astola TV</header>
  <input type="text" id="search-bar" placeholder="🔍 Search channels or countries..." />
  <div id="logo-container">
    <div id="particles"></div>
  </div>

  <div class="container">
    <div id="player-container">
      <video id="video-player" class="video-js vjs-big-play-centered vjs-fluid" controls preload="auto">
        <p>Your browser does not support video.</p>
      </video>
      <div id="quality-controls">
        <button class="quality-btn active" data-quality="auto">Auto</button>
        <button class="quality-btn" data-quality="240">240p</button>
        <button class="quality-btn" data-quality="360">360p</button>
        <button class="quality-btn" data-quality="480">480p</button>
        <button class="quality-btn" data-quality="720">720p</button>
        <button class="quality-btn" data-quality="1080">1080p</button>
      </div>
      <div id="now-playing">Select a channel to begin your enchanting journey</div>
    </div>

    <div id="channel-list">
      <div id="loading-message">✨ Loading magical channels from around the world... ✨<br>(10-40 seconds)</div>
    </div>
  </div>

  <script>
    const countryPlaylists = {
      "India 🇮🇳": "https://iptv-org.github.io/iptv/countries/in.m3u",
      "Pakistan 🇵🇰": "https://iptv-org.github.io/iptv/countries/pk.m3u",
      "United Kingdom 🇬🇧": "https://iptv-org.github.io/iptv/countries/gb.m3u",
      "United States 🇺🇸": "https://iptv-org.github.io/iptv/countries/us.m3u",
      "Bangladesh 🇧🇩": "https://iptv-org.github.io/iptv/countries/bd.m3u",
      "Turkey 🇹🇷": "https://iptv-org.github.io/iptv/countries/tr.m3u",
      "Germany 🇩🇪": "https://iptv-org.github.io/iptv/countries/de.m3u",
      "France 🇫🇷": "https://iptv-org.github.io/iptv/countries/fr.m3u",
      "Italy 🇮🇹": "https://iptv-org.github.io/iptv/countries/it.m3u",
      "Spain 🇪🇸": "https://iptv-org.github.io/iptv/countries/es.m3u",
      "International 🌍": "https://iptv-org.github.io/iptv/countries/int.m3u"
    };

    const channelList = document.getElementById('channel-list');
    const loadingMessage = document.getElementById('loading-message');
    const searchBar = document.getElementById('search-bar');
    const videoPlayer = videojs('video-player', {
      fluid: true,
      responsive: true,
      playbackRates: [0.5, 1, 1.5, 2],
      controlBar: { fullscreenToggle: true }
    });
    const nowPlaying = document.getElementById('now-playing');
    const qualityButtons = document.querySelectorAll('.quality-btn');

    let allChannels = [];
    let currentUrl = '';
    let preferredQuality = 'auto'; // default Auto

    // Quality switch handler
    qualityButtons.forEach(btn => {
      btn.addEventListener('click', () => {
        qualityButtons.forEach(b => b.classList.remove('active'));
        btn.classList.add('active');
        preferredQuality = btn.dataset.quality;
        if (currentUrl) {
          const finalUrl = (preferredQuality === 'auto') ? currentUrl : applyQuality(currentUrl, preferredQuality);
          videoPlayer.src({ type: 'application/x-mpegURL', src: finalUrl });
          videoPlayer.play().catch(() => {});
        }
      });
    });

    function applyQuality(url, quality) {
      let modified = url;

      const qualityMap = {
        '240': ['240p', 'b400000', 'low', 'lq', 'sdlow'],
        '360': ['360p', 'b800000', 'b1000000', 'sd'],
        '480': ['480p', 'b1600000', 'b2000000'],
        '720': ['720p', 'b3000000', 'b4000000', 'hd'],
        '1080': ['1080p', 'b6000000', 'b8000000', 'fullhd', 'hq']
      };

      const targets = qualityMap[quality] || qualityMap['720'];

      if (quality === '240') {
        modified = modified.replace(/(_|\-|\/)(720|1080|hd|high|hq)(p|\.)/gi, '$1' + '240' + '$3');
        modified = modified.replace(/chunklist.*\.m3u8/, 'chunklist_b400000.m3u8');
      } else if (quality === '360') {
        modified = modified.replace(/(_|\-|\/)(720|1080|240|hd|hq)(p|\.)/gi, '$1' + '360' + '$3');
      } else if (quality === '480') {
        modified = modified.replace(/(_|\-|\/)(720|1080|360|240)(p|\.)/gi, '$1' + '480' + '$3');
      } else if (quality === '720') {
        modified = modified.replace(/(_|\-|\/)(240|360|480|1080|low)(p|\.)/gi, '$1' + '720' + '$3');
      } else if (quality === '1080') {
        modified = modified.replace(/(_|\-|\/)(240|360|480|720|sd|low)(p|\.)/gi, '$1' + '1080' + '$3');
      }

      modified = modified
        .replace(/\/hq\//g, '/lq/')
        .replace(/\/high\//g, '/low/')
        .replace(/\/hd\//g, '/sd/');

      return modified;
    }

    async function loadPlaylists() {
      for (const [countryName, url] of Object.entries(countryPlaylists)) {
        try {
          const response = await fetch(url + '?t=' + Date.now());
          if (response.ok) {
            const text = await response.text();
            parseCountryM3U(countryName, text);
          }
        } catch (e) {
          console.log('Failed to load:', countryName);
        }
      }

      if (allChannels.length === 0) {
        loadingMessage.innerHTML = '⚠️ No channels loaded. Please refresh the page.';
      } else {
        loadingMessage.style.display = 'none';
      }
      initSearch();
      initCollapsibleGroups();
    }

    function parseCountryM3U(countryName, data) {
      const lines = data.split('\n');

      const countryDiv = document.createElement('div');
      countryDiv.className = 'country-group';
      countryDiv.innerHTML = `<div class="country-title">${countryName}</div><div class="channels"></div>`;
      channelList.appendChild(countryDiv);

      for (let i = 0; i < lines.length; i++) {
        const line = lines[i].trim();
        if (line.startsWith('#EXTINF:')) {
          const info = line.substring(8);
          const nameMatch = info.match(/,(.*)$/);
          const logoMatch = info.match(/tvg-logo="([^"]+)"/) || info.match(/tvg-logo='([^']+)'/);

          let channelName = nameMatch ? nameMatch[1].trim() : 'Unknown Channel';
          channelName = channelName.replace(/\(Astola TV\)$/gi, '') + ' ✨ Astola TV';
          const logo = logoMatch ? logoMatch[1] : 'https://via.placeholder.com/60x60/000/00ff9d?text=TV';

          if (i + 1 < lines.length && lines[i + 1].trim() && !lines[i + 1].startsWith('#')) {
            let url = lines[i + 1].trim();

            const channelDiv = document.createElement('div');
            channelDiv.className = 'channel';
            channelDiv.innerHTML = `
              <img src="${logo}" alt="logo" onerror="this.src='https://via.placeholder.com/60x60/000/00ff9d?text=TV'">
              <div class="channel-name">${channelName}</div>
            `;
            channelDiv.onclick = () => {
              document.querySelectorAll('.channel').forEach(ch => ch.classList.remove('active'));
              channelDiv.classList.add('active');
              currentUrl = url;
              const finalUrl = (preferredQuality === 'auto') ? url : applyQuality(url, preferredQuality);
              videoPlayer.src({ type: 'application/x-mpegURL', src: finalUrl });
              videoPlayer.play().catch(() => {});
              nowPlaying.textContent = `✨ Now Playing: ${channelName}`;
            };
            countryDiv.querySelector('.channels').appendChild(channelDiv);

            allChannels.push({
              element: channelDiv,
              name: channelName.toLowerCase(),
              country: countryName.toLowerCase()
            });
          }
        }
      }
    }

    function initSearch() {
      searchBar.addEventListener('input', (e) => {
        const query = e.target.value.toLowerCase() || '';
        allChannels.forEach(ch => {
          const matches = ch.name.includes(query) || ch.country.includes(query);
          ch.element.style.display = matches ? 'flex' : 'none';
        });
      });
    }

    function initCollapsibleGroups() {
      channelList.addEventListener('click', (e) => {
        if (e.target.classList.contains('country-title')) {
          e.target.parentElement.classList.toggle('collapsed');
        }
      });
    }

    particlesJS('particles', {
      particles: {
        number: { value: 80 },
        color: { value: ['#00ff9d', '#ff00aa', '#ffffff'] },
        shape: { type: 'circle' },
        opacity: { value: 0.8, random: true },
        size: { value: 4, random: true },
        line_linked: { enable: true, distance: 150, color: '#00ff9d', opacity: 0.4, width: 1 },
        move: { enable: true, speed: 2, direction: 'none', random: false }
      },
      interactivity: {
        detect_on: 'canvas',
        events: { onhover: { enable: true, mode: 'repulse' } }
      },
      retina_detect: true
    });

    loadPlaylists();
  </script>
</body>
</html>
