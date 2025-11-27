<html lang="ru">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Fame List</title>
  <style>
    :root{
      --bg:#071017;
      --card:#0f1720;
      --muted:#98a0ab;
      --accent:#ffb86b;
      --glass: rgba(255,255,255,0.03);
    }

    /* Reset-ish */
    *{box-sizing:border-box}
    html,body{height:100%}
    body{margin:0;font-family:Inter,Segoe UI,Arial;background:linear-gradient(180deg,var(--bg),#03121a);color:#e6eef6;-webkit-font-smoothing:antialiased}
    .container{max-width:1100px;margin:0 auto;padding:20px}

    /* Header */
    .site-header{position:sticky;top:0;background:linear-gradient(180deg, rgba(2,6,23,0.6), rgba(2,6,23,0.3));backdrop-filter:blur(6px);border-bottom:1px solid rgba(255,255,255,0.02);z-index:10}
    .header-inner{display:flex;align-items:center;justify-content:space-between;padding:12px 0}
    .logo{font-weight:700;text-decoration:none;color:var(--accent);font-size:20px;cursor:pointer}
    .main-nav{display:flex;gap:16px}
    .main-nav a{color:var(--muted);text-decoration:none;cursor:pointer;white-space:nowrap}
    .main-nav a.active{color:var(--accent);font-weight:600}

    /* Hero */
    .hero{text-align:center;padding:28px 0}
    .hero h1{font-size:40px;margin:6px 0}
    .subtitle{color:var(--muted);margin-bottom:12px}

    /* Controls */
    .controls{display:flex;gap:10px;justify-content:center;flex-wrap:wrap;margin-bottom:6px}
    .controls input, .controls select{padding:10px 12px;border-radius:10px;border:1px solid rgba(255,255,255,0.04);background:var(--glass);color:inherit;min-width:180px}
    .btn{padding:10px 14px;border-radius:10px;border:0;background:var(--accent);color:#071017;cursor:pointer;font-weight:700;text-decoration:none;display:inline-block}

    /* Grid */
    .cards-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:16px;margin-top:18px}
    .card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(0,0,0,0.18));padding:14px;border-radius:12px;display:flex;gap:14px;align-items:flex-start;box-shadow:0 8px 20px rgba(2,6,23,0.6);border:1px solid rgba(255,255,255,0.03)}
    .card img{width:72px;height:72px;border-radius:50%;object-fit:cover;flex-shrink:0}
    .card-body{flex:1}
    .nick-row{display:flex;align-items:center;gap:8px;justify-content:space-between}
    .nick{margin:0;font-size:18px}
    .badge{padding:6px 8px;border-radius:999px;font-weight:700;font-size:12px;color:#071017}
    .badge.owner{background:gold}
    .badge.high{background:#ff8c00}
    .badge.medium{background:#1e90ff}
    .badge.low{background:gray;color:#fff}
    .badge.banned{background:crimson;color:#fff}
    .role{margin:6px 0;color:var(--accent);font-weight:600}
    .desc{margin:0;color:var(--muted);font-size:13px}
    .card a.link-profile{display:inline-block;margin-top:8px;text-decoration:none;color:var(--accent);font-weight:700;cursor:pointer}

    /* Profile page */
    .profile-card{background:var(--card);padding:18px;border-radius:12px}
    .profile-card .bigavatar{width:120px;height:120px;border-radius:50%;object-fit:cover;margin-right:18px}
    .profile-top{display:flex;gap:18px;align-items:center}
    .profile-meta{color:var(--muted);margin-top:6px}

    /* Apply form */
    .apply-form{max-width:700px;margin:0 auto;margin-top:12px;display:grid;gap:10px}
    .apply-form label{display:flex;flex-direction:column;color:var(--muted);font-size:14px}
    .apply-form input, .apply-form select, .apply-form textarea{padding:10px;border-radius:10px;border:1px solid rgba(255,255,255,0.04);background:var(--glass);color:inherit}
    .apply-form textarea{min-height:90px;resize:vertical}
    .format-info{background:rgba(255,255,255,0.03);padding:16px;border-radius:12px;margin-bottom:20px;border:1px solid rgba(255,255,255,0.05)}
    .format-info h3{color:var(--accent);margin-top:0}

    /* Footer */
    .site-footer{padding:18px 0;text-align:center;color:var(--muted);border-top:1px solid rgba(255,255,255,0.02);margin-top:36px}

    /* Страницы */
    .page{display:none;}
    .page.active{display:block;}

    /* Mobile */
    @media (max-width:720px){
      .profile-top{flex-direction:column;align-items:flex-start}
      .cards-grid{grid-template-columns:repeat(auto-fill,minmax(200px,1fr))}
      .hero h1{font-size:28px}
      .header-inner{flex-direction:column;gap:12px;text-align:center}
      .main-nav{gap:12px;justify-content:center}
      .controls{flex-direction:column;align-items:center}
      .controls input, .controls select{width:100%;max-width:300px}
      .btn{width:100%;max-width:300px;text-align:center}
    }

    @media (max-width:480px){
      .container{padding:12px}
      .hero{padding:20px 0}
      .hero h1{font-size:24px}
      .cards-grid{grid-template-columns:1fr;gap:12px}
      .card{flex-direction:column;text-align:center;align-items:center}
      .card img{margin-bottom:8px}
      .profile-top{flex-direction:column;text-align:center;align-items:center}
      .profile-card .bigavatar{margin-right:0;margin-bottom:12px}
    }

    .hint {
      color: var(--muted);
      font-style: italic;
      text-align: center;
      padding: 20px;
    }
  </style>
</head>
<body>
  <header class="site-header">
    <div class="container header-inner">
      <a class="logo" id="homeLink">?? Fame List</a>
      <nav class="main-nav">
        <a id="mainLink" class="active">Главная</a>
        <a id="profileLink">Профиль</a>
        <a id="applyLink">Подать заявку</a>
      </nav>
    </div>
  </header>

  <main class="container">
    <!-- Главная страница -->
    <div id="mainPage" class="page active">
      <section class="hero">
        <h1>Fame List</h1>
        <p class="subtitle">Список участников, отсортированный по старшинству</p>

        <div class="controls">
          <input id="search" placeholder="Поиск по нику или описанию..." aria-label="Поиск" />
          <select id="filterMedia" aria-label="Фильтр по медийке">
            <option value="all">Все медийки</option>
             <option value="owner">Разработчик</option>
            <option value="Высокая медийка">Высокая медийка</option>
            <option value="Средняя медийка">Средняя медийка</option>
            <option value="Малая медийка">Малая медийка</option>
            <option value="Бомж/скамер">Бомж/скамер</option>
          </select>

          <select id="filterRank" aria-label="Фильтр по рангу">
            <option value="all">Все ранги</option>
            <option value="owner">разработчик</option>
            <option value="high">Высокая</option>
            <option value="medium">Средняя</option>
            <option value="low">Малая</option>
            <option value="banned">Бомж/скамер</option>
          </select>

          <button id="resetBtn" class="btn">Сброс</button>
        </div>
      </section>

      <section>
        <div id="cards" class="cards-grid" aria-live="polite"></div>
      </section>
    </div>

    <!-- Страница профиля -->
    <div id="profilePage" class="page">
      <div id="profileCard" class="profile-card" aria-live="polite">
        <p class="hint">Зайдите на профиль через ссылку "Смотреть профиль" на главной или добавьте параметр ?user=Nick</p>
      </div>
    </div>

    <!-- Страница заявки -->
    <div id="applyPage" class="page">
      <section class="hero">
        <h1>Подать заявку</h1>
        <p class="subtitle">Заполните форму для добавления в Fame List</p>
      </section>

      <div class="format-info">
        <h3>Формат заявки</h3>
        <p>Для подачи заявки нажмите кнопку ниже - она откроет Telegram-бота, где нужно будет отправить информацию в следующем формате:</p>
        <p><strong>Ник:</strong> Ваш никнейм в телеграмм</p>
        <p><strong>Ссылка на профиль телеграмм:</strong> https://t.me/username</p>
        <p><strong>Медийность:</strong> Высокая/Средняя/Малая</p>
        <p><strong>Как пришёл в KM:</strong> Описание как вы появились в KM</p>
      </div>

      <div style="text-align: center; margin-top: 30px;">
        <a href="https://t.me/PsulistHelp_Bot" class="btn" target="_blank" style="padding: 12px 24px; font-size: 16px;">
          Подать заявку в бота
        </a>
      </div>
    </div>
  </main>

  <footer class="site-footer">
    <div class="container">
      <p>© <span id="year"></span> Fame List — @Psulist</p>
    </div>
  </footer>

  <script>
    // ======= Demo-данные (замени на свои) =======
    const people = [
     {
        nick: 'Прокурор Алекс',
        rank: 'owner',            // owner | high | medium | low | banned 
        rankName: 'Разработчик',
        media: 'Высокая медийка',
        since: '0000',
        profile: 'https://t.me/AlOsint',
        img: 'https://github.com/glitterinzem-star/test/raw/2751079d5f1d012bb6d06226949884906edd11fa/alex.jpg.jpeg',
        desc: 'разработчик сайта (0000 это эксклюзивный тест номер)'
      },
      {
        nick: 'Психология',
        rank: 'owner',           
        rankName: 'разработчик',
        media: 'Высокая медийка', // медиапопулярность
        since: '0000',
        profile: 'https://t.me/psixotatia',
        img: '',
        desc: 'разработчик сайта (0000 это эксклюзивный тест номер)'
      },
      {
        nick: 'NoName',
        rank: 'medium',
        rankName: 'Средняя',
        media: 'Малая медийка',
        since: '2025',
        profile: 'https://t.me/noname',
        img: 'assets/avatars/avatar1.png',
        desc: 'описание'
      },
      {
        nick: 'NoName',
        rank: 'medium',
        rankName: 'Средняя',
        media: 'Малая медийка',
        since: '2025',
        profile: 'https://t.me/noname',
        img: 'assets/avatars/avatar1.png',
        desc: 'описание'
      },
      {
        nick: 'ScammerGuy',
        rank: 'banned',
        rankName: 'Бомж/скамер',
        media: 'Бомж/скамер',
        since: '2025',
        profile: 'https://t.me/ScammerGuy',
        img: 'assets/avatars/avatar2.png',
        desc: 'Бан за мошенничество.'
      }
    ];

    // порядок старшинства — меньше = старше
    const rankOrder = { owner: 1, high: 2, medium: 3, low: 4, banned: 5 };

    // ======= Общие функции =======
    function sortPeople(arr) {
      return arr.slice().sort((a,b)=> {
        const r = (rankOrder[a.rank] || 99) - (rankOrder[b.rank] || 99);
        if (r !== 0) return r;
        // вторичный порядок — по году появления (раньше выше)
        return (a.since || '9999').localeCompare(b.since || '9999');
      });
    }

    // создать DOM-карту-карточку
    function createCard(person) {
      const art = document.createElement('article');
      art.className = 'card';
      art.dataset.rank = person.rank;
      art.dataset.media = person.media || '';
      art.innerHTML = `
        <img src="${person.img}" alt="${person.nick} avatar" onerror="this.src='assets/avatars/avatar1.png'">
        <div class="card-body">
          <div class="nick-row">
            <h3 class="nick">${person.nick}</h3>
            <span class="badge ${person.rank}">${person.rankName || person.rank}</span>
          </div>
          <p class="role">Медийка: <b>${person.media || person.rankName || '-'}</b></p>
          <p class="desc">${person.desc || ''}</p>
          <p class="profile-meta">В КМ с: <b>${person.since || '-'}</b></p>
          <a class="link-profile view-profile" data-user="${person.nick}">Смотреть профиль</a>
          &nbsp;·&nbsp;
          <a class="link-profile" href="${person.profile}" target="_blank" rel="noopener noreferrer">Профиль (внешний)</a>
        </div>
      `;
      return art;
    }

    // рендер главной сетки
    function renderMainGrid(containerId = 'cards', source = people) {
      const cont = document.getElementById(containerId);
      if (!cont) return;
      cont.innerHTML = '';
      const sorted = sortPeople(source);
      sorted.forEach(p => cont.appendChild(createCard(p)));
      
      // Добавляем обработчики для ссылок "Смотреть профиль"
      document.querySelectorAll('.view-profile').forEach(link => {
        link.addEventListener('click', function() {
          const user = this.getAttribute('data-user');
          showProfilePage(user);
        });
      });
    }

    // ======= Поиск и фильтры на главной =======
    function initFilters() {
      const search = document.getElementById('search');
      const filterMedia = document.getElementById('filterMedia');
      const filterRank = document.getElementById('filterRank');
      const resetBtn = document.getElementById('resetBtn');

      function apply() {
        const q = search ? search.value.trim().toLowerCase() : '';
        const fMedia = filterMedia ? filterMedia.value : 'all';
        const fRank = filterRank ? filterRank.value : 'all';

        const nodes = document.querySelectorAll('#cards .card');
        nodes.forEach(node => {
          const nick = node.querySelector('.nick').textContent.toLowerCase();
          const desc = node.querySelector('.desc').textContent.toLowerCase();
          const media = node.dataset.media || '';
          const rank = node.dataset.rank || '';

          const matchesQ = q === '' || nick.includes(q) || desc.includes(q);
          const matchesMedia = (fMedia === 'all') || media === fMedia;
          const matchesRank = (fRank === 'all') || rank === fRank;

          node.style.display = (matchesQ && matchesMedia && matchesRank) ? '' : 'none';
        });
      }

      if (search) search.addEventListener('input', apply);
      if (filterMedia) filterMedia.addEventListener('change', apply);
      if (filterRank) filterRank.addEventListener('change', apply);
      if (resetBtn) resetBtn.addEventListener('click', () => {
        if (search) search.value = '';
        if (filterMedia) filterMedia.value = 'all';
        if (filterRank) filterRank.value = 'all';
        renderMainGrid('cards');
      });
    }

    // ======= Профиль =======
    function showProfilePage(userNick = null) {
      // Переключаемся на страницу профиля
      switchPage('profilePage');
      
      const profileContainer = document.getElementById('profileCard');
      if (!profileContainer) return;
      
      let nick = userNick;
      
      // Если ник не передан, проверяем URL параметры
      if (!nick) {
        const params = new URLSearchParams(window.location.search);
        nick = params.get('user');
      }
      
      if (!nick) {
        profileContainer.innerHTML = `<p class="hint">Параметр user не указан. Откройте профиль через ссылку 'Смотреть профиль' на главной.</p>`;
        return;
      }
      
      const person = people.find(p => p.nick.toLowerCase() === nick.toLowerCase());
      if (!person) {
        profileContainer.innerHTML = `<p class="hint">Пользователь <strong>${escapeHtml(nick)}</strong> не найден.</p>`;
        return;
      }

      profileContainer.innerHTML = `
        <div class="profile-card">
          <div class="profile-top">
            <img class="bigavatar" src="${person.img}" alt="${person.nick}" onerror="this.src='assets/avatars/avatar1.png'">
            <div>
              <h2>${person.nick} <span class="badge ${person.rank}">${person.rankName || person.rank}</span></h2>
              <div class="profile-meta">
                <p>Медийка: <b>${person.media || '-'}</b></p>
                <p>В КМ с: <b>${person.since || '-'}</b></p>
                <p>Ссылка: <a href="${person.profile}" target="_blank" rel="noopener noreferrer">${person.profile}</a></p>
              </div>
            </div>
          </div>
          <hr style="margin:12px 0;border:0;border-top:1px solid rgba(255,255,255,0.03)">
          <p>${person.desc || '-'}</p>
        </div>
      `;
    }

    // ======= Навигация между страницами =======
    function switchPage(pageId) {
      // Скрываем все страницы
      document.querySelectorAll('.page').forEach(page => {
        page.classList.remove('active');
      });
      
      // Показываем нужную страницу
      document.getElementById(pageId).classList.add('active');
      
      // Обновляем активную ссылку в навигации
      document.querySelectorAll('.main-nav a').forEach(link => {
        link.classList.remove('active');
      });
      
      if (pageId === 'mainPage') {
        document.getElementById('mainLink').classList.add('active');
      } else if (pageId === 'profilePage') {
        document.getElementById('profileLink').classList.add('active');
      } else if (pageId === 'applyPage') {
        document.getElementById('applyLink').classList.add('active');
      }
    }

    // ======= Утилиты =======
    function escapeHtml(str){
      if (!str) return '';
      return String(str).replace(/[&<>"']/g, function(m){
        return ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[m]);
      });
    }

    // ======= Инициализация при загрузке =======
    document.addEventListener('DOMContentLoaded', () => {
      // футер года
      const y = new Date().getFullYear();
      document.getElementById('year').textContent = y;

      // Инициализация главной страницы
      if (document.getElementById('cards')) {
        renderMainGrid('cards');
        initFilters();
      }

      // Навигация
      document.getElementById('homeLink').addEventListener('click', () => switchPage('mainPage'));
      document.getElementById('mainLink').addEventListener('click', () => switchPage('mainPage'));
      document.getElementById('profileLink').addEventListener('click', () => showProfilePage());
      document.getElementById('applyLink').addEventListener('click', () => switchPage('applyPage'));

      // Проверяем URL при загрузке для открытия профиля
      const urlParams = new URLSearchParams(window.location.search);
      if (urlParams.has('user')) {
        showProfilePage(urlParams.get('user'));
      }
    });
  </script>
</body>
</html>
