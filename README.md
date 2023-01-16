# Querying Companies House API via JavaScript Fetch
The official documentation for the **Companies House API** is limited at best.

It can take literally hours of scouring:

 - the [Companies House Developer Hub](https://developer.company-information.service.gov.uk/)
 - the [Companies House Developer Forum](https://forum.aws.chdev.org/)
 - the wider web (e.g. [How to use OpenCorporates and Companies House APIs](https://carmen-aguilar-garcia.medium.com/how-to-use-opencorporates-and-companies-house-apis-79ba0647d0d0) by Carmen Aguilar García)

to accrue enough information to figure out how to write the JavaScript to query the API correctly. (The forum contains many answers regarding how to query the API correctly, but some answers are for **cURL**, others for **PHP**, others for **Python**, so it's time-consuming if you only want to find a cut-and-paste *how-to* in **JavaScript**. 

This repo contains a series of working JavaScript snippets to save others time and frustration in future.
_________

## #1 Get Company Profile (from Company Registration No.)

**N.B.** *Vital information which appears to be missing from the **Companies House Developer Hub**:*

After you have:
 - Signed In
 - Created an application *and*
 - Created an API Key for that Application
 
 you *must*:

- Add the domain from which you intend to initiate the `fetch()` request to... the **JavaScript Domains** field of the **API Key Interface**


Once you have completed all these steps, you can run the following JavaScript on a page hosted on the domain you have stated above:

```js

async function getCompanyProfile(companyNo) {

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

  const displayOutput = document.createElement('pre');
  displayOutput.textContent = JSON.stringify(JSON.parse(response), undefined, 2);
  document.body.appendChild(displayOutput);
}

getCompanyProfile('09090909'); // <= MUST BE A STRING, CONTAINING 8 DIGITS

```
