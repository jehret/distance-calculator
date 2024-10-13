# Challenge : Refactoriser un Calculateur de Distances - Pureté des Méthodes

## Dates : du 13/10/24 au 20/10/24

## Difficulté : facile

## Technologies cibles : 
- Java 17+ (ou Kotlin)

## Description
Ce challenge a pour but de vous familiariser avec le concept de **pureté des méthodes**. 
Une méthode pure :
1. **Ne modifie pas d’état** externe ou de variable partagée.
2. **Produit toujours le même résultat** pour les mêmes paramètres.
3. Est **facilement testable** de manière isolée.


## Objectif
Vous allez partir d’un code existant qui calcule la distance totale d’un trajet composé de plusieurs points géographiques, puis le refactorer pour introduire des méthodes **pures** et structurer le code en plusieurs classes. 

Ci-dessous un code qui calcule la distance totale d’un trajet en kilomètres en utilisant la formule de Haversine. Ce code est actuellement tout-en-un, et il n’est ni modulaire ni facilement testable. L’objectif est de refactoriser ce code en le rendant plus structuré et en introduisant des méthodes pures.

### Code de départ

Voici le code de départ dans une méthode `main`. Ce code n'est ni modulaire ni facilement testable, car toutes les opérations sont regroupées dans une seule méthode :

```java
import java.util.ArrayList;
import java.util.List;

public class DistanceCalculatorMain {

    public static void main(String[] args) {
        // Définir les points pour le trajet
        List<double[]> points = new ArrayList<>();
        points.add(new double[]{48.8566, 2.3522}); // Paris
        points.add(new double[]{51.5074, -0.1278}); // Londres
        points.add(new double[]{40.7128, -74.0060}); // New York
        points.add(new double[]{34.0522, -118.2437}); // Los Angeles

        // Calcul de la distance totale
        double totalDistance = 0;
        for (int i = 0; i < points.size() - 1; i++) {
            double lat1 = points.get(i)[0];
            double lon1 = points.get(i)[1];
            double lat2 = points.get(i + 1)[0];
            double lon2 = points.get(i + 1)[1];

            // Formule de Haversine pour calculer la distance entre deux points
            double earthRadius = 6371; // rayon de la Terre en kilomètres
            double dLat = Math.toRadians(lat2 - lat1);
            double dLon = Math.toRadians(lon2 - lon1);
            double a = Math.sin(dLat / 2) * Math.sin(dLat / 2) +
                       Math.cos(Math.toRadians(lat1)) * Math.cos(Math.toRadians(lat2)) *
                       Math.sin(dLon / 2) * Math.sin(dLon / 2);
            double c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
            double distance = earthRadius * c;

            totalDistance += distance;
        }

        // Affichage du résultat
        System.out.println("La distance totale du trajet est de : " + totalDistance + " km");
    }
}
```

## Exigences

Votre mission est de transformer ce code en un ensemble de classes distinctes, avec des méthodes **pures** pour permettre une meilleure testabilité et un code plus modulaire. Voici quelques classes que vous pourriez implémenter :

1. **Point** : Une classe pour représenter un point géographique, contenant les informations nécessaires pour décrire un emplacement sur la Terre.

2. **DistanceCalculator** : Une classe responsable des calculs de distance entre deux points géographiques. Elle doit être conçue pour effectuer ce calcul indépendamment de l’état externe.

3. **JourneyManager** : Une classe qui gère un trajet composé de plusieurs points et utilise la classe `DistanceCalculator` pour calculer la distance totale d’un trajet.

Vous êtes libres d’implémenter les classes et les méthodes que vous voulez, les propositions ci-dessus sont des suggestions. Assurez-vous cependant que chaque méthode soit **pure** et qu’elle fonctionne de manière autonome.

Attention : Vous aurez probablement des classes qui dépendent d’autres, comme par exemple `JourneyManager` et `DistanceCalculator`. Pour obtenir un maximum de points à ce challenge, vous devrez trouvez une solution pour que les méthode restent pures, mais dans ces cas là.

## Bonus (Pour aller plus loin)

- Créez les classes de test unitaires permettant de couvrir le maximum de cas (couverture de test)
- Un court résumé expliquant comment les méthodes pures facilitent la testabilité, et comment vous avez résolu le problème de la pureté des méthodes lorsque des classes dépendent d’autres classes.

## Critères d'évaluation

- Proportion de méthodes pures
- Code fonctionnel
- Bonus 1 : Couverture de test
- Bonus 2 : Résumé explicatif

## Livraison

- Code source sur un dépôt GitHub public
- Copie du lien GitHub sur le canal reponse-challenges
- Durée recommandée : 1-3 heures

N'hésitez pas à poser vos questions sur le Discord de la communauté si vous avez besoin d'éclaircissements. Bon courage à tous les participants !

## Récompenses
- Vainqueur : 5 pts
- 2ème : 3 pts
- 3ème : 1 pts

Rappel: Les participants accumulent des points en fonction de leur performance dans les challenges. Ces points peuvent être convertis en cartes cadeaux Prezzy, utilisables pour des achats en ligne ou en magasin dans n'importe quelle devise.
