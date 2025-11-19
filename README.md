# AppsBunches Integration Requirements for Third-Party Services (Zid Merchants)

This document is a guideline for third-party providers who want to integrate their services into apps built using Apps Bunches Mobile App for Zid merchants.

### Notes To Consider

* Coordinating with the Partnerships Team regarding the collaboration agreement.
* The application must include more than 20 merchants from Apps Bunches’ clients using the app, and this does not represent any direct confirmation of support.

---

## 1. Introduction

Apps Bunches Mobile App is a mobile layer for Zid merchants that allows third-party services to integrate their apps via a **Flutter SDK**.
The SDK communicates with Zid APIs and integrates services seamlessly into the mobile app experience without modifying core functionalities.

---

## 2. Business Cycle Requirements

### App Information

* Full description of the app and its features
* App URL in Zid Apps Market
* Support email and official website (if available)

### Media & Demonstration

* Introductory video explaining the app's service
* Clear indication of where the service should appear in the mobile app (e.g., product page, checkout, order success page)

### User Stories

* User story describing how the service works on the Zid web store
* User story describing how the service should work on Apps Bunches mobile app

#### Examples

**Chatbot SDK:**
Open the app → Home page → Click on SDK chat icon

**Upselling SDK:**
Open the app → Cart page → Upselling bottom sheet appears automatically → User adds product to cart

**Loyalty Program SDK:**
Open the app → Home page → Points widget should appear
Open the app → Account page → Points widget should appear

---

## 3. Technical Requirements

### 3.1 Flutter SDK Development

* Developers must build a **Flutter SDK**
* SDK must include **full usage documentation**
* SDK must be published on **pub.dev**
* SDK must support the latest **Flutter stable version**

### 3.2 Initialization & Configuration

* SDK must accept initial configuration values in **JSON**
* SDK must support **sandbox mode** for testing
* Sensitive data must be **encrypted**
* Example JSON received from Zid API:

```json
{
  "app_key": "XXXX",
  "status": true,
  "sandbox": false,
  "primary_color": "#FF6600",
  "store_id": "12345",
  "token": "ABCDEF123456",
  "config": {
    "show_button": true,
    "widget_position": "home_page"
  }
}
```

### 3.3 SDK Lifecycle

1. App fetches JSON configuration from Zid API on launch
2. Pass JSON to third-party SDK via init method
3. SDK configures itself based on JSON
4. SDK should handle:

   * Page route tracking
   * Cart updates
   * Store changes

### 3.4 Integration with Zid APIs

* `GET /api/v1/scripts`
* `GET /api/v2/catalog/stores/$storeId/layout-setting`

JSON includes:

* App status
* Tokens & IDs
* Colors
* Any required configuration

### 3.5 Initialization Example

```dart
APPSDKNAME.init(initialJson: {
  'status': true,
  'token': '123456890',
})
.onSuccess((value) => print(value))
.onCatchError((e) => print(e));
```

---

## 4. Optional SDK Features

### 4.1 Page Listener

```dart
APPSDKNAME.trackPageRoute(pageName: "wishlist");
```

### 4.2 Cart Events (CRUD)

```dart
APPSDKNAME.sendEvent(
  cartEvent: CartEvents(
    onAddToCart: (itemCartId) {},
    onDeleteToCart: (itemCartId) {},
  ),
);
```

### 4.3 UI Widgets

```dart
Column(
  children: [
    OrderSuccessHeaderWidget(orderId: widget.orderId),
    OrderDetailsButtonWidget(orderId: widget.orderId),
    APPSDKNAME.orderDetailsWidget(),
    SizedBox(height: 30),
    TransferPaymentWidget(orderId: widget.orderId),
    SizedBox(height: 30),
    VatInfoWidget(),
  ],
);
```

### 4.4 Search Events

```dart
List<Products> products = await APPSDKNAME.getProducts(q: 'Search Item');
```

### 4.5 Abandoned Cart Events

```dart
APPSDKNAME.addCartUpdates(
  deviceId: '123456789',
  customerObject: {},
  cartObject: {},
  phase: 'add_to_cart',
);
```

### 4.6 Customer Support Widgets

```dart
floatingActionButton: APPSDKNAME.showFloatingActionButton();
```

### 4.7 Cashback / Exchange / Return Events

```dart
APPSDKNAME.showWidgets();

APPSDKNAME.return(
  mobileNumber: '+966666',
  userID: '',
  orderModel: {},
);
```

You can also develop any type of widgets and functions needed to showcase your services.

---

## 5. Quality Standards

* SDK must not crash the app
* SDK must not request extra permissions unnecessarily
* SDK must be lightweight and optimized
* SDK must not interfere with Core App functionality
* SDK should provide graceful error handling

---

## 6. Targeted App Categories

* Customer Support Apps
* Marketing Apps
* Operations Apps
* Other Service Apps

---

## 7. Notes

All examples are illustrative and may be modified based on service requirements.

---

### Contact Emails

* **Partnership Email:** [Partnership@appsbunches.com](mailto:Partnership@appsbunches.com)
* **Support & Development Email:** [Dev@appsbunches.com](mailto:Dev@appsbunches.com)

---

## About AppsBunches

(عناقيد التطبيقات)
Technology company specializing in:

* Mobile app development
* E-commerce solutions
* System integrations
* Zoho customization
* Digital transformation
