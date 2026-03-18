---
{"dg-publish":true,"permalink":"/apuntes-de-fede/","created":"2026-03-18T15:03:04.933-03:00","updated":"2026-03-18T15:12:09.233-03:00"}
---


<style>
.fede-homepage {
  width: 100%;
  box-sizing: border-box;
  padding: 1rem 0 2rem 0;
}

.fede-homepage__title {
  font-size: 2rem;
  font-weight: 700;
  text-align: center;
  margin-bottom: 2rem;
}

.fede-homepage__grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  width: 100%;
  box-sizing: border-box;
}

/* La quinta card centrada en la segunda fila */
.fede-homepage__card:nth-child(5) {
  grid-column: 2 / 3;
}

.fede-homepage__card {
  position: relative;
  width: 100%;
  aspect-ratio: 1 / 1;
  border-radius: 14px;
  overflow: hidden;
  cursor: pointer;
  box-sizing: border-box;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  display: block;
}

.fede-homepage__card:hover {
  transform: scale(1.03);
  box-shadow: 0 16px 48px rgba(0, 0, 0, 0.4);
}

.fede-homepage__card img {
  display: block !important;
  width: 100% !important;
  height: 100% !important;
  object-fit: cover !important;
  position: absolute !important;
  top: 0 !important;
  left: 0 !important;
  margin: 0 !important;
  padding: 0 !important;
}

.fede-homepage__overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 55%;
  background: linear-gradient(to top, rgba(0,0,0,0.78) 0%, transparent 100%);
  pointer-events: none;
  z-index: 2;
}

.fede-homepage__label {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 0.85rem 0.9rem;
  color: #fff !important;
  font-size: 0.95rem;
  font-weight: 700;
  margin: 0 !important;
  text-shadow: 0 2px 6px rgba(0,0,0,0.6);
  line-height: 1.3;
  z-index: 3;
}

.fede-homepage__card a {
  position: absolute !important;
  inset: 0 !important;
  z-index: 10 !important;
  opacity: 0 !important;
  display: block !important;
}

/* Tablet: 2 columnas, quinta centrada */
@media (max-width: 700px) {
  .fede-homepage__grid {
    grid-template-columns: repeat(2, 1fr);
  }
  .fede-homepage__card:nth-child(5) {
    grid-column: 1 / 3;
    max-width: calc(50% - 0.5rem);
    justify-self: center;
  }
}

/* Mobile: 1 columna */
@media (max-width: 420px) {
  .fede-homepage__grid {
    grid-template-columns: 1fr;
  }
  .fede-homepage__card:nth-child(5) {
    grid-column: 1;
    max-width: 100%;
  }
}
</style>

<div class="fede-homepage">
  <h1 class="fede-homepage__title">Apuntes de Fede</h1>
  <div class="fede-homepage__grid">

    <div class="fede-homepage__card">
      <img src="https://picsum.photos/seed/instrumentacion/600/600" alt="Instrumentación y Control">
      <div class="fede-homepage__overlay"></div>
      <p class="fede-homepage__label">Instrumentación y Control</p>
      <a href="/Instrumentación-y-Control">Instrumentación y Control</a>
    </div>

    <div class="fede-homepage__card">
      <img src="https://picsum.photos/seed/circuitos/600/600" alt="Circuitos Digitales y Microcontroladores">
      <div class="fede-homepage__overlay"></div>
      <p class="fede-homepage__label">Circuitos Digitales y Microcontroladores</p>
      <a href="/Circuitos-Digitales-y-Microcontroladores">Circuitos Digitales y Microcontroladores</a>
    </div>

    <div class="fede-homepage__card">
      <img src="https://picsum.photos/seed/databases/600/600" alt="Bases de Datos">
      <div class="fede-homepage__overlay"></div>
      <p class="fede-homepage__label">Bases de Datos</p>
      <a href="/Bases-de-Datos">Bases de Datos</a>
    </div>

    <div class="fede-homepage__card">
      <img src="https://picsum.photos/seed/concurrencia/600/600" alt="Concurrencia y Paralelismo">
      <div class="fede-homepage__overlay"></div>
      <p class="fede-homepage__label">Concurrencia y Paralelismo</p>
      <a href="/Concurrencia-y-Paralelismo">Concurrencia y Paralelismo</a>
    </div>

    <div class="fede-homepage__card">
      <img src="https://picsum.photos/seed/legal/600/600" alt="Aspectos Legales de Ingeniería">
      <div class="fede-homepage__overlay"></div>
      <p class="fede-homepage__label">Aspectos Legales de Ingeniería</p>
      <a href="/Aspectos-Legales-de-Ingeniería">Aspectos Legales de Ingeniería</a>
    </div>

  </div>
</div>
