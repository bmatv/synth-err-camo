# synth-err-camo
A set of test examples for GipsyX to illustrate synth_err issue (Matviichuk et al., 2022)

The solutions can be replicated using the run scripts in each directory. Directories have suffixes in their names which correspond to the coordinate process noise values in mm and also a “synth” suffix if apriori values contain synthetic signals. 

The plots provided demonstrate estimated values (EST), a priori values (APR) and the difference between them. Two different process noise values were used in the tests: `1e-6 mm/sqrt(s)` and `3.2 mm/sqrt(s)`, or a process noise close to 0 and a standard coordinate process noise used throughout the manuscript. 

Please note that GipsyX uses meters, and though the directories are have process noise suffixes in $mm$, *1e-6*$\frac{mm}{\sqrt{s}}$ and *3.2*$\frac{mm}{\sqrt{s}}$, the actual values in the tree config files are *1e-9*$\frac{m}{\sqrt{s}}$ and *3.2e-3*$\frac{m}{\sqrt{s}}$, respectively. The plots were made only for Z coordinate component using Linux standard utilities and utilities provided with GipsyX (plots for other components can be made similarly):

```bash
cd camo2010.001_3.2
```
```bash
grep Station.CAMO.State.Pos.Z smoothFinal.tdp | cm 1 "c2*1000" | matp -nk -xl "Hours Past 2010-01-01 00:00:00" -secPast -fmtX "%H" -yl "(mm)" -t "Pos.Z APR at CAMO" -png APR_Z.png
```

```bash
grep Station.CAMO.State.Pos.Z smoothFinal.tdp | cm 1 "c3*1000" | matp -nk -xl "Hours Past 2010-01-01 00:00:00" -secPast -fmtX "%H" -yl "(mm)" -t "Pos.Z EST at CAMO" -png EST_Z.png
```

```bash
grep Station.CAMO.State.Pos.Z smoothFinal.tdp | cm 1 "(c3 - c2)*1000" | matp -nk -xl "Hours Past 2010-01-01 00:00:00" -secPast -fmtX "%H" -yl "(mm)" -t "Pos.Z EST - APR at CAMO" -png diff_EST_APR_Z.png
```

