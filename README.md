Brain_Segmentation
==============================

Segmentation of the brain from mri images

DAT255 - Deeplearning HVL 2023
------------

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make data` or `make train`
    ├── README.md          <- The top-level README for developers using this project.
    ├── data
    │   ├── external       <- Data from third party sources.
    │   ├── interim        <- Intermediate data that has been transformed.
    │   ├── processed      <- The final, canonical data sets for modeling.
    │   └── raw            <- The original, immutable data dump.
    │
    ├── docs               <- A default Sphinx project; see sphinx-doc.org for details
    │
    ├── models             <- Trained and serialized models, model predictions, or model summaries
    │
    ├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g.
    │                         `1.0-jqp-initial-data-exploration`.
    │
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
    │   └── figures        <- Generated graphics and figures to be used in reporting
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    │   │
    │   ├── data           <- Scripts to download or generate data
    │   │   └── make_dataset.py
    │   │
    │   ├── features       <- Scripts to turn raw data into features for modeling
    │   │   └── build_features.py
    │   │
    │   ├── models         <- Scripts to train models and then use trained models to make
    │   │   │                 predictions
    │   │   ├── predict_model.py
    │   │   └── train_model.py
    │   │
    │   └── visualization  <- Scripts to create exploratory and results oriented visualizations
    │       └── visualize.py
    │
    └── tox.ini            <- tox file with settings for running tox; see tox.readthedocs.io


--------

<img width="454" alt="Oppgavetekst" src="https://user-images.githubusercontent.com/69795381/233673937-60fd4e30-d091-4fdd-a8d3-99dc61b89511.png">


Oppsummering: 
I denne oppgaven skal jeg lage en modell som kan segmentere MRI skanninger av hjernen. For å få dette til må vi først få tak i data. Heldigvis finnens det åpne resurser til forskning på akkurat MRI skanninger. 


MRI: Magnet-resonans-tomografi (Magnetic resonance imaging) er en teknikk for å fremstille bilder av kroppsvev hos mennesker eller dyr. Teknologien er utledet fra prinsippet om atomers spesifikke egensvingetid og hvordan disse oppfører seg når de utsettes for radiobølger mens de er plassert i et kraftig magnetfelt. I dette tilfellet er det MRI av hjernen vi skal se på.

NiFTi-1 data format :  Neuroimaging Informatics Technology Initiative. NiFTi-1 er en metode for å lagre MRI bilder av hjernen. Man kan tenke på bildene som en firkantet blokk med en x, y og z akse. Blokken består av MRI bilder av et hode fra bunnen til toppen.

![InniMr](https://user-images.githubusercontent.com/69795381/233673847-7f109584-5dba-4717-97f2-1c3365e03ba3.png)

<img width="454" alt="NIFTI-explained" src="https://user-images.githubusercontent.com/69795381/233673889-48dfbc38-3089-4a39-8763-e970013bafd8.png">


Nibabel : “Read and write access to some common neuroimaging file formats.” Jeg bruker nibabel for å lese NiFTi-1 filene.

FreeSurfer : Et program for å mappe ulike deler av hjernen.

<img width="454" alt="BilderAvHjerner" src="https://user-images.githubusercontent.com/69795381/233673998-8b458ef4-4852-4eb9-a132-9486044e36ea.png">


ITK-SNAP : Er et funksjonelt program for å lage 3D-segmenteringsbilder fra MRI bilder.
ITK-SNAP is a free, open-source, multi-platform software application used to segment structures in 3D and 4D biomedical images.



The big picture:

Helse er et stort område som bruker ny teknologi for å bistå leger, sykepleiere og pasienter

Hva er hjernesegmentering?
-	Bruker segmentering til å automatisk gjenkjenne deler av hjernen, slik at mennesker slipper å finne områdene selv.

Utfordringer:
-	Når det kommer til helse er det veldig viktig at vi ikke bare gjetter, men kan med rimelig sikkerhet si at vi er korrekte.
-	Kan vi utføre oppgaven like bra eller bedre enn et menneske?
-	Kan vi vite at treningsdataen er 100% riktig? Det er veldig vanskelig for meg å sjekke over datasettet og si om dataen re segmentert riktig.

Data: (finn alle kilder data du kan komme over)
Først å fremst må jeg si at jeg ikke kan slev segmentere treningsdataen ettersom jeg er ikke utdannet lege. Så treningsdataen trenger jeg å finne ferdig segmentert.

-	Datasettet kommer fra IXI som er en samling med nesten 600 MR bilder fra normal, sunne individer.



-	IXI er hentet fra Hammersmith Hospital, Guy’s Hospital og Institute of Psychiatry.
-	ADNI – Alzheimer’s Disease Neuroimaging Initiative
-	https://adni.loni.usc.edu 

-	https://www.kaggle.com/datasets/ilknuricke/neurohackinginrimages

-	


IXI: (Alle filene er hentet og testet.)

<img width="359" alt="T1-eks" src="https://user-images.githubusercontent.com/69795381/233674069-40be8123-67e9-4691-a03a-681c29e5e933.png">

T1 = enhances. The signal of the fatty tissue and suppresses the signal of the water.
T2 = Enhances. The signal of the water.
PD = proton density
MRA = Magnetic Resonance Angiography. Brukes til å gi bilder av blodårer i kroppen.
DTI = Diffusion Tensor imaging.  is an MRI technique that uses anisotropic diffusion to estimate the axonal (white matter) organization of the brain.
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8086713/ 

Nearly 600 images
•	T1, T2 and PD-weighted images
•	MRA images
•	Diffusion-weighted images (15 directions)



Teknologivalg:
-	fastMonai
-	nibabel
-	Freesurfer


(for struktur)
pip install cookiecutter
trenger ikke å dokumentere med sphinxs
pip install tree



Struktur i repo:
-	README
-	Ende opp med en deployment av prosjektet.



Jeg gjør et forsøk på laste ned freesurfer for å teste deres program for klassifisering av hjernens strukturer. (Gamle versjoner av Mac er støttet, ukjent om jeg kan få det til i det hele tatt).


For å teste skal jeg ta T1 bildene og klassifisere dem med freesurfer, så skal jeg kun spare på ett bilde i midten av hjerne.

For å finne bilde i midten skal jeg hente ut den midterste snittet bildene og label bildene. Dermed kan jeg kjøre programmet.


Problemet er mange typer filformater for MRI.

NiFTi-1
MGH
MGZ
NII
NIIZ1
DCM 
DICOM image



Mot slutten av prosjektet innså jeg at jeg måtte korte ned på oppgaven ettersom for mye tid ble brukt på å lage 3D-modellen via fastMONAI. Grunnen til dette var at jeg ikke kunne prosessere dataen jeg hadde gjennom freesurfer. Freesurfer for mac er laget for en eldre versjon av mac. Derfor prøvde jeg å bruke ubuntu-disken deres, men når alt var satt opp fikk jeg opp at jeg måtte taste inn en valideringskode for å bruke freesurfer. Etter masse søk fant jeg ingen kode som kunne aktivere freesurfer. Ettersom jeg ikke fikk tilgang til freesurfer måtte jeg begrense oppgaven med at jeg ikke brukte fastMonai til å segmentere i 3D.

MR skanner består i vårt tilfelle av mange forskjellige bilder som blir tatt i ulik dybde på pasienten. I NII er filer i NIFTI-1 formatet som 

Etter flere dager med forsøk fikk jeg endelig til å kjøre notebooken på GPU framfor CPU. Det reduserte tiden den trengte for å kjøre ned fra 1.5 time til bare 5 min. Som er 18 ganger raskere enn å kjøre den på CPU.

Modellen klarer å gjøre segmentere bildene relativt bra med tanke på hvor mange labels modellen har.

Jeg prøvde å lage en applikasjon med huggingface, men fikk det ikke helt til pga problemer med å laste inn modellen.
https://huggingface.co/spaces/Andreas-w/Brain-segmentation 

