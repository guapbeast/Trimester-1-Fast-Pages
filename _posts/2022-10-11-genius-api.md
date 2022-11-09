---
toc: true
layout: post
description: api
categories: [markdown]
title: RapidAPI
---

<table>
  <thead>
  <tr>
    <th>song</th>
    <th>hits</th>
    <th>hits Abbreviated</th>
    <th>title</th>
  </tr>
  </thead>
  <tbody id="result">
    <!-- generated rows -->
  </tbody>
</table>

<!-- Script is layed out in a sequence (no function) and will execute when page is loaded -->
<script>
  // prepare HTML result container for new output
  const resultContainer = document.getElementById("result");

  // prepare fetch options
  const url = "https://wft-geo-db.p.rapidapi.com/v1/geo/adminDivisions";

const options = {
	method: 'GET',
	headers: {
		'X-RapidAPI-Key': '9d1b75d842msh20486d8bf8d5c19p1904abjsneb2943a9124c',
		'X-RapidAPI-Host': 'genius-song-lyrics1.p.rapidapi.com'
	}
};

  // fetch the API
  fetch(url, options)
    // response is a RESTful "promise" on any successful fetch
    .then(response => {
      // check for response errors
      if (response.status !== 200) {
          const errorMsg = 'Database response error: ' + response.status;
          console.log(errorMsg);
          const tr = document.createElement("tr");
          const td = document.createElement("td");
          td.innerHTML = errorMsg;
          tr.appendChild(td);
          resultContainer.appendChild(tr);
          return;
      }
      // valid response will have json data
      response.json().then(data => {
          console.log(data);

          // hits data
          for (const row of data.data) {
            console.log(row);

            // tr for each row
            const tr = document.createElement("tr");
            // td for each column
            const song = document.createElement("td");
            const hits = document.createElement("td");
            const abbre = document.createElement("td");
            const title = document.createElement("td");

            // data is specific to the API
            song.innerHTML = row.name;
            hits.innerHTML = row.hits; 
            abbre.innerHTML = row.hitsCode; 
            title.innerHTML = row.title; 

            // this build td's into tr
            tr.appendChild(song);
            tr.appendChild(hits);
            tr.appendChild(abbre);
            tr.appendChild(title);

            // add HTML to container
            resultContainer.appendChild(tr);
          }
      })
  })
  // catch fetch errors (ie ACCESS to server blocked)
  .catch(err => {
    console.error(err);
    const tr = document.createElement("tr");
    const td = document.createElement("td");
    td.innerHTML = err;
    tr.appendChild(td);
    resultContainer.appendChild(tr);
  });
</script>