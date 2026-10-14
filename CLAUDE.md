# Instruccions per a Claude

## Qui és l'usuari

- Professor de Matemàtiques de Batxillerat (Catalunya). Llicenciat en Matemàtiques.
- Parla en **català**: respon sempre en català.
- Coneixements de GitHub limitats: quan calgui fer alguna cosa a GitHub, explica-ho
  pas a pas, amb enllaços i textos per copiar i enganxar.

## Pull requests

- **Per defecte, crea tu mateix la pull request** quan hagis pujat feina a la branca,
  i dona'n l'enllaç. L'usuari només ha de fer: *Merge pull request* → *Confirm merge*.
- Abans de pujar feina nova, comprova si l'última pull request ja s'ha fusionat.
  Si és així, torna a començar la branca des de `main` i crea una pull request **nova**
  (una pull request fusionada no agafa commits nous).

## Què és el projecte

Web estàtica (GitHub Pages, sense servidor) d'exercicis de Matemàtiques II (2n de Batxillerat).
L'alumne navega **unitat → tasca setmanal → exercici** i veu la imatge de l'enunciat i la solució.
Vegeu `README.md` i `TODO.md`.

| Fitxer | Paper |
|---|---|
| `tasques.js` | Programació: una línia per setmana (`unitat`, `setmana`, `limit`, `exercicis`) |
| `cataleg.js` | Fitxa de **cada** exercici de la unitat (títol `t`, dificultat `d`, imatges `i`, `a:1` si és activitat del món real). Mantingut a mà, no es genera |
| `hints.js` | Pistes, **només** dels exercicis programats a `tasques.js` |
| `errades.js` | Errades del solucionari dels exercicis programats («On diu / Ha de dir / Motiu») i observacions. Clau `'uN/número'`. S'edita a mà |
| `assets/katex/` | KaTeX 0.16.47: pinta les fórmules de `errades.js`. No s'hi toca res |
| `marca.js` | Eina del professor per marcar on és una errada dins la imatge. Només es carrega amb `?tot=1&marca=1` |
| `pegats/` | Trossos de pàgina ja corregits (PNG petits) que `tasca.html` posa a sobre de les imatges. Camp `pegat` de `errades.js` |
| `index.html` | `UNITATS`: unitats i temes |
| `publicats.js` | Vista per temes (antiga): tots els temes a `'cap'` |
| `2Bat - Unitats i feina Classroom.xlsx` | Programació del curs (setmana, data límit, unitat, exercicis) |

## Com s'afegeix una unitat nova (workflow)

1. L'usuari passa el **PDF del solucionari** de la unitat.
2. **Imatges**: cada pàgina del PDF → `uN/<tema>/data/full-K.png`, retallada sense la
   capçalera "SOLUCIONARI" ni el número de pàgina, **1208 px d'amplada**. Comprova que cap
   text quedi fora del retall. Una pàgina amb exercicis de dos temes va a les dues carpetes.
3. **Catàleg** de **tota** la unitat a `cataleg.js` (no només dels seleccionats), afegir la unitat
   a `UNITATS_META` (`cataleg.js`), a `UNITATS` (`index.html`) i els temes a `publicats.js`.
   - La dificultat (●○○) es llegeix dels cercles del PDF; la secció PRACTICA i els
     problemes finals no en porten (`d:''`).
   - Els números 1–N de "Matemàtiques en el món real" porten `a:1` i ocupen aquests números:
     les activitats del text amb el mateix número no hi caben.
4. L'usuari passa la **llista-sel** (exercicis de cada setmana, segons l'Excel).
5. Afegir les setmanes a `tasques.js` i **una pista per exercici** a `hints.js`
   (que apunti al mètode, **mai** el resultat; segons l'apartat «Estil de les pistes»).
6. Provar-ho al navegador amb `?tot=1` i crear la pull request.

## Estil de les pistes

**Model únic: `u7`, `u8` i `u9`** (55 pistes). El professor les ha escrit o refet una per una. Les de `u1`–`u6` i
`u10`–`u14` són d'una primera versió escrita per una IA (un sol paràgraf, cap etiqueta, to de «truc» i de «guió de
sempre»): **no les imitis**. Es distingeixen perquè les del professor porten `<br>`, `<i>` o `<b>`.

- Clau `'uN/número'`. Apòstrofs escapats (`d\'una`) o tipogràfics (’).
- Orienten cap al mètode; **no donen el resultat del problema**. Sí que poden recordar una fórmula o un teorema
  estàndard, traduir cada condició a una equació («passar per l'origen vol dir que *(0, 0)* és de la gràfica») i
  dir què trobarà l'alumne («et quedarà una paràbola», «trobaràs dues solucions»).

### Abans d'escriure

1. **Mira l'enunciat de debò.** Cada exercici té una imatge (camp `i` de `cataleg.js`, a `uN/<tema>/data/full-K.png`)
   amb l'enunciat **i** la solució: obre-la amb Read. Mira també `errades.js` (el solucionari en té). Si no pots veure
   la imatge, no endevinis l'enunciat pel títol: digues-ho i marca l'esborrany com a «sense verificar».
2. **Mira les pistes veïnes**: les de la mateixa tasca (`tasques.js`) i les d'exercicis del mateix tipus. Si l'alumne ja
   ha vist la família, remet-hi («Fes el mateix que a l'exercici 30») i dona menys guia; el primer cop, més.
3. Decideix el **tipus** (plantilles de sota), el **concepte clau** i el **parany** on s'equivoca l'alumne de 2n de
   Batxillerat.

### Calibratge (mesurat a les 55 pistes del professor)

- ~300 caràcters visibles (mediana 315; normal 220–380; mai més de 610) i **3 línies** (`<br>`): 2–4 en 3 de cada 4.
- Frases de ~19 paraules. Gairebé mai `;` (la IA n'abusava 7 vegades més). Un parèntesi d'aclariment per pista. Mai
  guió llarg «—».
- 78 % porten `<i>`; 42 % porten una `<b>` (gairebé sempre una de sola); 22 % una llista «- »; 16 % un «Atenció:»;
  13 % una línia en blanc abans del tancament; **15 % una pregunta** (gairebé sempre «Saps per què…?»); 7 % remeten a un
  altre exercici. No ho forcis a totes.
- Llengua: «has de / hauràs de» (4 de cada 10 pistes), futur que anticipa el que veurà l'alumne, «Per tant», «En primer
  lloc… Després… Finalment / Per acabar», «En total, hauràs d'obtenir…». Mai «o sigui que».

### Estructura i plantilles

**Obertura** (situa l'exercici o dona el primer pas) → **cos** (1–3 passos o casos, cadascun amb el perquè) →
**tancament opcional** («Atenció:», «Saps per què…?» o «Per acabar, …»). Un pas o un cas per línia, mai tota
l'estratègia en un paràgraf. En un exercici de diversos apartats, una línia per apartat amb `<i>a)</i>`.

Models reals (text tal com es veu, amb les etiquetes):

- **Trobar paràmetres amb condicions** (`u7/40`, `u9/30`, `u9/70`): compta les equacions, llista condició → equació,
  tanca amb el sistema. El segon cop, l'alumne les escriu:
  `Fes el mateix que a l'exercici 30: en total, hauràs d'obtenir <b>tres</b> equacions, una per cada condició. Aquest cop les has d'escriure tu:<br>- Passar per l'origen vol dir que el punt <i>(0, 0)</i> és de la gràfica.<br>- Un punt d'inflexió és on canvia la curvatura, i això només pot passar on s'anul·la la derivada segona.<br>- El pendent de la tangent en un punt és el valor de la derivada en aquell punt.<br><br>Per acabar, hauràs de resoldre el sistema d'equacions que en surti.`
- **Casos o candidats** (`u9/34`, `u7/46`, `u7/92`):
  `Com que la funció és <b>definida a trossos</b>, els candidats a màxim i mínim són de tres tipus:<br>- Dins de cada tros: resol <i>f ′(x) = 0</i> amb la derivada d'aquell tros i comprova que la solució cau dins d'aquell tros.<br>- El punt on canvia la definició: la derivada hi pot no existir, i per això resoldre <i>f ′(x) = 0</i> no te'l donaria.<br>- Els extrems de l'interval.<br><br>Calcula la imatge <i>f(x)</i> de tots els candidats i compara-les.`
- **Funció a trossos** (`u7/88`):
  `La funció és <b>definida a trossos</b>.<br>A <i>x</i> = −1 i a <i>x</i> = 3, calcula per separat el límit amb l'expressió que val a l'esquerra del punt i el límit amb la que val a la dreta.<br>Per a <i>x</i> → +∞, fixa't només en el tros de la definició que val quan <i>x</i> pren valors tant grans com vulguem.`
- **Llegir una gràfica** (`u7/44`, `u9/41`):
  `Estudia, per a cada gràfica, dos límits per separat: quan (x → +∞) i quan (x → −∞).<br>Has d'observar si la corba s'apropa a una alçada fixa (llavors tenim una asímptota horitzontal), o bé puja o baixa sense parar, o bé no s'estabilitza.<br><b>Atenció</b>: no fa falta calcular res, només cal llegir el dibuix.`
- **Optimització** (`u9/77`, `u9/79`, `u9/86`, `u9/87`): variables → què vols fer màxim/mínim → el lligam que n'elimina una →
  deriva → comprova que és màxim/mínim. Dibuixar el full és el primer pas a `u9/79`.
  `Anomena <i>x</i> i <i>y</i> els catets. El que vols fer màxim és l'àrea, <i>x·y/2</i>, però té dues variables. El teorema de Pitàgores lliga els catets amb la hipotenusa de 8 cm, i això et permet eliminar-ne una.<br>Si no vols derivar amb una arrel, pots treballar amb el quadrat de l'àrea: saps per què té el màxim al mateix lloc que l'àrea?`
- **«Inventa un exemple» o teoria** (`u9/44`, `u7/47`, `u9/39`, `u9/66`): un sol exemple concret i l'alumne generalitza; o
  casos particulars (recta, paràbola) abans del cas general:
  `Una manera senzilla és pensar amb un polinomi de segon grau, perquè la seva gràfica és una paràbola i en el vèrtex és on hi ha el màxim relatiu, o bé el mínim relatiu.<br>Per exemple, la paràbola <i>f(x) = (x − 3)²</i> té el vèrtex a <i>x = 3</i>, i és un mínim.<br>A partir d'aquí, pensa quins exemples pots posar.`
- **Diversos apartats de càlcul rutinari** (`u8/97`, `u8/93`): una frase per apartat, nomenant la regla.
  `<i>a)</i> Aplica la regla de la cadena.<br><i>b)</i> Aplica la regla de la cadena <b>dues vegades</b>.<br><i>c)</i> Aplica la definició de derivada d'un quocient de funcions.<br><i>d)</i> En algun moment, apareixerà un <i>ln 2</i>.`
- **Pista mínima** quan l'alumne ja sap el mètode (`u9/42`, `u7/48`): una o dues línies. No és obligatori omplir.

### Els cinc moviments que el fan seu

1. **Estructura visible.** Passos i casos en línies separades; connectors «En primer lloc», «Després», «Finalment»,
   «Per acabar». Si hi ha una confusió freqüent, es neutralitza al començament (`u9/41`: «La gràfica que et donen és la
   de la derivada, no la de *f*»).
2. **Diu el perquè i anomena el concepte.** Una regla no va sola: «en un punt que no sigui del domini la funció no pot
   ser contínua perquè la imatge d'aquell punt no existeix» (`u7/93`). Diu «teorema de Bolzano», «funció auxiliar
   *h(x)*», «indeterminació 0/0», «(per bisecció)», «límits laterals», no una paràfrasi procedimental.
3. **Concret.** Un exemple o unes dades en lloc d'una descripció: «*log(3)* existeix, però *log(−3)* i *log(0)* no»
   (`u7/102`); «comprova que *f(−3)* i *f(−2)* tenen signes diferents» (`u7/114`). Digues l'objectiu tal com el demana
   l'enunciat («fins que la longitud de l'interval sigui 1/2 o inferior»).
4. **Deixa un forat a l'alumne.** No li dona el pas final: li deixa pensar el perquè. Tanca de tant en tant amb una
   pregunta de **comprensió**, mai de càlcul («Saps per què?», «Entens el motiu?», «realment creus que pot tenir alguna
   arrel positiva?»). Si la pregunta demanaria un càlcul, mostra el patró (1; 0,5; 0,25; 0,125…) i pregunta pel motiu.
   Un fet que cal recordar (el domini d'una arrel) s'afirma; la pregunta es reserva per al raonament.
5. **Anticipa el parany i llegeix l'enunciat.** «<b>Atenció</b>:» per al cas subtil (després de `<br><br>`);
   «L'enunciat et demana "els punts", en plural»; «no només *x* = 2»; «no fa falta calcular res». «Curiositat:» per a
   una observació opcional.

### Llengua

Tu, amable i directe, sense afalacs. De vegades «sabem / tenim» per modelar un raonament («Sabem que el punt *P* és
damunt de la corba…»). Lèxic seu: «damunt», «tros» (de funció a trossos), «a banda i banda», «cap amunt», «a la llarga»,
«l'eix d'abscisses», «obtenir», «deduir», «comprovar». Precisió: «el límit no és finit» (no «és infinit»: pot ser −∞ o
+∞); −∞ i +∞ per separat (no «±∞»); «polinomi» (expressió) i «una exponencial i una polinòmica» (tipus de funció);
«tant grans com vulguem».

**Marcadors d'IA que cal evitar** (els de la primera versió): tota l'estratègia en un paràgraf amb `;` i `:`; «o sigui
que», «mitja feina», «el guió de sempre», «t'estalvia», «n'hi ha prou», «val la pena que notis»; imperatius secs en
cadena («Comença per…, escriu…, busca…»); donar la regla ja resolta sense el perquè («si surt negatiu és un màxim»);
frases de cloenda que repeteixen; guió llarg; cometes dobles `"…"` (fes servir «…»).

### Format tècnic

- HTML (`innerHTML` a `tasca.html`): **només `<i>`, `<b>` i `<br>`**. Cap altre `<` enganxat a una lletra (fa desaparèixer
  text); una desigualtat porta espai: `f ″(a) < 0`. No es pinten fórmules `$...$`: tot en text pla amb Unicode
  (`−`, `·`, `×`, `²`, `√`, `ℝ`, `∞`, `→`, `≥`, `≤`). Derivades amb `′` i `″` (no calen escapar).
- Una pista és **una sola línia** de `hints.js` (cap salt de línia real); `<br>` separa. Llista: «- » al començament de cada
  ítem; si la precedeix una frase, acaba amb dos punts.
- `<i>` per a l'**expressió matemàtica sencera** (`<i>f ′(x) = 0</i>`, `<i>x = 2</i>`, `<i>(x, x²)</i>`), no per a nombres que
  compten o numeren («4 punts», «grau 2», «longitud 2», «exercici 40»).
- `<b>`: 0 o 1 per pista. Només per a l'etiqueta «Atenció» / «Curiositat», el **terme tècnic** la primera vegada
  (<b>indeterminació</b>, <b>definida a trossos</b>, <b>evitable</b>) o la quantitat o qualificatiu que no es pot perdre
  (<b>tres</b> equacions, <b>sempre</b> creixent, <b>no és finit</b>). Mai per decorar.
- Guionet i signe menys «−»: indistints, no els corregeixis.

### Revisió abans d'entregar

Relegeix cada pista i respon: (1) he tret la frase que només repeteix o resumeix? (2) cada regla porta el perquè?
(3) hi ha una dada o un exemple concret? (4) l'alumne ha de pensar alguna cosa, o li ho he donat tot? (5) he anomenat
el concepte? (6) hi ha cap resultat numèric del problema? (7) **la matemàtica és correcta** i la pista porta cap al
camí de la solució del llibre? (8) format: etiquetes tancades, cap `<` estrany, una sola línia. L'«Editor de pistes»
avisa de (8). Les pistes del professor poden tenir descuits («superiro», «fixart-te», «mínim negatiu» per «mínim
relatiu»): són errades, no estil. No les copiïs.

### Qui toca què

- Les pistes del professor (**`u7`, `u8`, `u9`**) **no es reescriuen** si ell no ho demana. Les altres unitats es
  reescriuran en aquest estil quan ho demani, en l'ordre de `tasques.js`.
- **Flux de treball.** El professor edita amb l'artifact privat «Editor de pistes»
  (https://claude.ai/artifact/NzczJWtYP2uPButkugF6pB), que parteix de `hints.js`, i copia el fitxer sencer cap a
  GitHub. Si Claude proposa pistes, les deixa com a **esborranys a la base de dades de l'artifact** (eina `ArtifactData`,
  col·lecció `hints`, document `uN_número`, camps `key` i `text`, text sense salts de línia reals) perquè ell les revisi.
  No les posa a `hints.js` si no li ho demana. Abans de sobreescriure un esborrany, comprova que el document encara és
  la versió de Claude (si el professor l'ha tocat, no el trepitgis). Si no pot escriure a l'artifact, entrega les
  pistes com a línies `'uN/n': '…',` en un bloc de codi.
- Quan el professor retoca els esborranys, Claude compara la seva versió amb la final i actualitza aquest apartat.

## Errades del solucionari

- Viuen a `errades.js`: una llista d'errades per exercici. El format és a la capçalera
  del fitxer i al `README.md`.
- El text s'escriu entre accents greus amb `TEX` al davant, i les fórmules entre `$...$`
  (LaTeX). No s'hi pot posar cap accent greu ni la parella `${`.
- Es veuen a `tasca.html`: etiqueta al costat del botó *Veure solució* a la llista de la tasca
  (les errades d'enunciat, senceres) i targetes «On diu / Ha de dir» abans de la imatge.
- El camp `marca` de cada errada diu on és dins la imatge (imatge i rectangle en tant per cent).
  Es calcula amb l'eina `tasca.html?tot=1&marca=1` (`marca.js`). Una marca mal posada és pitjor
  que cap marca: s'ha de comprovar sempre a la imatge ampliada.
- Amb `ERRADES_PEGATS = true`, una errada amb `pegat` no s'anuncia: la imatge ja es veu corregida.
  Les imatges originals no es toquen mai. Els pegats no es fan a mà.
- Després de tocar el fitxer, obrir `tasca.html?tot=1#u7/s3` i comprovar que cap fórmula
  surt en vermell (KaTeX pinta en vermell el que no entén).
