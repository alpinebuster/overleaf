# Getting Started
This guide explains how to update **TeX Live** and install the **full TeX Live scheme** inside an Overleaf Community Edition Docker container.

---

## **1. Run & Enter the ShareLaTeX Docker Container**

Use `docker exec` to open an interactive Bash shell inside the running ShareLaTeX container.

```bash
# At project's root dir
docker compose up -d
docker exec -it sharelatex bash
```

## **2. Navigate to the TeX Live Installation Directory**

TeX Live is installed under `/usr/local/texlive` inside the container.

```bash
cd /usr/local/texlive
```

All update operations will be performed from this directory.

---

## **3. Download the Latest TeX Live Manager (tlmgr) Updater**

Fetch the official update script from CTAN.
The `--no-check-certificate` option avoids SSL certificate issues in minimal containers.

```bash
wget http://mirror.ctan.org/systems/texlive/tlnet/update-tlmgr-latest.sh --no-check-certificate
```

This file contains the latest version of the TeX Live Manager installer.

## **4. Upgrade tlmgr Using the Downloaded Script**

Run the script to update `tlmgr` itself.

```bash
sh update-tlmgr-latest.sh -- --upgrade
```

## **5. Set a Faster CTAN Mirror (Optional but Recommended)**

Choose a nearby or faster mirror to speed up package downloads.
Here we use the Tsinghua University mirror in China:

```bash
tlmgr option repository https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet/
```

## **6. Update tlmgr and All Installed TeX Live Packages**

Perform a complete update, including the manager itself and every installed package.

```bash
tlmgr update --self --all
```

> **Note:**
> In some cases, you may need to rebuild font caches afterward using:
>
> ```
> luaotfload-tool -fu
> ```
>
> This is optional and only required if font issues occur.

## **7. Install the Full TeX Live Scheme**

Finally, install the complete collection of TeX Live packages.
This provides nearly every available LaTeX package and tool.
This step is optional but recommended if you want the widest compatibility with LaTeX documents.

```bash
tlmgr install scheme-full
```

Then **restart** the `sharelatex` container!

---

## **Open the Web Application**

Navigate to the Overleaf **Admin Panel** at:

* **[http://localhost:8080/launchpad](http://localhost:8080/launchpad)**

From there, set up an administrator account.
Once the admin user is created, you can access the Overleaf **Web Application** at:

* **[http://localhost:8080/](http://localhost:8080/)**
