# ShopeeFood Android App

A modern food delivery Android application built with Material Design principles and following Android best practices.

## Features

- Browse restaurants and their menus
- View restaurant details and ratings
- Add items to cart
- Manage cart items (add, remove, update quantity)
- Checkout process
- User profile management

## Technical Details

### Architecture
- MVVM architecture pattern
- Single Activity with multiple Fragments
- Repository pattern for data management
- Singleton pattern for cart management

### Libraries Used
- AndroidX and Material Design Components
- Navigation Component for fragment management
- Glide for image loading
- Retrofit for network operations
- Room for local database
- CircleImageView for circular profile images
- ViewBinding for view access

### Key Components

#### Activities
- `MainActivity`: Main container with bottom navigation
- `RestaurantDetailActivity`: Restaurant details and menu
- `CheckoutActivity`: Order checkout process

#### Fragments
- `HomeFragment`: Restaurant listings and featured items
- `CartFragment`: Shopping cart management
- `ProfileFragment`: User profile and settings

#### Models
- `Restaurant`: Restaurant data model
- `MenuItem`: Menu item data model
- `CartItem`: Cart item data model
- `Cart`: Singleton cart manager

#### Adapters
- `RestaurantAdapter`: Restaurant list adapter
- `MenuItemAdapter`: Menu items adapter
- `CartAdapter`: Cart items adapter

### Setup Instructions

1. Clone the repository
2. Open the project in Android Studio
3. Sync Gradle files
4. Run the app on an emulator or physical device

### Requirements

- Android Studio Arctic Fox or newer
- Minimum SDK: 24 (Android 7.0)
- Target SDK: 33 (Android 13)
- Java 8

### Building and Running

```bash
# Clone the repository
git clone https://github.com/yourusername/shopeefood.git

# Open in Android Studio
# Wait for Gradle sync to complete
# Run the app
```

## Project Structure

```
app/
├── src/
│   ├── main/
│   │   ├── java/com/shopeefood/
│   │   │   ├── activities/
│   │   │   ├── adapters/
│   │   │   ├── fragments/
│   │   │   └── models/
│   │   └── res/
│   │       ├── drawable/
│   │       ├── layout/
│   │       ├── menu/
│   │       ├── values/
│   │       └── xml/
│   └── test/
└── build.gradle
```

## Future Enhancements

- User authentication
- Payment gateway integration
- Real-time order tracking
- Push notifications
- Restaurant reviews and ratings
- Order history
- Favorite restaurants
- Address management
- Multiple language support

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.
