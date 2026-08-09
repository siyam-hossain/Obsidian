## Dart Project Folder Structure

A typical Dart project follows a simple and organized folder structure:

```text
project_name/
│
├── bin/
│   └── project_name.dart     # Main entry point
│
├── lib/
│   └── src/                  # Application source code
│
├── test/
│   └── project_name_test.dart # Unit tests
│
├── pubspec.yaml              # Project metadata & dependencies
├── pubspec.lock              # Locked dependency versions
└── README.md                 # Project documentation
```

### Key Folders & Files

| Path           | Purpose                                           |
| -------------- | ------------------------------------------------- |
| `bin/`         | Contains executable Dart programs                 |
| `lib/`         | Contains reusable application/library code        |
| `lib/src/`     | Internal implementation code                      |
| `test/`        | Contains unit and integration tests               |
| `pubspec.yaml` | Defines dependencies, project name, version, etc. |
| `pubspec.lock` | Records exact dependency versions                 |
| `README.md`    | Provides project documentation                    |

> **Note:** For larger Dart applications, `lib/` can be further organized into folders such as `models/`, `services/`, `repositories/`, and `utils/`.
