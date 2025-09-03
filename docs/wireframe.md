# Wireframes (mobile-first)

## 1) Rec list with “Get it near me”
+-----------------------------+
|  Today’s suggestions        |
|  [ Hydrating congee 15m ]   |
|  • gentle carbs • sodium    |
|  [Get it near me] [Save]    |
|-----------------------------|
|  [ Electrolyte smoothie 5m ]|
|  • fluids • potassium       |
|  [Get it near me] [Save]    |
+-----------------------------+

## 2) MapView (with filters)
+-----------------------------+
| ← Hydrating congee          |
| [Map] [List]                |
| [ Open now ][ Halal ] [▼1km]|
| [ Delivery ][ Cuisine ▾ ]   |
|       ○   ○ ○               |
|    ○  ○  ●(3)  ○            |
|   ○   • You                 |
|   [ Search this area ]      |
+-----------------------------+
(• cluster; ○ single pin; You = user location)

## 3) PlaceSheet (pin tapped)
+-----------------------------+
| [Place name] ★4.3  $$  650m |
| [Halal] [Chinese]           |
| Why it matches              |
|  ✓ Gentle soups, electrolyte|
|    drinks available         |
|                             |
| [Directions] [Order] [Save] |
|                             |
| Hours: 10:00–22:00          |
| Address, phone              |
| ⓘ External venue; verify... |
+-----------------------------+

## 4) PlaceList (accessibility-first)
+-----------------------------+
| ← Hydrating congee          |
| [List] [Map]                |
| Filters: Open now • Halal   |
|-----------------------------|
| 1. Place name  ★4.3  $$ 650m|
|    [Directions] [Order]     |
|    Badges: Halal, Chinese   |
|-----------------------------|
| 2. Grocery Mart  ★4.0  $ 1.2km
|    [Directions]            |
|    Badges: Ingredients ok  |
+-----------------------------+

## 5) LocationPermissionPrompt
+-----------------------------+
| See nearby options?         |
| Use approximate location to |
| show places.                |
| [Use once] [Allow always]   |
| [Enter area manually]       |
+-----------------------------+
