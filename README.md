# Aplicación con sensor de movimiento
Para el desarrollo de la aplicación usamos Device Motion, este plugin proporciona el acceso al aceleró metro del celular, el cual es el sensor de movimiento que permite obtener las coordenadas del dispositivo en los ejes x, y, z. 

Para más información del plugin acceder a la documentación: https://ionicframework.com/docs/native/Device-Motion.

## Desarrollo de la app
Esta aplicación esta desarrollada con el Framework Ionic en Angular, se uso una plantilla de tablas. Para hacer uso del plugin antes mencionada dentro del proyecto ejecutaremos los siguientes comandos:

 ```
 npm install cordova-plugin-device-motion 
 npm install @awesome-cordova-plugins/device-motion 
 ionic cap sync
```

En el archivo tab1.page.ts, se definiran las variables y metodos que permitiran obtener los datos del acelerometro.

```
import { Component } from '@angular/core';

import { DeviceMotion, DeviceMotionAccelerationData, DeviceMotionAccelerometerOptions } from '@awesome-cordova-plugins/device-motion/ngx';

@Component({
  selector: 'app-tab1',
  templateUrl: 'tab1.page.html',
  styleUrls: ['tab1.page.scss']
})
export class Tab1Page {

  x: string;
  y: string;
  z: string;
  timeStamp: string;

  id: any;

  constructor(private deviceMotion: DeviceMotion){
    this.x = "-";
    this.y = "-";
    this.z = "-";
    this.timeStamp = "-";

  }

  start(){
    
    try{
      var option: DeviceMotionAccelerometerOptions = 
      {
        frequency: 200
      };

      this.id = this.deviceMotion.watchAcceleration(option).subscribe((acc: DeviceMotionAccelerationData) => 
      {
        this.x = "" + acc.x;
        this.y = "" + acc.y;
        this.z = "" + acc.z;
        this.timeStamp = "" + acc.timestamp;
      }
      );

    }catch(err){
      alert("Error" + err)
    }
  }


  stop(){
    this.id.unsubscribe();
  }

}
```

Mientras que en el tab1.page.html mostraremos al usuario los datos obtenidos del acelerometro.

```
<ion-header [translucent]="true">
  <ion-toolbar>
    <ion-title>
      Sensor de movimiento
    </ion-title>
  </ion-toolbar>
</ion-header>

<ion-content [fullscreen]="true">
  <ion-header collapse="condense">
    <ion-toolbar>
      <ion-title size="large">Tab 1</ion-title>
    </ion-toolbar>
  </ion-header>

  <ion-card>

    <ion-card-header>
      <ion-card-title>Coordenadas</ion-card-title>
    </ion-card-header>
  
    <ion-card-content>
     
      <h1>X : {{ x }}</h1> 
      <h1>Y: {{ y }}</h1> 
      <h1>Z: {{ z }}</h1> 
      <h1>TimeStamp : {{ timeStamp }}</h1>

    </ion-card-content>
  </ion-card>
  <ion-button (click) = "start()">start</ion-button>
  <ion-button (click) = "stop()">stop</ion-button>

</ion-content>

```

### Link del video de YouTube

https://youtu.be/eQ1NeZBeORY


