# Third-Party Notices

Neonmem is distributed as compiled binaries that bundle third-party
open-source components. Those components remain under their own licenses,
reproduced or referenced below. This file satisfies the attribution
requirements of those licenses; it does **not** change the license of Neonmem
itself (see [LICENSE](LICENSE)).

Full, unmodified license texts for each component ship inside the corresponding
package directory in the installed application (Python packages under
`resources/neonmem/`, Node packages under the app's `node_modules/`). Electron
additionally ships the license texts of its bundled Chromium, Node.js, and V8
components in `LICENSES.chromium.html` within the application directory.

---

## Python core (bundled in `neonmem.exe`)

| Component | License | Project |
|---|---|---|
| NumPy | BSD-3-Clause | https://numpy.org |
| model2vec | MIT | https://github.com/MinishLab/model2vec |
| potion-retrieval-32M (model weights) | MIT | https://huggingface.co/minishlab/potion-retrieval-32M |
| tokenizers | Apache-2.0 | https://github.com/huggingface/tokenizers |
| safetensors | Apache-2.0 | https://github.com/huggingface/safetensors |
| huggingface-hub | Apache-2.0 | https://github.com/huggingface/huggingface_hub |
| faiss-cpu | MIT | https://github.com/facebookresearch/faiss |
| FastMCP | Apache-2.0 | https://github.com/jlowin/fastmcp |
| mcp (Model Context Protocol SDK) | MIT | https://github.com/modelcontextprotocol/python-sdk |
| pydantic | MIT | https://github.com/pydantic/pydantic |
| pydantic-core | MIT | https://github.com/pydantic/pydantic-core |
| rich | MIT | https://github.com/Textualize/rich |
| CPython runtime + standard library | PSF License Agreement | https://www.python.org |

## Node / Electron (bundled in the desktop app)

| Component | License | Project |
|---|---|---|
| Electron | MIT | https://github.com/electron/electron |
| — bundled Chromium | BSD-3-Clause + others | see `LICENSES.chromium.html` |
| — bundled Node.js | MIT | see `LICENSES.chromium.html` |
| — bundled V8 | BSD-3-Clause | see `LICENSES.chromium.html` |
| node-pty | MIT | https://github.com/microsoft/node-pty |
| three.js | MIT | https://github.com/mrdoob/three.js |
| ws | MIT | https://github.com/websockets/ws |
| xterm.js | MIT | https://github.com/xtermjs/xterm.js |
| xterm-addon-fit | MIT | https://github.com/xtermjs/xterm.js |
| xterm-addon-web-links | MIT | https://github.com/xtermjs/xterm.js |

---

### License summaries

- **MIT** and **BSD-3-Clause**: permissive; require the copyright notice and
  permission notice to be retained — satisfied by this file and the bundled
  package license texts.
- **Apache-2.0**: permissive; requires retention of copyright, the license, and
  any NOTICE files — satisfied by the bundled package license/NOTICE files.
- **PSF License Agreement**: governs the bundled CPython runtime.

If you believe a component is missing from this list or attributed incorrectly,
contact stmedvid@gmail.com and it will be corrected.
