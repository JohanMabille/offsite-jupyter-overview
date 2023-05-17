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

TODO

---

# Architecture and Protocol

TODO

---

![bg fit 60%](img/repos_map.svg)

---

# Debugger

TODO

---

# VS Code Notebook vs JupyterLab

---

# VS Code

- Support for Jupyter Widgets (core and custom widgets)
- Integrate with the VS Code debugger (but uses the Jupyter debugger underneath)
- Integrate with GitHub Copilot
- Slightly more complicated to use?
- Demo ?

---

# JupyterLab

- Official Jupyter frontend
- Run in the browser by default
- Jupyter AI: Copilot-like features coming to JupyterLab: `pip install jupyter-ai`
- Demo?

---

# JupyterLite

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

# JupyterLab 4

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

# Roadmap

- JupyterLab 4 is released :tada:
- Notebook 7 final will soon be released
- JupyterLite 0.2 based on JupyterLab 4 and Notebook 7
- ...

---


# Thanks!

Thanks to Martha Cryan, Afshin T. Darian and Frederic Collonval for their slides on JupyterLab 4.