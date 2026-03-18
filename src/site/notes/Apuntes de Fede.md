---
{"dg-publish":true,"permalink":"/apuntes-de-fede/","title":"Apuntes de Fede","created":"2026-03-18T15:03:04.933-03:00","updated":"2026-03-18T15:03:42.947-03:00"}
---


<style>
.fede-homepage {
  padding: 1rem 0 2rem 0;
  width: 100%;
  box-sizing: border-box;
}

.fede-homepage__title {
  font-size: 2rem;
  font-weight: 700;
  text-align: center;
  margin-bottom: 2rem;
}

.fede-homepage__grid {
  display: flex;
  flex-wrap: wrap;
  gap: 1.25rem;
  width: 100%;
  box-sizing: border-box;
  justify-content: center;
}

.fede-homepage__card {
  position: relative;
  width: calc(33.333% - 1rem);
  aspect-ratio: 1 / 1;
  border-radius: 14px;
  overflow: hidden;
  cursor: pointer;
  box-sizing: border-box;
  flex-shrink: 0;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.fede-homepage__card:hover {
  transform: scale(1.03);
  box-shadow: 0 16px 48px rgba(0, 0, 0, 0.35);
}

.fede-homepage__card img {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
  position: absolute;
  top: 0;
  left: 0;
  margin: 0 !important;
}

.fede-homepage__card-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 55%;
  background: linear-gradient(to top, rgba(0,0,0,0.75) 0%, transparent 100%);
  pointer-events: none;
}

.fede-homepage__card-title {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 1rem 1rem 0.85rem;
  color: #fff !important;
  font-size: 1rem;
  font-weight: 700;
  margin: 0;
  text-shadow: 0 2px 6px rgba(0,0,0,0.5);
  line-height: 1.3;
}

.fede-homepage__card a {
  position: absolute;
  inset: 0;
  z-index: 10;
  opacity: 0;
}

/* Tablet: 2 columnas */
@media (max-width: 860px) {
  .fede-homepage__card {
    width: calc(50% - 0.75rem);
  }
}

/* Mobile: 1 columna */
@media (max-width: 520px) {
  .fede-homepage__card {
    width: 100%;
  }
}
</style>

<div class="fede-homepage">
  <h1 class="fede-homepage__title">Apuntes de Fede</h1>
  <div class="fede-homepage__grid">

    <div class="fede-homepage__card">
      <img src="https://picsum.photos/seed/instrumentacion/600/600" alt="Instrumentación y Control">
      <div class="fede-homepage__card-overlay"></div>
      <p class="fede-homepage__card-title">Instrumentación y Control</p>
      <a href="/Instrumentación-y-Control">Instrumentación y Control</a>
    </div>

    <div class="fede-homepage__card">
      <img src="https://picsum.photos/seed/circuitos/600/600" alt="Circuitos Digitales y Microcontroladores">
      <div class="fede-homepage__card-overlay"></div>
      <p class="fede-homepage__card-title">Circuitos Digitales y Microcontroladores</p>
      <a href="/Circuitos-Digitales-y-Microcontroladores">Circuitos Digitales y Microcontroladores</a>
    </div>

    <div class="fede-homepage__card">
      <img src="https://picsum.photos/seed/databases/600/600" alt="Bases de Datos">
      <div class="fede-homepage__card-overlay"></div>
      <p class="fede-homepage__card-title">Bases de Datos</p>
      <a href="/Bases-de-Datos">Bases de Datos</a>
    </div>

    <div class="fede-homepage__card">
      <img src="https://picsum.photos/seed/concurrencia/600/600" alt="Concurrencia y Paralelismo">
      <div class="fede-homepage__card-overlay"></div>
      <p class="fede-homepage__card-title">Concurrencia y Paralelismo</p>
      <a href="/Concurrencia-y-Paralelismo">Concurrencia y Paralelismo</a>
    </div>

    <div class="fede-homepage__card">
      <img src="https://picsum.photos/seed/legal/600/600" alt="Aspectos Legales de Ingeniería">
      <div class="fede-homepage__card-overlay"></div>
      <p class="fede-homepage__card-title">Aspectos Legales de Ingeniería</p>
      <a href="/Aspectos-Legales-de-Ingeniería">Aspectos Legales de Ingeniería</a>
    </div>

  </div>
</div>
