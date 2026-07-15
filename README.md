# Artriapp

Um app para artrite reumatoide com features criadas pelos alunos da matéria de Desenvolvimento Móvel ministrada pelo professor André Takeshi Endo em 2026/1:
 
Gabriel Henrique Rodrigues - 
Guilherme de Souza Santiago - 790847
Lucas Gabriel Velloso - 790771

Link do drive com os videos de teste do aplicativo:
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

This project use `.env` file for communication with APIs. Make sure your `.env` file is set before start the project and following the `.env_example` file.

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
