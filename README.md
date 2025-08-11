<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Mi Cuenta - Prenoticia</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #fefefe;
      margin: 0;
      padding: 20px;
      color: #222;
    }
    .panel-cuenta {
      max-width: 700px;
      margin: 0 auto;
      background: #fff;
      box-shadow: 0 2px 10px rgb(0 0 0 / 0.1);
      border-radius: 8px;
      padding: 30px;
    }
    h1 {
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
      text-decoration: none;
      margin-top: 30px;
      transition: background-color 0.3s ease;
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
  </style>
</head>
<body>
  <div class="panel-cuenta" id="panelCuenta">
    <h1>Mi Cuenta</h1>
    <div id="contenidoCuenta"></div>
  </div>

  <script>
    // Simulamos usuarios, agrego "pais" y "monto" para suscripción
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
      // Podés agregar más usuarios acá
    };

    function mostrarPanel(usuario) {
      const cont = document.getElementById("contenidoCuenta");

      if (!usuario) {
        cont.innerHTML = `<p>No estás logueado. Por favor <a href="/login">iniciá sesión</a> para ver tu cuenta.</p>`;
        return;
      }

      if (!usuario.activo) {
        cont.innerHTML = `<p>Tu cuenta no está activa. Por favor regularizá tu situación.</p>
          <p><b>Deuda actual:</b> ${usuario.deuda || "No disponible"}</p>`;
        return;
      }

      // Info legal según país
      let infoLegal = "";
      switch (usuario.pais?.toLowerCase()) {
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

        <a href="https://www.prenoticia.com/baja-suscripción" target="_blank" class="btn-baja">Dar de baja suscripción</a>

        <div class="info-legal">${infoLegal}</div>
      `;
    }

    window.onload = () => {
      const usuarioLogueado = JSON.parse(localStorage.getItem("usuarioLogueado"));
      if (!usuarioLogueado) {
        mostrarPanel(null);
        return;
      }
      // Buscamos la info del usuario por email en el objeto usuarios
      const email = usuarioLogueado.email || usuarioLogueado.nombre?.toLowerCase() || null;
      // En tu localStorage guardás el objeto completo, asumo que tiene el email:
      let usuarioData = null;
      if (usuarioLogueado.email && usuarios[usuarioLogueado.email]) {
        usuarioData = usuarios[usuarioLogueado.email];
      }
      mostrarPanel(usuarioData);
    };
  </script>
</body>
</html>
