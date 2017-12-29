GIS WEB APPLICATION

How the Web App works:-

Basically, the app initially displays a map, file browser and 2 buttons(KML, Raster). When you get a file from file browser, if the file is in kml format, you click the kml button and on the map we see the kml layer else if the file is of geotiff format, then you click the raster button and the raster layer is displayed on the map.
There are two types of APIs used to develop the app:- Google Maps API and OpenLayers API.
  
Language used: Django

JS Files Used:-
    
For KML to work:
  1. geoxml3.js
  2. ProjectedOverlay.js

For Raster layer to work:
  1. ol.js
  2. lz-string.js
  3. ol3map.js ( changes made: element ID changed from 'map' to 'map-canvas')
  4. ol3geotiff.js
  5. testGeotiffParser.js
  6. GeotiffParser.js
  7. geotiff.js
  8. plotty.js/plotty.min.js
  9. require.js

JS files to be stored( Based on Anaconda3 installed ):- 
  >> ~/anaconda3/lib/python3.6/site-packages/Django-2.1.dev20171205201120-py3.6.egg/django/contrib/admin/static/admin/js

JS files used for KML supports the feature to load kml from offline kml files. 
JS files used for Geotiff(Raster Layer) is to display raster data in the form of .tif format in local storage.

Steps to get the Web App to work:-
1. traversing to the project.
2. Type in command line:

	>> python manage.py runserver
  
This command will start the server with the URL : 
127.0.0.1:8000/gmap

gmap being the application name.

Integration steps with Django:-
App name in Django project: gmap

In gmap/views.py:

    def index(request):
        return render(request,'map_1.html')

map_1.html has the template of extension to the main page (basemap.html) and also loads static files.

In gmap/urls.py:

    urlpatterns =[
        path('', views.index, name='index'),
    ] 
    urlpatterns += staticfiles_urlpatterns()

In this code, the index function in views.py is added to the list of urls you would want to add to the application.
staticfiles_urlpatterns() is added to link the static files( having all the js scripts).

In the project's urls.py:

    urlpatterns = [
        path('gmap/', include('gmap.urls')),
        path('admin/', admin.site.urls)
    ]

In this code, initially admin page has been already added and the gmap application is added so that we can access 127.0.0.1:8000/gmap page.

Support for static/dynamic KML:-
As explained, local KML files can be loaded using file broser. Offline KML is enabled by extracting the data in the kml file and being parsed by a function in geoxml3.js script.

Dynamic KML: Not tested but if the changes are being made in the local kml, then if the page is refreshed, it will work.

Static KML: It will work.

Support Raster Layer:-
Raster Layer made is working on Apache but not working in Django. The layer is shown but as we zoom in, it changes the place of display. I have added a ‘project’ folder which contains an html page and all required javascript files for the working of geotiff part. This folder can be added to the Apache html folder.
I have commented the Apache localhost webpage opening so that if you want the correct output of Raster layer in Apache, you can uncomment the line. Note:- It's not made working for KML, just a prototype for Geotiff display.
