To-do list
==========

These datasets still need a script. The table is read from the `Carob repository <https://github.com/carob-data/carob>`_ each time this page is opened. The same list is on the `GitHub to-do table <https://carob-data.github.io/carob/>`_.

You can discover other data sets with the `Gardian <https://gardian.cgiar.org>`_ search engine, but do look at our `done list <../data/done.html>`_ before starting to work on a dataset, to make sure that it has not already been processed.

Since there can be a delay in updating what is shown here, before you start working on a dataset, you should check with ``carobiner::on_github`` if it has already been done (and has been added to the github repo).

Difficulty: estimated effort to finish the draft script, from 1 (easy) to 5 (hard), based on its stated completion, open issues and number of data files.

.. raw:: html

   <style>
   .carob-todo { font-size: 13px; }
   .carob-todo .dt-input { font-size: 13px; }
   .carob-todo table.dataTable th,
   .carob-todo table.dataTable td { padding: 4px 8px; }
   </style>
   <p id="todo-status">Loading the to-do list…</p>
   <div class="carob-todo" style="overflow-x:auto">
   <table id="todo-table" class="display" style="width:100%"></table>
   </div>
   <script src="https://code.jquery.com/jquery-3.7.1.js"></script>
   <script src="https://cdn.datatables.net/2.0.7/js/dataTables.js"></script>
   <link rel="stylesheet" href="https://cdn.datatables.net/2.0.7/css/dataTables.dataTables.css" />
   <script src="https://cdn.jsdelivr.net/npm/papaparse@5.4.1/papaparse.min.js"></script>
   <script>
   (function () {
     var CSV = "https://raw.githubusercontent.com/carob-data/carob/main/misc/todo/to-do.csv";
     var REPO = "https://github.com/carob-data/carob/blob/main/";
     function esc(s) {
       return String(s == null ? "" : s).replace(/[&<>"']/g, function (c) {
         return { "&": "&amp;", "<": "&lt;", ">": "&gt;", "\"": "&quot;", "'": "&#39;" }[c];
       });
     }
     function uriHref(t) {
       t = String(t || "").trim();
       if (/^doi:/i.test(t)) return "https://doi.org/" + t.replace(/^doi:\s*/i, "");
       if (/^hdl:/i.test(t)) return "https://hdl.handle.net/" + t.replace(/^hdl:\s*/i, "");
       if (/^https?:\/\//i.test(t)) return t;
       return "";
     }
     function sourceOf(row) {
       var author = String(row.author || "").trim().replace(/,\s*$/, "");
       var year = String(row.year_pub || "").trim();
       if (author && year) return author + " (" + year + ")";
       if (author) return author;
       if (year) return "(" + year + ")";
       return "";
     }
     function scriptHref(path) {
       var p = String(path || "").trim().replace(/\\/g, "/").replace(/^\.\//, "");
       if (!p) return "";
       return REPO + p.split("/").map(encodeURIComponent).join("/");
     }
     function datasetCell(row) {
       var title = String(row.title || "").trim();
       var uri = String(row.uri || "").trim();
       var source = sourceOf(row);
       var html = esc(title);
       var href = uriHref(uri);
       if (href) html += " <a href=\"" + esc(href) + "\" target=\"_blank\" rel=\"noopener\">" + esc(uri) + "</a>";
       else if (uri) html += " " + esc(uri);
       if (source) html += (html ? ". " : "") + esc(source);
       var scriptUrl = scriptHref(row.script);
       if (scriptUrl) html += (html ? ". " : "") + "<a href=\"" + esc(scriptUrl) + "\" target=\"_blank\" rel=\"noopener\">draft script</a>";
       return html;
     }
     function difficultyOf(v) {
       var s = String(v == null ? "" : v).trim();
       if (!s || s === "NA") return "";
       var n = parseInt(s, 10);
       return isFinite(n) ? n : "";
     }
     var status = document.getElementById("todo-status");
     fetch(CSV, { cache: "no-cache" }).then(function (r) {
       if (!r.ok) throw new Error("HTTP " + r.status);
       return r.text();
     }).then(function (text) {
       var parsed = Papa.parse(text.replace(/^\uFEFF/, "").trim(), { header: true, skipEmptyLines: true });
       var rows = (parsed.data || []).filter(function (row) {
         return row && String(row.title || row.uri || "").trim();
       });
       status.textContent = rows.length.toLocaleString() + " datasets";
       new DataTable("#todo-table", {
         data: rows,
         pageLength: 25,
         order: [],
         language: { lengthMenu: "Show _MENU_ items", infoFiltered: "" },
         columns: [
           { title: "Dataset", data: null, render: function (row) { return datasetCell(row); } },
           { title: "Difficulty", data: "difficulty", className: "dt-body-center", render: function (v, type) {
             var n = difficultyOf(v);
             if (type === "sort" || type === "type") return n === "" ? -1 : n;
             return n === "" ? "" : String(n);
           } },
           { title: "Provider", data: "provider", defaultContent: "" },
           { title: "Region", data: "region", defaultContent: "" },
           { title: "Crop", data: "crop", defaultContent: "" },
           { title: "Group", data: "group", defaultContent: "" }
         ]
       });
     }).catch(function (e) {
       status.innerHTML = "Could not load the to-do list (" + esc(e.message) + "). You can open it on <a href=\"https://carob-data.github.io/carob/\">GitHub</a>.";
     });
   })();
   </script>
