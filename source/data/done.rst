Explore and filter
==================

.. raw:: html

	<head>
	  <script src="https://code.jquery.com/jquery-3.7.1.js"></script>
	  <script src="https://cdn.datatables.net/2.0.7/js/dataTables.js"></script>
	  <link rel="stylesheet" href="https://cdn.datatables.net/2.0.7/css/dataTables.dataTables.css" />
	</head>

	<style>
	.container {
		display: inline-block;
		vertical-align: top;
	}
	.inline-paragraph {
		display: inline;
	}
	</style>


	Below is table with datasets that have been standardized by the <em>Carob</em> project. You can filter by data-providing organization.
	</br></br>

	<div class="container">
		<select id="providerFilter">
			<option value="">All organizations</option>
		</select>
		&nbsp;&nbsp;
		<p class="inline-paragraph", id="txtOutput"></p>
	</div>

	</br>
	</br>
	
	You can use the search box to find data for specific crops and countries. 
	
	  <table id="myTable" class="display" style="width:100%">
		  <thead>
			  <tr>
				  <th>data</th>
			  </tr>
		  </thead>
		  <tbody>
			  <!-- DataTables fills this -->
		  </tbody>
	  </table>


	  <script>

		var organizations = {"name":["AARU","AAU","ABC","ABIO","ABU","AfricaRice","AMDSL","ANU","APNI","ARARI","ARC","ARSU","AUH","BARI","BAU","BIOV","BOKU","BOU","BRRI","BUK","CAAS","CARS","CAU","CIAT","CIMMYT","CIP","CIRAD","CLU","COLSU","CREA","CRS","CSIR","CSSRI","CSUEB","CU","DIMITRA","DRC","EEFRI","EIAR","Embrapa","ENSAT","ESS","ETH","FAO","FENALCE","FOFIFA","FRB","FVAL","GAU","GISS","GIZ","GMOFA","GT","GXU","HARAU","HAU","HCSB","HEBAU","HWU","IAPC","IARI","IASU","IAU","ICAR","ICARDA","ICDF","ICESI","ICRAF","ICRISAT","IDEMS","IER","IFA","IFC","IFPRI","IFZ","IIAM","IITA","ILO","ILRI","ILSU","INAT","INERA","INIFAP","INRAE","INRAMAR","INRAN","IPNI","IRD","IRRI","ISRIC","IWMI","JHU","JIRCAS","JMU","KALRO","KEU","KIOT","KSU","KUDK","KUN","KVC","LFN","LLNL","LUANAR","LUH","Luke","MAFFKH","MAK","MAM","MMOA","MONTSU","MSU","NARC","NARI","NARL","NARO","NCRI","NCSB","NCSU","NDSU","NMBU","OAF","OHSU","OSU","OUAT","PATAZ","PSU","PUADV","PURDUE","RAB","RDRS","ROTH","RRDI","RUA","SAQ","SARC","SARI","SCU","SIU","SLARI","SLU","SNV","SPIA","SSSA","STATS4SD","SUA","SUN","TAID","TAMU","TARI","TCD","TLC","TUAF","UAB","UAKS","UAR","UBKV","UBR","UCB","UCBU","UCD","UCM","UCR","UCANR","UCRC","UED","UFL","UFS","UGHA","UGRE","UGTO","UHel","UHoh","UIA","UIUC","UKY","UM5","UNIMA","UMD","UMELB","UMINN","UMPL","UNAL","UNAM","UNIQ","UNL","UONBI","UOR","UPE","UPS","UQL","URCA","USDA-ARS","USH","USM","UTK","UWM","UWP","UZIM","VT","WB","WHRC","WIU","WUR","WVI","Yale","Yanapai","ZALF","ZARI"],"longname":["Aarhus Universitet","Addis Ababa University","Alliance of Bioversity and International Center for Tropical Agriculture","abacusbio","Ahmadu Bello University","Africa Rice Center","Agencia Mexicana para el Desarrollo Sustentable en Laderas","Australian National University","African Plant Nutrition Institute","Amhara Regional Agricultural Research Institute","Agricultural Research Council of South Africa","Arkansas State University","Agricultural University of Hebei","Bangladesh Agricultural Research Institute","Bangor University","Bioversity International","BOKU University","Boston University","Bangladesh Rice Research Institute","Bayero University Kano","Chinese Academy of Agricultural Sciences","Chitedze Agricultural Research Station","Christian-Albrechts-Universität zu Kiel","International Center for Tropical Agriculture","International Maize and Wheat Improvement Center","International Potato Center","Centre de Coopération Internationale en Recherche Agronomique pour le Développement","Clemson University","Colorado State University","Consiglio per la ricerca in agricoltura e l'analisi dell'economia agraria","Catholic Relief Services","Council for Scientific and Industrial Research","Central Soil Salinity Research Institute","California State University, East Bay","Cornell University","Hellenic Agricultural Organization - DIMITRA","Danish Refugee Council","Ethiopian Environment and Forest Research Institute","Ethiopian Institute of Agricultural Research","Empresa Brasileira de Pesquisa Agropecuária","École Nationale Supérieure Agronomique de Toulouse","Ethiopian Statistics Service","ETH Zürich","Food and Agricultural Orgnization of the United Nations","Federación Nacional de Cultivadores de Cereales, Leguminosas y Soya","Centre National de la Recherche Appliquée au Developpement Rural","Fondation pour la recherche sur la biodiversité","Fundación Valles","Georg-August-Universität Göttingen","Goddard Institute for Space Studies","Deutsche Gesellschaft für Internationale Zusammenarbeit","Ministry of Food and Agriculture, Ghana","Grassroots Trust","Guangxi University","Haramaya University","Chaudhary Charan Singh Haryana Agricultural University","Hoima community seed bank","Hebei Agricultural University","Hawassa University","Institute of Atmospheric Physics, Chinese Academy of Sciences","Indian Agricultural Research Institute","Iowa State University","Islamic Azad University","Indian Council of Agricultural Research","International Center for Agricultural Research in the Dry Areas","International Cooperation and Development Fund","Universidad Icesi","World Agroforestry Center","International Crops Research Institute for the Semi-Arid Tropics","IDEMS International Community Interest Company","Institut d'Economie Rurale","International Fertilizer Association","International Finance Corporatin","International Food Policy Research Institute","Institute of Sugar Beet Research","Instituto de Investigação Agrária de Moçambique","International Institute of Tropical Agriculture","International Labour Organization","International Livestock Research Institute","Illinois State University","Institut National Agronomique de Tunisie","Institut de l'Environnement et de Recherches Agricoles","Instituto Nacional de Investigaciones Forestales Agrícolas y Pecuarias","Institut National de Recherche pour l'Agriculture, l'Alimentation et l'Environnement","Institut National de la Recherche Agronomique du Maroc","Institut National de la Recherche Agronomique du Niger","International Plant Nutrition Institute","Institut de Recherche pour le Développement","International Rice Research Institute","International Soil Reference and Information Centre","International Water Management Institute","James Hutton Institute","Japan International Research Centre for Agricultural Science","Julius-Maximilians-Universität Würzburg","Kenya Agricultural and Livestock Research Organization","Kenyatta University","Karlsruhe Institute of Technology","Kansas State University","Københavns Universitet","Kathmandu University","Kula Vyema Centre","Lao Farmer Network","Lawrence Livermore National Laboratory","Lilongwe University of Agriculture & Natural Resources","Leibniz Universität Hannover","Natural Resources Institute Finland","Ministry of Agriculture, Forestry and Fisheries, Cambodia","Makerere University","Ministère de l'Agriculture du Mali","Malawi Ministry of Agriculture","Montana State University","Michigan State University","Nepal Agricultural Research Council","National Agricultural Research Institute","National Agricultural Research Laboratories","National Agricultural Research Organization","National Cereals Research Institute","Nyando Community seed bank","North Carolina State University","North Dakota State University","Norwegian University of Life Sciences","One Acre Fund","The Ohio State University","Oregon State University","Odisha University of Agriculture and Technology","Asociación Pataz","Pennsylvania State University","Pour une Agriculture du Vivant","Purdue University","Rwanda Agriculture and Animal Resources Development Board","Rangpur Dinajpur Rural Service","Rothamsted Research","Rice Research and Development Institute","Royal University of Agriculture","Sustentabilidad Agropecuario Queretaro","Agricultural Research Council of South Africa","Selian Agricultural Research Institute","Southern Cross University","Southern Illinois University, Carbondale","Sierra Leone Agricultural Research Institute","Sveriges lantbruksuniversitet","SNV Netherlands Development Organisation","Standing Panel on Impact Assessment","Scuola Superiore Sant'Anna","Statistics for Sustainable Development","Sokoine University of Agriculture","Stellenbosch University","Tree AID","Texas A&M University","Tanzania Agricultural Research Institute","Trinity College Dublin","Total Land Care","Thai Nguyen University of Agriculture and Forestry","Universitat Autònoma de Barcelona","University of Arkansas System","University of Arkansas","Uttar Banga Krishi Viswavidyalaya","University of Bristol","University of California, Berkeley","Université Catholique de Bukavu","University of California, Davis","University of California, Merced","University of California, Riverside","University of California Division of Agriculture and Natural Resources","Universidad de Costa Rica","University of Edinburgh","University of Florida","University of the Free State","University of Ghana","University of Greenwich","Universidad de Guanajuato","University of Helsinki","University of Hohenheim","University of Iowa","University of Illinois Urbana-Champaign","University of Kentucky","Mohammed V University","University of Malawi","Univeristy of Maryland","University of Melbourne","University of Minnesota","Université de Montpellier","Universidad Nacional de Colombia","Universidad Nacional Autónoma de México","Unique land use","University of Nebraska, Lincoln","University of Nairobi","University of Oregon","University of Peradeniya","Université Paris-Saclay","University of Queensland","Universidade Regional do Cariri","United States Department of Agriculture, Agricultural Research Service","University of Sheffield","University of Southern Mindanao","University of Tennessee, Knoxville","University of Wisconsin, Madison","University of Wisconsin, Platteville","University of Zimbabwe","Virginia Tech","World Bank","Woodwell Climate Research Center","Western Illinois University","Wageningen University & Research","World Vision International","Yale University","Grupo Yanapai","Leibniz Centre for Agricultural Landscape Research","Zambian Agriculture Research Institute"],"URL":["au.dk","aau.edu.et","alliancebioversityciat.org","abacusbio.com","abu.edu.ng","africarice.org","","anu.edu.au","apni.net","arari.gov.et","arc.agric.za","astate.edu","www.hebau.edu.cn","bari.gov.bd","bangor.ac.uk","alliancebioversityciat.org","boku.ac.at","bu.edu","brri.gov.bd","buk.edu.ng","caas.cn","","uni-kiel.de","alliancebioversityciat.org","cimmyt.org","cipotato.org","cirad.fr","clemson.edu","colostate.edu","crea.gov.it","crs.org","csir.org.gh","cssri.res.in","csueastbay.edu","cornell.edu","elgo.gr","drc.ngo","tss.epa.gov.et","eiar.gov.et","embrapa.br","ensat.fr","ess.gov.et","ethz.ch","fao.org","fenalce.co","fofifa.mg","fondationbiodiversite.fr","fundacionvalles.org","uni-goettingen.de","giss.nasa.gov","giz.de","mofa.gov.gh","grassrootstrust.co.nz","www.gxu.edu.cn","haramaya.edu.et","hau.ernet.in","","hebau.edu.cn","hu.edu.et","iap.cas.cn","iari.res.in","iastate.edu","iau.ir","icar.org.in","icarda.org","icdf.org.tw","icesi.edu.co","cifor-icraf.org","icrisat.org","idems.international","ier.ml","fertilizer.org","","ifpri.org","ifz-goettingen.de","iiam.gov.mz","iita.org","ilo.org","ilri.org","illinoisstate.edu","inat.tn","","gob.mx/inifap","inrae.fr","inra.org.ma","inran.refer.ne","ipni.net","ird.fr","irri.org","isric.org","iwmi.org","hutton.ac.uk","jircas.go.jp","uni-wuerzburg.de","kalro.org","ku.ac.ke","kit.edu","k-state.edu","om.ku.dk","ku.edu.np","kulavyema.org","laofarmers.net","llnl.gov","luanar.ac.mw","uni-hannover.de","luke.fi","maff.gov.kh","mak.ac.ug","ma.gouv.ml","agriculture.gov.mw","montana.edu","msu.edu","narc.org.np","","naro.go.ug/naris/narl","naro.go.ug","ncribadeggi.org.ng","","ncsu.edu","ndsu.edu","nmbu.no","oneacrefund.org","osu.edu","","","asociacionpataz.org.pe","psu.edu","agricultureduvivant.org","purdue.edu","rab.gov.rw","rdrsbangladesh.org",".rothamsted.ac.uk","doa.gov.lk/rrdi_homepage/","rua.edu.kh","facebook.com/SAQac2012/","arc.agric.za","tari.go.tz/centres/tari-selian","","siu.edu","slari.gov.sl","slu.se","snv.org","iaes.cgiar.org/spia","santannapisa.it","stats4sd.org","sua.ac.tz","www.sun.ac.za","treeaid.org","tamu.edu","tari.go.tz","tcd.ie","totallandcare.net","tuaf.edu.vn","uab.cat","uasys.edu","uark.edu","ubkv.ac.in","bristol.ac.uk","berkeley.edu","ucbukavu.ac.cd","ucdavis.edu","ucmerced.edu","ucr.edu","ucanr.edu","ucr.ac.cr","www.ed.ac.uk","ufl.edu","ufs.ac.za","ug.edu.gh","gre.ac.uk","ugto.mx","helsinki.fi","uni-hohenheim.de","uiowa.edu","illinois.edu","uky.edu","um5.ac.ma","unima.ac.mw","umd.edu","unimelb.edu.au","umn.edu","umontpellier.fr","unal.edu.co","unam.mx","unique-landuse.de","unl.edu","uonbi.ac.ke","uoregon.edu","pdn.ac.lk","universite-paris-saclay.fr","uq.edu.au","urca.br","uq.edu.au","sheffield.ac.uk","usm.edu.ph","utk.edu","wisc.edu","uwplatt.edu","www.uz.ac.zw","vt.edu","worldbank.org","woodwellclimate.org","wiu.edu","wur.nl","wvi.org","yale.edu","yanapai.org","zalf.de","zari.gov.zm"],"dataURL":["","","","","","dataverse.harvard.edu/dataverse/AfricaRice","","","","","","","","","","","","","","","","","","dataverse.harvard.edu/dataverse/CIAT","data.cimmyt.org","data.cipotato.org","dataverse.cirad.fr","","","","","","","","","","","","","","","","","","","","","","data.goettingen-research-online.de","","","","","","","","","","","","","","","","data.mel.cgiar.org","","","data.worldagroforestry.org","data.worldagroforestry.org","","","","","dataverse.harvard.edu/dataverse/IFPRI","","","data.iita.org","","data.ilri.org","","","","","entrepot.recherche.data.gouv.fr/dataverse/inrae","","","","dataverse.ird.fr","dataverse.harvard.edu/dataverse/IRRI","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","dataverse.harvard.edu/dataverse/spia","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","","research.wur.nl/en/datasets/","","","","",""],"ROR":["01aj84f44","038b8e254","04xsxqp89","","019apvn83","040y9br29","","019wvm592","","01vwxpj86","04r1s2546","006pyvd89","009fw8j44","01n09m616","006jb1a24","01a15g348","057ff4y42","05qwgg493","01zmzpt10","049pzty39","0313jb750","","04v76ef78","037wny167","04d4vcg59","05asvgp75","05kpkpg04","037s24f05","03k1gpj17","0327f2m07","05xm0ec82","03ad6kn10","0366v8040","04jaeba88","05bnh6r87","0542gd495","04j9qwe36","03k2bxj15","01mhm6x57","0482b5b22","03d5w9863","","05a28rw58","00pe0tf51","","0579ray12","05x5km989","","01y9bpm73","01cyfxe35","00q08t645","056e86068","","02c9qn167","059yk7s89","0261g6j35","","009fw8j44","04r15fz20","0424h4e32","01bzgdw81","04rswrd78","049g0t365","04fw54a43","02n2syw04","","02t54e151","01kmz4383","0541a3n79","00cj7p615","01c5j0443","","049rm1a24","03pxz9p87","01mdqc612","05p3cb968","0556kt608","03tebpn36","01jxjwb74","050kcr883","02zdnfn05","","00r6gdp61","003vg9w96","05y503v71","00rnmt205","05dn5a810","051ykjw41","0593p4448","01z8yfp14","04vpcaw67","03rzp5127","005pdtr14","00fbnyb24","00wawdr98","05p2z3x69","04t3en479","05p1j8758","035b05819","036xnae80","","","041nk4h53","0188qm081","0304hq317","02hb7bm88","","03dmz0111","","","02w0trx84","00yfma824","05aqbwk58","","","044aa1z42","04p4abm19","","04tj63d06","05h1bnb22","04a1mvv97","","00rs6vg23","00ysfqy60","","","04p491231","","05p8z3f47","03nkkb025","","0347fy350","","033dmae14","","04r1s2546","","001xkv632","049kefs16","05xkpwf58","02yy8x990","01a4v4q66","","025602r80","","00jdryp44","05bk57929","","","00h98p168","02tyrky19","","028zxrr95","052g8jq94","05vvhh982","05jbt9m15","02c8fr539","0524sp257","01an7q238","03cg80535","05rrcem69","00d9ah105","03nawhv43","03t0t6y08","02yzgww51","01nrxwf90","02y3ad647","009xwd568","01r22mr83","00bmj0a71","058cjye32","040af2s02","00b1c9541","036jqmy94","047426m28","02k3smh20","00r8w8f84","04vtx5s55","00yfma824","01ej9dk98","017zqws13","051escj72","059yx9a68","01tmp8f25","","043mer456","02y9nww90","0293rh119","025h79t26","03s92mv58","00rqy9422","05y26ar20","02d2m2044","05krs5044","04mtcj695","020f3ap87","01y2jtd41","02xpkhc07","04ze6rb18","02smfhw86","00ae7jd04","04cvvej54","02sshz518","04qw24q55","01s0tbj55","03v76x132","","01ygyzs83","00vz50m28"]}
		$(document).ready(function() {
			var table; 
			const urlParams = new URLSearchParams(window.location.search);
			const pInst = urlParams.get('org');
			//console.log(pInst);

			$.ajax({
				url: "https://carob-data.org/_static/providers.json", 
				dataType: "json", 
				success: function(json) {
					var data = json.data; 

					// Initialize DataTables
					table = $('#myTable').DataTable({
						pageLength: 25,
						language: {	
							"lengthMenu": "Show _MENU_ items",
							"infoFiltered": "" //"(Filtered from _MAX_ records)"
						},
						data: data, 
						columns: [
							{"data": "data_organization", "visible": false, "searchable": true},
							{"data": "dataset"},
							{"data": "project", "visible": false, "searchable": true},
							{"data": "crops", "visible": false, "searchable": true},
							{"data": "countries", "visible": false, "searchable": true}
						]
					});

					// Populate the select dropdown
					var select = $('#providerFilter');
					const uniqueProviders = organizations.name
					// uniqueProviders.sort();
					for (var i = 0; i < uniqueProviders.length; i++) {
						var str = uniqueProviders[i];
						if ((!str.includes(";")) && (str !== "")) {
							select.append('<option value="' + str + '">' + str + '</option>');
						}
					}
					
					const index = organizations.name.indexOf(pInst);
					if (index >= 0) {
						select.val(pInst);
						table.column(0).search("(?<![A-Za-z])" + pInst + "(?![A-Za-z])", true, false).draw();
						$('#txtOutput').html('<a href="https://' + organizations.URL[index] + '">' + organizations.longname[index] + "</a>");
					}
					// console.log(organizations.name); 

				}
			});

			$(document).on('change', '#providerFilter', function() {
				var val = $.fn.dataTable.util.escapeRegex($(this).val());
				const index = organizations.name.indexOf(val);
				if (index >= 0) {
					table.column(0).search("(?<![A-Za-z])" + val + "(?![A-Za-z])", true, false).draw();
					var url = organizations.URL[index];
					if (url == "") {
						$('#txtOutput').text(organizations.longname[index]);   					
					} else {
						$('#txtOutput').html('<a href="https://' + url + '">' + organizations.longname[index] + "</a>");   
					}
				} else {
					table.column(0).search("").draw();
					$('#txtOutput').text("");
				}
			});	
		});

	</script>
	  
