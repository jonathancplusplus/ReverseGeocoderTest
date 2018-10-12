# Geocodificación Inversa en Android


<img src="https://github.com/jonathancplusplus/ReverseGeocoderTest/blob/master/example_geocoder.png" width="480">

# ¿Qué es la Geocodificación inversa?

La geocodificación inversa es el proceso por el cual se obtiene una ubicación (País,Ciudad,etc) dada una coordenada GPS (latitud y longitud), más información en [Wikipedia](https://en.wikipedia.org/wiki/Reverse_geocoding).


# ¿Comó integrarlo en un proyecto?

<b>Primero se deben agregar las siguientes dependencias al archivo </b> ``` build.gradle (Module : app ) ```

Para habilitar el uso de Lambda

    android {
        ...
        compileOptions {
            sourceCompatibility = '1.8'
            targetCompatibility = '1.8'
        }
    }
Para integrar los servicios de la API de Google

    dependencies {
        ...
        implementation 'com.google.android.gms:play-services:12.0.1'
    }

<b> Segundo se deben agregar los siguientes cambios al archivo </b> ``` AndroidManifest.xml```

Permisos necesarios para habilitar la geolocalización

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />

Siempre en manifest dentro de las etiquetas ``` <application> ... </application> ``` se agrega el siguiente servicio

    <application ...>
        ... 
        <service
            android:name=".FetchAddressIntentService"
            android:exported="false"/>
    </application>
  
<b> Finalmente copia los archivos </b>  ``` Constants.java , FetchAddressIntentService.java , PositionLatLngActivity.java , Utils.java ``` <b> que estan en [ReverseGeocoderTest/app/src/main/java/com/softlutions/hv12/reversegeocodertest/](https://github.com/jonathancplusplus/ReverseGeocoderTest/tree/master/app/src/main/java/com/softlutions/hv12/reversegeocodertest). a tu proyecto </b>

# ¿Comó usar los servicios de geolocalización?

<b> Aplica herencia de la clase </b> ``` PositionLatLngActivity ``` <b> en el activity que deseas agregar la funcionalidad de Geolocalización. </b>

    public class MainActivity extends PositionLatLngActivity {
      ...
    }

Para obtener Latitud y Longitud de la posición en ese instante llama a la función ``` updateLatLng(); ``` y captura el resultado agregando el siguiente método
    
    
    @Override
    protected void handleNewLocation(Location location) {
        super.handleNewLocation(location);
        double lat = location.getLatitude();
        double lng = location.getLongitude();
    }
    
Por defecto las actualizaciones automaticas estan desactivadas pero si deseas cambiar esto llama al metodo ``` isAutomaticUpdates( true o false ) ``` y asignale true o false dependiendo que desees, y si quieres establecer cada cuanto tiempo se haran las actualizaciones entonces llama al mismo método pero envia como segundo parametro el tiempo en milisegundos.


