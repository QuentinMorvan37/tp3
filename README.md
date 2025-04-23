
# TP3 – Projet collaboratif Java : Marché de crypto-monnaies

## Objectifs

- Travailler en équipe avec GitHub
- Gérer un dépôt collaboratif
- Implémenter un marché de crypto-monnaies en Java
- Gérer les fonctionnalités via des branches Git

---

## Étape 1 : Initialisation du dépôt GitHub

### Athos :
1. Créer un nouveau dépôt **tp3** sur GitHub (dépôt personnel).
2. Aller dans **Settings > Manage access > Invite a collaborator**.
3. Inviter **Porthos** (demander son identifiant GitHub).

### Porthos :
1. Accepter l’invitation par e-mail.
2. Cloner le dépôt :

```bash
git clone git@github.com:<athos_username>/tp3.git
```

---

## Étape 2 : Copier les fichiers du TP2

### Porthos :
1. Copier `README.md` et `src/Cryptomonnaie.java` du TP2 vers TP3 (ne pas copier `.git`).
2. Commit et push.

### Athos :
1. Faire un `git pull` pour récupérer les fichiers.

---

## Étape 3 : Implémentation du projet Java

### Fichiers à ajouter :
- `Portefeuille.java`
- `CryptoMarche.java`
- `TestCryptoMarche.java`

```bash
git add src/*
git commit -m "Ajout des fichiers du marché"
git push
```

### Compilation & exécution :
```bash
javac -d bin src/*.java
java -cp bin TestCryptoMarche
```

---

## Étape 4 : Compléter les classes

### Porthos – Portefeuille.java

```java
public boolean transfertDevise (Portefeuille destination, double montantJetons) {
    if (!this.monnaie.equals(destination.monnaie)) return false;
    if (this.nbJetons < montantJetons) return false;
    this.nbJetons -= montantJetons;
    destination.nbJetons += montantJetons;
    return true;
}

public boolean achatDevise (double montantEuros) {
    if (montantEuros < 0) return false;
    double nbAchat = montantEuros / monnaie.getValeurEuro();
    this.nbJetons += nbAchat;
    return true;
}
```

### Athos – CryptoMarche.java

```java
public double capitalEnEuros(String proprietaire) {
    double total = 0;
    for (Portefeuille p : marche) {
        if (p.getProprietaire().equals(proprietaire)) {
            total += p.getNbJetons() * p.getMonnaie().getValeurEuro();
        }
    }
    return total;
}

public double capitalMonneaie(Cryptomonnaie monnaie) {
    double total = 0;
    for (Portefeuille p : marche) {
        if (p.getMonnaie().equals(monnaie)) {
            total += p.getNbJetons() * monnaie.getValeurEuro();
        }
    }
    return total;
}
```

---

## Étape 5 : Tests

```bash
javac -d bin src/*.java
java -cp bin TestCryptoMarche
```

Attendu : tous les tests en OK.

---

## Étape 6 : Branches Git et monnaies personnalisées

1. Créer une branche :
```bash
git checkout -b AthosCoin
```

2. Ajouter une crypto :
```java
public class AthosCoin extends Cryptomonnaie {
    public AthosCoin() {
        super("ATH", 500);
    }
}
```

3. Commit, push et merge :
```bash
git add src/AthosCoin.java
git commit -m "Ajout de AthosCoin"
git checkout main
git merge AthosCoin
git push
```

4. Répéter pour PorthosCoin

---

## Fin du TP
Tout est à jour, synchronisé, et testé.
