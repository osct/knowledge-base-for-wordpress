=============================================
CONFIGURATION amcharts-charts-and-maps plugin
=============================================



**Download:**

https://wordpress.org/plugins/amcharts-charts-and-maps/

Last version https://downloads.wordpress.org/plugin/amcharts-charts-and-maps.1.0.9.zip


**Installation:**

Use WordPress Plugin page to search and install the amCharts plugin.

If you choose to install in manually, make sure all the files from the downloaded archive are placed into your /wp-content/plugins/amcharts/ directory.

**USE**

For create new charts  using presets left from the Admin menu.

Modify resources, HTML and  JavaScript portion of the map. NOT apply defaults value.



**Create "Country View - MAP"**



Resources

::


	http://www.amcharts.com/lib/3/ammap.js
	http://www.amcharts.com/lib/3/maps/js/worldLow.js
	http://www.amcharts.com/lib/3/themes/none.js
	http://www.amcharts.com/lib/3/plugins/dataloader/dataloader.min.js


Html

::


	<div id="%CHART%" style="width: 100%; height: 500px;"></div>
	<div id="placeholder"></div>


JavaScript

::



	var %CHART% = AmCharts.makeChart("%CHART%", {
            
        "type": "map",
        "theme": "none",
        "pathToImages": "http://www.amcharts.com/lib/3/images/",
            
        "dataLoader": {
        "url": "http://grid.ct.infn.it/knowledge-base/api/index.php/countryWP",
        "format": "json",
        "showErrors": true
        },
            
        "areasSettings" : {
        "autoZoom" : false,
        "selectable": true,
        "color" : "#1C6320",
        "colorSolid" : "#EBAD41",
        "selectedColor" : "#EBAD41",
        "outlineColor" : "#FFFFFF",
        "rollOverColor" : "#9DF5A0",
        "rollOverOutlineColor" : "#FFFFFF"
        }
     	}
     	);
            

  	%CHART%.addListener("clickMapObject", function (event) {
        if ( event.mapObject.IdF == null)
        var idf = "Non existent";
        else
        var idf = '<a href="'+ event.mapObject.URL_IdF + '">' + event.mapObject.IdF +'</a>';
            
        if ( event.mapObject.REG == null  || event.mapObject.REG == 'undefined'){
        var REG = "Non existent"; }
        else{
        var splitreg = event.mapObject.REG;
        var REGa = splitreg .split("^");
        var REG = '<a href=' + REGa[1] + '>'+  REGa[0] +'</a>';
            
        }
        if ( event.mapObject.CA == null)
        var CA = "Non existent";
        else
        var CA = '<a href="'+ event.mapObject.URL_CA + '">' + event.mapObject.CA +'</a>';
            
        if ( event.mapObject.NREN == null)
        var NREN = "Non existent";
        else
        var splitnren = event.mapObject.NREN;
        var NRENa = splitnren.split("^");
        var NREN = '<a href=' + NRENa[1] + '>'+  NRENa[0] +'</a>';
            
        if ( event.mapObject.ROC == null || event.mapObject.ROC == 'undefined'){
        var ROC = "Non existent"; }
        else{
        var splitroc = event.mapObject.ROC;
        var ROCa = splitroc.split("^");
        var ROC = '<a href=' + ROCa[1] + '>'+  ROCa[0] +'</a>';
        }
            
        if ( event.mapObject.NGI == null)
        var NGI = "Non existent";
        else
        var NGI = '<a href="'+ event.mapObject.NGI_URL + '">' + event.mapObject.NGI + '</a>';
            
            
        document.getElementById("placeholder").innerHTML =
        '<p><img src=http://grid.ct.infn.it/knowledge-base/api/flags/' + event.mapObject.ISOcode +'.png >' + event.mapObject.title
        + '</p><p><img src=http://grid.ct.infn.it/knowledge-base/api/icons/network_wired.png>Regional Network: ' + REG
        + '</p><p><img src=http://grid.ct.infn.it/knowledge-base/api/icons/wireless.png>National Research Education Network:' + NREN 
        + '</p><p><img src=http://grid.ct.infn.it/knowledge-base/api/icons/ngi.png> National Grid Initiative: ' 
	+ NGI + '</p><p><img src=http://grid.ct.infn.it/knowledge-base/api/icons/ca.png>Certification Authority:' 
	+ CA + '</p><p><img src=http://grid.ct.infn.it/knowledge-base/api/icons/IdF.png>Identity federation: ' 
	+ idf +  '</p><p><img src=http://grid.ct.infn.it/knowledge-base/api/icons/roc.png>Regional Operation Centre(s): ' + ROC + '</p>';
        });
            

**Chart tools**

Use this field to enter a user-friendly slug (ID) for your chart that can be used in shortcodes, i.e. [amcharts id="chart-1"]


**OADR Repositories - MAP**


*Resourses*
::



	http://www.amcharts.com/lib/3/ammap.js
	http://www.amcharts.com/lib/3/maps/js/worldLow.js
	http://www.amcharts.com/lib/3/themes/light.js
	http://www.amcharts.com/lib/3/plugins/dataloader/dataloader.min.js


*Html*
::


	<div id="%CHART%" style="width: 100%; height: 500px;"></div>
	<div id="placeholder"></div>


*JavaScript*

::


	var currentObject;

	var %CHART% = AmCharts.makeChart( "%CHART%", {
  		      "type": "map",
 		      "theme": "light",
  		      "pathToImages": "http://www.amcharts.com/lib/3/images/",
		      imagesSettings: {
		      rollOverColor: "#089282",
		      rollOverScale: 2,
		      selectedScale: 2,
		      selectedColor: "#089282",
                      color:"#13564e"
	              },

                      zoomControl:{buttonFillColor:"#15A892"},
                      areasSettings:{unlistedAreasColor:"#15A892"},
   		      "dataLoader": {
                      "url": "http://grid.ct.infn.it/knowledge-base/api/index.php/oadrWP",
                      "format": "json",
                      "showErrors": true
                      },
  
  
       } );

       %CHART%.addListener("clickMapObject", function (event) {
  		      var repo = event.mapObject.repositories;
  		      var url_repo = event.mapObject.url_repo;
  		      var institution = event.mapObject.institution;
  		      var domain = event.mapObject.domain;
		      var repoSplitResult = repo.split("=");
  		      var urlSplitResult = url_repo.split("=");
  		      var instSplitResult = institution.split("=");  
                      var domainSplitResult = domain.split("=");  
                      var div = document.getElementById('placeholder');
                      var content = "";
                      for(i = 0; i < repoSplitResult.length; i++){
                               content = content +  
                                         '<br><p>Name: ' + '<a href="' + urlSplitResult[i] + '" target=_blank>' 
                                         + repoSplitResult[i] + '</a><br>Domain(s): ' 
                                         + domainSplitResult[i]+'<br>Institution: ' + instSplitResult[i] + '</p>';
		      }
  		      div.innerHTML= '<p>Repository(ies): ' + repoSplitResult.length 
                      + '<br>Country: ' + event.mapObject.country + '<img src=http://grid.ct.infn.it/knowledge-base/api/flags/' 
                      + event.mapObject.id + '.png> '+ '  <br><a href="https://www.google.it/maps/place/' 
                      + event.mapObject.latitude + ',' + event.mapObject.longitude + '" target=_blank> Location </a></p>' + content;

      })

*Chart tools*

Use this field to enter a user-friendly slug (ID) for your chart that can be used in shortcodes, i.e. [amcharts id="chart-1"]


**Dr Repositories - MAP**


*Resourses:*

::



	http://www.amcharts.com/lib/3/ammap.js
	http://www.amcharts.com/lib/3/maps/js/worldLow.js
	http://www.amcharts.com/lib/3/themes/light.js
	http://www.amcharts.com/lib/3/plugins/dataloader/dataloader.min.js


*Html*

::


	<div id="%CHART%" style="width: 100%; height: 500px;"></div>
	<div id="placeholder"></div>

*JavaScript*

::



	var currentObject;
	var %CHART% = AmCharts.makeChart( "%CHART%", {
  		      "type": "map",
  		      "theme": "light",
                      "pathToImages": "http://www.amcharts.com/lib/3/images/",
                      imagesSettings: {
		                     rollOverColor: "#089282",
		                     rollOverScale: 2,
		                     selectedScale: 2,
		                     selectedColor: "#089282",
                                     color:"#13564e"
	              },
		      zoomControl:{buttonFillColor:"#15A892"},
                      areasSettings:{unlistedAreasColor:"#15A892"},
   		      "dataLoader": {
                                    "url": "http://grid.ct.infn.it/knowledge-base/api/index.php/drWP",
                                    "format": "json",
                                    "showErrors": true
                      },
  
  
        });

       %CHART%.addListener("clickMapObject", function (event) {
                      var repo = event.mapObject.repositories;
 		      var url_repo = event.mapObject.url_repo;
                      var institution = event.mapObject.institution;
                      var domain = event.mapObject.domain;
                      var repoSplitResult = repo.split("=");
                      var urlSplitResult = url_repo.split("=");
                      var instSplitResult = institution.split("=");  
                      var domainSplitResult = domain.split("=");  
                      var div = document.getElementById('placeholder');
                      var content = "";
                      for(i = 0; i < repoSplitResult.length; i++){
                      content = content +  '<br><p>Name: ' 
                      + '<a href="' + urlSplitResult[i] + '" target=_blank>' + repoSplitResult[i] 
                      + '</a><br>Domain(s): ' + domainSplitResult[i]
                      +'<br>Institution: ' + instSplitResult[i] + '</p>';
                      }
                     div.innerHTML= '<p>Repository(ies): ' + repoSplitResult.length 
                     +' <br>Country: ' + event.mapObject.country + '<img src=http://grid.ct.infn.it/knowledge-base/api/flags/' 
                     + event.mapObject.id + '.png> '+ '  <br><a href="https://www.google.it/maps/place/' 
                     + event.mapObject.latitude + ',' + event.mapObject.longitude + '" target=_blank> Location </a></p>' + content;

       })


**OER Repositories - MAP**

::


*Resourses*
::


	http://www.amcharts.com/lib/3/ammap.js
	http://www.amcharts.com/lib/3/maps/js/worldLow.js
	http://www.amcharts.com/lib/3/themes/light.js
	http://www.amcharts.com/lib/3/plugins/dataloader/dataloader.min.js


*Html*
::


	<div id="%CHART%" style="width: 100%; height: 500px;"></div>
	<div id="placeholder"></div>


*JavaScript*

::



	var currentObject;
	var %CHART% = AmCharts.makeChart( "%CHART%", {
  		      "type": "map",
                      "theme": "light",
                      "pathToImages": "http://www.amcharts.com/lib/3/images/",
                      imagesSettings: {
		      rollOverColor: "#089282",
		      rollOverScale: 2,
		      selectedScale: 2,
		      selectedColor: "#089282",
                      color:"#13564e"
                      },
		      zoomControl:{buttonFillColor:"#15A892"},
		      areasSettings:{unlistedAreasColor:"#15A892"},
   		      "dataLoader": {
                                    "url": "http://grid.ct.infn.it/knowledge-base/api/index.php/oerWP",
                                    "format": "json",
                                    "showErrors": true
                                    },
	} );

	%CHART%.addListener("clickMapObject", function (event) {
		  var repo = event.mapObject.repositories;
 		  var url_repo = event.mapObject.url_repo;
  		  var institution = event.mapObject.institution;
  		  var domain = event.mapObject.domain;
                  var repoSplitResult = repo.split("=");
                  var urlSplitResult = url_repo.split("=");
                  var instSplitResult = institution.split("=");  
                  var domainSplitResult = domain.split("=");  
                  var div = document.getElementById('placeholder');
                  var content = "";
                  for(i = 0; i < repoSplitResult.length; i++){
                  content = content +  '<br><p>Name: ' + '<a href="' + urlSplitResult[i] 
                  + '" target=_blank>' + repoSplitResult[i] + '</a><br>Domain(s): ' 
                  + domainSplitResult[i]+'<br>Institution: ' + instSplitResult[i] + '</p>';
		  }
                  div.innerHTML= '<p>Repository(ies): ' + repoSplitResult.length +' <br>Country: ' 
                  + event.mapObject.country + '<img src=http://grid.ct.infn.it/knowledge-base/api/flags/' 
                  + event.mapObject.id + '.png> '+ '  <br><a href="https://www.google.it/maps/place/' + event.mapObject.latitude 
                  + ',' + event.mapObject.longitude + '" target=_blank> Location </a></p>' + content;

       })

