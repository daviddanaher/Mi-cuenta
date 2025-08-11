<style>
  /* Barra flotante, ocupa todo el ancho */
  #ventana-flotante {
    position: fixed;
    top: 75px;
    left: 0;
    width: 100vw;
    height: 50px;
    background: #f68e02;
    box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    z-index: 49;

    display: flex;
    justify-content: center; /* centra el contenido */
    align-items: center;

    /* Para animación de deslizar */
    transform: translateY(0);
    opacity: 1;
    transition: top 0.3s ease, transform 0.3s ease, opacity 0.3s ease;
  }

  /* Estado oculto: barra deslizada hacia arriba y oculta */
  #ventana-flotante.oculto {
    opacity: 0;
    transform: translateY(-100%);
    pointer-events: none; /* para que no interfiera cuando está oculta */
  }

  /* Contenedor interno para limitar ancho y centrar contenido */
  #ventana-flotante .contenido {
    width: 100%;
    max-width: 1090px;
    height: 100%;
  }

  #ventana-flotante iframe {
    width: 100%;
    height: 100%;
    border: none;
    display: block;
  }

  /* Móvil: barra fija visible con top 50px, ancho total y sin bordes ni márgenes */
  @media (max-width: 768px) {
    #ventana-flotante {
      top: 50px !important;
      left: 0 !important;
      width: 100vw !important;
      border-radius: 0 !important;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    }
  }
</style>

<div id="ventana-flotante">
  <div class="contenido">
    <iframe src="https://daviddanaher.github.io/Prenoticia/"></iframe>
  </div>
</div>

<script>
  const ventana = document.getElementById("ventana-flotante");

  function esEscritorio() {
    return window.innerWidth > 768;
  }

  function actualizarBarra() {
    if (!esEscritorio()) {
      // En móvil barra fija visible a top 50px sin márgenes ni bordes
      ventana.classList.remove("oculto");
      ventana.style.top = "50px";
      ventana.style.left = "0";
      ventana.style.width = "100vw";
      ventana.style.borderRadius = "0";
      return;
    }

    const scrollY = window.pageYOffset;

    if (scrollY === 0) {
      // Parte superior: barra visible, top 75px sin margen extra
      ventana.classList.remove("oculto");
      ventana.style.top = "75px";
      ventana.style.left = "0";
      ventana.style.width = "100vw";
      ventana.style.borderRadius = "0";
    } else if (scrollY > 0 && scrollY < 200) {
      // Scroll entre 0 y 200px: ocultar barra
      ventana.classList.add("oculto");
    } else if (scrollY >= 200) {
      // Scroll mayor a 200px: barra visible, top 45px (margen flotante)
      ventana.classList.remove("oculto");
      ventana.style.top = "45px";
      ventana.style.left = "0";
      ventana.style.width = "100vw";
      ventana.style.borderRadius = "0";
    }
  }

  window.addEventListener("scroll", actualizarBarra);
  window.addEventListener("load", actualizarBarra);
  window.addEventListener("resize", actualizarBarra);
</script>
