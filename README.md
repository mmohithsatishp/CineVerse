# CineVerse
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CineVerse | Movie World</title>

<style>
/* ===== BASE DESIGN FROM THE CINEVERSE WEBSITE ===== */
* { margin: 0; padding: 0; box-sizing: border-box; }
html { scroll-behavior: smooth; }
body {
    background: #101018;
    color: #fff;
    font-family: Arial, sans-serif;
}
header {
    background: #191923;
    padding: 20px 7%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 15px;
    position: sticky;
    top: 0;
    z-index: 20;
}
.logo { font-size: 28px; font-weight: bold; color: #fff; }
.logo span { color: #e63946; }
nav { display: flex; flex-wrap: wrap; gap: 22px; }
nav a {
    color: #fff;
    text-decoration: none;
    font-size: 15px;
    transition: color .3s;
}
nav a:hover { color: #e63946; }

/* ===== HERO + CONVERTED 3D COVERFLOW UI ===== */
.hero {
    min-height: 650px;
    padding: 55px 7% 35px;
    background:
        radial-gradient(ellipse at 50% 40%, rgba(125,28,44,.35), transparent 55%),
        linear-gradient(135deg, #171722, #09090e);
    overflow: hidden;
    display: flex;
    flex-direction: column;
    justify-content: center;
}
.hero-content { text-align: center; max-width: 760px; margin: 0 auto 12px; }
.eyebrow {
    color: #ff6975;
    text-transform: uppercase;
    letter-spacing: 3px;
    font-size: 12px;
    font-weight: bold;
    margin-bottom: 15px;
}
.hero h1 { font-size: clamp(32px, 5vw, 54px); margin-bottom: 15px; }
.hero p { color: #c7c7d0; line-height: 1.7; max-width: 650px; margin: auto; }
.hero-btn {
    display: inline-block;
    margin-top: 22px;
    padding: 13px 25px;
    border-radius: 5px;
    background: #e63946;
    color: white;
    text-decoration: none;
    font-weight: bold;
    transition: background .3s, transform .3s;
}
.hero-btn:hover { background: #b91c2a; transform: translateY(-2px); }

/* 3D Coverflow */
.coverflow {
    position: relative;
    width: 100%;
    max-width: 1050px;
    height: 390px;
    margin: 22px auto 0;
    display: flex;
    align-items: center;
    justify-content: center;
    perspective: 1500px;
    outline: none;
}
.coverflow-stage {
    position: relative;
    width: 100%;
    height: 100%;
    transform-style: preserve-3d;
}
.cover-slide {
    position: absolute;
    left: 50%;
    top: 50%;
    width: min(min(55vw, 390px), 78vw);
    height: 330px;
    border-radius: 12px;
    overflow: hidden;
    background: #252535;
    transform-origin: center center;
    transition: transform .65s cubic-bezier(.22,1,.36,1), opacity .65s ease, filter .65s ease;
    cursor: pointer;
    box-shadow: 0 22px 55px rgba(0,0,0,.5);
}
.cover-slide img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
    background: linear-gradient(145deg, #54202c, #171725 65%, #08080d);
}
.cover-slide.image-missing {
    background: linear-gradient(145deg, #54202c, #171725 65%, #08080d);
}
.cover-slide::after {
    content: "";
    position: absolute;
    inset: 35% 0 0;
    background: linear-gradient(transparent, rgba(0,0,0,.88));
    pointer-events: none;
}
.cover-title {
    position: absolute;
    z-index: 1;
    left: 20px;
    right: 15px;
    bottom: 20px;
    font-size: 23px;
    font-weight: bold;
    text-shadow: 0 2px 10px #000;
}
.cover-controls {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 18px;
    margin-top: -3px;
}
.cover-controls button {
    border: 1px solid #5b5b69;
    color: white;
    background: #242430;
    width: 42px;
    height: 42px;
    border-radius: 50%;
    cursor: pointer;
    font-size: 20px;
    transition: .25s;
}
.cover-controls button:hover { background: #e63946; border-color: #e63946; }
.cover-dots { display: flex; gap: 8px; align-items: center; }
.cover-dot {
    width: 7px; height: 7px; border-radius: 20px;
    background: #666; border: 0; cursor: pointer;
    transition: .3s;
}
.cover-dot.active { width: 24px; background: #e63946; }

/* ===== MOVIE LISTING SECTIONS ===== */
.movie-section { padding: 55px 7%; }
.section-heading {
    display: flex;
    justify-content: space-between;
    align-items: end;
    gap: 15px;
    margin-bottom: 12px;
}
.movie-section h2 { font-size: 30px; }
.section-description { color: #aaa; margin-bottom: 28px; line-height: 1.6; }
.movie-container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(190px, 1fr));
    gap: 25px;
}
.movie-card {
    background: #1d1d29;
    border-radius: 10px;
    overflow: hidden;
    transition: transform .3s, box-shadow .3s;
}
.movie-card:hover {
    transform: translateY(-8px);
    box-shadow: 0 10px 25px rgba(230,57,70,.2);
}
.movie-card img {
    width: 100%;
    height: 280px;
    object-fit: cover;
    display: block;
    background: #292936;
}
.movie-info { padding: 17px; }
.movie-info h3 { font-size: 18px; margin-bottom: 12px; }
.movie-info p { font-size: 13px; color: #bbb; margin-bottom: 10px; line-height: 1.45; }
.rating { color: #ffc107 !important; font-size: 15px !important; font-weight: bold; }
.movie-info a {
    display: block;
    text-align: center;
    background: #e63946;
    color: white;
    padding: 11px;
    margin-top: 15px;
    text-decoration: none;
    border-radius: 5px;
    transition: background .3s;
}
.movie-info a:hover { background: #b91c2a; }

/* ===== ABOUT + FOOTER ===== */
.about {
    background: #191923;
    text-align: center;
    padding: 60px 10%;
}
.about h2 { font-size: 30px; margin-bottom: 20px; }
.about p { max-width: 750px; margin: auto; color: #bbb; line-height: 1.9; }
footer { background: #0b0b10; text-align: center; padding: 30px 15px; }
footer h3 { color: #e63946; font-size: 24px; margin-bottom: 12px; }
footer p { color: #999; margin-top: 10px; font-size: 14px; }

/* ===== RESPONSIVE DESIGN ===== */
@media (max-width: 768px) {
    header { justify-content: center; }
    nav { justify-content: center; gap: 14px; }
    .hero { min-height: 590px; padding: 45px 5% 30px; }
    .coverflow { height: 330px; }
    .cover-slide { height: 270px; }
    .movie-container { grid-template-columns: repeat(2, minmax(0, 1fr)); }
    .movie-section { padding: 42px 5%; }
}
@media (max-width: 480px) {
    header { padding: 17px 5%; }
    .logo { font-size: 24px; }
    nav a { font-size: 13px; }
    .hero { min-height: 540px; }
    .hero p { font-size: 14px; }
    .coverflow { height: 280px; }
    .cover-slide { height: 225px; width: 72vw; }
    .cover-title { font-size: 18px; left: 14px; bottom: 14px; }
    .movie-section { padding: 35px 5%; }
    .movie-section h2 { font-size: 25px; }
    .movie-container { gap: 12px; }
    .movie-card img { height: 205px; }
    .movie-info { padding: 10px; }
    .movie-info h3 { font-size: 15px; }
    .movie-info p { font-size: 11px; }
    .movie-info a { font-size: 12px; padding: 9px 5px; }
}
@media (prefers-reduced-motion: reduce) {
    *, *::before, *::after { scroll-behavior: auto !important; transition-duration: .01ms !important; }
}
</style>
</head>

<body>

<header>
    <div class="logo">CINE<span>VERSE</span></div>
    <nav>
        <a href="#home">Home</a>
        <a href="#indian">Indian Movies</a>
        <a href="#hollywood">Hollywood</a>
        <a href="#about">About</a>
    </nav>
</header>

<!-- HERO SECTION WITH 3D COVERFLOW UI -->
<section class="hero" id="home">
    <div class="hero-content">
        <div class="eyebrow">Your movie destination</div>
        <h1>Discover The World Of Cinema</h1>
        <p>Explore Indian and Hollywood cinema. Discover unforgettable stories, talented actors, movie ratings and trailers — all in one place.</p>
        <a href="#indian" class="hero-btn">Explore Movies</a>
    </div>

    <div class="coverflow" id="coverflow" tabindex="0" aria-label="Featured movie carousel">
        <div class="coverflow-stage" id="coverflowStage">
            <div class="cover-slide">
                <img src="https://image.tmdb.org/t/p/w780/1XDDXPXGiI8id7MrUxK36ke7gkX.jpg" alt="Kalki 2898 AD poster" loading="eager">
                <div class="cover-title">Kalki 2898 AD</div>
            </div>
            <div class="cover-slide">
                <img src="https://image.tmdb.org/t/p/w780/5aUVLiqcW0kFTBfGsCWjvLas91w.jpg" alt="RRR poster" loading="lazy">
                <div class="cover-title">RRR</div>
            </div>
            <div class="cover-slide">
                <img src="https://image.tmdb.org/t/p/w780/qJ2tW6WMUDux911r6m7haRef0WH.jpg" alt="The Dark Knight poster" loading="lazy">
                <div class="cover-title">The Dark Knight</div>
            </div>
            <div class="cover-slide">
                <img src="https://image.tmdb.org/t/p/w780/8Gxv8gSFCU0XGDykEGv7zR1n2ua.jpg" alt="Oppenheimer poster" loading="lazy">
                <div class="cover-title">Oppenheimer</div>
            </div>
            <div class="cover-slide">
                <img src="https://image.tmdb.org/t/p/w780/8cdWjvZQUExUUTzyp4t6EDMubfO.jpg" alt="Deadpool and Wolverine poster" loading="lazy">
                <div class="cover-title">Deadpool &amp; Wolverine</div>
            </div>
            <div class="cover-slide">
                <img src="https://image.tmdb.org/t/p/w780/1pdfLvkbY9ohJlCjQH2CZjjYVvJ.jpg" alt="Dune Part Two poster" loading="lazy">
                <div class="cover-title">Dune: Part Two</div>
            </div>
            <div class="cover-slide">
                <img src="https://image.tmdb.org/t/p/w780/or06FN3Dka5tukK1e9sl16pB3iy.jpg" alt="Avengers Endgame poster" loading="lazy">
                <div class="cover-title">Avengers: Endgame</div>
            </div>
            <div class="cover-slide">
                <img src="https://image.tmdb.org/t/p/w780/1g0dhYtq4irTY1GPXvft6k4YLjm.jpg" alt="Spider-Man No Way Home poster" loading="lazy">
                <div class="cover-title">Spider-Man: No Way Home</div>
            </div>
        </div>
    </div>

    <div class="cover-controls" aria-label="Carousel controls">
        <button type="button" id="previousSlide" aria-label="Previous movie">&#8249;</button>
        <div class="cover-dots" id="coverDots"></div>
        <button type="button" id="nextSlide" aria-label="Next movie">&#8250;</button>
    </div>
</section>

<!-- INDIAN MOVIES -->
<section class="movie-section" id="indian">
    <h2>Indian Movies</h2>
    <p class="section-description">Explore popular movies from Indian cinema.</p>

    <div class="movie-container">
        <div class="movie-card">
            <img src="https://image.tmdb.org/t/p/w500/5aUVLiqcW0kFTBfGsCWjvLas91w.jpg" alt="RRR poster" loading="lazy">
            <div class="movie-info">
                <h3>RRR</h3>
                <p>Genre: Action / Drama</p>
                <p>Release: 2022</p>
                <p class="rating">★ 7.8 / 10</p>
                <a href="https://www.imdb.com/title/tt8178634/" target="_blank" rel="noopener">View Details</a>
            </div>
        </div>

        <div class="movie-card">
            <img src="https://image.tmdb.org/t/p/w500/8eifdha9GQeZAkexgtD45546XKx.jpg" alt="Animal poster" loading="lazy">
            <div class="movie-info">
                <h3>Animal</h3>
                <p>Genre: Action / Crime</p>
                <p>Release: 2023</p>
                <p class="rating">★ 6.1 / 10</p>
                <a href="https://www.imdb.com/title/tt13751694/" target="_blank" rel="noopener">View Details</a>
            </div>
        </div>

        <div class="movie-card">
            <img src="https://image.tmdb.org/t/p/w500/1XDDXPXGiI8id7MrUxK36ke7gkX.jpg" alt="Kalki 2898 AD poster" loading="lazy">
            <div class="movie-info">
                <h3>Kalki 2898 AD</h3>
                <p>Genre: Sci-Fi / Action</p>
                <p>Release: 2024</p>
                <p class="rating">★ 7.0 / 10</p>
                <a href="https://www.imdb.com/title/tt12735488/" target="_blank" rel="noopener">View Details</a>
            </div>
        </div>

        <div class="movie-card">
            <img src="https://image.tmdb.org/t/p/w500/8Gxv8gSFCU0XGDykEGv7zR1n2ua.jpg" alt="Oppenheimer poster" loading="lazy">
            <div class="movie-info">
                <h3>Oppenheimer</h3>
                <p>Genre: Biography / Drama</p>
                <p>Release: 2023</p>
                <p class="rating">★ 8.3 / 10</p>
                <a href="https://www.imdb.com/title/tt15398776/" target="_blank" rel="noopener">View Details</a>
            </div>
        </div>
    </div>
</section>

<!-- HOLLYWOOD MOVIES -->
<section class="movie-section" id="hollywood">
    <h2>Hollywood Movies</h2>
    <p class="section-description">Discover popular international movies.</p>

    <div class="movie-container">
        <div class="movie-card">
            <img src="https://image.tmdb.org/t/p/w500/qJ2tW6WMUDux911r6m7haRef0WH.jpg" alt="The Dark Knight poster" loading="lazy">
            <div class="movie-info">
                <h3>The Dark Knight</h3>
                <p>Genre: Action / Crime</p>
                <p>Release: 2008</p>
                <p class="rating">★ 9.0 / 10</p>
                <a href="https://www.imdb.com/title/tt0468569/" target="_blank" rel="noopener">View Details</a>
            </div>
        </div>

        <div class="movie-card">
            <img src="https://image.tmdb.org/t/p/w500/gEU2QniE6E77NI6lCU6MxlNBvIx.jpg" alt="Interstellar poster" loading="lazy">
            <div class="movie-info">
                <h3>Interstellar</h3>
                <p>Genre: Sci-Fi / Adventure</p>
                <p>Release: 2014</p>
                <p class="
