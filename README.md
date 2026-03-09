# movies
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>🎬 ReelRush · movie showcase</title>
  <!-- Poppins font & fallback -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap" rel="stylesheet">
  <!-- Font Awesome 6 (free) icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background: linear-gradient(145deg, #0b0f1c 0%, #141b2b 100%);
      font-family: 'Poppins', system-ui, -apple-system, sans-serif;
      color: #f0f4fa;
      line-height: 1.5;
      min-height: 100vh;
      padding: 2rem 1.5rem;
    }

    .container {
      max-width: 1280px;
      margin: 0 auto;
    }

    /* header / navigation */
    .top-bar {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 3rem;
      gap: 1.5rem;
    }

    .logo {
      display: flex;
      align-items: center;
      gap: 0.6rem;
      font-weight: 700;
      font-size: 1.9rem;
      letter-spacing: -0.5px;
      background: linear-gradient(130deg, #ffb87c, #ff7eb6);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
    }

    .logo i {
      font-size: 2.2rem;
      background: none;
      color: #ff9f7c; /* warm accent */
    }

    .search-wrapper {
      display: flex;
      align-items: center;
      background: rgba(20, 30, 45, 0.7);
      backdrop-filter: blur(8px);
      border: 1px solid rgba(255, 165, 120, 0.2);
      border-radius: 3rem;
      padding: 0.3rem 0.3rem 0.3rem 1.5rem;
      box-shadow: 0 12px 30px -10px rgba(0, 0, 0, 0.5);
    }

    .search-wrapper i {
      color: #ffaa80;
      font-size: 1.1rem;
    }

    .search-wrapper input {
      background: transparent;
      border: none;
      padding: 0.7rem 0.8rem;
      font-size: 1rem;
      font-weight: 300;
      color: #f0f4fa;
      min-width: 210px;
      outline: none;
    }

    .search-wrapper input::placeholder {
      color: #a8b3cf;
      font-weight: 300;
      opacity: 0.8;
    }

    .search-wrapper button {
      background: linear-gradient(145deg, #ff9467, #ff6a9c);
      border: none;
      color: white;
      font-weight: 500;
      padding: 0.65rem 1.8rem;
      border-radius: 3rem;
      cursor: default;   /* static demo — just aesthetic */
      font-size: 0.95rem;
      letter-spacing: 0.3px;
      box-shadow: 0 6px 14px rgba(255, 110, 110, 0.3);
      transition: 0.2s ease;
    }

    .search-wrapper button:hover {
      opacity: 0.9;
      transform: scale(1.02);
    }

    /* filter chips */
    .filter-row {
      display: flex;
      flex-wrap: wrap;
      gap: 0.8rem 1.2rem;
      margin: 2rem 0 2.2rem 0;
      align-items: center;
    }

    .filter-label {
      font-weight: 300;
      font-size: 1rem;
      color: #b1c3e0;
      margin-right: 0.5rem;
    }

    .chip {
      background: rgba(25, 35, 55, 0.8);
      backdrop-filter: blur(4px);
      padding: 0.5rem 1.2rem;
      border-radius: 40px;
      font-size: 0.9rem;
      font-weight: 400;
      border: 1px solid rgba(255, 140, 120, 0.2);
      color: #d6e2ff;
      transition: all 0.2s;
      cursor: default;
      display: inline-flex;
      align-items: center;
      gap: 7px;
    }

    .chip i {
      color: #ffa67e;
      font-size: 0.8rem;
    }

    .chip.active {
      background: linear-gradient(120deg, #ff8656, #ff5f8e);
      border-color: transparent;
      color: white;
      font-weight: 500;
      box-shadow: 0 6px 14px rgba(255, 95, 120, 0.4);
    }

    .chip.active i {
      color: white;
    }

    /* main grid – movie cards */
    .movie-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(210px, 1fr));
      gap: 2rem 1.5rem;
      margin-top: 1rem;
    }

    .movie-card {
      background: #1e2639;
      background: linear-gradient(165deg, #1b2335, #131b2c);
      border-radius: 1.8rem;
      overflow: hidden;
      box-shadow: 0 25px 40px -15px #00000080;
      transition: transform 0.25s ease, box-shadow 0.3s;
      border: 1px solid rgba(255, 160, 140, 0.1);
      backdrop-filter: blur(2px);
      display: flex;
      flex-direction: column;
    }

    .movie-card:hover {
      transform: translateY(-9px);
      box-shadow: 0 32px 55px -8px #ff7b8150, 0 0 0 1px rgba(255, 150, 120, 0.3);
    }

    .poster {
      position: relative;
      aspect-ratio: 2 / 3;
      background: #2a3145;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .poster img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
      transition: opacity 0.2s;
    }

    /* badge (rating / imdb) */
    .badge {
      position: absolute;
      top: 12px;
      right: 12px;
      background: #0e141cdd;
      backdrop-filter: blur(4px);
      padding: 0.3rem 0.7rem;
      border-radius: 40px;
      font-size: 0.8rem;
      font-weight: 600;
      border: 1px solid #ffb37c;
      color: #ffdec5;
      display: flex;
      align-items: center;
      gap: 5px;
    }

    .badge i {
      color: #ffb241;
      font-size: 0.7rem;
    }

    .movie-info {
      padding: 1.2rem 1rem 1.2rem 1rem;
      display: flex;
      flex-direction: column;
      gap: 0.4rem;
    }

    .movie-title {
      font-weight: 700;
      font-size: 1.2rem;
      line-height: 1.3;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      color: #f6f2ff;
    }

    .meta-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 0.9rem;
      color: #b0c3e8;
    }

    .year {
      display: flex;
      align-items: center;
      gap: 5px;
    }

    .year i {
      font-size: 0.7rem;
      color: #ff9e78;
    }

    .genre {
      font-size: 0.8rem;
      background: rgba(255, 150, 130, 0.18);
      padding: 0.2rem 0.7rem;
      border-radius: 40px;
      border: 1px solid rgba(255, 150, 130, 0.3);
      color: #ffc9b5;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      max-width: 110px;
    }

    .description {
      font-size: 0.85rem;
      font-weight: 300;
      color: #b6c4ec;
      margin: 0.2rem 0 0.2rem;
      display: -webkit-box;
      -webkit-line-clamp: 2;
      -webkit-box-orient: vertical;
      overflow: hidden;
      line-height: 1.4;
    }

    .card-footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 0.4rem;
    }

    .rating-stars i {
      color: #ffb444;
      font-size: 0.75rem;
      letter-spacing: -1px;
    }

    .rating-stars span {
      margin-left: 4px;
      font-weight: 500;
      font-size: 0.8rem;
      color: #d4e0ff;
    }

    .watch-btn {
      background: none;
      border: 1px solid rgba(255, 140, 140, 0.4);
      color: #ffe2d0;
      border-radius: 30px;
      padding: 0.3rem 1rem;
      font-size: 0.75rem;
      font-weight: 500;
      transition: 0.15s;
      cursor: default;
    }

    .watch-btn i {
      font-size: 0.7rem;
      margin-right: 4px;
      color: #ff9f7c;
    }

    /* extra section – trending */
    .section-divider {
      display: flex;
      align-items: center;
      gap: 1rem;
      margin: 3.5rem 0 1.5rem 0;
    }

    .section-divider h2 {
      font-weight: 500;
      font-size: 1.7rem;
      background: linear-gradient(130deg, #ffc7a2, #ffa2c0);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
    }

    .section-divider i {
      font-size: 2rem;
      color: #ff9f8c;
    }

    .mini-list {
      display: flex;
      flex-wrap: wrap;
      gap: 1rem;
      margin-bottom: 2rem;
    }

    .trending-item {
      background: rgba(25, 34, 50, 0.8);
      backdrop-filter: blur(4px);
      padding: 0.7rem 1.5rem;
      border-radius: 60px;
      font-size: 1rem;
      border: 1px solid #ff9f7c40;
      display: flex;
      align-items: center;
      gap: 10px;
      box-shadow: 0 8px 18px -10px #000000;
    }

    .trending-item i {
      color: #ff9f7c;
    }

    /* footer */
    .footer-note {
      margin-top: 4rem;
      text-align: center;
      font-weight: 300;
      font-size: 0.9rem;
      color: #7d8bb0;
      border-top: 1px solid rgba(255, 160, 140, 0.15);
      padding-top: 2rem;
    }

    .footer-note a {
      color: #ffb998;
      text-decoration: none;
    }

    /* responsiveness */
    @media (max-width: 650px) {
      body { padding: 1.5rem 1rem; }
      .top-bar { flex-direction: column; align-items: stretch; }
      .search-wrapper { justify-content: space-between; }
      .search-wrapper input { min-width: 140px; }
    }
  </style>
</head>
<body>
<div class="container">
  <!-- header + search (decorative) -->
  <div class="top-bar">
    <div class="logo">
      <i class="fas fa-film"></i> 
      <span>reel<span style="font-weight:300;">RUSH</span></span>
    </div>
    <div class="search-wrapper">
      <i class="fas fa-search"></i>
      <input type="text" placeholder="Search movies... (demo)">
      <button><i class="fas fa-sliders-h" style="margin-right: 6px;"></i> Filter</button>
    </div>
  </div>

  <!-- filter chips (just static) -->
  <div class="filter-row">
    <span class="filter-label"><i class="fas fa-tags"></i> quick picks</span>
    <span class="chip active"><i class="fas fa-fire"></i> trending</span>
    <span class="chip"><i class="fas fa-clock"></i> coming soon</span>
    <span class="chip"><i class="fas fa-star"></i> top rated</span>
    <span class="chip"><i class="fas fa-mask"></i> action</span>
    <span class="chip"><i class="fas fa-robot"></i> sci‑fi</span>
    <span class="chip"><i class="fas fa-heart"></i> drama</span>
  </div>

  <!-- movie grid – cards with posters, ratings, description -->
  <div class="movie-grid">
    <!-- movie 1 : Dune 2 -->
    <div class="movie-card">
      <div class="poster">
        <img src="https://image.tmdb.org/t/p/w600_and_h900_bestv2/8b8R8l88Qje9dn9OE8GY05QPbYn.jpg" alt="Dune: Part Two poster">
        <div class="badge"><i class="fab fa-imdb"></i> 8.7</div>
      </div>
      <div class="movie-info">
        <div class="movie-title">Dune: Part Two</div>
        <div class="meta-row">
          <span class="year"><i class="far fa-calendar-alt"></i> 2024</span>
          <span class="genre">Sci‑Fi</span>
        </div>
        <div class="description">Paul Atreides unites with Chani and the Fremen while seeking revenge against the conspirators who destroyed his family.</div>
        <div class="card-footer">
          <div class="rating-stars"><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star-half-alt"></i><span>4.7</span></div>
          <div class="watch-btn"><i class="far fa-clock"></i> 2h 46m</div>
        </div>
      </div>
    </div>

    <!-- movie 2 : Poor Things -->
    <div class="movie-card">
      <div class="poster">
        <img src="https://image.tmdb.org/t/p/w600_and_h900_bestv2/kCGlIMHnOm8JPXq3rXM6c5wMxcT.jpg" alt="Poor Things">
        <div class="badge"><i class="fab fa-imdb"></i> 8.4</div>
      </div>
      <div class="movie-info">
        <div class="movie-title">Poor Things</div>
        <div class="meta-row">
          <span class="year"><i class="far fa-calendar-alt"></i> 2023</span>
          <span class="genre">Comedy</span>
        </div>
        <div class="description">The incredible tale about the fantastical evolution of Bella Baxter, a young woman brought back to life by an unorthodox scientist.</div>
        <div class="card-footer">
          <div class="rating-stars"><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><span>4.9</span></div>
          <div class="watch-btn"><i class="far fa-clock"></i> 2h 21m</div>
        </div>
      </div>
    </div>

    <!-- movie 3 : The Batman -->
    <div class="movie-card">
      <div class="poster">
        <img src="https://image.tmdb.org/t/p/w600_and_h900_bestv2/74xTEgt7R36Fpooo50r9T25onhq.jpg" alt="The Batman">
        <div class="badge"><i class="fab fa-imdb"></i> 8.1</div>
      </div>
      <div class="movie-info">
        <div class="movie-title">The Batman</div>
        <div class="meta-row">
          <span class="year"><i class="far fa-calendar-alt"></i> 2022</span>
          <span class="genre">Crime</span>
        </div>
        <div class="description">When a sadistic killer targets Gotham's elite, Batman embarks on a dark investigation that forces him to confront his family's legacy.</div>
        <div class="card-footer">
          <div class="rating-stars"><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star-half-alt"></i><span>4.5</span></div>
          <div class="watch-btn"><i class="far fa-clock"></i> 2h 56m</div>
        </div>
      </div>
    </div>

    <!-- movie 4 : Everything Everywhere All at Once -->
    <div class="movie-card">
      <div class="poster">
        <img src="https://image.tmdb.org/t/p/w600_and_h900_bestv2/w3LxiVYdWWRvEVdn5RYq6jIqkb1.jpg" alt="Everything Everywhere">
        <div class="badge"><i class="fab fa-imdb"></i> 8.9</div>
      </div>
      <div class="movie-info">
        <div class="movie-title">Everything Everywhere</div>
        <div class="meta-row">
          <span class="year"><i class="far fa-calendar-alt"></i> 2022</span>
          <span class="genre">Adventure</span>
        </div>
        <div class="description">An aging Chinese immigrant is swept up in an insane adventure, where she alone can save the multiverse by exploring other lives.</div>
        <div class="card-footer">
          <div class="rating-stars"><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><span>5.0</span></div>
          <div class="watch-btn"><i class="far fa-clock"></i> 2h 19m</div>
        </div>
      </div>
    </div>

    <!-- movie 5 : Spider-Verse -->
    <div class="movie-card">
      <div class="poster">
        <img src="https://image.tmdb.org/t/p/w600_and_h900_bestv2/bVqYqJxK3MmarkFacL6LZKv509e.jpg" alt="Across the Spider-Verse">
        <div class="badge"><i class="fab fa-imdb"></i> 8.6</div>
      </div>
      <div class="movie-info">
        <div class="movie-title">Spider‑Verse</div>
        <div class="meta-row">
          <span class="year"><i class="far fa-calendar-alt"></i> 2023</span>
          <span class="genre">Animation</span>
        </div>
        <div class="description">Miles Morales catapults across the Multiverse, where he encounters a team of Spider-People charged with protecting its existence.</div>
        <div class="card-footer">
          <div class="rating-stars"><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><span>4.9</span></div>
          <div class="watch-btn"><i class="far fa-clock"></i> 2h 20m</div>
        </div>
      </div>
    </div>

    <!-- movie 6 : Oppenheimer -->
    <div class="movie-card">
      <div class="poster">
        <img src="https://image.tmdb.org/t/p/w600_and_h900_bestv2/8Gxv8gSFCU0XGDykEGv7zR1n2ua.jpg" alt="Oppenheimer">
        <div class="badge"><i class="fab fa-imdb"></i> 8.9</div>
      </div>
      <div class="movie-info">
        <div class="movie-title">Oppenheimer</div>
        <div class="meta-row">
          <span class="year"><i class="far fa-calendar-alt"></i> 2023</span>
          <span class="genre">History</span>
        </div>
        <div class="description">The story of J. Robert Oppenheimer's role in the development of the atomic bomb during World War II.</div>
        <div class="card-footer">
          <div class="rating-stars"><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><span>5.0</span></div>
          <div class="watch-btn"><i class="far fa-clock"></i> 3h 0m</div>
        </div>
      </div>
    </div>
  </div> <!-- end movie-grid -->

  <!-- trending this week (simple extra row) -->
  <div class="section-divider">
    <i class="fas fa-chart-line"></i>
    <h2>trending this week</h2>
  </div>
  <div class="mini-list">
    <span class="trending-item"><i class="fas fa-crown" style="color: #f7c35c;"></i> #1 Godzilla x Kong</span>
    <span class="trending-item"><i class="fas fa-crown" style="color: #c0c0c0;"></i> #2 Furiosa</span>
    <span class="trending-item"><i class="fas fa-crown" style="color: #cd7f32;"></i> #3 The Fall Guy</span>
    <span class="trending-item"><i class="fas fa-eye"></i> Civil War</span>
    <span class="trending-item"><i class="fas fa-eye"></i> Challengers</span>
  </div>

  <!-- subtle footer with fake links -->
  <div class="footer-note">
    ✦ a movie discovery concept ✦ <br>
    <i class="fas fa-star" style="color: #ff9980;"></i> data from <a href="#">reelRUSH db</a> · all posters © their studios · demo purpose
  </div>
</div> <!-- container -->
</body>
</html>
<meta name="monetag" content="33209b6e3137a97bfd8143a9ee5ae2f0">
