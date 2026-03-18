---
{"dg-publish":true,"permalink":"/apuntes-de-fede/","title":"Apuntes de Fede","created":"2026-03-18T14:42:18.549-03:00","updated":"2026-03-18T14:56:08.250-03:00"}
---


  

<style>

/*

  Scoped styles for Fede's Homepage

  All styles are wrapped in .fede-homepage to avoid conflicts with Digital Garden theme

*/

  

.fede-homepage {

  padding: 2rem 0;

}

  

.fede-homepage__title {

  font-size: 2.5rem;

  font-weight: 700;

  text-align: center;

  margin-bottom: 2rem;

}

  

.fede-homepage__grid {

  display: grid;

  grid-template-columns: repeat(3, 1fr);

  gap: 1.5rem;

  max-width: 1200px;

  margin: 0 auto;

}

  

/* Tablet: 2 columns */

@media (max-width: 900px) {

  .fede-homepage__grid {

    grid-template-columns: repeat(2, 1fr);

  }

}

  

/* Mobile: 1 column */

@media (max-width: 600px) {

  .fede-homepage__grid {

    grid-template-columns: 1fr;

  }

}

  

.fede-homepage__card {

  position: relative;

  aspect-ratio: 1 / 1;

  border-radius: 12px;

  overflow: hidden;

  cursor: pointer;

  transition: transform 0.3s ease, box-shadow 0.3s ease, filter 0.3s ease;

}

  

.fede-homepage__card:hover {

  transform: scale(1.03);

  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.25);

  filter: brightness(1.08);

}

  

.fede-homepage__card-image {

  position: absolute;

  top: 0;

  left: 0;

  width: 100%;

  height: 100%;

  object-fit: cover;

  z-index: 1;

}

  

.fede-homepage__card-overlay {

  position: absolute;

  bottom: 0;

  left: 0;

  right: 0;

  height: 50%;

  background: linear-gradient(to top, rgba(0, 0, 0, 0.7) 0%, rgba(0, 0, 0, 0) 100%);

  z-index: 2;

  pointer-events: none;

}

  

.fede-homepage__card-content {

  position: absolute;

  bottom: 0;

  left: 0;

  right: 0;

  padding: 1.25rem;

  z-index: 3;

}

  

.fede-homepage__card-title {

  color: #ffffff;

  font-size: 1.1rem;

  font-weight: 700;

  margin: 0;

  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);

}

  

.fede-homepage__card-link {

  position: absolute;

  top: 0;

  left: 0;

  width: 100%;

  height: 100%;

  z-index: 4;

}

  

/* Hide the wiki-link brackets for cleaner look */

.fede-homepage__card-link .internal-link {

  color: transparent;

}

</style>

  

<div class="fede-homepage">

  <h1 class="fede-homepage__title">Apuntes de Fede</h1>

  <div class="fede-homepage__grid">

    <!-- Card 1: Instrumentación y Control -->

    <!-- TODO: Replace placeholder image URL with the 'image' property from [[2-Areas/Facultad/Materias/Instrumentación y Control\|Instrumentación y Control]] frontmatter -->

    <div class="fede-homepage__card">

      <img class="fede-homepage__card-image" src="https://picsum.photos/seed/instrumentacion/600/600" alt="Instrumentación y Control">

      <div class="fede-homepage__card-overlay"></div>

      <div class="fede-homepage__card-content">

        <p class="fede-homepage__card-title">Instrumentación y Control</p>

      </div>

      <a class="fede-homepage__card-link" href="Instrumentación y Control">[[2-Areas/Facultad/Materias/Instrumentación y Control\|Instrumentación y Control]]</a>

    </div>

    <!-- Card 2: Circuitos Digitales y Microcontroladores -->

    <!-- TODO: Replace placeholder image URL with the 'image' property from [[2-Areas/Facultad/Materias/Circuitos Digitales y Microcontroladores\|Circuitos Digitales y Microcontroladores]] frontmatter -->

    <div class="fede-homepage__card">

      <img class="fede-homepage__card-image" src="https://picsum.photos/seed/circuitos/600/600" alt="Circuitos Digitales y Microcontroladores">

      <div class="fede-homepage__card-overlay"></div>

      <div class="fede-homepage__card-content">

        <p class="fede-homepage__card-title">Circuitos Digitales y Microcontroladores</p>

      </div>

      <a class="fede-homepage__card-link" href="Circuitos Digitales y Microcontroladores">[[2-Areas/Facultad/Materias/Circuitos Digitales y Microcontroladores\|Circuitos Digitales y Microcontroladores]]</a>

    </div>

    <!-- Card 3: Bases de Datos -->

    <!-- TODO: Replace placeholder image URL with the 'image' property from [[2-Areas/Facultad/Materias/Bases de Datos\|Bases de Datos]] frontmatter -->

    <div class="fede-homepage__card">

      <img class="fede-homepage__card-image" src="https://picsum.photos/seed/databases/600/600" alt="Bases de Datos">

      <div class="fede-homepage__card-overlay"></div>

      <div class="fede-homepage__card-content">

        <p class="fede-homepage__card-title">Bases de Datos</p>

      </div>

      <a class="fede-homepage__card-link" href="Bases de Datos">[[2-Areas/Facultad/Materias/Bases de Datos\|Bases de Datos]]</a>

    </div>

    <!-- Card 4: Concurrencia y Paralelismo -->

    <!-- TODO: Replace placeholder image URL with the 'image' property from [[2-Areas/Facultad/Materias/Concurrencia y Paralelismo\|Concurrencia y Paralelismo]] frontmatter -->

    <div class="fede-homepage__card">

      <img class="fede-homepage__card-image" src="https://picsum.photos/seed/concurrencia/600/600" alt="Concurrencia y Paralelismo">

      <div class="fede-homepage__card-overlay"></div>

      <div class="fede-homepage__card-content">

        <p class="fede-homepage__card-title">Concurrencia y Paralelismo</p>

      </div>

      <a class="fede-homepage__card-link" href="Concurrencia y Paralelismo">[[2-Areas/Facultad/Materias/Concurrencia y Paralelismo\|Concurrencia y Paralelismo]]</a>

    </div>

    <!-- Card 5: Aspectos Legales de Ingeniería -->

    <!-- TODO: Replace placeholder image URL with the 'image' property from [[2-Areas/Facultad/Materias/Aspectos Legales de Ingeniería\|Aspectos Legales de Ingeniería]] frontmatter -->

    <div class="fede-homepage__card">

      <img class="fede-homepage__card-image" src="https://picsum.photos/seed/legal/600/600" alt="Aspectos Legales de Ingeniería">

      <div class="fede-homepage__card-overlay"></div>

      <div class="fede-homepage__card-content">

        <p class="fede-homepage__card-title">Aspectos Legales de Ingeniería</p>

      </div>

      <a class="fede-homepage__card-link" href="Aspectos Legales de Ingeniería">[[2-Areas/Facultad/Materias/Aspectos Legales de Ingeniería\|Aspectos Legales de Ingeniería]]</a>

    </div>

  </div>

</div>