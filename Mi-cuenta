<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Barra Flotante + Mi Cuenta Integrado</title>
  <style>
    /* Reset básico */
    * { box-sizing: border-box; }
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding-top: 100px; /* espacio para la barra flotante */
      background: #fefefe;
      color: #222;
    }

    /* ========== Barra Flotante ========== */
    .barra-flotante {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 50px;
      background-color: #f68e03;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 0 10px;
      z-index: 9999;
      box-shadow: 0 2px 8px rgba(0,0,0,0.15);
    }

    .barra-contenido {
      width: 100%;
      max-width: 1085px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      height: 100%;
    }

    .grupo-botones {
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .btn {
      background-color: #bb6c00;
      color: #fff;
      border: none;
      padding: 6px 12px;
      border-radius: 4px;
      font-size: 14px;
      cursor: pointer;
      text-decoration: none;
      display: inline-flex;
      align-items: center;
      transition: background-color 0.3s ease;
    }
    .btn:hover {
      background-color: #a55a00;
      text-decoration: none;
    }

    /* Popup login */
    .popup-login {
      position: absolute;
      top: 50px;
      left: 10px;
      background-color: #f68e03;
      display: none;
      align-items: center;
      gap: 8px;
      padding: 8px 10px;
      border-radius: 0 0 6px 6px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.2);
      z-index: 10000;
    }
    .popup-login input[type="email"] {
      padding: 6px 8px;
      border-radius: 4px;
      border: none;
      width: 220px;
      font-size: 14px;
    }
    .popup-login .mensaje-error {
      color: #fff;
      background-color: #cc0000;
      padding: 4px 8px;
      border-radius: 4px;
      font-size: 13px;
      display: none;
      white-space: nowrap;
    }

    /* ========== Panel Mi Cuenta ========== */
    #contenedorMiCuenta {
      max-width: 700px;
      margin: 20px auto 60px;
      background: #fff;
      box-shadow: 0 2px 10px rgb(0 0 0 / 0.1);
      border-radius: 8px;
      padding: 30px;
    }
    #contenedorMiCuenta h1 {
      text-align: center;
      color: #f68e02;
      margin-bottom: 30px;
    }
    .fila {
      display: flex;
      justify-content: space-between;
      margin-bottom: 15px;
      border-bottom: 1px solid #eee;
      padding-bottom: 10px;
    }
    .fila:last-child {
      border-bottom: none;
    }
    .etiqueta {
      font-weight: bold;
      color: #555;
      min-width: 180px;
    }
    .valor {
      flex: 1;
      color: #111;
    }
    .verificado {
      color: green;
      font-weight: bold;
      margin-left: 8px;
      font-size: 18px;
      vertical-align: middle;
    }
    .btn-baja {
      display: block;
      width: 100%;
      padding: 12px;
      background-color: #bb6c00;
      color: white;
      font-weight: bold;
      text-align: center;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      margin-top: 30px;
      transition: background-color 0.3s ease;
      text-decoration: none;
    }
    .btn-baja:hover {
      background-color: #a55a00;
      text-decoration: none;
      color: white;
    }
    .info-legal {
      margin-top: 40px;
      background: #fff4e5;
      padding: 20px;
      border-radius: 6px;
      font-size: 14px;
      line-height: 1.5;
      color: #663d00;
    }

    /* Responsive */
    @media (max-width: 600px) {
      .popup-login input[type="email"] {
        width: 140px;
      }
      .etiqueta {
        min-width: 120px;
      }
    }
  </style>
</head>
<body>

  <!-- Barra Flotante -->
  <div class="barra-flotante">
    <div class="barra-contenido">
      <div class="grupo-botones" id="izquierda">
        <button class="btn" id="btnIniciarSesion" onclick="mostrarLogin()">Iniciar sesión</button>
        <span id="saludoUsuario" style="color:white; font-weight:bold;"></span>
      </div>
      <div class="grupo-botones" id="derecha">
        <a href="https://www.prenoticia.com/p/suscribirme-prenoticia.html" class="btn" target="_blank" rel="noopener noreferrer">Suscribirme</a>
        <a href="https://www.prenoticia.com/mi-cuenta-ayuda" class="btn" target="_blank" rel="noopener noreferrer">Ayuda</a>
      </div>
    </div>

    <!-- Popup Login -->
    <div class="popup-login" id="popupLogin">
      <input type="email" id="inputEmail" placeholder="Tu correo" autocomplete="username" />
      <button class="btn" onclick="validarEmail()">Ingresar</button>
      <button class="btn" onclick="cerrarLogin()">✕</button>
      <span class="mensaje-error" id="mensajeError"></span>
    </div>
  </div>

  <!-- Panel Mi Cuenta -->
  <div id="contenedorMiCuenta">
    <h1>Mi Cuenta</h1>
    <div id="contenidoCuenta"></div>
  </div>

  <script>
    // Datos centrales usuarios
    const usuarios = {
      "mauricioacostacom@gmail.com": {
        activo: true,
        nombre: "Mauricio",
        apellido: "Acosta Danaher",
        email: "mauricioacostacom@gmail.com",
        medioPago: "Mercado Pago",
        pais: "Argentina",
        montoSuscripcion: "$2.000",
        ultimoPago: "31 de julio de 2025",
        proximoPago: "31 de septiembre de 2025",
        emailVerificado: true
      },
      "luciacarpio20@gmail.com": {
        activo: false,
        nombre: "Maria",
        apellido: "Carpio Peralta",
        email: "luciacarpio20@gmail.com",
        medioPago: "PayPal",
        pais: "Chile",
        montoSuscripcion: "$1.000",
        ultimoPago: "15 de junio de 2025",
        proximoPago: "15 de julio de 2025",
        emailVerificado: false,
        deuda: "$1.000"
      }
    };

    // Mostrar login
    function mostrarLogin() {
      document.getElementById("popupLogin").style.display = "flex";
      document.getElementById("mensajeError").style.display = "none";
      document.getElementById("inputEmail").value = "";
      document.getElementById("inputEmail").focus();
    }

    // Cerrar login
    function cerrarLogin() {
      document.getElementById("popupLogin").style.display = "none";
      document.getElementById("mensajeError").style.display = "none";
      document.getElementById("inputEmail").value = "";
    }

    // Validar email y login
    function validarEmail() {
      const emailInput = document.getElementById("inputEmail");
      const email = emailInput.value.trim().toLowerCase();
      const mensaje = document.getElementById("mensajeError");
      mensaje.style.display = "none";

      if (!email) {
        mensaje.textContent = "Por favor, ingresá tu correo electrónico";
        mensaje.style.display = "inline-block";
        emailInput.focus();
        return;
      }

      if (usuarios[email]) {
        if (usuarios[email].activo) {
          // Guardar sesión
          localStorage.setItem("usuarioLogueado", JSON.stringify({ email }));
          actualizarUI();
          cerrarLogin();
        } else {
          mensaje.textContent = `Tu cuenta registra una deuda impaga de ${usuarios[email].deuda}.`;
          mensaje.style.display = "inline-block";
        }
      } else {
        mensaje.textContent = "El correo ingresado no está suscripto.";
        mensaje.style.display = "inline-block";
      }
    }

    // Mostrar usuario en barra y en panel Mi Cuenta
    function mostrarUsuario(nombre) {
      document.getElementById("btnIniciarSesion").style.display = "none";
      document.getElementById("saludoUsuario").textContent = `Hola, ${nombre}`;
    }

    // Mostrar panel "Mi Cuenta"
    function mostrarPanel(usuario) {
      const cont = document.getElementById("contenidoCuenta");

      if (!usuario) {
        cont.innerHTML = `<p>No estás logueado. Por favor <a href="#" id="linkLogin">iniciá sesión</a> para ver tu cuenta.</p>`;
        document.getElementById("linkLogin").addEventListener("click", e => {
          e.preventDefault();
          mostrarLogin();
        });
        return;
      }

      if (!usuario.activo) {
        cont.innerHTML = `<p>Tu cuenta no está activa. Por favor regularizá tu situación.</p>
          <p><b>Deuda actual:</b> ${usuario.deuda || "No disponible"}</p>`;
        return;
      }

      // Info legal según país
      let infoLegal = "";
      switch ((usuario.pais || "").toLowerCase()) {
        case "argentina":
          infoLegal = `<p><b>Información legal para Argentina:</b> De acuerdo a la Ley de Defensa del Consumidor, tenés derecho a dar de baja tu suscripción en cualquier momento y sin penalización. Para solicitar la baja, usá el botón que figura abajo o contactanos a soporte.</p>`;
          break;
        case "peru":
          infoLegal = `<p><b>Información legal para Perú:</b> Según la Ley de Protección al Consumidor, podés cancelar tu suscripción sin cargos adicionales y con derecho a recibir un comprobante. Contactá soporte si necesitás ayuda.</p>`;
          break;
        case "chile":
          infoLegal = `<p><b>Información legal para Chile:</b> Conforme a la Ley del Consumidor, podés dar de baja tu suscripción en cualquier momento y solicitar la devolución proporcional de pagos anticipados si aplica.</p>`;
          break;
        default:
          infoLegal = `<p><b>Información legal:</b> Podés gestionar tu suscripción según los términos y condiciones vigentes en tu país. Para más información, contactá soporte.</p>`;
          break;
      }

      cont.innerHTML = `
        <div class="fila"><div class="etiqueta">Nombre:</div><div class="valor">${usuario.nombre}</div></div>
        <div class="fila"><div class="etiqueta">Apellido:</div><div class="valor">${usuario.apellido}</div></div>
        <div class="fila"><div class="etiqueta">Email:</div><div class="valor">${usuario.email}
          ${usuario.emailVerificado ? '<span class="verificado" title="Email verificado">✅</span>' : ''}
        </div></div>
        <div class="fila"><div class="etiqueta">Método de pago:</div><div class="valor">${usuario.medioPago || "No especificado"}</div></div>
        <div class="fila"><div class="etiqueta">País:</div><div class="valor">${usuario.pais || "No especificado"}</div></div>
        <div class="fila"><div class="etiqueta">Monto actual suscripción:</div><div class="valor">${usuario.montoSuscripcion || "No disponible"}</div></div>
        <div class="fila"><div class="etiqueta">Último pago:</div><div class="valor">${usuario.ultimoPago || "No disponible"}</div></div>
        <div class="fila"><div class="etiqueta">Próximo pago:</div><div class="valor">${usuario.proximoPago || "No disponible"}</div></div>

        <a href="https://www.prenoticia.com/baja-suscripción" target="_blank" class="btn-baja" rel="noopener noreferrer">Dar de baja suscripción</a>

        <div class="info-legal">${infoLegal}</div>
      `;
    }

    // Actualizar UI según sesión
    function actualizarUI() {
      const sesion = JSON.parse(localStorage.getItem("usuarioLogueado"));
      if (sesion && sesion.email && usuarios[sesion.email]) {
        const usuario = usuarios[sesion.email];
        if (usuario.activo) {
          mostrarUsuario(usuario.nombre);
          mostrarPanel(usuario);
          return;
        }
      }
      // No sesión activa o usuario inactivo
      document.getElementById("btnIniciarSesion").style.display = "inline-flex";
      document.getElementById("saludoUsuario").textContent = "";
      mostrarPanel(null);
    }

    // Cerrar sesión
    function cerrarSesion() {
      localStorage.removeItem("usuarioLogueado");
      actualizarUI();
    }

    // Botón cerrar sesión dinámico
    function agregarBotonCerrar() {
      const derecha = document.getElementById("derecha");
      // Si ya existe no agregar
      if(document.getElementById("btnCerrarSesion")) return;

      const btnCerrar = document.createElement("button");
      btnCerrar.id = "btnCerrarSesion";
      btnCerrar.className = "btn";
      btnCerrar.textContent = "Cerrar sesión";
      btnCerrar.onclick = () => cerrarSesion();
      derecha.appendChild(btnCerrar);
    }

    // Remover botón cerrar sesión
    function removerBotonCerrar() {
      const btnCerrar = document.getElementById("btnCerrarSesion");
      if(btnCerrar) btnCerrar.remove();
    }

    // Actualizar botones en derecha según sesión
    function actualizarBotonesDerecha() {
      const derecha = document.getElementById("derecha");
      derecha.innerHTML = `
        <a href="https://www.prenoticia.com/p/suscribirme-prenoticia.html" class="btn" target="_blank" rel="noopener noreferrer">Suscribirme</a>
        <a href="https://www.prenoticia.com/mi-cuenta-ayuda" class="btn" target="_blank" rel="noopener noreferrer">Ayuda</a>
      `;
    }

    // Actualizar todo UI con manejo botón cerrar sesión
    function sincronizarUI() {
      const sesion = JSON.parse(localStorage.getItem("usuarioLogueado"));
      if (sesion && sesion.email && usuarios[sesion.email] && usuarios[sesion.email].activo) {
        mostrarUsuario(usuarios[sesion.email].nombre);
        mostrarPanel(usuarios[sesion.email]);
        actualizarBotonesDerecha();
        agregarBotonCerrar();
        document.getElementById("btnIniciarSesion").style.display = "none";
      } else {
        // sesión no activa o no logueado
        document.getElementById("btnIniciarSesion").style.display = "inline-flex";
        document.getElementById("saludoUsuario").textContent = "";
        mostrarPanel(null);
        actualizarBotonesDerecha();
        removerBotonCerrar();
      }
    }

    // Al cargar la página
    window.onload = () => {
      sincronizarUI();
    };
  </script>
</body>
</html>
