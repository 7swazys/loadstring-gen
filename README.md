# loadstring-gen
roblox loadstring gen for lazy ppl
html version
<details>
  <summary>Click to expand!</summary>
  ``lua
    <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Loadstring Converter · Raw URL to Roblox Executor String</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(145deg, #0a0f1e 0%, #0c1222 100%);
            font-family: 'Inter', system-ui, -apple-system, 'Segoe UI', 'Fira Code', monospace;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 1.5rem;
        }

        /* modern glassmorphic card */
        .glass-card {
            max-width: 1100px;
            width: 100%;
            background: rgba(18, 25, 45, 0.75);
            backdrop-filter: blur(14px);
            border-radius: 2.5rem;
            border: 1px solid rgba(72, 187, 255, 0.25);
            box-shadow: 0 25px 45px -12px rgba(0, 0, 0, 0.6), 0 0 0 1px rgba(56, 189, 248, 0.1);
            overflow: hidden;
            transition: all 0.2s ease;
        }

        /* header area */
        .header {
            padding: 1.75rem 2rem;
            background: rgba(12, 18, 34, 0.7);
            border-bottom: 1px solid rgba(56, 189, 248, 0.3);
        }

        .header h1 {
            font-size: 1.9rem;
            font-weight: 600;
            background: linear-gradient(135deg, #c0e0ff, #3b82f6);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
            letter-spacing: -0.3px;
            display: inline-flex;
            align-items: center;
            gap: 12px;
        }

        .header h1::before {
            content: "⚡";
            font-size: 2rem;
            background: none;
            background-clip: unset;
            -webkit-background-clip: unset;
            color: #3b82f6;
        }

        .sub {
            color: #9ab3d5;
            margin-top: 0.5rem;
            font-size: 0.9rem;
            border-left: 3px solid #3b82f6;
            padding-left: 0.85rem;
            font-family: monospace;
        }

        /* main content */
        .content {
            padding: 2rem;
        }

        .input-group {
            margin-bottom: 1.8rem;
        }

        label {
            display: flex;
            align-items: center;
            gap: 10px;
            font-weight: 500;
            color: #cfdfff;
            margin-bottom: 0.6rem;
            font-size: 0.9rem;
            letter-spacing: 0.3px;
        }

        label i {
            font-style: normal;
            font-size: 1.2rem;
        }

        .url-input-wrapper {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
        }

        input {
            flex: 1;
            background: #0f1422;
            border: 1.5px solid #26324a;
            border-radius: 1.25rem;
            padding: 0.9rem 1.2rem;
            color: #eef4ff;
            font-family: 'Fira Code', monospace;
            font-size: 0.9rem;
            transition: all 0.2s;
            outline: none;
        }

        input:focus {
            border-color: #3b82f6;
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.3);
            background: #0b1020;
        }

        input::placeholder {
            color: #4c5a7a;
            font-family: monospace;
            font-size: 0.85rem;
        }

        button {
            background: linear-gradient(100deg, #2563eb, #1e40af);
            border: none;
            padding: 0 1.8rem;
            border-radius: 1.5rem;
            font-weight: 600;
            color: white;
            font-family: inherit;
            font-size: 0.9rem;
            cursor: pointer;
            transition: transform 0.1s, background 0.2s;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            box-shadow: 0 4px 10px rgba(37, 99, 235, 0.3);
        }

        button:hover {
            background: linear-gradient(100deg, #3b82f6, #1e3a8a);
            transform: scale(0.98);
        }

        button:active {
            transform: scale(0.96);
        }

        /* result panels */
        .result-section {
            margin-top: 2rem;
            background: rgba(0, 0, 0, 0.35);
            border-radius: 1.5rem;
            padding: 0.2rem;
            border: 1px solid rgba(59, 130, 246, 0.3);
        }

        .panel-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 1.5rem;
            background: rgba(20, 28, 45, 0.7);
            border-radius: 1.5rem 1.5rem 0 0;
            border-bottom: 1px solid #26324a;
            flex-wrap: wrap;
            gap: 12px;
        }

        .panel-header h3 {
            font-size: 1rem;
            font-weight: 500;
            color: #8caee0;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .copy-btn {
            background: #1e293b;
            padding: 0.4rem 1rem;
            border-radius: 2rem;
            font-size: 0.75rem;
            font-weight: 500;
            box-shadow: none;
            gap: 6px;
        }

        .copy-btn:hover {
            background: #2d3a5e;
            transform: none;
        }

        pre {
            background: #070b14;
            padding: 1.5rem;
            overflow-x: auto;
            font-family: 'Fira Code', 'Cascadia Code', monospace;
            font-size: 0.85rem;
            line-height: 1.5;
            color: #b9e2ff;
            border-radius: 0 0 1.2rem 1.2rem;
            white-space: pre-wrap;
            word-break: break-word;
            tab-size: 4;
            margin: 0;
            border-top: 1px solid #1e2a3e;
        }

        .status-message {
            margin-top: 1.2rem;
            font-size: 0.8rem;
            padding: 0.5rem 1rem;
            border-radius: 1rem;
            background: rgba(0, 0, 0, 0.4);
            display: inline-block;
            color: #7f9fcf;
        }

        .error-message {
            color: #ffaeae;
            background: rgba(220, 38, 38, 0.2);
            border-left: 3px solid #ef4444;
        }

        .success-message {
            color: #b2ffcf;
            background: rgba(34, 197, 94, 0.15);
            border-left: 3px solid #22c55e;
        }

        .example-row {
            margin-top: 1.2rem;
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            align-items: center;
            justify-content: space-between;
        }

        .example-badge {
            font-size: 0.75rem;
            background: #111827;
            padding: 0.3rem 0.8rem;
            border-radius: 2rem;
            color: #7aa9ff;
            cursor: pointer;
            transition: all 0.1s;
            border: 1px solid #2a3a60;
        }

        .example-badge:hover {
            background: #1e2b3f;
            border-color: #3b82f6;
            color: white;
        }

        footer {
            padding: 1rem 2rem;
            text-align: center;
            font-size: 0.7rem;
            color: #4c6188;
            border-top: 1px solid rgba(72, 120, 184, 0.2);
            background: rgba(0, 0, 0, 0.2);
        }

        @media (max-width: 640px) {
            .content {
                padding: 1.2rem;
            }
            .header h1 {
                font-size: 1.4rem;
            }
            button {
                padding: 0 1.2rem;
            }
            pre {
                font-size: 0.7rem;
            }
        }
    </style>
</head>
<body>

<div class="glass-card">
    <div class="header">
        <h1>loadstring() · raw2exec</h1>
        <div class="sub">
            🔗 Paste any raw script URL → instantly get Roblox-compatible loadstring wrapper
        </div>
    </div>
    <div class="content">
        <div class="input-group">
            <label><i>🌐</i> Raw script URL (must be raw text / .lua or raw.githubusercontent)</label>
            <div class="url-input-wrapper">
                <input type="text" id="rawUrlInput" placeholder="https://raw.githubusercontent.com/user/script/main/example.lua" value="">
                <button id="convertBtn">✨ Generate loadstring</button>
            </div>
            <div class="example-row">
                <span style="color:#6a86b3; font-size:0.75rem;">📋 Try examples:</span>
                <span class="example-badge" data-url="https://raw.githubusercontent.com/Exunys/Roblox-Scripts/main/Example.lua">Example script (dummy)</span>
                <span class="example-badge" data-url="https://raw.githubusercontent.com/scripts/Test/main/hello.lua">Hello World raw</span>
                <span class="example-badge" data-url="https://gist.githubusercontent.com/raw/example/raw-link-test.txt">Custom text link</span>
            </div>
        </div>

        <!-- loadstring output block -->
        <div class="result-section" id="resultBlock">
            <div class="panel-header">
                <h3><span>📜</span> LOADSTRING READY · Roblox Executor Format</h3>
                <button class="copy-btn" id="copyLoadstringBtn">📋 Copy Code</button>
            </div>
            <pre id="loadstringOutput">// Your generated loadstring will appear here
-- Example:
loadstring(game:HttpGet("https://your.raw.link/script.lua"))()</pre>
        </div>

        <!-- optional: raw script preview (bonus) -->
        <div class="result-section" style="margin-top: 1.5rem;">
            <div class="panel-header">
                <h3><span>🔍</span> Raw script preview (first 300 chars)</h3>
                <button class="copy-btn" id="copyRawPreviewBtn">📄 Copy preview</button>
            </div>
            <pre id="rawPreview">Waiting for URL conversion ...</pre>
        </div>

        <div id="statusMsg" class="status-message">💡 Paste a raw URL and click generate — supports HTTP/HTTPS raw links.</div>
    </div>
    <footer>
        ⚙️ Converts any direct raw file URL → loadstring(game:HttpGet("..."))()  |  Secure & local only, no external calls except your provided URL.
    </footer>
</div>

<script>
    (function(){
        // DOM elements
        const urlInput = document.getElementById('rawUrlInput');
        const convertBtn = document.getElementById('convertBtn');
        const loadstringOutput = document.getElementById('loadstringOutput');
        const rawPreview = document.getElementById('rawPreview');
        const statusDiv = document.getElementById('statusMsg');
        const copyLoadstringBtn = document.getElementById('copyLoadstringBtn');
        const copyRawPreviewBtn = document.getElementById('copyRawPreviewBtn');
        
        // helper: update status with style
        function setStatus(message, isError = false) {
            statusDiv.textContent = message;
            if (isError) {
                statusDiv.classList.add('error-message');
                statusDiv.classList.remove('success-message');
            } else {
                statusDiv.classList.remove('error-message');
                statusDiv.classList.add('success-message');
            }
            // auto remove special highlight after 4 sec but keep message
            setTimeout(() => {
                if(!isError && statusDiv.textContent === message) {
                    statusDiv.classList.remove('success-message');
                }
                if(isError && statusDiv.textContent === message) {
                    statusDiv.classList.remove('error-message');
                }
            }, 4000);
        }
        
        // core function: validate URL and fetch, then build loadstring
        async function processRawUrl(rawUrl) {
            if(!rawUrl || rawUrl.trim() === "") {
                setStatus("❌ Please enter a valid raw URL (HTTP/HTTPS).", true);
                loadstringOutput.innerText = `// Error: No URL provided\n-- Insert a valid raw link and try again.`;
                rawPreview.innerText = "⚠️ No URL entered.";
                return false;
            }
            
            let url = rawUrl.trim();
            // simple URL validation + enforce http/https
            try {
                const parsed = new URL(url);
                if(parsed.protocol !== 'http:' && parsed.protocol !== 'https:') {
                    throw new Error("Only HTTP/HTTPS links are allowed");
                }
            } catch(e) {
                setStatus(`Invalid URL: ${e.message || "Bad format"}`, true);
                loadstringOutput.innerText = `// Invalid URL format\n-- Use a full raw link starting with http:// or https://`;
                rawPreview.innerText = `❌ URL parsing error: ${e.message || "incorrect structure"}`;
                return false;
            }
            
            // show loading state
            setStatus(`⏳ Fetching script from ${url} ...`, false);
            loadstringOutput.innerText = `// Generating loadstring...\n-- fetching remote content...`;
            rawPreview.innerText = `⏳ Loading preview...`;
            
            try {
                // Fetch the raw content (CORS? but many raw hosts allow, also fetch works in browser context)
                // For general raw links (github raw, pastebin raw, etc) we respect CORS. If fails due to CORS,
                // we still generate a loadstring based on the URL, but inform user that preview might be blocked.
                const controller = new AbortController();
                const timeoutId = setTimeout(() => controller.abort(), 8000);
                const response = await fetch(url, { 
                    method: 'GET',
                    mode: 'cors',        // try cors, but if fails we catch
                    signal: controller.signal,
                    headers: { 'Cache-Control': 'no-cache' }
                });
                clearTimeout(timeoutId);
                
                if(!response.ok) {
                    throw new Error(`HTTP ${response.status}: ${response.statusText}`);
                }
                
                const scriptContent = await response.text();
                // Preview first ~300 chars (clean)
                let preview = scriptContent.slice(0, 500);
                if(scriptContent.length > 500) preview += "\n... (truncated)";
                rawPreview.innerText = preview || "[empty script]";
                
                // Build the loadstring line: loadstring(game:HttpGet("URL"))()
                // Use lua string escaping: escape double quotes and backslashes for safe embedding inside loadstring argument.
                // Since we are embedding inside game:HttpGet("...") we must escape " and \ inside URL? but URL shouldn't have double quotes generally.
                // To be safe, replace " with \" and backslash with double backslash.
                let safeUrl = url.replace(/\\/g, '\\\\').replace(/"/g, '\\"');
                const loadstringCode = `loadstring(game:HttpGet("${safeUrl}"))()`;
                loadstringOutput.innerText = loadstringCode;
                setStatus(`✅ Success! loadstring ready. Script length: ${scriptContent.length} chars.`, false);
                return true;
                
            } catch(fetchError) {
                console.warn("Fetch preview error:", fetchError);
                // Even if fetching fails (CORS / network), we can still generate loadstring code based on URL.
                // Because the executor will handle game:HttpGet at runtime. So we provide loadstring anyway.
                let safeUrl = url.replace(/\\/g, '\\\\').replace(/"/g, '\\"');
                const fallbackLoadstring = `loadstring(game:HttpGet("${safeUrl}"))()`;
                loadstringOutput.innerText = fallbackLoadstring;
                
                let errorNote = "";
                if(fetchError.name === 'AbortError') errorNote = "Request timeout.";
                else if(fetchError.message.includes('Failed to fetch') || fetchError.message.includes('CORS')) {
                    errorNote = "⚠️ Preview blocked by CORS or network. Loadstring still generated (executor will fetch at runtime).";
                } else {
                    errorNote = `⚠️ Preview error: ${fetchError.message}`;
                }
                rawPreview.innerText = `⚠️ Could not fetch raw preview due to: ${errorNote}\n\nBut loadstring is ready to use.\nURL: ${url}`;
                setStatus(`⚠️ ${errorNote} Loadstring generated anyway.`, false);
                return true; // still successful in generating loadstring
            }
        }
        
        // generate based on current input
        async function generateFromCurrentUrl() {
            const rawUrl = urlInput.value.trim();
            if(!rawUrl) {
                setStatus("📛 Please type or paste a raw script URL first.", true);
                loadstringOutput.innerText = `// No URL provided\n-- Example: loadstring(game:HttpGet("https://raw.githubusercontent.com/..."))()`;
                rawPreview.innerText = "// waiting for valid raw url";
                return;
            }
            await processRawUrl(rawUrl);
        }
        
        // copy helpers
        async function copyToClipboard(text, successMsg) {
            try {
                await navigator.clipboard.writeText(text);
                setStatus(`✅ ${successMsg} copied to clipboard!`, false);
                setTimeout(() => {
                    if(statusDiv.textContent.includes("copied")) setStatus("💡 Ready for next conversion.", false);
                }, 1800);
            } catch(err) {
                setStatus(`❌ Copy failed: ${err.message}`, true);
                // fallback: use textarea method
                const textarea = document.createElement('textarea');
                textarea.value = text;
                document.body.appendChild(textarea);
                textarea.select();
                document.execCommand('copy');
                document.body.removeChild(textarea);
                setStatus(`📋 Copied using fallback method.`, false);
            }
        }
        
        copyLoadstringBtn.addEventListener('click', () => {
            let code = loadstringOutput.innerText;
            if(code.startsWith("//") && code.includes("Error")) {
                setStatus("No valid loadstring to copy yet, generate one first.", true);
                return;
            }
            copyToClipboard(code, "Loadstring code");
        });
        
        copyRawPreviewBtn.addEventListener('click', () => {
            let previewText = rawPreview.innerText;
            if(previewText.includes("Waiting for URL") || previewText.includes("no URL entered")) {
                setStatus("No script preview available. Generate a loadstring first.", true);
                return;
            }
            copyToClipboard(previewText, "Raw preview");
        });
        
        convertBtn.addEventListener('click', () => {
            generateFromCurrentUrl();
        });
        
        // enter key support in input field
        urlInput.addEventListener('keypress', (e) => {
            if(e.key === 'Enter') {
                e.preventDefault();
                generateFromCurrentUrl();
            }
        });
        
        // example click fill & auto-generate
        const exampleBadges = document.querySelectorAll('.example-badge');
        exampleBadges.forEach(badge => {
            badge.addEventListener('click', () => {
                const exampleUrl = badge.getAttribute('data-url');
                if(exampleUrl) {
                    urlInput.value = exampleUrl;
                    generateFromCurrentUrl();
                }
            });
        });
        
        // initial demo message and default loadstring example (nice placeholder)
        loadstringOutput.innerText = `loadstring(game:HttpGet("https://raw.githubusercontent.com/Exunys/Roblox-Scripts/main/Example.lua"))()\n\n// 👆 Paste your raw link and click Generate.`;
        rawPreview.innerText = "💡 Use any raw .lua or .txt file URL. The converter creates a Roblox-compatible loadstring wrapper. Click on examples to test!";
        setStatus("✨ Ready! Enter a raw URL (GitHub raw, pastebin raw, etc).", false);
    })();
</script>
</body>
</html>
    ```
    
</details>


```lua
loadstring(game:HttpGet("https://raw.githubusercontent.com/7swazys/loadstring-gen/refs/heads/main/script"))()
```
