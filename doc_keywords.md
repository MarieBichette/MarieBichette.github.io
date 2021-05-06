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

### initial-velocity
