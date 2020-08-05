---
title: Página estado de inscripción de Windows AutoPilot
ms.reviewer: ''
manager: laurawi
description: Proporciona información general sobre las capacidades de la página estado de inscripción, configuración
keywords: AutoPilot plug and olvídese, Windows 10
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 129023d73f7a0ed458c351e8b2bcfd482a201c23
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757221"
---
# <a name="windows-autopilot-enrollment-status-page"></a>Página estado de inscripción de Windows AutoPilot

**Se aplica a**

-   Windows 10, versión 1803 y posteriores 

La página estado de inscripción (ESP) muestra el estado del proceso de configuración de dispositivo completo cuando un usuario administrado por MDM inicia sesión en un dispositivo por primera vez.  El ESP ayudará a los usuarios a entender el progreso del aprovisionamiento de dispositivos y garantiza que el dispositivo cumpla el estado deseado de las organizaciones antes de que el usuario pueda tener acceso al escritorio por primera vez.

ESP realizará un seguimiento de la instalación de las aplicaciones, las directivas de seguridad, los certificados y las conexiones de red.  Con Intune, un administrador puede implementar perfiles ESP en un usuario de Intune con licencia y configurar opciones específicas en el perfil ESP. algunos de estos valores son: forzar la instalación de las aplicaciones especificadas, permitir a los usuarios recopilar registros de solución de problemas, especificar lo que un usuario puede hacer si se produce un error en la configuración del dispositivo.  Para obtener más información, consulte Configuración de la [Página de estado de inscripción en Intune](https://docs.microsoft.com/intune/windows-enrollment-status).   
 
 ![Página de estado de inscripción](images/enrollment-status-page.png)
 

## <a name="more-information"></a>Más información

Para obtener más información sobre la configuración de la página estado de inscripción, consulte la [documentación de Microsoft Intune](https://docs.microsoft.com/intune/windows-enrollment-status).<br>
Para obtener más información sobre la implementación subyacente, consulte los [detalles de FirstSyncStatus en la documentación de DMCLIENT CSP](https://docs.microsoft.com/windows/client-management/mdm/dmclient-csp).<br>
Para obtener más información sobre el bloqueo de la instalación de aplicaciones:
- [Bloqueando la instalación de aplicaciones mediante la página estado de inscripción](https://blogs.technet.microsoft.com/mniehaus/2018/12/06/blocking-for-app-installation-using-enrollment-status-page/).
- [Sugerencia de soporte: ahora se realiza un seguimiento de la instalación de Office C2R durante ESP](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Office-C2R-installation-is-now-tracked-during-ESP/ba-p/295514).