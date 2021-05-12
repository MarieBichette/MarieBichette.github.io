# time-management

## final-time

Temps final de calcul en secondes. 

Type : Real

## initial-time-step

Pas de temps initial en secondes.

Type : Real

## constant-time-step
Si vrai : le pas de temps est constant au long du calcul.

Si faux, il est calculé à partir de la condition CFL.

Type : Boolean ("true" / "false")

# geometry

## section

Section de la barre

Type : Real

## initial-interface-position

Position de l'interface entre la cible et le projectile.

Doit correspondre à la position d'un noeud du maillage.

Paramètre non obligatoire si la cible et le projectile ne sont pas définis.

Type : Real.


# matter

## projectile | target | " "

Si plusieurs matériaux, on spécifie le comportement de chacun à l'intérieur de ces balises.

Si un seul matériau, pas besoin de ``<projectile>`` ou ``<target>``, on peut renseigner directement les propriétés du matériau sous la balise ``<matter>``.

### initialisation

Données relatives à l'initialisation du matériau

#### initial-velocity

Vitesse initiale du matériau (en m/s).

Tye : Real

#### init-thermo

Chemin vers le fichier de données contenant les champs thermodynamiques initiaux (à t=0) de la matière.

Ce fichier contient les pression, température, densité et énergie interne (massique) du matériau.

Type : String

### equation-of-state

Données relatives à l'équation d'état définissant le comportement volumique du matériau

#### name
Choix du type de l'équation d'état.

Seule l'équation de Mie Gruneisen est possible pour le moment.

Type : String
```
<name>mie-gruneisen</name>
```

#### coefficients

Chemin vers le fichier contenant les coefficients du matériau pour l'équation de Mie Grüneisen

Type : String

### rheology

Données relatives à la loi de comportement définissant le comportement élasto-plastique du matériau

#### coefficients

Chemin vers le fichier contenant les propriétés d'élastoplasticité du matériau 

Type : String

#### elasticity-model

Choix du type de loi d'élasticité

Seul le modèle l'élasticité linéaire est possible pour le moment 

Type : String

```
"elasticity-model": "linear"
```

#### plasticity-model

Choix du type de loi de modèle de plasticité

Seul le modèle de plasticité EPP (Elastique Parfaitemetn Plastique) est possible pour le moment 

Type : String

```
"plasticity-model": "EPP"
```

#### plasticity-criterion

Choix du critère de plasticité

Seul le critère de plasticité de Von Mises est possible pour le moment 

Type : String

```
"plasticity-criterion": "VonMises"
```

### failure

Données relatives aux propriétés d'endommagement et de rupture du matériau

#### porosity-model

Données relatives aux modèles d'endommagement avec une évolution de porosité

##### name

Choix du modèle d'endommagement avec évolution de porosité. 

Seul le modèle JohnsonModel est disponible pour le moment

Type : String

```
"name" : "JohnsonModel"
```

##### coefficients

Définition de l'ensemble des coefficients du modèle de Johnson

###### initial-porosity

Porosité initiale du modèle de Johnson

Type : Real

###### effective-strength

Contrainte effective du modèle de Johnson

Type : Real

###### viscosity

Viscosité du modèle de Johnson

Type : Real

#### failure-criterion

Choix du critère déclenchant le modèle de rupture

##### name

Nom du critère déclenchant le modèle de rupture

Type : String

Choix possibles : 
- "MinimumPressure"
- "Damage"
- "Porosity"
- "HalfRodComparison"
- "MaximalStress"

Tous ces modèles attendent une valeur comme paramètre.

##### value

Valeur du seuil déclenchant la rupture

Type : Real

##### index      

Index de la cellule où déclencher la rupture pour le critère HalfRodComparison

Type : Integer

#### failure-treatment

Choix du modèle de rupture

##### name

Nom du modèle de rupture

Type : String

Choix possibles : 
- "ImposedPressure" : on impose la pression à une valeur indiquée dans les mailles rompues

Champ obligatoire : "value"

- "Enrichment" : on enrichit les mailles rompues

Champ obligatoire : "value", "lump-mass-matrix"

##### lump-mass-matrix

Choix de la condensation de la matrice de masse dans le cas d'un traitement de type Enrichment

Type : String

Choix possibles : 
- "somme"
- "menouillard"
                  
##### value

Valeur imposée dans la maille rompue

Type : Real

#### cohesive-model

Choix du modèle de loi cohésive

##### name

Nom du modèle de loi cohésive 

Type : String

Choix possibles :
- "linear" : Champs obligatoires : "cohesive-strength", "critical-separation"
- "bilinear" : Champs obligatoires : "cohesive-strength", "critical-separation", "separation-at-point-1", "stress-at-point-1"
- "trilinear" : Champs obligatoires : "cohesive-strength", "critical-separation", "separation-at-point-1", "stress-at-point-1", "separation-at-point-2", "stress-at-point-2"

##### coefficients

Définition de l'ensemble des paramètres de la loi cohésive

###### cohesive-strength

Valeur de la contrainte caractéristique pour les lois cohesives

Type : Real

###### critical-separation

Valeur de la distance limite pour les lois cohésives

Type : Real

###### separation-at-point-1

Valeur de la distance limite à la première rupture de pente dans la loi cohésive pour les lois bilinear ou trilinear

Type : Real

###### stress-at-point-1

Valeur de la contrainte à la première rupture de pente dans la loi cohésive pour les lois bilinear ou trilinear

Type : Real

###### separation-at-point-2

Valeur de la distance limite à la deuxième rupture de pente dans la loi cohésive pour la loi trilinear

Type : Real

###### stress-at-point-2

Valeur de la contrainte à la deuxième rupture de pente dans la loi cohésive pour la loi trilinear

Type : Real

##### unloading-model

Nom du modèle de décharge

Type : String

Choix possibles : 
- "lossofstiffnessunloading" pour une décharge élastique
- "progressiveunloading" pour une décharge plastique. Champs requis : "slope"

##### slope

Valeur de la pente pour la décharge plastique

Type : Real
 
#### contact-treatment

Choix du modèle de contact

##### name
Nom du modèle de contact

Type : String 

Choix possibles : 
- "penalty" contact avec pénalisation
- "lagrangianmultiplier" contact avec multiplicateur de Lagrange

##### penalty-stiffness

Raideur de la pénalité pour le contact de type penalty

Type : Real

# boundary-conditions

## left-boundary | right-boundary

Surface dont les conditions aux limites seront caractérisées

### type

Choix du type de conditions aux limites

Type : String

Choix possibles : 
- "pressure"
- "velocity"

### bc-law

Choix de la forme de la conditions aux limites

Type : String

Choix possibles : 
- "constant" ; Champ obligatoire : "value"
- "twostep" ; Champs obligatoires : "value1", "value2", "time-activation"
- "ramp" ; Champs obligatoires : "value1", "value2", "time-activation1",  "time-activation2"
- "marchtable" ; Champ obligatoire : "value"
- "creneauramp" ; Champs obligatoires : "initial-value", "plateau-value", "start-first-ramp-time", "reach-value2-time"

#### value

Valeur pour la condition aux limites "constant"

Nom du fichier pour la condition aux limites "marchtable"

Type :
- Real pour la condition aux limites "constant"
- String pour la condition aux limites "marchtable"

#### value1

Première valeur pour la condition aux limites "twostep" ou "ramp"

Type : Real

#### value2

Deuxième valeur pour la condition aux limites "twostep" ou "ramp"

Type : Real

#### time-activation

Temps d'activation de la deuxième valeur pour la condition aux limites "twostep"

Type : Real

#### time-activation-value-1

Temps d'activation de la première valeur pour la condition aux limites "ramp"

Type : Real

#### time-activation-value-2

Temps d'activation de la deuxième valeur pour la condition aux limites "ramp"

Type : Real

#### initial-value

Valeur initiale pour la condition aux limites "creneauramp"

Type : Real

#### plateau-value

Valeur du premier plateau pour la condition aux limites "creneauramp"

Type : Real

#### start-first-ramp-time

Temps de début de la transition de la valeur initiale à la valeur finale  pour la condition aux limites "creneauramp"

Type : Real

#### reach-value2-time

Temps de la fin de la transition de la valeur initiale à la valeur finale pour la condition aux limites "creneauramp"

Type : Real

#### start-second-ramp-time

Temps de début de la deuxième transition du plateau à la valeur finale pour la condition aux limites "creneauramp"

Type : Real

#### reach-value3-time

Temps de la fin de la transition du plateau à la valeur finale pour la condition aux limites "creneauramp"

Type : Real

#### end-value

Valeur du plateau final pour la condition aux limites "creneauramp"  pour la condition aux limites "creneauramp"

Type : Real


# numeric-parameters

## linear-pseudo

Valeur du paramètre linéaire de la pseudo

Type: Real

## quadratic-pseudo

Valeur du paramètre quadratique de la pseudo

Type: Real

## cfl

Valeud de la cfl

Type : Real

## cfl-pseudo

Valeud de la cfl pseudo

Type : Real

# output

## number-of-images

Nombre d'images dans la simulation

Type : Integer

## database

Liste des propriétés des sorties demandées

### path

Nom du fichier de sorties

Type : string

### iteration-period

Nombre d'iterations du calcul entre chaque sorties

Type: integer

### time-period

Durée entre chaque sorties

Type : Real

## variables

Liste des varibles de sorties

Choix possibles: 
- All 
- choix de plusieurs variables parmi la liste suivante: "ArtificialViscosity",
 "CellSize", "CohesiveForce", "Density", "DeviatoricStress", "DiscontinuityOpening", "EquivalentPlasticStrainRate", "InternalEnergy", "NodeVelocity", "NodeCoordinates", "PlasticStrainRate", "Porosity", "Pressure", "ShearModulus", "SoundVelocity", "Stress", "YieldStress"

