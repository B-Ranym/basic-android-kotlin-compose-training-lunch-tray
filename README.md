Lunch Tray Practice Problem - Solution Code
==================================


## Overview
Lunch Tray is a food ordering application built with Jetpack Compose that demonstrates navigation between multiple screens. The app allows users to select meal items from various categories and complete an order.

## Features
- Multi-screen navigation using Jetpack Compose Navigation
- Order flow through different food categories
- Order summary and checkout
- Back navigation support

## Screens
The app contains five main screens:
1. **Start Screen** - Entry point for the application
2. **Entree Selection** - Choose main dish items
3. **Side Dish Selection** - Choose side dish items
4. **Accompaniment Selection** - Choose accompaniment items
5. **Checkout Screen** - Review order and complete payment

## Implementation Details

### Navigation Architecture
- Uses Compose Navigation with a custom NavController wrapper
- Implements enum-based route management for type safety
- Maintains current screen state for UI updates

### Key Components

#### LunchTrayScreen Enum
```kotlin
enum class LunchTrayScreen(@StringRes val title: Int) {
    Start(title = R.string.app_name),
    Entree(title = R.string.choose_entree),
    SideDish(title = R.string.choose_side_dish),
    Accompaniment(title = R.string.choose_accompaniment),
    Checkout(title = R.string.order_checkout)
}
```

#### Navigation Controller
```kotlin
class LunchTrayNavController(
    val navController: NavHostController
) {
    var currentScreen by mutableStateOf<LunchTrayScreen>(LunchTrayScreen.Start)
        private set
    
    fun navigateTo(destination: LunchTrayScreen) {
        currentScreen = destination
        navController.navigate(destination.name)
    }
    
    fun navigateBack() {
        navController.popBackStack()
        navController.currentBackStackEntry?.destination?.route?.let { route ->
            LunchTrayScreen.values().find { it.name == route }?.let {
                currentScreen = it
            }
        }
    }
}
```


## Project Structure
- **ui/** - Contains UI components and screens
  - **LunchTrayScreen.kt** - Enum class for screen routes
  - **LunchTrayNavController.kt** - Custom navigation controller
  - **screens/** - Individual screen composables
- **model/** - Data models for menu items and order
- **data/** - Repository and data sources

## Technologies Used
- Kotlin
- Jetpack Compose
- Compose Navigation
- ViewModel
- StateFlow

