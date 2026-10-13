# CRESCENT Community Velocity Model Book

[![License: BSD-3-Clause](https://img.shields.io/badge/License-BSD_3--Clause-blue.svg)](LICENSE)

Documentation for the CRESCENT Community Velocity Model (CVM): the velocity models in the repository, how to submit a model, and the CVM-Tools Python package for building, inspecting and converting CVM files.

**Read the book:** https://cascadiaquakes.github.io/cvm-tools-book/
**Viewer:** https://cvm.cascadiaquakes.org
**Code:** https://github.com/cascadiaquakes/CRESCENT-CVM

---

## Contents

- **Velocity Models**: one page per 3D and 2D model (`3Dmodels/`, `2Dmodels/`)
- **Submission Instructions**: how to contribute a model (`submission.md`)
- **CVM-Tools Reference**: standards and conventions, setup, and usage guides for the primary and utility tools (`usage/`)

---

## Building Locally

The book is built with [MyST](https://mystmd.org). With Node.js installed, run from the repository root:

```bash
npx --yes mystmd start
```

Then open the URL it prints.

---

## Deployment

GitHub Actions builds the book on every push to `main` and publishes it to GitHub Pages.

---

## Contributing

See the [Submission Instructions](https://cascadiaquakes.github.io/cvm-tools-book/submission/) for how to contribute a velocity model.

---

## License

This project is licensed under the BSD 3-Clause License. See [LICENSE](LICENSE).

---

## Contacts

- **Amanda M. Thomas**, University of California, Davis: [amthom@ucdavis.edu](mailto:amthom@ucdavis.edu)
- **William Marfo**, University of California, Davis: [wmarfo@ucdavis.edu](mailto:wmarfo@ucdavis.edu)
- **Loïc Bachelot**, University of Oregon: [lbachelo@uoregon.edu](mailto:lbachelo@uoregon.edu)

For corrections or suggestions, please [open an issue](https://github.com/cascadiaquakes/cvm-tools-book/issues).

---

## Acknowledgments

<table>
  <tr>
    <td align="center" valign="middle">
      <img src="https://raw.githubusercontent.com/cascadiaquakes/.github/main/assets/crescent-circle.png" alt="CRESCENT Logo" width="150" />
    </td>
    <td align="center" valign="middle">
      <img src="https://raw.githubusercontent.com/cascadiaquakes/.github/main/assets/nsf-logo.png" alt="NSF Logo" width="450" />
    </td>
  </tr>
</table>

This project is supported by the National Science Foundation through the Cascadia Region Earthquake Science Center (CRESCENT), Cooperative Agreement EAR-2225286.
