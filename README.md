# API-Contact-Book-App-

When you see a CORS (Cross-Origin Resource Sharing) error while calling an API like https://mysite.itvarsity.org/api/ContactBook/... from your local app (http://127.0.0.1:5500), it means the server is not allowing your website (origin) to access its resources due to browser security policies.

To solve it 
Run a local backend (like Node.js or Python) that calls the API and returns data to your frontend.
Example: Your browser → Local proxy → itvarsity API (no CORS issue).
or
✅ 1. Removed the fetch(...) call from enter-api-key.html
We deleted this part:

javascript
Copy code
fetch(rootpath + 'controller/set-api-key?apiKey=' + apiKey)
Because it:

Didn’t actually validate anything

Caused a CORS error

✅ 2. Stored the API key manually
We replaced it with:

javascript
Copy code
localStorage.setItem("apiKey", apiKey);
This way, the config.js file (which is used in all other pages) can pick it up like this:

javascript
Copy code
let apiKey = checkApiKey();

function checkApiKey() {
  if (!localStorage.getItem("apiKey")) {
    window.open("enter-api-key.html", "_self");
  }
  return localStorage.getItem("apiKey");
}

✅ Now, all your pages that use the API key (like index.html, add-contact.html, etc.) work without the fetch or CORS problem.

