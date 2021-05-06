# Time-management

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

# Geometry

## section
Section de la barre
Type : Real

## initial-interface-position
Position de l'interface entre la cible et le projectile.
Doit correspondre à la position d'un noeud du maillage.
Paramètre non obligatoire si la cible et le projectile ne sont pas définis.
Type : Real


# Matter

## projectile | target | " "
Si plusieurs matériaux, on spécifie le comportement de chacun à l'intérieur de ces balises.
Si un seul matériau, pas besoin de <projectile> ou <target>, on peut renseigner directement les propriétés du matériau sous la balise <matter>

## initialisation
Données relatives à l'initialisation du matériau

### initial-velocity
Vitesse initiale du matériau (en m/s).
Tye : Real

### init-thermo
Chemin vers le fichier de données contenant les champs thermodynamiques initiaux (à t=0) de la matière.
Ce fichier contient les pression, température, densité et énergie interne (massique) du matériau.
Type : String

## equation-of-state
Données relatives à l'équation d'état définissant le comportement volumique du matériau

### name
Choix du type de l'équation d'état.
Seule l'équation de Mie Gruneisen est possible pour le moment.
Type : String
```
<name>mie-gruneisen</name>
```
### coefficients
Chemin vers le fichier contenant les coefficients du matériau pour l'équation de Mie Grüneisen
Type : String
