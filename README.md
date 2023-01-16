# Querying Companies House API via JavaScript Fetch
The documentation for the **Companies House API** is limited at best.

It can take literally hours to figure out how to write the JavaScript to query the API correctly.

This repo contains a series of working JavaScript snippets to save others time and frustration in future.

```js

async function queryCompaniesHouseAPI(companyNo) {

  const pre = document.querySelector('pre');

  const apiKey = [/* API KEY HERE */];
  const apiURL = 'https://api.companieshouse.gov.uk/company/';
  const queryURL = apiURL + companyNo;
  
  const headers = new Headers ({
    'Authorization': 'Basic ' + btoa(apiKey + ':'),
    'Content-Type': 'text/json'
  });
  
  const dataObject = {
    method: 'GET',
    headers: headers
  };
  
  const companiesHouseAPIResponse = await fetch(queryURL, dataObject);
  const response = await companiesHouseAPIResponse.text();

  pre.textContent = JSON.stringify(JSON.parse(response), undefined, 2);
}

queryCompaniesHouseAPI('09090909'); // <= MUST BE A STRING, CONTAINING 8 DIGITS

```
