# Push Notification para PWA

- [Push Notification para PWA](#push-notification-para-pwa)
  - [Investigación en funciones, limitaciones y viabilidad para Android, iOS browsers en desktop](#investigación-en-funciones-limitaciones-y-viabilidad-para-android-ios-browsers-en-desktop)
    - [Navegadores desktop](#navegadores-desktop)
    - [Android](#android)
    - [iOS](#ios)

## Investigación en funciones, limitaciones y viabilidad para Android, iOS browsers en desktop

### Navegadores desktop

Fuentes:

- [How to make PWAs re-engageable using Notifications and Push
](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Re-engageable_Notifications_Push), 2022-09-09

Según MDN, los browsers deberían tener incorporado el API de Push Notifications. Esto los habilita para el funcionamiento sin discriminar el sistema operativo.

Sin embargo, pueden haber limitaciones adicionales  impuestas por el sistema operativo.

El funcionamiento con PWA's requiere de un servidor que puede ser un servicio contratado como el de Firebase o puede ser hosteado personalmente en un servidor propio y utilizando librerías como [web-push](https://www.npmjs.com/package/web-push).

### Android

Con Android no hay problema, ya que el sistema operativo permite el uso de Push Notifications y lo fomenta debido a los mismos servicios ofrecidos por Google como Firebase.

En la mayoría de los casos, se espera que la documentación que existe aplique para Android.

### iOS

Fuentes:

- [Push Notifications, WebXR, and better PWA support coming to iOS](https://firt.dev/ios-15.4b), 2022-01-31
- [iOS 16 enables web push notifications and extension syncing with Safari update](https://9to5mac.com/2022/06/06/ios-16-web-push-notifications-safari-update/), 2022-06-06

iOS 16 es la versión que incorpora el soporte para Push Notifications en Safari; sin embargo, no lanzará la versión hasta el 2022-09, y no se sabe aún si será compatible con PWA's. Según Apple, no será una funcionalidad incorporada en el lanzamiento de iOS 16, sino que será en una actualización posterior:

```text
Now with iOS 16, this will become a reality. The first signs of push notifications for web apps appeared in iOS 15.4, but the feature never worked since it was labeled as “experimental.” Now, according to Apple’s website, iOS 16 and iPadOS 16 will finally enable web push notifications – but there’s a catch.

Apple says the feature will come in 2023 with a future update of iOS 16, so it won’t be available at launch. At least the company has now finally confirmed that it is working on web push notifications.
```
