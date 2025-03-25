---
tags:
  - utilities
  - windows
  - clipboard
---
When you copy text from a website or an application, it often includes **links, formatting, and other rich content**. However, if you paste it into a simple text editor like **Notepad**, you may lose this extra information.

Windows stores both **plain text** and **HTML-formatted content** in the clipboard, but viewing the rich content requires a different approach.

### 🛠 Extracting HTML Content from the Clipboard

To retrieve the **full HTML content**, you can use **PowerShell** with the following script:

```powershell
Add-Type -AssemblyName System.Windows.Forms
$clipboardData = [System.Windows.Forms.Clipboard]::GetData("HTML Format")

if ($clipboardData) {
    $filePath = "$env:TEMP\clipboard.html"
    $clipboardData | Out-File -Encoding utf8 $filePath
    Write-Output "Clipboard HTML content saved to: $filePath"

    $response = Read-Host "Do you want to open the HTML file now? (Y/N)"
    if ($response -match "^[Yy]$") {
        Start-Process $filePath
    }
} else {
    Write-Output "No HTML content found in the clipboard."
}
```

### 📌 How It Works

1. **Copies the HTML version of the clipboard content** (if available).
2. **Saves it to a file (`clipboard.html`)** for easy viewing.
3. **You can open `clipboard.html` in a browser** to see the full formatted content, including hyperlinks.

This method is useful when copying from **webpages, emails, or formatted documents** and ensures you don’t lose important embedded links or styles.