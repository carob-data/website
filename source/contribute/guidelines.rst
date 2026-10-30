Guidelines
==========

Before you start
----------------

.. raw:: html

	<!--- <style>	li { margin-bottom: 1rem; } </style> --->

	<ul>
	<li>Anyone is welcome to contribute to <em>Carob</em>. It is not easy to standardize research data. Please try your best to follow the guidelines provided here. But we won’t get angry if you make mistakes — as long as you are willing to learn from them.</li></br>

	<li>When looking at a dataset you want to process, first carefully read the description provided. If there is a related publication, read the abstract and scan the Methods section. The Methods section often provides data for (constant) management variables that are not treatments. For example, if all treatments received the same amount of fertilizer, these numbers are frequently omitted from the dataset.</li></br>

	<li>Consider what the data are about. With experimental data ask: “what are the treatments”, “how are they captured”, “what are the important response variables”? All treatments (factors) must be included as one or more standard variables. There is a variable called “treatment” that may have a combination of treatments (e.g., “NP”, “PK”, but they must also be specified in separate variables such as “N_fertilizer” and “P_fertilizer”. This seems obvious, but in many datasets the treatments are not explicitly provided as variables, and you may need to do some work. For example you may need to translate a treatment code into multiple variables.</li></br>

	<li>To contribute to *Carob* you need to clone the carob git repo and install the “carobiner” R package. You can do that with <code>remotes::install_github("carob-data/carobiner")</code>. The package contains helper functions for data processing, and functions that check for compliance with the standard. It depends on two other packages, <em>yuri</em> and <em>vocal</em> that will be automatically installed as well (or else you will be prompted to do so).</li></br>

	<li>When writing a new script, start by running the carobiner::draft` function for your dataset of interest.</li></br> 
	
	<li>If you are using AI, see <a href="./ai.html">Using AI</a>. Tell the agent to read <a href="https://github.com/carob-data/carob/blob/main/AGENTS.md">AGENTS.md</a> (in the root of the repo). AI can be very helpful, but it cuts corners and requires supervision. You need to critically evaluate their work and push them to do better (or fix things yourself).</li></br> 

	<li><em>Carob</em> scripts are normally contributed and/or improved via a github pull request (PR). Before creating a pull request, make sure that your fork is synced, and that there are no conflicts. We strongly prefer PRs for a single file at a time.</li></br>
	</ul>


Scripts
-------

.. raw:: html

	<ul>
	</li></br>
	<li>Carob scripts download and re-organize data to make them standard compliant, and they save the standardized data and relevant metadata on disk. See <a href="https://github.com/carob-data/carob/blob/main/scripts/_template.R">template.R</a> in the *scripts* folder for the general structure of such a script.</li></br>

	<li>All original data should be downloaded from a URI (uniform resource identifier) such as a DOI or HDL. For example <code>"doi:10.7910/DVN/UNLRGC"</code> is a valid URI. It is important to use this specific notation, do *not* use a http address such as </code>https://doi.org/10.7910/DVN/UNLRGC</code>. Data that does not have a URI but does have a URL (Internet address) can also be used. Data that can not be downloaded from the Internet should be hosted somewhere. We can host it on the <a href="https://dataverse.harvard.edu/dataverse/carob/">carob dataverse</a>. We can make exceptions for especially valuable datasets that cannot be (easily) downloaded directly.</li></br>

	<li>Each original dataset gets its own script. The script file should be <code><nuri>.R</code> where <</code>nuri</code>> is a normalized URI. That is, a URI without a colon or slashes. You can create these with <code>carobiner::simple_uri</code>. For example, <code>carobiner::simple_uri("doi:10.7910/DVN/UNLRGC")</code> returns <code>"doi_10.7910_DVN_UNLRGC"</code> and filename for the script should be <code>"doi_10.7910_DVN_UNLRGC.R"</code></li></br>

	<li>Scripts and data are grouped by domain. These groups are “agronomy”, “survey”, “soil_samples“ and “varieties_*”. Take the one that seems most appropriate. Group membership can be somewhat arbitrary as they are partly overlapping. That is not a problem as the aggregated data may include records from multiple groups.</li></br>

	<li>Test your script. The last line in a script should always be <code>carobiner::write_files</code>. This function checks whether you are using the controlled vocabulary, among other things. Fix any errors or warnings to the extent possible (without guessing things you do not know or suppressing warnings). It is OK to leave some warnings if you believe they cannot be fixed by you (perhaps because the controlled vocabulary needs to be expanded). You can also use <code>carobiner::check_terms</code> to evaluate compliance with the standard.</li></br>

	<li>If a dataset is associated with a publication, you can often get important additional information from the Methods section (for example, on location, fertilizer used, plant spacing). If you get values from a related publication, or because of your reasoning, document where you got these values by adding comments in the script.</li>
	<ul>


Standardization
---------------

.. raw:: html

	<ul>
	</li></br>
	<li>The aim is to standardize all relevant variables in the original data. We generally omit variables that are measured in the field to compute a variable of interest, but are not of much interest themselves. For example, we include yield (kg/ha), but not the mass of a sample that was taken to estimate it.</li></br>

	<li>We use the <a href="https://controvoc.github.io/terminag/">terminag</a> vocabulary. If you think that there are terms (concepts) or accepted values that are missing in this standard, just add/keep these in your script and ignore the warning messages. An editor will look at your pull-request (PR) and decide whether the standard needs to be expanded or changed.</li></br>

	<li>It is expected that there is variation between data sets; they do not all have the same variables. But all records should have common variables such as country, crop, yield, longitude and latitude (even if some of their values are missing (<code>NA</code>))</li></br>

	<li>Some variables such as <code>country</code>, <code>crop</code>, and <code>fertilizer_type</code> have controlled vocabularies that you need to use (or suggest adding additional terms). If there are multiple values (for example, two crops or fertilizer types), separate these with a semi-colon (<code>;</code>).</li></br>

	<li>Apart from the standard variable names you also need to express all data in standard units. See the  <a href="https://controvoc.github.io/terminag/">terminag variables</a>.</li></br>

	<li>Check character variables for spelling variations (use <code>unique</code> and <code>table</code>) and standardize. You can use <code>carobiner::fix_name</code> in some cases.</li></br>

	<li>Make sure that variables that should be numeric are not stored as text</li></br>

	<li>Do not guess values to make things work (for example, because a value is required, or because it needs to match a vocabulary). Instead, submit the script with warnings/errors so that we can discuss the best way to handle these.</li></br>

	<li>Store dates as text after first creating dates (<code>as.character(as.Date(x))</code>) so that they are in a standard format. You can also store years (e.g., “2023” or year-months such as “2023-06” if that is all the available information.</li></br>

	<li>All experimental treatment variables need to be included. These variables should also be specified at the dataset level under “treatment_vars”</li>
	
	<li>It is very important that locations are correctly georeferenced. You can use Google Maps and other on-line tools for that. Location names are often common, so make sure that you consider all the information you have (location names, admin subdivision) and check geographic outliers. In R, you can inspect the longitude/latitude locations with 
	<code>terra::plet(terra::vect(d))</code></li>.

	</ul>


R coding style
--------------

.. raw:: html

	<ul>
	</li></br>
	<li>We rely as much as we can on base <em>R</em> to keep code simple and dependencies low.</li></br>

	<li>We do *not* use the "tidyverse" dialect.</li></br>

	<li>To make it easy to read and debug a script, avoid or sparingly use <code>|></code>. Never use more than 2 in one statement.</li></br>

	<li>Avoid nesting function calls. Do not nest more than 2 function calls. For example, instead of nested <code>ifelse</code> calls, use <code>%in%</code>, <code>match</code> or <code>merge</code>.</li></br>

	<li>When using <code>ifelse</code> do not use a default last condition for a known case (unless it is obvious). Instead, use <code>NA</code> as the default for all other, unexpected, conditions). Do not indent nested <code>ifelse</code> statements.</li></br>

	<li><bold># comment your code</bolde>. Document your assumptions. Document where you got numbers introduced in the script (from a publication, for example) Comments start on the line above the code that is commented on (not on the same line)</li>

	</ul>


*Carob* is under active development. To stay current, you should frequently pull the *Carob* repo and update the carobiner package.


