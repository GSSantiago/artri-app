# Artriapp

Um app para artrite reumatoide com features criadas pelos alunos da matéria de Desenvolvimento Móvel ministrada pelo professor André Takeshi Endo em 2026/1:
 
Gabriel Henrique Rodrigues - 813345

Guilherme de Souza Santiago - 790847

Lucas Gabriel Velloso - 790771

***Link do drive com os videos de teste do aplicativo***:
https://drive.google.com/drive/folders/1hDrBeuAMP-_Bc8H98vv5iU8yZBkcIsEz?usp=sharing

## Table of contents

- [Getting started](#getting-started)
- [Project architecture](#project-architecture)
- [Additional information](#additional-information)

# Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)

For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.

## Setup the environment

### 1. Backend

O app depende do [backend](https://github.com/artri-app/artri-app-api) rodando (localmente via Docker ou já publicado). Siga o `README` daquele repositório para subir a API. Por padrão ela escuta em `http://localhost:8000`.

### 2. Instalar dependências do Flutter

```bash
flutter pub get
```

### 3. Configurar o `.env`

O projeto usa um arquivo `.env` (baseado no `.env_example`) para configurar a URL da API:

```
API_URL="http://<host>:8000/api"
```

O valor de `<host>` depende de onde você vai rodar o app:

| Onde roda o app | Valor do `<host>` |
|---|---|
| Emulador Android | `10.0.2.2` |
| Dispositivo físico via USB | `localhost`,  mas antes rode `adb reverse tcp:8000 tcp:8000` (redireciona a porta do celular para a porta 8000 da sua máquina) |
| Dispositivo físico via Wi-Fi | o IP da sua máquina na rede local (ex: `192.168.x.x`) |
| Web / Desktop | `localhost` |

### 4. Configurar a chave de API do Google Maps

A feature de exercícios ao ar livre usa o `google_maps_flutter`, que precisa de uma chave de API do Google Maps (Google Cloud Console → APIs & Services → Credentials, com a "Maps SDK for Android" habilitada).

Essa chave **não é versionada**, cada dev precisa adicioná-la no seu `android/local.properties`:

```
MAPS_API_KEY=sua_chave_aqui
```

Sem essa linha, o app builda normalmente, mas o mapa da tela "Ao ar livre" aparece em branco/cinza.

### 5. Rodar o app

Com um emulador aberto ou dispositivo conectado:

```bash
flutter run
```

# Project architecture

This project will follow the concepts of MVC architecture pattern, so the current project use this following organization:

```bash
lib/
│
├── models/                      # Data models representing the business logic entities
│   └── <model_name>.dart        # Example model
│
├── views/                       # UI screens and widgets
│   ├── widgets                  # Shared widgets with views
│   │   └── <widget>.dart
│   └── <view-name>              # View folder
│       ├── widgets              # Widgets used only on the page
│       │   └── <widget>.dart
│       └── <view-name>.dart
│
├── view_models/                 # Business logic controllers
│   └── <view_model_name>.dart
│
├── blocs/                       # Business logic components (For BLoC pattern)
│   └── <bloc_name>.dart
│
├── services/                    # Services like API or database management
│   └── <service_name>.dart      # Service for network calls
│
├── utils/                       # Utility functions and constants
│   ├── constants.dart           # Application constants
│   └── utils.dart               # Utility functions
│
├── routes/                      # Routes
│   ├── index.dart               # Export all routes
│   └── <route_name>.routes.dart # Route for each usage
│
└── main.dart                    # Entry point of the app
```

# Additional information

The bellow information is additional, but can help you to understand how flutter works and has some insights about best practices on the flutter framework.

- [The architecture of flutter](https://docs.flutter.dev/resources/architectural-overview#building-widgets)
- [Best practices of flutter](https://www.mindinventory.com/blog/flutter-development-best-practices/)
- [Widgets design](https://docs.flutter.dev/ui/widgets)

## Go Router navigation

The project use the library [GoRouter](https://pub.dev/packages/go_router) to make the navigation more easy. Below has a description about routing methods:

- `context.go()`: Will push a new page to the page stack. Use this to maintain the page stack.
- `context.go()`: Replace the page stack with the page using a new page key.
