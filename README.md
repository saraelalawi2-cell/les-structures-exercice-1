   #include <stdio.h>
   #include <stdlib.h>
   #include <math.h>

/* Définition de la structure Point
   Un point contient deux coordonnées entières : x et y */
typedef struct {
    int x;
    int y;
} Point;

/* Fonction pour saisir un point
   Elle demande à l'utilisateur de saisir x et y */
Point SaisirPoint() {
    Point p;
   printf("Entrer x : ");
   scanf("%d", &p.x); 
   printf("Entrer y : ");
   scanf("%d", &p.y); 
   return p;
}

/* Fonction pour afficher un point
   Le point est affiché sous la forme (x,y) */
void AfficherPoint(Point p) {
    printf("(%d,%d)\n", p.x, p.y);
}

/* Fonction pour calculer la distance (passage par valeur)
   On utilise la formule : sqrt(x^2 + y^2) */
float Distance(Point p) {
    return sqrt(p.x * p.x + p.y * p.y);
}

/* Fonction pour calculer la distance (passage par adresse)
   On utilise un pointeur et l'opérateur -> */
float DistancePtr(Point *p) {
    return sqrt(p->x * p->x + p->y * p->y);
}

/* Fonction pour trier un tableau de points
   Tri à bulles selon la distance à l'origine */
void TrierPoints(Point tab[], int n) {
    int i, j;
    Point temp;

   for(i = 0; i < n - 1; i++) {
        for(j = 0; j < n - i - 1; j++) {
            if (Distance(tab[j]) > Distance(tab[j + 1])) {
                temp = tab[j];
                tab[j] = tab[j + 1];
                tab[j + 1] = temp;
            }
        }
    }
}

int main() {
    int n, i;

   /* Demande du nombre de points */
    printf("Donner le nombre de points : ");
    scanf("%d", &n);

 /* Allocation dynamique du tableau */
    Point *tab = (Point*) malloc(n * sizeof(Point));

 /* Vérification si l'allocation a réussi */
    if (tab == NULL) {
        printf("Erreur d'allocation mémoire\n");
        return 1;
    }

   /* Saisie des points */
    for(i = 0; i < n; i++) {
        printf("\nPoint %d :\n", i + 1);
        tab[i] = SaisirPoint();
    }

 /* Affichage des points */
    printf("\nListe des points :\n");
    for(i = 0; i < n; i++) {
        AfficherPoint(tab[i]);
    }

   /* Affichage des distances */
    printf("\nDistances des points :\n");
    for(i = 0; i < n; i++) {
        printf("Distance du point %d = %.2f\n", i + 1, Distance(tab[i]));
    }

   /* Tri des points */
    TrierPoints(tab, n);

   /* Affichage après tri */
    printf("\nPoints après tri :\n");
    for(i = 0; i < n; i++) {
        AfficherPoint(tab[i]);
    }

    /* Libération de la mémoire */
    free(tab);

    return 0;
}
