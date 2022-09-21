# Push Notification: Investigación en disponibilidad y viabilidad para web browsers en desktop, Android, y iOS browsers

Last date of research: **2022-09-21**

- [Push Notification: Investigación en disponibilidad y viabilidad para web browsers en desktop, Android, y iOS browsers](#push-notification-investigación-en-disponibilidad-y-viabilidad-para-web-browsers-en-desktop-android-y-ios-browsers)
  - [Navegadores desktop](#navegadores-desktop)
  - [Android](#android)
  - [iOS](#ios)

## Navegadores desktop

Fuentes:

- [How to make PWAs re-engageable using Notifications and Push
](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Re-engageable_Notifications_Push), **[2022-09-09]**

Según MDN, los browsers deberían tener incorporado el API de Push Notifications. Esto los habilita para el funcionamiento sin discriminar el sistema operativo.

Sin embargo, pueden haber limitaciones adicionales  impuestas por el sistema operativo.

El funcionamiento con PWA's requiere de un servidor que puede ser un servicio contratado como el de Firebase o puede ser hosteado personalmente en un servidor propio y utilizando librerías como [web-push](https://www.npmjs.com/package/web-push).

## Android

Con Android no hay problema, ya que el sistema operativo permite el uso de Push Notifications y lo fomenta debido a los mismos servicios ofrecidos por Google como Firebase.

En la mayoría de los casos, se espera que la documentación que existe para esta tecnología aplique para Android.

Si bien todos los navegadores soportan el Notification API, no todos los navegadores soportan el Push API.

Para circunvalar esto, se utiliza los métodos del Service Worker API.

- [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API), **[2022-12-15]**

## iOS

Fuentes:

- [Push Notifications, WebXR, and better PWA support coming to iOS](https://firt.dev/ios-15.4b), **[2022-01-31]**

>There are two new experiments on iPadOS and iOS 15.4: "Built-In Web Notifications" and "Push API," both disabled by default in the latest beta. (iOS 15.4 beta)
>
> The API to request notification permissions, subscribe to the Push service, and receive the push notification in the service worker context are available when you enable the experiments in Settings.
>
> However, I couldn't make it work. The issue appears to be with Permissions, as permissions are always denied without seeing any permission dialog request, no matter if it's after a user action or not.

- [iOS 16 enables web push notifications and extension syncing with Safari update](https://9to5mac.com/2022/06/06/ios-16-web-push-notifications-safari-update/), **[2022-06-06]**

iOS 16 es la versión que incorpora el soporte para Push Notifications en Safari; sin embargo, no lanzará la versión hasta el 2022-09, y no se sabe aún si será compatible con PWA's. Según Apple, no será una funcionalidad incorporada en el lanzamiento de iOS 16, sino que será en una actualización posterior:

> Now with iOS 16, this will become a reality. The first signs of push notifications for web apps appeared in iOS 15.4, but the feature never worked since it was labeled as “experimental.” Now, according to Apple’s website, iOS 16 and iPadOS 16 will finally enable web push notifications – but there’s a catch.
>
> Apple says the feature will come in 2023 with a future update of iOS 16, so it won’t be available at launch. At least the company has now finally confirmed that it is working on web push notifications.

- [web-push](https://www.npmjs.com/package/web-push), **[2022-05-04]**

Librería que facilita el uso de Push Notifications en navegadores... sin embargo, no permite el uso de Push Notifications en iOS:

>**Browser Support**
>| Browser | Push without Payload | Push with Payload | VAPID        | Notes                                                                                                               |
>| ------- | -------------------- | ----------------- | ------------ | ------------------------------------------------------------------------------------------------------------------- |
>| Chrome  | ✓ v42+              | ✓ v50+           | ✓ v52+      | In v51 and less, the `gcm_sender_id` is needed to get a push subscription.                                          |
>| Edge    | ✓ v17+ (April 2018) | ✓ v17+           | (April 2018) | ✓ v17+ (April 2018)                                                                                                |
>| Firefox | ✓ v44+              | ✓ v44+           | ✓ v46+      |                                                                                                                     |
>| Opera   | ✓ v39+ *            | ✓ v39+ *         | ✗           | * Opera supports push on Android but not on desktop. <br> The `gcm_sender_id` is needed to get a push subscription. |
>Safari |✗ |✗ |✗ ||
>Samsung Internet Browser |✓ v4.0.10-53+ |✓ v5.0.30-40+ |✗ |The `gcm_sender_id` is needed to get a push subscription.|

- [New features available with iOS 16](https://www.apple.com/ios/ios-16/features/), **[2022-06-06]**

La página oficial de Apple para iOS 16 indica los New Features que se incorporarán en la versión, y entre ellos se encuentra el soporte para Push Notifications en Safari:

> **Web push notifications**
>
> Adds support for opt‑in notifications on iOS. Coming in 2023.

- [Sending web push notifications in Safari and other browsers](https://developer.apple.com/documentation/usernotifications/sending_web_push_notifications_in_safari_and_other_browsers), **[Fecha desconocida]**

Documentación oficial de Apple que explica cómo habilitar el soporte para Push Notifications en Safari para macOS, mas no en otras plataformas como iOS o iPadOS.

> In Safari 16 in macOS 13 or later, Safari supports web push — push notifications that use the cross-browser Push API, Notifications API, and Service Worker standards.
