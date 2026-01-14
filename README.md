# Lab-3

# --- OPÉRATIONS ARITHMÉTIQUES ---
a, b = 15, 4
print(f"{a} + {b} = {a + b}")          # Addition
print(f"{a} // {b} = {a // b}")        # Quotient entier (3)
print(f"{a} % {b} = {a % b}")          # Reste (modulo)
print(f"{a} ** {b} = {a ** b}")        # Puissance

# --- COMPARAISONS ---
x, y = 20, 15
print(f"\n{x} == {y} : {x == y}")      # False
print(f"{x} >= {y} : {x >= y}")        # True

# --- LOGIQUE BOOLÉENNE ---
age = 22
permis = True
casier_vierge = False

# Utilisation de AND, OR et NOT
peut_conduire = age >= 18 and permis
peut_louer = age >= 21 or (permis and casier_vierge)
sanction = not casier_vierge

print(f"\nPeut conduire : {peut_conduire}")
print(f"Peut louer voiture : {peut_louer}")

import sys

def calculer_prix():
    print("--- Système de Calcul de Réduction ---")
    
    # Étape 4.2 : Saisie et validation
    try:
        prix_initial = float(input("Prix du produit (€) : "))
        if prix_initial <= 0:
            print("Le prix doit être supérieur à 0.")
            return
    except ValueError:
        print("Saisie invalide pour le prix.")
        sys.exit(1)

    statut = input("Êtes-vous étudiant ? (o/n) : ").strip().lower()
    fid_saisie = input("Fidélité (en années) : ").strip()

    try:
        fidelite = int(fid_saisie)
    except ValueError:
        print("Saisie invalide pour la fidélité.")
        sys.exit(1)

    # Étape 4.1 : Application des règles
    reduction = 0.0

    # Règle 1 : Étudiant (-10%)
    if statut == 'o':
        reduction += prix_initial * 0.10
    
    # Règle 2 : Client fidèle >= 5 ans (-15%)
    if fidelite >= 5:
        reduction += prix_initial * 0.15
    
    # Règle 3 : Prix > 100€ (-5€ supplémentaire)
    if prix_initial > 100:
        reduction += 5.0

    # Calcul final
    prix_final = prix_initial - reduction

    # Sécurité : Le prix ne peut pas être inférieur à 0
    if prix_final < 0:
        prix_final = 0.0

    print("-" * 30)
    print(f"Réduction totale : {reduction:.2f} €")
    print(f"Prix final à payer : {prix_final:.2f} €")

if __name__ == "__main__":
    calculer_prix()

    def calcul_reduction_pure(prix, est_etudiant, annees_fid):
    """Fonction optimisée pour les tests unitaires."""
    remise = 0
    if est_etudiant: remise += prix * 0.10
    if annees_fid >= 5: remise += prix * 0.15
    if prix > 100: remise += 5
    
    resultat = prix - remise
    return max(0, resultat) # Utilise max() pour garantir un prix >= 0

# Test rapide (Scénario : Étudiant, 6 ans fidélité, prix 150€)
# Réduction : 15 (10%) + 22.5 (15%) + 5 = 42.5. Prix final = 107.5
print(f"\nTest unitaire : {calcul_reduction_pure(150, True, 6)} €")
