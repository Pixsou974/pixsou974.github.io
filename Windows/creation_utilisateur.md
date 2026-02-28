# Creation Utilisateur avec Powershell

```powershell
# Configuration des chemins
$CSVFile = "C:\utilisateurs.csv"
$BaseOU = "OU=Utilisateurs,DC=MULTIVERSE,DC=LOCAL"

# Importation des données avec le bon délimiteur
$CSVData = Import-CSV -Path $CSVFile -Delimiter ";" -Encoding UTF8

foreach($Utilisateur in $CSVData){

    # Nettoyage des données (supprime les espaces inutiles)
    $Prenom = $Utilisateur.Prenom.Trim()
    $Nom = $Utilisateur.Nom.Trim()
    $NomOU = $Utilisateur.OU.Trim()

    # Construction des identifiants
    $UtilisateurLogin = ($Prenom.Substring(0,1) + "." + $Nom).ToLower()
    $UtilisateurEmail = "$UtilisateurLogin@multiverse.local"
    $UtilisateurMotDePasse = "P@ssword"

    # Définition du chemin de l'OU cible
    $TargetOU = "OU=$NomOU,$BaseOU"

    # --- 1. CRÉATION DE L'OU SI ELLE N'EXISTE PAS ---
    if (-not (Get-ADOrganizationalUnit -Filter "DistinguishedName -eq '$TargetOU'")) {
        Write-Host "Création de l'OU : $NomOU" -ForegroundColor Cyan
        New-ADOrganizationalUnit -Name $NomOU -Path $BaseOU
    }

    # --- 2. CRÉATION DE L'UTILISATEUR ---
    if (Get-ADUser -Filter "SamAccountName -eq '$UtilisateurLogin'") {
        Write-Warning "L'identifiant $UtilisateurLogin existe déjà dans l'AD"
    }
    else {
        # Utilisation du Splatting pour éviter les erreurs de syntaxe (backticks `)
        $UserParams = @{
            Name                  = "$Nom $Prenom"
            DisplayName           = "$Nom $Prenom"
            GivenName             = $Prenom
            Surname               = $Nom
            SamAccountName        = $UtilisateurLogin
            UserPrincipalName     = "$UtilisateurLogin@multiverse.local"
            EmailAddress          = $UtilisateurEmail
            Path                  = $TargetOU
            AccountPassword       = (ConvertTo-SecureString $UtilisateurMotDePasse -AsPlainText -Force)
            ChangePasswordAtLogon = $false
            Enabled               = $true
        }

        New-ADUser @UserParams
        Write-Host "Utilisateur créé : $UtilisateurLogin dans l'OU $NomOU" -ForegroundColor Green
    }
}
```
