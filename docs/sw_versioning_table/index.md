Software Distros
===

## 🚀 Software Distros Workflow
- 📅 SW Distros are typically delivered on a **time-based workflow**.
- 4️⃣ SW Distros are usually released along with **binaries** at the following quarters: **Feb, May, Aug, Nov**.
- 🆓 The feature-freeze lasts **one month**.
- 📛 Naming convention adheres therefore to **`YYYY.MM.0`**, where **`YYYY`** identifies the year so as **`MM`** the month of the distro. The patch number **`0`** clarifies that it is a major distro. Examples: 2021.11.0, 2022.02.0...
- 📝 Repositories stay on their usual release convention in order to enable proper **semantic versioning**. To link repos tags to SW Distro and run CI, we rely on the infrastructure provided in [`robotology/robotology-superbuild`](https://github.com/robotology/robotology-superbuild).
- 📦 Occasionally, we may release **feature-based distros** and/or **patches** as a collection of tags/branches (i.e., no binaries). Naming convention follows the pattern **`YYYY.MM.P`**, where **`YYYY.MM`** identifies the major release used as baseline and the patch number **`P`** is simply increased also in the case of a feature or patch distro released after YYYY/MM.
- ⚠ Distros released before `2021.11.0` may be named without the patch number **`P`** and may also be marked explicitly with `feat` or `patch` labels. 
- 📢 We make **announcements** of the distros and their content on a dedicated channel of [Robotology Community](https://github.com/orgs/robotology/discussions/categories/releases).

## Software Versioning Table
The table hereinafter reports on the versions of the packages (specified in terms of Git tags/branches/commits)
composing our software ecosystem that are bundled as distros.

Once the versions are known, one can download the distro's source code by using Git.

For example, to download the SW Distro `2020.08` do:
```sh
$ git clone https://github.com/robotology/ycm.git -b v0.11.3
$ git clone https://github.com/robotology/yarp.git -b v3.4.0
$ git clone https://github.com/robotology/icub-main.git -b v1.17.0
 ...
```

## Table
This table has been generated automatically by processing data available in [`robotology/robotology-superbuild@v2026.08.0/releases`](https://github.com/robotology/robotology-superbuild/tree/v2026.08.0/releases).

Click on the distros below to explore their package versions:

- [📦 Distro **2026.08.0**](./2026.08.0.md){:target="_blank"}
- [📦 Distro **2025.11.1**](./2025.11.1.md){:target="_blank"}
- [📦 Distro **2025.11.0**](./2025.11.0.md){:target="_blank"}
- [📦 Distro **2025.08.0**](./2025.08.0.md){:target="_blank"}
- [📦 Distro **2025.05.0**](./2025.05.0.md){:target="_blank"}
- [📦 Distro **2025.02.0**](./2025.02.0.md){:target="_blank"}
- [📦 Distro **2024.11.2**](./2024.11.2.md){:target="_blank"}
- [📦 Distro **2024.11.1**](./2024.11.1.md){:target="_blank"}
- [📦 Distro **2024.11.0**](./2024.11.0.md){:target="_blank"}
- [📦 Distro **2024.08.0**](./2024.08.0.md){:target="_blank"}
- [📦 Distro **2024.05.0**](./2024.05.0.md){:target="_blank"}
- [📦 Distro **2024.02.0**](./2024.02.0.md){:target="_blank"}
- [📦 Distro **2023.11.0**](./2023.11.0.md){:target="_blank"}
- [📦 Distro **2023.08.0**](./2023.08.0.md){:target="_blank"}
- [📦 Distro **2023.05.2**](./2023.05.2.md){:target="_blank"}
- [📦 Distro **2023.05.1**](./2023.05.1.md){:target="_blank"}
- [📦 Distro **2023.05.0**](./2023.05.0.md){:target="_blank"}
- [📦 Distro **2023.02.3**](./2023.02.3.md){:target="_blank"}
- [📦 Distro **2023.02.2**](./2023.02.2.md){:target="_blank"}
- [📦 Distro **2023.02.1**](./2023.02.1.md){:target="_blank"}
- [📦 Distro **2023.02.0**](./2023.02.0.md){:target="_blank"}
- [📦 Distro **2022.11.0**](./2022.11.0.md){:target="_blank"}
- [📦 Distro **2022.09.1**](./2022.09.1.md){:target="_blank"}
- [📦 Distro **2022.09.0**](./2022.09.0.md){:target="_blank"}
- [📦 Distro **2022.08.1**](./2022.08.1.md){:target="_blank"}
- [📦 Distro **2022.08.0**](./2022.08.0.md){:target="_blank"}
- [📦 Distro **2022.05.2**](./2022.05.2.md){:target="_blank"}
- [📦 Distro **2022.05.1**](./2022.05.1.md){:target="_blank"}
- [📦 Distro **2022.05.0**](./2022.05.0.md){:target="_blank"}
- [📦 Distro **2022.02.2**](./2022.02.2.md){:target="_blank"}
- [📦 Distro **2022.02.1**](./2022.02.1.md){:target="_blank"}
- [📦 Distro **2022.02.0**](./2022.02.0.md){:target="_blank"}
