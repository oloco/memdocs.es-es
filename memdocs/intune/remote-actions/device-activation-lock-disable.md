---
title: Omisión del Bloqueo de activación de iOS/iPadOS con Intune
titleSuffix: Microsoft Intune
description: Obtenga información sobre cómo usar Intune para omitir el Bloqueo de activación de iOS/iPadOS a fin de acceder a los dispositivos bloqueados.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 9ca3b0ba-e41c-45fb-af28-119dff47c59f
ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: eec2bb84a27445444c85f7d64a8d0531fbc30939
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989936"
---
# <a name="disable-activation-lock-on-supervised-iosipados-devices-with-intune"></a>Deshabilitación del Bloqueo de activación en dispositivos iOS/iPadOS supervisados con Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Microsoft Intune puede ayudarle a administrar el Bloqueo de activación de iOS/iPadOS, una característica de la aplicación Buscar mi iPhone para dispositivos iOS/iPadOS 8.0 y versiones posteriores. El bloqueo de activación se habilita automáticamente cuando un usuario abre la aplicación Buscar mi iPhone en un dispositivo. Tras su activación, se debe escribir el identificador y la contraseña de Apple del usuario para poder:

- Desactivar Buscar mi iPhone
- Borrar el dispositivo
- Reactivar el dispositivo

## <a name="how-activation-lock-affects-you"></a>Cómo afecta el bloqueo de activación

Aunque el Bloqueo de activación ayuda a proteger los dispositivos iOS/iPadOS y aumenta las posibilidades de recuperar un dispositivo perdido o robado, esta funcionalidad puede suponerle una serie de desafíos como administrador de TI. Por ejemplo:

- Un usuario establece el bloqueo de activación en un dispositivo. Luego, el usuario se va de la empresa y devuelve el dispositivo. Sin el identificador y la contraseña de Apple del usuario, no hay forma de volver a activar el dispositivo.
- Necesita un informe de todos los dispositivos que tienen habilitado el bloqueo de activación.
- Durante una actualización de los dispositivos de la organización, puede que quiera reasignar algunos dispositivos a un departamento diferente. Solo puede volver a asignar dispositivos que no tengan habilitado el bloqueo de activación.

Para ayudar a resolver estos problemas, Apple incorporó la deshabilitación del Bloqueo de activación en iOS/iPadOS 7.1. La deshabilitación del Bloqueo de activación permite quitar el Bloqueo de activación de los dispositivos supervisados sin el identificador y la contraseña de Apple del usuario. Los dispositivos supervisados pueden generar un código de bypass del bloqueo de activación específico del dispositivo, que se almacena en el servidor de activación de Apple.

>[!TIP]
>El modo supervisado de los dispositivos iOS/iPadOS permite usar Apple Configurator para bloquear un dispositivo y limitar la funcionalidad para fines empresariales específicos. El modo supervisado solo se usa para los dispositivos de la empresa.

Puede leer más acerca de bloqueo de activación en [el sitio web de Apple](https://support.apple.com/HT201365).

## <a name="how-intune-helps-you-manage-activation-lock"></a>Cómo ayuda Intune a administrar el bloqueo de activación
Intune puede solicitar el estado de Bloqueo de activación de dispositivos supervisados que ejecutan iOS/iPadOS 8.0 y versiones posteriores. Solamente para los dispositivos supervisados, Intune puede recuperar el código de deshabilitación del Bloqueo de activación y emitirlo directamente al dispositivo. En caso de que el dispositivo se haya borrado, puede acceder directamente a él usando un nombre de usuario en blanco y el código como la contraseña.

**Las ventajas empresariales de usar Intune para administrar el Bloqueo de activación son las siguientes:**

- El usuario obtiene los beneficios de seguridad de la aplicación Buscar mi iPhone.
- Puede permitir que los usuarios hagan su trabajo y sepa que, cuando el dispositivo se deba reasignar, podrá retirarlo o desbloquearlo.

## <a name="before-you-start"></a>Antes de empezar
Para deshabilitar el Bloqueo de activación en los dispositivos, primero debe habilitarlo. Para ello, siga estas instrucciones:

1. Configure un perfil de restricción de Intune para iOS/iPadOS mediante la información que se describe en [Configurar restricciones de dispositivos en Microsoft Intune](../configuration/device-restrictions-configure.md).
2. En la [configuración de restricción de dispositivos para iOS/iPadOS](../configuration/device-restrictions-ios.md), en la sección **General**, habilite la opción **Bloqueo de activación**.
3. Guarde el perfil y [asígnelo](../configuration/device-profile-assign.md) a los dispositivos en los que quiera administrar la deshabilitación del Bloqueo de activación.


## <a name="how-to-use-disable-activation-lock"></a>Uso de la deshabilitación del Bloqueo de activación

>[!IMPORTANT]
>Después de deshabilitar el Bloqueo de activación en un dispositivo, si se inicia la aplicación Buscar mi iPhone, se aplica automáticamente un nuevo Bloqueo de activación. Por este motivo, **para realizar este procedimiento, debe tener el dispositivo físicamente**.

La acción remota del dispositivo **Deshabilitar el bloqueo de activación** de Intune quita el bloqueo de activación de un dispositivo iOS/iPadOS sin requerir el ID de Apple ni la contraseña del usuario. Después de deshabilitar el Bloqueo de activación, el dispositivo lo vuelve a activar cuando se inicia la aplicación Buscar mi iPhone. Deshabilite el bloqueo de activación solo si tiene acceso físico al dispositivo.

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. En la hoja **Intune**, haga clic en **Dispositivos**.
4. En la hoja **Dispositivos**, haga clic en **Todos los dispositivos**.
5. En la lista de dispositivos que administra, seleccione la acción de dispositivo remoto **Deshabilitación del Bloqueo de activación**.
6. Vaya a la sección "Hardware" del dispositivo y, después, copie el valor **Código de omisión del bloqueo de activación**, bajo **Acceso condicional**.

    >[!NOTE]
    >Copie el código de omisión antes de borrar el dispositivo. Si restablece la configuración del dispositivo antes de copiar el código, el código se quita de Azure.

7. Vaya a la hoja **Información general** del dispositivo y, después, haga clic en **Borrar**.
8. Después de restablecer el dispositivo, se le solicitará el *ID de Apple* y la *contraseña*. Deje el campo *ID* en blanco y, después, escriba el **código de omisión** para la *contraseña*. Esto quita la cuenta del dispositivo. 


## <a name="next-steps"></a>Pasos siguientes

Puede examinar el estado de la solicitud de desbloqueo en la página de detalles del dispositivo de la carga de trabajo **Administrar dispositivos**.
