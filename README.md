# Ubax Platform - Monorepo avec Submodules

Architecture complète de la plateforme Ubax avec trois composants principaux gérés comme submodules Git.

## Structure du Projet

```
ubax-project/
├── ubax-platform/    # Backend - Spring Boot (submodule)
├── ubax-web/         # Frontend - Angular (submodule)
├── ubax-mobile/      # Mobile - Flutter (submodule)
├── git-repos/        # Repositories centralisés
└── .gitmodules       # Configuration des submodules
```

## Pour les Développeurs

### Cloner tout le projet avec les submodules
```bash
git clone <ubax-project-url>
cd ubax-project
git submodule init          # Initialiser les submodules
git submodule update        # Télécharger les contenus
```

Ou en une seule commande :
```bash
git clone --recurse-submodules <ubax-project-url>
```

### Cloner un seul module (Backend, Frontend ou Mobile)
```bash
# Backend uniquement
git clone <chemin-vers-ubax-platform-repo>

# Frontend uniquement
git clone <chemin-vers-ubax-web-repo>

# Mobile uniquement
git clone <chemin-vers-ubax-mobile-repo>
```

### Backend (Spring Boot)
```bash
cd ubax-platform
mvn clean install
mvn spring-boot:run
```

### Frontend (Angular)
```bash
cd ubax-web
npm install
ng serve
# Accessible à http://localhost:4200
```

### Mobile (Flutter)
```bash
cd ubax-mobile
flutter pub get
flutter run
```

## Travailler avec les Submodules

### Mettre à jour tous les submodules
```bash
cd ubax-project
git submodule update --remote
```

### Mettre à jour un submodule spécifique
```bash
cd ubax-platform
git pull origin master
cd ..
git add ubax-platform
git commit -m "Update ubax-platform"
```

### Créer une nouvelle branche dans un submodule
```bash
cd ubax-platform
git checkout -b feature/your-feature
# Faire vos changements
git push origin feature/your-feature
cd ..
git add ubax-platform          # L'état du submodule change
git commit -m "Update ubax-platform"
```

## Requirements

- **Backend**: Java 21+, Maven 3.8+
- **Frontend**: Node.js 18+, Angular CLI
- **Mobile**: Flutter 3.41.4+, Dart 3.x+

## Configuration

Chaque projet contient sa propre configuration :
- `ubax-platform`: `application.yml`
- `ubax-web`: `environment.ts`, `angular.json`
- `ubax-mobile`: `pubspec.yaml`

## Support

Pour des questions ou des problèmes, consultez la documentation spécifique de chaque module.
