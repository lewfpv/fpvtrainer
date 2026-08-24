# FPV Trainer – GitHub Pages kiadás

Ez a mappa egy előre elkészített, teljesen statikus GitHub Pages kiadás. Node.js szerver nélkül fut.

## Feltöltés új GitHub repositoryba

1. Hozz létre a GitHubon egy új, lehetőleg nyilvános repositoryt.
2. A `release` mappa **tartalmát** töltsd fel a repository gyökerébe. Ne magát a `release` mappát tedd egy almappába.
   A `game_room.glb` nagyobb a GitHub böngészős feltöltésének korlátjánál, ezért a feltöltéshez Git parancssort vagy GitHub Desktopot használj, ne a weboldal **Add file / Upload files** funkcióját.
3. A GitHub repositoryban nyisd meg: **Settings → Pages**.
4. A **Build and deployment / Source** értéke legyen **Deploy from a branch**.
5. Branch: `main`, mappa: `/(root)`.
6. Nyomd meg a **Save** gombot, majd várd meg a publikálást.

A cím általában:

```text
https://FELHASZNALONEV.github.io/REPOSITORY-NEVE/
```

Parancssoros feltöltési példa a `release` mappából:

```powershell
git init
git add .
git commit -m "FPV Trainer GitHub Pages kiadás"
git branch -M main
git remote add origin https://github.com/FELHASZNALONEV/REPOSITORY-NEVE.git
git push -u origin main
```

## Ebben a kiadásban működik

- PlayCanvas/Ammo drónfizika és PID/rates;
- kontrollerkiosztás és kalibráció;
- minden grafikai, kamera-, drón- és pályabeállítás;
- GLB-pályaválasztás, skybox, spawn és irányfüggő kapuk;
- háromkörös verseny, rajtlámpa, DNF és köridők;
- beállítások JSON exportálása és importálása.

## Szándékosan kikapcsolva

- online leaderboard;
- szerveren tárolt replay;
- MP4-videórenderelés;
- minden `/api` szerverhívás.

Az oldal HTTPS-en fut a GitHub Pages szolgáltatásán. A felhasználói beállításokat minden böngésző a saját `localStorage` tárhelyén tárolja.

## Új kiadás készítése

A projekt forrásmappájában futtasd:

```powershell
npm run build:pages
```

Ez újra elkészíti a teljes `release` mappát.
