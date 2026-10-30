Data
====


.. raw:: html
   :file: ../_R/compiled.html


.. raw:: html

	<h3>Download</h3>
    <embed>
	<label for="data-select">group:</label>
	<select name="data-select" id="data-select">
		<option value=""></option>
		<option value="agronomy">agronomy</option>
		<option value="pest_disease">pest_disease</option>
		<option value="soil_samples">soil_samples</option>
		<option value="survey">survey</option>
		<option value="varieties_cassava">varieties_cassava</option>
		<option value="varieties_cowpea">varieties_cowpea</option>
		<option value="varieties_maize">varieties_maize</option>
		<option value="varieties_potato">varieties_potato</option>
		<option value="varieties_sorghum">varieties_sorghum</option>
		<option value="varieties_wheat">varieties_wheat</option>
		<option value="varieties_other">varieties_other</option>
		<option value="weather">weather</option>
		<option value="all">everything</option>
	</select>

	</br></br>	
   
	<div><input type="radio" id="format_csv" name="format" value="csv" checked>.csv (Comma Separated Values)</div>
	<div id="hideMe">
		<div><input type="radio" id="format_xls" name="format" value="xls">.xlsx (Excel)</div>
	</div>


	</br>
	
	<button onclick = "make_link()">OK</button> 
	<p> 
	  <div id = "prog">
	  <progress hidden="hidden" id="progress" max="100" value="0"></progress>
	  </div>
      <div id = "result">&nbsp;</div> 
	</p> 

	<script> 

		const hideMeDiv = document.getElementById('hideMe');
	    const selectElement = document.getElementById("data-select");
	

		function rb() { 
			document.getElementById("result").innerHTML = "";
			//const radioxls = document.getElementById('format_xls');
			if (selectElement.value == "all") {
				//radioxls.style.display = 'none';
				hideMeDiv.style.display = 'none';
				document.getElementById('format_csv').checked = true;
			} else {
				//radioxls.style.display = 'inline';
				hideMeDiv.style.display = '';
			}
		}
		
		selectElement.addEventListener("change", function() {
			rb()
		});
		const radios = document.getElementsByName('format');
		radios[0].addEventListener("change", function() { rb() });
		radios[1].addEventListener("change", function() { rb() });
	

		function move(i, name) {
			var id = document.getElementById("progress"); 
			if (i < 100) {
				id.value=i;
				i++;
				setTimeout(function() { move(i, name) }, 10);
			} else {
				id.value=0;
				id.setAttribute("hidden", "hidden");
				//if (document.getElementById('cclicense').checked) {
				//}
				name = name.concat("_latest-CC");
				var linktxt = 'Download: <a href="https://geodata.ucdavis.edu/carob/carob_';
				if (document.getElementById("format_csv").checked) {
					linktxt = linktxt.concat(name.toLowerCase()).concat('.zip">');
					name = name.concat(".zip");
				} else {
					linktxt = linktxt.concat(name.toLowerCase()).concat('.xlsx">');				
					name = name.concat(".xlsx");
				}
				linktxt = linktxt.concat(name).concat('</a>');
				document.getElementById("result").innerHTML = linktxt;
			}
		}
		
		function make_link() { 
			var e = document.getElementById("data-select");
			var value = e.value;
			var text = e.options[e.selectedIndex].value;
			if (text == "") {
				document.getElementById("result").innerHTML = "Choose a group";
			} else { // if (document.getElementById('license').checked) {
				document.getElementById("result").innerHTML = "processing";
				var pid = document.getElementById("progress"); 
				pid.removeAttribute("hidden");
				setTimeout(move(0, text), 1000); 
			}
			/*
			} else {
				document.getElementById("result").innerHTML = "You must accept the licenses";
			}
			*/
		} 	
	</script>
    </embed>



.. toctree::
	:hidden:
	:maxdepth: 2
	
	done
