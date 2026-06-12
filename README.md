

### Requirements
| Requirement | Status |
|-------------|--------|
| Create Product List Screen | ✅ |
| Create Product Details Screen | ✅ |
| Pass product name to details | ✅ (via Constructor) |
| Return result from details | ✅ (via `Navigator.pop(result)`) |
| Show result in SnackBar | ✅ |

### Navigation Flow

```
ProductListScreen ──push()──> ProductDetailsScreen
       ↑                              │
       │                              │
       └──── pop('Added to favorites')┘
              ↓
       SnackBar shows "Added to favorites"
```

### Data Flow

#### 1️⃣ Forward Data Passing (Constructor)
```dart
// In ProductListScreen - passing data FORWARD
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => ProductDetailsScreen(
      productName: product['name']!,  // ← Data passed via constructor
    ),
  ),
);
```

#### 2️⃣ Backward Result Returning (await + pop)
```dart
// In ProductListScreen - receiving data BACKWARD
final result = await Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => ProductDetailsScreen(...)),
);

if (result != null) {
  ScaffoldMessenger.of(context).showSnackBar(
    SnackBar(content: Text('$result')),  // ← Shows "Added to favorites"
  );
}
```

#### 3️⃣ Returning Data from Details Screen
```dart
// In ProductDetailsScreen - sending result BACK
Navigator.pop(context, 'Added to favorites');  // ← Second argument is the result
```

---

## 🚀 How to Run

### Prerequisites
- Flutter SDK installed
- Android Studio / VS Code with Flutter extension
- Emulator or physical device

### Steps
```bash
# 1. Create new Flutter project
flutter create navigation_exercises
cd navigation_exercises

# 2. Replace lib/main.dart with the provided code

# 3. Run the app
flutter run
```

### Project Structure
```
navigation_exercises/
├── lib/
│   └── main.dart          # All exercises in one file
├── pubspec.yaml           # Dependencies
└── README.md              # This file
```

---

## 🗂️ Code Structure

| Widget | Exercise | Purpose |
|--------|----------|---------|
| `MyApp` | Both | Root widget, MaterialApp setup |
| `HomeScreen` | 01 | Starting screen with stack visualization |
| `DetailScreen` | 01 | Second screen with pop button |
| `ProductListScreen` | 02 | List of products, initiates data passing |
| `ProductDetailsScreen` | 02 | Shows product, returns favorite status |
| `_buildStackInfoCard` | Helper | Visual stack state display |

---

## 📚 Key Concepts Learned

### Navigator Methods
| Method | Purpose | Exercise |
|--------|---------|----------|
| `Navigator.push()` | Add screen to stack | 01 |
| `Navigator.pop()` | Remove screen from stack | 01 |
| `Navigator.pop(context, result)` | Remove + return data | 02 |

### Data Passing Patterns
| Direction | Method | Example |
|-----------|--------|---------|
| Forward | Constructor parameters | `ProductDetailsScreen(productName: "iPhone")` |
| Backward | `await` + `pop(result)` | `final result = await Navigator.push(...)` |

---

## 🎓 Stack Behavior Explanation (Detailed)

### What is the Navigation Stack?
The navigation stack is a **LIFO (Last In, First Out)** data structure:
- `push()` → Adds a new screen on **top**
- `pop()` → Removes the screen from **top**

### Visual Example
```
Step 1: App starts
┌─────────────────┐
│   HomeScreen    │  ← Only screen in stack
└─────────────────┘

Step 2: User taps "Go to Detail"
┌─────────────────┐
│  DetailScreen   │  ← Top (visible)
├─────────────────┤
│   HomeScreen    │  ← Bottom (hidden behind)
└─────────────────┘

Step 3: User taps "Go Back"
┌─────────────────┐
│   HomeScreen    │  ← Back to top, DetailScreen removed
└─────────────────┘
```

---

## ✅ Checklist

- [x] Exercise 01: Basic navigation works correctly
- [x] Exercise 02: Data passes forward via constructor
- [x] Exercise 02: Data returns backward via pop result
- [x] SnackBar displays returned message
- [x] Visual stack state shown on screens
- [x] Code is well-commented and documented

---


---

<div align="center">
  <b>🎯 عبدالرحمن شداد  🚀</b>
</div>
