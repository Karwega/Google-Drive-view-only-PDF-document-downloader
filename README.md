# Google Drive view-only PDF document downloader
Want to download a PDF document from Google Drive but is restricted to view only? No need to worry! Below are the procedures to follow to achieve your goal.

1. Make sure to use a web browser, most preferably, Google Chrome, and locate the document.
2. Open the document using the online Google Drive PDF viewer. The URL in the address bar should read something like "https://drive.google.com/file/d/Pd35K3r....."
3. Scroll to the last page of the document.
4. Open the developer mode of the browser. For Windows, you can do this using the keyboard shortcut **Ctrl + Shift + C**. For Mac, you can do this using the keyboard shortcut **Cmd + Shift + C**.
5. Click on the **Console** tab as shown <img width="414" alt="console" src="https://github.com/Karwega/Google-Drive-view-only-PDF-document-downloader/assets/130556507/dd0f2293-7467-4411-a6cf-bb833fff5d6b">

6. Paste the code below and hit **Enter** on your keyboard.
   ```
   let jspdf = document.createElement("script");
   jspdf.onload = function () {
   let pdf = new jsPDF();
   let elements = document.getElementsByTagName("img");
   for (let i in elements) {
   let img = elements[i];
   console.log("add img ", img);
   if (!/^blob:/.test(img.src)) {
   console.log("invalid src");
   continue;
   }
   let can = document.createElement('canvas');
   let con = can.getContext("2d");
   can.width = img.width;
   can.height = img.height;
   con.drawImage(img, 0, 0, img.width, img.height);
   let imgData = can.toDataURL("image/jpeg", 1.0);
   pdf.addImage(imgData, 'JPEG', 0, 0);
   pdf.addPage();
   }
   pdf.save("download.pdf");
   };
   jspdf.src = 'https://cdnjs.cloudflare.com/ajax/libs/jspdf/1.5.3/jspdf.debug.js';
   document.body.appendChild(jspdf);

The code should run and the document should be downloaded as a PDF to your local computer successfully!

