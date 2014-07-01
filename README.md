ADXL335 Hardwarepins Library
============================

This library provides an interface to the ADXL335 analog triple-axis accelerometer.

* [Product information and data sheet](http://www.analog.com/en/mems-sensors/mems-inertial-sensors/adxl335/products/product.html)

Getting Started
---------------

This library can be imported into Kinoma Studio and added to an application's build path settings. You can then use the ADXL335 module to create an object that polls the sensor's accelerometer values and returns the result to the application.

The following objects can be created using the ADXL335 module in this library:

* [ADXL335](#adxl335)

Example
-------

The following example demonstrates how to instantiate a new ADXL335 object and poll the accelerometer values from the sensor.

```xml
<program xmlns="http://www.kinoma.com/kpr/1">
    <require id="ADXL335" path="ADXL335" />
    <script>
        <![CDATA[
            // create a new ADXL335 instance and specify the 
            // analog pin numbers connected to the sensor
            var adxl335 = new ADXL335.ADXL335( 56, 55, 54 );

            // initialize the sensor and start polling
            adxl335.init();
            adxl335.poll( 50, "milliseconds", "/adxl335/value" );
        ]]>
    </script>
    <handler path="/adxl335/value">
        <behavior>
            <method id="onInvoke" params="handler, message">
                <![CDATA[
                    var data = message.requestObject;

                    if( data != null )
                        trace( data.x + "," + data.y + "," + data.z + "\n" );
                ]]>
            </method>
        </behavior>
    </handler>
</program>
```

API Reference
-------------

The following reference describes the object interfaces defined in the ADXL335 module.

ADXL335
------

The ADXL335 object interface is used to get accelerometer values from the ADXL335 sensor.

Creating a new instance of a ADXL335 object:

```javascript
var adxl335 = new ADXL335.ADXL335( xpin, ypin, zpin, config );
```

Initializing the ADXL335 object instance:

```javascript
adxl335.init();
```

To request the current accelerometer values from the sensor, you must specify a callback to receive the result. The callback is the name of a handler that is implemented in your program or module:

```javascript
adxl335.get( callback );
```

To continuously poll the data from the sensor, you must specify the polling interval and time units, as well as the callback handler to receive the sensor values:

```javascript
adxl335.poll( time, units, callback, skipFirst );
```

>The units parameter must be one of the following string literal values:
>
>* milliseconds
>* seconds
>* minutes
>* microseconds
>* nanoseconds
>* hours
>* days

When the ADXL335 object's callback handler is invoked, the result will be passed in the message requestObject property. The structure of the result object will be as follows:

```javascript
{ x:.35, y:.68, z:.43 }
```
