---
marp: true
theme: default
paginate: true
footer: ![height:20px](img/twitter.svg) ![height:20px](img/github.svg) @JohanMabille @jtpio @QuantStack
style: |
  .columns {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1rem;
  }
---

<style>
section::after {
  content: attr(data-marpit-pagination) '/' attr(data-marpit-pagination-total);
}
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
video {
  width: 100%;
  height: auto;
}
</style>

![bg fit right:30%](https://jupyter.org/assets/homepage/main-logo.svg)

# The Jupyter Ecosystem

## Offsite Event - 2023-05-24

---

# About
<div class="columns">
<div>

## Johan Mabille

- Technical Director at QuantStack
- Jupyter Distinguished Contributor
- Co-authored the xeus stack, the debugger in Jupyter
- Leads the development of mamba

</div>
<div>

## Jérémy Tuloup

- Technical Director at QuantStack
- Jupyter Distinguished Contributor
- Contributes to JupyterLab, Jupyter Notebook, Voilà
- Author of JupyterLite

</div>
</div>

---

# History

---

# October 2001

- IPython 0.0.1: 1 file, 110 lines of code (excluding comments)
- IPython 0.1 (November): 3k lines of code

TODO: screenshot IPython

---

# December 2011

- First release of IPython notebook
- IPython 0.12: 46k Python, 3k Javascript

TODO: screenshot notebook

---

# October 2020

- IPython 7.12: 34k Python
- Notebook 6.1: 13k Python, 16k Javascript
- JupyterHub 1.2: 16k Python
- JupyterLab 3.0: 100k Typescript
- 282 repos across 9 GitHub organizations

---

# Governance

---

# 2014: creation of Project Jupyter

- BDFL + steering council model
- Steering council composed of most active members
- Limitations:
    - people not active anymore still in the council
    - the council can not grow undefinitely

---

# 2020: JDC elections

- Jupyter Distinguished Contributors elections
- rewards people active in the community for 2 consecutive years
- cohort of 10 JDC per year

---

# 2022: new governance model

- Executive council: responsible for all dimensions of the project (legal, financial, community, operations, ...)
- Software Steering Council: software-related decisions across Project Jupyter, coordination across subprojects
- Software Subprojects: governance and software decisions of subparts of Project Jupyter (Kernels, Server, JupyterLab, ...)
- Each software subproject nominates a single representative to the SSC

---

# Architecture and Protocol

---

# The Jupyter Kernel Protocol

- Documentation at https://jupyter-client.readthedocs.io/en/stable/messaging.html
- Agnostic to the language
- `jupyter_client` is the reference implementation in Python
- `xeus` is the reference implementation in C++
- Implementations rely on ZeroMQ

![bg fit right:30%](https://xeus.readthedocs.io/en/latest/_images/jupyter_archi.svg)

---

# The Jupyter kernel protocol

Clients and kernels communicate (over the network) through 5 channels:

- Shell: code execution, code completion
- Control: stop and restart, kernel info, debugging
- stdin: input request
- IOPub: broadcast channel to publish results and kernel state
- Heartbeat: to check the kernel is still alive

ZeroMQ provides the low-level transport layer over which the messages are sent.

---

![bg fit 60%](img/client_server_kernel-0.svg)

---

![bg fit 60%](img/client_server_kernel-1.svg)

---

![bg fit 60%](img/client_server_kernel-2.svg)

---

# Jupyter Server

- Backend to Jupyter Web applications (not the consoles):
    - core services
    - APIs
    - REST endpoints
- Client of kernels
- Responsible for launching and keeping kernels alive
- Use the same protocol for Web apps and kernels

---

# Servers

- Jupyter Server: historical, mono user, based on tornado
- Jupyverse: alternative implementation based on FastAPI
- JupyterHub: multi-user server using Jupyter Server

---

# Kernels

- ipykernel, reference implementation of python kernel
- kernel wrapper approach (kernels based on ipykernel)
- standalone kernels (IJulia, IRKernel)
- xeus-based kernels (xeus-cling, xeus-python, xeus-lua, etc...)

---

![bg fit 60%](img/widgets.svg)

---

# Jupyter Widgets

- ipywidgets / xwidgets: basic interactive widgets (sliders, buttons, checkboxes...)
- ipyleaflet / xleaflet: interactive maps based on leaflet
- bqplot / xplot: plotting libraries implementing the grammar of graphics
- many others ....

![bg fit right](img/widgets.png)

---

![bg fit 60%](img/repos_map.svg)

---

# Debugger

---


# Debugger Protocol

- New debug\_request / debug\_reply sent over the control channel
- Content follows the specification of the DAP by Microsoft: https://microsoft.github.io/debug-adapter-protocol/
- Additional messages:
    - dumpCell: maps a temporary file to a cell
    - debugInfo: retrieves debugger state after refresh + dumpCell file computation info
    - inspectVariables: gets defined variables values
    - richInspectVariables: same as previous with rich rendering

---

![bg fit 60%](img/debugger_sequence-1.svg)

---

![bg fit 60%](img/debugger_sequence-2.svg)

---

![bg fit 60%](img/debugger_sequence-3.svg)

---


![bg fit 60%](img/debugger_sequence-4.svg)

---

# Using the debugger frontend

---

![bg fit 70%](img/debugger-1.png)

---

![bg fit 70%](img/debugger-2.png)

---

![bg fit 70%](img/debugger-3.png)

---

# VS Code Notebooks vs JupyterLab

---

# VS Code

- Support for Jupyter Widgets (core and custom widgets)
- Integrate with the VS Code debugger (but uses the Jupyter debugger underneath)
- Integrate with GitHub Copilot
- Slightly more complicated to use?

---

# JupyterLab

- Official Jupyter frontend
- Run in the browser by default
- Jupyter AI: ChatGPT-like features coming to JupyterLab: `pip install jupyter-ai`

---

# JupyterLite :bulb:

- WebAssembly powered Jupyter running in the browser
- Stands on the shoulder of giants:
  - Xeus kernels running in the browser
  - JupyterLab and Jupyter Notebook
  - Voici to turn notebooks into static web applications
  - Support for Jupyter Widgets and visualization libraries
- No real `jupyter-server`, `jupyter-client`, `nbconvert`

---

![bg fit 60%](./img/jupyterlite.png)

---

![bg fit 75%](./img/jupyterlite.svg)

---

# JupyterLite

- Used on many websites: [numpy.org](https://numpy.org), [sympy.org](https://sympy.org), [Try Jupyter](https://try.jupyter.org), ...
- Works as a PWA (Progressive Web App) on mobile devices:


<div style="text-align: center">
<img src="./img/jupyterlite-pwa-1.png" height="400px">
<img src="./img/jupyterlite-pwa-2.png" height="400px">

</div>

---

# JupyterLab 4

![bg fit right:33%](./img/jupyterlab-logo.png)

---

# New Features

- Performance improvements (Codemirror 6, virtual rendering)
- Real-Time Collaboration improvements (install with `pip install jupyter-collaboration`)
- Improved search
- Table of Contents
- PyPI Extension Manager
- Linked kernels enhancements
- Support for notifications
- JupyterLab Desktop

---

# Notifications

<video controls src="./img/02-notifications.mov"></video>

---

# Search

<video controls src="./img/03-search.mov" ></video>

---

# Cell Toolbar

<video controls src="./img/04-celltoolbar.mov" ></video>

---

# Table of Contents

<video controls src="./img/06-toc.mov" ></video>

---

# Linked Kernel Enhancements

<video controls src="./img/07-linkedkernels.mov" ></video>

---

# Settings Editor

<video controls src="./img/08-settings.mov" ></video>

---

# Performance Enhancmenents

<video controls src="./img/10-performance.mp4" ></video>

---

# Extension Manager

![center](https://github.com/jupyterlab/jupyterlab/assets/591645/54e4945a-89a4-408e-9932-a9bfdd414336)

---

# Collaborative Editing

<video controls src="./img/11-RTC.mp4" ></video>

---

# Collaborative Editing for developers

<video controls src="./img/12-jcad-rtc.mp4" ></video>

---

# New extension points

- Notifications
- Custom settings editor
- Metadata editor
- Text editor (CodeMirror 6)
- New completer
- New table of contents
- New search in documents

![bg fit right](https://github.com/jupyterlab/jupyterlab/assets/591645/987834da-0a50-4b82-a1a3-0c6828b7fc08)

---

# Jupyter Notebook 7

---

# A new version for Jupyter Notebook

- Notebook 7 includes many new features
- Keeps the same UX and document-centric look and feel
- Uses the same Notebook Format and Jupyter Protocol
- Is compatible with the JupyterLab extension ecosystem


![center h:300px](https://jupyter.org/assets/homepage/main-logo.svg)

---

![center](img/notebook-7.png)

---

# Roadmap

- JupyterLab 4 is released :tada:
- Notebook 7 final will soon be released
- JupyterLite 0.2 based on JupyterLab 4 and Notebook 7
- ...

---


# Thanks!

Thanks to Martha Cryan, Afshin T. Darian and Frederic Collonval for their slides on JupyterLab 4.
