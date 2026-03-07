# Ubax Platform - Monorepo

Architecture complète de la plateforme Ubax avec trois composants principaux.

## Structure du Projet

```
ubax-project/
├── ubax-platform/    # Backend - Spring Boot
├── ubax-web/         # Frontend - Angular
└── ubax-mobile/      # Mobile - Flutter
```

## Pour les Développeurs

### 1. Cloner le repository
```bash
git clone <ubax-project-url>
cd ubax-project
```

### 2. Backend (Spring Boot)
```bash
cd ubax-platform
mvn clean install
mvn spring-boot:run
```

### 3. Frontend (Angular)
```bash
cd ubax-web
npm install
ng serve
# Accessible à http://localhost:4200
```

### 4. Mobile (Flutter)
```bash
cd ubax-mobile
flutter pub get
flutter run
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
