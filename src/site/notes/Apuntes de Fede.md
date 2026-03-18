---
{"dg-publish":true,"permalink":"/apuntes-de-fede/","created":"2026-03-18T15:03:04.933-03:00","updated":"2026-03-18T15:16:57.788-03:00"}
---


  

<style>

/*

  Scoped styles for Fede's Homepage

  Using !important to override Digital Garden theme styles

*/

  

/* Reset any theme interference on the container */

.fede-homepage {

  display: block !important;

  width: 100% !important;

  max-width: 100% !important;

  padding: 2rem 0 !important;

  margin: 0 !important;

  box-sizing: border-box !important;

}

  

.fede-homepage__title {

  display: block !important;

  font-size: 2.5rem !important;

  font-weight: 700 !important;

  text-align: center !important;

  margin: 0 0 2rem 0 !important;

  padding: 0 !important;

}

  

/* Grid container - force proper matrix layout */

.fede-homepage__grid {

  display: grid !important;

  grid-template-columns: repeat(3, 1fr) !important;

  grid-auto-rows: auto !important;

  gap: 1.25rem !important;

  width: 100% !important;

  max-width: 900px !important;

  margin: 0 auto !important;

  padding: 0 !important;

  box-sizing: border-box !important;

  list-style: none !important;

}

  

/* Force all cards to be direct grid items without any extra spacing */

.fede-homepage__grid > * {

  margin: 0 !important;

  padding: 0 !important;

}

  

/* Card styles */

.fede-homepage__card {

  display: block !important;

  position: relative !important;

  width: 100% !important;

  height: 0 !important;

  padding-bottom: 100% !important; /* Square aspect ratio fallback */

  aspect-ratio: 1 / 1 !important;

  border-radius: 12px !important;

  overflow: hidden !important;

  cursor: pointer !important;

  margin: 0 !important;

  box-sizing: border-box !important;

  transition: transform 0.3s ease, box-shadow 0.3s ease, filter 0.3s ease !important;

}

  

.fede-homepage__card:hover {

  transform: scale(1.03) !important;

  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.35) !important;

  filter: brightness(1.08) !important;

}

  

/* Card image - absolute fill */

.fede-homepage__card-image {

  display: block !important;

  position: absolute !important;

  top: 0 !important;

  left: 0 !important;

  width: 100% !important;

  height: 100% !important;

  object-fit: cover !important;

  z-index: 1 !important;

  margin: 0 !important;

  padding: 0 !important;

  border: none !important;

  border-radius: 0 !important;

}

  

/* Gradient overlay */

.fede-homepage__card-overlay {

  display: block !important;

  position: absolute !important;

  bottom: 0 !important;

  left: 0 !important;

  right: 0 !important;

  height: 55% !important;

  background: linear-gradient(to top, rgba(0, 0, 0, 0.75) 0%, rgba(0, 0, 0, 0) 100%) !important;

  z-index: 2 !important;

  pointer-events: none !important;

  margin: 0 !important;

  padding: 0 !important;

}

  

/* Card content area */

.fede-homepage__card-content {

  display: block !important;

  position: absolute !important;

  bottom: 0 !important;

  left: 0 !important;

  right: 0 !important;

  padding: 1rem !important;

  z-index: 3 !important;

  margin: 0 !important;

  box-sizing: border-box !important;

}

  

/* Card title */

.fede-homepage__card-title {

  display: block !important;

  color: #ffffff !important;

  font-size: 1rem !important;

  font-weight: 700 !important;

  line-height: 1.3 !important;

  margin: 0 !important;

  padding: 0 !important;

  text-shadow: 0 2px 6px rgba(0, 0, 0, 0.5) !important;

}

  

/* Invisible link overlay */

.fede-homepage__card-link {

  display: block !important;

  position: absolute !important;

  top: 0 !important;

  left: 0 !important;

  right: 0 !important;

  bottom: 0 !important;

  width: 100% !important;

  height: 100% !important;

  z-index: 4 !important;

  margin: 0 !important;

  padding: 0 !important;

  text-decoration: none !important;

  color: transparent !important;

  font-size: 0 !important;

}

  

/* Hide internal link text completely */

.fede-homepage__card-link,

.fede-homepage__card-link * {

  color: transparent !important;

  font-size: 0 !important;

}

  

/* Tablet: 2 columns */

@media (max-width: 700px) {

  .fede-homepage__grid {

    grid-template-columns: repeat(2, 1fr) !important;

  }

}

  

/* Mobile: 1 column */

@media (max-width: 480px) {

  .fede-homepage__grid {

    grid-template-columns: 1fr !important;

  }

  .fede-homepage__card-title {

    font-size: 0.95rem !important;

  }

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