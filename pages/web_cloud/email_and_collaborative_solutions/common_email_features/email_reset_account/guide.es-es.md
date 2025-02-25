---
title: "Eliminar una cuenta de correo"
excerpt: "Cómo eliminar o restaurar una dirección de correo electrónico en un servicio de correo"
updated: 2023-01-27
---

> [!primary]
> Esta traducción ha sido generada de forma automática por nuestro partner SYSTRAN. En algunos casos puede contener términos imprecisos, como en las etiquetas de los botones o los detalles técnicos. En caso de duda, le recomendamos que consulte la versión inglesa o francesa de la guía. Si quiere ayudarnos a mejorar esta traducción, por favor, utilice el botón «Contribuir» de esta página.
>

## Objetivo

Quiere:

- Eliminar una dirección de correo electrónico que ya no esté utilizando. 
- Restaurar una cuenta de correo para utilizarla en una nueva dirección de correo. 
- Restaurar una cuenta de correo para darlo de baja.

**Cómo eliminar o restaurar una dirección de correo en un servicio de correo**

## Requisitos

- Disponer de una solución de correo electrónico de OVHcloud previamente configurada (**MX Plan**, incluida en nuestros [planes de hosting](/links/web/hosting), incluida en un [Alojamiento gratuito 100M](/links/web/domains-free-hosting) o contratada por separado como solución autónoma, como [**Hosted Exchange**](/links/web/emails-hosted-exchange) o [**Email Pro**](/links/web/email-pro)).
- Estar conectado al [área de cliente de OVHcloud](/links/manager), en la sección `Web Cloud`{.action}.
- Disponer de la información de conexión a las direcciones de correo electrónico correspondientes.

## En la práctica <a name="instructions"></a>

OVHcloud ofrece 3 soluciones de correo electrónico. El concepto de eliminación de cuenta es diferente según su solución.

- **Email MX Plan**: esta solución se vende en forma de pack de varias cuentas de correo. Cuando elimina una cuenta, libera una ubicación en su pack. 
- **Email Pro** y **Hosted Exchange**: estos dos productos son a la carta, usted contrata una suscripción individual por cuenta e-mail. Si quiere eliminar una dirección de correo, deberá **restaurar** la cuenta de correo. Una vez que haya restaurado la cuenta de correo, puede reutilizar la cuenta para crear una nueva dirección de correo. También puede [dar de baja la suscripción](/pages/web_cloud/email_and_collaborative_solutions/microsoft_exchange/manage_billing_exchange#eliminar-cuentas) de esta cuenta si desea eliminarla definitivamente.

### Eliminar o restaurar una cuenta de correo

Seleccione la pestaña correspondiente a su servicio de correo:

> [!tabs]
> **MX Plan histórico**
>>
>> Para comprobar si su MX Plan es una versión histórica o nueva, consulte el cuadro de la sección "[Identifique su solución MX Plan](#whichmxplan)" de esta guía.<br><br>
>>
>> Haga clic en `Correo electrónico`{.action} y seleccione el servicio MX Plan correspondiente. Abra la pestaña `Cuentas de correo`{.action}. Se abrirá una ventana en la que se mostrarán las cuentas de correo existentes. Haga clic en el botón `...`{.action} situado a la derecha de la cuenta que desea modificar y, seguidamente, en `Eliminar la cuenta`{.action}.<br><br>
>>![Correo electrónico](images/email-mxplan-legacy-reset.png){.thumbnail}<br>
>>
> **Emails MX Plan nueva versión**
>>
>> Para comprobar si su MX Plan es una versión histórica o nueva, consulte el cuadro de la sección "[Identifique su solución MX Plan](#whichmxplan)" de esta guía.<br><br>
>>
>> Haga clic en `Correo electrónico`{.action} y seleccione el servicio MX Plan correspondiente. Abra la pestaña `Cuentas de correo`{.action}. Se abrirá una ventana en la que se mostrarán las cuentas de correo existentes. Haga clic en el botón `...`{.action} situado al final de la línea correspondiente a la cuenta que quiera modificar y seleccione `Restaurar la cuenta`{.action}.<br><br>
>>![Correo electrónico](images/email-mxplan-new-reset.png){.thumbnail}<br>
>>
> **Email Pro**
>>
>> Haga clic en `Email Pro`{.action} y seleccione el nombre de la plataforma correspondiente. Abra la pestaña `Cuentas de correo`{.action}. Se abrirá una ventana en la que se mostrarán las cuentas de correo existentes. Haga clic en el botón `...`{.action} situado al final de la línea correspondiente a la cuenta que desea modificar y, seguidamente, en `Restaurar la cuenta`{.action}.<br><br>
>> Después de restaurar su cuenta, si desea eliminarla definitivamente, deberá darlo de baja. Para ello, consulte nuestra guía [Gestionar la facturación de sus cuentas Email-Pro](/pages/web_cloud/email_and_collaborative_solutions/email_pro/manage_billing_emailpro).<br><br>
>>![Correo electrónico](images/emailpro-reset.png){.thumbnail}<br>
>>
> **Exchange**
>>
>> Haga clic en `Microsoft`{.action}, luego en `Exchange`{.action}, y seleccione el nombre de la plataforma correspondiente. Abra la pestaña `Cuentas de correo`{.action}. Haga clic en el botón `...`{.action} situado al final de la línea correspondiente a la cuenta que desea modificar y, seguidamente, en `Reiniciar`{.action}.<br><br>
>> Después de restaurar su cuenta, si desea eliminarla definitivamente, deberá darlo de baja. Para ello, consulte nuestra guía [Gestionar la facturación de sus cuentas Exchange](/pages/web_cloud/email_and_collaborative_solutions/microsoft_exchange/manage_billing_exchange).<br><br>
>>![Correo electrónico](images/exchange-reset.png){.thumbnail}<br>
>>

#### Identifique su solución MX Plan <a name="whichmxplan"></a>

En la siguiente tabla encontrará la información necesaria para identificar su solución MX Plan.

|Versión histórica de la solución MX Plan|Nueva versión de la solución MX Plan|
|---|---|
|![Correo electrónico](images/mxplan-starter-legacy-step1.png){.thumbnail}<br> El nombre del producto aparece en el recuadro Suscripción, en el epígrafe Producto.|![Correo electrónico](images/mxplan-starter-new-step1.png){.thumbnail}<br>El nombre del producto aparece en el recuadro Resumen, en el epígrafe Referencia del servidor.|
|En esta guía, seleccione la pestaña **MXplan histórica** de esta guía.|Abra la pestaña **MXplan de la nueva versión** de esta guía.|<br>

## Más información

[Primeros pasos con la solución MX Plan](/pages/web_cloud/email_and_collaborative_solutions/mx_plan/email_generalities)

[Primeros pasos con la solución Email Pro](/pages/web_cloud/email_and_collaborative_solutions/email_pro/first_config)

[Primeros pasos con la solución Hosted Exchange](/pages/web_cloud/email_and_collaborative_solutions/microsoft_exchange/exchange_starting_hosted)

[Gestionar la facturación de las cuentas Email Pro](/pages/web_cloud/email_and_collaborative_solutions/email_pro/manage_billing_emailpro)

[Gestionar la facturación de las cuentas Exchange](/pages/web_cloud/email_and_collaborative_solutions/microsoft_exchange/manage_billing_exchange)

Si quiere disfrutar de ayuda para utilizar y configurar sus soluciones de OVHcloud, puede consultar nuestros distintos [servicios de soporte](/links/support).

Interactúe con nuestra [comunidad de usuarios](/links/community).
