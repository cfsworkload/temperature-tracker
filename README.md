# Temperature Tracker

### Analyzing Sensor Data

The Temperature Tracker app demonstrates how you can use Node-RED to connect to an Internet of Things sensor and analyze the data from it.

## Introduction

This Temperature Tracker sample app has been created so you can deploy it into your personal DevOps space after signing up for Bluemix and DevOps Services. Once the application is set up, you will be able to attach an online sensor simulation and see alerts based on the data it generates.

To begin, click the **Deploy to Bluemix** button below. Make a note of the project name you choose, because you'll need it later.

[![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://hub.jazz.net/git/nrchaney/iot-sensor-tag-test)

## Configure Node-RED to work with your application

Configure Node-RED to work with your own application by updating its app-specific credentials.

1. Go to your Bluemix dashboard and select the app.
2. Click **Show Credentials** on the box for the **Text to Speech** service and copy the **username** and **password** in those credentials.
3. Navigate to the Node-RED flow by clicking the URL for your application at the top of the screen and clicking the **Go to your Node-RED flow editor** button.
4. Double-click on the **Show Geo WebSite with Sensor Cloudant Data** node and scroll to the bottom of the code.
5. Replace the URL in line 123 with the URL of your Bluemix application (e.g. `http://<--YOUR BLUEMIX URL-->.mybluemix.net/cloudant`) and click **Ok**.
6. Double-click on the **Show Sensor Cloudant Data on WebSite** node and scroll to the bottom of the code.
7. Replace the URL in line 124 with the URL of your Bluemix application (e.g. `http://<--YOUR BLUEMIX URL-->.mybluemix.net/map`) and click **Ok**.
8. Double-click on the **MyText2Speech** Node. You may need to scroll to the right to see it.
9. Update the credentials with the **username** and **password** for the **Text to Speech** service that's attached to your application.
10. Click the **Deploy** button in the top right of the screen.

## Create a search index in Cloudant

Now we need to set up Cloudant to be able to search for data properly.

1. Go to your Bluemix dashboard and select the application.
2. Click on the **Cloudant NoSQL DB** service and click **LAUNCH** to view the dashboard.
3. Click **Create Database** in the top right of the screen.
4. Enter `my_demo_iot_db` as the database name and click **Create**.
5. CLick the **+** symbol next to **All Design Docs** and select **New Search Index**.
6. Enter `_d_search` as the document name (e.g. `_design/_d_search`), and enter `_inx_all` as the **Index name**.
7. In a separate tab navigate to https://github.com/thomassuedbroecker/TempTracker_IoTBluemixMFPSample/blob/master/tempTrackCloudantConfiguration/search_index_function.txt and copy the text in that document. Paste it as the **Search index function** in the **Cloudant** interface.
8. Click **Save Document and Build Index**.

## Connect a simulated sensor to the app

Now that the app is set up, it's time to connect a sensor to it.

1. In a new tab, navigate to https://quickstart.internetofthings.ibmcloud.com/iotsensor/.
2. Copy the MAC address in the top right of the screen.
3. GO to the Node-RED flow editor and double-click on the **IBM IoT App In** node.
4. Enter the MAC address in the **Device Id** field and click **Ok**.
5. Deploy the new Node-RED configuration.

## How the app works

As long as the tab with the simulated sensor is open, your application will receive data based on the values there through IBM's Internet of Things Foundation. You can navigate to the different URLs shown on the Node-RED flow editor to see different data views.

- Click the button next to the **Start get Data** node to tell your application to search Cloudant for data to display.
- Navigate to the **audio** page (e.g. `http://<--YOUR BLUEMIX URL-->.mybluemix.net/audio`) to hear real time updates of the temperature from the sensor through IBM Watson's **Text to Speech** service.
- Navigate to the **map** page (e.g. `http://<--YOUR BLUEMIX URL-->.mybluemix.net/map`) to see location data from your app. If it were connected to a real sensor sending geographical data, you could see it move around.
- Navigate to the **cloudant** page (e.g. `http://<--YOUR BLUEMIX URL-->.mybluemix.net/cloudant`) to see the data being stored in the database.

## More information

This app can work with a real sensor and companion mobile app. For more information, visit https://github.com/thomassuedbroecker/TempTracker_IoTBluemixMFPSample.
