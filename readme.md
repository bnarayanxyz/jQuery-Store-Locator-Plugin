# [jQuery Google Maps Store Locator Plugin](http://www.bjornblog.com/web/jquery-store-locator-plugin)

### [Please see my blog for more information and examples](http://www.bjornblog.com/web/jquery-store-locator-plugin).

This jQuery plugin takes advantage of Google Maps API version 3 to create an easy to implement store locator. No back-end programming is required, you just need to feed it KML, XML, or JSON data with all the location information. How you create the data file is up to you. I originally created this for a company that didn’t have many locations, so I just used a static XML file. I also decided to geocode all the locations beforehand, to make sure it was quick and to avoid any potential geocoding errors. However, if you’re familiar with JavaScript you could easily make a modification to geocode everything on the fly (I may add this as an option at some point). 

A note on the distance calculation: this plugin currently uses a distance function that was originally programmed by [Chris Pietschmann](http://pietschsoft.com/post/2008/02/01/Calculate-Distance-Between-Geocodes-in-C-and-JavaScript.aspx). Google Maps API version 3 does include a distance calculation service ([Google Distance Matrix API](http://code.google.com/apis/maps/documentation/distancematrix/)) but I decided not to use it because of the current request limits, which seem somewhat low. In addition, because the plugin currently calculates each location’s distance one by one, it appeared that I would have to re-structure some things to make all the distance calculations at once (or risk making many request for one location lookup). So, the distance calculation is “as the crow flies” instead of a road distance.

## Changelog

### Version 1.4

This is a large update that has many updates and improvements. It’s very important to note that the plugin now requires the [Handlebars](http://handlebarsjs.com) template engine. I made this change so that the data that’s displayed in the location list and the infowindows can be easily customized. I also wanted to separate the bulk of the layout additions from the main plugin file. Handlebars pretty slick, will read Mustache templates, and the built-in helpers can really come in handy. Depending on what your data source is, 2 of the 4 total templates will be used (KML vs XML or JSON) and there are options to set the paths of each template if you don’t want them in the default location. If you’re developing something for mobile devices the templates can be pre-compiled for even faster loading. Additionally, I’d also like to note that it probably makes more sense to use KML now as the data source over the other options but I’m definitely leaving XML and JSON support in. XML is still the default datatype but I may switch it to KML in the future.

####New features:####

**Kilometers option**  
This was a no-brainer. You could make the change without too much trouble before but I thought I’d make it easier for the rest of the world.

**Origin marker option**  
If you’d like to show the origin point, the originMarker option should be set to true. The default color is blue but you can also change that with the originpinColor option. I’m actually not positive how many colors Google has available but I know red, green and blue work - I would just try the color you want to see if it works.

**KML support**  
Another obvious add-on. If you’d like to use this plugin with more customized data this would be the method I’d recommend because the templates are simplified to just name and description. So, you could put anything in the descriptions and not have to worry about line by line formatting. This method also allows you to create a map with Google “My Maps” and export the KML for use with this plugin. 

**Better JSONP support and 5 callbacks**  
Thanks to “Blackout” for passing these additions on. It should make working with JSONP easier and the callbacks should be helpful for anyone wanting to hook in add some more advanced customization. 

**ASP.net WebForms support**  
If you’re woking with ASP.net WebForms, including form tags is obviously going to cause some problems. If you’re in this situation simply set the new noForm option to true and make sure the formContainerDiv setting matches your template.

**Maximum distance option**  
You can now easily add a distance dropdown with any options that you’d like. I’ve specifically added a new HTML file as an example. 

**Location limit now supports any number**  
This plugin was previously limited to only display a maximum of 26 locations at one time (based on the English alphabet). You can now set the limit to whatever you’d like and if there are more than 26 it will switch to just show dot markers with numbers in the location list.

**Open with a full map of all locations**  
I had several requests asking how to accomplish this so I’ve added it as an option. There’s a new fullMapStart option that if set to true, will immediately display a map with all locations and the zoom will automatically fit all the markers and center.

**Reciprocal focus**  
“JO” was particularly interested in adding this to the plugin and I finally got around to it. To accomplish reciprocal focus I add an ID to each marker and then add that same ID to each list element in the location list taking advantage of [HTML5’s new data- attributes](http://ejohn.org/blog/html-5-data-attributes). I also added some jQuery to make the location list scroll to the correct position when its marker is clicked on the map. 

**Notes:**

A few option names have changed, so be sure to take note of the changes before updating your files - especially people using JSON data.

I've included a basic [LESS](http://lesscss.org) stylesheet without variables that can be used in place of the main map.css stylesheet. If you want to use it make any changes you want and compile it or include it in your main LESS file.

I’m somewhat concerned about the markers for future versions. Google has deprecated the Image Charts API, which is annoying (they always seem to deprecate the best things), but these should still continue to work for a long time. With that said though, my opinion of the look of Google’s markers is that they’re quite ugly. I was working on adding a new custom markers that could be controlled with CSS via the [Rich Marker utility](http://google-maps-utility-library-v3.googlecode.com/svn/trunk/richmarker/examples/richmarker.html) but I was unable to get that to work with the marker animations. I was also looking into using [Nicolas Mollet’s custom marker icons](http://mapicons.nicolasmollet.com), which look very nice compared to Google’s, but that project is apparently under maintenance until further notice. If you have suggestions on this concern I’d be interested in hearing them.

### Version 1.3.3

Forgot to remove one of the UTF-8 encoding lines in the Geocoder function. 

### Version 1.3.2

Only a few special characters were working with the previous fix. Removed special encoding and all seem to be working now.

### Version 1.3.1

Replaced .serialize with .val on line 169 and added the line directly below, which encodes the string in UTF-8. This should solve special character issues with international addresses. 

### Version 1.3

Added directions links to left column location list and HTML5 geolocation API option. Also did a little cleanup.

### Version 1.2

Added JSON compatibility, distance to location list, and an option for a default location. Also updated jQuery calls to the latest version (1.7.2) and removed an unnecessary line in the process form input function.

### Version 1.1.3

Serlialize was targeting any form on the page instead of the specific formID. Thanks to Scott for pointing it out.

### Version 1.1.2

Changed it so that the processing stops if the user input is blank.

### Version 1.1.1

Added a modal window option. Set slideMap to false and modalWindow to true to use it. Also started using the new [jQuery .on() event api](http://blog.jquery.com/2011/11/03/jquery-1-7-released/) - make sure you're using jQuery v1.7+ or this won't work.

### Version 1.0.1

Left a couple of console.logs in my code, which was causing IE to hang.

### Version 1.0

This is my first jQuery plugin and the first time I’ve published anything on Github. Let me know if I can improve something or if I’m making some kind of mistake. 