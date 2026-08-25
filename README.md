# Ex.No:5 Develop a simple application for proximity sensor using Sensor Manager in android studio.


## AIM:

To develop a sensor application for proximity sensor using sensor manager in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Giraffe)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as proximitysensor and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display process of proximitysensor in android mobile devices.

Step 7: Save and run the application.

## PROGRAM:
```
Program to print the process of proximitysensor in android mobile devices”.
Developed by: SWETHA A
Registeration Number : 212223220114

```
## MainActivity.java
```
package com.example.proximitysensor;

import android.hardware.Sensor;
import android.hardware.SensorEvent;
import android.hardware.SensorEventListener;
import android.hardware.SensorManager;
import android.os.Bundle;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

import java.util.Locale;

public class MainActivity extends AppCompatActivity
        implements SensorEventListener {

    private SensorManager sensorManager;
    private Sensor proximitySensor;

    private TextView tvStatus;
    private TextView tvStatusIcon;
    private TextView tvStatusDescription;
    private TextView tvDistance;
    private TextView tvMaxRange;
    private TextView tvAvailability;
    private TextView tvDeviceIndicator;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_main);

        
        tvStatus = findViewById(R.id.tvStatus);
        tvStatusIcon = findViewById(R.id.tvStatusIcon);
        tvStatusDescription = findViewById(R.id.tvStatusDescription);
        tvDistance = findViewById(R.id.tvDistance);
        tvMaxRange = findViewById(R.id.tvMaxRange);
        tvAvailability = findViewById(R.id.tvAvailability);
        tvDeviceIndicator = findViewById(R.id.tvDeviceIndicator);

        
        sensorManager =
                (SensorManager) getSystemService(SENSOR_SERVICE);

        
        proximitySensor =
                sensorManager.getDefaultSensor(Sensor.TYPE_PROXIMITY);

        
        if (proximitySensor == null) {

            tvStatus.setText("UNAVAILABLE");
            tvStatusIcon.setText("●");
            tvStatusIcon.setTextColor(
                    getColor(android.R.color.holo_red_light));

            tvStatusDescription.setText(
                    "This device has no proximity sensor");

            tvAvailability.setText(
                    "Proximity sensor not available");

            tvDeviceIndicator.setTextColor(
                    getColor(android.R.color.holo_red_light));

            tvDistance.setText("--");

            tvMaxRange.setText("-- cm");

        } else {

            
            float maxRange = proximitySensor.getMaximumRange();

            tvMaxRange.setText(
                    String.format(
                            Locale.getDefault(),
                            "%.1f cm",
                            maxRange
                    )
            );

            tvAvailability.setText(
                    "Proximity sensor available"
            );

            tvDeviceIndicator.setTextColor(
                    getColor(android.R.color.holo_green_light)
            );
        }
    }

    @Override
    protected void onResume() {
        super.onResume();

        if (proximitySensor != null) {

            sensorManager.registerListener(
                    this,
                    proximitySensor,
                    SensorManager.SENSOR_DELAY_NORMAL
            );
        }
    }

    @Override
    protected void onPause() {
        super.onPause();

        
        sensorManager.unregisterListener(this);
    }

    @Override
    public void onSensorChanged(SensorEvent event) {

        if (event.sensor.getType() ==
                Sensor.TYPE_PROXIMITY) {

            float distance = event.values[0];

           
            tvDistance.setText(
                    String.format(
                            Locale.getDefault(),
                            "%.1f",
                            distance
                    )
            );

            

            if (distance < proximitySensor.getMaximumRange()) {

                tvStatus.setText("NEAR");

                tvStatusIcon.setText("●");

                tvStatusIcon.setTextColor(
                        getColor(android.R.color.holo_orange_light)
                );

                tvStatusDescription.setText(
                        "Object detected nearby"
                );

            } else {

                tvStatus.setText("FAR");

                tvStatusIcon.setText("●");

                tvStatusIcon.setTextColor(
                        getColor(android.R.color.holo_green_light)
                );

                tvStatusDescription.setText(
                        "Nothing detected nearby"
                );
            }
        }
    }

    @Override
    public void onAccuracyChanged(
            Sensor sensor,
            int accuracy) {

        
    }
}
```


## Activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>

<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#0B1020">


    <View
        android:id="@+id/topGlow"
        android:layout_width="280dp"
        android:layout_height="280dp"
        android:background="@drawable/glow_circle"
        android:alpha="0.35"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toTopOf="parent" />


    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:fillViewport="true">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical"
            android:padding="24dp">

            

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="SENSOR LAB"
                android:textColor="#8B9EFF"
                android:textSize="13sp"
                android:textStyle="bold"
                android:letterSpacing="0.15"
                android:layout_marginTop="12dp" />

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Proximity Sensor"
                android:textColor="#FFFFFF"
                android:textSize="32sp"
                android:textStyle="bold"
                android:layout_marginTop="5dp" />

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Real-time sensor monitoring"
                android:textColor="#8991A8"
                android:textSize="15sp"
                android:layout_marginTop="5dp"
                android:layout_marginBottom="24dp" />

           

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="220dp"
                android:orientation="vertical"
                android:gravity="center"
                android:padding="20dp"
                android:background="@drawable/status_card">

                <TextView
                    android:id="@+id/tvStatusIcon"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="●"
                    android:textColor="#6CFF9B"
                    android:textSize="42sp" />

                <TextView
                    android:id="@+id/tvStatus"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="FAR"
                    android:textColor="#FFFFFF"
                    android:textSize="30sp"
                    android:textStyle="bold"
                    android:layout_marginTop="4dp" />

                <TextView
                    android:id="@+id/tvStatusDescription"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="Nothing detected nearby"
                    android:textColor="#A8B0C5"
                    android:textSize="14sp"
                    android:layout_marginTop="5dp" />

            </LinearLayout>

            

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:orientation="vertical"
                android:padding="20dp"
                android:layout_marginTop="18dp"
                android:background="@drawable/info_card">

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="CURRENT DISTANCE"
                    android:textColor="#8B9EFF"
                    android:textSize="12sp"
                    android:textStyle="bold"
                    android:letterSpacing="0.1" />

                <LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:orientation="horizontal"
                    android:gravity="bottom"
                    android:layout_marginTop="8dp">

                    <TextView
                        android:id="@+id/tvDistance"
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:text="0.0"
                        android:textColor="#FFFFFF"
                        android:textSize="42sp"
                        android:textStyle="bold" />

                    <TextView
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:text=" cm"
                        android:textColor="#8B9EFF"
                        android:textSize="18sp"
                        android:layout_marginBottom="7dp" />

                </LinearLayout>

            </LinearLayout>


            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="SENSOR INFORMATION"
                android:textColor="#FFFFFF"
                android:textSize="15sp"
                android:textStyle="bold"
                android:layout_marginTop="25dp"
                android:layout_marginBottom="12dp" />

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:orientation="horizontal">

              

                <LinearLayout
                    android:layout_width="0dp"
                    android:layout_height="110dp"
                    android:layout_weight="1"
                    android:orientation="vertical"
                    android:padding="16dp"
                    android:background="@drawable/info_card"
                    android:layout_marginEnd="8dp">

                    <TextView
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:text="TYPE"
                        android:textColor="#8991A8"
                        android:textSize="11sp" />

                    <TextView
                        android:id="@+id/tvSensorType"
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:text="Proximity"
                        android:textColor="#FFFFFF"
                        android:textSize="16sp"
                        android:textStyle="bold"
                        android:layout_marginTop="12dp" />

                </LinearLayout>


                <LinearLayout
                    android:layout_width="0dp"
                    android:layout_height="110dp"
                    android:layout_weight="1"
                    android:orientation="vertical"
                    android:padding="16dp"
                    android:background="@drawable/info_card"
                    android:layout_marginStart="8dp">

                    <TextView
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:text="MAX RANGE"
                        android:textColor="#8991A8"
                        android:textSize="11sp" />

                    <TextView
                        android:id="@+id/tvMaxRange"
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:text="-- cm"
                        android:textColor="#FFFFFF"
                        android:textSize="16sp"
                        android:textStyle="bold"
                        android:layout_marginTop="12dp" />

                </LinearLayout>

            </LinearLayout>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:orientation="horizontal"
                android:gravity="center_vertical"
                android:padding="18dp"
                android:layout_marginTop="16dp"
                android:layout_marginBottom="20dp"
                android:background="@drawable/device_card">

                <TextView
                    android:id="@+id/tvDeviceIndicator"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="●"
                    android:textColor="#6CFF9B"
                    android:textSize="18sp" />

                <LinearLayout
                    android:layout_width="0dp"
                    android:layout_height="wrap_content"
                    android:layout_weight="1"
                    android:orientation="vertical"
                    android:layout_marginStart="12dp">

                    <TextView
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:text="Sensor Manager"
                        android:textColor="#FFFFFF"
                        android:textSize="15sp"
                        android:textStyle="bold" />

                    <TextView
                        android:id="@+id/tvAvailability"
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:text="Proximity sensor available"
                        android:textColor="#8991A8"
                        android:textSize="12sp"
                        android:layout_marginTop="3dp" />

                </LinearLayout>

            </LinearLayout>

        </LinearLayout>

    </ScrollView>

</androidx.constraintlayout.widget.ConstraintLayout>
```

## OUTPUT

### Project Build : 

<img width="1917" height="1078" alt="Screenshot 2026-08-25 082712" src="https://github.com/user-attachments/assets/6501659e-160c-4028-87df-e0b64134b260" />

### Execution / Detecting :

<img width="720" height="1600" alt="image" src="https://github.com/user-attachments/assets/1b7b37ef-dcf7-4264-af67-46cb31d0f39f" />

<img width="720" height="1600" alt="image" src="https://github.com/user-attachments/assets/14f4c7d3-edeb-44fe-9f8c-7b772ed5a9c6" />





## RESULT
Thus a Simple Android Application to display the details of proximity sensor using sensor manager in Android Studio is developed and executed successfully.
